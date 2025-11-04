# Custom Webpack set up

## Minimal start version

```shell
mkdir build public src
touch public/index.html
mkdir src/styles src/util src/ui
touch src/index.ts src/App.tsx
npm init
npm i -D webpack webpack-cli webpack-dev-server @babel/core @babel/plugin-transform-react-jsx @babel/preset-env @babel/preset-react @types/node @types/react @types/react-dom babel-loader cross-env css-loader style-loader html-webpack-plugin ts-loader typescript
touch webpack.config.js tsconfig.json
```

tsconfig.json:

```json
{
  "compilerOptions": {
    "target": "es2020" /* Specify ECMAScript target version: 'ES3' (default), 'ES5', 'ES2015', 'ES2016', 'ES2017','ES2018', 'ES2019', 'ES2020' or 'ESNEXT'. */,
    "module": "esnext" /* Specify module code generation: 'none', 'commonjs', 'amd', 'system', 'umd', 'es2015', or 'ESNext'. */,
    "lib": [
      "esnext",
      "dom",
      "dom.iterable"
    ] /* Specify library files to be included in the compilation. */,
    "jsx": "react" /* Specify JSX code generation: 'preserve', 'react-native', or 'react'. */,
    "outDir": "build" /* Redirect output structure to the directory. */,
    "strict": true /* Enable all strict type-checking options. */,
    "allowSyntheticDefaultImports": true /* Allow default imports from modules with no default export. This does not affect code emit, just typechecking. */,
    "moduleResolution": "node" /* Specify module resolution strategy: 'node' (Node.js) or 'classic' (TypeScript pre-1.6). */
  },
  "exclude": ["coverage"],
  "include": ["src", "@types"]
}
```

## TypeSctipt start version

### Init

```bash
# Initialize project
npm init -y

# Install dependencies
npm install react react-dom
npm install -D webpack webpack-cli webpack-dev-server typescript ts-loader html-webpack-plugin css-loader style-loader sass-loader sass

# Create config files and start coding!
```

webpack.config.js:

```js
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

// setting up automatically in package.json start/build
//  commands via "cross-env" package
const isDevelopment = process.env.NODE_ENV === 'development';
const DEV_PORT = process.env.DEV_PORT || 4000;

// entry, output, mode, plugins, module, resolve, devServer
module.exports = {
  entry: './src/index.tsx',

  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'build'),
    clean: true,
  },

  mode: isDevelopment ? 'development' : 'production',

  plugins: [
    new HtmlWebpackPlugin({
      inject: true,
      template: path.resolve(__dirname, 'public', 'index.html'),
      minify: isDevelopment
        ? undefined
        : {
            removeComments: true,
            collapseWhitespace: true,
            removeRedundantAttributes: true,
            useShortDoctype: true,
            removeEmptyAttributes: true,
            removeStyleLinkTypeAttributes: true,
            keepClosingSlash: true,
            minifyJS: true,
            minifyCSS: true,
            minifyURLs: true,
          },
    }),
  ],

  module: {
    rules: [
      {
        test: /\.css$/i,
        use: ['style-loader', 'css-loader'],
      },
      {
        test: /\.(js|jsx)$/i,
        exclude: /node_modules/,
        use: ['babel-loader'],
      },
      {
        test: /\.(ts|tsx)$/i,
        use: [
          {
            loader: 'ts-loader',
            options: {
              transpileOnly: true,
            },
          },
        ],
      },
    ],
  },

  resolve: {
    extensions: ['.js', '.jsx', '.ts', '.tsx'],
  },

  devServer: {
    static: {
      directory: path.join(__dirname, 'build'),
    },
    port: DEV_PORT,
    hot: true,
    historyApiFallback: true,
  },
};
```

### package.json

```json
{
  "name": "react-typescript-webpack-2025",
  "version": "1.0.0",
  "type": "module",
  "scripts": {
    "dev": "webpack serve --mode development",
    "build": "webpack --mode production",
    "build:analyze": "webpack --mode production --env analyze"
  },
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0"
  },
  "devDependencies": {
    "@types/react": "^18.2.0",
    "@types/react-dom": "^18.2.0",
    "typescript": "^5.3.0",
    "webpack": "^5.89.0",
    "webpack-cli": "^5.1.4",
    "webpack-dev-server": "^4.15.1",
    "html-webpack-plugin": "^5.5.3",
    "ts-loader": "^9.5.1",
    "css-loader": "^6.8.1",
    "style-loader": "^3.3.3",
    "sass-loader": "^13.3.2",
    "sass": "^1.69.0",
    "file-loader": "^6.2.0",
    "url-loader": "^4.1.1",
    "webpack-bundle-analyzer": "^4.10.0"
  }
}
```

### Webpack configuration

```javascript
// webpack.config.js
import { fileURLToPath } from 'url';
import { dirname, resolve } from 'path';
import HtmlWebpackPlugin from 'html-webpack-plugin';
import { BundleAnalyzerPlugin } from 'webpack-bundle-analyzer';

const __dirname = dirname(fileURLToPath(import.meta.url));

export default (env, argv) => {
  const isProduction = argv.mode === 'production';
  const isDevelopment = !isProduction;

  return {
    target: 'browserslist', // Modern browser targeting
    entry: './src/index.tsx',
    
    output: {
      path: resolve(__dirname, 'dist'),
      filename: isProduction 
        ? 'static/js/[name].[contenthash:8].js'
        : 'static/js/[name].js',
      chunkFilename: isProduction
        ? 'static/js/[name].[contenthash:8].chunk.js'
        : 'static/js/[name].chunk.js',
      clean: true,
      publicPath: '/',
    },

    resolve: {
      extensions: ['.tsx', '.ts', '.js', '.jsx'],
      alias: {
        '@': resolve(__dirname, 'src'),
      },
    },

    module: {
      rules: [
        {
          test: /\.tsx?$/,
          use: 'ts-loader',
          exclude: /node_modules/,
        },
        {
          test: /\.css$/,
          use: [
            'style-loader',
            {
              loader: 'css-loader',
              options: {
                modules: {
                  auto: true,
                  localIdentName: isDevelopment
                    ? '[name]__[local]--[hash:base64:5]'
                    : '[hash:base64]',
                },
              },
            },
          ],
        },
        {
          test: /\.scss$/,
          use: [
            'style-loader',
            {
              loader: 'css-loader',
              options: {
                modules: {
                  auto: true,
                  localIdentName: isDevelopment
                    ? '[name]__[local]--[hash:base64:5]'
                    : '[hash:base64]',
                },
                importLoaders: 2,
              },
            },
            'sass-loader',
          ],
        },
        {
          test: /\.(png|jpe?g|gif|svg|webp)$/i,
          type: 'asset',
          parser: {
            dataUrlCondition: {
              maxSize: 8 * 1024, // 8kb
            },
          },
          generator: {
            filename: 'static/media/[name].[hash:8][ext]',
          },
        },
        {
          test: /\.(woff2?|eot|ttf|otf)$/i,
          type: 'asset/resource',
          generator: {
            filename: 'static/fonts/[name].[hash:8][ext]',
          },
        },
      ],
    },

    plugins: [
      new HtmlWebpackPlugin({
        template: './public/index.html',
        minify: isProduction,
      }),
      ...(env.analyze ? [new BundleAnalyzerPlugin()] : []),
    ],

    optimization: {
      minimize: isProduction,
      splitChunks: {
        chunks: 'all',
        cacheGroups: {
          vendor: {
            test: /[\\/]node_modules[\\/]/,
            name: 'vendors',
            chunks: 'all',
            priority: 10,
          },
          react: {
            test: /[\\/]node_modules[\\/](react|react-dom)[\\/]/,
            name: 'react',
            chunks: 'all',
            priority: 20,
          },
        },
      },
      runtimeChunk: 'single',
    },

    devServer: {
      port: 3000,
      open: true,
      hot: true,
      historyApiFallback: true,
      client: {
        overlay: {
          errors: true,
          warnings: false,
        },
      },
    },

    devtool: isDevelopment ? 'eval-source-map' : 'source-map',

    cache: {
      type: 'filesystem',
      buildDependencies: {
        config: [__filename],
      },
    },
  };
};
```

### tsconfig.json

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "lib": ["DOM", "DOM.Iterable", "ES6"],
    "allowJs": true,
    "skipLibCheck": true,
    "esModuleInterop": true,
    "allowSyntheticDefaultImports": true,
    "strict": true,
    "forceConsistentCasingInFileNames": true,
    "noFallthroughCasesInSwitch": true,
    "module": "ESNext",
    "moduleResolution": "bundler",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "react-jsx",
    "baseUrl": "src",
    "paths": {
      "@/*": ["*"]
    }
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "dist"]
}
```

### Browser list configuration

```json
{
  "browserslist": {
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  }
}
```

### React app

```tsx
// src/index.tsx
import { StrictMode } from 'react';
import { createRoot } from 'react-dom/client';
import App from './App';

const container = document.getElementById('root');
const root = createRoot(container!);

root.render(
  <StrictMode>
    <App />
  </StrictMode>
);
```

```tsx
// src/App.tsx
import { useState } from 'react';
import styles from './App.module.scss';

const App = () => {
  const [count, setCount] = useState(0);

  return (
    <div className={styles.container}>
      <h1>React + TypeScript + Webpack 2025</h1>
      <button onClick={() => setCount(count + 1)}>
        Count: {count}
      </button>
    </div>
  );
};

export default App;
```

## Key Modern Features:

1. ES Modules: Uses native ES modules in config
2. Asset Modules: Modern asset handling without extra loaders
3. Caching: Filesystem caching for faster builds
4. Code Splitting: Automatic vendor and runtime chunk splitting
5. Modern Browser Targeting: Uses browserslist for optimal bundles
6. TypeScript 5.x: Latest TypeScript with modern features
7. CSS Modules: Scoped CSS with hot reloading
