# cordova+vue开发 #（https://cordova.apache.org/）
## 1.开发环境 ##

### node ###

v8.11.2（https://nodejs.org/dist/latest-v8.x/）

### java ###

1.下载安装JDK
(http://www.oracle.com/technetwork/java/javase/downloads/index.html)  
2.设置JAVA_HOME环境变量，指定为JDK安装路径

### 安卓环境 ###

1.下载安装Android SDK(installer_r24.4.1-windows.exe)  
2.安装必要的API  
3.配置ANDROID_HOME环境变量，指定为Android SDK安装路径

## 2.安装Cordova构建App ##

1.npm install -g cordova  
2.cordova create appBuild  
3.添加浏览器平台 cordova platform add browser  
  添加安卓平台 cordova platform add android  
4.添加插件cordova plugin add xxx 
4.运行 cordova run browser  
5.真机/模拟器运行（android） cordova run android