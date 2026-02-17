# Topic 02: Binary and Data Representation

## 🎯 Learning Objectives

By the end of this topic, you will:
1. Understand why computers use binary (only 0s and 1s)
2. Convert between decimal, binary, and hexadecimal
3. Understand bits, bytes, and data size units
4. Know how text is stored (ASCII and Unicode)
5. Understand how negative numbers are represented
6. Know how images and files are stored as binary
7. Apply this knowledge to DevOps scenarios

---

# SECTION A: WHY BINARY?

---

## Part 1: Why Do Computers Use Binary?

### The Simple Answer

Computers are made of billions of tiny switches called **transistors**. Each switch can only be in TWO states:

```
┌─────────────────────────────────────────────────────────────┐
│                     TRANSISTOR STATES                        │
│                                                              │
│     OFF (no electricity)          ON (electricity flowing)   │
│     ┌─────────────┐               ┌─────────────┐           │
│     │             │               │  ⚡⚡⚡⚡⚡    │           │
│     │    ○────    │               │    ●────    │           │
│     │   (open)    │               │  (closed)   │           │
│     │             │               │             │           │
│     │   = 0       │               │   = 1       │           │
│     └─────────────┘               └─────────────┘           │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

### Why Not Use 10 Digits Like Humans?

| System | Why We Use It | Why Computers Don't |
|--------|---------------|---------------------|
| Decimal (0-9) | Humans have 10 fingers | Would need 10 different voltage levels - too unreliable |
| Binary (0-1) | - | Only 2 states: ON/OFF - very reliable! |

**Key Insight:** Binary is not the most efficient for humans, but it's the most **reliable** for electronics.

### Real-World Analogy: Light Switches

```
Your home has light switches:

    OFF         ON
     ○           ●
     │           │
   ──┴──       ──┴──

Could you have a switch with 10 positions?
Technically yes, but it would be:
- Harder to read
- More likely to be "in between"
- Less reliable

Same with computer circuits!
```

---

## Part 2: What is Binary?

### Binary = Base-2 Number System

In our normal **decimal** system (base-10), we use 10 digits: 0, 1, 2, 3, 4, 5, 6, 7, 8, 9

In **binary** (base-2), we use only 2 digits: **0** and **1**

### Counting in Binary

```
Decimal │ Binary │ Explanation
────────┼────────┼──────────────────────────────────
   0    │  0000  │ Zero
   1    │  0001  │ One
   2    │  0010  │ Two (no "2" digit, so carry over)
   3    │  0011  │ Three
   4    │  0100  │ Four (carry again)
   5    │  0101  │ Five
   6    │  0110  │ Six
   7    │  0111  │ Seven
   8    │  1000  │ Eight (another carry)
   9    │  1001  │ Nine
  10    │  1010  │ Ten
  11    │  1011  │ Eleven
  12    │  1100  │ Twelve
  13    │  1101  │ Thirteen
  14    │  1110  │ Fourteen
  15    │  1111  │ Fifteen
  16    │ 10000  │ Sixteen (need 5 digits now!)
```

### Pattern Recognition

Notice how it's like counting with only 0 and 1:
- When you reach 1, the next number "rolls over" like an odometer
- Just like 9 → 10 in decimal, 1 → 10 in binary

---

# SECTION B: BINARY CONVERSION

---

## Part 3: Understanding Place Values

### Decimal Place Values (What You Know)

In decimal, each position is a power of 10:

```
Number: 4,527

Position:    Thousands  Hundreds   Tens     Ones
Power of 10:    10³        10²      10¹      10⁰
Value:         1000       100       10        1
Digit:           4          5        2        7

Calculation: (4×1000) + (5×100) + (2×10) + (7×1) = 4527
```

### Binary Place Values

In binary, each position is a power of 2:

```
Binary number: 1101

Position:     8's    4's    2's    1's
Power of 2:   2³     2²     2¹     2⁰
Value:         8      4      2      1
Digit:         1      1      0      1

Calculation: (1×8) + (1×4) + (0×2) + (1×1) = 8 + 4 + 0 + 1 = 13
```

### The Magic Table (MEMORIZE THIS!)

```
┌────────────────────────────────────────────────────────────────────┐
│                    POWERS OF 2 (Memorize!)                         │
├────────────────────────────────────────────────────────────────────┤
│                                                                    │
│   2⁰ = 1                                                          │
│   2¹ = 2                                                          │
│   2² = 4                                                          │
│   2³ = 8                                                          │
│   2⁴ = 16                                                         │
│   2⁵ = 32                                                         │
│   2⁶ = 64                                                         │
│   2⁷ = 128                                                        │
│   2⁸ = 256                                                        │
│   2⁹ = 512                                                        │
│   2¹⁰ = 1024 (≈ 1 Kilo)                                          │
│                                                                    │
│   Pattern: Each number is DOUBLE the previous                     │
│   1 → 2 → 4 → 8 → 16 → 32 → 64 → 128 → 256 → 512 → 1024          │
│                                                                    │
└────────────────────────────────────────────────────────────────────┘
```

---

## Part 4: Converting Binary to Decimal

### Method: Add the Place Values Where There's a 1

**Example 1: Convert 1011 to decimal**

```
Step 1: Write the place values (right to left, starting at 1)

Binary:        1     0     1     1
              ─┬─   ─┬─   ─┬─   ─┬─
Place value:   8     4     2     1

Step 2: Add values where binary digit is 1

               1     0     1     1
               ×     ×     ×     ×
               8     4     2     1
               ↓     ↓     ↓     ↓
               8  +  0  +  2  +  1  =  11

Answer: 1011 (binary) = 11 (decimal)
```

**Example 2: Convert 11001010 to decimal**

```
Binary:        1     1     0     0     1     0     1     0
              ─┬─   ─┬─   ─┬─   ─┬─   ─┬─   ─┬─   ─┬─   ─┬─
Place value: 128    64    32    16     8     4     2     1

Add the 1s:   128 +  64 +  0  +  0  +  8  +  0  +  2  +  0

             = 128 + 64 + 8 + 2
             = 202

Answer: 11001010 (binary) = 202 (decimal)
```

---

## Part 5: Converting Decimal to Binary

### Method: Divide by 2, Track Remainders

**Example 1: Convert 13 to binary**

```
Step 1: Divide by 2 repeatedly, note the remainder

13 ÷ 2 = 6  remainder 1  ↑
 6 ÷ 2 = 3  remainder 0  │
 3 ÷ 2 = 1  remainder 1  │  Read remainders
 1 ÷ 2 = 0  remainder 1  │  BOTTOM to TOP
                         ↓

Step 2: Read remainders from bottom to top: 1101

Answer: 13 (decimal) = 1101 (binary)

Verify: 8 + 4 + 0 + 1 = 13 ✓
```

**Example 2: Convert 50 to binary**

```
50 ÷ 2 = 25  remainder 0  ↑
25 ÷ 2 = 12  remainder 1  │
12 ÷ 2 = 6   remainder 0  │
 6 ÷ 2 = 3   remainder 0  │  Read bottom to top
 3 ÷ 2 = 1   remainder 1  │
 1 ÷ 2 = 0   remainder 1  ↓

Answer: 50 (decimal) = 110010 (binary)

Verify: 32 + 16 + 0 + 0 + 2 + 0 = 50 ✓
```

### Alternative Method: Subtraction (Often Faster!)

**Example: Convert 50 to binary**

```
Start with 50. Find the largest power of 2 that fits:

Powers of 2: 1, 2, 4, 8, 16, 32, 64...
64 > 50, so use 32

50 - 32 = 18    → 32's place gets a 1
18 - 16 = 2     → 16's place gets a 1
 2 -  8 = X     → 8's place gets a 0 (8 > 2)
 2 -  4 = X     → 4's place gets a 0 (4 > 2)
 2 -  2 = 0     → 2's place gets a 1
 0 -  1 = X     → 1's place gets a 0

         32  16   8   4   2   1
          1   1   0   0   1   0

Answer: 50 = 110010
```

---

# SECTION C: BITS AND BYTES

---

## Part 6: Bits, Bytes, and Data Units

### What is a Bit?

A **bit** (binary digit) is the smallest unit of data:
- Can only be 0 or 1
- Represents a single ON/OFF switch

### What is a Byte?

A **byte** = 8 bits

```
1 BYTE = 8 BITS

┌───┬───┬───┬───┬───┬───┬───┬───┐
│ 0 │ 1 │ 1 │ 0 │ 0 │ 1 │ 0 │ 1 │  ← This is 1 byte
└───┴───┴───┴───┴───┴───┴───┴───┘
  7   6   5   4   3   2   1   0    ← Bit positions

Why 8 bits?
- 8 bits can represent 2⁸ = 256 different values (0-255)
- Perfect for storing a single character (A-Z, a-z, 0-9, symbols)
- Became the industry standard in the 1960s
```

### Data Size Units

```
┌─────────────────────────────────────────────────────────────────┐
│                       DATA SIZE UNITS                            │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│   1 bit (b)        = 0 or 1                                     │
│   1 Byte (B)       = 8 bits                                     │
│   1 Kilobyte (KB)  = 1,000 bytes        (short text file)       │
│   1 Megabyte (MB)  = 1,000 KB           (MP3 song)              │
│   1 Gigabyte (GB)  = 1,000 MB           (movie file)            │
│   1 Terabyte (TB)  = 1,000 GB           (laptop hard drive)     │
│   1 Petabyte (PB)  = 1,000 TB           (data center)           │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Binary Units vs Decimal Units (IMPORTANT!)

There are TWO systems, and they cause confusion:

```
┌─────────────────────────────────────────────────────────────────┐
│              DECIMAL (SI) vs BINARY (IEC) UNITS                  │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│   DECIMAL (Marketing uses this)    BINARY (Technical accuracy)  │
│   ─────────────────────────────    ──────────────────────────── │
│   1 KB = 1,000 bytes               1 KiB = 1,024 bytes          │
│   1 MB = 1,000,000 bytes           1 MiB = 1,048,576 bytes      │
│   1 GB = 1,000,000,000 bytes       1 GiB = 1,073,741,824 bytes  │
│                                                                  │
│   Why the difference?                                           │
│   - Computers work in powers of 2: 2¹⁰ = 1024                   │
│   - Humans prefer powers of 10: 10³ = 1000                      │
│   - Marketing uses decimal (bigger-looking numbers!)            │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### DevOps Application: Kubernetes Memory Units

```yaml
# Kubernetes uses BINARY units for memory!
resources:
  limits:
    memory: "512Mi"    # Mi = Mebibytes (binary: 2²⁰ × 512)
    memory: "1Gi"      # Gi = Gibibytes (binary: 2³⁰)

# Can also use decimal:
    memory: "500M"     # M = Megabytes (decimal: 10⁶ × 500)
    memory: "1G"       # G = Gigabytes (decimal: 10⁹)

# Best practice: Use Mi/Gi (binary) for clarity
```

### Why This Matters

When you buy a "500 GB" hard drive:
- Marketing says: 500,000,000,000 bytes
- Computer sees: 500,000,000,000 ÷ 1,073,741,824 = ~465 GiB
- You "lose" ~35 GB!

**This is NOT a scam** - it's just different measurement systems.

---

## Part 7: What Can Different Bit Sizes Store?

```
┌────────────────────────────────────────────────────────────────┐
│                    BIT SIZE CAPABILITIES                        │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│   Bits │ Possible Values │ Range        │ Common Use           │
│   ─────┼─────────────────┼──────────────┼───────────────────── │
│    1   │ 2               │ 0-1          │ True/False, Yes/No   │
│    2   │ 4               │ 0-3          │ DNA bases (A,T,G,C)  │
│    4   │ 16              │ 0-15         │ Single hex digit     │
│    8   │ 256             │ 0-255        │ ASCII char, RGB each │
│   16   │ 65,536          │ 0-65,535     │ Unicode BMP, ports   │
│   32   │ 4.3 billion     │ 0-4294967295 │ IPv4 address, int    │
│   64   │ 18 quintillion  │ Huge!        │ Modern integers      │
│                                                                 │
│   Formula: n bits can store 2ⁿ different values               │
│                                                                 │
└────────────────────────────────────────────────────────────────┘
```

### DevOps Examples:

**IPv4 Addresses (32 bits):**
```
IP: 192.168.1.1

Each number (octet) is 8 bits (0-255):
192 = 11000000
168 = 10101000
  1 = 00000001
  1 = 00000001

Full binary: 11000000.10101000.00000001.00000001
Total: 32 bits = 4 bytes
Max possible IPs: 2³² = ~4.3 billion (why we need IPv6!)
```

**Port Numbers (16 bits):**
```
Ports range from 0 to 65,535
Why? Because 16 bits can store 2¹⁶ = 65,536 values

Well-known ports: 0-1023 (HTTP=80, HTTPS=443, SSH=22)
Registered ports: 1024-49151
Dynamic ports: 49152-65535
```

---

# SECTION D: HEXADECIMAL

---

## Part 8: What is Hexadecimal?

**Hexadecimal (hex)** = Base-16 number system

Binary is hard for humans to read (too many digits). Hex is a shorthand:

```
┌────────────────────────────────────────────────────────────────┐
│                      HEXADECIMAL DIGITS                         │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│   Decimal │ Binary │ Hex    Decimal │ Binary │ Hex             │
│   ────────┼────────┼─────   ────────┼────────┼─────            │
│      0    │  0000  │  0        8    │  1000  │  8              │
│      1    │  0001  │  1        9    │  1001  │  9              │
│      2    │  0010  │  2       10    │  1010  │  A              │
│      3    │  0011  │  3       11    │  1011  │  B              │
│      4    │  0100  │  4       12    │  1100  │  C              │
│      5    │  0101  │  5       13    │  1101  │  D              │
│      6    │  0110  │  6       14    │  1110  │  E              │
│      7    │  0111  │  7       15    │  1111  │  F              │
│                                                                 │
│   Hex uses: 0,1,2,3,4,5,6,7,8,9,A,B,C,D,E,F (16 symbols)      │
│                                                                 │
└────────────────────────────────────────────────────────────────┘
```

### Why Hexadecimal?

Each hex digit = exactly 4 binary bits!

```
Binary:  1111 0011 1010 0101
Hex:       F    3    A    5

Much easier to read and write!

Instead of: 1111001110100101 (16 digits)
Write:      F3A5 (4 digits)
```

### Converting Binary ↔ Hexadecimal

**Binary to Hex: Group by 4 bits**

```
Convert 11010110 to hex:

Step 1: Split into groups of 4 (from right):
        1101  0110

Step 2: Convert each group:
        1101 = 13 = D
        0110 = 6  = 6

Answer: 11010110 = D6 (hex)
```

**Hex to Binary: Expand each digit to 4 bits**

```
Convert A7 to binary:

A = 10 = 1010
7 = 7  = 0111

Answer: A7 = 10100111
```

### Hexadecimal Notation

Different contexts use different prefixes:

```
┌─────────────────────────────────────────────────────────────────┐
│                    HEX NOTATION STYLES                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│   0x1A2B    ← Programming (C, Python, JavaScript, etc.)         │
│   #FF5733   ← Web colors (CSS, HTML)                            │
│   1A2Bh     ← Assembly language                                 │
│   \x1A      ← Escape sequences in strings                       │
│   %20       ← URL encoding (space = %20)                        │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## Part 9: Hexadecimal in the Real World

### Color Codes (RGB)

```
Web colors use hex:

#FF5733

FF = Red component   (255 in decimal, maximum red)
57 = Green component (87 in decimal, some green)
33 = Blue component  (51 in decimal, little blue)

Result: An orange color!

┌────────────────────────────────────────┐
│  Common colors:                        │
│                                        │
│  #FFFFFF = White (all max)             │
│  #000000 = Black (all zero)            │
│  #FF0000 = Pure Red                    │
│  #00FF00 = Pure Green                  │
│  #0000FF = Pure Blue                   │
│  #FFFF00 = Yellow (Red + Green)        │
│                                        │
└────────────────────────────────────────┘
```

### MAC Addresses

```
Network card identifier: 00:1A:2B:3C:4D:5E

6 bytes (48 bits) in hex, colon-separated
Each pair is one byte: 00, 1A, 2B, 3C, 4D, 5E
```

### Memory Addresses

```
When debugging, you'll see:

Segmentation fault at address 0x7fff5fbff8c0

This hex number is a memory location.
In 64-bit systems: up to 16 hex digits (64 bits)
```

### DevOps: Docker and Container IDs

```
Container ID: a3b2c1d4e5f6

Docker uses hex for IDs to keep them short but unique.
Full ID: a3b2c1d4e5f67890abcdef1234567890abcdef12
Short ID: a3b2c1d4e5f6 (first 12 characters)
```

---

# SECTION E: TEXT REPRESENTATION (ASCII & UNICODE)

---

## Part 10: How Computers Store Text

Computers only understand numbers. So how do they store letters?

**Answer:** Every character has a number code!

### ASCII (American Standard Code for Information Interchange)

Created in 1963, ASCII uses 7 bits (128 characters):

```
┌────────────────────────────────────────────────────────────────┐
│                        ASCII TABLE (Selection)                  │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│   Dec │ Hex │ Char    Dec │ Hex │ Char    Dec │ Hex │ Char     │
│   ────┼─────┼──────   ────┼─────┼──────   ────┼─────┼──────    │
│    32 │ 20  │ SPACE    65 │ 41  │  A       97 │ 61  │  a       │
│    33 │ 21  │  !       66 │ 42  │  B       98 │ 62  │  b       │
│    34 │ 22  │  "       67 │ 43  │  C       99 │ 63  │  c       │
│    48 │ 30  │  0       68 │ 44  │  D      100 │ 64  │  d       │
│    49 │ 31  │  1       69 │ 45  │  E      101 │ 65  │  e       │
│    50 │ 32  │  2       ...                                      │
│    ...                 90 │ 5A  │  Z      122 │ 7A  │  z       │
│                                                                 │
│   Key patterns:                                                 │
│   - 'A' = 65, 'B' = 66... (consecutive)                        │
│   - 'a' = 97, 'b' = 98... (also consecutive)                   │
│   - 'a' - 'A' = 32 (difference between upper/lower)            │
│   - '0' = 48, '1' = 49... (digit characters)                   │
│                                                                 │
└────────────────────────────────────────────────────────────────┘
```

### How "Hello" is Stored

```
Text: H    e    l    l    o
     ─┬─  ─┬─  ─┬─  ─┬─  ─┬─
Dec:  72  101  108  108  111
Hex:  48   65   6C   6C   6F
Bin:  01001000 01100101 01101100 01101100 01101111

In memory (hex): 48 65 6C 6C 6F
```

### ASCII Control Characters

```
First 32 codes (0-31) are "control characters":

Code │ Name       │ Use
─────┼────────────┼─────────────────────────────
  0  │ NUL        │ Null (end of string in C)
  9  │ TAB        │ Horizontal tab
 10  │ LF (\\n)   │ Line Feed (Unix newline)
 13  │ CR (\\r)   │ Carriage Return (Windows uses \\r\\n)
 27  │ ESC        │ Escape (terminal sequences)

This is why Windows text files sometimes show extra characters
on Linux - different newline representations!
```

---

## Part 11: Unicode - Beyond ASCII

### The Problem with ASCII

ASCII only has 128 characters - enough for English, but what about:
- Chinese (你好) - thousands of characters
- Arabic (مرحبا) - right-to-left scripts
- Emoji (😀) - modern communication

### Unicode: The Universal Character Set

```
┌────────────────────────────────────────────────────────────────┐
│                    UNICODE OVERVIEW                             │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│   - Created in 1991                                            │
│   - Supports 1,112,064 possible characters                     │
│   - Currently defines ~150,000 characters                      │
│   - Includes every language, emoji, symbol, etc.               │
│                                                                 │
│   Unicode represents characters as "code points":              │
│   - U+0041 = 'A' (same as ASCII 65)                           │
│   - U+4E2D = '中' (Chinese character)                          │
│   - U+1F600 = '😀' (Grinning face emoji)                       │
│                                                                 │
└────────────────────────────────────────────────────────────────┘
```

### UTF-8: The Dominant Encoding

Unicode is the CHARACTER SET (which numbers = which characters)
UTF-8 is an ENCODING (how to store those numbers in bytes)

```
┌────────────────────────────────────────────────────────────────┐
│                      UTF-8 ENCODING                             │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│   Character Range      │ Bytes │ Example                       │
│   ─────────────────────┼───────┼───────────────────────────────│
│   U+0000 to U+007F     │   1   │ A, B, 1, 2, ! (ASCII)        │
│   U+0080 to U+07FF     │   2   │ é, ñ, ü (Latin extended)     │
│   U+0800 to U+FFFF     │   3   │ 中, 日, 한 (Asian scripts)    │
│   U+10000 to U+10FFFF  │   4   │ 😀, 🎉, 🚀 (Emoji)            │
│                                                                 │
│   Key advantage: ASCII text is valid UTF-8!                    │
│   (Backward compatible)                                        │
│                                                                 │
└────────────────────────────────────────────────────────────────┘
```

### Example: Storing Different Characters

```
Character: A
- Unicode: U+0041
- UTF-8: 41 (1 byte, same as ASCII)

Character: é
- Unicode: U+00E9
- UTF-8: C3 A9 (2 bytes)

Character: 中
- Unicode: U+4E2D
- UTF-8: E4 B8 AD (3 bytes)

Character: 😀
- Unicode: U+1F600
- UTF-8: F0 9F 98 80 (4 bytes)
```

### DevOps Implications

```bash
# Always specify encoding in scripts and configs!

# Python 3 (default is UTF-8)
# -*- coding: utf-8 -*-

# HTML
<meta charset="UTF-8">

# MySQL
CREATE DATABASE mydb CHARACTER SET utf8mb4;

# Bash (set locale)
export LANG=en_US.UTF-8

# Why utf8mb4 in MySQL?
# MySQL's "utf8" only supports 3-byte characters (no emoji!)
# utf8mb4 supports full 4-byte Unicode including emoji
```

---

# SECTION F: NEGATIVE NUMBERS AND FLOATING POINT

---

## Part 12: Representing Negative Numbers

How do you store -5 when you only have 0s and 1s?

### Two's Complement (The Standard Method)

```
In 8-bit Two's Complement:

Positive numbers: Normal binary (0 to 127)
Negative numbers: Flip all bits, add 1

Example: Represent -5

Step 1: Start with +5
        00000101

Step 2: Flip all bits (one's complement)
        11111010

Step 3: Add 1 (two's complement)
        11111011

So -5 = 11111011

How to verify: Add -5 + 5
  11111011  (-5)
+ 00000101  (+5)
──────────
 100000000  = 0 (ignore the overflow bit!)
```

### Why Two's Complement?

```
┌────────────────────────────────────────────────────────────────┐
│   The beauty of Two's Complement:                              │
│                                                                 │
│   - Same addition circuit works for positive AND negative      │
│   - No "negative zero" problem                                 │
│   - Easy to detect sign: leftmost bit = 1 means negative       │
│                                                                 │
│   8-bit range: -128 to +127                                    │
│   16-bit range: -32,768 to +32,767                            │
│   32-bit range: -2,147,483,648 to +2,147,483,647              │
│                                                                 │
└────────────────────────────────────────────────────────────────┘
```

### Integer Overflow (Bug!)

```
What happens when you exceed the range?

8-bit signed max is 127...
127 = 01111111

Add 1:
  01111111
+ 00000001
──────────
  10000000 = -128 (WRAPPED AROUND!)

This is called INTEGER OVERFLOW.
127 + 1 = -128 (not 128!)

This has caused real bugs and security vulnerabilities!
```

---

## Part 13: Floating Point Numbers (Decimals)

How do computers store 3.14159?

### IEEE 754 Floating Point Standard

```
A 32-bit float has 3 parts:

┌───────┬─────────────────┬─────────────────────────────────────┐
│ Sign  │    Exponent     │              Mantissa               │
│ 1 bit │    8 bits       │              23 bits                │
└───────┴─────────────────┴─────────────────────────────────────┘

Like scientific notation: ± M × 2^E

Sign: 0 = positive, 1 = negative
Exponent: Controls magnitude (how big/small)
Mantissa: The significant digits
```

### Why Floating Point Can Be Imprecise

```python
# In Python (or any language):
>>> 0.1 + 0.2
0.30000000000000004    # NOT exactly 0.3!

Why? 
- 0.1 in decimal is an infinite repeating fraction in binary
- Like 1/3 = 0.333... in decimal
- Computer truncates, causing small errors
```

### DevOps Implication: Money Calculations

```
NEVER use floating point for money!

$19.99 + $0.01 might equal $19.999999999999...

Solutions:
- Store as cents (integer): 1999 + 1 = 2000 = $20.00
- Use decimal/numeric database types
- Use BigDecimal (Java) or Decimal (Python) classes
```

---

# SECTION G: HOW FILES ARE STORED

---

## Part 14: Everything is Binary

Every file on your computer is just binary data. The file extension tells programs HOW to interpret those bytes.

### Text Files

```
A .txt file contains raw text bytes:

File: hello.txt
Content: "Hi"

Bytes: 48 69 (hex)
       H  i  (ASCII)

No special formatting - just character codes.
```

### Image Files

```
A .png or .jpg stores pixel colors as bytes:

Simplified example (uncompressed):

Pixel (255, 128, 0) = Orange
Stored as: FF 80 00

A 1920×1080 image = 1920 × 1080 × 3 bytes = ~6 MB (uncompressed)
Compression (PNG, JPEG) reduces this significantly.
```

### Executable Files

```
A .exe file contains machine code (CPU instructions):

When you run a program, the OS:
1. Reads the binary file
2. Loads it into RAM
3. Tells CPU to start executing from the first instruction

The CPU reads bytes as instructions:
B8 01 00 00 00 = MOV EAX, 1 (assembly instruction)
```

### DevOps: Binary vs Text Config Files

```
TEXT-based (human readable):
- .yaml, .json, .xml, .ini, .conf
- Can edit with any text editor
- Git can show meaningful diffs

BINARY (machine optimized):
- .sqlite, .db, compiled configs
- Smaller, faster to parse
- Git can't show useful diffs

Best practice: Use text-based configs for version control.
```

---

# SECTION H: DEVOPS APPLICATIONS

---

## Part 15: Binary in DevOps Work

### Base64 Encoding

Sometimes you need to put binary data in text (like JSON or YAML):

```
Binary data can't go in text directly (might have null bytes, etc.)
Solution: Base64 encodes binary as safe text characters

Example:
Binary: 48 65 6C 6C 6F (Hello)
Base64: SGVsbG8=

# Kubernetes secrets are Base64 encoded:
apiVersion: v1
kind: Secret
data:
  password: cGFzc3dvcmQxMjM=    # Base64 of "password123"
```

### Bitwise Operations in Networking

```
Subnet masks use binary AND:

IP:      192.168.1.100
         11000000.10101000.00000001.01100100

Mask:    255.255.255.0 (/24)
         11111111.11111111.11111111.00000000

AND:     11000000.10101000.00000001.00000000
         = 192.168.1.0 (Network address)

This is how routers determine if IPs are on the same network!
```

### File Permissions (Octal/Binary)

```
Linux permissions are binary flags:

rwxr-xr-x = 755

r w x   r - x   r - x
1 1 1   1 0 1   1 0 1
  7       5       5

Each group of 3 bits = 1 octal digit
chmod 755 file.sh = rwxr-xr-x
chmod 644 file.txt = rw-r--r--
```

---

## Part 16: Quick Reference

```
┌─────────────────────────────────────────────────────────────────┐
│                      QUICK REFERENCE                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│   CONVERSIONS:                                                  │
│   • Binary → Decimal: Add place values where bit = 1           │
│   • Decimal → Binary: Divide by 2, read remainders up          │
│   • Binary → Hex: Group by 4 bits, convert each group          │
│   • Hex → Binary: Expand each hex digit to 4 bits              │
│                                                                  │
│   UNITS:                                                        │
│   • 1 byte = 8 bits                                            │
│   • 1 KB = 1,000 bytes (decimal) or 1 KiB = 1,024 (binary)     │
│   • Kubernetes: Mi = Mebibytes, Gi = Gibibytes (binary)        │
│                                                                  │
│   TEXT:                                                         │
│   • ASCII: 7-bit, 128 chars, English only                      │
│   • Unicode: 1M+ chars, all languages                          │
│   • UTF-8: Variable width (1-4 bytes), backward compatible     │
│                                                                  │
│   NUMBERS:                                                      │
│   • Unsigned: 8 bits = 0 to 255                                │
│   • Signed: 8 bits = -128 to 127 (two's complement)            │
│   • Floating point: Approximate, not exact!                    │
│                                                                  │
│   HEX NOTATION:                                                 │
│   • 0xFF (programming), #FF5733 (colors), \xFF (strings)       │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## Key Takeaways

1. **Computers use binary because electronics have ON/OFF states**
2. **Each hex digit = 4 binary bits** (easier to read and write)
3. **1 byte = 8 bits** = 256 possible values
4. **ASCII uses 7 bits** for English; **Unicode/UTF-8** for everything
5. **Negative numbers use two's complement** (flip bits + 1)
6. **Floating point is approximate** - don't use for money!
7. **Everything is binary** - file type determines interpretation
8. **Base64 encodes binary as text** (used in K8s secrets)
9. **IP subnetting uses binary AND operations**
10. **File permissions are binary flags** (rwx = 111 = 7)

---

## 📝 Self-Check Questions

Before moving on, make sure you can answer:

1. Why do computers use binary instead of decimal?
2. Convert 45 to binary.
3. Convert binary 10110011 to decimal.
4. Convert binary 11110101 to hexadecimal.
5. How many values can 8 bits represent?
6. What's the difference between KB and KiB?
7. What is the ASCII code for 'A'?
8. Why can't 0.1 + 0.2 = 0.3 exactly in computers?
9. How is -5 represented in 8-bit two's complement?
10. What does UTF-8 stand for and why is it preferred?

---

*Next: Complete the exercises, then move to Topic 03: Memory and Storage*
