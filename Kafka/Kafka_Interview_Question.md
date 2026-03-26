# Kafka Basics Interview Questions From GFG
## Q1 : What is Apache Kafka?
1. Defination
Apache Kafka ek distributed event streaming platform hai jo real-time me data ko
👉 publish (send)
👉 store (persist)
👉 consume (read/process)
karne ke liye use hota hai — wo bhi high speed aur fault-tolerance ke saath.
👉 Simple bolu:
Kafka = ek super-fast messaging system + data pipeline + storage system

2. Example :
-- Maan le tu ek Stock Trading Firm chala raha hai:
-- 👉 Client ne order dala: "BUY 100 shares of INFY @ ₹1500"
-- Ab kya hota hai:
    - Order Service → Kafka ko message bhejta hai (Producer)
    - Kafka usko ek Topic: Orders me store karta hai
    - Multiple systems usko read karte hain (Consumers):
        - Matching Engine → buy/sell match karega
        - Risk Management → check karega ki paisa hai ya nahi
        - Trade Analytics → data collect karega
        - Notification Service → user ko update bhejega
-- 👉 Important: Sab systems independent hain — ek fail ho gaya toh bhi dusre chalenge

3. Visualization (Flow samajh lo):
Client App
   ↓
Order Service (Producer)
   ↓
Kafka (Topic: Orders)
   ↓       ↓         ↓         ↓
Risk    Matching   Analytics   Notification

## Q2 : What are the key components of Kafka?
1. Defination
Kafka ke kuch core building blocks hote hain jo milke ek event streaming system banate hain.
👉 Main components:
    - Producer
    - Consumer
    - Topic
    - Partition
    - Broker
    - Zookeeper / KRaft (Cluster Management)

2. Example
    Maan le ek trading firm me order flow chal raha hai:    
    👉 Client ne order dala:
    BUY 100 shares of RELIANCE
    Ab Kafka components ka role:
        1. Producer (Message bhejne wala)
            - 👉 Order Service : Client ka order lekar Kafka me bhejta hai
            - Example : Order Service → Kafka topic me order push karta
        2. Topic (Category / Channel)
            - 👉 Message ka logical group
            - Example :
                - Orders
                - Trades
                - MarketData
            - 👉 Order Orders topic me jayega
        3. Partition (Parallel processing ke liye split)
            - 👉 Topic ko multiple parts me divide karte hain
            - Example :         
                - Orders topic → 3 partitions
                - Different orders alag partitions me
            - Benefit: Parallel processing (fast execution)
        4. Broker (Kafka Server)
            - 👉 Kafka ka actual server jo data store karta hai
            - Example : 
                - Broker 1
                - Broker 2
                - Broker 3
            - 👉 Orders in servers pe store honge
        5. Consumer (Message read karne wala)
            - 👉 Systems jo Kafka se data read karte hain
            - Example : 
                - Matching Engine
                - Risk System
                - Notification Service
        6. Zookeeper / KRaft (Cluster manager)
            - 👉 Kafka cluster ko manage karta hai
                - Leader election
                - Metadata maintain
                - Brokers coordination
            - 👉 New Kafka me: KRaft mode (Zookeeper remove ho raha hai)

3. Visualization 
Client
  ↓
Order Service (Producer)
  ↓
Kafka Topic: Orders
  ↓
Partitions (P1, P2, P3)
  ↓
Brokers (Server1, Server2, Server3)
  ↓
Consumers:
   → Matching Engine
   → Risk System
   → Notification Service

4. 


## Q3 : What is a topic in Kafka?
1. Defination
Kafka me Topic ek logical category / channel hota hai jisme messages store hote hain.
👉 Simple samajh:
Topic = ek folder / queue jisme similar type ka data store hota hai

2. Example :
Topics Like
    - Orders → sab client orders
    - Trades → executed trades
    - MarketData → live stock prices
    - Payments → fund transactions

## Q4 : What is a partition in Kafka?
1. Defination
Kafka me Partition ek topic ka subset (chhota part) hota hai jahan actual data store hota hai.
👉 Simple samajh:
Topic = Folder
Partition = us folder ke andar files ke chunks (parallel storage units)
👉 Har partition me data ordered + sequential log me store hota hai

2. Example
-- Topic Order
-- Topic ko divide kar diya:
Partition 0 → some orders
Partition 1 → some orders
Partition 2 → some orders

3. Visulization
            Topic: Orders
        ---------------------
        |   P0  |  P1  | P2  |
        ---------------------
          ↓      ↓      ↓
       Consumer Consumer Consumer
         (C1)     (C2)     (C3)

4. Important
-- Ordering Guarantee
👉 Order sirf within a partition maintain hota hai
❌ Across partitions order guarantee nahi hota
-- Parallelism - Performace
👉 Zyada partitions → zyada consumers → faster processing
-- Key-based Partitioning
👉 Agar tu key deta hai (e.g., userId)
same user ke orders same partition me jayenge
👉 Trading me useful:
Same client ka order sequence maintain rahe
-- Offset Concept
👉 Har message ka ek unique number hota hai (offset)
Example : Partition 0 → offset 0,1,2,3...
-- Partition = Unit of Scalability
👉 Kafka scale hota hai partitions ke basis pe

## Q5 : What is the role of ZooKeeper in Kafka?
1. Defination
ZooKeeper ek centralized coordination service hai jo Kafka cluster ko manage karta hai.
👉 Simple bolu:
ZooKeeper = Kafka ka “manager / coordinator” jo sab brokers ko control aur sync me rakhta hai

2. Example :
-- Maan le tumhari trading firm me multiple Kafka servers (brokers) chal rahe hain:
    - Broker1
    - Broker2
    - Broker3
👉 Ab in sab ko coordinate kaun karega?
    Yahi kaam karta hai ZooKeeper 
3. Important
-- Broker Management : Kaun broker alive hai / down hai
-- Leader Election : Agar Broker1 crash ho gaya ❌ ->ZooKeeper new leader elect karega (e.g., Broker2)
-- Metadata Storage : Topics , Partitions , Leader Info
-- Cluster Coordination : Sab brokers sync me rahen
-- ZooKeeper ab deprecated ho raha hai , KRaft mode (Kafka Raft Metadata mode) use hota hai

## Q6 : What is a broker in Kafka?
1. Defination
Kafka me Broker ek server (machine) hota hai jo:
👉 messages ko store karta hai
👉 clients (producers/consumers) se data receive & serve karta hai
👉 Simple bolu:
Broker = Kafka ka storage + handling server

2. Example
-- Maan le ek bada restaurant hai:
-- 👉 Tumne order diya: "1 Paneer Butter Masala + 2 Naan"
-- Ab kya hota hai:
    - Waiter (Producer) order lekar kitchen system me daalta hai
    - Kitchen me multiple stations (brokers) hote hain:
        - Kitchen Server 1 → Main Course
        - Kitchen Server 2 → Tandoor
        - Kitchen Server 3 → Dessert
👉 Ye sab milke Kafka cluster (restaurant kitchen) banate hain
-- Broker ka role:
    - Order receive karna
    - Order ko store karna (jab tak cook na ho)
    - Correct chef (consumer) tak pahunchana

3. Visualization (Broker ka role):
Customer
   ↓
Waiter (Producer)
   ↓
-------------------------
|  Kitchen System       |
|  (Kafka Cluster)      |
|                       |
|  Broker1  Broker2     |
|  Broker3  Broker4     |
-------------------------
   ↓
Chefs (Consumers)  
👉 Har broker ek kitchen server hai jahan orders store ho rahe hain

4. Important Points
-- 1. Kafka Cluster = Multiple Brokers
👉 Ek Kafka system me usually multiple brokers hote hain
-- 2. Data Distribution
👉 Partitions alag-alag brokers me store hote hain
👉 Load balance + scalability
-- 3. Faut Tolerance
👉 Data replicate hota hai across brokers
👉 Ek broker down ho gaya toh bhi system chal raha
-- 4. Broker ID
👉 Har broker ka unique ID hota hai
-- 5. Client Interaction
👉 Producers & Consumers directly broker se baat karte hain


## Q7 : How does Kafka ensure fault tolerance?
1. Defination
-- Kafka fault tolerance ensure karta hai by:
    - data replication
    - leader-follower mechanism
    - automatic failover
-- Kafka data ko multiple jagah store karta hai, taaki ek system fail ho jaaye toh bhi data safe rahe

2. Example
-- Maan le ek busy restaurant hai:
-- Customer ne order diya: "1 Pizza + 1 Cold Drink"
-- Normal Case
    - Order kitchen me gaya (Broker1)
    - Ye main chef (Leader) handle kar raha hai
    👉 But smart system kya karta hai?
    - Same order ka copy backup kitchens (Follower brokers) me bhi store hota hai
-- Problem Case : 👉 Main kitchen (Broker1) suddenly band ho gaya 😱
-- Solution : 
    - Backup kitchen (Broker2) automatically leader ban jata hai
    - Order processing continue hoti hai
    - Customer ko pata bhi nahi chalta

3. Visualization
        Topic: Orders (Partition P0)
              
        Leader (Broker1)
              ↓
   -------------------------
   |        |              |
Follower  Follower     Follower
(Broker2) (Broker3)    (Broker4)
❌ Broker1 Down
→ Broker2 becomes NEW Leader ✅

4. Important
-- 1. Replication Factor
    👉 Har partition ke multiple copies hote hain
    Example : Replication Factor = 3 (1 Leader + 2 Followers)
-- 2. Leader & Follower
    👉 Leader: Read/write handle karta hai And Followers: Backup copies maintain karte hain
-- 3. ISR (In-Sync Replicas)
    👉 Jo followers leader ke saath sync me hain
    👉 Sirf ISR me se hi new leader choose hota hai
-- 4. Automatic Failover
    👉 Leader down → Kafka automatically new leader elect karta hai
-- 5. Acknowledgement (acks)
    👉 Producer decide karta hai data kitna safe hona chahiye:
        - acks=0 → fastest, no guarantee ❌
        - acks=1 → leader confirm karega
        - acks=all → all replicas confirm (most safe ✅)

## Q8 : What is the difference between a Kafka consumer and consumer group?
1. Defination
👉 Consumer : Ek single application / service jo Kafka se messages read karta hai
👉 Consumer Group : Consumers ka ek group jo milke same topic ko parallel me consume karte hain
👉 Simple line :
    - Consumer = ek banda kaam kar raha hai
    - Consumer Group = team milke kaam kar rahi hai

2. Example : 
-- Maan le ek restaurant me orders aa rahe hain:
-- Topic = Food Orders
-- 🔹 Case 1: Single Consumer
    👉 Sirf ek chef hai:
        - Sab orders ek hi chef bana raha hai
        - Slow Ho jayega
-- 🔹 Case 2: Consumer Group
    👉 Ab 3 chefs hain (same group): Chef 1 , Chef 2 , Chef 3
    👉 Orders distribute ho jaate hain:
        -- Order1 → Chef1
        -- Order2 → Chef2
        -- Order3 → Chef3
    👉 Sab milke kaam kar rahe hain → fast service 🚀

## Q9 : What is the purpose of the offset in Kafka?
1. Defination
-- Kafka me Offset ek unique ID (number) hota hai jo har message ko assign hota hai within a partition.
-- 👉 Simple bolu:
-- Offset = message ka position number (index) jisse Kafka track karta hai ki consumer ne kaha tak read kiya

2. Example 
-- Maan le kitchen me ek order queue chal rahi hai:
-- Orders aa rahe hain:
| Offset | Order   |
| ------ | ------- |
| 0      | Pizza   |
| 1      | Burger  |
| 2      | Pasta   |
| 3      | Noodles |
-- Chef (Consumer) kaam kar raha hai:
    - Chef ne Pizza, Burger bana liya
    - Ab wo Offset = 2 pe hai
👉 Matlab:
👉 "Maine pehle 2 orders process kar liye, ab next Pasta hai"

3. Visualiation
Partition (Orders)
Offset →   0     1     2     3
         -------------------------
         Pizza Burger Pasta Noodles
                ↑
           Chef current position

4. Important
-- 1. Offset per Partition hota hai
👉 Har partition ka apna offset sequence hota hai
-- 2. Consumer Offset Track karta hai
👉 Kafka ya consumer group yaad rakhta hai:
"last processed message ka offset kya tha"
-- 3. Replay Capability
👉 Agar chef chahe:
-- Offset reset karke purane orders dobara process kar sakta hai
    - For Debugging
    - Reprocessing data
    - Audit
-- 4. Auto Vs Manual Commit
👉 Offset kaise save hota hai:
    - Auto commit → Kafka khud save karega
    - Manual commit → developer control karega (safe option)
-- 5. At-least-once / At-most-once
👉 Offset handling decide karta hai:
    - Duplicate processing hoga ya nahi
    - Data loss hoga ya nahi

## Q10 : How does Kafka handle message delivery semantics?
1. Defination
-- Kafka message delivery ko 3 tarike se handle karta hai:
    1. At-most-once → message kabhi duplicate nahi hoga, but lose ho sakta hai
    2. At-least-once → message lose nahi hoga, but duplicate ho sakta hai
    3. Exactly-once → na duplicate, na loss (perfect delivery ✅)
-- Simple bolu:
Kafka decide karta hai ki message kitna safely deliver hona chahiye

2. Example 
-- Maan le customer ne order diya:
👉 "1 Burger"
-- 🔹 1. At-most-once (Fast but Risky ❌)
    👉 Flow:
        - Waiter ne order chef ko diya
        - Order system me mark ho gaya as processed
        - But chef ne order banana bhool gaya 😅
    👉 Result:
    ❌ Customer ko burger mila hi nahi (data loss)
-- 🔹 2. At-least-once (Safe but Duplicate ho sakta hai ⚠️)
    👉 Flow:
        - Waiter order deta hai
        - Chef burger bana raha hai
        - System crash ho gaya before confirmation
    👉 Next chef kya karega?
        - Same order dobara bana dega
    👉 Result:
    ✅ Customer ko burger mila
    ❌ But 2 burger mil gaye 😅 (duplicate)
-- 🔹 3. Exactly-once (Perfect Delivery ✅)
    👉 Flow:
        - Waiter order deta hai
        - Chef banata hai
        - System ensure karta hai:
            Ek hi baar bana
            Proper confirm hua
    👉 Result:
    ✅ Na order miss hua
    ✅ Na duplicate bana

## Q11 : What is the role of the Kafka producer API?
1. Defination
-- Kafka Producer API ek interface/library hai jiske through applications
👉 Kafka topics me messages send (publish) karte hain
👉 Simple bolu:
-- Producer API = Kafka ko data bhejne ka official tareeka

2. Example : 
-- Maan le restaurant me :
👉 Customer ne order diya: "1 Pizza + 1 Coke"
👉 Flow samajh:
    - Waiter = Producer
    - Waiter ka notepad / system = Producer API
👉 Waiter kya karta hai:
    1. Order leta hai
    2. Proper format me likhta hai
    3. Correct kitchen section ko bhejta hai
👉 Ye sab kaam Producer API karta hai backend me

3. Visualization (Producer API Flow):
Customer
   ↓
Waiter (Producer)
   ↓
Producer API (send logic)
   ↓
Kafka Topic (Orders)
👉 Producer API ensure karta hai ki message correct jagah + safe tareeke se jaye

4. Important
-- 1. Message Send Karna : 
    👉 Topic me data publish karna
-- 2. Partition Selection : 
    👉 Decide karta hai message kis partition me jayega:
        - Key ke basis pe
        - Round-Robin
        - Custom Logic
-- 3. Batching (Performance Boost 🚀)
    👉 Multiple messages ko ek saath bhejta hai
    → network calls kam ho jati hain
-- 4. Compression
    👉 Data compress karke bhejta hai
    -> faster + less bandwidth
-- 5. Acknowledgement Handling (acks)
    👉 Decide karta hai : Leader confirm kare ya sab replicas (acks=all)
-- 6. Retry Mechanism
    👉 Agar message fail ho gaya: Automatically retry karega
-- 7. Idempotent Producer (Advanced 🔥)
    👉 Duplicate messages avoid karta hai

## Q12 : How does Kafka support scalability?
1. Defintion
-- Kafka scalability support karta hai by:
    👉 horizontal scaling (more brokers add karna)
    👉 partitioning (data split karna)
    👉 consumer groups (parallel processing)
-- Kafka system ko aise design kiya gaya hai ki load badhne par easily scale ho sake bina system todhe

2. Example :
-- Maan le tumhara restaurant viral ho gaya 😅
👉 Suddenly 10x orders aa rahe hain
❌ Without Scalability:
    - Sirf 1 kitchen
    - 1 Chef
    - Result : delay , Angry customers
✅ With Kafka-style Scalability:
    - More Kitchens add karte ho (Brokers)
    - Order types divide karte ho (Partitions)
    - More chefs hire karte ho (Consumer Groups)
👉 Result:
    - Orders distribute ho jaate hain
    - Sab fast process hota hai

3. How Kafka Achieve Scalibality
-- 1. Partitioning
    👉 Topic ko multiple partitions me divide karta hai
    → Parallel processing possible
-- 2. Horizontal Scaling (Add Brokers)
    👉 New servers add karo → load distribute ho jata hai
-- 3. Consumer Groups
    👉 Multiple consumers ek hi topic ko parallel read karte hain
    -> faster processing
-- 4. Distributed Architecture
    👉 Data multiple brokers me spread hota hai
    -> single machine pe load nahi
-- 5. Load Balancing
    👉 Partitions automatically different brokers me distribute hote hain

## Q13 : What is log compaction in Kafka?
1. Defination
-- Kafka me Log Compaction ek process hai jisme:
    👉 har key ke liye sirf latest value retain hoti hai
    👉 purane duplicate/old records remove ho jaate hain
-- 👉 Simple bolu:
Log Compaction = “latest state ko preserve karna, history clean kar dena”

2. Example :
-- Maan le ek customer ne apna order multiple baar update kiya:
-- 👉 Same Order ID = #101
| Time    | Order                  |
| ------- | ---------------------- |
| 1:00 PM | Pizza                  |
| 1:05 PM | Pizza + Coke           |
| 1:10 PM | Pizza + Coke + Dessert |
-- 👉 Without Compaction: Saare records store honge ❌
-- 👉 With Log Compaction: Sirf latest record store hoga ✅
-- 👉 Final : Order #101 → Pizza + Coke + Dessert
 
3. Visualization (Before vs After):
Before Compaction:
Order#101 → Pizza
Order#101 → Pizza + Coke
Order#101 → Pizza + Coke + Dessert
..................................
After Compaction:
Order#101 → Pizza + Coke + Dessert ✅

4. Important
-- 1. Key-based Retention : 👉 Compaction tabhi kaam karega jab message me key ho
-- 2. Latest Value Retained : 👉 Har key ka sirf latest update store hota hai
-- 3. Not Immediate : 👉 Compaction background me hota hai (instant nahi)
-- 4. Tombstone Records : 
    👉 Agar key delete karni hai:
        Null value send karo -> Kafka usko bhi clean kar deta hai
-- 5. Use Case = State Storage : 👉 Jab tumhe latest state chahiye, history nahi


## Q14 : How does Kafka handle message ordering?
1. Definition
-- Kafka message ordering ko partition level par guarantee karta hai
-- 👉 Simple bolu:
-- Same partition ke andar messages hamesha order me milte hain
-- ❌ Different partitions ke beech order guarantee nahi hota

2. Example :
-- Maan le ek restaurant me orders aa rahe hain:
-- 👉 Same table (Table #5) ne multiple orders diye:
    - Soup
    - Main Course
    - Dessert
-- ✅ Case 1: Same Partition (Correct Ordering)
    👉 Agar saare orders same partition me gaye:
    - Chef ko milega:
        Soup
        Main Course
        Dessert
    - 👉 Perfect sequence maintain ✅
-- ❌ Case 2: Different Partitions
    👉 Agar orders alag partitions me chale gaye:
        - Soup → Chef1
        - Dessert → Chef2
        - Main Course → Chef3
    👉 Result:
    ❌ Dessert pehle aa sakta hai 😅 (wrong order)

3. Visualization
Partition 0:
Offset → 0      1        2
        Soup → Main → Dessert  ✅
Partition 1:
Offset → 0      1
        Dessert → Soup  ❌ (no global order)
👉 Ordering sirf within partition guaranteed hai

4. Important
-- 1. Ordering = Partition Level
    👉 Kafka globally ordering guarantee nahi karta
    👉 Sirf per-partition ordering deta hai
-- 2. Key-based Ordering
    👉 Agar tu key use kare:
    Example : Key = TableId
    👉 Same table ke orders same partition me jayenge
    → order maintain rahega
-- 3. Producer Role Important
    👉 Producer decide karta hai:
    message kis partition me jayega
-- 4. Single Partition = Full Order
    👉 Agar strict ordering chahiye:
    Use 1 partition (but low scalability ❌)
-- 5. Trade-off
    👉 Ordering vs Scalability:
    | Option              | Result                      |
    | ------------------- | --------------------------- |
    | 1 Partition         | ✅ Order correct, ❌ slow     |
    | Multiple Partitions | ✅ Fast, ❌ global order nahi |



## Q15 : What is the significance of the acks parameter in Kafka producers?
1. Defination
-- Kafka me acks (acknowledgements) parameter decide karta hai ki
-- 👉 producer ko message send karne ke baad kitni confirmation chahiye brokers se
-- acks = "Waiter kitni confirmation lega ki order safely kitchen me pahunch gaya?"

2. Example
-- Maan le waiter order bhej raha hai kitchen me : 👉 Order: "1 Paneer Tikka"
🔹 1. acks = 0 (No confirmation ❌)
👉 Waiter kya karta hai:
Order bol diya kitchen ko
Confirm kiya bhi nahi
Seedha chala gaya 😅
👉 Result:
❌ Order lost ho sakta hai
⚡ Fast but risky
.......
🔹 2. acks = 1 (Leader confirmation ⚖️)
👉 Waiter:
Head chef (leader broker) ko bolta hai
Chef bolta: "Haan mil gaya"
👉 Waiter satisfied
👉 Result:
✅ Better than 0
⚠️ But agar leader crash ho gaya before backup → data loss possible
.......
🔹 3. acks = all (Full safety ✅)
👉 Waiter:
    Sirf head chef nahi
    Backup chefs (followers) se bhi confirmation leta hai
👉 Result:
✅ Order fully safe
❌ Thoda slow

3. Visualization
Order → Kitchen
acks=0:
  Waiter → Send → No confirmation ❌
acks=1:
  Waiter → Leader Chef confirms ✅
acks=all:
  Waiter → Leader + Backup Chefs confirm ✅✅

## Q16 : How does Kafka handle data retention?
1. Defination 
-- Kafka me data retention ka matlab hai:
-- messages kitne time tak ya kitne size tak store rahenge
-- Retention = “Kitchen order history kitni der tak sambhal ke rakhe?”

2. Example :
-- Maan le restaurant me har order ka record store ho raha hai:
-- Ab manager decide karta hai:
-- 🔹 Option 1: Time-based Retention
    - "Orders sirf 24 hours tak store honge"
    - 1 din baad → old orders delete ❌
    - Example : 
        - Kal ke orders → delete
        - Aaj ke orders → available
-- 🔹 Option 2: Size-based Retention
    - "Max 1GB order data store hoga"
    - Jaise hi limit cross hui
        -> purane orders delete hone lagenge

3. Important
-- 1. Time-based Retention
    👉 Config: log.retention.hours
    e.g. 7 days
    → 7 din purana data delete
-- 2. Size-based Retention
    👉 Config: log.retention.bytes
    e.g. 10GB
    → limit cross → old data remove
-- 3. Log Compaction (Special Case)
    👉 Already padha:
    Sirf latest value per retain hoti hai
    -> history remove


## Q17 : What is the purpose of the Kafka Connect API?
1. Defination
-- Kafka Connect API ka purpose hai:
    👉 external systems (DB, files, APIs, etc.) ko Kafka ke saath easily integrate karna
    👉 bina custom code likhe data import/export karna
-- Simple Bolu : 
Kafka Connect = ready-made pipeline system jo data ko Kafka me laata aur Kafka se bahar bhejta hai

2. Example
-- Maan le tumhara restaurant multiple systems use karta hai:
    - Billing System
    - Inventory DB
    - Online Orders(Zomato / Swiggy)
    - Analytics System.
-- Ab problem : Har system ko Manually connect karna = complex
-- Solution : Kafka Connect
-- 🔹 Case 1: Source Connector (Data Kafka me lana)
👉 Example:
    - Swiggy se orders aa rahe hain
    - Kafka Connect automatically unko Kafka topic me daal deta hai
👉 Like:
    - External Orders -> Kafka(Orders topic)
-- 🔹 Case 2: Sink Connector (Kafka se data bahar bhejna)
👉 Example:
    - Kafka me jo orders aaye -> unko Database me store karna
👉 Kafka Connect automatically karega

3. Visualization
External Systems
 (Swiggy / DB / API)
        ↓
   Source Connector
        ↓
     Kafka Topics
        ↓
   Sink Connector
        ↓
 Database / Analytics / Storage

4. Important 
-- Source Connector
    👉 External → Kafka
    Example : 
        - DB → Kafka
        - API → Kafka
-- Sink Connect
    👉 Kafka → External
    Example : 
        - Kafka → DB
        - Kafka → ElasticSearch
-- Connectors 
    👉 Pre-built plugins (ready-made integrations)
-- Distributed Mode
    👉 Multiple workers → scalable system

## Q18 : How does Kafka ensure high availability?
1. Defination
-- Kafka high availability ensure karta hai by:
    👉 replication (multiple copies of data)
    👉 leader-follower architecture
    👉 automatic failover
👉 Simple bolu:
Kafka system ko aise design karta hai ki agar kuch servers fail ho jayein, tab bhi system chalta rahe

2. Example
-- Maan lo ek bada restaurant hai jahan:
👉 Har order multiple kitchens me copy hota hai
🔹 Normal Flow:
    - Order aaya: "1 Pasta"
    - Main kitchen (Leader) usko handle kar raha hai
    - Backup kitchens (Followers) me bhi uski copy hai
❌ Problem:
👉 Main kitchen band ho gaya (Chef sick 😅)
✅ Kafka Solution:
Backup kitchen turant new main kitchen (Leader) ban jata hai
Order processing continue hoti hai
Customer ko delay nahi hota 😎

3. IMPORTANT
-- Replication Factor
    👉 Har partition ke multiple copies (replicas) hote hain
    Example : RF = 3 → 1 leader + 2 followers
-- Leader-Follower Model
    👉 Leader: Read/write handle karta hai
    👉 Followers: Backup copies maintain karte hain
-- ISR (In-Sync Replicas)
    👉 Jo followers updated hain leader ke saath
    👉 New leader sirf ISR me se hi select hota hai
-- Automatic Failover
    👉 Leader down → Kafka automatically new leader elect karta hai
-- Distributed Cluster
    👉 Multiple brokers → no single point of failure

## Q19 : What is the difference between Kafka Streams and Apache Flink?
1. Defination
👉 Kafka Streams : Kafka ka lightweight stream processing library hai jo directly Kafka ke data pe kaam karta hai
👉 Apache Flink : Ek powerful distributed stream processing engine hai jo complex real-time processing ke liye bana hai
👉 Simple bolu:
    Kafka Streams = simple, app-level processing
    Flink = heavy-duty, enterprise-level processing

2. Example :
-- Maan le tumhara restaurant data process kar raha hai:
-- 🔹Kafka Streams (Simple Kitchen Logic 🍳)
    - Orders aa rahe hain
    - Tum simple kaam karna chahte ho:
        - Count orders
        - Filter veg/non-veg
        - Total sales calculate
    - Ye kaam ek chef easily handle kar lega
    ✔ No separate system needed
    ✔ Same app me logic likh diya
    👉 Kafka Streams = ek smart chef jo basic processing karta hai
--🔹Apache Flink (Advanced Central Kitchen 🏭)
    - Tumhe complex kaam karna hai:
        - Fraud detection
        - Real Time analytics dashboard
        - Window - based calcuation
        - Eent Time Processing
    👉 Ye kaam ek advanced central kitchen system karega
    ✔ Dedicated system
    ✔ High scalability
    ✔ Complex logic
    👉 Flink = full-fledged processing engine

## Q20 : How does Kafka handle message compression?
-> Kafka supports message compression to reduce the size of data transferred and stored. Compression can be configured at the producer level, and Kafka supports several compression types including gzip, snappy, lz4, and zstd. The broker can be configured to decompress messages to validate and convert them to the message format version on the broker.


## Q21 : What is the purpose of the Kafka Streams API?
1. Defination
Kafka Streams API ek Java library hai jo developers ko Kafka topics ke data ko
    👉 process,
    👉 transform,
    👉 aggregate,
    👉 analyze in real-time
Karne ki ability deta hai.
👉 Simple bolu: Kafka Streams API = Kafka data ko real-time me process karne ka tool

2. Example 
-- Maan lo restaurant me har order Kafka me aa raha hai:
-- Topic: Orders
-- Example orders:
| OrderID | Item   | Price |
| ------- | ------ | ----- |
| 1       | Pizza  | 300   |
| 2       | Burger | 200   |
| 3       | Pizza  | 300   |
| 4       | Pasta  | 250   |
👉 Ab restaurant owner ko real-time insights chahiye:
    - Pizza kitni baar order hua
    - Total sales kitni hui
    - Veg vs Non-Veg orders
    - Last 10 min orders
👉 Ye sab Kafka Streams API process karega.
Example : Orders Topic → Kafka Streams Processing → Analytics Topic

3. Visualization
        Orders Topic
             ↓
     Kafka Streams App
   (Filter / Map / Aggregate)
             ↓
      Processed Data Topic
             ↓
      Dashboard / Analytics
👉 Data continuously flow karta hai (stream processing)


## Q22 : How does Kafka handle message size limits?
1. Defination
-- Kafka me har message ka maximum size limit hota hai.
-- Agar message is limit se bada ho jaye to Kafka usko reject kar deta hai.
👉 Simple bolu: Kafka ek limit set karta hai ki ek message kitna bada ho sakta hai.
Default KAfka me : Default max message size ≈ 1 MB

2. Important Configurations
-- Producer : max.request.size
    👉 Producer kitna bada message bhej sakta hai.
    Example : max.request.size = 5MB
-- Broker Side : message.max.bytes
    👉 Broker kitna bada message accept karega
-- Topic Level : max.message.bytes
    👉 Specific topic ke liye message limit.
-- Consumer Side : fetch.max.bytes
    👉 Consumer kitna bada message read karega.

3. Important Points
-- Default Limit - 1mb
-- Large Messgage Not Recommended
    - Network slow karte hain
    - Broker memory pressure badhate hain

## Q23 : What is the role of the group coordinator in Kafka?
1. Defination
-- Kafka me Group Coordinator ek broker hota hai jo:
    - consumer group ko manage karta hai
    - partitions assign karta hai consumers ko
    - consumer heartbeats monitor karta hai
    - rebalancing trigger karta hai
👉 Simple bolu:
Group Coordinator = Consumer group ka manager jo decide karta hai kaun consumer kaunsa kaam karega.

2. Example 
-- Maan lo restaurant me orders kitchen me aa rahe hain.
-- Topic = Food Orders
-- Partitions : P0 ,P1 ,P2 ,P3
-- Kitchen me 4 chefs (consumers) ka group hai : Chef1, Chef2 , Chef3 , Chef4
-- Ab kaun decide karega kaunsa chef kaunsa order banayega
 👉 Kitchen Manager (Group Coordinator)

3. Visualization
           Orders Topic
       -------------------
       P0   P1   P2   P3
       -------------------
            ↓
      Group Coordinator
      (Kitchen Manager)
     ↓      ↓      ↓      ↓
   Chef1  Chef2  Chef3  Chef4
   (C1)   (C2)   (C3)   (C4)

4. Responsibilities
-- Consumer Group Management
    - Group Coordinator track karta hai:    
        - Kaun consumer group me join hua
        - Kaun leave hua
        - Kaun Active hai.
    Resturant Analogy : Manager check karta hai kaun chef duty par hai.
-- Partition Assignment 
    - Coordinator decide karta hai: Kaunsa consumer → kaunsi partition read karega
    - Example : C1 -> P0 , C2 -> P1 , C3 -> P2
-- Rebalancing Trigger
    - Agar : 
        - New consumer join kare
        - Consumer crash ho jaye
    - To coordinator rebalance start karega.
-- Heartbeat Monitoring
    - Consumers periodically heartbeat bhejte hain.
    - Agar heartbeat na aaye: "Consumer dead assume kiya jata hai"
-- Offset Tracking
    - Coordinator ensure karta hai: "Consumers ka offset properly commit ho raha hai"

    
## Q24 : How does Kafka handle data replication?
1. Defination
-- Kafka data replication use karta hai taaki :
    - data loss na ho.
    - system highly available rahe
    - broker failure se system survive kar sake,
👉 Simple bolu : Replication = Kafka ek message ki multiple copies different brokers par store karta hai.

2. Example 
-- Maan lo restaurant me ek important order aaya:
    Order #101
    Pizza + Coke
-- Restaurant manager kya karta hai?
    👉 Order sirf ek kitchen me nahi bhejta.
    Instead :
        - Kitchen1 → Main Chef
        - Kitchen2 → Backup Chef
        - Kitchen3 → Backup Chef
-- Same Order ki multiple copies

4. Important
-- Replication Factor
    - Define Karta hai : kitni copies store hongi
    - Example : Replication Factor = 3
    - Matlab :  1 Leader , 2 Followers
-- Leader Replica
    - Leader responsible hota hai:
        - Producers se writes receive karna
        - Consumers ko data serve karna
-- Follower Replicas
    - Followers continuously leader se data copy karte hain.
    - Resturant Example : Backup chefs same recipe copy kar rahe hain
-- ISR (In-Sync Replicas)
    - ISR = replicas jo leader ke saath fully synced hain.
    - Example : Leader
                Follower1
                Follower2
    - Agar koi follower slow ho jaye: ISR se remove ho jata hai
-- Leader Election
    - Agar leader crash ho jaye : Kafka automatically new leader choose karega
    - Example : Follower1 → New Leader

## Q25 : What is the purpose of the Idempotent Producer in Kafka?
1. Defination
-- Idempotent Producer ka purpose hai : 
👉 duplicate messages ko prevent karna jab producer retries karta hai.
Kafka ensure karta hai ki:
    Even if producer retries → message topic me sirf ek hi baar store hoga
-- Even if producer retries → message topic me sirf ek hi baar store hoga

2. How Kafka Achieves Idempotency
-- Kafka internally use karta hai:
    - Producer ID(PID) : 
        - Har producer ko Kafka ek unique producer ID deta hai. Example : Producer ID : 78945
    - Sequence Numbers : 
        - Har message ko ek sequence number assign hota hai. Example : Msg1 -> Seq1 , Msg2 -> Seq2 , Msg3 -> Seq3
        - Agar Duplicate Message aaya : Seq 2 again
        - Kafka detect Karega : Duplicate -> Reject
    - Broker Validation : 
        - Broker check karta hai: PID + Sequence Number
        - Agar Duplicate mila : Message Discard

3. Important Configuration
-- Idempotent producer enable karne ke liya : enable.idempotence=true
-- Kafka automatically configure karta hai :    
    acks=all
    retries > 0
    max.in.flight.requests.per.connection <= 5

4. Why Idempotent Producer Important ?
-- Without idempotence:
    - duplicate events
    - incorrect analytics
    - duplicate payments
    - wrong order processing


## Q26 : How does Kafka handle consumer offsets?
1. Defination
-- Kafka me Consumer Offser Ek number hota hai jo batata hai :
👉 consumer ne partition me kaunsa last message read/process kiya hai
-- Matlab: Offset = consumer ka progress tracker
-- Offset = position of a message in a partition
-- Isse Kafka ko pata hota hai : 
    - Next kaunsa message dena hai
    - Crash ke baad processing kaha se resume hogi.

2. Where Kafka Stores Offsets (Important 🔥)
-- Kafka offsets store karta hai special topic me: "__consumer_offsets"
-- ye topic store karta hai : 
    - consumer group id.
    - partition
    - last commited offset.
-- Example record :
    Group : Kitchen-chefs
    Partitions : 0
    Offset : 2

3. Offset Commit Types
-- Auto Commit : 
    - Kafka automatically offset save karta hai.
    - Config : enable.auto.commit = true
    - Example : Chef har 5 seconds me manager ko batata hai : 
         ""Main order #2 tak complete kar chuka hoon""
-- Manual Commit (Best Practice)
    - Application khud decide karta hai kab offset commit karna hai.
    - Example : Order cook hua → then offset commit

4. Why Offsets Are Importnat
-- Offsets Ensure :
    - Crash recovery
    - No Data Loss
    - Controlled Processing

## Q27 : What is the difference between a round-robin partitioner and a key-based partitioner in Kafka?
1. Defination
-- Kafka producer decide karta hai ki message kis partition me jayega.
Iske liye Kafka different partitioning strategies use karta hai.
-- Do Common strategies :
    - Round-Robin Partitioner : messages evenly distribute karta hai
    - Key-Based Partitioner : same key wale messages same partition me bhejta hai

2. Example :
-- Maan lo Resturant me 3 chefs(partitions) hain
    Chefs1 -> Partition 0
    Chefs2 -> Partition 1
    Chefs3 -> Partition 2
-- Order aa rahe hain.
-- Round Robin Partitioner :
    -- Round-robin me order sequentially distribute hota hai.
    -- Example :
        - Orders :
            Order1 → Pizza
            Order2 → Burger
            Order3 → Pasta
            Order4 → Noodles
            Order5 → Soup
        - Distribution :
            Order1 → Chef1
            Order2 → Chef2
            Order3 → Chef3
            Order4 → Chef1
            Order5 → Chef2
        - Visulization : 
            Orders → P0 → P1 → P2 → P0 → P1
-- Key Based Partitioner
    -- Key-based partitioner me message key decide karta hai partition.
    -- Example : Key = Table ID
    -- Key = Table ID
        - Orders : 
            Table1 → Pizza
            Table2 → Burger
            Table1 → Pasta
            Table3 → Soup
            Table2 → Noodles
        - Distribution : 
            Table1 → Chef1
            Table1 → Chef1
            Table2 → Chef2
            Table2 → Chef2
            Table3 → Chef3
        - Visulization
            Key(Table1) → Hash → Partition0
            Key(Table2) → Hash → Partition1
            Key(Table3) → Hash → Partition2


## Q28 : How does Kafka handle message deletion?
1. Defination
-- Kafka messages ko immediately delete nahi karta jab consumer unko read kar leta hai.
-- Instead Kafka retention policies use karta hai jisse decide hota hai:
-- 👉 messages kab delete honge
-- Deletion mainly 2 tarike se hoti hai
    - Time Based retention
    - Size based retention
    - Log compaction (special case)
-- Simple Bolu : Kafka messages tab delete karta hai jab retention rules trigger hote hain.

2. Time-Based Retention : 
-- Config : log.retention.hours
-- Exmaple : log.retention.hours = 168
-- Matlb : 7 days old messages → delete

3. Size-Based Retention
-- Config : log.retention.bytes
-- Example : Topic max size = 10GB
-- Agar size exceed ho gaya: Old segments -> delete

4. Log Compaction (Special Case)
-- Log compaction me Kafka sirf latest value per key retain karta hai.
-- Example :        
    Order#101 → Pizza
    Order#101 → Pizza + Coke
    Order#101 → Pizza + Coke + Dessert
-- Compaction ke baad : 
    Order#101 → Pizza + Coke + Dessert

## Q29 : What is the purpose of the Kafka Mirror Maker?
1. Defination
-- Kafka MirrorMaker ek tool hai jo use hota hai:
-- 👉 Kafka clusters ke beech data replicate karne ke liye
-- MAtlb : Cluster A → data copy → Cluster B
-- Simple Bola : "MirrorMaker = ek Kafka cluster ka data doosre Kafka cluster me copy karta hai."

2. Example : 
-- Maan lo ek restaurant chain hai jiske 2 branches hain:
    - Resturant Delhi
    - Resturant Mumbai
-- Delhi branch me orders aa rahe hain
    - Order1 -> Pizza
    - Order2 -> Burger
    - Order3 -> Pasta
-- Owner chahta hai ki Mumbai branch ko bhi same order mila analytics ke liya.
-- Solution : MirrorMaker
-- Flow : Delhi Orders -> MirrorMaker -> Mumbai Kafka
-- Ab Mumbai system bhi same data read kar sakta hai.

3. Visualization
Kafka Cluster A (Delhi)
        ↓
      Topic: Orders
        ↓
      MirrorMaker
        ↓
Kafka Cluster B (Mumbai)
        ↓
      Topic: Orders

4. Why MirrorMaker Important
-- MirrorMaker mainly use hota hai:
    - Disaster Recovery : 
        - Agar primary Kafka cluster crash ho jaye:
        - Backup Cluster ready hota hai.
    - Multi-Region Architecture
        - US , EU , Asia Kafka Cluster
        - Mirror Maker Ensure karta hai:
        - data sab clusters me avilable ho
    - Data Migration
        - Kabhi kabhi companies:
        - Old Kafka cluster → New Kafka cluster
        - Migration karta hai.
        - MirriMaker Help karta hai live data copy karne me.
    - Load Distribution
        - Production Cluster  , Analytics Cluster
        - MirrorMaker data Copy karta hai taaki analytics system production ko overload na kare.
    
5. How MirrorMaker Works
-- MirrorMaker Internally Use Karta hai :   
    "Kafka Consumer + Kafka Proucer"
-- Process :
    - Source cluster se data read
    - Target cluster me produce
-- Flow : Source Kafka -> Consumer -> MirrorMaker -> PRoducer -> Traget Kafka


## Q30 : How does Kafka handle message versioning?
1. Defination
-- Kafka directly message versioning manage nahi karta.
-- Instead Developer Use karte hain :
    - Schema evolution
    - Schema Registry (Avro / Protobuf / JSON Schema)
    - Backward / Forward Compatibility.
-- Simple Bolu : 
-- Message versioning = jab message structure change ho jaye, system phir bhi old aur new messages ko process kar sake.

2. Example :
-- Maan lo restaurant system me order message ka format hai:
-- Version 1
    OrderID
    Item
    Price
-- Restaurant system upgrade hua.
-- Version 2
    OrderID
    Item
    Price
    TableNumber
-- Problem : Old systems sirf Version 1 samajhte hain.
-- Slution : Kafka ecosystem me Schema Registry + Compatibility Rules use kiye jaate hain.

## Q31 : What is the role of the controller in a Kafka cluster ?
1. Defination
-- Kafka cluster me Controller ek special broker hota hai jo cluster ke administrative decisions handle karta hai.
-- Contrller Ka Kaam
    - Leader election manage karna
    - Broker failures detect karna
    - Partition leadership assign karna
    - Cluster metadata maintain karna
-- Simple bolu:
-- Controller = Kafka cluster ka manager jo decide karta hai kaunsa broker kya kaam karega.

2. Example 
-- Maan lo ek restaurant me multiple kitchens (brokers) hain.
-- Kitchen1 , Kitchen2 , Kitchen3
-- Restaurant owner ek Head Manager appoint karta hai.
-- Ye Manager :
    - decide karta hai kaunsa chef kis order ko handle karega
    - Agar Koi kitchen band ho jaye to backup kitcen activate karega
    - ensure karta hai resturant smoorthy chale
-- Kafka me ye manager hota hai: Controller

3. Visulization
           Kafka Cluster
      Broker1   Broker2   Broker3
         |         |         |
         ---------------------
                |
            Controller
         (Cluster Manager)

4. Important Points
-- Leader Election : 
    - Kafka me har partition ka ek leader broker hota hai.
    - Example : 
        Partition P0
        Leader -> Broker1
        Followers -> Broker2 , Broker3
    - Agar leader crash ho jaye:
        Controller elect karega new leader
    - Example : New Leader → Broker2
-- Broker Failure Detection
    - Controller continuously check karta hai:  
        Kaunsa broker alive hai
        kaunsa broker down ho gaya
    - Restaurant example : 
    - MAnager check karta hai : 
        Chef duty par hai ya nahi
-- Partition Reassignment
    - Agar : 
        - new broker add ho
        - cluster rebalance ho
    - Controller decide karega : "Partitions ka redistribution"
-- Metadata Updates
    - Controller manager karta hai :
        - topic metadata
        - partition leadership
        - replica assignment

5. How Controller Is Selected
-- Kafka cluster me Sirf ek controller hota hai.
-- Controller election automatically hota hai.
-- Old Kafka versions me : 
    zooKeeper controller elect karta tha
-- New Kafka (KRaft model)
    Kafka internally controller elect karta hai.


## Q32 : How does KAfka ensure data consistency ?
1. Defination
-- Kafka data consistency ensure krta hai taaki 
    - sab brokers par same data ho
    - messages correct order me store ho
    - failures ke baad bhi data corrupt ya inconsistent na ho
-- Kafka mainly use karta hai :
    - Replication
    - Leader - Follower model
    - IRS (In-Sync Replicas)
    - Acknowledgements (acks)
    - Idempotent Producers
-- Simple Bolu : "Kafka ensure karta hai ki har partition ka data sab replicas me consistent rahe"

## Q33 : What is the purpose of the Kafka AdminClient API?
1. Defination 
-- Kafka AdminClient API ek API hai jo use hoti hai kafka cluster ko programmatically manage karne ke liya
-- Is API se developers administrative operations perform kar sakte hain, jaise:
    - Topics create karna
    - Topics delete karna 
    - Partitions add karna
    - Broker infomration fetch karna
    - Cosumer groups montior karna.
-- Simple Bolu : AdminClient API = Kafka cluster k manage krane ka programmatic tool.

## Q34 : How does Kafka handle message batching?
1. Defination
-- Kafka message batching use karta hai taaki:
    - network calls kam ho
    - throughput increase ho
    - performance improve ho
👉 Simple bolu:
-- Message batching = multiple messages ko ek saath ek batch me send karna instead of sending them individually.

2. Example 
-- Maan lo restaurant me waiter kitchen ko orders bhej raha hai.
-- Order :
    - Order1 → Pizza
    - Order2 → Burger
    - Order3 → Pasta
    - Order4 → Soup
-- Without Banching
    - Waiter har order individually kitchen me le jata hai.
        Order1 → Kitchen
        Order2 → Kitchen
        Order3 → Kitchen
        Order4 → Kitchen
    - Problem 
        - Time Waste
        - Unncessary Trips
-- With Batching
    - Waiter ek tray me multiple orders le jata hai.
        "Batch1 → Pizza + Burger + Pasta + Soup"
    - Ek hi trip me sab orders kitchen me pahunch gaye
    - Result : 
        - Fast Processing
        - Less Overhead
    
3. How Kafka Producer Performs Batching
-- Producer internally messages ko memory buffer me collect karta hai.
-- Batch crate hota hai per partition.
-- Flow : 
    Producer
   ↓
    Buffer (Batch)
   ↓    
    Batch full / timeout reached
   ↓
    Send to Kafka broker

4. Important Configuration
-- batch.size
    - Maximum batch size
    - Example : batch.size = 16KB
    - Matlab batch me itna data collect hona tak wait karega
-- linger.ms
    - Producer kirni der wait kare before sendign batch
    - Example : linger.ms = 5ms
    - Producer 5 ms wait karega aur messages accumulate karega.

5. buffer.memory
-- Producer ka total memory buffer.
-- Example : buffer.memory = 32 mb

6. Benefits of Message Batching
-- Kafka batching se :
    - network overhead reduce hota hai.
    - throughput increase hota hai.
    - latency optimize hoti hai.
-- Large-scale systems me batching perfoemce performance drastically improve karti hai. 


## Q35 : What is the difference between a Kafka consumer and a Kafka streams application?
1. Defination
-- Kafka Consumer
    - Kafka Consumer ek application hoti hai jo:
    - 👉 Kafka topic se messages read (consume) karti hai.
    - Simple bolu: Consumer = sirf messages read karta hai.
-- Kafka Streams Application
    - Kafka Streams ek stream processing application hoti hai jo
    - Kafka se messages read karti hai
    - unko process / transform / aggregate karti hai
    - aur result dobara Kafka topic me write karti hai
    - Simple : Kafka Steams = read + Process + write pipiline

## Q36 : How does Kafka handle message ordering within a partition?
1. Defination
-- Kafka message ordering guarantee karta hai within a partition.
-- Matlab : 
    - Jo messages producer send karta hai
    - Kafka unko same order me store aur deliver karta hai
-- Ye possible hota hai kyunki Kafka partition ek append-only log hota hai.
-- Simple bolu: Partition ke andar messages hamesha sequential order me store hote hain.

2. Why Ordering Works in Kafka
-- Kafka ordering maintain karta hai kyunki:
-- Append-Only Log
    - Partition me messages end me append hote hain.
    - Example : 
        Msg1 -> append
        Msg2 -> append
        Msg3 -> append
    - Isse order break nahi hota.
-- Offset Numbers
    - Har message ko ek offset number milta hai.
    - Example : 
        Offset 0 -> Pizza
        Offset 1 -> Burget
        Offset 2 -> Pasta
    - Consumer offset order me hi read karta hai
-- Single Leader Writes
    - Har partition ka sirf ek leader broker hota hai.
    - Rule : Writes -> leader par hi allowed
    - Isse write conflicts avoid hote hain. 

## Q37 : What is the purpose of the Kafka Transactions API?
1. Defination
-- Kafka Transactions API use hoti hai taaki multiple messages ko ek atomic operation me process kiya ja sake.
-- Matlab : 
    Ya to sab messages commit honge
    Ya koi bhi nahi hoga
-- Simple Bolu : Transactions API = Kafka me atomic write + exactly-once processing ensure karta hai.

2. Example :
-- Customer order karta hai:
    Order#200
    Pizza
    Burger  
    Drink
-- Kitchen Rule
    Agar order ka ek item fail ho gaya
    To poora order cancel
-- Possible Cases : 
    ✅ All items prepared → order complete
    ❌ Burger unavailable → poora order cancel
    Exactly ye hi kafka transcation karta hai.

3. Why Transcation Important
-- Transcation ensure : 
    - Exactly once processing
    - Multiple topic writes consistency
    - No partial writes.


## Q38 : How does Kafka handle message key hashing?
1. Defination
-- Kafka message key ka hash calculate karta hai taaki decide kare:
    "Message kis partition me jayega"
-- Formula :
    "Partition = hash(Key) % number_of_partitions"

2. Example 
-- Restaurant me 3 chefs (partitions) hain.
    - Chef1 -> partiton0
    - Chef2 -> Partiton1
    - Chef3 -> Partiton2
-- Orders table ID se hash hote hai.
-- Example : 
    Table5 → Hash → Partition1
    Table5 → Hash → Partition1
    Table5 → Hash → Partition1
-- Result : 
    Same table ke orders same chef ko milte hain.

3. Why Key Hashing Important
-- Key hashing ensure karta hai :
    - Ordering per key
    - Consistent partiton assignment
    - Load balancing

## Q39 : What is the role of the Kafka consumer coordinator?
1. Defination
-- Consumer Coordinator ek broker hota hai jo consumer group operations manage karta hai.
-- Responsibilities:
    - consumer group membership track karna
    - partitions assign karna
    - rebalancing trigger karna
    - offset commits manage karna
👉 Simple bolu: Consumer Coordinator = consumer group ka manager.

## Q40 : How does Kafka handle message timestamps?
1. Definition
-- Kafka har message ke saath timestamp store karta hai.
-- Timestamp help karta hai:
    - event ordering
    - retention policies
    - time-based processing

2. Types of Timestamps
-- Kafka me 2 types hote hain  :
-- CreateTime :
    - Producer jab message send karta hai tab timestamp set hota hai.
    - Example : Producer -> Msg -> Timestamp = send time
-- LogAppendTime
    - Broker Jab message recieve karta hai timestamp
    - Example : Broker receive time = timestamp

## 41 : What is the purpose of the Kafka Quota API?
1. Defination
-- Kafka Quota API ka purpose hai : 
-- Kafka cluster me resource usage control karna
-- taaki koi single client system ko overload na kare.
-- Kafka quotas limit karte hain:
    -- Producer throughput
    -- Consumer throughput
    -- Request Rate
-- Simple Bolu  : Kafka Quota API = traffic control system jo ensure karta hai ki sab clients fair tareeke se resources use karein.

2. Example :
-- Maan lo ek restaurant me multiple customers orders de rahe hain.
-- Agar ek customer bole : 
    - 100 pizzas
    - 100 burgers
    - 100 frinks
-- To kitchen overload ho jayega
-- Resturanrt manager rule banata hai :
    "Ek customer ek time me max 10 orders hi place kar sakta hai"
-- Isse kya hoga :
    -- Kitchen Overload nahi hoga
    -- Sab customers ko fair service milegi
-- Kafka me ya role play krta hai : Quota API.

## 42 : How does Kafka handle message acknowledgments?
1. Defination
-- Kafka me message acknowledgment (ACK) ka matlab hai:
👉 Broker producer ko confirm karta hai ki message successfully receive aur store ho gaya hai
-- Producer decide karta hai ki kitni confirmation chahiyee using acks configuration
-- Simple Bolu : ACK = confirmation ki message Kafka me safely store ho gaya.
 
2. Types L 
-- acks = 0
    - Producer confirmation wait nahi karta.
    - Flow : Waiter → Order kitchen ko diya → turant chala gaya
    - Risk : Order Loss ho skta hai 
    - Advantage : Fast Performance
-- acks = 1
    - Producer leader broker se confirmation wait karta hai.
    - Flow  : Producer → Leader Broker
                Leader store karta hai → ACK send karta hai
    - Risk : Agar leader crash ho gaya before replication → data loss possible.
-- acks = all (or -1)
    - Producer wait karta hai jab tak all in-sync replicas confirm na kar dein.
    - Flow  : Producer -> Leader Broker -> Followers replicate -> ACK send
    - Result : highest reliability  , slightly Slow.


## 43 : How does Kafka handle message acknowledgments?
1. Defination
-- Kafka me message acknowledgment (ACK) ka matlab hai:
👉 Broker producer ko confirm karta hai ki message successfully receive aur store ho gaya hai
-- Producer decide karta hai ki kitni confirmation chahiyee using acks configuration
-- Simple Bolu : ACK = confirmation ki message Kafka me safely store ho gaya.
 
2. Types L 
-- acks = 0
    - Producer confirmation wait nahi karta.
    - Flow : Waiter → Order kitchen ko diya → turant chala gaya
    - Risk : Order Loss ho skta hai 
    - Advantage : Fast Performance
-- acks = 1
    - Producer leader broker se confirmation wait karta hai.
    - Flow  : Producer → Leader Broker
                Leader store karta hai → ACK send karta hai
    - Risk : Agar leader crash ho gaya before replication → data loss possible.
-- acks = all (or -1)
    - Producer wait karta hai jab tak all in-sync replicas confirm na kar dein.
    - Flow  : Producer -> Leader Broker -> Followers replicate -> ACK send
    - Result : highest reliability  , slightly Slow.

## 44 : How does Kafka handle message serialization and deserialization?
1. Defination
-- Kafka messages byte format (binary data) me store karta hai.
-- Isliye jab application data bhejti hai ya read karti hai to:
    Serialization → object ko bytes me convert karna
    Deserialization → bytes ko original object me convert karna

2. Visualization
Producer Application
        ↓
   Serialization
        ↓
      Bytes
        ↓
     Kafka Broker
        ↓
     Bytes
        ↓
   Deserialization
        ↓
Consumer Application

3. Why Serialization Needed
-- Kafka language -independent system hai.
-- Example :
    Producer - Java
    Consumer - Python
-- Serialization ensure karta hai ki different languages data exchange kar sakein.


## 45 : What is the purpose of the Kafka Schema Registry?
1. Defination
-- Kafka Schema Registry ek service hai jo Kafka messages ke schemas (data structure definitions) ko manage karta hai.
-- Iska main Purpose 
    - Message structure define karna 
    - schema version track karna
    - producer aur consumer ke beech compatibility maintain karna
-- Simple Bolu : Schema Registry = Kafka messages ka structure manager.

2. Example
-- Maan lo restaurant me order format defined hai.
-- Order Structure
    - OrderId
    - Item
    - Price
    - Tablenumber
-- Ye order format rulebook hai jise kitchen aur billing system dono follow karte hain.
-- Agar Koi Waiter order bheje :
    OrderID : 501
    Item : Pizza
    Price : 300
    Table : 5
-- Kitchen easily samajh jayega kyunki format same hai
-- Ye rulebook Kafka me hoti hai:   Schema Registry

3. Compatibility Types
-- Schema Registry Support Karta hai :
    - Backward Compatibility : New consumers old messages read kar sakte hain.
    - Forward Compatibility : Old Consumer new messages read kar sakte hain
    - Full Compatibility : Old Aur new systems dono compatible rehte hain.



## 46 : How does Kafka handle topic deletion?
1. Definition
-- Kafka me topic deletion ka matlab hai
👉 poora topic aur uske saare partitions ka data permanently remove karna.
-- Topic delete hone par:
    topic metadata remove ho jata hai
    log files (messages) delete ho jate hain
    consumers topic read nahi kar sakte
👉 Simple bolu : Topic deletion = Kafka se poora message stream hata dena.

2. How Topic Deletion Works Internally
-- Step 1 : Admin Request Bhejta Hia 
    "deleteTopic(topicName)"
-- Step 2 : Controller broker request receive karta hai.
-- Step 3 : Controller sab brokers ko instruct karta hai:
    "Delete topic partitions"
-- Step 4 : Kafka brokers : 
    - Kafka brokers :
        - partition log files delete karte hain
        - metadata remove karte hain
    - Topic permanently remove ho jata hai.

3. Important Configuration : "delete.topic.enable=true"

## 47 : What is the difference between a Kafka consumer's poll() and subscribe() methods?
1. Defination
-- Kafka consumer me subscribe() aur poll() dono important methods hain, lekin unka role alag hota hai.
👉 Simple difference:
-- Method	          Purpose
    subscribe()	      Consumer ko topic se connect karna
    poll()	          Kafka se messages fetch karna
-- Matlab : 
    subscribe() → topic join karo
    poll() → messages read karo

2. Example 
-- Maan lo restaurant me chefs (consumers) ka system hai.
-- Topic: FoodOrders
-- Chef ko pehle decide karna padega ki kaunsi order category handle karega.
-- Step 1 : subscribe()
    -- Chef manager ko bolta hai: "Mujhe FoodOrders section me kaam karna hai"
    -- Ye process kafka me hota hai :
        "consumer.subscribe(List.of("FoodOrders"))"
    -- Is step ke baad chef order queue ka member ban gaya.
-- Step 2 : poll()
    -- Ab chef actual orders lene lagta hai.
        - Order1 -> Pizza
        - Order2 -> Burger
        - Order3 -> Pasta
    -- Kafka me : consumer.poll(Duration.ofMillis(100));

# Interview Question From Chat GPT
## Kafka Fundamentals (Must Know – 100% Asked)
What is Apache Kafka?
Why is Kafka used instead of traditional message queues?
What are the key components of Kafka?
What is a Topic in Kafka?
What is a Partition in Kafka?
What is a Broker in Kafka?
What is a Kafka Cluster?
What is the role of Apache ZooKeeper in Kafka?
What is the role of the Kafka Controller?
What is the difference between Producer and Consumer?

## Producer Concepts
What is the Kafka Producer API?
How does Kafka send messages to partitions?
What is the difference between Round-Robin and Key-based partitioning?
What is message key hashing in Kafka?
How does Kafka handle message batching?
What is the role of the acks configuration?
What is the Idempotent Producer?
How does Kafka ensure exactly-once delivery?
How does Kafka handle message serialization?
What serializers are commonly used in Kafka?

## Consumer Concepts
What is a Kafka Consumer?
What is a Consumer Group?
What is the role of the Consumer Coordinator?
What is the difference between subscribe() vs assign()?
What is the difference between subscribe() vs poll()?
How does Kafka handle consumer offsets?
Where are offsets stored in Kafka?
What happens if a consumer crashes?
What is consumer lag?
How do you monitor consumer lag?

## Partitioning & Ordering
How does Kafka maintain message ordering?
Why is ordering guaranteed only within a partition?
How does Kafka assign partitions to consumers?
What happens when partitions are more than consumers?
What happens when consumers are more than partitions?

## Replication & Fault Tolerance
How does Kafka ensure fault tolerance?
What is Replication Factor?
What are Leader and Follower replicas?
What are In-Sync Replicas (ISR)?
What happens when a leader broker fails?
How does Kafka ensure high availability?
What is the role of the Controller in leader election?

## Storage & Data Management
How does Kafka store messages on disk?
What are log segments?
What is data retention in Kafka?
What is log compaction?
How does Kafka delete messages?
How does Kafka delete topics?
What are message timestamps?

## Kafka APIs & Ecosystem
What is the purpose of the Kafka Connect API?
What is Apache Kafka Streams?
What is the difference between Kafka Streams and Apache Flink?
What is the AdminClient API?
What is the Kafka Transactions API?
What is the Kafka Quota API?

## Schema & Data Compatibility
What is the purpose of the Confluent Schema Registry?
What is schema evolution?
What is backward compatibility?
What is forward compatibility?
How does Kafka handle message versioning?

## Cluster Operations & Scaling
How does Kafka support scalability?
What happens when a new consumer joins a group?
What is Kafka Rebalancing?
What causes rebalancing?
How can rebalancing impact performance?
## Multi-Cluster & Replication
What is the purpose of Kafka MirrorMaker?
What is MirrorMaker2?
Why do companies use multi-region Kafka clusters?
## Production / Real-World Questions (Very Common)
How do you monitor Kafka in production?
How do you handle slow consumers?
How do you avoid message duplication?
How do you tune Kafka producer performance?
What are common Kafka bottlenecks?
How do you scale Kafka clusters?
How do you handle large messages in Kafka?
## System Design / Senior Level Kafka Questions
Design a real-time order processing system using Kafka
Design a log aggregation system using Kafka
How would you design a real-time analytics pipeline using Kafka?
How would you ensure exactly-once processing in a distributed system?
How would you scale Kafka to millions of messages per second?

💡 Suggestion for you (since you’re preparing seriously):

Next best step is learning 10 Kafka concepts deeply, because interviewers focus on these most:

Kafka Architecture
Consumer Groups
Rebalancing
ISR
Offsets
Partitioning
Replication
Exactly Once Processing
Schema Registry
Consumer Lag