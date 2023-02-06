# Network Communication Model

### **TCP**

TCP stands for Transmission Control Protocol, and it's like a set of rules for sending information over the internet. Imagine you want to send a letter to someone through the mail. You write the letter, put it in an envelope, and write the address on the envelope. This is similar to sending information over the internet.

TCP is like a special type of envelope that makes sure the information you send arrives safely at its destination. It checks to see that the information has been sent correctly and if anything gets lost along the way, it asks to send it again. This makes sure the information you send arrives exactly as you sent it and in the right order.

This is important for things like sending emails, downloading files, or browsing websites. TCP makes sure the information gets to where it needs to go, even if it takes a little longer to get there.



### **How TCP Works**

- Segment: A segment is a piece of the information being sent over the internet, kind of like a page of a book. TCP takes the information you want to send and breaks it into smaller segments to make it easier to send and receive.
- Flow control: This is like a traffic light for the information being sent over the internet. It makes sure that too much information isn't sent at once and helps prevent traffic jams.
- Reliable connection: When you send information using TCP, a reliable connection is established between your device and the recipient's device. This means that the information you send will get to its destination, even if it takes a few tries.
- Error checking: This is like a spell checker for the information being sent over the internet. It makes sure that the information hasn't changed or gotten mixed up during transit, and if it has, it asks to send it again.
- Re-transmission: If something goes wrong during the transmission of a segment, the recipient will ask the sender to send it again. This is called re-transmission, and it helps make sure that the information you send arrives exactly as you sent it.

### **How TCP three way handshake works?**

The TCP three-way handshake is a key aspect of how the TCP protocol ensures reliable communication over the internet. Here's a bit more detail on each step of the process:

1. SYN (Synchronize): The initiating device (let's say it's your computer) sends a SYN message to the receiving device (let's say it's a server), effectively saying "Hey, I want to start a conversation with you." This SYN message includes information such as the initial sequence number that will be used for the data transmission.
2. SYN-ACK (Synchronize-Acknowledgment): The receiving device responds to the SYN message with a SYN-ACK message, effectively saying "I got your request and I'm ready to talk. Here's my own initial sequence number." This SYN-ACK message also acknowledges receipt of the SYN message and confirms that the receiving device is ready to communicate.
3. ACK (Acknowledgment): The initiating device sends an ACK message back to the receiving device, effectively saying "I got your SYN-ACK message and I'm ready to start sending data." This ACK message includes the sequence number that the initiating device is expecting to receive next from the receiving device.

The three-way handshake process helps establish a reliable connection between the two devices by making sure that both devices are ready to communicate and that they have agreed on the initial sequence numbers that will be used for the data transmission. It also helps prevent network congestion by allowing devices to coordinate and limit the number of active connections. Additionally, if any of the messages are lost or corrupt, the process can be repeated to ensure that the connection is established successfully.