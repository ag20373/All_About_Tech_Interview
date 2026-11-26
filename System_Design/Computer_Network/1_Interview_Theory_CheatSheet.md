# Basics

# Networking And Subnetting

## 1. What is IP Address ?
- IP Address (Internet Protocol Address) ek unique logical address hota hai jo Network mein connected kisi Device ke Network Interface ko identify karta hai.
- Jaise real world mein kisi ghar tak letter pahunchane ke liye uska address chahiye hota hai, waise hi Network mein ek Device se doosre Device tak data pahunchane ke liye IP Address ki zaroorat hoti hai.
- Example: Jab tum apne Laptop se Google open karte ho, toh tumhara Laptop aur Google ka Server IP Address ki help se ek doosre ke saath communicate karte hain.

## 2. What is IPv4 ?
- IPv4 ka full form Internet Protocol Version 4 hai.
- Ye 32-bit addressing system use karta hai, jisme total 4 parts (Octets) hote hain aur har part ko "." se separate kiya jata hai.
- Har Octet ki value 0 se 255 ke beech hoti hai.
- Example: 192.168.1.10
- IPv4 total 2^32 (approximately 4.3 billion) addresses support karta hai.
- Problem ye hai ki aaj ke time mein internet-connected devices ki quantity bahut zyada ho gayi hai, jiski wajah se IPv4 Addresses limited padne lage hain.
- Isi problem ko solve karne ke liye IPv6 introduce kiya gaya.

## 3. What is IPv6 ?
- IPv6 ka full form Internet Protocol Version 6 hai.
- Ye 128-bit addressing system use karta hai.
- IPv4 ki tarah 4 parts ke bajaye, IPv6 mein 8 groups hote hain aur har group hexadecimal format mein hota hai.
- Har group ko ":" se separate kiya jata hai.
- Example: 2001:0db8:85a3:0000:0000:8a2e:0370:7334
- IPv6 total 2^128 (approximately 3.4 x 10^38) unique addresses support karta hai.
- Itne saare addresses hone ki wajah se future mein IP Address ki shortage ka problem practically solve ho jata hai.
- IPv6 mein IPsec support available hai, lekin iska matlab ye nahi ki IPv6 automatically IPv4 se faster ya more secure hota hai.

## 4. Why IPv6 is Better Then IPv4 ?
- More IP Addresses: IPv4 sirf 4.3 billion addresses support karta hai, jabki IPv6 approximately 3.4 x 10^38 addresses support karta hai.
- No NAT Required in Normal Addressing: IPv6 mein itne saare addresses available hain ki har device ko globally unique IP Address diya ja sakta hai. Isliye IPv4 ki tarah NAT par depend karne ki zaroorat nahi hoti.
- Better Routing: IPv6 ka address structure aur network design routing ko more efficient banane mein help karta hai.
- Auto Configuration: IPv6 mein SLAAC (Stateless Address Autoconfiguration) ki help se devices automatically apna IP Address configure kar sakte hain.
- Better Multicast Support: IPv6 multicast ko support karta hai aur broadcast use nahi karta.
- Security: IPv6 mein IPsec support standardized hai, lekin actual security network configuration par depend karti hai.

## 5. What is a Public IP Addresses ?
- Public IP Address wo IP Address hota hai jo internet par globally routable hota hai.
- Humara Internet Service Provider (ISP), jaise Jio ya Airtel, humare internet connection ko Public IP Address provide karta hai.
- Isko ek Society ke Main Address ki tarah samajh sakte hain, jiske through bahar se koi bhi delivery society tak pahunch sakti hai.
- Jab hum internet par koi request bhejte hain, toh humara Router us request ko Public IP ke through internet par forward karta hai.
- Jab response wapas aata hai, toh Router NAT (Network Address Translation) ki help se response ko correct Private IP wale device tak pahunchata hai.
- Example:
	- Society -> Public IP Address (Internet par society ka common address).
	- Society Apartments -> Private IP Addresses (Society ke andar individual apartments ke addresses).

## 6. What is Private Ip Address ?
- Private IP Address wo IP Address hota hai jo humare Local Network ke andar devices ko identify karne ke liye use hota hai.
- Jaise Laptop, Mobile, Smart TV etc. ko Router ek Private IP Address assign karta hai.
- Ye IP Address globally routable nahi hota, matlab internet par ise directly access nahi kiya ja sakta.
- Jab koi device internet par request bhejta hai, toh Router NAT ki help se Private IP ko Public IP ke through communicate karwata hai.
- Example:
	- Society -> Public IP Address (Society ka common address).
	- Society Apartments -> Private IP Addresses (Har apartment ka individual address).
- Private IPv4 Address ki common ranges:
	- 10.0.0.0 - 10.255.255.255
	- 172.16.0.0 - 172.31.255.255
	- 192.168.0.0 - 192.168.255.255

## 7. What is Static IP Address ?
- Static IP Address wo IP Address hota hai jo manually configure kiya jata hai ya DHCP Reservation ke through fixed rakha jata hai.
- Iska address normally change nahi hota, jab tak Network Administrator ya ISP ise change na kare.
- Use Case:
	- High-End Servers: Bank ya Company ke Servers ko stable IP Address ki zaroorat hoti hai, taaki doosre systems consistently unhe access kar sakein.
	- Server Hosting: Agar hum koi Website ya Application host kar rahe hain, toh Static Public IP se users consistently us Server tak pahunch sakte hain.
	- Network Devices: Printers, Routers aur doosre important Network Devices ke liye bhi Static IP use kiya ja sakta hai.

## 8. What is Dynamic Ip Address ?
- Dynamic IP Address wo IP Address hota hai jo automatically assign hota hai aur time ke saath change ho sakta hai.
- Is IP Address ko assign karne ka kaam DHCP (Dynamic Host Configuration Protocol) karta hai.
- Example:
	- Jab tum apne Laptop ko Wi-Fi se connect karte ho, toh Router DHCP ki help se tumhare Laptop ko ek Private IP Address assign karta hai.
	- Kuch time baad DHCP Lease expire ya renew hone par same ya different IP Address mil sakta hai.
- Use Case:
	- Humare ghar ke Wi-Fi, Mobile aur Laptop mein generally Dynamic IP use hota hai.
	- Isse Network Administrator ko har device ka IP Address manually configure nahi karna padta.
	- DHCP automatically available IP Address assign karta hai, jisse Network Management easy ho jata hai.

## 9. What is Subnet Mask ?
- Subnet Mask ek 32-bit number hota hai jo IPv4 Address ke Network Portion aur Host Portion ko identify karne mein help karta hai.
- Simple words mein, ye batata hai ki IP Address ka kaunsa part Network ko represent karta hai aur kaunsa part us Network ke andar specific Device ko.
- Example:
	- Landline Number: 0191-2345678
	- 0191 -> Area Code -> Network ID
	- 2345678 -> Individual Number -> Host ID
- Bilkul isi tarah Subnet Mask batata hai ki IP Address ka kaunsa portion Network ID hai aur kaunsa Host ID.

## 10. Subnet Mask Kam kasa Krta ha?
- Subnet Mask binary AND operation ki help se IP Address ka Network Portion identify karta hai.
- Subnet Mask mein 1 bits Network Portion ko represent karti hain aur 0 bits Host Portion ko represent karti hain.
- Example:
	- IP Address: 192.168.1.10
	- Subnet Mask: 255.255.255.0
	- Binary Subnet Mask: 11111111.11111111.11111111.00000000
	- Yahan first 24 bits Network Portion hain aur last 8 bits Host Portion hain.
	- Isliye Network ID: 192.168.1.0
	- Host ID: 10
	- Is Subnet Mask ko /24 bhi likha jata hai, kyunki ismein 24 bits Network ke liye use hoti hain.

## 11. Why Subnet mask is needed?
- Network Identification: Subnet Mask ki help se Computer identify karta hai ki destination IP Address same Local Network mein hai ya kisi doosre Network mein.
- Routing Decision: Agar destination device same Network mein hai, toh Computer directly us device ko data bhejne ki koshish karta hai. Agar destination doosre Network mein hai, toh data Default Gateway (Router) ke through bheja jata hai.
- Traffic Management: Ek badi Company mein 1,000 computers ko alag-alag Subnets (HR, IT, Sales) mein divide kiya ja sakta hai. Isse har Network ka Broadcast Traffic limited rehta hai.
- Security: Different Departments ko alag Subnets mein rakhkar Firewall aur Access Control Rules ki help se unke beech communication control kiya ja sakta hai.
