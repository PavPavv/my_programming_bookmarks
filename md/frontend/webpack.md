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
