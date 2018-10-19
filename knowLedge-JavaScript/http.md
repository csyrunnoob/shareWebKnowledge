HTTP是基于TCP/IP协议的应用层协议。它不涉及数据包（packet）传输，主要规定了客户端和服务器之间的通信格式，默认使用80端口。
    
    一、0.9版本

    最早版本是1991年发布的0.9版。该版本极其简单，只有一个命令GET。
    上面命令表示，TCP 连接（connection）建立后，客户端向服务器请求（request）网页index.html。
    协议规定，服务器只能回应HTML格式的字符串，不能回应别的格式。



    二、1.0版本

    1996年5月，HTTP/1.0 版本发布，内容大大增加。
    首先，任何格式的内容都可以发送。这使得互联网不仅可以传输文字，还能传输图像、视频、二进制文件。这为互联网的大发展奠定了基础。
    其次，除了GET命令，还引入了POST命令和HEAD命令，丰富了浏览器与服务器的互动手段。
    再次，HTTP请求和回应的格式也变了。除了数据部分，每次通信都必须包括头信息（HTTP header），用来描述一些元数据。
    其他的新增功能还包括状态码（status code）、多字符集支持、多部分发送（multi-part type）、权限（authorization）、缓存（cache）、内容编码（content encoding）等

    1.Content-Type
    关于字符的编码，1.0版规定，头信息必须是 ASCII 码，后面的数据可以是任何格式。因此，服务器回应的时候，必须告诉客户端，数据是什么格式，这就是Content-Type字段的作用。
    常见的Content-Type字段的值：text/plain,text/html,text/css,image/png,image/jpeg等等
    例如:Content-Type: text/html; charset=utf-8该类型表明，发送的是网页，而且编码是UTF-8。

    2.Content-Encoding
    由于发送的数据可以是任何格式，因此可以把数据压缩后再发送。Content-Encoding字段说明数据的压缩方法。
    Content-Encoding: gzip
    Content-Encoding: compress
    Content-Encoding: deflate
    客户端在请求时，用Accept-Encoding字段说明自己可以接受哪些压缩方法。Accept-Encoding: gzip, deflate

    HTTP/1.0 版的主要缺点是，每个TCP连接只能发送一个请求。发送数据完毕，连接就关闭，如果还要请求其他资源，就必须再新建一个连接。
    TCP连接的新建成本很高，因为需要客户端和服务器三次握手，并且开始时发送速率较慢（slow start）。所以，HTTP 1.0版本的性能比较差。随着网页加载的外部资源越来越多，这个问题就愈发突出了。
    为了解决这个问题，有些浏览器在请求时，用了一个非标准的Connection字段。

    3.Connection
    Connection: keep-alive。这个字段要求服务器不要关闭TCP连接，以便其他请求复用。服务器同样回应这个字段。
    一个可以复用的TCP连接就建立了，直到客户端或服务器主动关闭连接。但是，这不是标准字段，不同实现的行为可能不一致，因此不是根本的解决办法。



    三、http1.1版本

    1.1 版的最大变化，就是引入了持久连接（persistent connection），即TCP连接默认不关闭，可以被多个请求复用，不用声明Connection: keep-alive。
    客户端和服务器发现对方一段时间没有活动，就可以主动关闭连接。不过，规范的做法是，客户端在最后一个请求时，发送Connection: close，明确要求服务器关闭TCP连接。
    1.1 版还引入了管道机制（pipelining），即在同一个TCP连接里面，客户端可以同时发送多个请求。这样就进一步改进了HTTP协议的效率
    1.1版还新增了许多动词方法：PUT、PATCH、HEAD、 OPTIONS、DELETE。另外，客户端请求的头信息新增了Host字段，用来指定服务器的域名。

    1.Content-Length
    一个TCP连接现在可以传送多个回应，势必就要有一种机制，区分数据包是属于哪一个回应的。这就是Content-length字段的作用，声明本次回应的数据长度。

    HTTP/1.1缺点：虽然1.1版允许复用TCP连接，但是同一个TCP连接里面，所有的数据通信是按次序进行的。服务器只有处理完一个回应，才会进行下一个回应。要是前面的回应特别慢，后面就会有许多请求排队等着。这称为"队头堵塞"（Head-of-line blocking）。
    为了避免这个问题，只有两种方法：一是减少请求数，二是同时多开持久连接。这导致了很多的网页优化技巧，比如合并脚本和样式表、将图片嵌入CSS代码、域名分片（domain sharding）等等。如果HTTP协议设计得更好一些，这些额外的工作是可以避免的。




    四、http2.0


    HTTP/2 复用TCP连接，在一个连接里，客户端和浏览器都可以同时发送多个请求或回应，而且不用按照顺序一一对应，这样就避免了"队头堵塞"。
    HTTP/2 允许服务器未经请求，主动向客户端发送资源，这叫做服务器推送（server push）
    头信息压缩
    二进制协议
    数据流