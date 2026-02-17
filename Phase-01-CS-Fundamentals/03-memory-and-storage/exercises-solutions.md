# Topic 03: Exercises with Solutions - Memory and Storage

---

## Exercise 1: Memory Hierarchy

Order from FASTEST to SLOWEST:

| # | Answer | Component |
|---|--------|-----------|
| 1 | **1st** | CPU Registers |
| 2 | **2nd** | L1 Cache |
| 3 | **3rd** | L2 Cache |
| 4 | **4th** | L3 Cache |
| 5 | **5th** | RAM |
| 6 | **6th** | SSD |
| 7 | **7th** | HDD |

---

## Exercise 2: Memory vs Storage

| Characteristic | Answer |
|----------------|--------|
| Volatile (data lost on power off) | **Memory (RAM)** |
| Measured in terabytes typically | **Storage** |
| Nanosecond access time | **Memory (RAM)** |
| Stores your files permanently | **Storage** |
| Where running programs live | **Memory (RAM)** |
| Cheaper per gigabyte | **Storage** |
| Where your OS boots from | **Storage** |

---

## Exercise 3: Cache Concepts

### Part A: Cache Hit Rate Calculation

1. **Total memory requests?** → **1000** (950 + 50)

2. **Cache hit rate?** → **95%** (950/1000 × 100)

3. **Average access time?**
   - Calculation: (950 × 1ns + 50 × 100ns) / 1000
   - = (950 + 5000) / 1000 = **5.95ns**

### Part B: Real-World Cache

1. **Hit rate?** → **98%** (980,000/1,000,000 × 100)

2. **Time saved?**
   - Without cache: 1,000,000 × 50ms = 50,000,000ms
   - With cache: (980,000 × 1ms) + (20,000 × 50ms) = 980,000 + 1,000,000 = 1,980,000ms
   - **Saved: ~48,000,000ms (48,000 seconds = 13+ hours)**

---

## Exercise 4: Linux Memory Commands

```
              total        used        free      shared  buff/cache   available
Mem:           16Gi        10Gi       512Mi       256Mi        5Gi        5.5Gi
Swap:          4Gi         2Gi        2Gi
```

1. **Total physical RAM?** → **16 GiB**

2. **Memory available for new apps?** → **5.5 GiB** (the "available" column)

3. **Is server under memory pressure?**
   - **Yes, moderate concern** - Swap is being used (2Gi), which indicates RAM pressure. Available is only 5.5Gi of 16Gi.

4. **Swap being used?** → **2 GiB**

5. **Should you be concerned?**
   - **Yes** - Active swap usage indicates memory pressure. Applications may be slower. Consider adding RAM or reducing workload.

---

## Exercise 5: Virtual Memory

### True or False

| # | Statement | Answer |
|---|-----------|--------|
| 1 | Each process sees its own private address space starting at 0 | **T** |
| 2 | Virtual memory allows processes to access each other's memory | **F** |
| 3 | Pages are typically 4 KB in size | **T** |
| 4 | The MMU translates virtual addresses to physical addresses | **T** |
| 5 | Virtual memory requires a disk to function | **F** (swap is optional) |
| 6 | Two processes can have the same virtual address but different physical addresses | **T** |

### Short Answer

7. **Why is process isolation important?**
   - Security (processes can't read each other's data), stability (one crash doesn't affect others), simplicity (each process has clean address space).

8. **What happens if Process A tries to access Process B's memory?**
   - **Segmentation fault** - The OS terminates the process for attempting illegal memory access.

---

## Exercise 6: Swap and OOM

### Scenario A: Server Analysis

```
Mem:  total=32Gi  used=31Gi  free=100Mi  available=500Mi
Swap: total=8Gi   used=7Gi   free=1Gi
```

1. **Is this node healthy?** → **No, critical condition**

2. **What is happening?**
   - **Severe memory pressure/thrashing** - Almost all RAM used, almost all swap used. System is likely very slow.

3. **How to fix?**
   - Identify and kill/relocate memory-hungry pods
   - Add more RAM to the node
   - Scale horizontally (add more nodes)
   - Review application memory leaks

### Scenario B: Container OOMKilled

1. **Why is container being killed?**
   - Application uses ~600Mi but limit is 512Mi. Exceeding limit triggers OOMKill.

2. **Two solutions:**
   - **Solution 1:** Increase memory limit to 700Mi+
   - **Solution 2:** Optimize application to use less memory

3. **Which is better?**
   - **Solution 2 is better long-term** (fix root cause), but Solution 1 is faster if app genuinely needs more memory.

---

## Exercise 7: Storage Types

### Part A: Match Use Case to Storage

| Use Case | Answer |
|----------|--------|
| Production PostgreSQL database | **NVMe SSD** |
| Log archive storage (rarely accessed) | **HDD** |
| Boot volume for development server | **SATA SSD** |
| High-frequency trading application | **NVMe SSD** |
| Video file storage | **HDD** |
| Container registry cache | **NVMe SSD** or **SATA SSD** |

### Part B: IOPS Calculation

1. **IOPS needed at peak?**
   - 500 users × 20 operations = **10,000 IOPS**

2. **Can HDD handle this?**
   - **No** - HDD only provides ~100 IOPS

3. **Recommended storage?**
   - **NVMe SSD** (500,000+ IOPS) or at minimum SATA SSD (90,000 IOPS)

---

## Exercise 8: Kubernetes Memory

1. **Minimum memory guaranteed?** → **256Mi** (requests)

2. **Maximum memory allowed?** → **512Mi** (limits)

3. **If pod tries to use 600Mi?** → **OOMKilled** (terminated)

4. **Java -Xmx setting?**
   - **~384Mi** (~75% of limit)
   - Why: Leave headroom for JVM overhead, native memory, and OS

---

## Exercise 9: Practical Troubleshooting

```
Mem: 8Gi used=7.8Gi free=50Mi available=100Mi
Swap: 2Gi used=1.9Gi
top: 65.0 wa
```

1. **What does 65.0 wa mean?**
   - **65% I/O wait** - CPU is idle waiting for disk operations

2. **Most likely cause of slowness?**
   - **Swap thrashing** - System is constantly reading/writing to swap

3. **Evidence supporting this?**
   - Almost no free RAM (50Mi), almost all swap used (1.9Gi of 2Gi), high I/O wait (65%)

4. **Recommendation?**
   - **Add more RAM** or reduce application memory usage. Identify memory-hungry processes.

---

## Exercise 10: Memory Math

1. **64 GiB in MiB?**
   - 64 × 1024 = **65,536 MiB**

2. **2048Mi in GiB?**
   - 2048 / 1024 = **2 GiB**

3. **4KB pages in 1 GiB?**
   - 1 GiB = 1024 × 1024 × 1024 bytes = 1,073,741,824 bytes
   - 1,073,741,824 / 4096 = **262,144 pages**

4. **Page table size for 16 GiB virtual space?**
   - Pages needed: 16 × 1024 × 1024 × 1024 / 4096 = 4,194,304 pages
   - Entry size: 8 bytes
   - Total: 4,194,304 × 8 = 33,554,432 bytes = **32 MiB**

---

## Exercise 11: Fill in the Blanks

1. Cache **hit**
2. **swap** (or swap space/disk)
3. **thrashing**
4. **OOMKilled** (or terminated)
5. **Input/Output Operations Per Second**
6. **MMU** (Memory Management Unit)
7. **PCIe** (bus)
8. **df -h**

---

## Exercise 12: Mini DevOps Scenarios

### Scenario 1: Slow CI/CD Builds
- **Bottleneck:** HDD storage
- **Fix:** Replace HDD with SSD/NVMe. Builds involve many small file operations where IOPS matters more than RAM.

### Scenario 2: Slow Database Despite Cache
- **Problem:** Database writes or cache misses hitting slow storage
- **The 40% iowait indicates disk is the bottleneck, not application caching

### Scenario 3: OOMKilled on K8s but worked on VM
- **Why:** JVM/application likely using more than 4GB. On VM, it could use swap. In Kubernetes (no swap), hard limit is enforced. Also JVM overhead and container overhead add up.

---

## Bonus Challenge Solutions

1. **Available vs Free memory?**
   - "Free" is completely unused RAM (often low). "Available" includes free + reclaimable cache/buffers. Linux uses free RAM for caching - this is good and can be reclaimed when apps need it.

2. **Slow apps with 0% swap?**
   - Memory leaks, garbage collection pauses, disk I/O bottleneck, CPU contention, network latency, lock contention.

3. **Why databases benefit more from NVMe?**
   - Databases do many random read/write operations. NVMe excels at random IOPS. Web servers serving static files do sequential reads which HDDs can handle better.

---

*These are the correct answers for self-checking after completing exercises.*
