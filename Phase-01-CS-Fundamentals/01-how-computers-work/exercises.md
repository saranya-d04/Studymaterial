# Topic 01: Exercises - How Computers Work

Complete these exercises to reinforce your understanding.

---

## Exercise 1: Component Matching

Match each scenario to the component that would be the bottleneck:

| Scenario | Your Answer |
|----------|-------------|
| Video rendering taking hours | |
| Application crashes with "Out of Memory" | |
| Database queries are slow | |
| Web app has high latency to users | |
| Opening large files takes forever | |

**Options:** CPU, RAM, Storage (SSD/HDD), Network I/O

---

## Exercise 2: Fill in the Blanks

1. The CPU runs in a cycle called ________-________-________
2. RAM is ________ (volatile/non-volatile), meaning it loses data when power is off
3. A 3 GHz processor can do approximately ________ cycles per second
4. ________ is the fastest type of memory but has the smallest capacity
5. When RAM is full, the system starts using ________ which is much slower

---

## Exercise 3: True or False

Mark each statement T (True) or F (False):

| # | Statement | T/F |
|---|-----------|-----|
| 1 | More RAM always makes a computer faster | |
| 2 | SSD is faster than RAM | |
| 3 | A single CPU core can only execute one instruction at a time | |
| 4 | Cache is larger but slower than RAM | |
| 5 | The ALU performs math calculations | |
| 6 | Storage is volatile memory | |
| 7 | I/O stands for Input/Output | |
| 8 | A CPU-bound task would benefit from adding more RAM | |

---

## Exercise 4: Memory Hierarchy

Put these in order from FASTEST to SLOWEST:

- [ ] RAM
- [ ] Registers  
- [ ] SSD
- [ ] HDD
- [ ] L2 Cache

Write your answer here:
1. (fastest) __________
2. __________
3. __________
4. __________
5. (slowest) __________

---

## Exercise 5: Real-World Scenario Analysis

**Scenario:** Your company's build server is taking 45 minutes to compile code. You check:
- CPU: 95-100% utilization
- RAM: 40% used (8GB of 20GB)
- Disk: Low I/O wait

**Questions:**

1. Which component is the bottleneck?
   
   Your answer: _______________

2. Would adding more RAM help?
   
   Your answer: _______________ Why? _______________

3. What upgrade would most likely improve build times?
   
   Your answer: _______________

---

## Exercise 6: DevOps Application

You see this Kubernetes resource configuration:

```yaml
resources:
  limits:
    cpu: "500m"
    memory: "512Mi"
```

Answer:
1. What does `500m` mean for CPU?
   
   Your answer: _______________

2. What does `512Mi` mean for memory?
   
   Your answer: _______________

3. What happens if the application tries to use more than 512Mi of RAM?
   
   Your answer: _______________

---

## Exercise 7: Explain Like I'm Five (ELI5)

Write a simple explanation (2-3 sentences) for each concept as if explaining to someone with no tech background:

1. **What does the CPU do?**
   
   Your explanation:

2. **What's the difference between RAM and a hard drive?**
   
   Your explanation:

3. **Why does a computer slow down when running many programs?**
   
   Your explanation:

---

## Exercise 8: Diagram Drawing

On paper (or using a drawing tool), draw:

1. The basic 4-component computer architecture
2. Show how data flows between components
3. Label each component with one key characteristic

*Note: This is for your own practice. Visual learning reinforces concepts.*

---

## Bonus Challenge

Research and answer:

1. What is "virtual memory" and how does it relate to RAM and storage?

2. What is "cache hit ratio" and why do DevOps engineers care about it?

3. Why do servers often have multiple CPUs with many cores?

---

## Self-Assessment

After completing exercises, rate your understanding:

| Concept | Confidence (1-5) |
|---------|-----------------|
| CPU and its role | |
| Memory vs Storage | |
| Fetch-Decode-Execute cycle | |
| Memory hierarchy | |
| Bottleneck analysis | |

If any rating is below 3, re-read that section of the notes.

---

*Complete the exercises, then request the test from your instructor.*
