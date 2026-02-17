# Topic 02: Exercises - Binary and Data Representation

Complete these exercises to reinforce your understanding.
Check your answers in `exercises-solutions.md` after completing.

---

## Exercise 1: Binary to Decimal Conversion

Convert these binary numbers to decimal:

| Binary | Your Answer | Work Space |
|--------|-------------|------------|
| 1010 | | |
| 1111 | | |
| 10101 | | |
| 11001100 | | |
| 10000001 | | |

---

## Exercise 2: Decimal to Binary Conversion

Convert these decimal numbers to binary:

| Decimal | Your Answer | Work Space |
|---------|-------------|------------|
| 7 | | |
| 25 | | |
| 42 | | |
| 100 | | |
| 255 | | |

---

## Exercise 3: Hexadecimal Conversions

### Part A: Binary to Hex

| Binary | Hex |
|--------|-----|
| 1111 | |
| 10101010 | |
| 11001111 | |
| 00001111 | |

### Part B: Hex to Binary

| Hex | Binary |
|-----|--------|
| A | |
| 3F | |
| C8 | |
| FF | |

### Part C: Hex to Decimal

| Hex | Decimal |
|-----|---------|
| 10 | |
| 2A | |
| FF | |
| 100 | |

---

## Exercise 4: Data Size Questions

1. How many bits in 3 bytes?
   
   Your answer: __________

2. How many different values can 4 bits represent?
   
   Your answer: __________

3. A file is 2 KiB. How many bytes is that exactly?
   
   Your answer: __________

4. An IPv4 address uses how many bits?
   
   Your answer: __________

5. What's the maximum port number and why?
   
   Your answer: __________

---

## Exercise 5: ASCII and Text

1. What is the ASCII decimal value for 'A'?
   
   Your answer: __________

2. What is the ASCII decimal value for 'a'?
   
   Your answer: __________

3. What is the difference between 'A' and 'a' in ASCII codes?
   
   Your answer: __________

4. The word "OK" stored in hexadecimal would be:
   
   Your answer: __________
   
   (Hint: O=79, K=75 in decimal)

5. Why can't ASCII store Chinese characters?
   
   Your answer: __________

---

## Exercise 6: UTF-8 and Unicode

1. How many bytes does UTF-8 use to store the letter 'A'?
   
   Your answer: __________

2. How many bytes does UTF-8 use to store a Chinese character?
   
   Your answer: __________

3. How many bytes does UTF-8 use to store an emoji 😀?
   
   Your answer: __________

4. In a MySQL database, why should you use `utf8mb4` instead of `utf8`?
   
   Your answer: __________

---

## Exercise 7: Two's Complement

Using 8-bit two's complement, answer:

1. What is the binary representation of -1?
   
   Your answer: __________
   
   Work:

2. What is the binary representation of -128?
   
   Your answer: __________

3. In 8-bit signed numbers, what is the range (min to max)?
   
   Your answer: __________

4. What happens if you add 1 to 127 in 8-bit signed arithmetic?
   
   Your answer: __________ Why? __________

---

## Exercise 8: Real-World Application

### Scenario A: Kubernetes Secret

You need to store the password "admin123" as a Kubernetes secret.

1. Why does Kubernetes require Base64 encoding for secrets?
   
   Your answer: __________

2. If "admin123" in Base64 is `YWRtaW4xMjM=`, what does this mean when someone says "Kubernetes secrets are not encrypted"?
   
   Your answer: __________

### Scenario B: IP Subnetting

Given:
- IP: 192.168.10.50
- Subnet mask: 255.255.255.0

1. Convert the last octet of the IP (50) to binary:
   
   Your answer: __________

2. What is the network address? (No need to calculate, just explain what operation is used)
   
   Your answer: __________

### Scenario C: File Permissions

1. What does `chmod 755` mean in binary?
   
   Owner: ___  ___  ___ (rwx)
   Group: ___  ___  ___ (rwx)
   Other: ___  ___  ___ (rwx)

2. What permissions does `chmod 644` give?
   
   Your answer: __________

---

## Exercise 9: Debugging Scenario

A developer complains that their test fails:

```python
price = 0.1 + 0.2
if price == 0.3:
    print("Price is correct")
else:
    print("Price is WRONG!")  # This prints!
```

1. Why does this code print "Price is WRONG!"?
   
   Your answer: __________

2. How would you fix this for a real e-commerce application?
   
   Your answer: __________

---

## Exercise 10: True or False

| # | Statement | T/F |
|---|-----------|-----|
| 1 | 1 KB always equals 1024 bytes | |
| 2 | Hexadecimal F equals decimal 16 | |
| 3 | ASCII is a subset of UTF-8 | |
| 4 | Every file on a computer is stored as binary | |
| 5 | A 32-bit integer can store any whole number | |
| 6 | Two's complement uses the leftmost bit as the sign | |
| 7 | UTF-8 always uses 4 bytes per character | |
| 8 | Port numbers can go up to 65535 | |

---

## Exercise 11: Fill In The Powers of 2

Complete without a calculator (memorize these!):

| Power | Value |
|-------|-------|
| 2⁰ | |
| 2¹ | |
| 2² | |
| 2³ | |
| 2⁴ | |
| 2⁵ | |
| 2⁶ | |
| 2⁷ | |
| 2⁸ | |
| 2¹⁰ | |

---

## Exercise 12: Color Codes

1. What color is #FF0000?
   
   Your answer: __________

2. What color is #00FF00?
   
   Your answer: __________

3. What hex code would give you yellow? (Hint: Red + Green)
   
   Your answer: __________

4. How many possible colors can be represented with 24-bit RGB?
   
   Your answer: __________

---

## Bonus Challenge

1. A container has a memory limit of "256Mi". How many bytes is this exactly?
   
   Calculation:
   
   Answer: __________

2. Why is the ASCII code for '0' (digit zero) not 0?
   
   Your answer: __________

3. What is "endianness" and why does it matter when transferring binary data between systems?
   
   Your answer: __________

---

## Self-Assessment

After completing exercises, rate your understanding:

| Concept | Confidence (1-5) |
|---------|-----------------|
| Binary conversion | |
| Hexadecimal | |
| Bits and bytes | |
| ASCII/Unicode | |
| Negative numbers (two's complement) | |
| Real-world applications | |

---

*After completing, check `exercises-solutions.md` for correct answers.*
