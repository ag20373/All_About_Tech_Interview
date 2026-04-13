# 🔷 SECTION 1 — Basics & Fundamentals
## What is a Class vs an Object?
1. Analogy
-- Class = Blueprint
-- Object = Actual House
-- Agar tum ghar banana chahte ho:
    - Blueprint me design hota hai (rooms, kitchen, bathroom)
    - Us blueprint se multiple houses ban sakte hain
-- Same tarah:
    - Class = blueprint / design
    - Object = actual instance jo memory me create hota hai
-- Example : 
    - Car = Class
    - BMW , Audi , Tesla = Objects

2. Techincal
-- Class
    - Ek user-defined data type hota hai
    - Isme properties (data) + methods (behavior) defined hote hain
    - Ye Sirf structure define karta hai.
-- Object
    - Class ka instance hota hai
    - Runtime me memory allocate hoti hai
    - Object ke through hi class ke methods aur properties use karte hain

3. Code (Important)
    class Car
    {
        public string Color;
        public void Drive()
        {
            Console.WriteLine("Car is driving");
        }
    }

    // Object creation
    Car myCar = new Car();
    myCar.Color = "Red";
    myCar.Drive();

4. Important
-- Class = Defination
-- Object = Instance
-- Ek class se multiple objects create ho sakte hain
-- Object create hone par memory allocate hoti hai

5. Interview
-- A class is a blueprint that defines properties and methods,
-- While an object is an instance of that class created at runtime which occupies memory.

## What is a Constructor and what are its types?
1. Analogy
-- Socho tum naya mobile phone kharidte ho
-- Jab phone first time ON hota hai, wo automatically initial setup karta hai:
    - Language Select
    - Date Time Set
    - Default Settings
-- Ye setup automatic hota hai jab object create hota hai.
-- Same tahar Prohramming me : 
    - Constructor automatically run hota hai
    - Jab object create hota hai

2. Technical 
-- Constructor ek special method hota hai jo object create hone par automatically call hota hai.
-- Purpose 
    - Object Ko initizlize Karne
    - Default values set karna
-- Rules
    - Constructor ka name class ke same hota hai
    - Return Type Nahi hoti
    - Object create hone par Automatically execute hota hai.

3. Code 
    class Car
    {
        public string color;

        public Car()
        {
            color = "Red";
        }
    }

    Car c1 = new Car();
-- Jab new Car() Call Hua -> Construmtor automatically run ho gaya

4. Types : 
-- Default Constructor
    - Agar programmer constructor nahi banata, compiler khud bana deta hai.
    - class car {}
...........
-- Parameterized Constructor
    - Values bahar se deke object banao
    - Code :
        class Student
        {
            public string Name;
            public int Age;

            // Parameterized Constructor
            public Student(string name, int age)
            {
                Name = name;
                Age = age;
                Console.WriteLine($"{Name} ka object ban gaya!");
            }
        }

        // Usage
        Student s1 = new Student("Rahul", 20);
        // Output: Rahul ka object ban gaya!

        Student s2 = new Student("Priya", 22);
        // Output: Priya ka object ban gaya!
...............
-- Copy Constructor
    - Ek object ki copy banao doosre se
    - Code : 
        class Student
        {
            public string Name;
            public int Age;

            // Parameterized
            public Student(string name, int age)
            {
                Name = name;
                Age = age;
            }

            // Copy Constructor
            public Student(Student other)
            {
                Name = other.Name;
                Age  = other.Age;
                Console.WriteLine($"{Name} ki copy ban gayi!");
            }
        }

        // Usage
        Student s1 = new Student("Rahul", 20);
        Student s2 = new Student(s1);  // s1 ki copy
        // Output: Rahul ki copy ban gayi!
............
-- Static Constructor
    - Class level pe ek baar chalta hai — objects se pehle Sirf static data initialize karta hai
    - Code
        class School
        {
            public static string SchoolName;
            public string StudentName;

            // Static Constructor
            static School()
            {
                SchoolName = "Delhi Public School";
                Console.WriteLine("School ek baar setup ho gayi!");
            }

            // Parameterized Constructor
            public School(string name)
            {
                StudentName = name;
                Console.WriteLine($"{StudentName} join kiya {SchoolName}");
            }
        }

        // Usage
        School s1 = new School("Rahul");
        School s2 = new School("Priya");

        // Output:
        // School ek baar setup ho gayi!   ← Static: sirf 1 baar
        // Rahul join kiya Delhi Public School
        // Priya join kiya Delhi Public School
............    
-- Private Constructor
    - Bahar se object nahi ban sakta — Singleton pattern mein use hota hai
    - Code : 
        class DatabaseConnection
        {
            private static DatabaseConnection instance;

            // Private Constructor — bahar se block!
            private DatabaseConnection()
            {
                Console.WriteLine("DB Connected!");
            }

            // Sirf is method se milega object
            public static DatabaseConnection GetInstance()
            {
                if (instance == null)
                    instance = new DatabaseConnection();
                
                return instance;
            }
        }

        // Usage
        // DatabaseConnection db = new DatabaseConnection(); 
        // ❌ ERROR — private hai!

        DatabaseConnection db = DatabaseConnection.GetInstance(); 
        // ✅ Output: DB Connected!


5. Real Life Scenario
-- Socho Zomato pe order karte ho
    Default Constructor     → App khula, default location "Unknown" set ho gayi
    Parameterized           → Tune apna naam + address diya → account bana
    Copy Constructor        → "Save this address" → naya address copy se bana
    Static Constructor      → Zomato ka server ek baar start hua — sabke liye
    Private Constructor     → Sirf EK database connection — dunia mein ek hi instance

6. Interview
-- Constructor ek special method hai jo object creation ke time automatically invoke hota hai, iska koi return type nahi hota aur naam class jaisa hota hai
-- C# mein 5 types hote hain — Default, Parameterized, Copy, Static, aur Private. Static constructor sirf ek baar run hota hai aur Private constructor Singleton pattern implement karne ke liye use hota hai.

## What is a Destructor? When is it called in C#?
1. Analogy
-- Destructor ek special method hai jo automatically call hota hai jab object destroy hone wala hota hai — yaani jab object ki life khatam hoti hai.
-- Jaise school mein last day hota hai — TC (Transfer Certificate) milta hai, records clean hote hain, locker khali karta hai. Koi manually nahi karta — system automatically karta hai. Wahi Destructor hai! 🏫

2. Techincally
-- Destructor ek special method hota hai jo object destroy hone se pehle cleanup ke liye use hota hai.
-- C# me Destructiir
    - automatic call hota hai
    - Garbage Collector (GC) call karta hai
    - Object memory se remove hone se pehle run hota hai
    - Syntax me ~ use hota hai.

3. Code
    class Student
    {
        public string Name;

        // Constructor — Object bana
        public Student(string name)
        {
            Name = name;
            Console.WriteLine($"{Name} ka object BAN gaya! ✅");
        }

        // Destructor — Object destroy hoga
        ~Student()
        {
            Console.WriteLine($"{Name} ka object DESTROY ho gaya! ❌");
        }
    }

    class Program
    {
        static void Main()
        {
            Student s1 = new Student("Rahul");
            Student s2 = new Student("Priya");

            Console.WriteLine("Program chal raha hai...");

        } // Yahan scope khatam → GC destroy karega

    // Output:
    // Rahul ka object BAN gaya! ✅
    // Priya ka object BAN gaya! ✅
    // Program chal raha hai...
    // Priya ka object DESTROY ho gaya! ❌
    // Rahul ka object DESTROY ho gaya! ❌
    }

4. C# Mein Destructor Kaise Kaam Karta Hai?
Tumhara Code
     ↓
Object bana  →  Constructor call ✅
     ↓
Object use hua
     ↓
Object ka reference khatam hua
     ↓
Garbage Collector (GC) aaya  ←─── C# automatically manage karta hai
     ↓
Destructor call hua  ~ClassName()
     ↓
Memory free! 🧹

5. IDisposable — Better Alternative in C#
-- C# mein Destructor se zyada IDisposable prefer karte hain!

6. IDisposable — Code
    class DatabaseConnection : IDisposable
    {
        public DatabaseConnection()
        {
            Console.WriteLine("DB Connection OPEN hua! ✅");
        }

        // Dispose — Tum khud control karo cleanup
        public void Dispose()
        {
            Console.WriteLine("DB Connection CLOSE ho gaya! ❌");
        }
    }

    // Usage — 'using' block automatically Dispose() call karta hai
    class Program
    {
        static void Main()
        {
            using (DatabaseConnection db = new DatabaseConnection())
            {
                Console.WriteLine("Database use ho raha hai...");

            } // Yahan automatically Dispose() call!

            // Output:
            // DB Connection OPEN hua! ✅
            // Database use ho raha hai...
            // DB Connection CLOSE ho gaya! ❌
        }
    }

7. IDisposable Real Life Scenario
    Constructor  →  Book issue karwai  (resource liya)
    using block  →  Book padhi
    Dispose()    →  Book wapas ki      (resource choda — TUM control mein ho!)

    vs

    Destructor   →  Tum bhool gaye — Library wala khud aake 
                    book le gaya jab uska mann kiya 😅
                    (GC control mein hai — TUM nahi!)

8. Interview
-- Destructor C# mein ~ClassName() se define hota hai aur Garbage Collector automatically call karta hai jab object destroy hone wala ho
-- Iska koi return type, parameter, ya access modifier nahi hota aur overload nahi ho sakta.
-- But practically C# mein hum Destructor ke bajaye IDisposable interface aur using statement prefer karte hain — kyunki isse hum khud control karte hain ki resources kab release hon, instead of GC pe depend karna.
-- C# ka GC non-deterministic hai — exact time pata nahi kab destroy karega
-- Destructor internally Finalize() method mein convert hota hai by compiler
-- IDisposable + using → Production code mein yahi use karo ✅
-- File, DB Connection, Network Stream → Inke liye hamesha Dispose() use karo
-- Destructor aur IDisposable dono saath use karna → Best Practice hai

## What is the this keyword in C#?
1. Analogy
-- this keyword current object ko refer karta hai — yaani jo object abhi kaam kar raha hai, uski taraf point karta hai.
-- Jaise class mein teacher puche "Kaun present hai?" — tum khud apni taraf point karke bolo "Main!" — wahi this hai! 🙋‍♂️

2. Techincal
-- this ek reference keyword hai jo current class object ko refer karta hai.
-- Mostly Use Hota Hai :
    - Current object ko refer karne ke liye
    - Class variables aur parameters ko differentiate karne ke liye
    - Constructor chaining me

3. C# Code — 5 Uses of this
-- Variable Ambiguity Hatana
    - Jab parameter aur field ka naam same ho
    - Code 
        class Student
        {
            private string name;  // Field
            private int age;      // Field

            public Student(string name, int age)
            {
                // name = name; ❌ Confusing! Konsa name?
                
                this.name = name;  // ✅ this.name = Field
                                //        name = Parameter
                this.age  = age;
            }

            public void Show()
            {
                Console.WriteLine($"Name: {this.name}, Age: {this.age}");
            }
        }

        // Usage
        Student s1 = new Student("Rahul", 20);
        s1.Show();
        // Output: Name: Rahul, Age: 20   
............        
-- Constructor Chaining - this()
    - Ek Constructor se Doosra constructor call kro
    - Code 
        class Student
        {
            public string Name;
            public int Age;
            public string City;

            // Main Constructor
            public Student(string name, int age, string city)
            {
                Name = name;
                Age  = age;
                City = city;
                Console.WriteLine($"Full Object bana: {Name}, {Age}, {City}");
            }

            // Chaining — this() se upar wala call hoga
            public Student(string name, int age) 
                : this(name, age, "Unknown City")  // ← Chaining!
            {
                Console.WriteLine($"2 param se bana: {Name}");
            }

            // Aur ek chaining
            public Student(string name) 
                : this(name, 0)  // ← Upar wale ko call kiya
            {
                Console.WriteLine($"1 param se bana: {Name}");
            }
        }

        // Usage
        Student s1 = new Student("Rahul", 20, "Delhi");
        Console.WriteLine("---");
        Student s2 = new Student("Priya", 22);
        Console.WriteLine("---");
        Student s3 = new Student("Amit");

        // Output:
        // Full Object bana: Rahul, 20, Delhi
        // ---
        // Full Object bana: Priya, 22, Unknown City
        // 2 param se bana: Priya
        // ---
        // Full Object bana: Amit, 0, Unknown City
        // 2 param se bana: Amit
        // 1 param se bana: Amit      
.................. 
-- Current Object Ko Method Mein Pass Karna
    - Code
        class Order
        {
            public string Item;
            public double Price;

            public Order(string item, double price)
            {
                Item  = item;
                Price = price;
            }

            // Apne aap ko Invoice ko pass karna
            public void GenerateInvoice()
            {
                Invoice inv = new Invoice();
                inv.Print(this);  // ← Current object pass kiya!
            }
        }

        class Invoice
        {
            public void Print(Order order)
            {
                Console.WriteLine($"Invoice: {order.Item} → ₹{order.Price}");
            }
        }

        // Usage
        Order o1 = new Order("Laptop", 75000);
        o1.GenerateInvoice();
        // Output: Invoice: Laptop → ₹75000
...............
-- Method Chaining — Fluent Style
    - Ek Line mein baar baar methods call karo
    - Code
        class QueryBuilder
        {
            private string table  = "";
            private string condition = "";
            private int    limit  = 0;

            public QueryBuilder From(string tableName)
            {
                table = tableName;
                return this;  // ← Apne aap ko return kiya!
            }

            public QueryBuilder Where(string cond)
            {
                condition = cond;
                return this;  // ← Apne aap ko return kiya!
            }

            public QueryBuilder Limit(int n)
            {
                limit = n;
                return this;  // ← Apne aap ko return kiya!
            }

            public void Run()
            {
                Console.WriteLine($"SELECT * FROM {table} WHERE {condition} LIMIT {limit}");
            }
        }

        // Usage — Fluent / Chained style!
        new QueryBuilder()
            .From("Students")
            .Where("Age > 18")
            .Limit(10)
            .Run();

        // Output:
        // SELECT * FROM Students WHERE Age > 18 LIMIT 10 
................
-- Indexer Mein this
    - Class ko array jaisa use karne do   
    - Code : 
        class Classroom
        {
            private string[] students = new string[5];

            // Indexer — this use karta hai
            public string this[int index]
            {
                get { return students[index]; }
                set { students[index] = value; }
            }
        }

        // Usage
        Classroom room = new Classroom();
        room[0] = "Rahul";   // ← Array jaisa!
        room[1] = "Priya";
        room[2] = "Amit";

        Console.WriteLine(room[0]);  // Rahul
        Console.WriteLine(room[1]);  // Priya   

4. Interview
-- this keyword C# mein current instance ka reference hai. 
-- Iske 4 main uses hain 
    - pehla: field aur parameter ka naam same hone par ambiguity resolve karna
    - Doosra: constructor chaining ke liye this() use karna.
    - Teesra: current object ko kisi method mein argument ki tarah pass karna.
    - chautha: method chaining ke liye return this use karna jo Fluent Interface pattern banata hai."

5. Interview Killer Point
-- this sirf instance context mein kaam karta hai — static methods mein nahi ❌
-- Constructor Chaining se code duplication avoid hoti hai ✅
-- return this → Fluent Interface / Builder Pattern ka base hai
-- Indexer sirf this keyword se hi banta hai C# mein
-- this ka use optional hai jab ambiguity na ho — but readability ke liye likh sakte ho


## What is the difference between a Class and a Struct in C#?
1. Analogy
-- Socho Courier Service
-- Class
    - Tum original package bhejte ho
    - Agar kisi ne package modify kiya → original bhi change ho jata hai
-- Struct 
    - Tum package ki copy bhejte ho
    - Agar copy change hui → original par koi effect nahi
-- Yani : 
    - Class - referecne share hota hai.
    - Struct - Copy Create hota hai

2. Technical
-- Class 
    - Reference Type
    - Memory Heap me allocate hoti hai.
    - Variable me reference store Hota  hai.
-- Struct 
    - Value Type 
    - Memory mostly Stack me Allocate hoti hai.
    - Variable me actual value store hoti hai

3. Sabse Bada Difference — Value vs Reference Type
    CLASS (Reference Type)
    ━━━━━━━━━━━━━━━━━━━━━
    Stack                    Heap
    ┌─────────┐             ┌──────────────┐
    │ s1  ────┼────────────►│ Name: Rahul  │
    └─────────┘             │ Age : 20     │
    ┌─────────┐             └──────────────┘
    │ s2  ────┼────────────►  (Same object!)
    └─────────┘             

    s1 aur s2 SAME object point kar rahe hain!
    Ek change karo → dono mein change!

    STRUCT (Value Type)
    ━━━━━━━━━━━━━━━━━━━
    Stack only
    ┌──────────────┐    ┌──────────────┐
    │ s1           │    │ s2           │
    │ Name: Rahul  │    │ Name: Rahul  │ ← COPY ban gayi!
    │ Age : 20     │    │ Age : 20     │
    └──────────────┘    └──────────────┘

    s1 aur s2 ALAG copies hain!
    Ek change karo → doosra nahi badlega!

4. Kab Kya Use Karein ?
-- STRUCT use karo jab:
    - Data chhota ho (16 bytes)
    - Short-lived objects    
    - Value copy chahiye  
    - Math/Geometry (Point, Color)
    - Performance critical code
-- CLASS use karo jab
    - Data complex ho
    - Inheritance chahiye
    - Reference behaviour chahiye
    - Business logic ho
    - Long-lived objects

5. Interview Important
-- Stack vs Heap — struct fast, class flexible
-- DateTime, int, bool, Point — C# ke built-in structs hain ✅
-- Struct mein parameterless constructor C# 9 se pehle nahi bana sakte the
-- Boxing/Unboxing — struct ko object mein convert karna costly hai 
-- Record Struct — C# 10 mein aaya — immutable value type 
-- Struct interface implement kar sakta hai — but inherit nahi kar sakta

6. Interview
-- Class ek reference type hai jo heap pe store hoti hai — assignment pe reference copy hota hai. Struct ek value type hai jo stack pe store hota hai — assignment pe value copy hoti hai. 
-- Class inheritance support karti hai, null ho sakti hai, aur complex objects ke liye best hai. Struct lightweight hai, faster hai small data ke liye, lekin inheritance support nahi karta
-- C# mein DateTime, Point, Color — yeh sab structs hain. Jab data 16 bytes se chhota ho aur copy semantics chahiye, tab struct prefer karo."

## What are instance variables vs static variables?
1. Analogy
-- Socho School
-- Instance Variable
    - Har student ka apna roll number aur name hota hai
    - Ye har student ke liye alag hota hai
-- Static Variable
    - School ke naam same hota hai sab students ke liye.
-- Example :
    - Student1 -> RollNo. = 1
    - Student2 -> RollNo = 2
    - SchoolName → Same for everyone
-- Yani:
    - Instance → object specific
    - Static → class shared

2. Technical
-- Instance Variable
    - Class ke andar define hoti hai.
    - Har Object ke liye separate copy hoti ha
    - Object ke through access hoti hai.
-- Technical
    - static keyword se declare hoti hai
    - Sab objects ke beech shared hoti hai
    - Class ke through access hoti hai

3. Memory Mein Kya Hota Hai ?
    INSTANCE VARIABLE
    ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
            Heap Memory

    ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐
    │   s1 (Object)   │  │   s2 (Object)   │  │   s3 (Object)   │
    │─────────────────│  │─────────────────│  │─────────────────│
    │ Name  : Rahul   │  │ Name  : Priya   │  │ Name  : Amit    │
    │ Age   : 20      │  │ Age   : 22      │  │ Age   : 19      │
    │ Marks : 85      │  │ Marks : 90      │  │ Marks : 78      │
    └─────────────────┘  └─────────────────┘  └─────────────────┘
    Alag copy ✅           Alag copy ✅          Alag copy ✅


    STATIC VARIABLE
    ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
            Class Level Memory (Single Copy)

                ┌──────────────────────┐
                │   Student (Class)    │
                │──────────────────────│
                │ SchoolName : "DPS"   │ ◄─── Ek hi copy!
                │ TotalStudents : 3    │ ◄─── Sab share karte!
                └──────────────────────┘
                        ▲       ▲       ▲
                    s1      s2      s3
                (sab yahi dekhte hain)

## Can a constructor be private? What's the use case?
1. Analogy
-- Haan! Constructor private ho sakta hai.
-- Jaise VIP Club ka door — bahar se koi directly andar nahi aa sakta. Sirf ek special entry gate hai. Wahi private constructor hai! 

2. Techincal
-- Haan, constructor private ho sakta hai.
-- Agar constructor private ho 
    - Class ka object bahar se create nahi ho sakta
    - Sirf class ke andar se hi object create hoga
-- Use Case 
    - Singleton Pattern
    - Utility Class (static class)
    - Object creation control karna

3. Code 
    class DatabaseConnection
    {
        // Sirf ek instance — static
        private static DatabaseConnection instance = null;

        // Private Constructor — bahar se block!
        private DatabaseConnection()
        {
            Console.WriteLine("DB Connected! ✅");
        }

        // Sirf yahan se milega object
        public static DatabaseConnection GetInstance()
        {
            if (instance == null)
                instance = new DatabaseConnection(); // Pehli baar bana

            return instance; // Wahi purana deta hai
        }
    }

    // Usage
    var db1 = DatabaseConnection.GetInstance(); // DB Connected! ✅
    var db2 = DatabaseConnection.GetInstance(); // Kuch nahi — wahi dega

    Console.WriteLine(db1 == db2); // True — Same object! ✅

4. Important Points
-- Private constructor → object creation restrict karta hai
-- Mostly use hota hai Singleton pattern me
-- Utility classes me bhi use hota hai

5. Interview
-- Yes, a constructor can be private in C#.
-- It is used to restrict object creation from outside the class
-- A common use case is the Singleton pattern where only one instance of the class is allowed.

## What is a copy constructor in C#?
1. Analogy
-- Socho tumhare paas ek filled form hai
-- Ab tum same details wala ek aur form banana chahte ho.
-- Tum kya karoge?
-- Purane form ko dekh kar same details copy kar doge.
-- Programming me bhi copy constructor ka kaam hota hai:
👉 ek object ki values dusre object me copy karna

2. Techincal
-- Copy Constructor ek constructor hota hai jo same class ka object parameter me leta hai aur uski values new object me copy karta hai.
-- Purpose: 
    - Object ki duplicate copy create karna
    - Same data ke saath naya object banana

3. Code: 
    class Car
    {
        public string Color;

        public Car(string color)
        {
            Color = color;
        }

        // Copy Constructor
        public Car(Car obj)
        {
            Color = obj.Color;
        }
    }

    Car c1 = new Car("Red");
    Car c2 = new Car(c1);    
-- c1 -> Original
-- c2 -> Copied Object

4. Important Point
-- Parameter same class ka object hota hai
-- New object create hota hai
-- Data copy hota hai reference share nahi hota (value fields)

5. Interview Me Kaise Bolna 
-- A copy constructor is a constructor that takes an object of the same class as a parameter and creates a new object by copying the values from the existing object.

## What is object initializer syntax in C#?
1. Analogy
-- Socho tum online form fill kar rahe ho
-- Normal Trika
    - Pehle account create karo
    - Phir alag-alag fields fill karo
-- Better Tarika
    - Form open karo aur ek hi time par saari details fill kar do
-- Programming me object initializer bhi same kaam karta hai.

2. Technical
-- Object Initlizer Syntax Allow karta hai :
    - Object create karte time hi properties initialize karna
    - Without calling multiple setters manually
-- Syntax :
    - new ClassName {Property = value}

3. Real World Coding Use Case
-- Trading / Order Management System me jab Order object create karte hain.
-- Normal Trika
    Order order = new Order();
    order.ClientId = "C101";
    order.Qty = 100;
    order.Price = 250;
-- Better readable Tarika
    Order order = new Order
    {
        ClientId = "C101",
        Qty = 100,
        Price = 250
    };
-- Real projects me DTOs, Models, API responses, Entity objects create karte waqt ye bahut use hota hai.

4. Important
-- Code Clean And Readable
-- Multiple setter calls avoid ho jate hain
-- Mostly used with properties (get/set)


## What is the difference between new keyword and object pooling? 
1. Analogy
-- new — har baar fresh object banao — memory lo, kaam karo, phek do!
-- Object Pooling — pehle se bane objects reuse karo — wastage nahi! 
-- Jaise OLA / Uber
    - new = Har ride ke liye nई car kharido, kaam ho gaya toh phek do 
    - Pooling = Ek fleet of cars ready hai — kisi ko do, kaam ho gaya toh wapas pool mein

2. Code 
🔴 new — Har Baar Naya Object
    class DBConnection
    {
        public DBConnection()
        {
            Console.WriteLine("Naya connection banaya! 🔌");
        }

        public void Query()
        {
            Console.WriteLine("Query chal rahi hai...");
        }
    }

    // Har baar naya — costly! ❌
    for (int i = 0; i < 3; i++)
    {
        DBConnection conn = new DBConnection(); // Baar baar naya!
        conn.Query();
    } 

    // Output:
    // Naya connection banaya! 🔌
    // Query chal rahi hai...
    // Naya connection banaya! 🔌
    // Query chal rahi hai...
    // Naya connection banaya! 🔌
    // Query chal rahi hai...
.........
🟢 Object Pooling — Reuse Karo
    using Microsoft.Extensions.ObjectPool; // .NET built-in pool

    class DBConnection
    {
        public string Name;

        public void Query(string q)
        {
            Console.WriteLine($"{Name} → {q}");
        }
    }

    // Pool banao
    var pool = new DefaultObjectPool<DBConnection>(
        new DefaultPooledObjectPolicy<DBConnection>()
    );

    // Object lo pool se
    DBConnection conn1 = pool.Get();
    conn1.Name = "Conn1";
    conn1.Query("SELECT * FROM Users");

    // Kaam hua — wapas pool mein do!
    pool.Return(conn1);

    // Phir se lo — SAME object milega!
    DBConnection conn2 = pool.Get();
    conn2.Query("SELECT * FROM Orders"); // Naya nahi bana! ♻️

    // Output:
    // Conn1 → SELECT * FROM Users
    // Conn1 → SELECT * FROM Orders  ← Same object reuse! ✅   

3. Real Life
    new keyword   =  Har baar naya glass lo,
                    paani piyo, glass todo 😱
                    (wasteful + expensive)

    Object Pool   =  Restaurant mein glasses
                    pool mein hain — lo, use karo,
                    wash karo, wapas rakho ♻️
                    (smart + efficient)

4. Important
-- new → Simple, easy, low performance apps ke liye
-- Object Pool → High traffic, performance critical apps ke liye
-- Real Examples → DB Connection Pool, Thread Pool, ArrayPool

5. Interview
-- new keyword har baar heap pe fresh object banata hai aur GC usse destroy karta hai — yeh costly operation hai. 
-- Object Pooling mein pehle se bane objects reuse hote hain — object kaam karne ke baad destroy nahi hota, pool mein wapas jaata hai.
-- Yeh performance critical applications mein use hota hai jaise database connections, HTTP clients, ya game engines. .NET mein ObjectPool<T> aur ArrayPool<T> built-in pooling provide karte hain."

# 🔷 SECTION 2 — Encapsulation
## What is Encapsulation and why does it matter?
1. Analogy
-- Socho ATM Machine 🏧
-- Tum ATM me :
    - Withdraw kar sakte ho
    - Balance Check Kr Sakrte ho
-- Lekin tum bank database ya internal logic access nahi kar sakte.
-- ATM internal system ko hide karta hai aur sirf controlled operations allow karta hai
-- Ye hi Encapsulation ha

2. Technical 
-- Encapsulation ka matlab hai:
    👉 Data (variables) aur behavior (methods) ko ek class me bundle karna
    👉 Direct access ko restrict karna using access modifiers
-- Usually :
    - Data -> private
    - Access -> public methods / properties

3. Real World Coding Use Case
-- Trading / RMS system me client balance directly change nahi hona chahiye.
-- Galat tarika :   
    client.Balance = -1000000;
-- Correct Traika   
    - Balance Private Rakho
    - Changes methods ke through allow karo
-- Example  
    - Deposit
    - Withdraw
    - Margin Block
-- Isse invalid state prevent hoti ha.

4. Code 
    class BankAccount
    {
        private decimal balance;

        public void Deposit(decimal amount)
        {
            balance += amount;
        }

        public decimal GetBalance()
        {
            return balance;
        }
    }

5. Important
-- private field + public property = Encapsulation
-- Validation Sirf ek jagah - propery ke andar.
-- Auto Property shorthand bhi hota hai jab validation na ho: 
    public string Name { get; set; }

6. Interview
-- Encapsulation ka matlab hai data ko hide karna aur sirf controlled interface ke through access dena.
-- C# mein private fields aur public properties se implement karte hain. 
-- Iska sabse bada faida hai ki validation ek jagah hoti hai — koi bhi directly invalid data set nahi kar sakta
-- Real project mein yeh har model class mein use hota hai."

## What are access modifiers in C#? (public, private, protected, internal, protected internal)
1. Analogy
-- Socho Apartment Building 
    - public → Main gate — koi bhi aa sakta hai
    - private → Apna bedroom — sirf tum
    - protected → Family room — tum + tumhare bacche (child class)
    - internal → Building ke andar — sirf same building waale
    - protected internal → Same building waale + bahar ki family dono

2. Technical Defination
-- Access modifiers control karte hain visibility of:
    - Classes
    - methods 
    - Variables
    - properties

3. Types
-- pulbic 
    - Sab jagah se accessible.
    - Code
        public class Order
        {
            public int Qty;
        }
    - Use When Global access allowed ho.
-- private
    - Sirf same class ke andar access.
    - Code
        class Account
        {
            private decimal balance;
        }
    - Usually data hiding ke liye.
-- protected
    - Sirf same class + derived class access kar sakte hain.
    - Inheritence me use hota hai.
    - Code : protected int margin;
-- internal
    - Sirf same assembly / project ke andar access.
    - Different project access nahi kar sakta.
    - Example : internal class RiskEngine {}
-- protected internal
    - Accessible by: 
    - Same assembly
    - derived classes

4. Important Points
-- Default for class member -> private
-- Default for top-level -> internal
-- Encapsulation implement karne me help karta hai

5. Interview
-- Access modifiers in C# control the visibility of classes and their members.
-- The main types are public, private, protected, internal, and protected internal, each defining where the member can be accessed from.

## What are Properties in C#? How are they better than public fields?
1. Analogy
-- Socho Bank Account 💳
-- Agar bank bole : " Aap directly database me jaakar balance change kar sakte ho. "
-- ye dangerous hai.
-- Isliya bank kya karta hai :
    - Deposit()
    - Withdraw()
    - CheckBalance()
-- Yani direct access nahi — controlled access.
-- C# me properties bhi same kaam karti hain. 

2. Technical
-- Property ek class member hota hai jo fields ko controlled access deta hai using get and set.
    - get : value read karne ke liye
    - set : value update karne ke liya
-- Isse encapsulation maintain hoti hai.

3. Important Point
-- Validation add kar sakte ho
-- Encapsulation maintain hoti hai.
-- Future me logic add kar sakte ho without breaking code
-- Public fields me control nahi hota

4. Interview
-- Properties in C# provide controlled access to class fields using get and set accessors.
-- They are better than public fields because they support validation, encapsulation, and allow logic to be added without changing the external interface.

## What is the difference between private and protected?
1. Analogy
-- Socho Family House
-- Private
    - Tumhara personal locker
    - Sirf tum access kar sakte ho
-- Protected 
    - Family locker
    - Tum bhi access kar sakte ho aur tumhare children bhi
-- Programming me:
    - Private → only same class
    - Protected → same class + derived class



## What is data hiding and how does encapsulation achieve it?
1. Analogy
-- Socho Car Engine
-- Driver kya control karta hai ?
    - Accelerator
    - Brake
    - Steering
-- Lekin driver engine ke internal parts directly access nahi karta.
-- Car manufacturer internal engine parts hide karta hai aur sirf controls expose karta hai.
-- Yahi Data Hiding Hai.

2. Technical
-- Data Hiding : 👉 Object ke internal data ko direct access se hide karna
-- Encapsulation : 
    👉 Data + methods ko class me bundle karke
    👉 Access modifiers (private, protected, etc.) se data hide karna
-- Yani : Encapsulation -> Data hiding achieve karta hai.

3. Code
    class Patient
    {
        // Data Hidden — direct access band! 🔒
        private string _bloodReport   = "B+";
        private string _medicalHistory = "Diabetic";

        // Sirf authorized method se milega
        public string GetReport(string role)
        {
            if (role == "Doctor")
                return $"Report: {_bloodReport}, History: {_medicalHistory}";

            return "❌ Access Denied!";
        }
    }

    // Usage
    Patient p = new Patient();

    // p._bloodReport = "A+"; // ❌ Direct access — blocked!

    Console.WriteLine(p.GetReport("Doctor"));      
    // ✅ Report: B+, History: Diabetic

    Console.WriteLine(p.GetReport("Receptionist")); 
    // ❌ Access Denied!

4. Interview 
-- Data hiding means restricting direct access to the internal data of a class. Encapsulation achieves this by using access modifiers and exposing controlled access through methods or properties.

## What are auto-implemented properties?
1. Techical
-- Jab sirf data store karna ho — koi validation, koi logic nahi
-- C# automatically private field bana deta hai andar — tumhe nahi likhna
-- Short aur clean syntax
    Normal Property:          Auto Property:
    ━━━━━━━━━━━━━━━━━━━━━━━   ━━━━━━━━━━━━━━━━━━
    private string _name;     
    public string Name        public string Name
    {                         { get; set; }
    get { return _name; }  
    set { _name = value; } 
    }

2. Code
    class Product
    {
        // Auto Properties — clean & simple ✅
        public string Name     { get; set; }
        public double Price    { get; set; }
        public string Category { get; set; }

        // Read-Only Auto Property
        public string ProductId { get; private set; }

        // Default Value bhi de sakte ho!
        public bool InStock { get; set; } = true;

        public Product(string id)
        {
            ProductId = id;  // Sirf constructor set kare
        }
    }

    // Usage
    Product p = new Product("P001");
    p.Name     = "Laptop";
    p.Price    = 75000;
    p.Category = "Electronics";

    // p.ProductId = "P002"; // ❌ private set — blocked!

    Console.WriteLine($"{p.ProductId} | {p.Name} | ₹{p.Price} | Stock: {p.InStock}");
    // Output: P001 | Laptop | ₹75000 | Stock: True



## What is the difference between a read-only property and a constant?
1. Analogy
-- Socho Company ID Card System
-- Constant 
    - Company ka Country Code = "IN"
    - Ye kabhi change nahi hota
-- Read-Only
    - Employee ka Joining Date
    - Ye object create hone par set hota hai.
    - Baad me change nahi hota.

2. Technical
-- Read-Only Property
    - Value object creation ke time set hoti hai
    - Baad me Change nahi hoti
    - Usually Constructor me assign hoti hai.
-- Constant
    - Compile Time constant hota hai
    - Value compile time par fixed hoti hai
    - Runtime me change nahi ho sakti

3. Ream World Example
-- Trading System me 
-- Const Example 
    - Exchange name
    - Tax percentage
    - Fixed config values
-- ReadOnly Example
    - OrderId
    - Created Time
    - Ye kabhi change nahi hota

4. Code
    class AppConfig
    {
        // CONST — Compile time, har jagah same
        public const double PI          = 3.14159;
        public const string AppName     = "MyApp";

        // READONLY — Runtime pe set, constructor mein
        public readonly string AppVersion;
        public readonly DateTime StartTime;

        public AppConfig(string version)
        {
            AppVersion = version;           // ✅ Constructor mein set
            StartTime  = DateTime.Now;      // ✅ Runtime value!
        }
    }

    // Usage
    AppConfig config = new AppConfig("2.0.1");

    Console.WriteLine(AppConfig.PI);          // 3.14159 — Class se access
    Console.WriteLine(AppConfig.AppName);     // MyApp
    Console.WriteLine(config.AppVersion);     // 2.0.1
    Console.WriteLine(config.StartTime);      // Current time

    // config.AppVersion = "3.0"; // ❌ readonly — blocked!
    // AppConfig.PI = 3.0;        // ❌ const — blocked!

5. Important Points
    const  → DateTime.Now nahi de sakte    ❌
            Sirf primitive types          ⚠️
            Implicitly static — object    
            ki zaroorat nahi              ✅

    readonly → Koi bhi type de sakte hain  ✅
            Har object ka alag value    
            ho sakta hai                ✅
            Constructor mein logic      
            likh sakte hain             ✅
 
## What is the readonly keyword vs const in C#?
-> const compile time pe set hota hai — sirf primitive types ke liye, implicitly static hota hai aur kabhi change nahi ho sakta. 
-> readonly runtime pe set hota hai — constructor mein — aur koi bhi type ho sakti hai.
-> Jab value compile time pe pata ho jaise PI ya fixed strings toh const use karo. Jab runtime pe set karni ho jaise DateTime ya injected config toh readonly use karo."

# 🔷 SECTION 3 — Inheritance
## What is Inheritance and what problem does it solve?
1. Analogy
-- Socho Family inheritance
--Father ke paas kuch properties hain:
    - House
    - Land
    - Business
-- Children ye properties inherit kar lete hain.
-- Unhe phir se sab kuch create nahi karna padta.
-- Programming me bhi child class parent class ke features inherit karti hai.

2. Technical
-- Inheritance allow karta hai ek class ko dusri class ke properties aur methods inherit karne ke liye.
    - Parent Class -> Base / Super Class
    - Child Class -> Dervied Class
-- Syntex me ":" use hota ha

3. Code
    // Base Class — Common Code
    class Product
    {
        public string Name  { get; set; }
        public double Price { get; set; }

        public void ShowDetails()
        {
            Console.WriteLine($"Product : {Name}");
            Console.WriteLine($"Price   : ₹{Price}");
        }
    }

    // Child Class — Inherit + Extra
    class DigitalProduct : Product
    {
        public string DownloadUrl { get; set; }

        public void Download()
        {
            Console.WriteLine($"Downloading {Name} from {DownloadUrl}");
        }
    }

    // Child Class — Inherit + Extra
    class PhysicalProduct : Product
    {
        public double WeightKg { get; set; }

        public void Ship()
        {
            Console.WriteLine($"Shipping {Name} | Weight: {WeightKg}kg");
        }
    }

    // Usage
    DigitalProduct dp = new DigitalProduct();
    dp.Name        = "C# Course";       // ✅ Inherited
    dp.Price       = 999;               // ✅ Inherited
    dp.DownloadUrl = "udemy.com/csharp"; // ✅ Own
    dp.ShowDetails();                    // ✅ Inherited method
    dp.Download();                       // ✅ Own method

    Console.WriteLine("───────────────");

    PhysicalProduct pp = new PhysicalProduct();
    pp.Name     = "Laptop";   // ✅ Inherited
    pp.Price    = 75000;      // ✅ Inherited
    pp.WeightKg = 1.8;        // ✅ Own
    pp.ShowDetails();          // ✅ Inherited method
    pp.Ship();                 // ✅ Own method

    // Output:
    // Product : C# Course
    // Price   : ₹999
    // Downloading C# Course from udemy.com/csharp
    // ───────────────
    // Product : Laptop
    // Price   : ₹75000
    // Shipping Laptop | Weight: 1.8kg

4. Important Points
-- Code Reuse
-- Maintainability improve
-- Hierarchy Create hoti hai.
-- Polymorphism enable karta hai.


## What types of inheritance does C# support?
1. Analogy
-- Socho Family Tree
-- Different inheritance structures ho sakte hain:
    - Single → Father → Son
    - Multilevel → Grandfather → Father → Son
    - Hierarchical → Father → Multiple children
    - Multiple → Child ke multiple parents (real life me nahi hota 😄)

2. Technical
-- C# classes ke through ye inheritance types support karta hai:
    - Single Inheritance
    - MultiLevel Inheritance
    - Hierarchical Inheritance
--  ⚠️ Multiple inheritance classes ke through support nahi karta
Lekin interfaces ke through possible hai.

3. Type 
-- Single Inheritance : 
    - Ek child → ek parent
    - Code
        class Order
        {
        }

        class EquityOrder : Order
        {
        }
-- Multilevel Inheritance
    - Multilevel Inheritance
    - Code
        class Order
        {
        }

        class TradeOrder : Order
        {
        }

        class EquityTrade : TradeOrder
        {
        }
-- Hierarchical Inheritance
    - Ek parent -> multiple Children
    - Code                
        class Order
        {
        }

        class EquityOrder : Order
        {
        }

        class FNOOrder : Order
        {
        }

4. Important
-- C# single base class allow krta hai
-- Multiple inheritance interfaces se hota hai

## Why doesn't C# support multiple inheritance with classes?
1. Analogy
-- Socho ek child ke do teachers hain 👨‍🏫👩‍🏫
-- Dono teachers bolte hain:
    - Teacher A → “Homework method A use karo”
    - Teacher B → “Homework method B use karo”
-- Child confuse ho jayega kaunsa follow kare?
-- Programming me bhi same problem hoti hai.
-- Isko Diamond Problem bolte hain.

2. Technical
-- Multiple inheritance ka matlab hai:
-- Ek class multiple base classes inherit kare.
-- Example
    class A
    class B

    class C : A , B 
-- Problem : 
    - Method Ambiguity
    - Diamond problem
    - Complexity increase
-- Ek class multiple base classes inherit kare.

## What is the base keyword in C#?
1. Analogy (Real World)
-- Socho Father aur Son ka relationship
-- Father ke paas ek method hai: CalculateSalary()
-- Son ne bhi same method bana liya 
-- Ab agar son ko father ka original method call karna ho, to wo bolega:
    "Call my Father's version of the method"
-- Programming me ya kam base keyword karta hai.

2. Technical
-- base keyword use hota hai:
    - Base class constructor call karne ke liya
    - Base class methods access karne ke liye
    - Base class members access karne ke liye
-- Base class members access karne ke liye

3. Code
-- Base Method Call
    class Order
    {
        public virtual void Validate()
        {
            Console.WriteLine("Base validation");
        }
    }

    class EquityOrder : Order
    {
        public override void Validate()
        {
            base.Validate(); // base class method call
            Console.WriteLine("Equity validation");
        }
    }   
-- Base Constructor Call
    class Order
    {
        public Order(int id)
        {
            Console.WriteLine("Order Created");
        }
    }

    class EquityOrder : Order
    {
        public EquityOrder() : base(10)
        {
        }
    }

4. Important Points
-- base -> parent class ko refer karta hai
-- Base constructor call kar sakte hain
-- Base methods access kar sakte hain
-- Mostly inheritance + overriding me use hota hai

## What is constructor chaining using : this() and : base()?
1. Analogy
-- Socho Restaurant Kitchen 
-- this() = Same kitchen mein junior chef senior chef ko call karta hai — "Bhai tu already jaanta hai base recipe, tu bana, main extra topping add karta hoon!"
-- base() = Branch restaurant head office ki recipe follow karta hai — "Head office wali base recipe use karo, hum upar se customize karenge!"

2. Real World Coding Use Case 
-- this() → Different constructors mein code repeat na ho — ek main constructor sab handle kare
-- base() → AdminUser aur GuestUser — dono User ka base constructor call karein — common initialization ek jagah!

3. Code : ✅ this() — Same Class Chaining
        class User
        {
            public string Name;
            public string Email;
            public string Role;

            // Main Constructor — sab yahan handle hoga
            public User(string name, string email, string role)
            {
                Name  = name;
                Email = email;
                Role  = role;
                Console.WriteLine($"User bana: {Name} | {Role}");
            }

            // Chaining — this() se upar wala call hoga
            public User(string name, string email)
                : this(name, email, "Guest")  // Default role = Guest
            { }

            public User(string name)
                : this(name, "unknown@email.com")  // Default email
            { }
        }

        // Usage
        User u1 = new User("Rahul", "rahul@gmail.com", "Admin");
        User u2 = new User("Priya", "priya@gmail.com");
        User u3 = new User("Amit");

        // Output:
        // User bana: Rahul | Admin
        // User bana: Priya | Guest   ← Default role
        // User bana: Amit  | Guest   ← Default email + role

4. Code : ✅ base() — Parent Constructor Call
        class User
        {
            public string Name;
            public string Email;

            public User(string name, string email)
            {
                Name  = name;
                Email = email;
                Console.WriteLine($"User init: {Name}");
            }
        }

        class AdminUser : User
        {
            public string AdminCode;

            // base() se parent constructor call kiya
            public AdminUser(string name, string email, string code)
                : base(name, email)  // ← Parent ka constructor!
            {
                AdminCode = code;
                Console.WriteLine($"Admin init: {AdminCode}");
            }
        }

        class GuestUser : User
        {
            public int SessionTimeout;

            public GuestUser(string name)
                : base(name, "guest@temp.com")  // ← Default email parent ko
            {
                SessionTimeout = 30;
                Console.WriteLine($"Guest init: Timeout={SessionTimeout}min");
            }
        }

        // Usage
        AdminUser admin = new AdminUser("Rahul", "rahul@gmail.com", "ADM001");
        Console.WriteLine("───────────────");
        GuestUser guest = new GuestUser("Amit");

        // Output:
        // User init : Rahul       ← base() se parent pehle chala
        // Admin init: ADM001      ← Phir child chala
        // ───────────────
        // User init : Amit        ← base() se parent pehle chala
        // Guest init: Timeout=30  ← Phir child chala

5. Important
    Order of Execution:
    ━━━━━━━━━━━━━━━━━━━━━━━━━━━━
    base() → Parent PEHLE chalta hai
        → Phir Child ka constructor

    this() → Chain mein jo last hai
        → Woh PEHLE chalta hai
        → Phir calling constructor

6. Interview
-- this() same class ke doosre constructor ko call karta hai — code duplication avoid karne ke liye. 
-- base() parent class ke constructor ko call karta hai — child class mein common initialization reuse karne ke liye.
-- Dono constructor signature ke saath : ke baad likhte hain
-- base() ke saath parent ka constructor hamesha pehle execute hota hai, phir child ka.

## What is method overriding in C#? What rules apply?
1. Analogy
-- Socho Vehicle ka example
-- Vehicle class me ek method hai: StartEngine()
-- Different vehicles usko apne tareeke se implement karte hain :
    - Car -> push button start
    - Bike -> self start
    - Truck -> heavy ignition
-- Sabka method name same hai, but behavior different.
-- Yahi Method Overriding hai.

2. Techincal
-- MEthod Overriding ka matlab hai:
-- Derived class base class ke virtual method ko redefine karti hai.
-- Keywords used:
    - virtual → base class method
    - override → derived class implementation
-- Runtime me derived class method execute hota hai.
-- Is Ko Runtime Polymorphism bolta ha

3. Code 
    class Order
    {
        public virtual void Validate()
        {
            Console.WriteLine("Base Order Validation");
        }
    }

    class EquityOrder : Order
    {
        public override void Validate()
        {
            Console.WriteLine("Equity Order Validation");
        }
    }
-- Usage :
    Order order = new EquityOrder();
    order.Validate();

4. Rules of Method Overriding
-- Base method virtual / abstract / override hona chahiye
-- Derived method override keyword use karega
-- Method name same hona chahiye
-- Return type same hona chahiye
-- Parameters same hone chahiye
-- Access modifier restrict nahi kar sakte.

5. Important
-- Runtime polymorphism achieve hota hai
-- Behivour Customize kar sakte hain
-- Mostly frameowrks aur extensible systems me use hota hai.

## What is the difference between virtual, override, and new keywords?
-- virtual : Base class method ko override karne ki permission deta hai
-- override : Derived class me base method ko redefine karta hai
-- new : Base class method ko hide karta hai.

-- Virtual + Override -> Runtime Polymorphism
-- new → method hiding
-- Override me same method replace hota hai
-- New me base method hide hota hai

## What is method hiding in C#?
1. Analogy
-- Socho Company Announcement System
-- CEO bolta hai : "Office timing 9 AM hai".
-- Ek department manager apna rule banata hai : "Hamare department ka timing 10 AM hai."
-- Manager ne CEO rule ko Modify nahi kiya.
-- balki apna naya rule bana diya jo CEO rule ko hide karta hai
-- Programming me isko Method Hiding bolte hain.

2. Technical
-- Method Hiding tab hota hai jab derived class same name ka method define karti hai using new keyword.
-- Isme :
    - Base method override nahi hota.
    - Base method hide ho jata hai.
-- Polymorphism apply nahi hota.

3. Code :
    class Order
    {
        public void Calculate()
        {
            Console.WriteLine("Base Calculation");
        }
    }

    class EquityOrder : Order
    {
        public new void Calculate()
        {
            Console.WriteLine("Equity Calculation");
        }
    }    
-- Usage:
    Order order = new EquityOrder();
    order.Calculate();
-- Output : Base Calculation

4. Important Points
-- new keyword use hota hai.
-- Base method hide hota hai.
-- Runtime polymorphism nahi hota
-- Method call reference type par depend karta hai

## Can we override a static method in C#?
1. Analogy
-- Socho Company Notice Board
-- Company ek general rule notice board par laga deti hai: "Office Closes at 6 PM"
-- Ye company level rule hai , kisi specific employee ka nahi.
-- Agar koi department bole: "Hum is rule ko override kar denge."
-- Wo Possible nahi hai , kyunki rule individual employee se linked nahi hai,
-- wo company level rule hai.
-- Static methods bhi class level par hote hain, object level par nahi.
-- Isliya override nahi ho sakte,,

2. Technical
-- Static methods : 
    - class se belong karte hain
    - Object se nahi
    - Polymorphism instance methods par kaam karta hai
-- Isliya : ❌ Static method override nahi ho sakta
-- Lekin : ✔ Static method hide kiya ja sakta hai using new

3. Code
-- Static Method Hiding
    class Order
    {
        public static void Show()
        {
            Console.WriteLine("Base Static Method");
        }
    }

    class EquityOrder : Order
    {
        public new static void Show()
        {
            Console.WriteLine("Derived Static Method");
        }
    }
-- Usage 
    Order.Show();
    EquityOrder.Show();

4. Important Points
-- Static methods override nahi ho sakte
-- Kyunki runtime polymorphism object par depend karta hai
-- Static methods compile time binding use karte hain
-- Sirf method hiding (new) possible hai

## What is the difference between IS-A and HAS-A relationships?
1. Analogy
-- IS-A Relationship
    - Socho 
        * Dog is a Animal
        * Car is a Vehicle
    - Yani Dog = Animal ka Type hai.
-- HAS - A Relationship
    - Socho 
        * Car has an Engine
        * Computer has a CPU
    - Uani object ke andar ek aur object hota hai.

2. Real World Coding Use Case
-- Trading System me
-- IS-A
    * EquityOrder is a Order
    * FNOOrder is a Order
    - Derived order types base order ko inherit karte hain
-- HAS-A
    * EquityOrder is a Order
    * FNOOrder is a Order
    - Order class ke andar helper components use hote hain.

3. Visulization
-- IS-A (Inheritance)
            Order
            |
        -------------
        |           |
    EquityOrder   FNOOrder
    - Child class parent class ka type hoti hai.
-- HAS-A (Composition)
            Order
            /     \
    RiskManager  MarginCalculator
    - Order ke paas other objects hote hain.

4. Technical
-- IS-A
    - Implemented using Inheritance
    - Derived class base class ka subtype hoti hai
    - Example 
        class EquityOrder : Order
        {
        }
-- HAS-A
    - Implemented using Composition / Aggregation
    - Class another class ka object hold karti hai.
    - Example : 
        class EquityOrder : Order
        {   
        }

5. Important Points
| Relationship | Implementation | Meaning                        |
| ------------ | -------------- | ------------------------------ |
| IS-A         | Inheritance    | Child is a type of parent      |
| HAS-A        | Composition    | Object contains another object |
-- Best Practice : Prefer composition over inheritance in many designs

## What is the sealed keyword? When would you use it?
1. Analogy 
-- Socho Government Official Document
-- Document par likha hai:
    FINAL VERSION – No modifications allowed
-- Matlab : Iske baad koi changes ya extensions allowed nahi hain
-- Programming me bhi sealed class ka matlab hai:
➡️ Is class ko inherit nahi kiya ja sakta.

2. The sealed keyword in C# is used to prevent a class from being inherited. It is typically used when we want to restrict extension of a class or protect critical logic from being overridden.

# 🔷 SECTION 4 — Polymorphism
## What is Polymorphism and what are its types?
1. Analogy
-- Socho Paymet System
-- Same Action : Pay()
-- But Different implementation :
    - Credit Card -> card payment
    - UPI -> UPI payment
    - NetBanking -> bank payment
-- Same method name -> Different behaviour

2. Technical
-- Polymorphism = one interface, many implementations
-- Types
    - Compile time polymorphism
    - Runtime Polymorphism
 
## What is compile-time polymorphism in C#? (Method Overloading)
1. Analogy
-- Restaurant order system 🍽️
    Order()
    Order(string food)
    Order(string food , int Qty)
-- Same method name -> different parameters

2. Techincal
-- Same method name
-- Different parameters
-- Decidsion compile time par hota hai.

3. Interview
-- Compile-time polymorphism is achieved using method overloading where multiple methods have the same name but different parameters, and the compiler decides which method to call

## What is runtime polymorphism in C#? (Method Overriding)
1. Analogy
-- Vehicle example StartEngine()
-- Different Behaviour
    - Car 
    - Bus 
    - Bike

2. Interview
Runtime polymorphism is achieved through method overriding where the method call is resolved at runtime based on the object type.


## What is dynamic method dispatch in C#?
1. Analogy
-- Socho Customer Support Call Center 
-- Custmer Call Krta hai : Support()
-- But Call different department me route ho sakti hai :
    - Billing Support
    - Technical Support
    - Account Support
-- Call same hai, but runtime par decide hota hai kaunsa department handle karega.
-- Programming me bhi same method call hota hai, but runtime decide karta hai kaunsa method execute hoga.

2. Trading Example
-- Base Order 
-- Method : HandleTranscation
-- Different Orders :
    - Normal
    - Bracket ,
    - SOR
-- System pe Order Aya ...
-- Runtime pe Decide hua kon sa Wala HandleTranscation pe Bheja

3. Techincal
-- Dynamic Method Dispatch ek mechanism hai jisme :
    - Base Class Reference
    - Dervied Class Object.
-- use hota hai.
-- Aur overridden method runtime me resolve hota hai.
-- Ye method overriding + Polymorphism ka part hai.

4. Important Points
-- Base class reference -> Dervied Object
-- Works with virtual + override
-- Method selection runtime par hota hai
-- Part of runtime polymorphism

5. Interview
Dynamic method dispatch is the process where a method call is resolved at runtime instead of compile time. It occurs when a base class reference points to a derived class object and the overridden method in the derived class is executed.

## What is operator overloading in C#?
1. Analogy
-- Socho + operator ➕
-- Normally : 5 + 3 = 8
-- But agar Money objects ho: ₹100 + ₹200 = ₹300
    - yaha + operation number ke liya nahi,
    - balki custom object ke liya behave kar raha hai.
    - Yahi Opeartion Overloading ha,

2. Technical
-- Operator Oveloading allow karta hai ki build-in operators ko custom types ke saath redefine karein
-- Common overloadable operators: + - * / == != < > <= >=
-- Important Rule : Operator method static hota hai.

3. Code (Important)
    class Money
    {
        public int Amount;

        public static Money operator +(Money a, Money b)
        {
            return new Money
            {
                Amount = a.Amount + b.Amount
            };
        }
    }
-- Usage
    Money m1 = new Money { Amount = 100 };
    Money m2 = new Money { Amount = 200 };
    Money m3 = m1 + m2;
-- Output : 300

4. Important Points
-- Opeartors Static methods se overload hote hain
-- Custom objects ke saath natural syntax milta hai.
-- Readibility improve hoti hai.

## What is covariant return type?
1. Analogy
-- Socho Vechile Factory
-- Factory method: CreateVehicle()
-- Base Factory bolti hai : Vehicle create karo
-- But CarFactory Bol sakti ha : Car create Karo
-- Car → Vehicle ka subtype hai.
-- Yani same method but more specific return type.
-- Yahi Covariant Return Type hai.

2. Technical
-- Covariant return type allow karta hai ki:
-- Derived class overridden method me base return type ka derived type return kare.
-- Ye feature C# 9 se introduce hua.

3. Code 
    class EquityOrder : Order { }

    class OrderFactory
    {
        public virtual Order CreateOrder()
        {
            return new Order();
        }
    }

    class EquityOrderFactory : OrderFactory
    {
        public override EquityOrder CreateOrder()
        {
            return new EquityOrder();
        }
    }

4. Important Points
-- Introduced In C# 9
-- Only works with method overriding
-- Derived method more specific return type use kar sakta hai     

## What is the dynamic keyword in C#? How does it relate to polymorphism?
1. Real World Use Case
-- COM objects
-- Reflaection
-- JSON dynamic data

2. Visulization
    dynamic obj

    Compile time → no type check
    Runtime → method resolution

3. Interview
The dynamic keyword bypasses compile-time type checking and resolves method calls at runtime.

## What is the difference between early binding and late binding?
| Feature     | Early Binding      | Late Binding      |
| ----------- | ------------------ | ----------------- |
| Decision    | Compile time       | Runtime           |
| Performance | Faster             | Slower            |
| Example     | Method overloading | Method overriding |
| Type safety | High               | Less              |

# 🔷 SECTION 5 — Abstraction
## What is Abstraction? 
1. Analogy
-- Socho Car Driving
-- Driver kya use karta hai ?
    - Steering
    - Accelerator
    - Brake
-- Driver ko engine ka internal mechanism nahi pata hota.
-- Driver sirf interface use karta hai, internal complexity hidden hoti hai.
-- Yahi Abstraction

2. Technical
-- Abstraction ka matlab hai:
    - Implementation hide karna
    - Sirf essential functionality expose karna
-- C# me abstraction achieve hota hai :
    - Abstract classes
    - Interfaces

3. Code
    abstract class Order
    {
        public abstract void Execute();
    }

    class EquityOrder : Order
    {
        public override void Execute()
        {
            Console.WriteLine("Equity Order Execution");
        }
    }

4. Important Points
-- Complexity hide karta hai
-- System simplify karta hai
-- Mostly interfaces / abstract classes se implement hota hai.

5. Interview
-- Abstraction means hiding complex implementation details and exposing onlt the necessary funcationality to user.

## How is it different from Encapsulation? Differece between Abstraction and Encapsulation
1. Analogy
-- Encapsulation : 
    - Data protection hai.
    - Example : ATM Machine (Deposit() , Withdraw())
-- Abstraction
    - Internal engine Details Hidden
    - Example : Car Driving (Drive() , Brake())
2. Visualization
    Encapsulation
    
    Data + Methods
    inside class
    Data Hidden
    

    Abstraction
        Expose only
    essential features
    Hide complexity
    

3. Technical Difference
| Feature        | Abstraction                | Encapsulation    |
| -------------- | -------------------------- | ---------------- |
| Focus          | Hide complexity            | Hide data        |
| Implementation | Abstract class / Interface | Access modifiers |
| Goal           | Simplify usage             | Protect data     |

4. Interview
-- Abstraction hides complex implementation and exposes only essential functionality, while encapsulation hides data and restricts direct access using access modifiers.

## What is an Abstract Class in C#? Can it have a constructor?
1. Analogy
-- Socho Vehicle Template
-- Ek Company bolti hai : Vechile must have Start() And Stop()
-- But company direct Vehicle create nahi karti.
-- Wo banati hai :  
    - Car 
    - Bike
    - Truck
-- Vehicle sirf template hai , actual object derived classes banati hain.
-- ye Hi Abstract Class ka Idea Hai.

2. Technical
-- abstract keyword se declare hoti hai
-- Object create nahi kar sakte
-- Abstract methods ho sakte hain
-- Normal methods bhi ho sakte hain

3. Code 
    abstract class Order
    {
        public int OrderId;

        public abstract void Execute();
    }

    class EquityOrder : Order
    {
        public override void Execute()
        {
            Console.WriteLine("Equity order executed");
        }
    }

4. Can an Abstract Class have a Constructor?
-- Yes , Abstract class constructor ho sakta hai
-- Direct object create nahi hota.

5. Important Points
-- Abstract class object create nahi kar sakte
-- Constructor allowed hota hai
-- Constructor derived class initialization ke liye use hota hai

6. Interview
An abstract class in C# is a class that cannot be instantiated and is used as a base class for other classes. It can contain abstract methods as well as normal methods. Yes, an abstract class can have a constructor, which is called when a derived class object is created.

## What is an Interface in C#? How is it different from an Abstract Class?
1. Analogy
-- Socho Electric Plug Standard
-- Plug board bolta hai : Devices must implement these pins
-- But wo ye nahi batata device internally kaise kaam karega.
-- Device Ho Sakte Hain :
    - Mobile charger
    - Laptop Charger
    - TV
-- Sab same interface follow karte hain , but implementation different hota hai.
-- Ye hi Interface Concept Hai.

2. Techincal
-- Contract define karta hai.
-- Methods implementation nahi hoti
-- Classes implement karti hain
-- Keyword : interface

3. Code (Important)
    interface IPayment
    {
        void ProcessPayment();
    }

    class UpiPayment : IPayment
    {
        public void ProcessPayment()
        {
            Console.WriteLine("UPI Payment");
        }
    }

4. Important 
-- Interface contract hota hai.
-- Multiple classes implement kar sakti hain
-- Implemenatinons Class provide karti hai.

5. Interview 
An interface in C# defines a contract that classes must implement. It contains method declarations without implementation, and implementing classes provide the actual behavior.

## Can an Interface have a constructor in C#?
-- No 
-- Bcoz It has Onlt method defination not implementaion
-- Also No Property.

## Differece Between Interface And Abstract Class?
1. Analogy
-- Abstract Class
    - Car template
    - Example : Vehicle , Vehicle_Handler() , Start() , Stop()
    - Some behavior already defined hota hai.
-- Interface
    - Plug Standard
    - Example : Connect() , Disconnect()
    - Sirf rules define karta hai, implementation nahi.

2. Visulization
-- Abstract Class 
    - Some method Define
    - Some abstract methods
    - Inheritance based
-- Interface
    - Only contract
    - No Implementation

3. Difference
| Feature              | Abstract Class         | Interface       |
| -------------------- | ---------------------- | --------------- |
| Purpose              | Partial implementation | Contract        |
| Methods              | Abstract + normal      | Mostly abstract |
| Fields               | Allowed                | Not allowed     |
| Constructors         | Allowed                | Not allowed     |
| Multiple inheritance | ❌ No                   | ✔ Yes         |

4. Interview
An abstract class can contain both implemented and abstract methods and is used for base class behavior, while an interface defines a contract that implementing classes must follow and supports multiple inheritance.


## What are default interface methods in C# 8+?
1. Analogy
-- Socho Company Policy Document
-- Company bolti hai : Every department must implement LeavePolicy()
-- But Company Ek Default rule bhi likh deti hai : Default LeavePolicy -> 10 Days Leave
-- Agar department apna rule define nahi karta,
-- to default rule apply ho jayega.
-- Programming me bhi Same concept Hai.

2. Technical
-- C# 8 se interfaces default method implementation allow karte hain.
-- Isse : 
    - Interface me Method Body likh Sakte hain
    - Classes Optional override kar sakti hain
-- Goal : Backward Compatibility

3. Code
    interface IValidator
    {
        void Validate();

        void Log()
        {
            Console.WriteLine("Default logging");
        }
    }
-- Implementation
    interface IValidator
    {
        void Validate();

        void Log()
        {
            Console.WriteLine("Default logging");
        }
    }
-- Usage 
    IValidator validator = new OrderValidator();
    validator.Log();
-- Output : Default Logging.

4. Important Points
-- Introduced in C# 8
-- Interface method body allow karta hai.
-- Classes override kar sakti hain.
-- Usefull for API evolution without breaking existing Code.

5. Interview
Default interface methods were introduced in C# 8 and allow interfaces to contain method implementations. This helps add new methods to interfaces without breaking existing implementations.

## What is an explicit interface implementation?
1. Analogy
-- Socho ek Employee hai jo 2 departments me kaam karta hai
    - HR Department
    - Finance Deparment
-- Dono department bolte hain : SubmitReport()
-- Employee dono reports banata hai, lekin:
    - HR Ke Liya HR Report
    - Finance ke liye Finance Report
-- Employee decide karta hai : 
    - Agar HR system se call aaye → HR report
    - Agar Finance system se Call aaye -> Finance Report
-- Programming me bhi isi ko Explicit Interface Impleentation bolte hain.

2. Code
    interface IOrderValidator
    {
        void Validate();
    }

    interface IRiskValidator
    {
        void Validate();
    }

    class OrderValidator : IOrderValidator, IRiskValidator
    {
        void IOrderValidator.Validate()
        {
            Console.WriteLine("Order validation");
        }

        void IRiskValidator.Validate()
        {
            Console.WriteLine("Risk validation");
        }
    }
-- Usage
    interface IOrderValidator
    {
        void Validate();
    }

    interface IRiskValidator
    {
        void Validate();
    }

    class OrderValidator : IOrderValidator, IRiskValidator
    {
        void IOrderValidator.Validate()
        {
            Console.WriteLine("Order validation");
        }

        void IRiskValidator.Validate()
        {
            Console.WriteLine("Risk validation");
        }
    }
-- Output : 
    Order validation
    Risk validation

3. Important
-- Interface method class object se directly call nahi hota
-- Interface reference required hota hai
-- Mostly use hota hai jab multiple interfaces me same method ho

4. Interview
Explicit interface implementation is used when a class implements multiple interfaces that have methods with the same name. The method is implemented using the interface name and can only be accessed through the interface reference.

## When would you use an Abstract Class over an Interface and vice versa?
1. Abstract Class
-- High Level Structural Change in Engine
-- Example : Order Handlers
    - Multiple Diff Order Like SOR , Bracket , Normal
    - All need to have their own Order Handler
    - Handler Enable or Disbale For Client For all Handler is Common

2. Interface 
-- Feature Addition in Code
-- Example : Exisitng 4 Interface imlemention , But for branch Adding One More.

## What is a Marker Interface?
1. Analogy
-- Socho Airport Security Tag
-- Airport par luggage par kabhi ek special tag lagaya jata hai : FRAGILE
-- Is tag ka koi behaviour nahi hota.
-- But system Ko pata Chal jata hai : Handle carefully
-- Programming me bhi market interface ek tag jaisa hota hai.

2. Visualization
           ILoggable
           (marker)
               |
        -----------------
        |               |
      Order          Trade
-- Market interface sirf identify karta hai.

3. Technical
-- Marker Interface
    - Empty interface hota hai
    - Koi methods nahi hote
    - Class ko mark karne ke liye use hota hai.
-- System runtime par check karta hai : object is MarkerInferface


# 🔷 SECTION 6 — Advanced OOP
## What is Composition vs Aggregation vs Association?
1. Analogy
-- Socho University System
-- Association : 
    - Teacher teaches Student
    - Teacher aur Student independent exist kar sakte hain.
-- Aggregation
    - Department has Teachers
    - Department delete ho jaye tab bhi Teachers exist kar sakte hain.
-- Composition
    - House has Rooms
    - Agar house destroy ho gaya -> rooms bhi destroy ho jayenge.

2. Association
    -- Real World Cding Use Case
        - Trader -> places -> Order
        - Trader aur Order independent entities hain.
    -- Techincal
        - Simple relationship between classes
        - No Ownership
        - Objects independent hota hai.
    -- Code
        class Trader
        {
            public void PlaceOrder(Order order) { }
        }
    -- Interview
        "Association represents a relationship between two independent objects where one object can use or interact with another."

3. Aggrehation
    -- Real World Coding Use Case
        - Portfolio has Orders
        - Portolio delete ho jaye to orders still exist kar sakte hain
    -- Techincal
        - HAS-A relationship
        - Weak ownership
        - Child Object independent exisit kar sakta hai.
    -- Code
        class Portfolio
        {
            public List<Order> Orders;
        }
    -- Interview
        "Aggregation is a weak “has-a” relationship where one object contains another but both objects can exist independently."

4.  Composition
    -- Real World Coding Use Case
        -- Order has Orderitem
        -- Agar Order Hi Delete ho gya , tho OrderItems bi delete ho jayega
    -- Techincal
        - Strong HAS-A relationship
        - Child object parent par depond karta hai,
        - Lifecycle tied hota hai.
    -- Code
        class Order
        {
            private List<OrderItem> items = new List<OrderItem>();
        }

5. Final Difference
Relationship	Ownership	        Lifecycle
................................................
Association	    No ownership	    Independent
Aggregation	    Weak ownership	    Independent
Composition	    Strong ownership	Dependent

## What is Dependency Injection in C#?
1. Analogy
-- Socho Restaurant Kitchen
-- Chef ko ingredients chahiye :
    - Tomato
    - Onion
    - Spices
-- Chef khud market jaake sab create nahi karta.
-- Instead :  Supplier ingredients proivde karta hai.
-- Chef sirf use karta hai.
-- Programming me bhi class ko jo objects chahiye hote hain wo bahar se diye jate hain.
-- Ye hi Dependency Injection (DI) hai.

2. Real World Coding Use Case
-- Trading system me OrderService hai.
-- OrderService ko RiskManager chahiye.
-- Bad design : OrderService khud RiskManager create kare
-- Good Design : RiskManager bahar se inject ho
-- ISse :
    - testing easy
    - loose coupling
    - flexibe Design

3. Technical
-- Dependency Injection , Ek Design Pattern hai Jisme 
-- Class apni dependencies khud create nahi karti .
-- Instead : External System dependecies provide karta hai.
-- Usually used in IoC Container
-- Example : ASP.NET Core DI container

4. Code
-- Interface
    interface IRiskManager
    {
        void CheckRisk();
    }
-- Implementation 
    class RiskManager : IRiskManager
    {
        public void CheckRisk()
        {
            Console.WriteLine("Risk checked");
        }
    }   
-- Service
    class OrderService
    {
        private IRiskManager riskManager;

        public OrderService(IRiskManager riskManager)
        {
            this.riskManager = riskManager;
        }
    }
-- Injection
    IRiskManager risk = new RiskManager();
    OrderService service = new OrderService(risk);

5. Important Points
-- Loose Coupling
-- Testable Code
-- Easy maintenance
-- Framework friendly

6. Types : 
-- Constructor Injection
-- Property Injection
-- Method Injection

7. Interview
Dependency Injection is a design pattern where a class receives its dependencies from an external source rather than creating them itself, helping achieve loose coupling and better testability.

## What is the difference between shallow copy and deep copy?
1. Analogy
-- Shallow Copy
    - Tum sirf folder ka duplicate bana dete ho,
    - But andar ke documents same reference se linked retha hain
    - Agar document change karo -> dono folders me change dikhega.
-- Deep Copy
    - Tum folder bhi copy karte ho aur andar ke documents bhi.
    - Ab agar ek document change karo → dusre folder par koi effect nahi.

2. Interview
"A shallow copy creates a new object but copies references of nested objects, so both objects share the same references. A deep copy creates a completely independent copy where both the object and its referenced objects are duplicated."


## What is ICloneable in C#?
1. Analogy
-- Socho Document Xerox Machine 🖨️
-- Tum ek document machine me dete ho: "Original Document"
-- Machine Kya karti hai : "Clone (duplicate) create kar deti hai"
-- Ab Tumhare pass : " Original + Copy "
-- Programming me bhi object ka duplicate banana hota hai,
-- Ye concept ICloneable interface provide karta hai.

2. Techincal
-- Build In Interface hai 
-- Allow Krta ha  : "object Cloning"
-- Is me Ek method hota ha : "Clone()"
-- Signature : "object Clone()"
-- Ye method current object ki copy return karta hai.

3. Important 
-- ICloneable object cloning ke liye use hota hai
-- Method: Clone()
-- Return type: object
-- Usually use Karta hai : MemberwiseClone()
-- Important : 
    - ICloneable specify nahi karta clone shallow ha ya deep
    -- Isliye medern .NET me custom clone methods prefer kiya jate hain

4. Interview
-- ICloneable is an interface in C# that allows an object to create a copy of itself 
-- using the Clone() method. 
-- However, it does not specify whether the cloning is shallow or deep.

## What are immutable objects? How do you create one in C#?
1. Analogy
-- Socho Aadhaar Card Number
-- Jab Aadhaar number generates ho gaya : 1234 5678 9012
-- Uske baad wo kabhi change nahi hota.
-- Agar kisi ko update karna hai to naya record create hota hai, purana modify nahi hota.
-- Programming me bhi isi concept ko Immutable Object bolte hain.

2. Technical
-- Ek object jiska state creation ke baad change nahi ho sakta.
-- Characteristics
    - Fields readonly
    - No setters
    - Values constructor se set hoti hain
-- Example : 
    - string
    - Datetime
    - Tuple

3. Important
-- Immutable Objects usefull for : 
    - Thread safety
    - Functional programming
    - Safe caching
    - Parallel Systems

4. Interview
-- Immutable objects are objects whose state cannot be changed after creation. 
-- In C#, they are typically created by using readonly fields or properties with only getters and initializing them through constructors.


## What is a Singleton class? How is it implemented thread-safely in C#?
1. Analogy
-- Socho Traffic Signal Controller
-- City me sirf ek cntral controller hota hai jo signals manage karta hai.
-- Agar multiple controllers ho gaye:
    - Signal A -> Green
    - Signal B -> Red
-- Traffic system confuse ho jayega
-- Isliye ruule : Only ONE controller allowed
-- Programming me bhi Singleton pattern ka rule hai : 
    Class ka sirf ek hi object hona chahiya.

2. Techincal 
-- Ensure krta ha class ka sirf ek hi object reha
-- Implementation steps
    - Constructor private
    - Static instance variable
    - Static method/property to get instance

3. Code
-- Basic Singleton Code
    class Logger
    {
        private static Logger instance;

        private Logger()
        {
        }

        public static Logger GetInstance()
        {
            if (instance == null)
            {
                instance = new Logger();
            }
            return instance;
        }
    }
    - Probleam  : Thread Safe Nahi Ha
.............
-- Thread Safe Singleton in C#
    - Visulization
        Thread1 -> create Instance
        Thread2 -< Wait
        Only ONE instance
    - Code
        class Logger
        {
            private static Logger instance;
            private static readonly object lockObj = new object();

            private Logger()
            {
            }

            public static Logger GetInstance()
            {
                lock (lockObj)
                {
                    if (instance == null)
                    {
                        instance = new Logger();
                    }
                }
                return instance;
            }
        }    

4. Interview
-- A Singleton class ensures that only one instance of a class exists and provides a global access point to it.
-- In C#, it is implemented using a private constructor and a static instance. Thread safety can be achieved using locking or the Lazy<T> approach.

## What is the difference between == and .Equals() in C#?
1. Analogy
-- Socho 2 Aadhar Cards
    - Card A 
        Name : Amit
        Number : 1234
    - Card B 
        Name : Amit
        Number : 1234
-- == comparison 
    - Check Karta ha : Kya dono cards SAME physical card hain (Object Memory)?
-- .Equals() comparison 
    - Check Karta ha : Kya dono cards ki information same hai (Object Data)?

2. Techincal
-- "==" Reference Comparison , .Equals() Value Comparison
-- "==" OverLoad Possible , .Equals() Overload Possible
-- "==" Used For Reference Comaprison , .Equals() Used For Logical Equality

3. Interview  
-- In C#, the == operator checks reference equality by default, while .Equals() checks logical equality. However, both behaviors can be customized by overriding them in a class.

## What is GetHashCode() and why must it be consistent with Equals()?
1. Analogy
-- Socho Library System
-- Har book ka ek unique shelf number hota hai:
    Shelf → 102
    Shelf → 205
    Shelf → 310
-- Library ko poori book scan karne ki zarurat nahi hoti.
-- Wo pehle shelf number (hash) check karta hai.
-- Programming me bhi objects ko fast lookup ke liye hash code diya jata hai.
-- Ye hi GetHashCode() ka kaam hai.

2. Techincal
-- GetHashCode() ek method hai Jo :
    - object ka integer hash code return karta hai.
-- Defined In  : System.Object
-- Use Hote hai : 
    - Dictionary
    - HashSet
    - HashTable

3. Code
    class Order
    {
        public int Id;

        public override int GetHashCode()
        {
            return Id.GetHashCode();
        }
    }

4. Why must GetHashCode() be consistent with Equals()?
-- Rule 
    - If two objects are equal → their hash codes must also be equal

5. Interview
-- GetHashCode() returns a hash value used for efficient lookup in hash-based collections like Dictionary and HashSet.
-- If Two objects are consider Equal Using Equals() ,They must return the same hash Code to Ensure behaviour in these collections.


## What are extension methods in C#?
1. Analogy
-- Socho SmartPhone App Store
-- Phone company ne basic features diye:
    Call
    SMS
    Camera
-- Baad me tum new apps install kar lete ho:
    WhatsApp
    Instagram
    Spotify
-- Phone change nahi hua, but new features add ho gaye.
-- Programming me bhi extension methods allow karte hain:
    - existing class ko modify kiye bina new methods add karna

2. Technical
-- Extension Method 
-- Allow Karta ha 
    - existing class me new method add karna
    - without modifying original class
-- Rules : 
    - Method static class me hota hai.
    - Method Static hota hai.
    - First parameter me this keyword use hota hai

3. Code : 
    public static class OrderExtensions
    {
        public static decimal CalculateValue(this Order order)
        {
            return order.Price * order.Qty;
        }
    }
-- Usage 
    - Order order = new Order { Qty = 10, Price = 100 };
    - decimal value = order.CalculateValue();

4. Usage
-- LINQ 
-- Helper utilities
-- Framework extensions
-- Example : 
    - list.Where()
    - list.Select()
    - list.First()

5. Interview
-- Extension methods allow developers to add new methods to an existing class without modifying its source code.
-- They are defined in a static class and use the this keyword in the first parameter to specify the type being extended.


## What are partial classes in C#?
-> Class Jo two Different cs file pe ho
-> Jis WinForms 

## What is object deconstruction in C#?
1. Analogy
-- Socho Lunch Box 🍱
-- Lunch box me multiple items hain:
    Rice
    Dal
    Salad
-- Normally tum pura lunch box use karte ho.
-- But agar tum bolo:
    Mujhe sirf Rice aur Dal chahiye
-- To tum box ko open karke items alag nikal lete ho.
-- Programming me bhi object ke values ko alag variables me extract karna ko deconstruction bolte hain.

2. Visulization
-- Before Deconstruction
    Order Object
    |
    ├── Id
    ├── Qty
    └── Price
-- After Deconstruction
    (Id , Qty , Price) = Order
-- Values separate Varibale me aa jati hain.

3. Techincal
-- Object Deconstruction
-- Allow karta hai : 
    - object properties ke tuple - style varibales me extract karna.
-- Ye work karta hai Deconstruct() method ke through.

4. Code
    class Order
    {
        public int Id;
        public int Qty;

        public void Deconstruct(out int id, out int qty)
        {
            id = Id;
            qty = Qty;
        }
    }

    Order order = new Order { Id = 1, Qty = 100 };

    var (id, qty) = order;

5. Inportant Points
-- Mostly Used With
    - Tuples
    - Records
    - Pattern matching
-- Example : var (x , y) = (10 , 20);

6. Interview 
-- Object deconstruction allows extracting values from an object into separate variables using a Deconstruct() method, making code cleaner and easier to read.

## What are records in C# 9+? How are they different from classes?
1. Analogy
-- Socho Student ID Card
-- Card par information hoti hai:
    Name
    RollNo
    Department
-- Agar 2 cards me same information ho, to hum bolte hain:
    Both represent the same student
-- Matlab value important hai, object identity nahi.
-- C# me records bhi value-based objects hote hain.

2. Techincal
-- Ek Refernce Type hai o Design ha immutable data models ke liye
-- Features
    - Value-Based Equality
    - Immutability
    - Build-in ToString()
    - Build-in Cloning

3. Code
-- Records : public record Order(int Id , int Qty)
-- Usage : 
    - var o1 = new Order(1, 100);
    - var o2 = new Order(1, 100);
    - Console.WriteLine(o1 == o2); // True

4. Difference In Record And Class
-- CLASS
    - Reference equality
    - Mutable By Default
-- RECORD 
    - Value Equality
    - Immutable By Default

5. Interview
-- Records in C# are reference types introduced in C# 9 designed for immutable data models.
-- Unlike classes, records use value-based equality instead of reference equality and provide built-in support for cloning and immutability. 

# More OOPs Questions....