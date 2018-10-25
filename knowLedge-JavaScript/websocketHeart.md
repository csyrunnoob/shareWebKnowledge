在使用原生websocket的时候，如果设备网络断开，不会触发任何函数，前端程序无法得知当前连接已经断开。这个时候如果调用websocket.send方法，浏览器就会发现消息发不出去，便会立刻或者一定短时间后（不同浏览器或者浏览器版本可能表现不同）触发onclose函数。

后端websocket服务也可能出现异常，连接断开后前端也并没有收到通知，因此需要前端定时发送心跳消息ping，后端收到ping类型的消息，立马返回pong消息，告知前端连接正常。如果一定时间没收到pong消息，就说明连接不正常，前端便会执行重连。

为了解决以上两个问题，以前端作为主动方，定时发送ping消息，用于检测网络和前后端连接问题。一旦发现异常，前端持续执行重连逻辑，直到重连成功。
websocket-heartbeat-js基于浏览器js原生websocket封装，主要目的是保障客户端websocket与服务端连接状态。

用法：
```
npm install websocket-heartbeat-js

import WebsocketHeartbeatJs from 'websocket-heartbeat-js';
let websocketHeartbeatJs = new WebsocketHeartbeatJs({
    url: 'ws://xxxxxxx'
});
websocketHeartbeatJs.onopen = function () {
    console.log('connect success');
    websocketHeartbeatJs.send('hello server');
}
websocketHeartbeatJs.onmessage = function (e) {
    console.log(`onmessage: ${e.data}`);
}
websocketHeartbeatJs.onreconnect = function () {
    console.log('reconnecting...');
}

```
关于参数配置：
```
const options = {
    url: 'ws://xxxx',
    pingTimeout: 15000, 
    pongTimeout: 10000, 
    reconnectTimeout: 2000,
    pingMsg: "heartbeat"
}
let websocketHeartbeatJs = new WebsocketHeartbeatJs(options);

```
url : 必填  websocket服务端接口地址
pingTimeout ： 每隔15秒发送一次心跳，如果收到任何后端消息定时器将会重置
pongTimeout ：ping消息发送之后，10秒内没收到后端消息便会认为连接断开
reconnectTimeout ：尝试重连的间隔时间
pingMsg ：ping消息值