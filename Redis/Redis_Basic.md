# Redis Fundamentals

## 1. What Is Redis?

### 1.1 Simple Meaning

Redis ek **in-memory data store** hai jo data ko primarily RAM (Random Access Memory) mein store karta hai. RAM se data access karna disk ke comparison mein bahut fast hota hai, isliye Redis low-latency responses provide kar sakta hai.

Redis ko commonly caching ke liye use kiya jata hai, lekin ye sirf cache nahi hai. Iska use session management, real-time data handling, counters, messaging aur other use cases mein bhi hota hai.

### 1.2 Real-Life Example – Trading Application

Suppose hamari Trading Application mein 1,000 users simultaneously NIFTY ka live price check kar rahe hain.

Agar har user ki request par Application Server directly Database ko hit karega, toh same data ke liye Database par baar-baar requests jayengi. Isse Database ka load increase ho sakta hai aur response time bhi slow ho sakta hai.

Is problem ko handle karne ke liye hum Redis use kar sakte hain:

1. Application Server NIFTY ka latest price Redis mein store karega.
2. Jab user NIFTY ka price request karega, Application Server pehle Redis check karega.
3. Agar price Redis mein available hai, toh Redis se directly data return ho jayega.
4. Agar data available nahi hai, toh Application Server Database ya original data source se fetch karega aur zarurat ke according Redis mein store karega.

Is approach se repeated Database calls reduce hoti hain.

### 1.3 Architecture Diagram

```text
          Client Application
                  |
                  v
          Application Server
                  |
                  v
             Redis Cache
                  |
            +-----+-----+
            |           |
            v           v
         Cache Hit   Cache Miss
            |           |
            v           v
       Return Data   Database
                         |
                         v
                   Store in Redis
                         |
                         v
                    Return Data
```

### 1.4 Important Terms

- **Cache Hit:** Jab requested data Redis mein already available hota hai.
- **Cache Miss:** Jab requested data Redis mein available nahi hota.
- **Cache:** Frequently accessed data ki temporary ya reusable copy, jisse application faster response de sake.

### 1.5 Interview Mein Kaise Explain Karein?

Redis ek in-memory data store hai jo data ko primarily RAM mein store karta hai. Iska use frequently accessed data ko fast retrieve karne ke liye hota hai.

For example, hamari Trading Application mein agar thousands of users NIFTY ka live price request kar rahe hain, toh hum us price ko Redis mein cache kar sakte hain.

Jab bhi request aati hai, Application Server pehle Redis check karta hai. Agar data available hai, toh Redis se directly return kar deta hai. Agar data available nahi hai, toh Database ya original data source se fetch karke Redis mein store kar sakte hain.

Isse repeated Database calls reduce hoti hain, response time improve hota hai aur application better performance handle kar pati hai.

---

## 2. Why Is Redis Called an In-Memory Database?

Redis ko In-Memory Data Store ya commonly In-Memory Database kaha jata hai because it stores and serves data primarily from RAM (Random Access Memory).

RAM ka access time traditional disk storage ke comparison mein bahut kam hota hai. Isi wajah se Redis data ko very quickly read aur update kar sakta hai.

### Real-Life Example – Trading Application

Suppose hamari Trading Application mein multiple users NIFTY ka live price baar-baar request kar rahe hain.

Agar hum har request par Database se price fetch karenge, toh same data ke liye repeated Database calls hongi.

Instead, hum latest NIFTY price Redis mein store kar sakte hain. Application Server Redis se price read karega aur users ko quickly response dega.

**Important:** Redis primarily RAM use karta hai, lekin iska matlab ye nahi hai ki Redis data ko disk par save hi nahi kar sakta. Redis persistence options bhi provide karta hai, jinke through data ko disk par save kiya ja sakta hai.

### Interview Mein Kaise Explain Karein?

Redis ko In-Memory Database kaha jata hai because it stores and accesses data primarily from RAM.

RAM se data access karna disk-based storage ke comparison mein much faster hota hai. For example, hamari Trading Application mein hum frequently accessed NIFTY price Redis mein store kar sakte hain.

Isse Application Server ko baar-baar Database hit nahi karna padta aur users ko faster response milta hai.

---

## 3. What Problem Does Redis Solve?

### 3.1 Simple Meaning

Redis mainly un situations mein help karta hai jahan application ko frequently accessed data fast retrieve karna hota hai aur Database par repeated requests ka load reduce karna hota hai.

Jab multiple users same data baar-baar request karte hain, toh har request ke liye Database query execute karna unnecessary overhead create kar sakta hai.

Redis frequently accessed data ko RAM mein maintain karke application ko fast response dene mein help karta hai.

### 3.2 Real-Life Example – Trading Application

Suppose hamari Trading Application mein 10,000 users simultaneously NIFTY ka live price check kar rahe hain.

**Without Redis:**

- Har user ki request Database ya original data source tak ja sakti hai.
- Same data ke liye repeated queries execute hongi.
- Database par load increase ho sakta hai.
- High traffic ke time response time slow ho sakta hai.

**With Redis:**

- Frequently accessed NIFTY price Redis mein available rahega.
- Application Server price Redis se quickly fetch kar sakta hai.
- Same data ke liye repeated Database calls reduce hongi.
- Database ko other important operations handle karne ke liye more capacity mil sakti hai.

### 3.3 Redis Se Kya Benefits Milte Hain?

1. **Faster Response Time:** Data RAM se quickly retrieve hota hai.
2. **Reduced Database Load:** Frequently accessed data ke liye repeated Database calls kam hoti hain.
3. **Better Scalability:** Application high-volume read requests ko better handle kar sakti hai.
4. **Improved User Experience:** Users ko data faster milta hai.

### 3.4 Interview Mein Kaise Explain Karein?

Redis mainly application ki performance improve karne aur Database par unnecessary load reduce karne ke liye use hota hai.

For example, hamari Trading Application mein thousands of users simultaneously NIFTY ka live price request kar rahe hain.

Agar har request Database par jayegi, toh same data ke liye repeated queries execute hongi. Isse Database load increase ho sakta hai aur response time slow ho sakta hai.

Is problem ko solve karne ke liye hum Redis use karte hain. Frequently accessed data Redis ki memory mein available rehta hai, jahan se Application Server usse quickly fetch kar sakta hai.

Isse response time improve hota hai aur Database par repeated requests ka load reduce hota hai.

**In Short:** Redis helps reduce repeated Database calls, improve response time and handle frequently accessed data efficiently.

---

## 4. What Is the Difference Between Redis and Traditional Databases?

Redis aur traditional databases jaise MySQL aur PostgreSQL ka purpose aur storage approach different ho sakta hai.

Redis primarily RAM se data serve karta hai, isliye ye high-speed data access ke liye useful hai. Traditional relational databases generally persistent data management, structured records, relationships aur complex queries ke liye use hote hain.

### 4.1 Difference

| Basis | Redis | Traditional Database (MySQL/PostgreSQL) |
|---|---|---|
| Primary Storage/Access | Primarily RAM | Generally disk-based persistent storage |
| Main Purpose | Fast data access, caching and real-time use cases | Persistent and structured data management |
| Data Model | Key-Value based with multiple data structures | Tables, rows and columns (relational databases) |
| Query Pattern | Key-based operations and data-structure commands | SQL queries |
| Common Use Cases | Cache, sessions, counters, real-time data | User records, orders, transactions and reports |
| Persistence | Optional persistence mechanisms available | Persistent storage is a core feature |

### 4.2 Real-Life Example – Trading Application

Hamari Trading Application mein hum dono technologies ko saath mein use kar sakte hain:

- **Redis:** Frequently accessed live market data, temporary data, counters ya user sessions ke liye.
- **MySQL/PostgreSQL:** User details, order history, transaction records aur other important persistent records ke liye.

For example, NIFTY ka frequently requested live price Redis se serve ho sakta hai, jabki user's order history relational Database mein maintain ki ja sakti hai.

### Interview Mein Kaise Explain Karein?

Redis and traditional databases differ mainly in their storage approach and use cases.

Redis primarily RAM se data serve karta hai, jiski wajah se data access bahut fast hota hai. On the other hand, MySQL and PostgreSQL jaise traditional relational databases persistent and structured data management ke liye commonly use hote hain.

For example, hamari Trading Application mein hum Redis ko frequently accessed live market data ke liye use kar sakte hain, while MySQL user details, order history aur transaction records maintain kar sakta hai.

So, Redis is useful for high-speed data access, whereas traditional relational databases are commonly used for reliable and persistent data management.

**In Short:**
- **Redis:** Fast Data Access, Caching and Real-Time Use Cases
- **Traditional Database:** Persistent and Structured Data Management

---

## 5. Why Is Redis So Fast?

Redis fast hone ke kuch important reasons hain:

1. **RAM-Based Data Access:** Redis primarily RAM se data read aur write karta hai. RAM access disk access ke comparison mein much faster hota hai.
2. **Optimized Data Structures:** Redis Strings, Lists, Sets, Hashes aur Sorted Sets jaise data structures provide karta hai. Inke operations specific use cases ke liye optimized hote hain.
3. **Efficient Operations:** Redis common operations ko efficiently execute karta hai.
4. **Reduced Database Calls:** Frequently accessed data Redis se serve hone ki wajah se application ko baar-baar main Database hit nahi karna padta.

### Real-Life Example – Trading Application

Suppose hamari Trading Application mein thousands of users NIFTY ka live price request kar rahe hain.

Agar har request par Application Server Database ko hit karega, toh repeated queries execute hongi.

Lekin agar latest NIFTY price Redis mein stored hai, toh Application Server directly Redis se price fetch kar sakta hai.

Isse data retrieval fast hota hai, latency reduce hoti hai aur overall application performance improve hoti hai.

### Interview Mein Kaise Explain Karein?

Redis is very fast mainly because it stores and accesses data primarily from RAM instead of relying on disk for normal data operations.

RAM access is much faster than disk access. Apart from that, Redis uses optimized data structures and efficient operations to process requests quickly.

For example, in our Trading Application, if multiple users are requesting NIFTY live prices, Redis can provide the cached data directly from memory instead of hitting the Database repeatedly.

This reduces latency and improves application performance.

**In Short:** Redis fast hai because of RAM-based data access, optimized data structures, efficient operations and reduced repeated Database calls.

---

## 6. What Are the Main Use Cases of Redis?

### 6.1 Simple Meaning

Redis ka use mainly application ki performance improve karne, frequently accessed data ko fast access karne aur real-time operations handle karne ke liye hota hai.

Redis ke common use cases hain:

1. **Caching:** Frequently accessed data ko temporarily store karna, taaki next request par data quickly mil sake.
2. **Session Management:** User ke login session aur session-related information maintain karna.
3. **Real-Time Data:** Live stock prices, counters aur frequently changing data ko fast access ke liye store karna.
4. **Rate Limiting:** Control karna ki ek user ya client particular time period mein kitni API requests bhej sakta hai.
5. **Messaging:** Redis Pub/Sub ya Redis Streams ke through different application components ke beech messages ya events exchange karna.

### 6.2 Real-Life Example – Trading Application

Suppose hamari ek Trading Application hai. Hum Redis ko multiple purposes ke liye use kar sakte hain:

| Use Case | Trading Application Example |
|---|---|
| Caching | NIFTY ka frequently accessed price |
| Session Management | User Login Session |
| Real-Time Data | Live Market Data |
| Rate Limiting | Ek user kitni API requests bhej sakta hai |
| Messaging | Order processing events ko different services tak pahunchana |

### 6.3 Architecture Diagram

```text
               Trading Application
                        |
                        v
                 Application Server
                        |
                        v
                      Redis
                        |
          +-------------+-------------+
          |             |             |
          v             v             v
        Cache         Session       Rate
       Storage       Management    Limiting
          |
          v
    Live Market Data


          Redis Pub/Sub or Streams
                        |
                        v
                 Other Services
```

### 6.4 Interview Mein Kaise Explain Karein?

Redis is commonly used for caching, session management, real-time data storage, rate limiting and messaging.

For example, in our Trading Application, we can use Redis to cache frequently accessed stock prices, maintain user login sessions and control API request limits.

We can also use Redis Pub/Sub or Redis Streams to exchange messages or events between different application components.

So, Redis helps improve application performance and supports fast data access and real-time processing.

**In Short:** Redis is commonly used for Caching, Session Management, Real-Time Data, Rate Limiting and Messaging.

---

## 7. What Is the Difference Between Redis and Memcached?

Redis and Memcached dono in-memory data stores hain jo commonly caching ke liye use hote hain. Dono ka main purpose frequently accessed data ko fast serve karna hai.

Lekin Redis additional data structures aur features provide karta hai, jabki Memcached mainly simple Key-Value caching par focused hai.

### 7.1 Difference

| Basis | Redis | Memcached |
|---|---|---|
| Data Structure | Strings, Lists, Sets, Hashes, Sorted Sets and more | Primarily simple Key-Value data |
| Main Use | Caching plus multiple additional use cases | Simple caching |
| Persistence | Persistence options available | Generally cache data ko persistent storage ke roop mein maintain nahi karta |
| Advanced Features | Pub/Sub, Streams, counters, expiry and other features | Comparatively focused on basic caching |
| Data Operations | Multiple data-structure-specific operations | Basic operations on cached values |

### 7.2 Real-Life Example – Trading Application

Suppose hamari Trading Application mein humein NIFTY ka live price frequently access karna hai.

- **Memcached:** Simple Key-Value format mein NIFTY ka price cache karne ke liye use kar sakte hain.
- **Redis:** NIFTY price cache karne ke saath user sessions, counters, Sorted Sets aur messaging-related use cases bhi handle kar sakte hain.

### 7.3 Interview Mein Kaise Explain Karein?

Redis and Memcached are both in-memory caching systems used to improve application performance.

The main difference is that Memcached is primarily designed for simple Key-Value caching, whereas Redis supports multiple data structures like Strings, Lists, Sets, Hashes and Sorted Sets.

For example, in our Trading Application, we can use Memcached for simple frequently accessed data like stock prices. Redis provides additional capabilities that can be useful for session management, counters, real-time data handling and messaging.

So, Memcached is mainly focused on simple caching, while Redis offers caching along with multiple data structures and additional features.

**In Short:**
- **Memcached:** Simple Key-Value Caching
- **Redis:** Caching + Multiple Data Structures + Additional Features

---

## 8. How Does Redis Store Data Internally?

### 8.1 Simple Meaning

Redis data ko primarily **Key-Value format** mein store karta hai.

Matlab har stored item ko access karne ke liye ek Key hoti hai aur us Key ke against ek Value associated hoti hai.

Redis sirf simple strings store nahi karta. Ye multiple data structures support karta hai, jaise:

- Strings
- Lists
- Sets
- Hashes
- Sorted Sets

Har data structure ka apna use case hota hai.

### 8.2 Real-Life Example – Trading Application

Suppose hamari Trading Application mein NIFTY aur BANKNIFTY ka price Redis mein store karna hai.

| Key | Value |
|---|---:|
| `NIFTY_PRICE` | `24500` |
| `BANKNIFTY_PRICE` | `52000` |

Jab Application Server ko NIFTY ka price chahiye, toh woh Redis ko `NIFTY_PRICE` key ke through request karega.

Redis us Key se associated Value return kar dega.

Example:

```text
GET NIFTY_PRICE

Response:
24500
```

Is tarah Application Server ko required data quickly mil jata hai.

### 8.3 Architecture Diagram

```text
          Application Server
                  |
                  v
             Redis Server
                  |
                  v
             Key-Value Store
                  |
            +-----+-----+
            |           |
            v           v
       NIFTY_PRICE  BANKNIFTY_PRICE
            |           |
            v           v
          24500       52000
```

### 8.4 Redis Data Structures

| Data Structure | Meaning | Trading Application Example |
|---|---|---|
| String | Single value store karne ke liye | `NIFTY_PRICE = 24500` |
| List | Ordered collection of values | Recent transaction events |
| Set | Unique values store karne ke liye | Unique active User IDs |
| Hash | Multiple fields ko ek Key ke under store karne ke liye | User Profile |
| Sorted Set | Score ke basis par ordered values | User Ranking / Leaderboard |

### 8.5 Interview Mein Kaise Explain Karein?

Redis stores data using a Key-Value model, where every key is associated with a value.

Apart from simple Strings, Redis supports multiple data structures like Lists, Sets, Hashes and Sorted Sets.

For example, in our Trading Application, we can store NIFTY's price using a key called `NIFTY_PRICE` and its corresponding value as `24500`.

Whenever the application needs this price, it sends the key to Redis, and Redis returns the associated value.

Depending on the requirement, we can also use other data structures. For example, Hashes can be used to store user profile fields, while Sets can be used to maintain unique User IDs.

**In Short:** Redis uses a Key-Value model and supports multiple data structures to store and manage different types of data efficiently.

---

## 9. What Is a Redis Key?

### 9.1 Simple Meaning

Redis mein **Key ek unique identifier hoti hai** jiske through hum stored data ko identify, access, update ya delete kar sakte hain.

Simple words mein, Key data ka naam ya reference hoti hai, aur us Key ke against Value store hoti hai.

### 9.2 Real-Life Example – Trading Application

Suppose humein Trading Application mein different instruments ke prices Redis mein store karne hain.

| Redis Key | Value |
|---|---:|
| `NIFTY_PRICE` | `24500` |
| `BANKNIFTY_PRICE` | `52000` |
| `RELIANCE_PRICE` | `2950` |

Agar Application Server ko NIFTY ka price chahiye, toh woh `NIFTY_PRICE` key request karega.

```text
GET NIFTY_PRICE

Response:
24500
```

Agar price update karna hai:

```text
SET NIFTY_PRICE 24550
```

Ab `NIFTY_PRICE` key ke against new value `24550` store ho jayegi.

### 9.3 Good Redis Key Naming

Redis Keys ko meaningful aur consistent names dene chahiye, taaki application mein unhe identify aur maintain karna easy ho.

Examples:

```text
NIFTY_PRICE
BANKNIFTY_PRICE
USER:1001:PROFILE
USER:1001:SESSION
ORDER:5001:STATUS
```

Colon (`:`) ka use naming convention ke liye kiya ja sakta hai. Ye Redis ki compulsory requirement nahi hai, bas keys ko readable aur organized banane ka common approach hai.

### 9.4 Interview Mein Kaise Explain Karein?

A Redis Key is a unique identifier used to identify and access a particular value stored in Redis.

For example, in our Trading Application, we can store NIFTY's price using the key `NIFTY_PRICE` and its value as `24500`.

Whenever the application needs the price, it uses the key to retrieve the associated value from Redis.

We should use meaningful and consistent key names so that data can be easily identified and managed.

**In Short:** Redis Key is an identifier used to store, access, update and delete the associated data.

---

## 10. What Is the Maximum Size of a Redis Key/Value?

### 10.1 Simple Meaning

Redis mein Key aur Value dono ki size limits hoti hain.

Redis String ki maximum size **512 MB** hoti hai. Since Redis Keys are also strings, the theoretical maximum size of a Key is also 512 MB.

Lekin practical applications mein itni large Keys ya Values use karna recommended nahi hota. Large data ko process karne mein memory consumption aur network overhead increase ho sakta hai.

### 10.2 Real-Life Example – Trading Application

Suppose hamari Trading Application mein NIFTY ka live price store karna hai.

```text
Key:
NIFTY_PRICE

Value:
24500
```

Yahan Key aur Value dono bahut small hain, isliye Redis unhe efficiently handle kar sakta hai.

Humein normally keys ko short, meaningful aur readable rakhna chahiye.

### 10.3 Important Points

- Redis String ki maximum size 512 MB hai.
- Redis Keys bhi strings hoti hain, isliye unki theoretical maximum size bhi 512 MB hai.
- Practical applications mein Keys aur Values ko unnecessarily large nahi rakhna chahiye.
- Large data store karne se memory usage aur network overhead increase ho sakta hai.
- Data ko application requirement ke according properly structure karna chahiye.

### 10.4 Interview Mein Kaise Explain Karein?

Redis supports String values up to a maximum size of 512 MB. Since Redis Keys are also strings, the theoretical maximum size of a Key is also 512 MB.

However, in real-world applications, we generally keep Keys short and meaningful. Very large Keys or Values can increase memory consumption and network overhead.

For example, in our Trading Application, instead of using a large Key, we can use a simple and meaningful key like `NIFTY_PRICE`.

**In Short:** Redis String ki maximum size 512 MB hoti hai, but practical applications mein Keys aur Values ko reasonably small rakhna better hota hai.

---

# Quick Revision – Redis Fundamentals

| No. | Interview Question | Key Point |
|---:|---|---|
| 1 | What Is Redis? | In-memory data store |
| 2 | Why Is Redis Called an In-Memory Database? | Data primarily RAM se access hota hai |
| 3 | What Problem Does Redis Solve? | Faster response and reduced Database load |
| 4 | Redis vs Traditional Database | Fast access vs persistent structured storage |
| 5 | Why Is Redis So Fast? | RAM, optimized data structures and efficient operations |
| 6 | Main Use Cases of Redis | Caching, Sessions, Real-Time Data, Rate Limiting and Messaging |
| 7 | Redis vs Memcached | Multiple data structures vs simple caching focus |
| 8 | How Does Redis Store Data? | Key-Value model and multiple data structures |
| 9 | What Is a Redis Key? | Identifier used to access a value |
| 10 | Maximum Key/Value Size | Redis String maximum size: 512 MB |

## One-Line Interview Summary

Redis ek fast in-memory data store hai jo primarily RAM mein data store karta hai. Iska use caching, session management, real-time data handling, rate limiting aur messaging jaise use cases mein hota hai. Redis frequently accessed data ko quickly serve karke application performance improve karne aur Database par repeated requests ka load reduce karne mein help karta hai.

# 2. Redis Data Structures (Very Important)
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

# 3. Caching Concepts
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



# 4. Persistence (Very Important)
## Does Redis persist data?
1. Analogy
-- Socho tumhara whiteboard hai office mein (Redis = RAM)
-- Sab kuch fast likho, fast padhlo — but light chali gayi toh sab gaya ❌
-- Ab socho tumne whiteboard ki photo le li (RDB Snapshot) — light aayi toh photo dekh ke restore kar lo ✅
-- Ya alternatively tumne har change ek diary mein likha (AOF Log) — ek ek step record hai ✅
-- Redis bhi yehi karta hai — by default volatile hai, but persistence ON kar sakte ho

2. Technical Kya Hua
-- By Default Redis data persisit nahi karta -> Server crash = data gone
-- But Redis 2 persistence options deta hai:
    RDB — Redis Database Snapshot
        - Har N seconds pe ek snapshot leta hai disk pe
        - Ek .rdb file banti hai
        - Fast restore hoti hai — but last snapshot ke baad ka data lost ho sakta hai
        - Use karo jab: backup chahiye, thoda data loss acceptable hai
    AOF — Append Only File
        - Har write operation ek file mein log hoti hai
        - Crash ke baad sab operations replay hote hain
        - Data loss almost zero — but file badi hoti jaati hai
        - Use karo jab: data loss bilkul nahi chahiye
-- RDB + AOF Dono — Best of Both
    - Production mein dono saath use karo
    - AOF = durability, RDB = fast restart

3. Interview Pe Kaise Bolo
-- Redis by default in-memory hai — restart pe data jaata hai
-- Do persistence modes hain — RDB aur AOF
    - RDB = periodic snapshot, fast restart, thoda data loss possible
    - AOF = har write log hoti hai, almost no data loss, slow restart
-- Production mein dono use karte hain — RDB for backup speed, AOF for durability
-- Agar poochha "Redis reliable hai kya?" toh bolo: "Persistence configure karein toh haan — but primary database replace nahi karta, complementary hai"
-- Cache use case mein persistence zaroori nahi — data toh DB mein already hai, Redis toh sirf speed ke liye hai

4. System Design
-- Pure caching ke liye persistence OFF rakho — restart pe DB se refill ho jaayega, no issue
-- Session store ke liye AOF ON karo — user ka login data nahi jaana chahiye
-- Leaderboard / Real-time counters ke liye RDB + AOF dono — data critical hai
-- Redis Sentinel / Redis Cluster use karo production mein — single point of failure avoid karo
-- Redis ko primary DB ki jagah use nahi karte — it's a complementary layer for speed

5. Summary 
-- Redis by default volatile hai 
--  but RDB aur AOF persistence modes se data survive kar sakta hai crashes ke baad.
-- Production mein dono use karte hain based on durability requirement.

## What is RDB persistence?
RDB — Redis Database Snapshot
        - Har N seconds pe ek snapshot leta hai disk pe
        - Ek .rdb file banti hai
        - Fast restore hoti hai — but last snapshot ke baad ka data lost ho sakta hai
        - Use karo jab: backup chahiye, thoda data loss acceptable hai

## What is AOF (Append Only File)?
AOF — Append Only File
        - Har write operation ek file mein log hoti hai
        - Crash ke baad sab operations replay hote hain
        - Data loss almost zero — but file badi hoti jaati hai
        - Use karo jab: data loss bilkul nahi chahiye

## What is snapshotting in Redis?
1. Analogy
-- Resident Evil 4 : concept Of Saving Game.

1. Techincal
-- RDB = Point-in-time snapshot of entire Redis data — ek .rdb file banti hai disk pe
-- Redis BGSAVE command use karta hai internally
-- BGSAVE kaise kaam karta hai:
    - Redis ek child process fork karta hai
    - Child process disk pe snapshot likhta hai
    - Main process bina ruke serve karta rehta hai requests
    - Fork ke time Copy-on-Write (COW) memory technique use hoti hai — memory double nahi hoti
-- Snapshot complete hone pe nayi .rdb file purani ko replace kar deti hai
-- Default Trigger Condition
    - save 3600 1 → 1 change hua ho toh 1 ghante mein save
    - save 300 100 → 100 changes hue hon toh 5 min mein save
    - save 60 10000 → 10,000 changes hue hon toh 60 sec mein save


## What is fsync policy in Redis?
## When would you use RDB vs AOF?

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