# Topic 01: Exercise Evaluation & Feedback

**Student Progress Check - How Computers Work**
**Date:** February 17, 2026

---

## Overall Score: 65% (13/20 points) - NEEDS IMPROVEMENT

To proceed to Topic 02, you need 70% or higher. Let's review your answers and strengthen weak areas.

---

## Exercise 1: Component Matching (3/5 points)

| Scenario | Your Answer | Correct Answer | Result |
|----------|-------------|----------------|--------|
| Video rendering taking hours | *(blank)* | **CPU** | ❌ |
| Application crashes with "Out of Memory" | RAM | **RAM** | ✅ |
| Database queries are slow | Network I/O | **Storage (SSD/HDD)** | ❌ |
| Web app has high latency to users | Network I/O | **Network I/O** | ✅ |
| Opening large files takes forever | RAM | **Storage (SSD/HDD)** | ❌ |

### Corrections Explained:

**Video rendering** → **CPU**
- Video encoding/decoding is computation-heavy
- The CPU is doing millions of calculations to compress video frames
- This is a classic CPU-bound task

**Database queries slow** → **Storage (Disk I/O)**, not Network
- Databases read/write data from disk
- Slow queries usually mean disk seeks (especially with HDDs) or unoptimized queries
- Network I/O would be relevant if the database was on a remote server AND network latency was proven

**Opening large files** → **Storage**, not RAM
- Files are STORED on disk (SSD/HDD)
- Opening = READING from storage
- RAM only becomes the bottleneck if the file doesn't fit in memory AFTER it's loaded

### Key Insight:
Think about **WHERE the data currently is** and **WHERE it needs to go**:
- Data on disk → CPU = **Storage bottleneck**
- Data in RAM → CPU = Could be **CPU or Memory bottleneck**
- Data over network → your app = **Network I/O bottleneck**

---

## Exercise 2: Fill in the Blanks (4/5 points)

| Question | Your Answer | Correct Answer | Result |
|----------|-------------|----------------|--------|
| CPU cycle name | fetch-decode-execute | fetch-decode-execute | ✅ |
| RAM volatility | volatile | volatile | ✅ |
| 3 GHz cycles | 3 billion | 3 billion | ✅ |
| Fastest memory type | RAM | RAM | ✅ |
| When RAM full, system uses... | cpu bounce | **swap** or **virtual memory** | ❌ |

### Correction for #5:
When RAM is full, the operating system moves less-used data to a special area on the disk called **swap space** (Linux) or **page file** (Windows). This is also known as **virtual memory**.

**Why it's called swap:** The OS "swaps" data between RAM and disk.

**Important:** This is NOT related to CPU at all. Swapping involves:
- RAM (source of data)
- Storage/Disk (destination)
- NOT the CPU (though CPU does manage the operation)

---

## Exercise 3: True or False (7/8 points)

| # | Statement | Your Answer | Correct | Result |
|---|-----------|-------------|---------|--------|
| 1 | More RAM always makes a computer faster | F | F | ✅ |
| 2 | SSD is faster than RAM | F | F | ✅ |
| 3 | A single CPU core can only execute one instruction at a time | T | T | ✅ |
| 4 | Cache is larger but slower than RAM | T | **F** | ❌ |
| 5 | The ALU performs math calculations | T | T | ✅ |
| 6 | Storage is volatile memory | F | F | ✅ |
| 7 | I/O stands for Input/Output | T | T | ✅ |
| 8 | A CPU-bound task would benefit from adding more RAM | F | F | ✅ |

### Correction for #4:

**Cache is SMALLER but FASTER than RAM** - The statement is FALSE.

Remember the memory hierarchy pyramid:
```
      /\
     /  \  ← Registers (fastest, smallest)
    /----\
   / Cache \ ← L1/L2/L3 Cache (very fast, small)
  /----------\
 /    RAM     \ ← RAM (fast, medium size)
/----------------\
      SSD/HDD     ← Storage (slow, largest)
```

**Cache characteristics:**
- Size: L1 = 64KB, L2 = 256KB, L3 = 8MB
- RAM size: 8GB - 64GB (thousands of times larger!)
- Cache speed: 1-20 nanoseconds
- RAM speed: ~100 nanoseconds

**Why cache exists:** It stores frequently accessed data closer to the CPU to avoid the "slow" trip to RAM.

---

## Exercise 4: Memory Hierarchy (5/5 points) ✅ PERFECT!

Your order: Registers → L2 Cache → RAM → SSD → HDD

This is **CORRECT!** You understand the speed hierarchy.

---

## Exercise 5: Real-World Scenario (1/3 points)

**Given:**
- CPU: 95-100% utilization
- RAM: 40% used (8GB of 20GB)  
- Disk: Low I/O wait

| Question | Your Answer | Correct Answer | Result |
|----------|-------------|----------------|--------|
| Which component is bottleneck? | CPU | **CPU** | ✅ |
| Would adding more RAM help? | Yes | **No** | ❌ |
| What upgrade would help? | *(blank)* | **Faster CPU or more cores** | ❌ |

### Critical Correction:

**Adding RAM would NOT help!** Here's why:

```
Current state:
CPU:  [████████████████████] 95-100%  ← MAXED OUT (bottleneck!)
RAM:  [████████░░░░░░░░░░░░] 40%       ← Plenty of room!
Disk: [██░░░░░░░░░░░░░░░░░░] Low       ← Not the problem
```

- RAM is only at 40% - you have 12GB unused!
- Adding RAM doesn't make the CPU work faster
- The CPU is the one struggling, not memory

**Correct solution:**
1. **Upgrade to a faster CPU** (higher GHz, better architecture)
2. **Add more CPU cores** (for parallel compilation)
3. **Optimize the build process** (parallel jobs, incremental builds)

### DevOps Application:
In CI/CD pipelines, if builds are slow and CPU is maxed:
- Use build servers with more cores
- Enable parallel job execution
- Consider distributed builds

---

## Exercise 6: Kubernetes Application (0/3 points) - NOT ATTEMPTED

Let me teach you this:

```yaml
resources:
  limits:
    cpu: "500m"      # 500 millicores = 0.5 CPU cores
    memory: "512Mi"  # 512 Mebibytes of RAM
```

### Answers:

**1. What does `500m` mean for CPU?**
- `m` = millicores (1/1000 of a core)
- `500m` = 500 millicores = 0.5 cores = half a CPU core
- `1000m` = 1 full CPU core

**2. What does `512Mi` mean for memory?**
- `Mi` = Mebibytes (1 MiB = 1,048,576 bytes)
- `512Mi` = 512 Mebibytes ≈ 536 MB of RAM
- Note: `Mi` (Mebibyte) vs `M` (Megabyte) - Kubernetes uses binary units

**3. What happens if the app tries to use more than 512Mi RAM?**
- The container gets **OOM Killed** (Out of Memory Killed)
- Kubernetes terminates the container immediately
- The pod restarts (if restart policy allows)

**CPU excess behavior (for comparison):**
- If CPU exceeds limit → container is **throttled** (slowed down)
- It is NOT killed, just given less CPU time

---

## Exercise 7: ELI5 - NOT ATTEMPTED

I'll provide model answers you should understand:

**1. What does the CPU do?**
> "The CPU is like the brain of the computer. It reads instructions and does what they say - like a very fast reader who can follow a recipe billions of times per second. Whatever you tell the computer to do, the CPU is the one actually doing it."

**2. What's the difference between RAM and a hard drive?**
> "RAM is like your desk - it's where you put things you're working on right now. It's fast to grab things, but when you turn off the lights (power), everything on the desk disappears. A hard drive is like a filing cabinet - it stores things permanently even when power is off, but it takes longer to get things from it."

**3. Why does a computer slow down when running many programs?**
> "Each program needs space on your desk (RAM) and the chef's attention (CPU). When you run too many programs, there's not enough desk space, so the computer starts putting some papers back in the filing cabinet (swap). This makes everything slow because walking to the filing cabinet takes much longer than grabbing something from your desk."

---

## Summary & Action Plan

### Score Breakdown:
| Exercise | Points | Max |
|----------|--------|-----|
| Exercise 1 | 3 | 5 |
| Exercise 2 | 4 | 5 |
| Exercise 3 | 7 | 8 |
| Exercise 4 | 5 | 5 |
| Exercise 5 | 1 | 3 |
| Exercise 6 | 0 | 3 |
| Exercise 7 | N/A | (practice) |
| **TOTAL** | **13** | **20** |

### Percentage: 65% - BELOW PASSING (70% required)

---

## Weak Areas Identified:

1. **Bottleneck identification confusion** - Mixing up which component causes which symptom
2. **Swap/Virtual Memory concept** - Need to understand RAM ↔ Disk relationship
3. **Cache vs RAM relationship** - Remember: Cache is smaller AND faster
4. **Kubernetes resource units** - Need to learn millicores and memory units
5. **Applying theory to scenarios** - Understanding WHEN each component is the problem

---

## Required Action: RETEACHING

Before proceeding to Topic 02, you must:

1. ✅ Read the corrections above carefully
2. ✅ Re-read the Bottleneck Analysis section in your notes
3. ✅ Complete a RETEST (provided below)

---

## RETEST - Answer These to Proceed

Answer the following questions correctly to advance to Topic 02:

### Question 1:
A web server is responding slowly. You check and find:
- CPU: 20%
- RAM: 95%
- Disk: 40%

What is the bottleneck? ____Ram__________
Would a faster CPU help? _____no ading more ram should be help_________
What solution would you recommend? _____adding more ram _________

### Question 2:
In Kubernetes, what does `cpu: "250m"` mean?
____0.25cpu__________

### Question 3:
What happens when a container tries to use MORE memory than its limit?
a) It gets throttled
b) It gets killed (OOM)
c) Nothing happens
b
### Question 4:
Cache is (smaller/larger) and (slower/faster) than RAM.
large slower
### Question 5:
When RAM is full, the operating system uses _____swap are virtually storage_________ which stores data on the disk temporarily.

---

**Submit your retest answers, and I'll evaluate them to determine if you can proceed to Topic 02: Binary and Data Representation.**
