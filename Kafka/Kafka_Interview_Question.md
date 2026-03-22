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

## Q22 : How does Kafka handle message size limits?

## Q23 : What is the role of the group coordinator in Kafka?

## Q24 : How does Kafka handle data replication?

## Q25 : What is the purpose of the Idempotent Producer in Kafka?

## Q26 : How does Kafka handle consumer offsets?

## Q27 : What is the difference between a round-robin partitioner and a key-based partitioner in Kafka?

## Q28 : How does Kafka handle message deletion?

## Q29 : What is the purpose of the Kafka Mirror Maker?

## Q30 : How does Kafka handle message versioning?