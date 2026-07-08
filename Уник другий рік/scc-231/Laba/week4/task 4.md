## Ping, iperf3 and traceroute
|Tool|Primary Use|
|---|---|
|**Ping**|Tests **connectivity** and **latency (RTT)** between two hosts.|
|**Iperf**|Tests **bandwidth**, **throughput**, and **network performance capacity**.|

---

### ⚙️ **2. Protocol Used**

|Tool|Protocol|
|---|---|
|**Ping**|Uses **ICMP (Internet Control Message Protocol)** — Echo Request and Echo Reply messages.|
|**Iperf**|Uses **TCP** or **UDP** (depending on mode). TCP for reliable throughput, UDP for jitter and packet loss testing.|![[Pasted image 20251103185334.png]]![[Pasted image 20251103185348.png]]![[Pasted image 20251103185400.png]]![[Pasted image 20251103190958.png]]![[Pasted image 20251103191015.png]]![[Pasted image 20251103191219.png]]Under ICMP
![[Pasted image 20251103191504.png]]![[Pasted image 20251103191644.png]]![[Pasted image 20251103192032.png]]- The main cause of fluctuating RTT is **network congestion** and **queuing delays** at routers.
    
- Sometimes the destination server might also be under load and take slightly longer to respond.
    
- Different routing paths can also contribute (but less commonly).![[Pasted image 20251103192505.png]]![[Pasted image 20251103192519.png]]
- 