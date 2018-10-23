跨平台最大的难点是设置环境变量（例如 NODE_ENV）。better-npm-run是一个很好的库来处理这个问题，特别是node项目。
用法下
```
"scripts": {
    "dev": "better-npm-run start-web",
    "node": "nodemon --exec better-npm-run start-node",
    "server": "concurrently \"npm run node\" \"npm run dev\""
  },
  "betterScripts": {
    "start-web": {
      "command": "webpack-dev-server --inline --progress --config build/webpack.dev.conf.js"
    },
    "start-node": {
      "command": "node ./server/app.js",
      "env": {
        "PORT": 3000
      }
    }
  },

```