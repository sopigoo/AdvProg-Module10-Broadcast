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

### 2.2 Modifying the websocket port
- Server port change
![server-port-change](/images/change-port-server.png)
- Client port change
![client-port-change](/images/change-port-client.png)
- Server
![server-8080](/images/server-8080.png)
- Client 1
![client-8080-1](/images/client-8080-1.png)
- Client 2
![client-8080-2](/images/client-8080-2.png)
- Client 3
![client-8080-3](/images/client-8080-3.png)
<br>

In this experiment, I changed the communication port between the server and clients from `2000` to `8080`. Since the application uses the WebSocket protocol, both server and clients must reference the same port and protocol to communicate properly. The server's binding address was updated to `127.0.0.1:8080` in the `TcpListener::bind(...)` line, and the client's WebSocket URI was changed to `ws://127.0.0.1:8080` in the `ClientBuilder::from_uri(...)` call. The application uses the same WebSocket protocol provided by the `tokio_websockets` crate, where the server wraps incoming TCP connections with `ServerBuilder::new().accept(...)`, and the client connects using `.connect()` on a WebSocket stream. After the modification, I tested the setup with the server and multiple clients, and all messages were still successfully broadcast among clients, confirming the application still worked as intended.

### 2.3 Small changes. Add some information to client
- Server
![server-change](/images/server-change.png)
- Client 1
![client-1-change](/images/client-1-change.png)
- Client 2
![client-2-change](/images/client-2-change.png)
- Client 3
![client-3-change](/images/client-3-change.png)
<br>

In this experiment, I modified the server's message broadcasting logic to include the sender's IP address and port in each broadcasted message. This helps clients identify who sent which message, even in the absence of usernames or unique identifiers. The change was made inside the `handle_connection` function, where the original broadcast line `bcast_tx.send(text.into())?` was replaced with `bcast_tx.send(format!("{addr} : {text}"))?`, appending the sender's `SocketAddr` (IP\:Port) to the message. On the client side, the receiving logic remained the same, as the message format change is handled transparently. This modification gives a clearer context in the chat logs about who is sending each message, which is especially useful for debugging, developing identity features, or simply enhancing the clarity of interactions between multiple clients. After applying the change, I tested it by running the server and connecting multiple clients. Each received message now includes the sender's address, confirming the broadcast format is functioning as intended.
