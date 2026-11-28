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

## Q12 : What is CIDR notation? How Does it Solve Problem ?
- Old Problem
	- Pehle IPv4 Addresses ko fixed-size blocks (Class A, B, C) mein divide kiya jata tha.
	- Iski wajah se IP Addresses waste ho jaate the. Example: Agar kisi company ko 500 IP Addresses chahiye, toh Class C ke 254 addresses sufficient nahi the, aur Class B ke 65,534 addresses bahut zyada the.
	- Saath hi Subnet Mask ko baar-baar 255.255.255.0 jaise long format mein likhna padta tha.
- Is Problem Ko Solve Kiya CIDR Notation Ne.
	- CIDR ka full form Classless Inter-Domain Routing hai.
	- Ye IP Address ko fixed classes (A, B, C) mein divide karne ke bajaye flexible-size networks mein divide karne ki facility deta hai.
	- Ismein IP Address ke saath slash (/) aur ek number likha jata hai, jo batata hai ki kitne bits Network Portion ke liye reserved hain.
	- Example:
		- 192.168.47.20/24
		- 192.168.47.29/16
	- CIDR ki help se hum apni requirement ke according Network Size define kar sakte hain, jisse IP Addresses waste nahi hote.
	- Ye multiple IP Networks ko ek single route mein combine karne (Route Aggregation) mein bhi help karta hai.

## Q13 : Explain /24 And /16 CIDR notation?
- Ek IPv4 Address total 32 bits ka hota hai, jise 4 parts (Octets) mein divide kiya jata hai.
- CIDR notation mein slash ke baad likha number (e.g., /24 ya /16) ye batata hai ki left side se kitne bits Network ID ke liye reserved hain.
- Baaki bache bits (32 - CIDR) Host ID ke liye available hote hain.

- /24 (Example: 192.168.1.0/24)
	- Total 32 bits mein se pehle 24 bits Network ke liye aur baaki 8 bits Host ke liye reserved hain.
	- Subnet Mask Equivalent: 255.255.255.0 (Binary: 11111111.11111111.11111111.00000000).
	- Total IP Addresses: 2^8 = 256.
	- Total Usable IP Addresses: 2^8 - 2 = 254 devices.
	- 2 IPs normally reserved hote hain:
		- Network Address: 192.168.1.0
		- Broadcast Address: 192.168.1.255
	- Use Case: Home Wi-Fi, Small Offices.

- /16 (Example: 172.16.0.0/16)
	- Total 32 bits mein se pehle 16 bits Network ke liye aur baaki 16 bits Host ke liye reserved hain.
	- Subnet Mask Equivalent: 255.255.0.0 (Binary: 11111111.11111111.00000000.00000000).
	- Total IP Addresses: 2^16 = 65,536.
	- Total Usable IP Addresses: 2^16 - 2 = 65,534 devices.
	- 2 IPs normally reserved hote hain:
		- Network Address: 172.16.0.0
		- Broadcast Address: 172.16.255.255
	- Use Case: Large Companies, Universities aur AWS/Azure mein large Virtual Networks (VPC/VNet) define karne ke liye.

## Q14 : What is Default GateWay?
- Jab tumhara Device apne Local Network se bahar kisi doosre Network ke Device se communicate karna chahta hai, toh usko ek Exit Point ki zaroorat hoti hai.
- Isi Exit Point ko Default Gateway kehte hain.
- Normally humare Home Wi-Fi mein Router ka Private IP Address hi Default Gateway hota hai.
- Example:
	- Socho tum ek Gated Colony ke andar rehte ho, jisme 50 ghar hain.
	- Agar Colony ke andar hi kisi doosre ghar se baat karni hai, toh tum directly us ghar tak message bhej sakte ho.
	- Lekin agar kisi doosri Colony ya bahar ke area mein message bhejna hai, toh tumhe Colony ke Main Gate se bahar jaana padega.

- Gate Colony: Home Wi-Fi / LAN Network.
- Colony ke Ghar: Tumhare Local Devices (Mobile: 192.168.1.10, Laptop: 192.168.1.11, Printer: 192.168.1.12).
- Colony ka Main Gate: Default Gateway (Tumhare Wi-Fi Router ka Private IP, usually 192.168.1.1).

## Q15 : Default Gate Way Kam Kasa Krta ha.
1. Jab tumhara Laptop (192.168.1.11) apne hi Network ke Printer (192.168.1.12) ko Print Command bhejta hai, toh Subnet Mask ki help se Laptop check karta hai ki dono same Network mein hain. Agar same Network mein hain, toh Laptop directly Local Network ke through Printer ko Data bhejta hai. Is case mein Default Gateway ki zaroorat nahi padti.

2. Jab tum Browser mein YouTube.com open karte ho, toh pehle DNS YouTube ka IP Address resolve karta hai (e.g., 142.250.190.46). Ab Laptop Subnet Mask ki help se check karta hai ki destination IP uske Local Network mein hai ya nahi. Kyunki YouTube ka Server kisi doosre Network mein hai, isliye Laptop Data ko Default Gateway (192.168.1.1 - Router) ke paas bhej deta hai.

3. Router apni Routing Table ki help se decide karta hai ki Data ko next kahan forward karna hai. Agar hum Private IPv4 Address use kar rahe hain, toh Router NAT (Network Address Translation) ki help se Source Private IP ko Public IP mein translate karta hai aur Data ISP ke through YouTube Server tak pahunchta hai.

4. Jab YouTube Server ka Response wapas aata hai, toh Router NAT Mapping ki help se Response ko correct Local Device tak pahunchata hai.

## Q16 : What is DHCP ?
- Jab bhi LAN mein koi New Device connect hota hai, toh usko Network Communication ke liye kuch important Network Settings ki zaroorat hoti hai:
	- IP Address
	- Subnet Mask
	- Default Gateway
	- DNS Server
- Agar hum ye saari Settings manually configure karein, toh ye Time Consuming aur Error Prone ho sakta hai.
- Example: Agar do Devices ko same IP Address manually assign kar diya, toh IP Address Conflict ho sakta hai.
- Isi Problem ko Solve Karta Hai DHCP.
	- DHCP ka full form Dynamic Host Configuration Protocol hai.
	- Ye ek Network Protocol hai jo Devices ko automatically IP Address aur doosri Network Settings assign karta hai.
	- DHCP Server ke paas ek IP Address Pool hota hai, jisme se wo available IP Address select karke New Device ko assign karta hai.
	- DHCP IP Address ke saath Subnet Mask, Default Gateway, DNS Server aur Lease Time bhi provide karta hai.
	- Isse Network Administrator ko har Device ki Settings manually configure nahi karni padti.

## Q17 : What is DHCP DORA Process ?
- DHCP ek DORA Process follow karta hai, jiske through New Device ko IP Address aur Network Settings assign ki jaati hain.
- DORA ke 4 Steps hote hain:

- D : Discovery (Broadcast)
	- Jab New Device Network se connect hota hai, toh uske paas abhi koi IP Address nahi hota.
	- Isliye wo poore Local Network mein ek Broadcast Message (255.255.255.255) bhejta hai aur DHCP Server ko search karta hai.
	- Message ka meaning hota hai: "Kya is Network mein koi DHCP Server available hai? Mujhe IP Address chahiye."
	- Example: Tum hall mein ghuste hi zor se puchte ho: "Koi Manager hai yahan? Mujhe ek khali table chahiye!"

- O : Offer (Unicast / Broadcast)
	- DHCP Server Discovery Message receive karta hai aur apne IP Pool mein se ek available IP Address select karke Client ko offer bhejta hai.
	- Is Offer mein IP Address, Subnet Mask, Default Gateway, DNS Server aur Lease Time ki information hoti hai.
	- Ye Offer Unicast ya Broadcast dono tarike se bheja ja sakta hai, depending on Client aur Network Configuration.
	- Example: Manager tumhari awaaz sunta hai aur kehta hai: "Haan bhai, main hoon Manager! Table No. 5 khali hai, 2 ghante ke liye le lo."

- R : Request (Broadcast)
	- Client available Offer mein se ek IP Address select karta hai aur DHCP Request Message Broadcast karta hai.
	- Is Message mein Client batata hai ki wo kaunsa IP Address aur kis DHCP Server ka Offer accept kar raha hai.
	- Ye Broadcast isliye hota hai taaki Network ke doosre DHCP Servers ko bhi pata chal jaye ki Client ne ek particular Offer select kar liya hai.
	- Example: Tum sabko sunate hue kehte ho: "Theek hai Manager Sahab, mujhe Table No. 5 hi de do, main ye le raha hoon!"
	- Isse doosre Managers ko pata chal jata hai ki unka Offer select nahi hua, aur wo apna IP Address kisi doosre Client ko offer kar sakte hain.

- A : Acknowledgement (Unicast / Broadcast)
	- DHCP Server Client ki Request receive karne ke baad us IP Address ko Client ke liye reserve/assign karta hai.
	- Uske baad DHCP Server Client ko DHCP ACK (Acknowledgement) Message bhejta hai.
	- Is Message mein final Network Configuration confirm hoti hai, jiske baad Client assigned IP Address use kar sakta hai.
	- Ye ACK bhi Unicast ya Broadcast ho sakta hai, depending on Client aur Network Configuration.
	- Example: Manager apne Register mein likh leta hai ki Table No. 5 tumhe de di gayi hai aur tumhe confirmation de deta hai: "Done! Table No. 5 ab tumhari hai."


