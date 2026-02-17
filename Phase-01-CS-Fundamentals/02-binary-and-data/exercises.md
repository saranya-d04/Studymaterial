# Topic 02: Exercises - Binary and Data Representation

Complete these exercises to reinforce your understanding.

---

## Exercise 1: Binary to Decimal Conversion

Convert these binary numbers to decimal:

| Binary | Your Answer | Work Space |
|--------|-------------|------------|
| 1010 | 10| |
| 1111 |15 | |
| 10101 |21 | |
| 11001100 |2 04|128+64+12|
| 10000001 |129 | |

---

## Exercise 2: Decimal to Binary Conversion

Convert these decimal numbers to binary:

| Decimal | Your Answer | Work Space |
|---------|-------------|------------|
| 7 | 0111| |
| 25 |11001 | |
| 42 |1010100 | |
| 100 |1100100 | |
| 255 | 100001111| |

---

## Exercise 3: Hexadecimal Conversions

### Part A: Binary to Hex

| Binary | Hex |
|--------|-----|
| 1111 | F|
| 10101010 | AA|
| 11001111 |CF |
| 00001111 |0F |

### Part B: Hex to Binary

| Hex | Binary |
|-----|--------|
| A |1010 |
| 3F |00111111 |
| C8 | 11001000|
| FF | 11111111|

### Part C: Hex to Decimal

| Hex | Decimal |
|-----|---------|
| 10 |16 |
| 2A | 42|
| FF | 255|
| 100 | 256|

---

## Exercise 4: Data Size Questions

1. How many bits in 3 bytes?
   
   Your answer: __24bits__________

2. How many different values can 4 bits represent?
   
   Your answer: ____1024 ,________

3. A file is 2 KiB. How many bytes is that exactly?
   
   Your answer: _____2 billion_______

4. An IPv4 address uses how many bits?
   
   Your answer: ___34_________

5. What's the maximum port number and why?
   
   Your answer: ____https is a maximum posrt 443________

---

## Exercise 5: ASCII and Text

1. What is the ASCII decimal value for 'A'?
   
   Your answer: ______65______

2. What is the ASCII decimal value for 'a'?
   
   Your answer: ______97______

3. What is the difference between 'A' and 'a' in ASCII codes?
   
   Your answer: ___A___the decimal number is 65 for A then decimal number is 97 for small a______

4. The word "OK" stored in hexadecimal would be:
   
   Your answer: _____4F 4B
_______
   
   (Hint: O=79, K=75 in decimal)

5. Why can't ASCII store Chinese characters?
   
   Your answer: _____the AscII store only the universal char the other alt UTF-8_______

---

## Exercise 6: UTF-8 and Unicode

1. How many bytes does UTF-8 use to store the letter 'A'?
   
   Your answer: ____A is a ASCII charater UTF-8 stores asscii in 1 byte________

2. How many bytes does UTF-8 use to store a Chinese character?
   
   Your answer: ____it is a unicode range that requires 3 bytes in 3 byte

3. How many bytes does UTF-8 use to store an emoji 😀?
   
   Your answer: ____________
4byte
4. In a MySQL database, why should you use `utf8mb4` instead of `utf8`?
   
   Your answer: ____________

---

## Exercise 7: Two's Complement

Using 8-bit two's complement, answer:

1. What is the binary representation of -1?
   
   Your answer: ____11111111________
   
   Work:

2. What is the binary representation of -128?
   
   Your answer: ____10000000________

3. In 8-bit signed numbers, what is the range (min to max)?
   
   Your answer: _____-128 to +127 _______

4. What happens if you add 1 to 127 in 8-bit signed arithmetic?
   
   Your answer: ____________ Why? ____________

---

## Exercise 8: Real-World Application

### Scenario A: Kubernetes Secret

You need to store the password "admin123" as a Kubernetes secret.

1. Why does Kubernetes require Base64 encoding for secrets?
   
   Your answer: __kubernetes store secrets as text in json,yaml so base64 ensures safe __________

2. If "admin123" in Base64 is `YWRtaW4xMjM=`, what does this mean when someone says "Kubernetes secrets are not encrypted"?
   
   Your answer: _____It means Base64 is encoding, not encryption — anyone can decode it easily._______

### Scenario B: IP Subnetting

Given:
- IP: 192.168.10.50
- Subnet mask: 255.255.255.0

1. Convert the last octet of the IP (50) to binary:
   
   Your answer: _____00110010
_______

2. What is the network address? (No need to calculate, just explain what operation is used)
   
   Your answer: ____Bitwise AND between IP and subnet mask
________

### Scenario C: File Permissions

1. What does `chmod 755` mean in binary?
   
   Owner: __111_  ___  ___ (rwx)
   Group: ___  101___  ___ (rwx)
   Other: ___  ___101  ___ (rwx)

2. What permissions does `chmod 644` give?
   
   Your answer: ___Owner → read + write
Group → read only
Other → read only_________

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
   
   Your answer: ____because it has a floating number________

2. How would you fix this for a real e-commerce application?
   
   Your answer: ______do not use decimal for the money calculation______

---

## Exercise 10: True or False

| # | Statement | T/F |
|---|-----------|-----|
| 1 | 1 KB always equals 1024 bytes | f|
| 2 | Hexadecimal F equals decimal 16 | f|
| 3 | ASCII is a subset of UTF-8 |t |
| 4 | Every file on a computer is stored as binary |t |
| 5 | A 32-bit integer can store any whole number |t |
| 6 | Two's complement uses the leftmost bit as the sign |t |
| 7 | UTF-8 always uses 4 bytes per character | f|
| 8 | Port numbers can go up to 65535 | f|

---

## Exercise 11: Fill In The Powers of 2

Complete without a calculator (memorize these!):

| Power | Value |
|-------|-------|
| 2⁰ |1 |
| 2¹ | 2|
| 2² | 4|
| 2³ | 8|
| 2⁴ | 16|
| 2⁵ | 32|
| 2⁶ | 64|
| 2⁷ |128 |
| 2⁸ |256 |
| 2¹⁰ | 1024|

---

## Exercise 12: Color Codes

1. What color is #FF0000?
   
   Your answer: ___red_________

2. What color is #00FF00?
   
   Your answer: _____green_______

3. What hex code would give you yellow? (Hint: Red + Green)
   
   Your answer: _____#FFFFF00_______

4. How many possible colors can be represented with 24-bit RGB?
   
   Your answer: _____RBG_______

---

## Bonus Challenge

1. A container has a memory limit of "256Mi". How many bytes is this exactly?
   
   Calculation:
   
   Answer: ____________

2. Why is the ASCII code for '0' (digit zero) not 0?
   
   Your answer: ____________

3. Research: What is "endianness" and why does it matter when transferring binary data between systems?
   
   Your answer: ____________

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

If any rating is below 3, re-read that section of the notes.

---

*Complete the exercises, then request the test from your instructor.*
