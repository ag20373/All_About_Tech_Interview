# Part 1 - Stack, Heap, Boxing, Unboxing, Array, ArrayList, Generics, Threading
## Q1 :- Explain difference between .NET and C# ?
1. Simple Analogy
-- Restaurant ki example lo:
    - C# = Chef (jo khana banata hai — yaani code likhta hai)
    - .NET = Kitchen + Equipment + Infrastructure (jisme chef kaam karta hai)
-- To The Pint :
    - C# Programming Language Code likhne ke liye
    - .NET Platform / Framework , Code run karne ke liye

2. Real Life mein:
-- Tum C# mein code likhte ho
-- .NET usse execute karta hai, memory manage karta hai, files handle karta hai

3. Key Point : 
-- C# sirf ek language hai
-- .NET mein bahut kuch hai — libraries, runtime, tools — aur C# ke alawa VB.NET, F# bhi chal sakte hain isme!

## Q2 :- .NET Framework vs .NET Core vs .NET 5.0
1. Analogy se Samjho:
-- Ghar ki example lo:
    - .NET Framework = Purana ghar — sirf Windows mein rehta hai, comfortable hai but limited
    - .NET Core = Naya portable tent — kahin bhi laga lo, Windows, Mac, Linux
    - .NET 5/6/7/8 = Modern Smart Home — tent aur ghar dono ka best combination!
-- Simple Table
    - .NETFramework
        - 2002 pe Aya
        - Sirf Windows ka Liya
        - Slow Speed
        - Future pe Discontinue Ho skta ha
        - Used : Legacy Only
    - .NET Core
        - 2016
        - Cross Platform And Open Source
        - Fast Speed 
        - Merge Ho gaya
        - Used Old Projects
    - .NET 5+
        - 2020
        - Cross PlatForm And Open Source
        - Faster
        - Future yahi ha
        - Haan, ab yehi use kro

2. Real Life Example
-- Purani government ya bank software — abhi bhi .NET Framework pe hai
-- Nayi company start karo — .NET 8 use karo directly
-- .NET Core tha bridge — Framework se .NET 5+ tak jaane ka raasta

3. Key Point :
" Microsoft ne .NET Core + .NET Framework dono ko merge karke
ek unified cheez banayi — ".NET 5" aur uske baad .NET 6, 7, 8...
Ab sirf version number badhta hai, naam nahi! 😄 "

4. Interviewer ko Bolna ho Toh :
Sir, .NET Framework sirf Windows pe chalta tha, legacy system hai. .NET Core cross-platform tha aur fast tha. Microsoft ne dono ko combine karke .NET 5 banaya — jo ab unified platform hai. Nayi projects ke liye hum .NET 8 use karte hain

## Q3 :- What is IL ( Intermediate Language) Code ?
1. Analogy
-- UN Meeting ki tarah socho:
    - Indian delegate Hindi mein bola → (C# Code)
    - Translator ne Universal English mein convert kiya → (IL Code)
    - Phir har desh ne apni language mein suna → (Machine Code — Windows/Mac/Linux)
-- Techincal 
    "C# Code -> [C# Compiler] -> IL Code -> [JIT Complier] -> MAchine Code -> Run!"
    - Tum C# mein code likhte ho
    - dotnet build karte ho toh Compiler C# ko IL mein convert karta hai
    - Ye IL code .dll ya .exe file mein save hota hai
    - Jab program run hota hai, tab CLR ka JIT Compiler IL ko us machine ke liye machine code mein convert karta hai
    - Isliye same IL code — Windows pe bhi chala, Linux pe bhi chala ✅

2. Key Point 
-- Full Form : Intermediate Language
-- Dusra Naam : MSIL ya CIL bhi bolte hain
-- File : .dll ya .exe mein hota hai
-- Faida : Ek hi IL Code - KAhin Bhi Chalo!
-- IL Code = Beech ki language jo C# aur Machine ke beech mein hoti hai! 

3. IL Code Dikhta Kaisa Hai?
-- C# Code  : int a = 5 + 3;
-- IL Code banate hai Kush Aise
    ldc.i4.5       // 5 load karo
    ldc.i4.3       // 3 load karo
    add            // dono add karo
    stloc.0        // result store karo
    > ❗ IL code **human readable** hota hai lekin **directly CPU nahi samajhta** — JIT ka kaam hai isse machine code mein todna

3. CLR , JIT , IL - Teeno Ka Connection
-- CLR  →  Overall Manager hai (Memory, Security, Execution sab handle karta hai)
-- JIT  →  CLR ka part hai jo IL ko Machine Code mein badalta hai
-- IL  →  JIT ka input hai

4. Interview
"Sir, jab hum C# code compile karte hain, toh directly machine code nahi banta — pehle IL (Intermediate Language) banta hai, jise MSIL ya CIL bhi kehte hain. Ye IL .dll ya .exe mein store hota hai. Runtime pe CLR ka JIT Compiler is IL ko current machine ke liye machine code mein convert karta hai. Iska sabse bada faida hai platform independence — same IL Windows, Linux, Mac sab pe chal sakta hai."

## Q4 :- What is the use of JIT ( Just in time compiler) ?
1. Techincal
-- JIT Karta Kya Hai Exactly:
    - IL Code platform independent hota hai — CPU seedha nahi samajhta
    - JIT runtime pe IL ko machine specific code mein convert karta hai
    - JIT smart hai — jo method pehle call hua, usi ko pehle compile karta hai
    - Baar baar same method call ho toh JIT cache kar leta hai — dobara compile nahi karta

2. Diagram
    Program Run Karo
        ↓
    CLR IL Code ko Dekha
        ↓
    JIT ne IL Code liya
        ↓
    Current Machine ke liye Machine Code Banaya
        ↓
    CPU ne Execute Kiya ✅

3. JIT ka Caching
-- 1st Time Method Call  →  JIT compile karta hai  →  Cache mein save
-- 2nd Time Same Method  →  Cache se directly use  →  Fast! ⚡

4. JIT ke Types — Bonus Point!
-- Normal JIT : Method tab compile karo jab call ho
-- Pre JIT : Sab kuch ek saath pehle compile karo
-- Econo JIT : Limited memory ke liye — cache nahi karta

5. JIT vs AOT - Quick Difference
-- Jit Runtime pe Compile Kra ga , AOT  Pehle se
-- Jit ka start up thoda slow , AOT ka Fast
-- jit .NET Default , AOT .NET Native / Blozor WASM

6. Key Points
-- Full Form : Just In Time Compiler
-- Kaam : IL-> Machine Code
-- Kahan Retha Hai : CLR ke Andar
-- Smart Feature : Compiled Code Cache karta hai
-- Faida : Platform Specific ptimization + Speed

7. Interview : 
"Sir, JIT yaani Just In Time Compiler — CLR ka ek part hai jo runtime pe IL Code ko machine specific code mein convert karta hai. Ye tab kaam karta hai jab method pehli baar call hoti hai, aur compiled code ko cache kar leta hai taaki dobara same method fast chale. Iska faida ye hai ki code platform ke according optimized hota hai aur performance better rehti hai."

## Q5 :- Is it possible to view IL code ?
1. Short Answer
-- IL Code dekha ja sakta hai — iske liye ek tool hota hai called ILDASM ya modern tools like ILSpy / dotPeek

2. Tools jo Use Hote Hain:
-- ILDASM : Microsift ka offical tool - .exe / .dll ka IL dikhata hai
-- ILSpy : Free open source tool - IL + C# dono mein dekhne do
-- dotPeek : JetBrains ka tool - Professional decompiler
-- Linqpad : Quick testing tool - IL output dekh sako

3. ILDASM Kaise Use Karo:
-- Step 1 : Pehle apna code build karo
    dotnet build
-- Step 2 : ILDASM run karo (Visual Studio Developer Command Prompt mein)
    ildasm YouApp.dll
"Ek GUI window khulegi jisme tumhara poora IL code dikhega!"

4. Practical Use Kab Hota Hai Ye?
-- Debugging : Samajhna ki compiler ne kya generate kiya
-- Security : Dekhna ki koi sensitive info toh nahi hai compiled code mein
-- Performance : Check karna ki code optimized hai ya nahi

5. Important
-- IL Code reversible hota hai — matlab koi bhi tumhari .dll file se original C# code wapas nikaal sakta hai! 
-- sliye production apps mein Obfuscation use karte hain (Code ko deliberately confusing bana dete hain)

6. Interview
"Sir, haan IL code dekha ja sakta hai — ILDASM jo Microsoft ka official tool hai ya ILSpy jaise third party tools se. Ye tools .dll ya .exe file ka IL code show karte hain. Ek important point ye hai ki IL code reversible hota hai, matlab original C# code bhi recover ho sakta hai — isliye production mein obfuscation use karte hain code ko protect karne ke liye."


## Q6 :- What is the benefit of compiling in to IL code ?
1. Platform Independence
-- Real Example: Tumne ek .NET App banai Windows pe , Same .dll file Linux aur Mac pe bhi chalegi , Kyunki IL ek neutral language hai — platform specific nahi!
    Same IL Code
    ├── Windows JIT  →  Windows Machine Code  ✅
    ├── Linux JIT    →  Linux Machine Code    ✅
    └── Mac JIT      →  Mac Machine Code      ✅

2. Language Independence
-- Restaurant Example: 3 alag chefs hain — ek Hindi mein recipe likhta hai, ek Urdu mein, ek English mein , Teeno ki recipe ek universal format mein convert hoti hai , Kitchen (CLR) sabki recipe banata hai bina kisi problem ke!
    C#   ──┐
    VB.NET ─┼──→  Same IL Code  →  CLR  →  Run ✅
    F#   ──┘
-- Matlab alag alag languages ek saath kaam kar sakti hain Ek C# class, VB.NET project mein use ho sakti hai!

3. JIT Optimization 
-- IL seedha machine code nahi hai — JIT runtime pe optimize karta hai JIT ko pata hota hai exact CPU kaun sa hai machine mein Toh us CPU ke liye best possible code generate karta hai
    IL Code  →  JIT  →  "Ye Intel i9 CPU hai"  →  i9 Optimized Code ⚡
    IL Code  →  JIT  →  "Ye ARM CPU hai"       →  ARM Optimized Code ⚡

4. Code Verification & Security
-- IL run hone se pehle CLR verify karta hai:
    - Koi illegal memory access toh nahi?
    - Koi type mismatch toh nahi?
    - Code safe hai ya nahi?

- Short Remember
-- ✅ Platform Independence : Windows, Linux, Mac — sab pe chalo
-- ✅ Language Independence : C#, VB, F# — sab ek saath
-- ✅ JIT Optimization : Runtime pe CPU specific best code
-- ✅ Interoperability : Alag languages ke code ek saath kaam kare

## Q7 :- Does .NET support multiple programming languages ?
-> VB.NET , C# , F# And More

## Q8 :- What is CLR ( Common Language Runtime) ?
1. Analogy se Samjho:
-- Factory Manager Example:
    - Tum worker ho (C# Code)
    - Factory Manager (CLR) sab kuch handle karta hai
        - Tumhe kaam deta hai (Code Execute karta hai)
        - Salary deta hai (Memory Allocate karta hai)
        - Kaam khatam hone pe cleanup karta hai (Garbage Collection)
        - Security check karta hai (Verification)
        - Koi error aaye toh handle karta hai (Exception Handling)

2. Techincal 
Tumhara C# Code
      ↓
  IL Code bana
      ↓
  CLR ne liya
      ↓
  ┌─────────────────────────┐
  │          CLR             │
  │  ┌─────────────────┐    │
  │  │   JIT Compiler  │    │  ← IL ko Machine Code banaya
  │  ├─────────────────┤    │
  │  │Garbage Collector│    │  ← Memory cleanup kiya
  │  ├─────────────────┤    │
  │  │ Type Safety     │    │  ← Code verify kiya
  │  ├─────────────────┤    │
  │  │Exception Handler│    │  ← Errors handle kiye
  │  └─────────────────┘    │
  └─────────────────────────┘
      ↓
  Program Run ✅

3. CLR Kya Kya Karta Hai 
-- JIT Compilation : IL Code ko runtime pe machine code mein convert karta hai Ye hum already padh chuke hain! ✅
-- Memory Management & Garbage Collection : Tumne khana banaya — bartan gande hue , CLR ka GC (Garbage Collector) automatically bartan saaf karta hai , Tumhe manually delete/free nahi karna memory!
-- Type Safety : CLR check karta hai ki galat type ka data toh assign nahi ho raha
-- Exception Handling :  Delivery Example: Order diya — address galat tha — delivery fail , CLR error ko gracefully handle karta hai — program crash nahi hota!
--  Code Verification & Security
    - Program execute hone se pehle CLR verify karta hai:
        * Code safe hai?
        * Unauthorized memory toh access nahi kar raha?
        * Permissions sahi hain?
-- Thread Management : Ek saath kai customers ke orders handle karna = Multithreading , CLR threads ko manage karta hai — sab smoothly chale!

4. Table
-> JIT Compiler : IL → Machine Code
-> Garbage Collector : Automatic Memory Cleanup
-> Type Checker : Type Safety Ensure karna
-> Exception Manager : Errors Handle karna
-> Thread Manager : Multithreading Handle karna
-> Security Manager : Code Permissions Check karna

5. One Line 
CLR = .NET ka Engine — jo tumhara code leta hai, verify karta hai, run karta hai, memory sambhalta hai — sab kuch! 

4. Interviewer ko Bolna Ho Toh:
"Sir, CLR yaani Common Language Runtime — ye .NET ka core engine hai jo humara code actually execute karta hai. Iske andar JIT Compiler hota hai jo IL ko machine code mein convert karta hai. Garbage Collector memory automatically manage karta hai. Type safety, exception handling, thread management aur security verification bhi CLR hi handle karta hai. .NET Core mein ise CoreCLR kehte hain lekin kaam same rehta hai."

## Q9 :- What is managed and unmanaged code ?
1. Analogy
-- PG (Paying Guest) vs Apna Ghar Example :
    - Managed Code = PG mein rehna
        - Owner(CLR) sab kush handle karta hai
        - Bijli, paani, safai — tumhari chinta nahi
        - Bas apna kaam karo!
    - Unmanaged Code = Apna Ghar
        - Sab khud karo — bijli bill, safai, repair
        - Zyada control hai tumhare haath mein
        - Lekin zyada zimmedari bhi hai!

2. Techincal 
Managed Code                    Unmanaged Code
─────────────────               ─────────────────
C# / VB.NET / F#                C / C++
      ↓                               ↓
   IL Code                      Direct Machine Code
      ↓                               ↓
CLR handle karta hai            Developer khud handle kare
(Memory, Security,              (Memory, Pointers,
 Exceptions sab)                 Cleanup sab kuch)

3.  Managed Code Kya Hai:
-- Jo code CLR ki supervision mein chalta hai — use Managed Code kehte hain i.e C#
-- Managed Code ke Fayde:
    - Automatic Memory : GC khud free karta hai.
    - Type Safety : CLR verify karta hai
    - Exception Handling : Errors gracefully handle
    - Security : CLR permissions check karta hai
    - Easy Development : Developer ko memory ki chinta nahi

4. Unmanaged Code Kya Hai : 
-- Jo Code CLR ke bahar chalta hai - directly OS pe - use Unmanaged Code ketha hain
-- Unmanaged Code ke Issues:
    - ❌ Memory Leak : Delete karna bhool gaye toh memory waste
    - ❌ Pointer Errors : Wrong pointer = App crash
    - ❌ No Type Safety : Galat type — runtime pe crash
    - ✅ Fast : CLR overhead nahi — direct execution
    - ✅ Hardware Control : Direct memory/hardware access

5. .NET mein Unmanaged Code kab aata hai?
-- Real Scenario: Tumhari C# app ko purani C++ DLL use karni hai Ya directly Windows OS APIs call karni hain Iske liye .NET mein P/Invoke ya unsafe keyword use karte hain
-- Code :
// C# mein Unmanaged Code call karna
[DllImport("user32.dll")]  // Windows ki C++ DLL
public static extern int MessageBox(int h, string m, string c, int type);
// ⚠️ Ab ye code CLR manage nahi karega!

6. Unsafe Code - Bouns Point
-- C# mein ek special keyword hai — unsafe , Isse tum C# ke andar bhi unmanaged style code likh sakte ho
-- Code :
unsafe void UnsafeExample()
{
    int x = 10;
    int* ptr = &x;  // Pointer use kar rahe hain — CLR manage nahi karega!
    Console.WriteLine(*ptr);
}
--  unsafe code ke liye project settings mein allow unsafe code enable karna hota hai

7. Quick Comapraion
-- Example : C# , F# ---- c,C++
-- Memory : CLR/GC ---- Developer Kudh kr rehe ha
-- Safety : Type Safe ---- Manually ensure karo
-- Speed : Thoda overhead ---- Faster Direct Execution
-- Use Case : Bussiness App , APIs , Web ----Game Engiens , Drives, OS

## Q10 :- Explain the importance of Garbage collector ?
1. Analogy
-- Ghar mein Kaam Waali Bai Example:
-- Tum ghar mein kaam karte ho — khana banaya, bartan gande kiye, kachra faila
-- Tum apne kaam mein busy ho
-- Bai (GC) automatically aati hai
-- ganda bartan saaf kiya, kachra uthaya
-- Tumhe bolna nahi pada — khud samajh ke kiya! ✅
-- ❌ Bai nahi hoti (C++ jaisa) = Tum khud saaf karo — bhool gaye toh -- -- ghar mein kachra bharta jayega (Memory Leak!)

2. Technical Samjho:
Tumhara C# Code objects banata hai
            ↓
     Heap Memory mein store hote hain
            ↓
     Kaam khatam — object unused ho gaya
            ↓
     GC automatically detect karta hai
            ↓
     Memory free kar deta hai ✅
     (Tumhe kuch nahi karna!)

3. Bina GC ke Kya Hota — Real Problem:
-- cpp
    // C++ mein (No GC) ❌
    void TakeLoan()
    {
        int* memory = new int[1000];  // Memory li
        // kaam kiya...
        // delete karna BHOOL GAYE! 💀
        // Ye memory kabhi free nahi hogi = MEMORY LEAK
    }
    // Ye function 1000 baar call hua
    // = 1000x Memory waste = App crash! 💀
.............
-- csharp
    // C# mein (GC hai) ✅
    void TakeLoan()
    {
        int[] memory = new int[1000];  // Memory li
        // kaam kiya...
        // GC khud free kar dega! ✅
    }

4. GC Kaam Kaise Karta Hai - Generations
-- 🗑️ **Colony ka Kachra Example:**
    > - **Naya kachra (Gen 0)** = Aaj ka kachra — roz uthao
    > - **Purana kachra (Gen 1)** = Weekly uthao
    > - **Bahut purana (Gen 2)** = Monthly uthao
-- Memory Heap
├── Generation 0  (Naye Objects)     ← Baar baar collect hota hai ⚡
├── Generation 1  (Thode purane)     ← Kabhi kabhi collect hota hai
└── Generation 2  (Bahut purane)     ← Kam collect hota hai

5. Why GC Important Kyun Hai :
✅ No Memory Leak -- Unused objects automatically free
✅ Developer Productive -- Memory ki chinta nahi — business logic pe focus
✅ App Stability -- Memory full nahi hogi — crash nahi hoga
✅ Automatic -- Tumhe kuch nahi karna — GC khud decide karta hai kab run karna

6. IDisposable 
-- Kuch resources hain jo GC handle nahi karta — jaise:
    - File handles
    - Database connections
    - Network connections
-- Inke liye IDisposable interface aur using block use karte hain
-- Code : 
    // using block — kaam khatam toh automatically dispose! ✅
    using (SqlConnection con = new SqlConnection(connString))
    {
        // DB kaam karo
    }
    // Block khatam = Connection automatically close ✅
    // GC ka wait nahi karna!  


## Q11 :- Can garbage collector claim unmanaged objects ?
1. Short Answer 
-- ❌ Nahi! GC sirf managed objects ki memory free karta hai , Unmanaged resources — GC ki reach se bahar hain!

2. Unmanaged Resources Kaunse Hain:
--> File Handles -- File open karke band nahi ki
--> DB Connections -- SqlConnection open rakha
--> Network Sockets -- HTTP connection open rakha
--> COM Objects -- Windows COM components
--> OS Resources -- Windows handles, mutexes

3. Problem Kya Hoti Hai :
-- Code
    // ❌ BAD CODE — Unmanaged resource leak!
    public void ReadFile()
    {
        FileStream fs = new FileStream("data.txt", FileMode.Open);
    }
-- file padhi...
-- fs.Close() karna BHOOL GAYE!
-- GC FileStream object toh free karega
-- Lekin andar jo OS File Handle hai
-- wo KABHI free nahi hoga! 💀
-- = RESOURCE LEAK!

4. Solution
-- Solution 1 : IDisposable + Dispose()
    public void ReadFile()
    {
        FileStream fs = new FileStream("data.txt", FileMode.Open);
        // kaam karo...
        fs.Dispose(); // ✅ Manually unmanaged resource free kiya!
    }
...........
-- Solution 2 :  using Block (Best Practice!)
    // using block automatically Dispose() call karta hai!
    public void ReadFile()
    {
        using (FileStream fs = new FileStream("data.txt", FileMode.Open))
        {
            // file padho...
        } // ✅ Block khatam = Dispose() automatic call!
    }

    // Modern C# mein aur bhi simple:
    public void ReadFile()
    {
        using FileStream fs = new FileStream("data.txt", FileMode.Open);
        // kaam karo...
    } // ✅ Method khatam = Dispose() automatic!
..............
-- Solution 3 : Finalizer / Destructor (Last Resort)
    public class MyResource
    {
        // Finalizer — GC last mein isko call karta hai
        ~MyResource()
        {
            // Unmanaged resource manually free karo
            // ⚠️ But ye unpredictable hai — kab chalega pata nahi!
        }
    }
    - ❗ Finalizer bad practice hai — sirf last resort mein use karo
    - using block sabse best approach hai! ✅

5. IDisposable Pattern — Proper Way:
-- Code 
    public class DatabaseHelper : IDisposable
    {
        private SqlConnection _connection;
        private bool _disposed = false;

        public DatabaseHelper()
        {
            _connection = new SqlConnection("connection string");
            _connection.Open();
        }

        public void Dispose()
        {
            if (!_disposed)
            {
                _connection.Close();    // ✅ Unmanaged resource free
                _connection.Dispose();
                _disposed = true;
            }
        }
    }

    // Use karo:
    using (var db = new DatabaseHelper())
    {
        // DB kaam karo
    } // ✅ Automatically Dispose() call hoga!


6. Interview
-- GC sirf managed objects ko free karta hai — unmanaged resources jaise file handles, database connections, network sockets ko GC handle nahi karta.
-- Agar hum inhe properly close na karein toh resource leak hota hai.
-- Iske solution ke liye hum IDisposable interface implement karte hain aur using block use karte hain — jo automatically Dispose() call karta hai aur resources free karta hai."

## Q12 :- What is the importance of CTS ?
1. Problem Samjo - Problem Kya Thi :
--  .NET mein alag alag languages hain:
    - C# mein int hota hai
    - VB.NET mein Integer hota hai
    - F# mein int32 hota hai
-- Ye sab same cheez hain — but naam alag! 
-- Toh jab C# ka code VB.NET se baat kare — confusion nahi hogi? 😕

2. CTS Solution Deta Hai : (Common Type System)
-- CTS ke andar har type ka ek official .NET naam hota hai
-- Jise FCL (Framework Class Library) type kehte hain
    C# Code          VB.NET Code        F# Code
    ──────────       ───────────        ────────
    int              Integer            int32
    string           String             string
    bool             Boolean            bool
    ↓                ↓                 ↓
    └────────────────┴─────────────────┘
                        ↓
                CTS Standard
            (System.Int32)
            (System.String)
            (System.Boolean)
                        ↓
                CLR Samjha ✅

3. CTS Important Kyun Hai:
-- ✅ Language Interop : C# aur VB.NET ek saath kaam kar sakte hain
-- ✅ Type Safety : Galat type assign nahi hoga
-- ✅ Consistency : Sab languages mein same types
-- ✅ CLR Samajh Pata Hai : Ek standard hone se CLR sab handle karta hai

4. CTS vs CLS 
-- Full Form : CTS (Common Type System) , CLS (Common Language Specifiaction)
-- Kya Hai : CTS (Sab Types Define Krta Hai) , CLS (Minimum Rules Jo Sab Languages Follow Karein)
-- Scope : CTS (Poora Type System) , CLS (Subset of CTS)

5. Ek Line Mein :
-- CTS = .NET ka Type Standard — jo ensure karta hai ki
-- C#, VB.NET, F# — sab ek hi language mein types samjhein! 

6. Interviewer 
-- CTS yaani Common Type System 
-- ye .NET ka ek standard hai jo define karta hai ki kaunse types exist karte hain aur wo kaise behave karte hain. 
-- Iska sabse bada faida ye hai ki C#, VB.NET, F# — alag alag languages hone ke bawajood ek doosre ke saath kaam kar sakti hain kyunki sab CTS follow karti hain
-- CTS mein do main categories hain 
    - Value Types jo stack pe store hote hain
    - Reference Types jo heap pe
-- CLS iska SubSet ha hai jo minimum rules define karta hai.

## Q13 :- Explain CLS ?
1. Pehle Problem Samjho :
-- .NET mein bahut saari languages hain:
    - C# — case sensitive hai (myVar aur MyVar alag hain)
    - VB.NET — case insensitive hai (myVar aur MyVar same hain)
    - F# — apne alag rules hain
-- Agar C# ne koi aisi cheez banai jo VB.NET samajh hi nahi sakta — toh interoperability khatam! 😕

2. CLS Solution Deta Hai:
-- Example: 
    - Alag alag ghar ke bacche school aate hain
    - Har ghar ke apne rules hain But school ne minimum rules banaye
        * uniform pehno
        * time pe aao
    - Sab ko ye follow karna hai — chahe ghar mein kuch bhi ho!
-- So , CLS = .NET ka Minimum Common Rules Set!
-- Techincal Samjo
    .NET Languages
    ──────────────
    C#          → Bahut saari features hain
    VB.NET      → Kuch alag features hain
    F#          → Apne unique features hain
        ↓
    ┌─────────────────────────────┐
    │           CTS               │  ← Sab possible types
    │   ┌─────────────────────┐   │
    │   │        CLS          │   │  ← Minimum common rules
    │   │  (Subset of CTS)    │   │
    │   └─────────────────────┘   │
    └─────────────────────────────┘
        ↓
    Jo CLS follow kare — sab languages use kar sakti hain ✅    
-- CLS, CTS ka subset hai
-- CTS mein sab kuch hai — CLS mein sirf minimum rules!



3. CLS Rules Kya Hain — Examples:
-- Rule 1 : Case Sensitivity mat use karo Publicly
    // ❌ CLS Compliant NAHI — C# mein chalega VB.NET mein nahi!
    public class MyClass
    {
        public int myValue = 10;   // alag naam
        public int MyValue = 20;   // sirf case alag — VB.NET confused! 😕
    }

    // ✅ CLS Compliant — sab samjhenge!
    public class MyClass
    {
        public int firstName = 10;   // properly alag naam
        public int lastName = 20;    // no case confusion ✅
    }
.............
-- Rule 2️ — Unsigned Types Public mat karo
    // ❌ CLS Compliant NAHI
    public uint GetAge()    // uint — VB.NET support nahi karta!
    {
        return 25;
    }

    // ✅ CLS Compliant
    public int GetAge()     // int — sab languages samjhengi! ✅
    {
        return 25;
    }
..............
-- Rule 3  — Method Names Meaningful Hon
    // ✅ CLS Compliant — sab languages mein kaam karega
    public class Calculator
    {
        public int Add(int a, int b)      // ✅ Clear name
        {
            return a + b;
        }
    }


4. CLSCompliant Attribute — Bonus Point:
-- C# mein ek attribute hai jisse tum apna code CLS check kara sakte ho!
    // Assembly level pe lagao — poora code check hoga
    [assembly: CLSCompliant(true)]
    public class MyClass
    {
        // ❌ Ye CLS violation hai — compiler warning dega!
        public uint BadMethod() { return 1; }

        // ✅ Ye sahi hai
        public int GoodMethod() { return 1; }
    }
-- [CLSCompliant(true)] lagane ke baad , Compiler khud batayega kahan rules toot rahe hain!

5. CLS Important Kyun Hai 
✅ Interoperability : C# library — VB.NET bhi use kar sake
✅ Consistency : Sab languages mein predictable behavior
✅ Library Developers : NuGet packages — sab ke liye kaam karein
✅ Team Work : Alag language use karne waale bhi collaborate kar sakein

6. CTS vs CLS vs CLR 
-- CTS (Common Type System)
    - Type System
    - Types define karta hai
    - Example : System.Int32 define kiya
    - Sab Types
-- CLS (Common Language Specification)
    - Minimum Rules
    - Interop rules
    - uint public mat karo
    - CTS ka Subset 
-- CLR (Common Language RunTime)
    - Runtime Engine
    - Code execute karta hai
    - JIT, GC, Memory
    - Execution environment

7. Interviewer
-- CLS yaani Common Language Specification
-- ye CTS ka ek subset hai jo minimum rules define karta hai jo sab .NET languages ko follow karne chahiye
-- Iska main purpose hai interoperability — agar meri C# library CLS compliant hai toh VB.NET ya koi bhi .NET language use kar sakti hai.

## Q14 :- Difference between Stack vs Heap ?
1. Analogy
-- Resturant Example
-- Stack = Waiter ki Tray
    - Ek ke upar ek plates rakhi hain
    - Upar wali pehle uthegi (Last In First Out)
    - Fast hai — organized hai
    - Limited space hai tray mein
-- Heap = Restaurant ka Store Room
    - Saman jahaan jagah mili — rakh diya
    - Koi fixed order nahi
    - Zyada space hai
    - Thoda slow hai — dhundhna padta hai

2. Techinal 
    ─────────────────────────────────────────
                MEMORY
    ─────────────────────────────────────────

    STACK                    HEAP
    ──────────────          ──────────────
    │  Method C   │          │  Object 3  │
    │  Method B   │          │            │
    │  Method A   │          │  Object 1  │
    │  Main()     │          │  Object 2  │
    ──────────────          ──────────────
    Organized!               Scattered!
    Fast ⚡                   Slower 🐢
    Limited 📦               Large 🏠
    Auto cleanup ✅          GC cleanup 🗑️

3. Stack Kya Hai:
-- Jo Value Types aur Method calls store karta hai
-- Code
    void MyMethod()
    {
        int age = 25;          // Stack pe store ✅
        bool isActive = true;  // Stack pe store ✅
        double price = 99.5;   // Stack pe store ✅

    } // Method khatam = Stack se automatically remove! ✅ 
-- Stack ki Properties:
    - Order : LIFO — Last In First Out
    - Speed : Buhat Fast
    - Size : Limit
    - Cleanup : Automatic - method khatam toh gone
    - Kya Store : Value types, method calls, references

4. Heap Kya Hai:
-- Jo Reference Types / Objects store karta hai
    void MyMethod()
    {
        // Reference (address) Stack pe
        // Actual Object Heap pe ✅
        Person p = new Person();
        string name = "Rahul";
        int[] arr = new int[5];
    }
    // Method khatam — reference gone
    // But Object Heap pe pada hai — GC free karega baad mein
-- Heap Ki Properties
    - Order : Koi order nahi — random
    - Speed : Stack se Slow
    - Size : Large
    - Clean Up : GC karta hai
    - Kya Store : Objects, Reference types, Arrays



5. Dono Ek Saath Kaise Kaam Karte Hain:
-- Codes
    void MyMethod()
    {
        int age = 25;              // age → Stack pe directly ✅

        Person p = new Person();   // p (reference/address) → Stack pe
                                // new Person() object → Heap pe
    }
    ```
    ```
    STACK                        HEAP
    ──────────────               ──────────────
    │ age = 25    │              │            │
    │ p = [1001]──│─────────────→│ Person{}   │
    │             │     address  │ Name=null  │
    ──────────────               ──────────────

6. Interiew
-- Stack aur Heap dono memory ke alag alag regions hain.
-- Stack fast hota hai, limited size ka hota hai aur value types store karta hai - method khatam hone pe automatically cleanup ho jaata hai LIFO order mein.
-- Heap zyada bada hota hai, reference types yaani objects store karta hai aur GC isko manage karta hai. Jab hum new keyword se object banate hain toh actual object Heap pe jaata hai lekin uska reference Stack pe store hota hai."

## Q15 :- What are Value types & Reference types?
1. Concept
-- Analogy
    - Value Type = Photocopy , Tumne document ki photocopy di dost ko   , Dost ne uspe kuch likha — tumhara original safe hai! , Dono ki apni copy — ek doosre se independent!
    - Reference Type = Google Maps Location Share , Tumne dost ko apne ghar ka address share kiya , Dost wahan gaya aur kuch badal diya Tumhara ghar bhi badal gaya! 😮 , Dono same jagah point kar rahe the!
..........
-- Technical Samjho:
    VALUE TYPE                    REFERENCE TYPE
    ──────────────                ──────────────
    int x = 10;                   Person p = new Person();

    STACK                         STACK        HEAP
    ┌─────────┐                   ┌─────────┐  ┌──────────────┐
    │ x = 10  │                   │ p =1001 │──→│ Person Object│
    └─────────┘                   └─────────┘  │ Name = Rahul │
                                                └──────────────┘
    Value directly                Reference(address)    Actual Object
    Stack pe store!               Stack pe              Heap pe



2. Important Points
-- Value Types
    - Directly value store karte hain — Stack pe
    - Value Type — Copy hoti hai: (Original Perserve)
-- Reference Types
    - Address/Reference store karte hain — Object Heap pe
    - Reference Type — Same Object Point Hota Hai:

3. String Special Case
-- String Reference Type hai — but Value Type jaisi behave karti hai!
-- Code : 
    string s1 = "Hello";
    string s2 = s1;    // Same object point kar raha hai

    s2 = "World";      // Naya object bana — s1 safe! ✅

    Console.WriteLine(s1); // "Hello" — same raha!
    Console.WriteLine(s2); // "World"
-- Ye Immutability hai — string badal nahi sakti , Har change pe naya string object banta hai , Isliye value type jaisi lagti hai!

4. Method mein Pass Karo — Difference:
-- // Value Type — Copy pass hoti hai
-- // Reference Type — Address pass hota hai

5. Null — Difference:
-- Value Types Null Nahi Ho skta
-- Reference Type — null ho sakta hai ✅

## Q16 :- Explain boxing and unboxing ?
-- Value Type ko Reference Type mein convert karna = Boxing
-- Reference Type se wapas Value Type = Unboxing
-- Boxing/Unboxing performance cost karta hai — avoid karo!

## Q17 :- What is consequence of boxing and unboxing ?
> Performace Hit
-- Boxing/Unboxing mein **3 costly operations** hote hain:
-- BOXING ke Steps : 
    Step 1 : Heap pe memory allocate karo    ← Costly! 💸
    Step 2 : Value copy karo Stack → Heap    ← Costly! 💸
    Step 3 : Reference return karo           ← Costly! 💸
-- UNBOXING ke Steps :
    Step 1: Heap pe object dhundho          ← Costly! 💸
    Step 2: Type check karo                 ← Costly! 💸
    Step 3: Value copy karo Heap → Stack    ← Costly! 💸

> Some More Consequences
-- Memory Waste
-- Code Complexity
-- GC Pressure
-- Runtime Error

## Q18 :- Explain casting, implicit casting and explicit casting ?
1. Concept
-- Analogy se Samjho:
-- Bartan Example : 
    - Implicit = Choti bottle se badi bottle mein daalo Paani, naturally chala jaayega — koi risk nahi! ✅
    - Explicit - Badi bottle se choti bottle mein daalo ,Paani bahar gir sakta hai — tumhe khud zimmedari leni hogi! ⚠️

2. Implicit Casting - Automatic 
-- Chota type → Bada type — automatically hota hai, koi risk nahi
-- Code : 
    int x = 100;
    long y = x;      // ✅ Automatic! int → long (bada type)
    double d = x;    // ✅ Automatic! int → double

    // Kyon safe hai?
    // int = 4 bytes
    // long = 8 bytes  → Zyada jagah hai — data fit ho jaayega!
    ```
    ```
    int (4 bytes) ──→ long (8 bytes)   ✅ Safe!
    int (4 bytes) ──→ double (8 bytes) ✅ Safe!

3. Explicit Casting — Manual:
-- Bada type → Chota type — manually karna padta hai — data loss ho sakta hai!
-- Code : 
    double d = 9.99;
    int x = (int)d;   // ✅ Explicit cast — manually kiya
                    // ⚠️ But 9.99 → 9 ho gaya! .99 gaya kahan? 💀

    long bigNum = 99999999999;
    int smallNum = (int)bigNum; // ⚠️ Data loss possible!

4. Implicit vs Explicit — Flow:
    IMPLICIT (Safe — Auto):
    ─────────────────────────────────────────────
    byte → short → int → long → float → double
            ↑
        Chota se bada — automatic ✅

    EXPLICIT (Risky — Manual):
    ─────────────────────────────────────────────
    double → float → long → int → short → byte
            ↑
        Bada se chota — manually karo ⚠️

5. String Conversion — Special:
    // int → string
    int x = 42;
    string s = x.ToString();        // ✅ ToString() use karo
    string s2 = Convert.ToString(x); // ✅ Convert class

    // string → int
    string str = "123";
    int num = int.Parse(str);         // ✅ Parse — but exception possible!
    int num2 = Convert.ToInt32(str);  // ✅ Convert
    int num3;
    bool success = int.TryParse(str, out num3); // ✅ SAFEST!

6. Interview
-- Casting ek type ko doosre mein convert karna hai
-- Implicit casting automatic hoti hai jab chota type bade mein jaata hai — safe hoti hai
-- Explicit casting manual hoti hai — bada type chote mein — yahan data loss, overflow ya InvalidCastException ho sakta hai. 
-- Safe casting ke liye hum 'as' aur 'is' operators use karte hain.

## Q19 :- What can happen during explicit casting ?
1. Possiility
    - Data Loss — Silent!
        double price = 99.99;
        int p = (int)price;
    - Overflow — Galat Value!
        long bigNumber = 999999999999;
        int small = (int)bigNumber; // ⚠️ Overflow!
    - InvalidCastException — Crash!
        object obj = "Hello";   // string store hai
        int x = (int)obj;       // ❌ CRASH! String ko int mein cast?
    
2. Safe Way Explicit Casting "as" & "is"
-- 'as'
    // 'as' operator — fail hone pe null deta hai, exception nahi!
    object obj = "Hello";
    string s = obj as string;  // ✅ "Hello" mila
    int? x = obj as int?;      // null — exception nahi! ✅
-- 'is'
    // 'is' operator — pehle check karo phir cast karo
    if (obj is string str)     // ✅ Check + Cast ek saath!
    {
        Console.WriteLine(str.ToUpper()); // Safe! ✅
    }

## Q20 :- Differentiate between Array and ArrayList ?
1. Concept
-- Bus Example
-- Array = Reserved Seating Bus
    - Fixed seats — 40 seat ki bus, 40 hi rahegi
    - Ek type ke passengers — sirf students ya sirf adults
    - Fast boarding — seat number pata hai!
-- ArrayList = General Bus
    - Flexible seats — jagah chahiye toh naye seats add ho jaate hain
    - Mixed passengers — koi bhi chadh sakta hai
    - Thoda slow — pehle check karna padta hai kaun hai

## Q21 :- Whose performance is better array or arraylist ?
1. Simple 
-- Array ALWAYS faster hai ArrayList se!
    - No Boxing
    - Type Safety at Compile Time
    - Fixed Memory — No Resize

2. Why Use ArrayList
-- Jab size pata nahi pehle se
✅ Jab mixed types store karni ho
⚠️ But aaj kal List<T> use karo — ArrayList outdated hai!

## Q22 :- What are generic collections ?
1. Concept
-- Analogy 
    - Socho restaurant ke kitchen mein containers rakhe hain
    ❌ Old Collection (ArrayList)
        - Ek hi container mein sab kuch mix hai -> Spoon , Fork , Knife
        - Jab spoon chahiye ho → search karna padega.
    ✅ Generic Collection
        - Alag containers ban gaye: Spoon Box , Fork Box  , Knife Box
        - Matlab har container ek specific type ka item hi rakhega.
    - Yahi Generic Collection ka concept hai.
...........
-- Technical
    - Generic Collections ka matlab hai:
    - Collection jisme hum pehle hi decide kar dete hain ki kis type ka data store hoga.
    - Example : List<int> numbers = new List<int>();
    - yaha : sirf integer values store hongi

2. Generic Vs Non Generic
|             | Non-Generic | Generic      |
| ----------- | ----------- | ------------ |
| Example     | ArrayList   | List<T>      |
| Data Type   | Mixed       | Fixed type   |
| Error       | Runtime     | Compile time |
| Performance | Slow        | Faster       |

3. Interviewer
-- Generic collections are type-safe collections in .NET where we specify the data type while creating the collection. Because of this the collection can store only that type of data. 
-- It improves type safety and performance compared to non-generic collections like ArrayList.


## Q23 :- What are threads (Multithreading)?
1. Concept
-- Restaurant mein sirf ek chef ho:
    - Pehle roti banayega
    - Phit sabji
    - phor salad
-- Sab kaam line by line hoga → slow
-- Ab 3 chefs ho gaye:
    - Chef 1 -> Roti
    - Chef 2 -> Sabji
    - Chef 3 -> Salad
-- Sab kaam ek saath ho raha hai → fast
-- Yahi Concept MultiThreading hai.

2. Technical
-- Thread program ka smallest execution unit hota hai.
-- Matlab : Thread program ka smallest execution unit hota hai.
-- Example : Ek application
    - File download ho rahi hai
    - UI responsive hai
    - Background mein Loggin ho rahi hai

3. Code
    using System.Threading;

    Thread t1 = new Thread(PrintNumbers);
    t1.Start();

    void PrintNumbers()
    {
        for(int i = 1; i <= 5; i++)
        {
            Console.WriteLine(i);
        }
    }

## Q24 :- How are threads different from TPL ?
1. Concept
-- Thread
    - Restaurant owner khud chef hire karta hai aur manage karta hai.
        - Kaun kaam karega
        - Kab karega
        - Kitne chefs chahiye
    - Sab manual manage karna padta hai.
-- TPL (Task Parallel Library)
    - Ab resturant ne manager rakh liya
    - Owner bas bolta hai: " Ye 3 kaam karwa do "
    - Manager Kudh Decide Kra ga 
        - Kitne chefs use karne hain
        - Kaunsa kaam pehle karna hai
        - Kaunsa baad mein
    - Owner ko thread manage nahi karna padta

2. Technical
-- Thread
    - Low level concept
    - Developer ko thread create aur manage karna padta hai
    - Example : 
        Thread t = new Thread(MyMethod);
        t.Start();
    - Yaha aap direct thread manage kar rahe ho.
-- TPL (Task Parallet Library)
    - High level abstraction
    - Thread Pool Use Karta hai
    - Automatic thread management
    - Example : Task.Run(() => MyMethod());
    - Yaha .NET khud decide karta hai kaunsa thread use karna hai.

3. Difference
|             | Thread         | TPL                  |
| ----------- | -------------- | -------------------- |
| Level       | Low level      | High level           |
| Management  | Manual         | Automatic            |
| Performance | Less optimized | Better (Thread Pool) |
| Use         | Rare now       | Recommended          |


## Q25 :- How do we handle exceptions in C#(try/catch)?
1. Concept 
-- Program mein error aaye toh usko gracefully handle karna.
-- C# mein errors ko handle karne ke liye try / catch use karte hain.

## Q26 :- What is the need of finally?
-- File Close
-- Database Close
-- For Killing/ Closing Task.

## Q27 :- Why do we need the out keyword ?
-> Out Keyword use Hota hai jab method ko multiple values return karni hoti hain.

# Part 2 - Questions on Delegates, Event and Delegates vs Events.
## Q28 :- What is the need of Delegates ?
1. Analogy
-- Restaurant Order Example
-- Process : Customer -> Waiter -> Chef
    - Customer bolta hai order
    - Waiter order forward karta hai chef ko
-- Yaha waiter ek middleman hai jo method call karwa raha hai.
-- Delegate bhi same kaam karta hai.
-- Delegate method ka reference hold karta hai aur usko call kar sakta hai.

2. Techincal
-- Delegate ek type-safe function pointer hota hai
-- jo method ka reference store karta hai aur usko invoke karta hai.
-- Matlab :  Method ko variable ki tarah pass ya call kar sakte hain.

3. Code
    public delegate void PrintMessage();

    void Hello()
    {
        Console.WriteLine("Hello");
    }

    PrintMessage del = Hello;
    del();
-- Flow
    - Delegate method ka reference store karta hai
    - Jab del() call hota hai
    - Hello() method execute hota hai


4. Example 
-- Doorbell Example
    - Doorbell press karte ho.
    - Bell system direct visitor ko handle nahi karta.
    - Wo house owner ko notify karta hai.
    - Mapping :
        - Doorbell → Delegate
        - Owner → Method
    - Delegate method ko trigger kar deta hai.

5. Delegates Kyu Chahiye
-- Callback methods ke liye
-- Event handing (Button click etc)
-- Loose coupling between objects
-- Dynamic Calls

6. Key Point
-- Delegate : Method referece Store karta hai
-- Type : Type-safe function pointer
-- Use : Events , Callbacks
-- Advantage : Loose Coupling

7. Interview
-- Delegates in C# are type-safe function pointers that hold references to methods and allow them to be invoked dynamically
-- They are mainly used for callback methods and event handling."

## Q29 :- What are events ?
1. Analogy
-- Doorbell Example
    - Socho ghar mein doorbell system hai,
    - Flow : Visitor -> Bell press karta hai -> Owner ka pata chal jata jai.
    - Bell ko nahi pata kaun open karega.
    - Bas signal bhejta hai.
    - Mapping :
        - Bell Press -> Event 
        - Owner -> Event Handler (Method)
    - Matlab jab koi action hota hai tab event trigger hota hai.

2. Technical
-- Event ek notification mechanism hai
-- Jo batata hai ki koi action ho gaya hai
-- Jab event trigger hota hai → attached method execute ho jata hai.
-- Important : Events internally delegates use karte hain

3. Code : 
    public event Action OnProcessCompleted;

    void Process()
    {
        Console.WriteLine("Process Running...");

        OnProcessCompleted?.Invoke();
    }    
-- yaha : 
    - OnProcessCompleted → event
    - .Invoke() → event trigger
-- Agar koi method subscribe hai → wo run ho jayega.
........
-- Event Subscribe Example
    process.OnProcessCompleted += ShowMessage;

    void ShowMessage()
    {
        Console.WriteLine("Process Finished");
    }
-- Flow : Process complete → Event trigger → ShowMessage() run


4. Interview
-- Events in C# are a notification mechanism that signals when an action occurs.
-- They are based on delegates and allow a class to notify other classes when something happens, such as a button click or process completion.



## Q30 :- What is a delegate and How to create a delegate ?
1. Techincal
-- Delegate ek type-safe function pointer hota hai
-- jo method ka reference store karta hai aur usko invoke karta hai.
-- Matlab :  Method ko variable ki tarah pass ya call kar sakte hain.

2. Code : 
    public delegate void PrintMessage();

    void Hello()
    {
        Console.WriteLine("Hello");
    }

    PrintMessage del = Hello;
    del();
-- Flow
    - Delegate method ka reference store karta hai
    - Jab del() call hota hai
    - Hello() method execute hota hai

## Q31 :- Where have you used delegates ?
1. Event Handling
-- Button Click 
-- Form Load
-- File Donload Complete

2. LINQ 
-- LINQ queries mein delegates use hote hain
-- Example : 
    var result = numbers.Where(x => x > 10);
-- Yaha : x => x > 10  (delegate function hai.)

3. Task / Async Programming
-- TPL aur async programming mein bhi delegates use hote hain.
-- Example : Task.Run(() => DoWork());

4. In Job
-- Button Click Pe Order Loading Start hua
-- Code pe Loading Event Compelte hota ka baad , Ek Trigger Function Takha tha .
-- Jis Ka Kaam UI ko Enable Krna retha ha.

## Q32 :- What is a Multicast delegates ?
1. Analogy
-- School Announcement Example
    - School mein principal announcement karta hai.
    - Announcement ek baar hota hai,
    - lekin multiple teachers sunte hain aur action lete hain.
    - Flow : 
        - Principal announcement → Teacher 1 react
        - Principal announcement → Teacher 2 react
        - Principal announcement → Teacher 3 react
    - Ek signal se multiple methods run ho rahe hain
    - Yahi Multicast Delegate hai.

2. Techincal 
-- Multicast Delegate ek delegate hai jo ek se zyada methods ko hold aur invoke kar sakta hai.
-- Matlab : Ek delegate call → multiple methods execute

3. Code 
    public delegate void Notify();

    void Message1()
    {
        Console.WriteLine("Message 1");
    }

    void Message2()
    {
        Console.WriteLine("Message 2");
    }

    Notify del = Message1;
    del += Message2;

    del();
-- Output 
    - Message 1
    - Message 2
-- Yaha :
    - del delegate
    - Message1 aur Message2 dono methods add ho gaye
    - Delegate Call hone par Dono methods Execute Hue.


## Q33 :- What is a Event ?
1. Analogy
-- Doorbell Example
    - Socho ghar mein doorbell system hai,
    - Flow : Visitor -> Bell press karta hai -> Owner ka pata chal jata jai.
    - Bell ko nahi pata kaun open karega.
    - Bas signal bhejta hai.
    - Mapping :
        - Bell Press -> Event 
        - Owner -> Event Handler (Method)
    - Matlab jab koi action hota hai tab event trigger hota hai.

2. Technical
-- Event ek notification mechanism hai
-- Jo batata hai ki koi action ho gaya hai
-- Jab event trigger hota hai → attached method execute ho jata hai.
-- Important : Events internally delegates use karte hain

3. Code : 
    public event Action OnProcessCompleted;

    void Process()
    {
        Console.WriteLine("Process Running...");

        OnProcessCompleted?.Invoke();
    }    
-- yaha : 
    - OnProcessCompleted → event
    - .Invoke() → event trigger
-- Agar koi method subscribe hai → wo run ho jayega.
........
-- Event Subscribe Example
    process.OnProcessCompleted += ShowMessage;

    void ShowMessage()
    {
        Console.WriteLine("Process Finished");
    }
-- Flow : Process complete → Event trigger → ShowMessage() run


4. Interview
-- Events in C# are a notification mechanism that signals when an action occurs.
-- They are based on delegates and allow a class to notify other classes when something happens, such as a button click or process completion.


## Q34 :- How to create a event ?
1. Event Creation
    public event Action OnProcessCompleted;
    void Process()
    {
        Console.WriteLine("Process Running...");

        OnProcessCompleted?.Invoke();
    }
-- Yaha 
    - OnProcessCompleted → event
    - .Invoke() → event trigger
-- Agar koi method subscribe hai → wo run ho jayega.

2. Event Subscribe Example
    process.OnProcessCompleted += ShowMessage;
    void ShowMessage()
    {
        Console.WriteLine("Process Finished");
    }
-- Flow : Process complete → Event trigger → ShowMessage() run

## Q35 :- Delegate vs Events.
1. Analogy
-- Doorbell Example 
    - Ghar mein doorbell system hai.
    - Visitor bell press karta hai → signal generate hota hai
    - AB : 
        - Bell system signal generate karta hai
        - Ghar ke log us signal par action lete hain
    - Mapping : 
        - Bell System : Event
        - Doorbell Wiring : Delegate
        - Door Open karna : Event Handler
    - Event actually delegate ka use karta hai

2. Technical
-- Delegate 
    - Delegate ek type-safe function pointer hota hai.
        - Method ka reference hold karta hai
        - Direct method call kar sakta hai
    - Example : 
        public delegate void Notify();

        Notify del = ShowMessage;
        del();
    - Yaha delegate direct method invoke kar raha hai.
-- Event 
    - Event ek special delegate wrapper hota hai jo notification system create karta hai.
        - Event ko class ke bahar se directly invoke nahi kar sakte  
        - Sirf Subscribe / Unsubscribe kar skate hai
    - Example 
        public event Action OnCompleted;
        process.OnCompleted += ShowMessage;
    - Event Delegate ko Internally Use Krta ha    

3. Main Difference
-- Delegate -> Function Pointer , Event -> Delegate Wrapper
-- Delegate -> Direct Call Possible , Event -> Direct Call Not Possible
-- Delegate -> Method Reference , Event -> Notification System
-- Delegate -> Callback , Event -> Event Driven Programming


# Part 3 - OOP, Abstraction, Encapsulation, Inheritance, Overriding & overloading
## Q36 :- Why do we need OOP ?
1. Analogy
-- Ghar Banane ka Example
-- Socho tum ghar bana rahe ho.
-- Agar sab cheeze random rakho:
    - Wiring idhar
    - Pipe udhar
    - Switch Kahin aur
    ➡️ Ghar manage karna bahut mushkil ho jayega.
-- Lekin agar proper design ho:
    - Alag room
    - Alag kitchen
    - Alag bathroom
    ➡️ Sab organized aur easy to manage ho jata hai.
-- Yahi OOP ka concept hai.
-- OOP code ko organize, reusable aur maintainable banata hai.

2. Technical
-- OOP (Object Oriented Programming) ek programming approach hai
-- jisme real world objects aur concepts ko use karke software design karte hain.
-- Example: Bank System
    - Customer 
    - Account
    - Transcation

3. OOP kyu chahiye (Main Reasons)
-- Code Reusability
    - Ek baar class banayi → multiple jagah use.
    - Example : Car class → different cars create.
-- Maintainability
    - Code organized hota hai, changes easy hote hain.
-- Security
    - Data encapsulation se protect hota hai.
    - Example : private variable
-- Scalability
    - Large application easily manage ho jati hain.

4. Interview
-- We need OOP to organize and manage complex applications using real-world objects.
-- It improves code reusability, maintainability, scalability, and security through concepts like encapsulation, inheritance, polymorphism, and abstraction.



## Q37 :- What are the important pillars of OOPs ?
dasd
## Q38 :- What is a class and object ?

## Q39 :- Abstraction vs Encapsulation?

## Q40 :- Explain Inheritance ?

## Q41 :- Explain virtual keyword ?

## Q42 :- What is overriding ?

## Q43 :- Explain overloading ?

## Q44 :- Overloading vs Overriding ?

# Part 4 - Polymorphism, Static vs Dynamic polymorphism and operator overloading.
## Q45 :- What is polymorphism ?

## Q46 :- Can polymorphism work with out inheritance ?

## Q47 :- Explain static vs dynamic polymorphism ?

## Q48 :- Explain operator overloading ?

## Q39 :- What's the difference between Abstract class and interface ?