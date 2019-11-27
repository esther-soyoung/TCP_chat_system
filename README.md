# Multi-user TCP chatting system
## Author: Soyoung Kang  

# Introduction
This is a multi-user real time chatting application based on python language and its select module. I implemented the entire server side code and updated skeleton client code so that the program processes multiple users with a single server by multiplexing.  

# Flow Chart
![Image of FlowChart](https://github.com/esther-soyoung/TCP_chat_system/img/flowchart.png)  

# Snapshots
![Demo image1](https://github.com/esther-soyoung/TCP_chat_system/img/Picture1.png)  
![Demo image2](https://github.com/esther-soyoung/TCP_chat_system/img/Picture2.png)  
![Demo image3](https://github.com/esther-soyoung/TCP_chat_system/img/Picture3.png)  

# Line by line
## Server
![srv1](https://github.com/esther-soyoung/TCP_chat_system/img/code1.png)  
Firstly, create a welcome socket welcome_sock which sets address as command line argument.  
Then wait for clients using listen(), whilst making a list of connections called conn_list, initializing it to the welcome_sock.  

![srv2](https://github.com/esther-soyoung/TCP_chat_system/img/code2.png)  
While conn_list is not empty, call select.select() to take client sockets that are ready to connect. For each client socket in ready, create a connection socket conn_sock by calling accept() on welcome_sock if that is newly connecting socket. Add this newly connected conn_sock into conn_list so that the server can keep tabs on what it’s sending.  
Send the connection status including the total number of users online to both incoming client socket and the rest of connected client sockets, as well as printing on the server side terminal.  

![srv3](https://github.com/esther-soyoung/TCP_chat_system/img/code3.png)  
Otherwise if there already exists a connection socket for this socket in the loop, receive data from it. Make sure to propagate the received data to other clients online since this is a real time multi-user chat application.  

![srv4](https://github.com/esther-soyoung/TCP_chat_system/img/code4.png)  
Disconnect the connection if the client types in invalid message such as keyboard interruption or blank. Remove the connection socket from conn_list and close it.  

![srv5](https://github.com/esther-soyoung/TCP_chat_system/img/code5.png)  
Catch KeyboardInterrupt so that the program terminates with Ctrl+C. Close all the existing connection sockets and welcome_socket in this case.
