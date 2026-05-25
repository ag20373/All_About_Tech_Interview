# BASICS (Start Here)
## Q1 : What is a thread in C# and how is it different from a process? 🔥
1. Analogy
-- Process = Resturant
    - Restaurant (Process) ek complete system hai (kitchen, tables, billing)
-- Thread = Waiters inside that restaurant
    - Waiters (Threads) ka kaam hai orders lena, serve karna, etc.
-- Important 
    - Ek restaurant me multiple waiters ho sakte hain (multiple threads)
    - Har waiter same kitchen use karta hai (shared memory)

2. Technical
-- Process kya hai?
    - Process ek independent running application hota hai
    - Apni separate memory space hoti hai
    - Example: Chrome, Visual Studio
-- Thread kya hai?
    - Thread ek lightweight execution unit hai
    - Process ke andar run karta hai
    - Same process ke threads memory share karte hain

3. Key Differences
| Feature       | Process         | Thread                       |
| ------------- | --------------- | ---------------------------- |
| Memory        | Separate memory | Shared memory                |
| Creation Cost | High            | Low                          |
| Communication | Slow (IPC)      | Fast (shared data)           |
| Isolation     | High (safe)     | Low (risky - race condition) |
| Example       | Chrome app      | Chrome tab worker            |

4. Important Interview Points
-- Why threads are faster than processes?
    - Because threads share memory (no need for IPC)
-- What problem occurs due to shared memory?
    - Race Condition / Deadlock
-- Can threads exist without process?
    - No — thread always belongs to a process
-- Is every app single-threaded?
    - No — most apps are multi-threaded
-- What is main thread?
    - Jab app start hoti hai → ek default thread hota hai (Main Thread)
-- Threads share memory → powerful but dangerous
-- Agar synchronization nahi use kiya → bugs

5. Code Example
-- Basic Thread Example
    using System;
    using System.Threading;

    class Program
    {
        static void PrintNumbers()
        {
            for (int i = 1; i <= 5; i++)
            {
                Console.WriteLine("Child Thread: " + i);
                Thread.Sleep(500);
            }
        }

        static void Main()
        {
            Thread t = new Thread(PrintNumbers);
            t.Start();

            for (int i = 1; i <= 5; i++)
            {
                Console.WriteLine("Main Thread: " + i);
                Thread.Sleep(500);
            }
        }
    }
.............
-- Process Example
    using System.Diagnostics;

    Process.Start("notepad.exe");

5. Summary
-- Process ek independent application hota hai jiska apna memory space hota hai.
-- Thread ek lightweight execution unit hai jo process ke andar run karta hai.
-- Threads memory share karte hain → fast but risky.
-- Processes isolated hote hain → safe but slow.

## Q2 : How does multithreading improve application performance? 🔥
-- Multithreading allows:
👉 Multiple tasks to run concurrently (ya parallel)

Q Performance kaise improve hoti hai?
1. Better CPU Utilization
-- Single thread → CPU idle ho sakta hai
-- Multiple threads → CPU busy rehta hai
-- Example :
    - Ek thread I/O wait kar raha hai
    - Dusra thread CPU work kar leta hai

2. Parallel Execution (Multi-core CPUs)
-- Aajkal CPUs me multiple cores hote hain
-- Threads alag-alag cores pe run kar sakte hain

3. Improved Responsiveness (UI Apps)
-- UI freeze nahi hoti 
-- Background me heavy task run hota hai

4. Efficient I/O Handling
-- Network / DB calls me waiting hoti hai
-- Thread free ho jata hai → dusra kaam kar sakta hai

-> Golden Rule
"Multithreading improves performance by utilizing CPU efficiently and allowing concurrent execution, but excessive threads can actually reduce performance due to overhead."

## Q3 : What are the different ways to create a thread in C#?🔥
1. Analogy
-- Manual driver hire karna (Thread class)
    - Har delivery ke liye driver khud hire karo
    - Control zyada, but effort bhi zyada
-- Company ke drivers use karna (ThreadPool)
    - Ready drivers available hain
    - Fast & efficient
-- Swiggy/Zomato system (Task)
    - Tu bas order de → system manage karega
    - Best & modern approach

2. Technical Explanation
-- Using Thread Class (Traditional Way)
    - Direct OS thread create karta hai
    - Full control milta hai
    - Heavy & costly
-- Using ThreadPool
    - Pre-created threads ka pool hota hai
    - Fast execution
    - Limited control
-- Using Task (Recommended 🚀)
    - Modern approach (Task Parallel Library)
    - Internally ThreadPool use karta hai
    - Async programming ke saath best

3. Difference
| Method     | Control    | Performance | Recommended |
| ---------- | ---------- | ----------- | ----------- |
| Thread     | High       | Slow        | ❌ Rare      |
| ThreadPool | Medium     | Fast        | ✅           |
| Task       | High-level | Very Fast   | 🚀 Best     |

4. Important Interview Points
-- In modern C#, Task is preferred over Thread.
-- Thread kab use kare?
    - Jab full control chahiye (priority, long-running thread)
-- ThreadPool limitation:
    - No control over thread lifecycle
    - Background threads hote hain
-- Task advantages:
    - Easy error handling
    - Continuation support
    - Async/await support

5. Code
-- Using Thread
    using System;
    using System.Threading;

    class Program
    {
        static void Main()
        {
            Thread t = new Thread(Work);
            t.Start();
        }

        static void Work()
        {
            Console.WriteLine("Thread is running");
        }
    }
.......
-- Using ThreadPool
    using System;
    using System.Threading;

    class Program
    {
        static void Main()
        {
            ThreadPool.QueueUserWorkItem(Work);
        }

        static void Work(object state)
        {
            Console.WriteLine("ThreadPool thread running");
        }
    }
.......
-- Using Task
    using System;
    using System.Threading.Tasks;

    class Program
    {
        static void Main()
        {
            Task.Run(() => 
            {
                Console.WriteLine("Task is running");
            });
        }
    }

6. Summary
-- C# me threads create karne ke 3 main ways hain:
    - Thread class → low-level, heavy
    - ThreadPool → efficient but less control
    - Task → modern, scalable, recommended
-- Task internally ThreadPool use karta hai
-- Most real-world apps me Task + async/await use hota hai

## Q4 : What is the difference between a foreground thread and a background thread?
1. Analogy
-- Soch tu ek office 🏢 me kaam kar raha hai:
-- Foreground Thread
    - Main employees
    - Jab tak yeh kaam kar rahe hain → office open hai
-- Background Thread
    - Cleaning staff
    - Agar main employees chale gaye → cleaning bhi band ho jayegi
-- Key Ideas
    - Foreground = important kaam
    - Background = supporting kaam

2. Foreground Thread (important kaam)
-- Application ko Alive rakhta hai.
-- Jab tak koi foreground thread chal raha hai -> app close nahi hoti.

3. Background Thread (supporting kaam)
-- Low priority / helper work karta hai
-- Agar saare foreground threads finish ho gaye
-- CLR automatically background threads ko terminate kar deta hai

4. Important
-- CLR does not wait for background threads to finish.
-- By default:
    - Main() thread → Foreground
    - ThreadPool / Task → Background
-- How to convert? 
    "t.IsBackground = true;"
-- Use Case
    - Foreground ( File save , Payment processing )
    - Background (Logging , Email Sending)

4. Code
    using System;
    using System.Threading;

    class Program
    {
        static void Main()
        {
            Thread t = new Thread(DoWork);

            t.IsBackground = true; // Background thread
            t.Start();

            Console.WriteLine("Main thread completed");
        }

        static void DoWork()
        {
            for (int i = 1; i <= 5; i++)
            {
                Console.WriteLine("Background working: " + i);
                Thread.Sleep(1000);
            }
        }
    }
-- OutPut :
    - Ho sakta hai sirf "Main thread completed" print ho
    - Background thread complete hone se pehle hi app band ho jaye
-- Same With Foreground
    "t.IsBackground = false;"
    - Ab program wait karega jab tak thread complete na ho jaye

5. Summary 
-- Foreground thread application ko alive rakhta hai
-- Background thread app close hone par terminate ho jata hai
-- CLR background threads ka wait nahi karta
-- Critical work → foreground
-- Non-critical work → background

## Q5 : What is context switching and why is it expensive?
1. Analogy
-- Soch tu ek chef 👨‍🍳 hai aur ek hi time pe 3 dishes bana raha hai:
    - Dish 1 → start ki
    - Fir Dish 2 pe switch
    - Fir Dish 3
    - Fir wapas Dish 1
-- Har Switch me :
    - Tu yaad karta hai kaha tak banaya tha
    - Tools chnage karta hai.
    - Ingredients adjust karta hai
-- Yeh jo switching ka overhead hai → wahi context switching hai

2. Technical Explanation
-- Context Switching kya hai?
    - Jab CPU ek thread/process se dusre pe switch karta hai
    - us process ko kehte hain Context Switching
-- Context me kya store hota hai?
    - CPU ko yeh sab save/restore karna padta hai:
        - Program Counter (kaunsa instruction chal raha tha)
        - Registers
        - Stack Pointer
        - Thread state
    - Isko bolte hain thread context
-- Flow
    - Current thread pause hota hai
    - Uska state save hota hai
    - Next thread ka state load hota hai
    - Execution resume hota hai

3. Important (Why Expensive)
-- CPU Time Waste 
    - Actual work nahi ho raha
    - Sirf switching ho rahi hai.
-- Memory Operations
    - Save + Load context
    - Cache miss ho sakta hai
-- Cache Invalidations
    - New thread → new data
    - CPU cache useless ho jata hai
-- Too Many Threads Problem
    - Zyada threads = zyada switching = performance down

4. Golder Rule
Context switching is expensive because it involves saving and restoring thread state, CPU cycles, and cache invalidation, which reduces actual execution time.

5. Code Example
-- Bad Approach
    for (int i = 0; i < 1000; i++)
    {
        new Thread(() =>
        {
            Console.WriteLine("Work");
        }).Start();
    }
    -- Result:
        - 1000 threads ❌
        - Heavy context switching ❌
        - Performance degrade 😵
.......
-- Good Approach(Task / ThreadPool)
    using System.Threading.Tasks;

    for (int i = 0; i < 1000; i++)
    {
        Task.Run(() =>
        {
            Console.WriteLine("Work");
        });
    }
    -- Thread reuse → less switching

5. Summary
-- Context switching = CPU switching between threads/processes
-- Isme thread state save + restore hota hai
-- Yeh expensive hai because:
    - CPU time waste hota hai
    - Memory operations hoti hain
    - Cache miss hota hai
-- Too many threads → performance degrade


## Q6 : What is thread lifecycle in .NET?
1. Analogy
-- 👉 Soch ek employee 👨‍💼 ka lifecycle:
    - Hire hua → (New)
    - Kaam assign hone ka wait → (Ready)
    - Kaam kar raha hai → (Running)
    - Break pe gaya → (Waiting/Blocked)
    - Kaam khatam → (Terminated)
-- Same flow thread ka hota hai

2. Technical Explanation
-- Unstarted(New)
    - Thread create hua hai
    - .Start() nahi hua abhi
    Thread t = new Thread(Work); // New state
-- Runnable/Ready
    - .Start() call ho gaya
    - CPU ka wait kar raha hai
-- Running
    - Thread actively CPU pe execute ho raha hai
-- Waiting / Blocked
    - Thread temporarily ruk gaya
    - Reasons:
        - Thread.Sleep()
        - lock
        - Wait()
        - I/O operations
-- Stopped / Terminated
    - Execution Complete
    - Ya exception aa gaya

3. Flow 
New → Runnable → Running → Waiting → Running → Terminated

4. Important
-- Thread ek time pe ek hi state me hota hai
-- Running ↔ Waiting multiple times ho sakta hai
-- Once terminated → restart nahi kar sakte ❌
-- Can we restart a thread? Ek baar thread finish ho gaya → new thread banana padega

5. Common Methods affecting lifecycle:
| Method  | Effect                  |
| ------- | ----------------------- |
| Start() | New → Runnable          |
| Sleep() | Running → Waiting       |
| Join()  | Wait for another thread |
| Abort() | Force stop (obsolete ❌) |

6. Summary
-- Thread lifecycle me major states hote hain:
    - New (Unstarted)
    - Runnable
    - Running
    - Waiting / Blocked
    - Terminated
-- Thread multiple times wait aur run ke beech switch kar sakta hai
-- Once terminated → restart possible nahi
-- OS scheduler decide karta hai kaunsa thread run karega

## Q7 : What is the difference between Thread class and ThreadPool?🔥
1. analogy
-- 👉 Soch tu ek company chalata hai
-- Thread (Manual Hiring)
    - Har kaam ke liye naya employee hire kar raha hai
    - Time lagta hai ⏳ + cost high 💸
-- ThreadPool (Existing Employees)
    - Already trained employees ready hain
    - Tu bas kaam assign karta hai
    - Fast + efficient

2. Difference
| Feature        | Thread                | ThreadPool    |
| -------------- | --------------------- | ------------- |
| Creation       | New thread every time | Reuse threads |
| Performance    | Slow                  | Fast          |
| Resource Usage | High                  | Low           |
| Control        | Full control          | Limited       |
| Use Case       | Long-running tasks    | Short tasks   |

3. Important
-- ThreadPool improves performance by reducing thread creation overhead.
-- ThreadPool threads: Always background threads hote hain
-- Thread kab use kare?
    - Long-running task
    - Dedicated thread chahiye
-- ThreadPool kab use kare?
    - Short tasks
    - High concurrency
-- Long-running task ThreadPool me daal diya ,Tho Pool block ho jayega
-- ThreadPool automatically manage karta hai: 
    - Number of threads
    - Load balancing

4. Code
-- Thread
        Thread t = new Thread(Work);
        t.Start();
-- Thread Pool
        ThreadPool.QueueUserWorkItem(Work);

5. Summary
-- Thread:
    - New thread create karta hai
    - Heavy but full control
-- ThreadPool :
    - Existing threads reuse karta hai
    - Fast & efficient
    - Limited control
-- Modern C#
    - Prefer Task (ThreadPool based)

# SYNCHRONIZATION
## Q8 : What is a race condition? Explain with example. 🔥
1. Analogy
-- 👉 Soch tere paas ek bank account 💰 hai (balance = ₹1000)
-- Do log ek hi time pe paise nikal rahe hain:
    - Person A withdraw ₹500
    - Person B withdraw ₹500
-- 👉 Expected final balance = ₹0
-- ❌ Problem kya hua?
-- Dono ne ek hi time pe balance check kiya:
    - A ne dekha → ₹1000
    - B ne bhi dekha → ₹1000
-- Dono ne ₹500 nikaal liya
-- Final balance = ₹500 ya inconsistent 😨
-- Yeh hi race condition hai
-- Multiple threads race kar rahe hain same data ko access karne ke liye

2. Technical Explnation
-- Jab multiple threads same shared resource ko simultaneously access/modify karte hain
-- aur result depend karta hai execution order/timing pe → usse race condition kehte hain

3. Key Points
-- shared resource (variable , object , memory)
-- Concurrent access 
-- No synchronization
-- Unpredictable output

4. Important Interview Points
-- Race condition occurs when multiple threads access shared data concurrently and the final result depends on the timing of execution.
-- Kab hota hai 
    - Shared variable update
    - Increment/Decrement
    - Collection modification
-- Kaise avoid kare ?
    - use Lock , Monitor , Mutex ,Interlocked

5. Summary 
-- 👉 Race condition tab hoti hai jab:
    - Multiple threads same data access karte hain
    - Without synchronization
-- Result unpredicatable hota hai
-- Solution : lock , Interlocked , Monitor , Mutex


## Q9 : What is a critical section in multithreading?
1. Analogy
-- 👉 Soch ek ATM machine 🏧 hai
    - Ek time pe sirf 1 banda use kar sakta hai
    - Agar 2 log ek saath ghus gaye → system crash
-- ATM ka wo part jahan transaction hota hai
-- Critical Section Hai.
-- Rule : Ek time pe sirf 1 thread allowed

2. Techincal
-- Code ka wo part jahan shared resource access hota hai
-- aur jise ek time pe sirf ek thread execute kare → usse critical section kehte hain

3. Why Important
-- Kyunki yahin pe race condition hoti hai
-- Example : counter++; // shared variable
-- Yeh line hi critical section hai
-- Kaise Protect Kare ?
    - lock
    - Monitor
    - Mutex
    - Semaphores

4. Important
-- Critical section is the part of code that accesses shared resources and must be executed by only one thread at a time  
-- Har shared variable access = potential critical section
-- Critical section chhota rakhna chahiye
-- warna performance slow ho jata hai

5. Golder Rule
-- Minimize the critical section
-- Agar protect nahi kiya : Race Condition
-- Over-protection : Deadlock / performance issues

6. Code
❌ Without Critical Section Protection
    Counter++; // unsafe
✅ With Critical Section (lock)
    static object lockObj = new object();

    lock (lockObj)
    {
        counter++; // critical section protected ✅
    }   

7. Summary
-- Critical section = code jo shared resource access karta hai
-- Ek time pe sirf 1 thread execute kare
-- Race condition avoid karne ke liye use hota hai
-- Protect using:
    - Lock
    - Monitor
    - Mutex
-- Critical Section ko small rakhna important hai.

## Q10 : How does the lock keyword work internally in C#? 🔥
1. Analogy
-- 👉 Soch ek meeting room 🚪 hai
    - Door pe lock laga hai
    - Jo pehle aaya -> andar gaya
    - Baaki sab bahar wait karenge
-- 👉 Jab wo banda bahar aayega → next banda andar
-- Same : 👉 lock = ek time pe sirf 1 thread ko entry

2. Techincal
-- lock internally kya karta hai ?
    - 👉 C# ka lock keyword actually use karta hai:
    - Monitor class internally

3. Code
    lock(obj)
    {
        // critical section
    }
    -- Internally Convert Hua
    Monitor.Enter(obj);
    try
    {
        // critical section
    }
    finally
    {
        Monitor.Exit(obj);
    }
4. Flow samajh
-- Thread Monitor.enter(obj) call karta hai.
-- check Karta hai : 
    - Kya koi aur thread lock hold kar raha hai?
    - ❌ Haan → wait
    - ✅ Nahi → lock acquire
-- Thread code execute karta hai
-- Monitor.Exit(obj) → lock release

5. Important Concept: Mutual Exclusion
-- Sirf ek thread ek time pe lock le sakta hai
-- Baaki sab block ho jaate hain

6. Important Interview Points
-- Lock is syntactic sugar over Monitor.Enter and Monitor.Exit, Ensuring mutual exclusion.
-- Lock Object : reference type hona chahiye
    lock(myObject)
-- Lock ka behaviour:
    - Blocking mechanism
    - FIFO guarantee nahi hota
-- Reentrancy
    - Same thread dobara lock le sakta hai:
    lock(obj)
    {
        lock(obj)
        {
            // allowed ✅
        }
    }
-- Best Practice : private static readonly object lockObj = new object();

7. Code
✅ Proper Lock Usage
    using System;
    using System.Threading;

    class Program
    {
        static int counter = 0;
        static object lockObj = new object();

        static void Increment()
        {
            for (int i = 0; i < 100000; i++)
            {
                lock (lockObj)
                {
                    counter++;
                }
            }
        }

        static void Main()
        {
            Thread t1 = new Thread(Increment);
            Thread t2 = new Thread(Increment);

            t1.Start();
            t2.Start();

            t1.Join();
            t2.Join();

            Console.WriteLine(counter);
        }
    }
⚡ Advanced (Manual Monitor)
    bool lockTaken = false;

    try
    {
        Monitor.Enter(lockObj, ref lockTaken);
        // critical section
    }
    finally
    {
        if (lockTaken)
            Monitor.Exit(lockObj);
    }

8. Summary
-- lock internally uses Monitor
-- Convert hota hai → Enter + Exit
-- Ensure : 
    - Mutual exclusion
    - Thread safety
-- Feature
    - Blocking
    - Reentrant
-- Best Practice : Private lock object use karo

## Q11 : What is the difference between lock and Monitor? 🔥
1. Analogy
-- Soch tu ek room booking system 🏢 manage kar raha hai
-- lock (simple System)
    - Bas ek rule : Ek time pe ek hi banda andar ja sakta hai
    - Easy To Use
    - Control Kam
-- Monitor (Advance System)
    - Tum Bol Skta hai : Wait Karo , Signal Do , Timeout Lagao.
    - Full control
    - Thoda Complex

2. Technical
-- lock
    - C# keyword hai
    - Internally use karta hai Monitor
    - Automatically handle karta hai: Entry , Exit , Exception Safety
-- Monitor
    - .NET class (System.Threading)
    - Manual control deta hai : 
        - Enter()
        - Exit()
        - Wait()
        - Pulse() / PulseAll()

3. Difference
| Feature          | lock            | Monitor            |
| ---------------- | --------------- | ------------------ |
| Type             | Keyword         | Class              |
| Ease of Use      | Easy            | Complex            |
| Control          | Limited         | Full control       |
| Wait/Pulse       | ❌ Not available | ✅ Available        |
| Exception Safety | Automatic       | Manual             |
| Use Case         | Simple locking  | Advanced scenarios |

4. Important
-- Most Important Line'
    "lock is syntactic sugar over Monitor, but Monitor provides more control like wait and pulse mechanisms."
-- lock internally
    Monitor.Enter(obj);
    try { }
    finally { Monitor.Exit(obj); }
-- Monitor.Wait()
    - Thread ko temporarily release kar deta hai lock
    - Wait karta hai signal k
-- Monitor.Pulse()
    - Waiting thread ko signal deta hai
-- Monitor.Exit Bhool gaye 
    - Deadlock
-- Producer - Consumer Problem -> Monitor use hota hai.

5. Summary
-- lock
    - Simple Syntax
    - Automatically handles locking
    - Internally uses Monitor
-- Monitor
    - More powerful
    - Gives fine-grained control
    - Supports Wait/Pulse
-- Use :
    - lock → 90% cases
    - Monitor → advanced scenarios

## Q12 : What is a deadlock? Give a real code example. 🔥
1. Analogy
-- Soch 2 log hain :
    - Person A ke paas Pen 🖊️ hai
    - Person B ke paas Notebook 📓 hai
-- Ab : 
    - A bolta hai: mujhe notebook chahiye
    - B bolta hai: mujhe pen chahiye
-- Dono ek dusre ka wait kar rahe hain
-- Koi bhi release nahi kar raha
-- Result : DeadLock

2. Technical
-- Deadlock kya hai?
"Jab 2 ya zyada threads ek dusre ka resource hold karke wait karte hain
aur koi bhi aage nahi badh pata → usse deadlock kehte hain"

3. Important Interview Points
-- Deadlock occurs when two or more threads are waiting for each other to release resources, causing indefinite blocking.
-- Common cause : Multiple locks wrong order me lena
-- Always acquire locks in same order

4. Algorithm
-- Step 1 : Initialize two resources R1 and R2
-- Step 2 : Start two threads T1 and T2
-- Step 3 : T1 acquires R1 and waits for R2
-- Step 4 : T2 acquires R2 and waits for R1
-- Step 5 : Both threads wait indefinitely
-- Step 6 : Deadlock occurs

5. Summary
-- Deadlock = threads ek dusre ka wait karte rehte hain indefinitely
    
## Q13 : What are the four conditions required for deadlock?🔥
1. Analogy
-- Soch 2 log : 
    - A ke paas 🖊️ Pen
    - B ke paas 📓 Notebook
-- Ab : 
    - A → Notebook ka wait kar raha
    - B → Pen ka wait kar raha
-- Dono ke paas already kuch hai + dusra chahiye
-- Koi bhi chhod nahi raha
-- Yeh situation tabhi possible hai jab 4 conditions satisfy hoti hain

2. Techincal 
-- Deadlock hone ke liye 4 necessary conditions hoti hain (Coffman Conditions):
-- Mutual Exclusion
    - 👉 Resource ek time pe sirf 1 thread use kar sakta hai
    - Example: Lock, file, DB connection
    - Agar resource shareable hota → deadlock nahi hota
-- Hold and Wait
    - Thread ek resource hold karke dusra wait karta hai
    - Example : T1 ke paas R1 hai, aur R2 ka wait kar raha hai
-- No Preemption
    - Resource forcibly cheena nahi ja sakta
    - Example : Lock jab tak thread release na kare → kisi aur ko nahi milega
-- Circular Wait (MOST IMPORTANT 🔥)
    - Threads circular chain me wait kar rahe hote hain
    - Example :
        - T1 -> R2 ka Wait
        - T2 -> R1 Ka Wait
    - Cycle ban gaya

3. Important
-- All four conditions must hold simultaneously for a deadlock to occur.
-- Agar ek bhi condition break ho gayi → deadlock impossible
-- Circular wait tod do (lock order fix)

4. Algorithm
-- Step 1 : Identify all threads (T1, T2, …)
-- Step 2 : Identify resources (R1, R2, …)
-- Step 3 : Check
    a. Kya resource exclusive hai? (Mutual Exclusion)
    b. Kya thread resource hold karke wait kar raha hai? (Hold & Wait)
    c. Kya resource forcibly release nahi ho sakta? (No Preemption)
    d. Kya circular dependency hai? (Circular Wait)
-- If All TRUE -> Deadlock Possible.

5. Visulization
T1 ---> R1
 |       |
 |       ↓
 R2 <--- T2
-- Breakdown:
    - T1 holds R1, wants R2
    - T2 holds R2, wants R1
-- Circular loop → 💥 Deadlock

6. Interview Traps + Answers
-- Can deadlock occur if one condition is missing? 
    No
-- Which condition is easiest to break?
    Circular Wait (by ordering locks)
-- Which is most dangerous ?
    Circular Wait (root cause in most cases)

7. Summary
-- Deadlock ke liye 4 conditions 
    - Mutual Exclusion
    - Hold and Wait
    - No Preemption
    - Circular Wait
-- Sabhi conditions ek saath hone chahiye
-- Circular wait tod do → deadlock avoid

## Q14 : How can you prevent deadlock in C#? 🔥
1. Lock Ordering follow Karo
2. Timeout use Karo
3. Minimize Locks
4. Aquire Lock in Same Order

## Q15 : What is thread starvation?
1. Analogy
-- Soch ek canteen 🍛 me line lagi hai
-- VIP log baar-baar aake line me ghus rahe hain
-- Normal log wait karte hi reh jaate hain
-- Normal log kabhi serve hi nahi ho paate
-- Yeh hi Thread Starvation hai
-- Resource available hai, par kuch threads ko mil hi nahi raha

2. Technical Explanation
-- Thread Starvation kya hai?
    - Jab kuch threads CPU ya resource ke liye indefinitely wait karte rehte hain,
    - kyunki dusre threads baar-baar priority ya scheduling ke basis pe resource le lete hain
-- Key Difference
    - Deadlock → sab threads stuck
    - Starvation → kuch threads chal rahe, kuch bhooke

3. Important
-- Thread starvation occurs when a thread is unable to get CPU time or resources for a long time due to unfair scheduling.
-- Reasons:
    - High priority threads dominate
    - Unfair locks
    - Improper scheduling
-- Common Scenario
    - lock me ek thread baar-baar enter ho raha hai
    - Dusre threads ko chance hi nahi mil raha

4. Solution
-- Fair scheduling
-- Reduce lock contention
-- Use concurrent Collections
-- Avoid long critical sections

5. Algorithm (Blueprint ✍️)
-- Step 1 : Initialize multiple threads (T1, T2, T3…)
-- Step 2 : Assign priorities (some high, some low)
-- Step 3 : Start execution
-- Step 4 : Scheduler Selects 
                - High priority thread first
-- Step 5 : High priority thread:
                - Acquires resource
                - Completes work
                - Again gets CPU (due to priority)
-- Step 6 : Low priority threads
                - Keep Waiting
-- Step 7 : Repeat steps 4-6
-- Result : 
    - Some Threads never Execute
    - thread Stravation Occurs

6. Visualization
CPU Scheduler
     |
     ↓
   [T1 - High Priority] ---> Running ---> Running ---> Running
     |
     ↓
   [T2 - Low Priority] ---> Waiting 😓
   [T3 - Low Priority] ---> Waiting 😓
-- 👉 T1 baar-baar run kar raha
-- 👉 T2, T3 ko chance hi nahi mil raha

7. Interview Traps + Answers
-- Is starvation same as deadlock?
    No
-- Can starvation happen without deadlock?
    Yes
-- Can Starvation be Resolved automatically
    Not Always

8. Summary
-- Thread starvation = kuch threads ko resource nahi milta
-- Reason = unfair scheduling / priority
-- Difference 
    - Deadlock = sab struck
    - Starvation = Kush hi stuck
-- Solution 
    - Fair Scheduling
    - Reduce lock usage

## Q16 : What is livelock and how is it different from deadlock?
1. Analogy
-- 👉 Soch 2 log narrow corridor me aa gaye:
-- Deadlock
    - Dono ruk gaye
    - Ek dusre ka wait kar rahe
    - Koi move nahi kar raha
-- Livelock 
    - Dono polite hain
    - A side hota hai -> B Side hota hai
    - Fir A Dusri Side -> Same B bhi
    - Dono move kar rahe hain
    - But aage badh nahi rahe
-- Key : 
    - DeadLock : No Movement
    - LiveLock : Movement hai but no Progress

2. Technical Explanation
-- Jab threads continuously state change karte rehte hain (retry / release / re-acquire),
-- but actual work complete nahi hota → usse livelock kehte hain

3. Deadlock vs Livelock
| Feature   | Deadlock      | Livelock                  |
| --------- | ------------- | ------------------------- |
| State     | Blocked       | Active                    |
| Movement  | ❌ No          | ✅ Yes                     |
| Progress  | ❌ No          | ❌ No                      |
| CPU Usage | Low           | High                      |
| Cause     | Circular wait | Over-coordination / retry |

4. Important
-- In deadlock, threads are blocked and waiting, while in livelock, threads keep changing state but still make no progress.
-- Livelock Me : 
    - Threads release locks voluntarily
    - Fir dobara try karte hain
-- Common Cause :
    - Over smart retry logic
    - Too much synchronization
-- Solution
    - Random delay (backoff strategy)
    - Limit retries

5. Interview Traps
-- Which is harder to detect?
    ✅ Livelock (kyunki threads active lagte hain)
-- CPU usage kis me zyada hota hai?
    ✅ Livelock
-- Can livelock become deadlock?
    ❌ Not directly, but both are failure states

6. Summary
-- Livelock
    - Threads active hota hain
    - But PRogress nahi hoti 
-- Deadlock 
    - Threads blocked hota haoin
-- Fix :    
    - Backoff Strategy
    - Reduce retries.

# ADVANCED SYNCHRONIZATION
## Q17 : What is the difference between Mutex and Semaphore?🔥

## Q18 : When should you use SemaphoreSlim instead of Semaphore?

## Q19 : What is ReaderWriterLockSlim and when would you use it? 🔥

## Q20 : What is AutoResetEvent vs ManualResetEvent?

## Q21 : What is the volatile keyword and when should it be used? 🔥

## Q22 : How does the Interlocked class ensure thread safety? 🔥