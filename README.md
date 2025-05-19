# AdvProg-Module10
Name : Siti Shofi Nadhifa <br>
NPM : 2306152172 <br>
Class : AdPro B

### 2.1. Original code of broadcast chat.
- Server
![server](/images/server.png)
- Client 1
![client-1](/images/client-1.png)
- Client 2
![client-2](/images/client-2.png)
- Client 3
![client-3](/images/client-3.png)
<br>
To run the server, execute `cargo run --bin server` on the console.
To run the client, execute `cargo run --bin client` on the console.
When the server is started, it begins listening for incoming connections on port 2000. Each time a client connects, the server prints a message such as "New connection from 127.0.0.1:(port)" to indicate a new connection has been established. On the client side, once connected, the message "From server: Welcome to chat! Type a message" is displayed, confirming that the client is successfully linked to the server. When a client sends a message (e.g., "client 1 check"), the server logs this with a print statement like "From client 127.0.0.1:64329 "client 1 check"". Then, the server broadcasts that message to all connected clients, including the sender, so each client sees something like "From server: client 1 check". Essentially, the server keeps track of all active client connections and relays messages from any client to all others, enabling real-time group communication. This behavior can be observed clearly in the screenshots included above, demonstrating how messages are propagated across clients.