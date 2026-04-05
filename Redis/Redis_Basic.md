# Redis Fundamentals
## 1. What is Redis ?
0. Golden Line 
"Redis is an in-memory key-value store that provides sub-millisecond latency, making it ideal for caching, session management, and real-time applications."

1. Simple Explanation 
-- Socho tumhare paas ek magic notebook hai jo bahut fast kaam karta hai.
-- Jab bhi tumhe kuch yaad karna hota hai — tum us notebook mein likh do, aur jab chahiye turant mil jaata hai!
-- Normal database ek almaari ki tarah hai — dhundna padta hai, time lagta hai. Lekin Redis ek dimag ki tarah hai — sab kuch yaad rehta hai, instantly milta hai! 🧠⚡

2. Technical Explanation
-- Redis = Remote Dictionary Server
-- Redis ek open-source, in-memory data structure store hai jo use hota hai as a:
    - Cache (temp fast storage)
    - Database
    - Message Broker

3. Key Points:
-- Storage : RAM mein store hota hai (disk nahi)
-- Speed : ~100,000 ops/sec — extremely fast
-- DataTypes : String, List, Set, Hash, ZSet
-- Language : C mein likha gaya hai

4. Example
-- Socho ek Busy restaurant hai :
    - Chef = Your Application
    - Menu Book (almaari mein) = MySQL Database → dhundne mein time lagta hai
    - Waiter ki yaaddasht / pocket notepad = Redis → instantly yaad hai!
-- Jab 100 log ek saath "Common Item" order karte hain — Waiter baar baar kitchen ki recipe book (MySQL) nahi dekhta.
-- Usne Sab Common Items padh ke yaad kar liya (Redis Cache) — ab instantly bata deta hai! (Rate)

5. Important
✅ Redis = In-Memory → RAM mein hota hai isliye fast hai
✅ Redis = Single Threaded → ek kaam ek time pe, but still blazing fast
✅ Redis supports Persistence → RDB & AOF (data loss nahi hoga)
✅ Redis ≠ Only Cache → Full database bhi ban sakta hai
✅ Redis is NOT relational → SQL nahi chalega
✅ Used by: Twitter, GitHub, Instagram, Stack Overflow


## 2. Why is Redis Called an in-memory database?
1. Simple Explanation 
-- Socho tumhare ghar mein 2 jagah hain cheezein rakhne ke liye:
    - 🎒 School Bag → Jo cheez abhi chahiye, woh bag mein rakho — turant milti hai!
    - 🏠 Store Room → Purani cheezein wahan hain — dhundna padta hai, time lagta hai!
-- Redis =  School Bag (RAM) → Sab kuch haath mein ready!
-- MySQL = Store Room (Disk/HDD) → Dhundne jaana padta hai!
-- Isliye Redis ko in-memory kehte hain — kyunki woh RAM (memory) mein kaam karta hai, hard disk mein nahi! ⚡

2. Technical Explanation
-- Normal Database vs Redis — Kahan store hota hai data?
    Traditional DB (MySQL, PostgreSQL)
    ──────────────────────────────────
    Application → Query → 💾 DISK → Result
                         ↑
                    Slow! (5-10ms+)
    ...................................
    Redis
    ──────────────────────────────────
    Application → Query → 🧠 RAM → Result
                        ↑
                  Super Fast! (<1ms)
-- RAM vs Disk — Speed Difference:
    Storage     Speed       Latency
    HDD         ~100 MB/s    ~10ms
    SSD         ~500 MB/s    ~0.1ms
    RAM         ~50 GB/s     ~0.0001ms
-- RAM, Disk se 100,000x faster hoti hai! Isliye Redis itna fast hai!
-- Techincally Kya Hota Hai?
    - Jab Redis start hota hai → Saara data RAM mein load ho jaata hai
    - Jab tum GET/SET karte ho → Directly RAM se read/write hota hai (Disk ko touch nahi karta normally)
    - Result → Sub-millisecond response! ⚡

3. Example
-- Socho restaurant mein 2 types ke recipes hain:
-- 📚 Normal Database (MySQL) = Recipe Book in Store Room
    - Customer ne order kiya Unknown Item "Paneer Makhni"
        → Chef gaya store room mein
        → Book dhundi
        → Page dhundha
        → Recipe padhi
        → Aaya wapas
        ⏱️ Time: Zyada laga!
-- 🧠 Redis (In-Memory) = Chef ke Dimaag mein Yaad!
    - Customer ne order kiya "Paneer Tikka"
        → Chef ko ALREADY yaad hai recipe!
        → Turant shuru kar diya!
        ⚡ Time: Almost Zero!

4. Important Interview Points
-- But agar server band ho gaya toh data kho jayega?
    - Redis ke paas 2 Persistence Options hain:
        1. RDB (Redis Database Backup)
           → Har kuch minutes mein snapshot leta hai disk pe
           → Jaise photo khichna! 📸
        2. AOF (Append Only File)
           → Har operation log hota hai disk pe
           → Jaise diary likhna! 📔
-- Toh Redis pure in-memory hai ya disk bhi use karta hai?
    - Primary Storage -> RAM  (fast access ke liye)
    - Backup/Persist   → Disk (data save rakhne ke liye)

## 3. What Problem Does Redis Solves?
1. Simple Explanation
-- Socho tumhari school canteen hai aur 500 bacche ek saath lunch ke liye aate hain! 😱
-- Agar ek hi cook hai jo har baar fresh banana shuru kare — toh kya hoga?
    - Sabko wait karna padega ⏳
    - Canteen slow ho jayegi
    - Bacche bhooke rahenge 😭
-- Solution? → Subah se hi khana bana ke ready rakh do!
Jab baccha aaye → turant do! 
-- Yahi kaam Redis karta hai! — Pehle se data ready rakhta hai, baar baar banana nahi padta!

2. Technical Explanation
-- Problem 1: Slow Database Queries
    - Without Redis:
      ──────────────
      User Request → Database Query → Disk Read → Response
                                   ↑
                              10-100ms lagta hai
                         (1000 users = server cry 😭)
      ...............................................
    - With Redis:
      ──────────────
      User Request → Redis Cache → Response
                   ↑
              <1ms lagta hai ⚡
              (1000 users = No problem! 😎)
........................................................................ 
--  Problem 2: Database Overload (Too Many Requests) 
    Without Redis:
    ──────────────
    1,000,000 users → MySQL → 💥 CRASH!
    (Database pe bohot zyada load)
    ................
    With Redis:
    ──────────────
    1,000,000 users → Redis (90% requests handle)
                     ↓
                  MySQL (sirf 10% requests)
                  → No Crash! ✅
.........................................................................
-- Problem 3 : Session Management
    Without Redis:
    ──────────────
    User login karta hai → Session disk mein save
    Next request → Disk se session dhundho → Slow!
    ..............................
    With Redis:
    ──────────────
    User login karta hai → Session RAM mein save
    Next request → Instantly milta hai → Fast! ⚡
.....................................................................
-- Problem 4: Real-Time Features
    Without Redis:
    ──────────────
    Live scoreboard → Har second DB query → Slow & Expensive
    ...............
    With Redis:
    ──────────────
    Live scoreboard → Redis mein update → Instant! ⚡
    (Sorted Sets use karta hai ranking ke liye)
.........................................................................
-- Problem 5: Message Queue / Pub-Sub
    Without Redis:
    ──────────────
    Service A → Direct call → Service B
    (Agar B down hai → Message lost! 😭)
    ..............
    With Redis:
    ──────────────
    Service A → Redis Queue → Service B
    (B down bhi ho → Message safe rehta hai! ✅)

3. Important Points
-- 🚀 CACHING
   → Slow DB queries ko fast banao
   → Most common use case!
   → Example: Product details, User profiles
.........................................
-- 👤 SESSION MANAGEMENT
   → User login sessions store karo
   → Fast aur scalable
   → Example: E-commerce cart, Auth tokens
.........................................
-- 📊 REAL-TIME LEADERBOARDS
   → Sorted Sets use karta hai
   → Example: Gaming scores, Live rankings
.........................................
-- 📨 MESSAGE QUEUE / PUB-SUB
   → Services ke beech communication
   → Example: Notifications, Email queue
..........................................
-- 🔢 RATE LIMITING
   → Ek user kitni baar request kar sakta hai
   → Example: API rate limiting (10 req/sec)
..........................................
-- ⏰ EXPIRY / TTL
   → Data automatically delete ho jaata hai
   → Example: OTP (5 min ke baad expire)


## 4. What is Difference between Redis and tradition databases?
1.  Simple Explanation
-- Socho tumra 2 dost hain:
-- Redis = Raju (Bahut Smart Dost)
    - Sab kuch dimag mein yaad rakhta hai
    - Koi bhi sawaal poocho → turant jawab! ⚡
    - Lekin... agar woh so jaye → sab bhool sakta hai 😴
    - Uske paas limited dimag hai (RAM costly hai)
-- Traditional DB = Sanju (Mehnati Dost)
    - Sab kuch diary mein likhta hai (disk)
    - Jawab dhundne mein time lagta hai ⏳
    - So jaye toh bhi → diary safe rehti hai! ✅
    - Diary mein unlimited pages hain (disk cheap hai)
-- Dono ki apni jagah hai! Fast chahiye → Raju (Redis) Safe & Permanent → Sanju (Traditional DB)

2. Technical Explanation
Feature             Redis 🔴            Traditional DB 🗄️
..................................................................
Storage             RAM(Memory)          Disk
Speed               ~0.1ms               ~10 - 100ms
Data Model          Key-Value            Tables(Rows and Cols)
Query Language      Redis Commands       SQL
Scalability         Horizontal ✅        Vertical (mostly)
Persistence         Option(RDB/AOF)      Always
Data Size           Limited (RAM Size)   Unlimited(Disk)
ACID                Partial              Full
Use Case            Cache, Realtime      Permanent Storage
Cost                RAM = Expensive      Disk = Cheap

3. Speed Comparison -  Internaly Kya Hota Hai?
-- Traditional Database Flow:
    User Request
    ↓
    SQL Query Parse
    ↓
    Query Optimizer
    ↓
    💾 Disk Read (Slow I/O)     ← Main bottleneck!
    ↓
    Data Load in Memory
    ↓
    Response
    ⏱️ Total: 10ms - 500ms
-- Redis Flow:
    User Request
    ↓
    Key Lookup
    ↓
    🧠 RAM Read (Already in Memory!)  ← Super Fast!
    ↓
    Response
    ⏱️ Total: 0.1ms - 1ms

4. ACID Properties - Kya Farq Hai?
-- ACID = Atomicity, Consistency, Isolation, Durability
-- DB
    ✅ Atomicity   → Full transaction ya kuch nahi
    ✅ Consistency → Data hamesha valid state mein
    ✅ Isolation   → Transactions ek doosre ko affect nahi karte
    ✅ Durability  → Data hamesha safe (disk pe)
-- Redis 
    ✅ Atomicity   → Single commands atomic hain
    ⚠️ Consistency → Basic level pe
    ⚠️ Isolation   → Limited (MULTI/EXEC se partial)
    ⚠️ Durability  → Optional (RDB/AOF enable karo)

5. Example
-- Traditional DB = Restaurant ka RECORD ROOM
    → Saare bills, orders, customer history yahan hai
    → Permanently store hota hai
    → Dhundne mein time lagta hai
    → "2019 mein Rahul ne kya khaya tha?" → Mil jayega! ✅
    → Har cheez organized tables mein hai
-- Redis = HEAD WAITER ki MEMORY
    → Aaj ke popular orders yaad hain
    → Current table status yaad hai
    → Live token numbers yaad hain
    → Bahut fast response deta hai ⚡
    → Restaurant band ho → sab bhool sakta hai 😴
-- Real Workflow in Restaurant:
    Customer: "Mera order kahan hai?"
    ↓
    Waiter pehle HEAD WAITER se poochta hai (Redis)
    ↓
    Agar yaad hai → Turant bata diya! ⚡
    ↓
    Agar yaad nahi → Record Room jaata hai (MySQL)
    ↓
    Record Room se laaya → Ab HEAD WAITER ko bhi
                        bata diya (Cache Update)


6. Important Interview Points
-- Toh Redis Traditional DB ko replace kar sakta hai?
    ❌ NAHI! Redis replacement nahi hai!
    ✅ Redis COMPLEMENT karta hai Traditional DB ko!
    Redis = Speed Layer(fast access)
    MySql = Truth Layer(Permanent storage)
     Dono milke kaam karte hain!
-- Kab Redis use karo, Kab Traditional DB?
    - Use Redis When: ✅
        → Caching chahiye
        → Session store karna hai
        → Real-time data chahiye
        → Rate limiting karna hai
        → OTP/Temporary data store karna hai
        → Leaderboards banana hai
    - Use Traditional DB When:
        → Permanent data store karna hai
        → Complex queries/joins chahiye
        → Financial transactions hain
        → ACID compliance chahiye
        → Large data store karna hai
        → Reporting/Analytics karna hai

## 5. Why Redis is so fast?
1. 6 Reasons
┌─────┬──────────────────────────┬─────────────────────────┐
│  #  │        Reason            │        Benefit          │
├─────┼──────────────────────────┼─────────────────────────┤
│  1  │ In-Memory Storage        │ 100,000x faster than HDD│
│  2  │ Single Threaded          │ No locks, no switching  │
│  3  │ Simple Data Structures   │ O(1) operations mostly  │
│  4  │ Non-Blocking I/O         │ Handles millions req/sec│
│  5  │ RESP Protocol            │ Lightweight networking  │
│  6  │ No Query Parsing         │ Direct key-value access │
└─────┴──────────────────────────┴─────────────────────────┘
2. Interview Triks
-- Q : Redis single threaded hai toh slow hoga na?
-- A : Nahi! Kyunki Redis ka bottleneck CPU nahi,MEMORY aur NETWORK hai!
        - Single thread = No context switching overhead
        - In-memory = No disk I/O wait
        - Non-blocking I/O = No thread blocking
        - Isliye single thread hone ke bawajood
        - Redis 100,000+ operations/second handle karta hai!" ✅

3. Redis Performace Number
Redis Performance:
──────────────────
→ 100,000 - 1,000,000 ops/second
→ Latency: < 1 millisecond
→ Single instance handles millions of users
→ Memory efficient: 1M keys ≈ ~100MB RAM


## 6. What are the main use cases of Redis?
- Use Redis When: ✅
        → Caching chahiye
        → Session store karna hai
        → Real-time data chahiye
        → Rate limiting karna hai
        → OTP/Temporary data store karna hai
        → Leaderboards banana hai

## 7. What is difference between Redis and Memcached?
1. Simple Explanation
-- 📦 Memcached = Simple Tiffin Box
    - Sirf roti aur sabzi rakh sakte ho (simple strings only)
    - Bahut lightweight hai
    - Bas khana rakhna aur nikalna — kuch aur nahi!
    - Agar tiffin gir gaya → sab kuch gir gaya! 😭
    - Multiple compartments nahi — ek hi jagah sab!
--  🎒 Redis = Smart School Bag
    - Bahut saari cheezein rakh sakte ho!
    - Alag alag pockets hain (different data types)
    - Lock bhi hai (persistence) — gir bhi gaya toh safe! ✅
    - Diary, tiffin, water bottle, compass box — sab kuch! 🎯
-- Dono fast hain — lekin Redis bahut zyada capable hai!

2. Comparison
Feature             Redis                   Memcached
.............................................................
Data Types          String,List,Hash,Set    Sirf String
Persistence         RDB And AOF             Nahi
Replication         Master-Slave            Nahi
Clustering          Build In                Limited
Pub/Sub             Yes                     Nahi
Lua Scripting       Yes                     Nahi
Transcations        MULTI/EXEC              Nahi
Threading           Single Threaded         MultiThreaded
Max Key Size        512 MB                  250 Bytes
Max Value Size      512 MB                  1 MB
Memory usage        Thoda zyada             Thoda Kam
Speed               Expermelly Fast         Extermely Fast
Use Case            Cache + Must More       Sirf Simple Cache

3. Data Types -- Sabse Bada Difference
-- Memcached
    ✅ String → "Hello"
    ❌ List   → Not supported
    ❌ Hash   → Not supported
    ❌ Set    → Not supported
    ❌ ZSet   → Not supported
    - Sirf ek type → Sirf simple caching! 😐
-- Redis:
    ✅ String  → "Hello"           → Simple values
    ✅ List    → [1, 2, 3]         → Queue/Stack
    ✅ Hash    → {name: "Rahul"}   → Object storage
    ✅ Set     → {A, B, C}         → Unique items
    ✅ ZSet    → {A:1, B:2, C:3}   → Leaderboards
    - 5 types → Unlimited possibilities! 

4. Persistence — Data Safety:
-- Memcached 
    Server restart/crash
    ↓
    💥 Saara data GONE!
    RAM flush → Kuch nahi bachta!
    No backup, No recovery! 😭
-- Redis :
    erver restart/crash
    ↓
    ✅ RDB Snapshot → Data recover ho jaata hai!
    ✅ AOF Log      → Har operation save hota hai!
    Restart ke baad → Sab wapas! 😎

5. Threading Model — Interesting Difference!
-- Memcached (Multi-Threaded):
    Request 1 → Thread 1 ┐
    Request 2 → Thread 2 ├→ Parallel process
    Request 3 → Thread 3 ┘
        ↓
    Multiple CPU cores use kar sakta hai
    Good for: Multi-core servers pe simple caching
-- Redis (Single-Threaded):
    Request 1 ┐
    Request 2 ├→ Single Thread → Queue mein process
    Request 3 ┘
        ↓
    No locking overhead
    No race conditions
    Good for: Complex operations, data integrity
-- ❓ Toh kaun faster hai?
    → Simple GET/SET pe: Almost SAME speed!
    → Complex operations pe: Redis wins! 🏆

6. Example :
-- Memcached = SIMPLE NOTICE BOARD
    - Restaurant mein ek simple notice board hai
        → Sirf simple notes chipka sakte ho (strings)
        → "Today's Special: Butter Chicken"
        → Agar board gir gaya → sab notes gone! 😭  
        → Koi backup nahi
        → Sirf read/write — kuch aur nahi
        → Fast hai — but limited! 😐
-- Redis = SMART MANAGER SYSTEM
    - Restaurant mein ek smart manager hai jiske paas:
        → 📝 Notes (Strings)     → "Today's special"
        → 📋 Order List (List)   → Queue of orders
        → 👤 Customer Cards(Hash)→ Customer details
        → ⭐ VIP Members (Set)   → Unique customers
        → 🏆 Top Customers (ZSet)→ Loyalty rankings
        → Backup bhi hai (Persistence) ✅
        → Dusri branch ko copy bhi milti hai (Replication) ✅
        → Announcements bhi kar sakta hai (Pub/Sub) ✅
-- Work Flow : 
    - Simple caching chahiye ?
        → Doo kaam karenge
    - Leaderboard, Queue, Session, Pub/Sub chahiye?
        → Sirf Redis! 🔴

7.  Important Interview Points
-- Use Memcached When : 
    ✅ Sirf simple string caching chahiye
    ✅ Multi-threaded performance priority hai
    ✅ Bahut simple use case hai
    ✅ Memory efficiency priority hai
    ✅ Legacy system already use kar raha hai
    ✅ Team ko simple solution chahiye
-- Use Redis When:
    ✅ Complex data types chahiye
    ✅ Data persistence chahiye
    ✅ Pub/Sub messaging chahiye
    ✅ Leaderboards/Rankings chahiye    
    ✅ Transactions chahiye 
    ✅ Replication/Clustering chahiye
    ✅ Session management chahiye
    ✅ Rate limiting chahiye
    ✅ Almost ALWAYS! 😎

## 8. How Does Redis store data internally?
1. Simple Explanation 
-- Socho tumhare paas ek magic cupboard hai:
    - Har drawer pe ek naam (key) likha hai
    - Drawer ke andar kuch bhi rakh sakte ho (value)
    - Koi bhi cheez chahiye → naam dekho → turant nikalo! ⚡
        🗄️ Magic Cupboard (Redis)
        "user:1"  →  "Rahul"
        "user:2"  →  "Priya"
        "score"   →  "950"
    - Bas itna simple hai! Key → Value!

2. Techincal Explanation
-- Redis = Giant Key-Value Store in RAM
        SET name "Rahul"
        GET name → "Rahul"
        Key    →    Value
        "name" →   "Rahul"
-- Internally 3 Cheezein Hoti Hain:
    1. HASH TABLE (Main Dictionary)
        - Har key ek Hash Table mein store hoti hai:
        - "user:1" ──→ Hash Function ──→ Index ──→ Value
                                ↑
                            Instant access!
                              O(1) ⚡
    2. REDISOBJ (Every value ek Object hai)
        - Har value ke saath Redis store karta hai:
            ┌──────────────────────────┐
            │  Type     → String?List? │  ← Kya hai?
            │  Encoding → Kaise store? │  ← Kaise rakha?
            │  Value    → Actual Data  │  ← Actual cheez
            └──────────────────────────┘
    3. SMART ENCODING (Redis Ka Smart Decision)
        - Redis automatically decide karta hai — "Is data ko kaise store karun ki memory bache!"
        - Example : 
            - SET age 25 
                → Redis stores it as INTEGER (not string "25")
                → Memory efficient! ✅
            - SET name "Rahul"
                → Redis stores as EMBSTR (small string)
                → Fast & compact! ✅
            - HSET user name "Rahul" age "25" city "Delhi"
                → Small hash → LISTPACK (compact)
            - HSET user [1000 Fields]
                → Big hash → HASHTABLE (fast access)

3. Example
-- Restaurant ka Order System = Redis Storage
-- ORDER REGISTER (Hash Table)
    "table:1" → "Butter Chicken"   ← Instant lookup
    "table:2" → "Paneer Tikka"     ← O(1) access
    "table:3" → "Dal Makhani"
-- EXPIRY REGISTER
    "offer:1" → expires in 1 hour  ← Auto delete!
    "otp:1"   → expires in 5 mins  ← Auto delete!
-- SMART STORAGE
    Chhota order (2-3 items) → Simple notepad
    Bada order (50+ items)   → Proper system

4. Important Interview Points
✅ Redis = Key-Value store in RAM
✅ Hash Table = O(1) access (super fast!)
✅ Har value ek RedisObject hai
✅ Redis automatically encoding choose karta hai
✅ Small data  → Compact encoding (memory save)
✅ Large data  → Fast encoding (speed priority)


## 9. What is a Redis Key ?
1. Simple Explanation
-- Socho tumhare ghar mein bahut saari almaariyaan hain:
    - Har almaari pe ek taala laga hai 
    - Har taale ki ek alag key hai
    - Sahi key dalo → turant khul jaati hai! 
            🔑 Key = "user:1"
            🗄️ Lock = Redis Storage
            📦 Value = "Rahul"
    - Sahi key dali -> Turant value mili!
    - Redis mein bhi aisa hi hai! Key = Address hai data ka! Jaise ghar ka address hota hai!

2. Technical Explanation
-- Redis Key = Unique Identifier for Every Value
    SET user:1 "Rahul"
    ↑
    KEY = "user:1"
    VALUE = "Rahul"
    GET user:1 → "Rahul" ⚡
-- Key Rules - Kya Hoan Chahiye :
    ✅ Key koi bhi string ho sakti hai
    ✅ Maximum size = 512 MB
    ✅ Binary safe (numbers, text, symbols sab)
    ✅ Case sensitive hai!
        "User:1" ≠ "user:1" ← Different keys!
-- Key Naming Convention - Best Practce
    - Format : object:id:field
    - Example : 
        user:1 -> User Id 1
        User:1:name -> User 1 Ka name
        User:1:email -> User 1 ka email
        order:101        → Order 101
        product:50:price → Product 50 ki price
        session:abc123   → Session data
    - Bad Key       Go0d Key
        "u1"        "user:1"
        "x"         "product:price:50"
        "data"      "order:101:status"
    - Colon ( : ) use karo separator ke liye! Redis mein ye standard practice hai!
-- TTL — Key Expire Bhi Ho Sakti Hai!
    - Example :
        SET otp:1234 "876"
        EXPIRE otp:1234 300    ← 300 seconds = 5 minutes
        Ab 5 minute baad → Key automatically DELETE ho jaayegi! ✅
    - More 
        OTP -> 5 minute Expiry
        Session -> 30 miute expiry
        Cache -> 1 hour expiry
        Auth Token -> 24 hour expiry...

## 10. What is the maximum size of a redis key/Value?
-> 512 MB

# Redis Data Structures (Very Important)
## 1. What data Structures Does Redis Support?
1. Techincal 
-- STRING - Sabse Simple
    - Kya hai?
        → Simple key-value
        → Text, Number, Boolean — sab!
    - Example
        SET name "Rahul"        → Text
        SET age 25              → Number
        SET is_active true      → Boolean
        SET score 100.5         → Decimal
    - GET name -> "Rahul"
    - Real Use : 
        → OTP store karna
        → Counter (likes, views)
        → Session token
        → Cache karna
-- LIST - Ordered Collection
    - Kya Hai ?
        → Ek ke baad ek items
        → Order maintain hota hai
        → Left se bhi add, Right se bhi add!
    - Example : 
        LPUSH orders "Burger"
        LPUSH orders "Pizza"
        LPUSH orders "Pasta"
    - orders = ["Pasta","Pizza","Burger"]
                    ↑ Latest pehle!
    - Real Use:
        → Recent activity feed
        → Message queue
        → Notification list
-- HASH — Object Storage 🗂️
    - Kya Hai?
        → Key ke andar aur Keys!
        → Ek object ki saari properties!
        → Bilkul JSON jaisa!
    - Example 
        HSET user:1 name "Rahul"
        HSET user:1 age  "25"
        HSET user:1 city "Delhi"
    - HGET user:1 name → "Rahul" ⚡
    - user : 1 = {
        name: "Rahul",
        age: "25",
        city: "Delhi"
    }
    - Real Use : 
        - User profile store karna
        - Product details
        - Shopping cart
-- SET — Unique Items Only 🎯
    - Kya Hai ?
        → Unique items ki collection
        → Duplicate allowed NAHI! ❌
        → Order matter nahi karta
    - Example :
        SADD tags "redis"
        SADD tags "database"
        SADD tags "redis"    ← Duplicate! Ignore! ❌
    - tags = {"redis" , "database"}
    - Real Use Case :
        → Unique visitors count
        → User ke interests/tags
        → "Who liked this post?"
-- SORTED SET (ZSet) — Ranked Collection 🏆
    - Kya Hai ?
        → Set jaisa BUT har item ka SCORE hota hai!
        → Score ke hisaab se automatically sort!
        → Leaderboard ke liye perfect!
    - Example : 
        ZADD leaderboard 950 "Rahul"
        ZADD leaderboard 870 "Priya"
        ZADD leaderboard 990 "Amit"
    - Automatically sorted
        → Amit  : 990 🥇
        → Rahul : 950 🥈
        → Priya : 870 🥉
    - Real Use : 
        -> Game leaderboard
        -> Top products ranking
        -> Trending Topics

3. Example
--  Restaurant mein 5 alag systems:
    1. STRING -> Simple sticky ote
      "Today's Special" -> "Butter Chicken"
    2. LIST -> Order queue
        [Table 3, Table 1 , Table 5] -> FIFO order
    3. HASH -> Customer card
        Customer:1 -> {name , phone, address}
    4. SET -> VIP Members List
        {Rahul , PRiya , Amit} -> No duplicates
    5. SORTED SET → Top customers
        Rahul : 5000rs , AMIT : 8000rs , Priya : 3000rs
        → Automatically ranked by spending! 🏆

4. Interview 
┌─────────────────┬──────────────┬───────────────────┐
│  Data Structure │   Unique?    │    Best Use       │
├─────────────────┼──────────────┼───────────────────┤
│ String          │ Simple value │ Cache, OTP, Count │
│ List            │ Ordered      │ Queue, Feed       │
│ Hash            │ Object       │ User Profile      │
│ Set             │ Unique items │ Tags, Likes       │
│ Sorted Set      │ Ranked items │ Leaderboard       │
└─────────────────┴──────────────┴───────────────────┘
-- Sabse Common : String
-- Sabse powerful : Sorted Set
-- Object store : Hash
-- Queue banana : List
-- Unique items = Set


## 2. What is a String Data type in Redis?
-> STRING - Sabse Simple
    - Kya hai?
        → Simple key-value
        → Text, Number, Boolean — sab!
    - Example
        SET name "Rahul"        → Text
        SET age 25              → Number
        SET is_active true      → Boolean
        SET score 100.5         → Decimal
    - GET name -> "Rahul"
    - Real Use : 
        → OTP store karna
        → Counter (likes, views)
        → Session token
        → Cache karna

## 3. What is a List in Redis?
LIST - Ordered Collection
    - Kya Hai ?
        → Ek ke baad ek items
        → Order maintain hota hai
        → Left se bhi add, Right se bhi add!
    - Example : 
        LPUSH orders "Burger"
        LPUSH orders "Pizza"
        LPUSH orders "Pasta"
        orders = ["Pasta","Pizza","Burger"]
                    ↑ Latest pehle!
        Real Use:
        → Recent activity feed
        → Message queue
        → Notification list

## 4. What is a Set in Redis ?
-- SET — Unique Items Only 🎯
    - Kya Hai ?
        → Unique items ki collection
        → Duplicate allowed NAHI! ❌
        → Order matter nahi karta
    - Example :
        SADD tags "redis"
        SADD tags "database"
        SADD tags "redis"    ← Duplicate! Ignore! ❌
    - tags = {"redis" , "database"}
    - Real Use Case :
        → Unique visitors count
        → User ke interests/tags
        → "Who liked this post?"

## 5. What is a Sorted Set (ZSET)?
-- SORTED SET (ZSet) — Ranked Collection 🏆
    - Kya Hai ?
        → Set jaisa BUT har item ka SCORE hota hai!
        → Score ke hisaab se automatically sort!
        → Leaderboard ke liye perfect!
    - Example : 
        ZADD leaderboard 950 "Rahul"
        ZADD leaderboard 870 "Priya"
        ZADD leaderboard 990 "Amit"
    - Automatically sorted
        → Amit  : 990 🥇
        → Rahul : 950 🥈
        → Priya : 870 🥉
    - Real Use : 
        -> Game leaderboard
        -> Top products ranking
        -> Trending Topics

## 6. What is a Hash in Redis?
-- HASH — Object Storage 🗂️
    - Kya Hai?
        → Key ke andar aur Keys!
        → Ek object ki saari properties!
        → Bilkul JSON jaisa!
    - Example 
        HSET user:1 name "Rahul"
        HSET user:1 age  "25"
        HSET user:1 city "Delhi"
    - HGET user:1 name → "Rahul" ⚡
    - user : 1 = {
        name: "Rahul",
        age: "25",
        city: "Delhi"
    }
    - Real Use : 
        - User profile store karna
        - Product details
        - Shopping cart

## 7. What is a Bitmap?
1. Simple Explanation
-- Socho tumhari attendance register hai school mein:
-- Attendance Register :
    - Student: Rahul
        Day 1  → ✅ (1) Aaya
        Day 2  → ✅ (1) Aaya
        Day 3  → ❌ (0) Nahi aaya
        Day 4  → ✅ (1) Aaya
        Day 5  → ❌ (0) Nahi aaya
    - = 1 1 0 1 0
    - Bas 0 aur 1 - aaya ya nahi aaya! yahi Bitmap hai! Bahut kam jagah mein bahut saari information.

2. Technical Explanation
-- Bitmap Kya Hai ?
    - Bitmap = String hi hai — BUT bit level pe kaam karta hai!
    - Eample :  
        - Normal String: "Hello"    -> Bytes Store karta hai.
        - Bitmap : 10110100         -> Bits store karta hai.
    - Har Bit ka ek positon hota hai 
        - Position : 0 1 2 3 4 5 6
        - Bit :      1 0 1 1 0 1 0
-- Basis Commands 
    - Example :
        SETBIT user:login 0 1   → Day 0 pe aaya ✅
        SETBIT user:login 1 1   → Day 1 pe aaya ✅
        SETBIT user:login 2 0   → Day 2 pe nahi aaya ❌
        SETBIT user:login 3 1   → Day 3 pe aaya ✅
    - Bit check karo :
        GETBIT user:login 1 -> 1 (aaya tha!)
        GETBIT user:login 2 -> 0 (nahi aaya!)
    - Count karo kitne 1 hain:
        BITCOUNT user:login -> 3
        (3 din aaya total!)
-- Memory Magic - Kyun Use Karte Hain?
    - Problem : 10 Million users ka daily login track karo
    - Normal Way (String.Set)
        → Har user ka naam store karo
        → 10M × 20 bytes = 200 MB! 😱
    - Bitmap Way : 
        → Sirf 0 ya 1 store karo
        → 10M bits = sirf 1.2 MB! 😎
    - Memory Saving : 99%

3. Importnat For Interview
-- Bitmap = String at bit level (0 or 1 only)
-- Bahut kam memory use karta hai
-- Perfect for YES/NO type data
-- 10 Million users = sirf 1.2 MB!
-- Real World Use Case :
    → User daily login tracking
    → Feature flag (on/off)
    → Attendance system
    → "Has user seen this notification?"
-- Key Commands : 
    SETBIT  → Bit set karo
    GETBIT  → Bit check karo
    BITCOUNT→ Kitne 1 hain count karo

## 8. What is a HyperLogLog?
1. Simple Explanation
-- Socho tumhare school mein Mela lag raha hai!
-- Principal na poocha :
    "Aaj Kitne bacche mele mein aaye"
-- Normal Way
    - Har bacche ka naam likho:Rahul, Priya, Amit, Sara...
    - Problem : 
        → Bahut time lagta hai!
        → Bahut jagah chahiye!
        → 10,000 bacche = 10,000 names! 😱
-- Smart Way (HyperLogLog) : 
    - Gate pe ek MAGIC COUNTER hai:
        → Har nayi face dekhi → Counter +1
        → Same face dobara aayi → Counter same!
        → Bas count batata hai — naam nahi yaad rakhta!   
    - "Aaj 9,850 unique bacche aaye!" 
        → Exact nahi — but ALMOST sahi! 🎯
        → Bahut kam memory mein! ⚡
-- HyperLogLog = Unique cheezein COUNT karta hai Exact nahi — but 99% accurate! Aur memory? Sirf 12 KB! 😎

2. Technical Explanation
-- HyperLogLog Kya Hai?
    - HyperLogLog = Probabilistic Data Structure
    - Matlab :
        → Unique items COUNT karta hai
        → 100% exact nahi — 99.81% accurate
        → Memory = Always sirf 12 KB!
        → Chahe 1 item ho ya 1 Billion!
-- Basic Commands : 
    - Add Karo : 
        PFADD visitors "Rahul"
        PFADD visitors "Priya"
        PFADD visitors "Amit"
        PFADD visitors "Rahul"  ← Duplicate! Ignore! ❌
    - Count Karo :
        PFCOUNT visitors -> 3 ((Sirf 3 unique visitors!) ✅)
    - Merge Karo
        PFADD page1 "Rahul" "Priya"
        PFADD page2 "Amit"  "Rahul"
        PFMERGE total page1 page2
        PFCOUNT total → 3
        (Rahul duplicate tha — sirf 3 unique!) ✅
-- Memory Comparison
    - Problem : 1 Billion unique Users Track Karo!
    - Normal Set : 
        → Har user store karo
        → 1B × 20 bytes = 20 GB RAM! 😱
    - HyperLogLog:
        → Sirf count rakho
        → Always = 12 KB!
    - Memory Saving = Almost 100%
-- TradeOff - Kya Miss Hota Hai?
    - HyperLogLog gives APPROXIMATE count:
    - Actual Users: 1,000,000
    - HLL Result:     998,000  ← ~0.81% error
    - Acceptable? ✅
        → "Roughly 1 Million users aaye"
        → Exact count nahi chahiye hota!
        → Analytics ke liye perfect!
    - ❌ Exact count chahiye?
        → HyperLogLog mat use karo!
        → Set use karo!

3. Important Interview
✅ HyperLogLog = Unique items COUNT karna
✅ Memory = Always sirf 12 KB
✅ Accuracy = 99.81% (0.81% error)
✅ Actual data store NAHI karta — sirf count!
✅ PFADD, PFCOUNT, PFMERGE — 3 commands!
-- Real World Use Cases
    → Unique website visitors count
    → Unique search terms track karna
    → Unique active users per day
    → Analytics dashboards

## 9. What is a Stream in Redis?
1. Defination
-- Socho tumhari school diary hai:
-- Diary mein har roz likhte ho:
    Jan 1  → "Aaj school gaya"
    Jan 2  → "Aaj cricket khela"
    Jan 3  → "Aaj test tha"
    Jan 4  → "Aaj picnic thi"
-- Purani entries delete nahi hoti! ✅
-- Nai entry hamesha end mein jaati hai! ✅
-- Koi bhi entry baad mein padh sakta hai! ✅
-- Multiple log ek saath padh sakte hain! ✅
-- Redis Stream = Aisi hi diary hai! Events ek ke baad ek record hote rehte hain! Koi bhi event miss nahi hota! 🎯

2. Technical Explanation
-- Stream Kya Hai ?
    - Redis Stream = Append-Only Log of Events
    - Matlab:
        → Events/Messages ek ke baad ek store hote hain
        → Purana data delete nahi hota
        → Har entry ka unique ID hota hai
        → Multiple consumers padh sakte hain

## 10. When Should you use each Redis Data Structure ?
1. String 
-- Real Use : 
        → OTP store karna
        → Counter (likes, views)
        → Session token
        → Cache karna

2. List 
-- Real Use:
        → Recent activity feed
        → Message queue
        → Notification list

3. Hash
-- Real Use : 
        - User profile store karna
        - Product details
        - Shopping cart

4. Set 
-- Real Use Case :
        → Unique visitors count
        → User ke interests/tags
        → "Who liked this post?"

5. Sorted Set :
-- Real Use : 
        -> Game leaderboard
        -> Top products ranking
        -> Trending Topics

# Caching Concepts
## 1. What is caching ?
1. Simple Explanation
-- Socho tumhara favourite question hai maths mein: "2 × 8 = ?"
❌ Bina Caching ke:
    - Har baar calculate karo:
    - 2 × 8 = ?
    - 2+2+2+2+2+2+2+2 = 16
    - Har baar time lagta hai! 😓
✅ Caching ke saath:
    - Ek baar calculate kiya → Yaad kar liya!
    - Ab koi bhi poocha "2 × 8?"
    - "16!" — Turant! ⚡
    - Dobara calculate nahi kiya!
-- Caching = Ek baar kaam karo Baar baar result yaad rakho!

2. Technical Explanation
-- Caching Kya Hai?
    - Cache = Temporary Fast Storage
    - Normal Flow (Without Cache):
        User Request
            ↓
        Application
            ↓
        💾 Database (Slow!) → 100ms
            ↓
        Response
    - Cached Flow (With Cache):
        User Request
            ↓
        Application
            ↓
        🧠 Redis Cache (Fast!) → 1ms
            ↓
        Response
    - Result = 100x Faster! ⚡
-- How Caching Works 
    - Step 1: User ne request kiya
        "Rahul ki profile dikhao"
    - Step 2: Cache check karo (Cache Hit/Miss)
        - Cache main hai? -> Cache Hit -> Turant Do
        - Cache main nai? -> Cache Miss -> Database se lao.
    - Step 3: Cache Miss hone pe 
        Database se data laya
            ↓
        Redis mein save kiya (Cache Store)
            ↓
        User ko diya
    - Step 4: Next time same request
        - Redis mein hai! -> Cache HIT
        -> Database touch nahi kiya!
-- Cache Hit vs Cache Miss
    - Cache HIT : 
        Request → Redis → Data mila! ✅
        Fast, No DB call, Happy! 😎
    - Cache MISS : 
        Request → Redis → Nahi mila!
        → Database → Data laya
        → Redis mein save kiya
        → Response diya
        Slow, DB call hua, but next time fast! ✅

3. Important Interview Points
✅ Cache = Fast temporary storage
✅ Cache HIT = Data mila Redis mein ✅
✅ Cache MISS = Data nahi mila, DB se laya ❌
✅ Cache reduces DB load by ~90%!
✅ Cache reduces response time 100x!
-- What is Cache 
    ✅ Frequently accessed data
    ✅ Data jo rarely change hota hai
    ✅ Expensive DB queries ka result
    ✅ User sessions
    ✅ API responses
-- What NOT to Cache?
    ❌ Highly sensitive data (passwords)
    ❌ Data jo har second change hota hai
    ❌ User specific real-time data
-- Cache TTL (Expiry):
    Hamesha TTL set karo!
    → Stale data problem avoid hoti hai
    → Memory free rehti hai
    SET menu "Butter Chicken" EX 3600
    → 1 hour baad automatically delete! ✅

## 2. Why is Redis Commonly used as a Cache?
✅ Cache = Fast temporary storage
✅ Cache reduces DB load by ~90%!
✅ Cache reduces response time 100x!

## 3. What is Cache eviction ?
1. Simple Explanation 
-- Socho tumhare paas ek small pencil box hai! ✏️
Pencil box mein sirf 5 cheezein aa sakti hain:
┌─────────────────────────────┐
│ Pencil │ Pen │ Eraser │ Scale│ Sharpner│
└─────────────────────────────┘
        → BOX FULL! 😱
-- Ab tumhe Crayon rakhna hai — lekin box full hai!
-- Kya karoge? 🤔
    → Koi ek cheez NIKALNI padegi!
    → Tab nai cheez andar aayegi!
-- Yahi Cache Eviction hai! Redis ka memory full ho gayi → Purani cheez hataao → Nai cheez daalo! 🎯

2. Technical Explanation
-- Redis ki memory LIMITED hai! (Jitni RAM — utni hi memory)
-- Jab memory full ho jaaye:
    Naya data aaya → Kahan rakhen? 😱
    ↓
    Purana data EVICT karo (hatao)
    ↓
    Naya data rakho! ✅
-- Ye process = Cache Eviction!

## 4. What are Redis eviction Policies?
-- Total 6 Policies
1. NOEVICTION(Default)
-- Policy: Kuch mat hatao!
-- Memory full + Naya data aaya
-- ❌ ERROR de do! "OOM command not allowed"
-- Use : Jab data loss bilkul nahi chahiye
⚠️ Warning: Application crash ho sakti hai!

2. ALLKEYS-LRU ⭐ Most Popular!
-- Policy: Sabse pehle PURANA hatao!
-- LRU = Least Recently Used
-- Jo key sabse pehle use hui thi
    → Wo pehle hataao!
-- Example : 
    Key A → Last used: 1 hour ago   ← EVICT! 🗑️
    Key B → Last used: 5 mins ago
    Key C → Last used: 1 min ago
-- Sabse purani = Key A -> Bye Bye
-- Use : General caching ke liye best! ✅

3. ALLKEYS-LFU
-- Policy: Sabse KAM use hone wala hatao!
-- LFU = Least Frequently Used
-- Jo key sabse kam use hui 
    -> Wo pehle hataao!
-- Example 
    Key A → Used: 2 times    ← EVICT! 🗑️
    Key B → Used: 50 times
    Key C → Used: 30 times
-- Sabse kam use = Key A → Bye bye! 👋
-- Use: Popular data retain karna ho!

4. ALLKKEYS-RANDOM
-- Policy: Random koi bhi hatao!
-- Memory full → Koi bhi random key delete karo!
-- Use: Jab koi pattern matter na kare
⚠️ Warning: Important data bhi ja sakta hai!

5. VOLATILE-LRU
-- Policy: Sirf EXPIRY wali keys mein se purani hatao!
-- TTL wali keys → LRU se hatao
-- No TTL wali keys → Safe! ✅
-- Example : 
    Key A (TTL: yes) → Last used: 1hr ← EVICT! 🗑️
    Key B (TTL: yes) → Last used: 1min
    Key C (TTL: no)  → SAFE! ✅
-- Use : Permanent data bachana ho! ✅

6. VOLATILE-TTL
-- Policy : Sabse jaldi expire hone wali
        key pehle hatao!
-- Jo key sabse jaldi expire hogi
    → Use pehle hataao!
-- Example : 
    Key A → TTL: 10 seconds  ← EVICT! 🗑️
    Key B → TTL: 1 hour
    Key C → TTL: 1 day
-- Sabse jaldi expire = Key A → Bye bye! 👋

## 5. What is cache invalidation?
1. Simple Explanation
-- Socho tumhari mummy ne subah tiffin pack kiya:
    Subah 8 AM:
    Tiffin mein → "Aloo Paratha" ✅
    Tumhe yaad hai → "Aaj Aloo Paratha hai!" 😋
-- Lekin tumhari mummy ne baad mein change kar diya:
    Subah 9 AM:
    Mummy ne tiffin badal diya → "Paneer Sandwich" 🥪
    Lekin tumhe abhi bhi lagta hai → "Aloo Paratha hai!" 😐
-- Problem : Tumhari purani yaad (cache) GALAT hai! Naya tiffin alag hai — purani info outdated!
-- Cache Invalidation = Purani galat yaad hatao Nai sahi info rakho! 🎯

2. Techincal Explnantion
-- Cache Invalidation Kya Hai?
    Jab Database mein data change ho —
    Cache mein purana (stale) data hota hai!

    Problem:
    ─────────────────────────────
    Database → Rahul ki salary = 50,000 ✅ (Updated)
    Cache    → Rahul ki salary = 40,000 ❌ (Old!)

    User cache se padh raha hai → GALAT DATA! 😱

    Solution = Cache Invalidation!
    → Purana cache hatao ya update karo! ✅

## 6. What is Cache aside pattern?
-- CACHE ASIDE (Most Popular!)
Flow:
─────────────────────────────
READ:
User → Cache check karo
         ↓
    Cache HIT? → Data do ✅
         ↓
    Cache MISS? → DB se lao
               → Cache mein save karo
               → Data do ✅

WRITE/UPDATE:
Data change hua DB mein
    ↓
Cache DELETE karo! 🗑️
    ↓
Next request → Cache MISS
            → DB se fresh data lega
            → Cache update ho jayega ✅

Simple Rule:
"Data change hua = Cache delete karo!"

## 7. What is Write-through caching?
Flow:
─────────────────────────────
Data update hua?
    ↓
PEHLE Cache update karo ✅
    ↓
PHIR Database update karo ✅

Dono hamesha sync mein! 🔄

Advantage:
→ Cache hamesha fresh! ✅
→ Stale data kabhi nahi! ✅

Disadvantage:
→ Har write pe double kaam 😓
→ Thoda slow writes

## 8. What is TTL BASED INVALIDATION?
Flow:
─────────────────────────────
Cache mein data rakho + Expiry lagao!

SET user:1 "Rahul" EX 3600
              ↑
         1 hour baad auto delete!

1 hour baad:
→ Cache automatically delete! 🗑️
→ Next request → Fresh DB se lega ✅

Simple Rule:
"Cache apne aap expire ho jaayega!"

Advantage:
→ Bahut simple! ✅
→ Koi extra code nahi!

Disadvantage:
→ 1 ghante tak purana data aa sakta hai! ⚠️

## 9. What is Cache stampede?
1. Simple Explanation
-- Socho ek popular ice cream shop hai! 🍦
    Subah 10 AM:
    Shop khuli → Bahut saare bacche line mein! 😄
    "Chocolate ice cream do!"
    "Chocolate ice cream do!"
    "Chocolate ice cream do!"
-- Lekin chocolate ice cream khatam ho gayi! 
        Ab kya hua?
    ──────────────────────────────
    1000 bacche ek saath chef ke paas gaye!
    "Chocolate banao! Chocolate banao!"

    Chef akela hai! 😵
    1000 bacche ek saath chilla rahe hain!
    Chef overwhelmed → Shop band ho gayi! 💥
-- Yahi Cache Stampede hai! Cache expire hua → Sab ek saath DB pe gaye → DB crash!

2. Technical Explanation
-- Cache Stampede Kya Hai?
-- Normal Flow:
    ─────────────────────────────
    1000 users → Redis Cache → Instant! ⚡
                (Cache HIT)

    Stampede Flow:
    ─────────────────────────────
    Cache EXPIRE ho gayi! ⏰
        ↓
    1000 users ek saath aaye
        ↓
    1000 Cache MISS! ❌
        ↓
    1000 DB queries ek saath! 😱
        ↓
    💥 DATABASE CRASH!
-- TimeLine : 
    ─────────────────────────────
    9:00 AM → Cache set hua ✅
    9:01 AM → 1000 users → Cache HIT ⚡
    9:02 AM → Cache EXPIRE! ⏰
    9:02 AM → 1000 users → Cache MISS ❌
    9:02 AM → 1000 DB hits → 💥 CRASH!

## 10. How Do you prevent cache stampede?
-- 3 Solutions:
1. MUTEX LOCK(Locking Soluction)
    Idea:
    ─────────────────────────────
    Sirf EK request DB se data laye!
    Baaki sab WAIT karen!

    Flow:
    ─────────────────────────────
    Cache Miss hua
        ↓
    Pehli request → Lock lelo! 🔒
                → DB se data lao
                → Cache update karo
                → Lock chodo! 🔓

    Baaki 999 requests → Lock dekha
                    → Wait karo ⏳
                    → Cache update hone do
                    → Cache se lelo! ✅

    Result:
    → Sirf 1 DB query! ✅
    → 999 requests cache se! ✅
    → No crash! 😎

2. EARLY EXPIRATION (Smart Expiry)
    Idea:
    ─────────────────────────────
    Expiry se PEHLE hi cache refresh karo!
    Expire hone ka wait mat karo!

    Flow:
    ─────────────────────────────
    Cache TTL = 60 minutes set kiya

    55 minutes pe:
    → "Expiry aane wali hai!"
    → Background mein cache refresh karo ✅
    → Users ko pata bhi nahi chala! 😎

    60 minutes pe:
    → Cache already fresh hai! ✅
    → Koi stampede nahi! ✅

    Jaise:
    ─────────────────────────────
    Ghar mein gas khatam hone se
    PEHLE hi cylinder mangwa lo!
    Khatam hone ka wait mat karo! 🎯

3. PROBABILISTIC EARLY EXPIRATION
    Idea:
    ─────────────────────────────
    Randomly kuch requests pehle
    hi cache refresh kar deti hain!

    Flow:
    ─────────────────────────────
    TTL check karo
        ↓
    "Kya mujhe abhi refresh karna chahiye?"
        ↓
    Random chance → Haan! → Refresh karo ✅
    Random chance → Nahi! → Cache use karo ✅

    Result:
    → Gradually refresh hota hai
    → Ek saath sab nahi jaate DB pe! ✅



# Persistence (Very Important)
Does Redis persist data?
What is RDB persistence?
What is AOF (Append Only File)?
What is the difference between RDB vs AOF?
What is snapshotting in Redis?
What is fsync policy in Redis?
When would you use RDB vs AOF?

#


🔄 5. Replication & High Availability
What is Redis replication?
What is master-slave replication?
What happens if the master fails?
What is Redis Sentinel?
What problem does Sentinel solve?
How does Sentinel detect failures?
What is automatic failover in Redis?
🌐 6. Redis Clustering & Scalability
What is Redis Cluster?
How does Redis distribute data across nodes?
What are hash slots in Redis?
How many hash slots exist in Redis cluster?
What is sharding?
Difference between Redis Cluster vs Redis Sentinel?
🔒 7. Transactions & Atomic Operations
Does Redis support transactions?
What are Redis transactions?
What are MULTI, EXEC, WATCH commands?
Are Redis transactions ACID compliant?
How does Redis ensure atomic operations?
📊 8. Pub/Sub & Streaming
What is Pub/Sub in Redis?
How does Redis Pub/Sub work?
What are Redis Streams?
When should you use Redis Streams instead of Kafka?
⚙️ 9. Performance & Optimization
How does Redis achieve high performance?
What is Redis single-threaded architecture?
Does Redis support multi-threading?
What are Redis pipelines?
What is Redis latency?
How do you optimize Redis performance?
🧩 10. Memory Management
How does Redis manage memory?
What are Redis memory eviction policies?
What is LRU eviction?
What is LFU eviction?
What is volatile vs allkeys eviction policy?
🔍 11. Debugging & Monitoring
How do you monitor Redis performance?
What is the INFO command?
What is Redis slow log?
How do you detect memory leaks in Redis?
🏭 12. Real Production Questions (Very Common)
When should you use Redis instead of a database?
What problems occur when Redis memory is full?
How do you scale Redis for millions of users?
How do you handle Redis node failure?
How do companies use Redis for session storage?
How do you design a rate limiter using Redis?
🎯 10 Redis Concepts Every Engineer Must Know

If you deeply understand these 10, most Redis interviews clear ho jaate hain:

Redis architecture
Redis data structures
Caching strategies
Persistence (RDB vs AOF)
Replication
Redis Sentinel
Redis Cluster
Memory eviction policies
Pub/Sub
Redis performance tuning
🚀 Redis System Design Questions (Senior Interviews)

These appear in backend/system design rounds:

Design a distributed cache using Redis
Design a rate limiter using Redis
Design session storage using Redis
Design real-time leaderboard using Redis sorted sets
Design chat system using Redis Pub/Sub
Design distributed locking using Redis