a. What is amqp?
- amqp (Advanded Message Queuing Protocol) is an open standard application layer protocol for message-oriented middleware, with a focus on queuing, routing, reliability and security.

b. What it means? guest:guest@localhost:5672 , what is the first quest, and what is the second guest, and what is localhost:5672 is for? 
- The string `guest:guest@localhost:5672` is a connection string for an AMQP server.
- `guest:guest` is the username and password for the server. In this case, both the username and password are "guest".
- `localhost` is the hostname of the server. In this case, the server is running on the same machine as the client.
- `5672` is the port number on which the server is listening. This is the default port for AMQP.

![alt text](img/image.png)
Screen capture ketika mensimulasikan subscriber yang lambat. Banyak queuenya sudah mencapai 30 karena saya menjalankan cargo run berkali-kali

![alt text](img/image-2.png)
![alt text](img/image-1.png)
![alt text](img/image-3.png)
Screen capture ketika mensimulasikan dengan 3 subscriber yang lambat, tampak spike dari message queue berkurang lebih cepat daripada sebelumnya karena request yang diterima queue akan dibagi tugaskan kepada 3 subscriber.

What can be improved from this code:
- Avoid using `unwrap()`: It's generally a bad practice to use unwrap() in production code because it can cause the program to panic if the Result is an Err. Instead, we can handle the error gracefully using match or if let.
- Use constants for repeated strings: If we have strings that are used multiple times (like "amqp://guest:guest@localhost:5672"), it's a good idea to define them as constants at the top of the file.
- Implement `get_handler_action` method: Currently, the `get_handler_action` method is not implemented and will panic at runtime. We should provide an implementation for this method.