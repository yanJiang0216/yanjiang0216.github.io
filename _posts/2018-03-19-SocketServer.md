---
layout: post

title: "SocketServer模块"

categorys: Python
---



​        SocketServer 是标准库中一个高级模块（Python 3.x 中重命名为socketserver），它的目标是简化很多样板代码，它们是创建网络客户端和服务器所必需的代码。这个模块中有为你
创建的各种各样的类。

​        除了为你隐藏了实现细节之外，另一个不同之处是，我们现在使用类来编写应用程序。
因为以面向对象的方式处理事务有助于组织数据，以及逻辑性地将功能放在正确的地方。
你还会注意到，应用程序现在是事件驱动的，这意味着只有在系统中的事件发生时，它们
才会工作。

​        事件包括消息的发送和接收。事实上，你会看到类定义只包括一个用来接收客户端消息
的事件处理程序。所有其他的功能都来自使用的SocketServer 类。此外，GUI 编程也是事件驱动的。你会立即注意到它们的相似性，因为最后一行代码通常是一个服务器的无限循环，它等待并响应客户端的服务请求。它工作起来几乎与本章前面的基础TCP 服务器中的无限while 循环一样。

​         在原始服务器循环中，我们阻塞等待请求，当接收到请求时就对其提供服务，然后继续等待。在此处的服务器循环中，并非在服务器中创建代码，而是定义一个处理程序，这样当服务器接收到一个传入的请求时，服务器就可以调用你的函数。

创建SocketServer TCP服务器

```python
from socketserver import (TCPServer as TCP,StreamRequestHandler as SRH)
from time import ctime
HOST = ''
PORT = 21567
ADDR = (HOST,PORT)
class MyRequestHandler(SRH):
    def Handle(self):
        print("connected from:",self.client_address)
        self.wfile.write('[%s] %s' % （ctime(),self.rfile.readline()) )
tcpServ = TCP(ADDR,MyRequestHander)
print('waitting  for connection ...')
tcpServ.serve_forever()
```

创建SocketServer TCP客户端

```python
from socket import * 
HOST = 'localhost'
PORT = 21567
BUFSIZ = 1024
ADDR = (HOST,PORT)
while True:
    tcpCliSock = socket(AF_INET,SOCK_STREAM)
    tcpCliSock.connect(ADDR)
    data = raw_input('> ')
    if not data:
        break
    tcpcliSock.send('%s\r\n' % data)
    data = tcpCliSock.recv(BUFSIZ)
    if not data:
        break
    print(data.strip())
    tcpCliSock.close()
```

因为这里使用的程序类对待套接字通信就像文件一样，所以必须发送终止符（回车和换行符）。而服务器只是保留并重用这里发送的终止符。当得到从服务器返回的消息时，用strip()函数对其进行处理并使用由print声明自动提供的换行符。

