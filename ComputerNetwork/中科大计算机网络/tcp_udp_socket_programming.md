# TCP套接字编程

## Socket：

* SAP: 在应用层和传输层之间
* 应用层通过 Socket API 来调用传输层的服务

TCP: 可靠，字节流（不维护边界）
UDP: 不可靠，数据报

## TCP Socket Programming

TCP的Socket代表了四个值，是代表了会话关系的整数！

### 流程：

1. 服务器先运行
* 创建 welcome socket（一个整数）
* 将这个整数和本地ip、端口bind
* accept(): 接收来自其他人的连接
2. 客户端向服务器连接：
* 创建一个本地socket(隐式bind)
* connect()服务器的ip和port
3. 接受请求：
* accept()的阻塞解除，返回一个connection socket

### 数据结构：

#### sockaddr_in:
（放本地的ip地址和端口号）
```c
struct sockaddr_in{
    short sin_family;  // 地址簇
    u_short sin_port;  // port
    struct in_addr sin_addr;  // sin_addr: ip
    char sin_zero[8];  // 对齐
}
```

#### hostent:
```c
struct host_ent{
    char *h_name;   //主机域名
    char **h_aliases;   //主机的别名
    int h_addrtype;     
    int h_length;       //地址长度
    char ** h_addr_list;    
    #define h_addr h_addr_list[0];  //ip地址的列表
}
```

### 代码大致用法：
```
// Server first
welcomeSocket = Socket(...);
bind(welcomeSocket, &server_sad);  // sad is a sockaddr_in
connectSocket = accept(welcomeSocket, ...)

// Client
clientSocket = Socket(...);
// 客户端implicitly bind，不调用的话就自动给你bind
bind(clientSocket, &client_sad);
connect(clientSocket, server_sad);

//连接建立后，之前阻塞的accept()返回一个新的值，包括新socket，client和server的ip和port

sendto(clientSocket, ...);      // client
read(ConnectionSocket,...);     // server
write(ConnectionSocket, ...);   // server
```

### 代码实例

client.c:
```c
void main(){

}
```

server.c:
```c
void main(){
    
}
```
