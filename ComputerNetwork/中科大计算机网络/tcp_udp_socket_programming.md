# 2.8-2.9: TCP、UDP套接字编程

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
void main(int argc, char *argv[]){
    struct sockaddr_in sad;
    int clientSocket;
    struct hostent *ptrh;   // pointer to host table

    char Sentence[128];
    char modifiedSentence[128];

    host = argv[1]; port = atoi(argv[2]);

    clientSocket = socket(PF_INET, SOCK_STREAM, 0); // sock_stream代表用的是tcp socket, 因为tcp是byte stream
    memset((char*)&sad, 0, sizeof(sad));
    sad.sin_family = AF_INET;
    sad.sin_port = htons((u_short)port);
    ptrh = gethostbyname(host);
    memcpy(&sad.sin_addr, ptrh->h_addr, ptrh->h_length);
    connect(clientSocket, (struct sockaddr *)&sad, sizeof(sad));

    gets(Sentence); // get input stream from user
    n = write(clientSocket, Sentence, strlen(Sentence)+1);  // Send to server
    n = read(clientSocket, modifiedSentence, sizeof(modifiedSentence));
    printf("From Server: %s\n", modifiedSentence);
    close(clientSocket);
}
```

server.c:
```c
void main(int argc, char *argv[]){
    struct sockaddr_in sad;
    struct sockaddr_in cad; // client
    int welcomeSocket, connectionSocket;
    struct hostent *ptrh;

    char clientSentence[128];
    char modifiedSentence[128];

    port = atoi(argv[1]);

    welcomeSocket = socket(PF_INET, SOCK_STREAM, 0);
    memset((char*)&sad, 0, sizeof(sad));
    sad.sin_family = AF_INET;
    sad.sin_addr.s_addr = INADDR_ANY;   // set local IP
    sad.sin_port = htons((u_short)port);    // set port number
    bind(welcomeSocket, (struct sockaddr *)&sad, sizeof(sad));

    while(1){
        connectionSocket = accept(welcomeSocket, (struct sockaddr*)&cad, &alen);
        n = read(connectionSocket, clientSentence, sizeof(clientSentence));
        /*Do some modification to the sentence*/
        n = write(connectionSocket, modifiedSentence, strlen(modifiedSentence)+1);
        close(connectionSocket);
    }
}
```

## UDP套接字编程

没有握手，无连接服务

Socket只代表两种信息（本地ip和udp port），所以发送报文必须带有对方的ip和port

### 基本流程：

1. Server建立一个serverSocket
2. bind(socket, &sad)
3. readfrom(socket, ...) 等待client发东西
4. client建立clientSocket，和本地bind
5. client sendto(...)
6. server write reply to client

### 代码

#### client.c:
```c
void main(int argc, char *argv[]){
    struct sockaddr_in sad;
    int clientSocket;
    struct hostent *ptrh;

    char Sentence[128];
    char modifiedSentence[128];

    host = argv[1]; port = atoi(argv[2]);

    clientSocket = socket(PF_INET, SOCK_DRAM, 0);   // sock_dram代表用的是udp socket, 因为udp是datagram

    memset((char*)&sad, 0, sizeof(sad)); // 对SAD清零
    sad.sin_family = AF_INET;   // 地址簇
    sad.sin_port = htons((u_short)port);
    ptrh = gethostbyname(host);
    memcpy(&sad.sin_addr, ptrh->h_addr, ptrh->h_length);

    gets(Sentence);
    addr_en = sizeof(struct sockaddr);
    n = sendto(clientSocket, Sentence, strlen(Sentence)+1, (struct sockaddr*)&sad, addr_len);

    n = recvfrom(clientSocket, modifiedSentence, sizeof(modifiedSentence), (struct sockaddr*)&sad, &addr_len);

    close(clientSocket);
}
```

#### server.c:
```c
void main(int argc, char *argv[]){
    struct sockaddr_in sad;
    struct socketaddr_in cad;
    int serverSocket;
    struct hostent *ptrh;

    char Sentence[128];
    char modifiedSentence[128];

    port = atoi(argv[1]);

    serverSocket = socket(PF_INET, SOCK_DGRAM, 0);
    memset((char*)&sad, 0, sizeof(sad));
    sad.sin_family = AF_INET;
    sad.sin_addr.s_addr = INADDRR_ANY;
    sad.sin_port = htons((u_short)port);
    bind(serverSocket, (struct sockaddr*)&sad, sizeof(sad));

    while(1){
        n = recvfrom((serverSocket), clientSentence, sizeof(clientSentence), 0)
        /* Modify the sentence*/
        n = sendto(serverSocket, modifiedSentence, strlen(capitalizedSentence)+1, (struct sockaddr*)&cad, &addr_len);
    }
}
```