# SECTION 1 — Value Types vs Reference Types
## What is the difference between Value Types and Reference Types in C#?
1. Analogy
-- Value Type → Photocopy ki tarah hai.
    "Agar tumhare paas ek document hai aur tumne uski photocopy kisi ko di — toh agar woh apni copy pe kuch likhta hai, tumhari original copy safe rehti hai. Dono independent hain."
-- Reference Type → Google Doc Share karne ki tarah hai.
    "Tumne ek Google Doc ka link share kiya — ab jo bhi us link pe jaake changes karega, dono ko same updated document dikhega. Ek hi cheez hai, sirf pointer/link alag alag logon ke paas hai." 

2. Techical
-- Stored In : Stack --- Heap
-- Holds : Actual Value --- Memory Address(Reference)
-- Copy Behaviour : Independent Copy --- Same object share hota hai
-- Default Value : 0, False etc --- null
-- Example : int, float, bool, struct, enum --- class, string, array, object
-- Speed : Fast --- Slow (Heap + GC)

3. Memory Diagram
    STACK                          HEAP
    ─────────────────              ──────────────────────
    a = 10  (actual value)         obj1 ──────────────► [ Name: "Ali" ]
    b = 10  (copy, independent)                              ▲
                                obj2 ─────────────────────┘
                                (same object, same memory!)

4. Interview
-- Value types store their actual data directly on the Stack, so when you assign one to another, a completely independent copy is created — changes in one don't affect the other. Common examples are int, bool, and struct.
-- Reference types, on the other hand, store only a memory address pointing to data on the Heap. So when you assign one reference variable to another, both point to the same object — changing one reflects in the other. Examples include class, array, and string.
-- This difference matters a lot in terms of performance, memory management, and avoiding unintended side effects in code.

5. Important :
-- String reference type hai, phir bhi copy jaisi behave kyun karti hai?"
→ Kyunki string immutable hai — har change pe naya object banta hai! Yeh ek common follow-up trap hai.

## Where are Value Types and Reference Types stored in memory?
-- Value Type : Stack
-- Reference Type : Heap

## What happens when you assign a Value Type to another variable?
-- Data A Copy To Data B 
-- Any Change On Data B Will not Impact Data A

## What happens when you assign a Reference Type to another variable?
-- Data A Copy To Data B 
-- Any Change On Data B Will Impact Data A
-- Bcause Of Refernece Type Behaviour
-- Both Data A and Data B Valiable Stored in Stack But Point to same value in Heap

## Give examples of Value Types and Reference Types in C#?
1. VALUE Types
-- Primitive Types
    int age = 25;
    float price = 99.99f;
    double pi = 3.14159;
    bool isActive = true;
    char grade = 'A';
    byte level = 255;
-- struct — Custom Value Type
    struct Point
    {
        public int X;
        public int Y;
    }

    Point p1 = new Point { X = 5, Y = 10 };
    Point p2 = p1;       // Independent copy!
    p2.X = 99;

    Console.WriteLine(p1.X); // 5  ✅ unchanged
    Console.WriteLine(p2.X); // 99        
-- enum — Named Constants
    enum Days { Monday, Tuesday, Wednesday }

    Days today = Days.Monday;  // Stack pe store    
-- decimal — Financial Calculations
    decimal salary = 75000.50m;  // Value type hai
    decimal bonus = salary;       // Copy ban gayi
-- Nullable Value Types
    int? marks = null;   // Value type but null hold kar sakta hai
    marks = 85;

2. REFERENCE TYPES
-- Class
-- string   
    -  String reference type hai BUT immutable hone ki wajah se Value Type jaisi behave karti hai!
--  array
-- interface 
-- delegate

## What is the difference between struct and class in terms of value/reference?
1. Analogy
-- Struct → Visiting Card
    " Jab tum kisi ko apna visiting card dete ho — tum uski photocopy dete ho. Agar woh us card pe kuch likhta hai, tumhara original card bilkul safe rehta hai. Dono alag alag hain. "
-- Class → Office Key / Access Card
    " Jab tum kisi ko apne office ki duplicate key dete ho — ab dono log same office mein jaate hain. Agar woh andar kuch rearrange kare, tum jaoge toh tumhe bhi wahi changed office milega! "

2. Techincal
-- Type  : Value --- Referecne
-- Stored : Stack --- Heap
-- Copy behaviour : Independent Copy --- Same Shared Object
-- Inheritance : ❌ Support nahi --- ✅ Full support
-- Default value : Fields ka default --- null
-- Constructor : Parameterless auto nahi --- Parameterless auto hota hai
-- null Assign : Nahi --- Ho Skta ha
-- Performance : Fast --- OverHead
-- Best For : Simple Data --- Complex , Large Objects

3. When to Use What?
    Use STRUCT when ✅                    Use CLASS when ✅
    ─────────────────────────             ──────────────────────────
    ✔ Small data (2-4 fields)            ✔ Complex, large objects
    ✔ Frequently copied data             ✔ Inheritance chahiye
    ✔ Short lifetime                     ✔ null value possible ho
    ✔ No inheritance needed              ✔ Methods heavy hoon
    ✔ Performance critical               ✔ Shared state chahiye

    Examples:                             Examples:
    → Point (X, Y)                       → Person, Car, Order
    → Color (R, G, B)                    → DbContext, HttpClient
    → DateTime                           → List<T>, Dictionary

## What is boxing and unboxing in C#? What are the performance implications of boxing and unboxing?
1. Analogy
-- Boxing → Gift Wrapping
    "Tumhare paas ek simple pen (value type) hai — jab tum use kisi ko gift karte ho, tum use ek fancy box mein pack karte ho (object/reference type). Ab woh pen ek box ke andar hai — directly accessible nahi, pehle box kholna padega."
-- Unboxing → Box Kholna 
    "Jab tumhe woh pen wapas use karni ho — tum box kholte ho, pen nikalte ho aur phir use karte ho. Yeh extra step time leta hai!"

2. Techincal
    BOXING                              UNBOXING
    ──────────────────────              ──────────────────────
    Value Type (Stack)                  Object (Heap)
        │                                   │
        ▼                                   ▼
    int i = 42                        object obj = 42
        │                                   │
    [Boxing]                          [Unboxing]
        │                                   │
        ▼                                   ▼
    object obj = i                     int i = (int)obj
    (Heap pe copy!)                    (Stack pe wapas!)


    STACK          HEAP                 STACK          HEAP
    ──────────     ────────────         ──────────     ────────
    i = 42    →   [ 42 ]  (boxed)      i = 42    ←   [ 42 ]
                object                             (unboxed)

3. Perforamce Implication
-- Boxing : High Cost -> Heap allocation + data copy
-- Unboxing :  Medium Type -> check + Stack copy
-- GC Pressure : High -> Heap objects = more GC work
-- Cache Miss : MediumHeap -> scattered in memory

4.  How to Avoid Boxing?
    ❌ Causes Boxing                    ✅ Solution
    ────────────────────────────        ────────────────────────
    ArrayList with value types    →     List<T> use karo
    String.Format with int/bool   →     String interpolation $""
    Non-generic collections       →     Generic collections
    interface variable = struct   →     Careful with interfaces
    object parameter = int        →     Generics <T> use karo

5. Interview
-- Boxing woh process hai jisme ek Value Type ko implicitly object mein convert kiya jaata hai — value Stack se Heap pe copy hoti hai aur ek wrapper object banta hai.
-- Unboxing iska ulta hai — object se wapas Value Type mein explicit cast karna padta hai.
-- Performance ke perspective se Boxing costly hai kyunki:*
    - Heap allocation hoti hai
    - Data copy hota hai
    - Garbage Collector pe extra pressure padta hai*
-- Isse avoid karne ka best tarika hai Generics use karna — jaise List<int> instead of ArrayList — jo completely type-safe hai aur boxing nahi karta."

## What is the object type in C#? How does it relate to all types?
1. Analogy
-- object → Aadhaar Card
-- India mein har insaan — doctor, engineer, farmer, student — sabke paas Aadhaar Card hai. Yeh common identity hai jo har Indian ko represent karta hai.
-- Bilkul isi tarah C# mein object woh common base hai jisse har type derive hoti hai!

2. Technical Relation
                System.Object  (object)
                            │
                ┌──────────┴──────────┐
                │                     │
            Value Types           Reference Types
                │                     │
        ┌─────────┴────────┐    ┌───────┴────────┐
        │         │        │    │       │        │
    int       bool    struct class  string   array
    float     char    enum  interface delegate
    double    decimal

3. Code
-- 4 Built-in Methods (Har Type Ko Milte Hain)
    int number = 42;
    string text  = "hello";

    number.ToString();      // "42"       — Text representation
    number.GetType();       // System.Int32 — Actual type kya hai?
    number.GetHashCode();   // Hash value
    number.Equals(42);      // True — Comparison

4. One Line Diff
-- Type Check : Object & var (Compile Time) , dynamic (Runtime)
-- Boxing : Object And dynamic (Hota hai) , var (Nahi)
-- Performace : Object (Medium) , var (Fast) , Dynamic (Slow)

5. Interview
-- object C# mein System.Object ka alias hai — yeh Universal Base Class hai jisse har type inherit karti hai — int, bool, class, string sab.
-- Yeh 4 methods provide karta hai jo har type ko milte hain — ToString(), Equals(), GetHashCode(), GetType().
-- Value type ko object mein assign karne pe Boxing hoti hai — isliye performance-critical code mein Generics prefer karte hain.

## What is a nullable value type? (int?, Nullable<T>)
1. Analogy
-- Normal int → Attendance Register 
    "Har student ka marks likhna compulsory hai — blank nahi chhod sakte. Koi na koi value deni hi padegi."
-- int? → Optional Form Field 
    "Ek form mein kuch fields optional hain — tum chahein toh bharo, chahein toh blank chhod do (null). Dono valid hai!"

2. Techincal
    int  age = null;   // ❌ Error! Value type null nahi ho sakta
    int? age = null;   // ✅ Valid! Nullable value type

    // int? internally yahi hai:
    Nullable<int> age = null;  // Same cheez!
-- int? sirf Nullable<int> ka shorthand hai — dono same hain!

3. Code
-- Basic Use
    int? marks = null;    // No value yet
    marks = 85;           // Ab value hai

    // Check karo — value hai ya nahi?
    Console.WriteLine(marks.HasValue);  // True
    Console.WriteLine(marks.Value);     // 85

    // GetValueOrDefault — null ho toh default do
    int? score = null;
    Console.WriteLine(score.GetValueOrDefault());     // 0
    Console.WriteLine(score.GetValueOrDefault(50));   // 50
...........
--  Null Coalescing Operator ??
    int? age = null;

    // ?? — null ho toh right side use karo
    int result = age ?? 18;   
    Console.WriteLine(result); // 18 ✅

    age = 25;
    result = age ?? 18;
    Console.WriteLine(result); // 25 ✅

4. Key Points
-- .HasValue : Value ha ya null (true / false)
-- .Value : Actual Value
-- .GetValueOrDefault() : null nahi tho default Do (age.GetValueOrDefault(18))
-- ?? : Null fallback (age ?? 18)

5. Interview
-- Value types by default null nahi ho sakte — jaise int, bool. Lekin real world mein kabhi kabhi value optional hoti hai — jaise database mein koi field empty ho.
-- Iske liye C# mein Nullable Value Type hai — int? ya Nullable<int> — jo value type ko null hold karne ki ability deta hai.
-- ?? operator use karte hain null ka fallback value dene ke liye.

6. Bonus
-- int? Value Type hai ya Reference Type?
→ Value Type hi hai! Bas null hold karne ki extra ability hai Nullable<T> struct ki wajah se! 

# SECTION 2 — Type System & Keywords

## What is the difference between var, explicit types, and dynamic?
## When should you use var and when should you avoid it?
## What is dynamic keyword? How is it different from object?
## What is the difference between const and readonly?
## Can readonly be set inside a constructor?
## Can const be used with reference types?
## What is static keyword? What are static classes?
## What is the difference between static readonly and const?
## What is the sealed keyword on a class?
## What is the partial keyword in C#?

# SECTION 3 — Strings

What is the difference between string and String in C#?
Why are strings immutable in C#?
What is string interning?
What is the difference between string and StringBuilder?
When should you use StringBuilder over string?
What is string.Format() vs string interpolation ($"")?
What is @ verbatim string literal?
What is the difference between == and .Equals() for strings?
What are raw string literals in C# 11?
What is string.IsNullOrEmpty() vs string.IsNullOrWhiteSpace()?

# SECTION 4 — Method Parameters

What is the difference between passing by value and passing by reference?
What is the ref keyword in C#?
What is the out keyword in C#?
What is the difference between ref and out?
What is the in keyword in C#?
What is the params keyword in C#?
Can you use ref and out with async methods?
What is optional parameters in C#?
What is named arguments in C#?
What is the difference between ref, out and returning a Tuple?




📌 SECTION 5 — Nullable & Null Handling

What is a nullable type in C#?
What is the difference between null and default value?
What is the null coalescing operator ???
What is the null coalescing assignment operator ??=?
What is the null conditional operator ?.?
What is the difference between ?. and null check if (x != null)?
What is NullReferenceException? How do you prevent it?
What are nullable reference types in C# 8+?
What is the ! null forgiving operator in C#?
What is the difference between default keyword for nullable vs non-nullable types?


📌 SECTION 6 — Pattern Matching

What is Pattern Matching in C#?
What is the is pattern matching expression?
What is the switch expression in C# 8+?
What is the difference between switch statement and switch expression?
What is a positional pattern in C#?
What is a property pattern in C#?
What is a tuple pattern in C#?
What is a relational pattern in C#?
What is a logical pattern (and, or, not) in C#?
What is a list pattern in C# 11?


📌 SECTION 7 — Tuples & Deconstruction

What are Tuples in C#?
What is the difference between Tuple<T> and ValueTuple?
How do you name tuple elements in C#?
What is tuple deconstruction in C#?
What is the _ discard variable in C#?
How are tuples useful as return types vs creating a class?
What is the performance difference between Tuple and ValueTuple?
Can you deconstruct a custom class in C#?
What is positional deconstruction?
When should you use Tuples vs creating a dedicated class/struct?


📌 SECTION 8 — Type Conversion & Casting

What is implicit conversion vs explicit conversion in C#?
What is the difference between (int)x casting and Convert.ToInt32(x)?
What is as keyword in C#?
What is is keyword in C#?
What is the difference between as and explicit casting?
What is TryParse vs Parse?
What are user-defined conversions (implicit operator, explicit operator)?
What is checked and unchecked in C#?
What is widening vs narrowing conversion?
What is the difference between Convert.ToString() and .ToString()?


📌 SECTION 9 — Modern C# Features

What are records in C# 9+?
What is the difference between record, record class, and record struct?
What is init only setter in C#?
What are global usings in C# 10?
What are file-scoped namespaces in C# 10?
What is required keyword in C# 11?
What are primary constructors in C# 12?
What is collection expressions in C# 12?
What is the difference between with expression and object initializer?
What are top-level statements in C# 9?


📌 SECTION 10 — Miscellaneous but Important

What is the difference between == and ReferenceEquals()?
What is GetHashCode() and when should you override it?
What is the nameof() operator?
What is the sizeof() operator?
What is typeof() vs GetType() in C#?
What is the difference between Array and Span<T>?
What is unsafe code in C#?
What is the stackalloc keyword?
What are preprocessor directives in C# (#if, #region, #pragma)?
What is the difference between early-bound and late-bound in C#?