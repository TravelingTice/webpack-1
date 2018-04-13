# SETUP

1. Clone this repo into your file
2. Run `npm init -y && npm install --save-dev babel-core babel-loader babel-preset-es2015 clean-webpack-plugin css-loader file-loader html-webpack-plugin mini-css-extract-plugin node-sass sass-loader webpack webpack-cli webpack-dev-server` (alias = webpack1)
3. Add to  `package.json`:
```javascript
"scripts": {
  ...
  "start": "webpack-dev-server --open --mode development --display-error-details",
  "build": "webpack -p --display-error-details"
}
```
4. Add webpack.config.js file with this content:
```javascript
var path = require("path");
var MiniCssExtractPlugin = require('mini-css-extract-plugin');
var HtmlWebpackPlugin = require('html-webpack-plugin');
var CleanWebpackPlugin = require('clean-webpack-plugin');

var cssExtractPlugin = new MiniCssExtractPlugin({
  filename: 'main.css'
})

module.exports = {
  entry: "./scripts/main.js",
  output: {
    path: path.resolve(__dirname, "dist"),
    filename: "bundle.js",
    // publicPath: "/dist"
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        use: {
          loader: "babel-loader",
          options: { presets: ["es2015"] }
        }
      },
      {
        test: /\.scss$/,
        use: [MiniCssExtractPlugin.loader, 'css-loader', 'sass-loader']
      },
      {
        test: /\.html$/,
        use: ['html-loader']
      },
      {
        test: /\.(jpg|png)$/,
        use: [
          {
            loader: 'file-loader',
            options: {
              name: '[name].[ext]',
              outputPath: 'images/',
              publicPath: 'images/'
            }
          }
        ]
      }
    ]
  },
  plugins: [
    cssExtractPlugin,
    new HtmlWebpackPlugin({
      template: 'index.html'
    }),
    new CleanWebpackPlugin(['dist'])
  ]
};
```
5. Make some stuff!
