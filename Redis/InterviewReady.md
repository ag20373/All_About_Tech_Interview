# Redis Interview Quick Sheet
### Quick revision notes | Simple Hinglish | Everyday human-life examples

**How to use this sheet:** Har topic ka simple meaning samjho, example se relate karo, aur interview answer ko apne words mein explain karo. Answers intentionally short rakhe gaye hain.

---

# 1. Redis Fundamentals

## 1. What Is Redis?
**Interview Mein Kaise Explain Karein?**
- Redis ek fast **in-memory data store** hai jo data primarily RAM mein store karta hai.
- RAM se data access fast hota hai, isliye Redis low-latency responses de sakta hai.
- Iska use caching, sessions, counters aur real-time data ke liye hota hai.
- **Real-life example:** Ghar mein roz use hone wali cheezon ki list fridge par chipka dete ho, taaki baar-baar cupboard ya notebook na dekhni pade. Redis bhi frequently needed information ko quickly available rakhta hai.
- Application pehle Redis check karegi; data na mile toh original source/Database se fetch karegi.

## 2. Why Is Redis Called an In-Memory Database?
**Interview Mein Kaise Explain Karein?**
- Redis data ko primarily RAM mein store aur access karta hai.
- RAM disk ke comparison mein fast hoti hai, isliye read/write operations low latency de sakte hain.
- Redis persistence options bhi support karta hai, so data disk par save kiya ja sakta hai.
- **Real-life example:** Jaise phone ke recent contacts yaad/recent list mein mil jaate hain, toh har baar diary mein number dhoondhna nahi padta. RAM se data access karna bhi disk se access karne ke comparison mein fast hota hai.

## 3. What Problem Does Redis Solve?
**Interview Mein Kaise Explain Karein?**
- Redis repeated data requests ko fast serve karke Database ka load reduce karne mein help karta hai.
- Frequently accessed data memory mein available rehta hai.
- Isse response time improve ho sakta hai aur high read traffic handle karna easier hota hai.
- **Real-life example:** Office reception par visitor list ki frequently needed copy desk par rakhi ho, toh har visitor ke liye records room nahi jaana padta. Redis repeated requests ko quickly serve karke main Database ka load kam karta hai.

## 4. Redis vs Traditional Database
**Interview Mein Kaise Explain Karein?**
- Redis primarily RAM se fast data access provide karta hai; relational Databases persistent, structured data manage karte hain.
- Redis key-value model aur data structures use karta hai; MySQL/PostgreSQL tables, rows aur SQL use karte hain.
- Redis cache, sessions aur real-time data ke liye useful hai.
- Traditional Database user records, orders aur transaction history ke liye useful hai.
- **Example:** Supermarket mein popular item ki quick-access stock list cache mein ho sakti hai; customer bills aur purchase history permanent Database mein maintain hoti hai.

## 5. Why Is Redis So Fast?
**Interview Mein Kaise Explain Karein?**
- Redis primarily RAM se data access karta hai, disk se nahi.
- Ye Strings, Lists, Sets, Hashes aur Sorted Sets jaise optimized data structures provide karta hai.
- Common operations efficiently execute hote hain.
- Cache use karne se repeated Database calls bhi kam hoti hain.
- **Example:** Kitchen mein chai banane ke liye sugar aur tea leaves counter par rakhe hon, toh har baar store room nahi jaana padta. Frequently used data RAM se milne aur efficient data structures ki wajah se Redis fast hota hai.

## 6. What Are the Main Use Cases of Redis?
**Interview Mein Kaise Explain Karein?**
- **Caching:** Frequently used data fast serve karna.
- **Session Management:** User login session maintain karna.
- **Real-time Data:** Live prices/counters access karna.
- **Rate Limiting:** API requests control karna.
- **Messaging:** Services ke beech events/messages exchange karna.
- **Example:** Shopping app mein Redis product details cache kar sakta hai, login session yaad rakh sakta hai, repeated coupon/API attempts limit kar sakta hai aur order updates services tak bhej sakta hai.

## 7. Redis vs Memcached
**Interview Mein Kaise Explain Karein?**
- Dono in-memory systems hain aur caching ke liye use hote hain.
- Memcached mainly simple Key-Value caching par focused hai.
- Redis Strings, Lists, Sets, Hashes, Sorted Sets, Streams aur additional features support karta hai.
- Redis persistence options bhi provide karta hai; Memcached generally cache-only hota hai.
- **Example:** Memcached ko ek simple shelf samjho jahan frequently used items rakhte ho. Redis ek organised utility shelf jaisa hai jahan different types ke items aur unke operations bhi manage kar sakte ho.

## 8. How Does Redis Store Data Internally?
**Interview Mein Kaise Explain Karein?**
- Redis data ko **Key-Value** model mein store karta hai.
- Key data ka identifier hoti hai aur Value uske against stored data hota hai.
- Value String ya Redis ke supported data structures mein ho sakti hai.
- **Example:** Phone contacts mein naam key ki tarah aur phone number value ki tarah hota hai. Redis mein `FAVOURITE_DISH` key ke against `Rajma Chawal` value ho sakti hai.
- `GET ROOM_TEMP` command se value retrieve kar sakte hain.

## 9. What Is a Redis Key?
**Interview Mein Kaise Explain Karein?**
- Redis Key ek identifier hai jisse stored data ko access, update ya delete karte hain.
- Har Key ke against ek value associated hoti hai.
- Keys ko meaningful aur consistent rakhna chahiye.
- **Example:** `ROOM_TEMP`, `USER:1001:SESSION`, `ORDER:5001:STATUS`.
- `GET ROOM_TEMP` se associated value mil sakti hai.

## 10. What Is the Maximum Size of a Redis Key/Value?
**Interview Mein Kaise Explain Karein?**
- Redis String ki maximum size **512 MB** hoti hai.
- Redis Keys bhi strings hoti hain, isliye unki theoretical maximum size bhi 512 MB hai.
- Practical applications mein Keys short aur meaningful rakhni chahiye.
- Very large values memory aur network overhead badha sakti hain.
- **Example:** Ghar ke storage boxes par `Winter Clothes` ya `Documents` jaise short labels lagate hain, poora paragraph nahi. Redis Keys bhi short, clear aur meaningful rakhni chahiye.

---

# 2. Redis Data Structures

## 1. What Data Structures Does Redis Support?
**Interview Mein Kaise Explain Karein?**
- Redis Strings, Lists, Sets, Sorted Sets, Hashes, Bitmaps, HyperLogLog aur Streams support karta hai.
- Har structure ka use different type ki requirement ke liye hota hai.
- **Daily-life examples:** String—room temperature; List—shopping list; Set—unique guests invited to a party.
- Sorted Set—class marks ranking; Hash—one person's contact card; Bitmap—daily attendance marked yes/no.
- HyperLogLog—approximate count of unique visitors at a fair; Stream—sequence of parcel delivery updates.
- Correct structure choose karne se data manage karna easier hota hai.

## 2. What Is a String Data Type in Redis?
**Interview Mein Kaise Explain Karein?**
- String Redis ka simplest data type hai.
- Ismein ek Key ke against single value store hoti hai; value text, number, JSON text ya binary data ho sakti hai.
- Common commands: `SET`, `GET`, `INCR`, `DECR`, `EXPIRE`, `TTL`.
- **Example:** `SET ROOM_TEMP 24` se room temperature store kar sakte hain aur `GET ROOM_TEMP` se read kar sakte hain.
- API request counter ke liye `INCR API_REQUEST_COUNT` use kar sakte hain.

## 3. What Is a List in Redis?
**Interview Mein Kaise Explain Karein?**
- List ordered collection of Strings hoti hai; duplicate values allowed hain.
- Elements beginning ya end se add/remove kar sakte hain.
- Commands: `LPUSH`, `RPUSH`, `LPOP`, `RPOP`, `LRANGE`.
- **Example:** Shopping list mein items ko jis order mein add kiya, us order mein maintain karna; ya kitchen ke recent tasks ki list rakhna.
- Simple queue ke liye List useful hai; reliable event processing ke liye Streams better ho sakte hain.

## 4. What Is a Set in Redis?
**Interview Mein Kaise Explain Karein?**
- Set unordered collection of unique Strings hota hai.
- Duplicate members automatically store nahi hote.
- Commands: `SADD`, `SREM`, `SMEMBERS`, `SISMEMBER`, `SINTER`.
- **Example:** Birthday party ke invitees ki unique list maintain karna. Ek hi guest ka naam dobara add karne par duplicate entry nahi banti.
- `SISMEMBER ACTIVE_USERS USER_101` se check kar sakte hain ki user Set mein hai ya nahi.

## 5. What Is a Sorted Set (ZSET)?
**Interview Mein Kaise Explain Karein?**
- Sorted Set mein har member unique hota hai aur uske saath numerical Score hota hai.
- Redis members ko Score ke basis par sorted order mein maintain karta hai.
- Commands: `ZADD`, `ZRANGE`, `ZREVRANGE`, `ZSCORE`, `ZRANK`.
- **Example:** School ke students ko exam marks ke basis par rank karna. Har student ka score hota hai aur list score ke order mein rehti hai.
- Highest profit wale customers dekhne ke liye `ZREVRANGE` use kar sakte hain.

## 6. What Is a Hash in Redis?
**Interview Mein Kaise Explain Karein?**
- Hash ek Redis Key ke andar multiple Field-Value pairs store karta hai.
- Isse small object ya record ki tarah samajh sakte hain.
- Commands: `HSET`, `HGET`, `HGETALL`, `HDEL`, `HEXISTS`.
- **Example:** Ek contact card mein person's name, phone number, email aur city ko alag-alag fields mein rakhna.
- `HGET USER:1001 name` se sirf name retrieve kar sakte hain.

## 7. What Is a Bitmap?
**Interview Mein Kaise Explain Karein?**
- Bitmap Redis String ke individual bits par operations karne ka feature hai.
- Har bit `0` ya `1` ho sakti hai, yani false/true status.
- Commands: `SETBIT`, `GETBIT`, `BITCOUNT`.
- **Example:** School attendance register mein har student ke liye present/absent ko 1/0 ke form mein track karna.
- `1` means login recorded; `0` means login recorded nahi hai.

## 8. What Is a HyperLogLog?
**Interview Mein Kaise Explain Karein?**
- HyperLogLog large dataset mein unique elements ka **approximate count** calculate karta hai.
- Iska advantage hai ki bahut kam memory use karta hai.
- Result exact nahi hota; standard error approximately 0.81% hota hai.
- Commands: `PFADD`, `PFCOUNT`, `PFMERGE`.
- **Example:** Mela ya exhibition mein approximate unique visitors count karna, chahe kuch log baar-baar gate se aaye hon. HyperLogLog exact identity list nahi deta, approximate count deta hai.

## 9. What Is a Stream in Redis?
**Interview Mein Kaise Explain Karein?**
- Redis Stream messages/events ko append-only, ordered log ki tarah store karta hai.
- Har entry ki unique ID hoti hai.
- Consumer Groups multiple consumers ko events process karne mein help karte hain.
- Commands: `XADD`, `XREAD`, `XREADGROUP`, `XACK`.
- **Example:** Parcel delivery ke events—Booked → Dispatched → Out for Delivery → Delivered—ko sequence mein record karke different teams/services se process karwana.

## 10. When Should You Use Each Redis Data Structure?
**Interview Mein Kaise Explain Karein?**
- Single value/counter chahiye → **String**.
- Ordered items chahiye → **List**; unique items chahiye → **Set**.
- Score-based ranking chahiye → **Sorted Set**; object ke fields chahiye → **Hash**.
- Boolean activity tracking → **Bitmap**; approximate unique count → **HyperLogLog**.
- Ordered event processing → **Stream**.
- **Example:** Home organiser mein room temperature String, unique guests Set, marks leaderboard Sorted Set aur parcel status updates Stream mein rakh sakte hain.

---

# 3. Caching Concepts

## 1. What Is Caching?
**Interview Mein Kaise Explain Karein?**
- Caching mein frequently accessed data ki copy fast storage mein temporarily store karte hain.
- Next request par application data ko original Database se fetch karne ke bajay cache se le sakti hai.
- Data mil jaye toh **Cache Hit**; na mile toh **Cache Miss**.
- Cache Miss par application Database se data fetch karke cache mein store kar sakti hai.
- **Example:** Roz subah weather app ka temperature baar-baar check karte ho; app latest result ko cache karke next view par quickly dikha sakti hai.

**Simple flow (important):**
```text
Request → Redis Cache
             |
        +----+----+
        |         |
      Hit       Miss
        |         |
     Return    Database
                 |
             Store Cache
                 |
               Return
```

## 2. Why Is Redis Commonly Used as a Cache?
**Interview Mein Kaise Explain Karein?**
- Redis primarily RAM se data serve karta hai, isliye access fast ho sakta hai.
- Ye TTL, multiple data structures aur atomic operations support karta hai.
- Frequently requested data ko cache karke repeated Database calls reduce kar sakte hain.
- **Example:** Restaurant menu ki frequently requested copy fast-access storage mein rakhna, taaki har customer ke liye full records dobara na nikaalne padein.
- Isse response time aur backend resource usage improve ho sakte hain.

## 3. What Is Cache Eviction?
**Interview Mein Kaise Explain Karein?**
- Cache eviction ka matlab memory limit reach hone par existing cache Keys remove karna hai.
- Redis configured eviction policy ke according decide karta hai kaunsi Key remove ho sakti hai.
- Eviction ka matlab hamesha oldest inserted Key delete karna nahi hota.
- **Example:** Phone storage/cache ki limited jagah bhar jaaye, toh system policy ke hisaab se kuch purani temporary files hata sakta hai taaki nayi files ke liye jagah bane.
- Agar policy `noeviction` hai, toh write operation fail ho sakti hai.

## 4. What Are Redis Eviction Policies?
**Interview Mein Kaise Explain Karein?**
- Eviction policy decide karti hai memory limit par Redis kaunsi Keys remove karega.
- `noeviction`—Keys remove nahi karta; memory limit par writes fail ho sakti hain.
- `allkeys-lru`—all Keys mein least recently used ko prefer karta hai; `allkeys-lfu`—least frequently used ko.
- `allkeys-random`—all Keys mein random selection.
- `volatile-lru`, `volatile-lfu`, `volatile-random`—sirf TTL wali Keys mein selection.
- `volatile-ttl`—TTL wali Keys mein shortest remaining TTL ko prefer karta hai.
- **Example:** Study desk par jagah kam ho toh jo books sabse kam use hoti hain unhe shelf par rakh sakte ho (LFU), ya jo book sabse der se use hui use hata sakte ho (LRU). Policy need par depend karti hai.

## 5. What Is Cache Invalidation?
**Interview Mein Kaise Explain Karein?**
- Cache invalidation ka matlab original data change hone par old cached data delete ya update karna hai.
- Agar cache update nahi hua, toh application stale/old data return kar sakti hai.
- Common approaches: cache Key delete karna, cache update karna, TTL ya event-based invalidation.
- **Example:** Tumne phone mein kisi friend ka address change kiya; purana saved address update/delete karna hoga, warna delivery galat jagah jaayegi.
- Next read par application latest profile load kar sakti hai.

## 6. What Is the Cache-Aside Pattern?
**Interview Mein Kaise Explain Karein?**
- Cache-Aside mein application khud Cache aur Database manage karti hai.
- Read par pehle Redis check hota hai; Cache Hit par data return hota hai.
- Cache Miss par Database se data fetch karke Redis mein store karte hain.
- Update ke baad common approach Database update karke related cache Key delete karna hai.
- **Example:** Guest ka phone number contact list mein nahi milta, toh tum diary se number dekhte ho aur phir contacts mein save kar lete ho. Next time directly contacts se mil jaata hai.

**Simple flow (important):**
```text
Read → Check Redis → Hit: Return
                 └→ Miss: Read DB → Set Redis → Return
Update → Update DB → Delete Redis Key
```

## 7. What Is Write-Through Caching?
**Interview Mein Kaise Explain Karein?**
- Write-Through mein write workflow ke part ke roop mein Cache aur Database dono update hote hain.
- Isse subsequent reads ke liye updated value cache mein available ho sakti hai.
- Write operation mein dono stores update karne padte hain, isliye latency badh sakti hai.
- Ek store update ho aur doosra fail ho, toh failure handling zaroori hai.
- **Example:** Tum apna new home address address book aur family emergency list dono mein ek hi update process ke dauraan change kar dete ho, taaki dono jagah same information rahe.

## 8. What Is TTL-Based Invalidation?
**Interview Mein Kaise Explain Karein?**
- TTL ka full form **Time To Live** hai.
- Ye define karta hai ki Redis Key kitne time tak valid/available rahegi.
- TTL complete hone par Key expire ho jati hai; next request Cache Miss ho sakti hai.
- Commands: `SET key value EX seconds` aur `TTL key`.
- **Example:** Fridge par laga milk reminder note sirf ek din ke liye useful hai; expiry ke baad use hata dena chahiye. TTL bhi cached item ko set time ke baad expire karta hai.
- TTL old data ka risk reduce karta hai, lekin data update hote hi cache refresh hone ki guarantee nahi deta.

## 9. What Is Cache Stampede?
**Interview Mein Kaise Explain Karein?**
- Cache Stampede tab hota hai jab popular cache entry expire/missing ho aur bahut saari requests ek saath Cache Miss kar dein.
- Ye requests same data ke liye simultaneously Database ko hit kar sakti hain.
- Isse Database load, latency aur connection usage suddenly increase ho sakte hain.
- **Example:** Popular online ticket booking page ki cached information expire hote hi bahut saare log ek saath same page kholte hain, aur sab requests backend par pahunch jaati hain. Ye sudden load Cache Stampede jaisa hai.
- Multiple requests Database ko hit karne ke bajay refresh ko coordinate karna chahiye.

## 10. How Do You Prevent Cache Stampede?
**Interview Mein Kaise Explain Karein?**
- **Mutex/Distributed Lock:** Ek request lock lekar Database se data refresh kare; others wait ya cache retry karein.
- **Early Refresh:** TTL expire hone se pehle background mein cache refresh kar dein.
- **Probabilistic Early Expiration:** Selected requests probability ke basis par early refresh trigger karein.
- In approaches ka goal same missing data ke liye simultaneous Database calls reduce karna hai.
- **Example:** Ghar mein drinking water khatam hone ka wait nahi karte; bottle pehle hi refill kar dete ho. Isi tarah cache expiry se pehle refresh karne se sudden load kam hota hai.

---

# Last-Minute Interview Revision

| Topic | One-line recall |
|---|---|
| Redis | Fast in-memory data store |
| In-Memory | Data primarily RAM se access hota hai |
| Cache Hit | Data Redis mein mil gaya |
| Cache Miss | Data Redis mein nahi mila |
| TTL | Key ki expiry duration |
| Eviction | Memory pressure par Keys remove karna |
| LRU | Least recently used |
| LFU | Least frequently used |
| Cache Invalidation | Old cache delete/update karna |
| Cache-Aside | App cache check karti hai, miss par DB se load |
| Write-Through | Write workflow mein Cache + DB update |
| Cache Stampede | Same expired Key par many simultaneous misses |

## One-Minute Interview Summary

Redis ek fast in-memory data store hai jo primarily RAM mein data store karta hai. Iska use caching, session management, counters, rate limiting aur real-time applications mein hota hai. Redis Strings, Lists, Sets, Sorted Sets, Hashes, Bitmaps, HyperLogLog aur Streams jaise data structures support karta hai. Caching se frequently accessed data quickly serve hota hai aur repeated Database calls reduce ho sakti hain. Cache ko properly manage karne ke liye TTL, eviction policies, cache invalidation aur stampede prevention important concepts hain.
