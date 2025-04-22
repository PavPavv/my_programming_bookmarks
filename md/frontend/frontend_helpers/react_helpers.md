# React helpers

## Add dynamic env variables to the Vite React TypeScript project

1. Create ".env" file in the root of the application
2. Create constants env getter helper function:

```typescript
const getEnvVar = (key: string): string => {
  if (import.meta.env.DEV) {
    return import.meta.env[key] || "";
  } else {
    const windowEnv = window._env_;
    if (windowEnv?.[key]) {
      return windowEnv[key];
    }
    return import.meta.env[key] || "";
  }
};
export const VITE_APP_BASE_API_URL_ENV = getEnvVar("VITE_APP_BASE_API_URL");
```

3. Declare global extended interface for "window" object in the global types of the application:

```typescript
declare global {
  interface Window {
    _env_: {
      [key: string]: string;
    };
  }
}
```

4. Add "env.sh" file to the root of the application:

```sh
#!/bin/bash

# Define paths
CONFIG_FILE="./public/env-config.js"
ENV_FILE=".env"

# Recreate config file
rm -rf $CONFIG_FILE
touch $CONFIG_FILE

# Add assignment 
echo "window._env_ = {" >> $CONFIG_FILE

# Read each line in .env file
while read -r line || [[ -n "$line" ]];
do
  # Skip comments and empty lines
  if [[ $line == \#* ]] || [[ -z $line ]]; then
    continue
  fi

  # Split env variables by character `=`
  if printf '%s\n' "$line" | grep -q -e '='; then
    varname=$(printf '%s\n' "$line" | sed -e 's/=.*//')
    varvalue=$(printf '%s\n' "$line" | sed -e 's/^[^=]*=//')
  fi

  # Read value of current variable if exists as Environment variable
  value=$(printf '%s\n' "${!varname}")
  # Otherwise use value from .env file
  [[ -z $value ]] && value=${varvalue}
  
  # Append configuration property to JS file
  echo "  $varname: \"$value\"," >> $CONFIG_FILE
done < $ENV_FILE

echo "}" >> $CONFIG_FILE
```

5. Add to "prepare" package.json script the following command to make shell script executable once and for all for this application on your machine ("prepare": *"chmod +x ./env.sh"* line):

```json
{
  "name": "example-front",
  "private": true,
  "version": "0.0.0",
  "type": "module",
  "scripts": {
    "prepare": "chmod +x ./env.sh",
    "dev": "./env.sh && vite",
    "build": "./env.sh && tsc -b && vite build",
    "lint": "eslint .",
    "preview": "vite preview"
  },
  "dependencies": {
    "@types/node": "^22.14.1",
    "classnames": "^2.5.1",
    "react": "^19.0.0",
    "react-dom": "^19.0.0"
  },
  "devDependencies": {
    "@eslint/js": "^9.22.0",
    "@types/react": "^19.0.10",
    "@types/react-dom": "^19.0.4",
    "@vitejs/plugin-react": "^4.3.4",
    "eslint": "^9.22.0",
    "eslint-plugin-react-hooks": "^5.2.0",
    "eslint-plugin-react-refresh": "^0.4.19",
    "globals": "^16.0.0",
    "typescript": "~5.7.2",
    "typescript-eslint": "^8.26.1",
    "vite": "^6.3.1",
    "vite-plugin-svgr": "^4.3.0"
  }
}
```

6. add **script** tag with src to generated file in index.html:

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <link rel="icon" type="image/svg+xml" href="/vite.svg" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Example</title>
    <!-- Add below -->
    <script src='/env-config.js'></script>
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="/src/main.tsx"></script>
  </body>
</html>
```

7. Run:

```bash
pnpm run prepare
pnpm run dev
```
