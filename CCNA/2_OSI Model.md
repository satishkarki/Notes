# OSI Model

### **Open System Interconnection**

The OSI (Open Systems Interconnection) Model is a conceptual framework used to describe the flow of information between devices in a computer network. The OSI Model is not an actual protocol or piece of software, but rather a model that provides a standardized way of thinking about how data is transmitted between devices.

The OSI Model consists of seven layers, each responsible for a different aspect of the information transmission process. The layers, from bottom to top, are:

1. Physical: This layer is concerned with the transmission of raw data over the network, including the electrical and mechanical connections between devices.
2. Data Link: This layer provides error-free transmission of data frames over the network.
3. Network: This layer is responsible for routing and delivering data between devices, including addressing and routing information.
4. Transport: This layer is responsible for ensuring reliable delivery of data, including flow control and error checking.
5. Session: This layer provides a mechanism for establishing and maintaining communication sessions between devices.
6. Presentation: This layer is concerned with the formatting and encryption of data, including data compression and encryption.
7. Application: This layer is the interface between the user and the network, including the protocols and services used by applications to access the network.

By dividing the information transmission process into these seven layers, the OSI Model provides a way to think about and understand the different components of a computer network and how they interact with one another.



### **Difference between OSI and TCP/IP Model**

The TCP/IP model and the OSI model are both frameworks used to describe how data is transmitted between devices in a computer network. However, there are some key differences between the two models:

1. Number of Layers: The TCP/IP model has four layers, while the OSI model has seven layers. The four layers in the TCP/IP model are the Application, Transport, Internet, and Link layers, while the seven layers in the OSI model are the Application, Presentation, Session, Transport, Network, Data Link, and Physical layers.
2. Purpose: The OSI model is a more comprehensive model that provides a complete description of how data is transmitted between devices, while the TCP/IP model focuses specifically on the protocols used on the internet.
3. Implementation: The OSI model is largely a theoretical model, while the TCP/IP model is used in actual implementations of computer networks. The protocols used in the internet, such as TCP, IP, HTTP, and FTP, are based on the TCP/IP model.
4. Flexibility: The OSI model is more flexible and can be used in a wider range of network environments, while the TCP/IP model is specifically designed for use in the internet.

Despite these differences, both models are used in different ways to help understand how data is transmitted over a computer network. The OSI model provides a complete picture of how data is transmitted, while the TCP/IP model focuses on the specific protocols used in the internet. 



### **Encapsulation**

Encapsulation is done in different layers of a computer network, with each layer adding its own header and trailer to the data. Here's a brief overview of how encapsulation is done in each layer:

1. Application Layer: At the application layer, the data being transmitted is divided into smaller units, or packets, for transmission over the network. This layer also adds any necessary information about the data, such as the type of data being transmitted, to the packet.
2. Presentation Layer: At the presentation layer, the data packet may be encrypted or compressed to ensure that it is secure during transmission. The presentation layer also ensures that the data is formatted in a way that can be understood by the next layer.
3. Session Layer: At the session layer, the data packet is divided into smaller segments if necessary, and a session header is added to the packet. The session header includes information about the session, such as the source and destination of the data.
4. Transport Layer: At the transport layer, a transport header is added to the data packet. The transport header includes information about the type of transmission, such as whether the transmission is reliable or unreliable, and information about flow control and error checking.
5. Network Layer: At the network layer, a network header is added to the data packet. The network header includes information about the source and destination of the data, as well as the routing information needed to deliver the data over the network.
6. Data Link Layer: At the data link layer, a data link header and trailer are added to the data packet. The data link header includes information about the source and destination of the data, and the trailer includes error-checking information to ensure that the data is transmitted accurately.
7. Physical Layer: At the physical layer, the data packet is converted into a stream of bits for transmission over the network. The physical layer also adds any necessary electrical or mechanical signals to the data, such as voltages or frequencies, to ensure that the data is transmitted accurately over the physical connection.

Each layer in a computer network encapsulates the data in its own unique way, providing the necessary information to ensure that the data is transmitted effectively and efficiently over the network.

