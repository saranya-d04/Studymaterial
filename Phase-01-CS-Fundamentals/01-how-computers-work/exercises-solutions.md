# Topic 01: Exercises with Solutions - How Computers Work

---

## Exercise 1: Component Matching

Match each scenario to the component that would be the bottleneck:

| Scenario | Answer |
|----------|--------|
| Video rendering taking hours | **CPU** - Video rendering is compute-intensive |
| Application crashes with "Out of Memory" | **RAM** - Application needs more memory |
| Database queries are slow | **Storage (SSD/HDD)** - Database I/O bound |
| Web app has high latency to users | **Network I/O** - Network is the bottleneck |
| Opening large files takes forever | **Storage (SSD/HDD)** - Reading from disk |

---

## Exercise 2: Fill in the Blanks

1. The CPU runs in a cycle called **fetch-decode-execute** cycle
2. RAM is **volatile**, meaning it loses data when power is off
3. A 3 GHz processor can do approximately **3 billion** cycles per second
4. **Registers** is the fastest type of memory but has the smallest capacity
5. When RAM is full, the system starts using **swap/virtual memory** which is much slower

---

## Exercise 3: True or False

| # | Statement | Answer | Explanation |
|---|-----------|--------|-------------|
| 1 | More RAM always makes a computer faster | **F** | Only helps if RAM was the bottleneck |
| 2 | SSD is faster than RAM | **F** | RAM is ~1000x faster than SSD |
| 3 | A single CPU core can only execute one instruction at a time | **T** | Basic principle (ignoring pipelining) |
| 4 | Cache is larger but slower than RAM | **F** | Cache is SMALLER and FASTER |
| 5 | The ALU performs math calculations | **T** | Arithmetic Logic Unit does math |
| 6 | Storage is volatile memory | **F** | Storage is non-volatile (persistent) |
| 7 | I/O stands for Input/Output | **T** | Correct definition |
| 8 | A CPU-bound task would benefit from adding more RAM | **F** | CPU-bound needs faster/more CPU |

---

## Exercise 4: Memory Hierarchy

Order from FASTEST to SLOWEST:

1. (fastest) **Registers**
2. **L2 Cache**
3. **RAM**
4. **SSD**
5. (slowest) **HDD**

**Full hierarchy:** Registers → L1 Cache → L2 Cache → L3 Cache → RAM → SSD → HDD

---

## Exercise 5: Real-World Scenario Analysis

**Scenario:** Build server taking 45 minutes, CPU at 95-100%, RAM at 40%

1. **Which component is the bottleneck?**
   - **CPU** - It's at 95-100% utilization

2. **Would adding more RAM help?**
   - **No** - RAM is only 40% used, not the bottleneck

3. **What upgrade would improve build times?**
   - **Faster CPU or more CPU cores** - The task is CPU-bound

---

## Exercise 6: DevOps Application

```yaml
resources:
  limits:
    cpu: "500m"
    memory: "512Mi"
```

1. **What does `500m` mean for CPU?**
   - **0.5 CPU cores (500 millicores)** - 1000m = 1 full core

2. **What does `512Mi` mean for memory?**
   - **512 Mebibytes of RAM** (536,870,912 bytes)

3. **What happens if the application tries to use more than 512Mi?**
   - **Container gets OOM Killed** (terminated by Kubernetes)

---

## Exercise 7: Explain Like I'm Five (ELI5)

1. **What does the CPU do?**
   - The CPU is like the brain of the computer. It does all the thinking and calculations, following instructions one by one very quickly.

2. **What's the difference between RAM and a hard drive?**
   - RAM is like your desk - it holds what you're working on right now and gets cleared when you leave. The hard drive is like a filing cabinet - it stores things permanently even when turned off.

3. **Why does a computer slow down when running many programs?**
   - Each program needs space on your "desk" (RAM). When too many programs run, they fight for the limited desk space, and the computer has to keep moving things in and out of the filing cabinet (storage), which is much slower.

---

## Bonus Challenge Solutions

1. **What is virtual memory?**
   - Virtual memory is a technique where the OS uses disk space as "pretend" RAM. When physical RAM is full, less-used data is moved to disk (swap) to make room for active programs.

2. **What is cache hit ratio?**
   - Cache hit ratio = (cache hits / total requests) × 100%. DevOps engineers care because higher hit ratio means faster performance and less load on databases.

3. **Why do servers have multiple CPUs with many cores?**
   - Servers handle many simultaneous requests. More cores = more parallel processing = handle more users/requests at once.

---

*These are the correct answers for self-checking after completing exercises.*
