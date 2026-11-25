
# Computer Networks – 100 Essential FAANG SDE Interview Questions

**Goal:** Prepare Computer Networks specifically for Software Developer interviews at Google, Amazon, Meta, Microsoft, Apple and other top tech companies.

**Total Questions:** 100

**Learning Path:** Fundamentals → IP Addressing → TCP/UDP → HTTP/HTTPS → DNS → Security → Routing → Application Protocols → Performance → Sockets → CDN/Load Balancing → Real-World Scenarios.

---

## 01. Networking Fundamentals (8)

1. What is a Computer Network and why do we need it?
2. What is the OSI Model? Explain all seven layers.
3. What is the TCP/IP Model? How is it different from OSI?
4. What is the difference between TCP/IP and UDP/IP communication?
5. What is Encapsulation and Decapsulation?
6. What is the difference between Packet, Frame, Segment and Datagram?
7. What is the difference between MAC Address and IP Address?
8. What is the difference between Hub, Switch and Router?

## 02. IP Addressing & Subnetting (8)

9. What is an IP Address? Explain IPv4 and IPv6.
10. What is the difference between Public and Private IP addresses?
11. What is a Static IP vs Dynamic IP?
12. What is a Subnet Mask and why is it needed?
13. What is CIDR notation? Explain /24 and /16.
14. What is a Default Gateway?
15. What is DHCP? Explain the DORA process.
16. What is NAT? Why do we need it?

## 03. TCP & UDP (13)

17. What is TCP? How does it provide reliable communication?
18. What is UDP? When should we use UDP?
19. What is the difference between TCP and UDP?
20. Explain the TCP Three-Way Handshake.
21. Why does TCP require a Three-Way Handshake?
22. Explain the TCP Four-Way Connection Termination.
23. What are SYN, ACK, FIN and RST flags?
24. What are Sequence Numbers and Acknowledgment Numbers?
25. How does TCP handle packet loss?
26. What is TCP Flow Control?
27. What is TCP Congestion Control? Explain Slow Start.
28. What is the difference between TIME_WAIT and CLOSE_WAIT?
29. What is TCP Head-of-Line Blocking?

## 04. HTTP & HTTPS (13)

30. What is HTTP? How does the HTTP Request-Response Cycle work?
31. What is HTTPS? How is it different from HTTP?
32. Explain GET, POST, PUT, PATCH and DELETE.
33. What is Idempotency in HTTP? Which methods are idempotent?
34. Explain HTTP Status Codes: 200, 201, 301, 400, 401, 403, 404 and 500.
35. What are HTTP Request and Response Headers?
36. What are Cookies and Sessions? How are they different?
37. What is JWT? How does JWT-based authentication work?
38. What is CORS? Why do browsers enforce it?
39. What is the Same-Origin Policy?
40. What is HTTP Caching? Explain Cache-Control and ETag.
41. What is the difference between HTTP/1.1, HTTP/2 and HTTP/3?
42. What is TLS Handshake? How does HTTPS establish a secure connection?

## 05. DNS (8)

43. What is DNS and why do we need it?
44. Explain the complete DNS Resolution Process.
45. What are Recursive and Iterative DNS Queries?
46. What are Root, TLD and Authoritative DNS Servers?
47. What are A, AAAA, CNAME and MX Records?
48. What is DNS Caching and TTL?
49. What happens when DNS resolution fails?
50. Why does DNS use UDP? Can DNS use TCP?

## 06. Network Security (7)

51. What is Symmetric vs Asymmetric Encryption?
52. What is the difference between Encryption and Hashing?
53. What is SSL vs TLS?
54. What is a Digital Certificate and Certificate Authority (CA)?
55. What is a Man-in-the-Middle Attack?
56. What is a DDoS Attack?
57. What is a Firewall? What is the difference between Firewall and WAF?

## 07. Routing, Switching & NAT (6)

58. What is Routing? How does a Router forward packets?
59. What is ARP and how does it work?
60. What is the difference between Layer 2 and Layer 3 Switching?
61. What is ICMP? How do Ping and Traceroute work?
62. What is VLAN?
63. What happens when two devices communicate across different networks?

## 08. Application Layer Protocols (5)

64. What is WebSocket and how does it work?
65. What is the difference between WebSocket and HTTP?
66. What is REST API vs RPC?
67. What is gRPC and why is it used?
68. What is SSH and how is it different from HTTP/HTTPS?

## 09. Network Performance & Reliability (7)

69. What is Latency?
70. What is Bandwidth vs Throughput?
71. What is Jitter and Packet Loss?
72. What is Round-Trip Time (RTT)?
73. What is MTU and MSS?
74. What is Network Congestion?
75. How can you reduce API Network Latency?

## 10. Socket Programming & Ports (6)

76. What is a Socket in Computer Networking?
77. What is the difference between IP Address, Port and Socket?
78. What is the difference between TCP Socket and UDP Socket?
79. What happens when a Server listens on a Port?
80. What is Blocking vs Non-Blocking I/O?
81. How can a Server handle thousands of concurrent connections?

## 11. Proxy, CDN & Load Balancing (8)

82. What is a Proxy Server?
83. What is the difference between Forward Proxy and Reverse Proxy?
84. What is a Load Balancer and why do we need it?
85. What are Round Robin, Least Connections and Consistent Hashing?
86. What is the difference between Layer 4 and Layer 7 Load Balancing?
87. What is a CDN and how does it work?
88. What is Cache Hit vs Cache Miss in a CDN?
89. What is an API Gateway and how is it different from a Reverse Proxy?

## 12. Real-World Scenario-Based Questions (11)

90. What happens when you type google.com in your browser and press Enter? Explain everything from DNS to page loading.
91. What happens if DNS resolves successfully but the website still does not open?
92. Why can you ping a server but cannot access its website?
93. Why might an API work locally but fail in production?
94. How would you debug a slow API response?
95. What happens when a TCP connection is lost during data transmission?
96. How would you design a real-time chat application using networking concepts?
97. How would you design a globally distributed service with low network latency?
98. What happens when a server receives thousands of concurrent HTTP requests?
99. How would you transfer a large file reliably over an unstable network?
100. What happens if a Load Balancer or one of the backend servers becomes unavailable?

---
