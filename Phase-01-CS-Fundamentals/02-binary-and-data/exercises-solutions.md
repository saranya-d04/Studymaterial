# Topic 02: Exercises with Solutions - Binary and Data Representation

---

## Exercise 1: Binary to Decimal Conversion

| Binary | Answer | Explanation |
|--------|--------|-------------|
| 1010 | **10** | 8+2 = 10 |
| 1111 | **15** | 8+4+2+1 = 15 |
| 10101 | **21** | 16+4+1 = 21 |
| 11001100 | **204** | 128+64+8+4 = 204 |
| 10000001 | **129** | 128+1 = 129 |

---

## Exercise 2: Decimal to Binary Conversion

| Decimal | Answer | Explanation |
|---------|--------|-------------|
| 7 | **111** | 4+2+1 |
| 25 | **11001** | 16+8+1 |
| 42 | **101010** | 32+8+2 |
| 100 | **1100100** | 64+32+4 |
| 255 | **11111111** | All 1s (2⁸-1) |

---

## Exercise 3: Hexadecimal Conversions

### Part A: Binary to Hex

| Binary | Answer | Explanation |
|--------|--------|-------------|
| 1111 | **F** | 15 in hex |
| 10101010 | **AA** | 1010=A, 1010=A |
| 11001111 | **CF** | 1100=C, 1111=F |
| 00001111 | **0F** | 0000=0, 1111=F |

### Part B: Hex to Binary

| Hex | Answer | Explanation |
|-----|--------|-------------|
| A | **1010** | 10 in binary |
| 3F | **00111111** | 3=0011, F=1111 |
| C8 | **11001000** | C=1100, 8=1000 |
| FF | **11111111** | F=1111, F=1111 |

### Part C: Hex to Decimal

| Hex | Answer | Explanation |
|-----|--------|-------------|
| 10 | **16** | 1×16 + 0 = 16 |
| 2A | **42** | 2×16 + 10 = 42 |
| FF | **255** | 15×16 + 15 = 255 |
| 100 | **256** | 1×256 = 256 |

---

## Exercise 4: Data Size Questions

1. **How many bits in 3 bytes?**
   - **24 bits** (3 × 8 = 24)

2. **How many different values can 4 bits represent?**
   - **16 values** (2⁴ = 16, values 0-15)

3. **A file is 2 KiB. How many bytes is that exactly?**
   - **2048 bytes** (2 × 1024 = 2048)

4. **An IPv4 address uses how many bits?**
   - **32 bits** (4 octets × 8 bits = 32)

5. **What's the maximum port number and why?**
   - **65535** - Port numbers use 16 bits (2¹⁶ - 1 = 65535)

---

## Exercise 5: ASCII and Text

1. **ASCII decimal value for 'A'?** → **65**

2. **ASCII decimal value for 'a'?** → **97**

3. **Difference between 'A' and 'a' in ASCII?**
   - **32** (97 - 65 = 32). Lowercase letters are 32 more than uppercase.

4. **"OK" in hexadecimal?**
   - **4F 4B** (O=79=0x4F, K=75=0x4B)

5. **Why can't ASCII store Chinese characters?**
   - ASCII only has 128 characters (7 bits), designed for English. Chinese has thousands of characters requiring Unicode/UTF-8.

---

## Exercise 6: UTF-8 and Unicode

1. **Bytes for letter 'A'?** → **1 byte** (ASCII characters use 1 byte in UTF-8)

2. **Bytes for Chinese character?** → **3 bytes** (Most CJK characters use 3 bytes)

3. **Bytes for emoji 😀?** → **4 bytes** (Emojis are in higher Unicode ranges)

4. **Why use `utf8mb4` instead of `utf8` in MySQL?**
   - MySQL's `utf8` only supports up to 3 bytes per character (no emojis). `utf8mb4` supports up to 4 bytes, including emojis.

---

## Exercise 7: Two's Complement

1. **Binary representation of -1?**
   - **11111111**
   - Work: Invert 00000001 → 11111110, add 1 → 11111111

2. **Binary representation of -128?**
   - **10000000**

3. **Range of 8-bit signed numbers?**
   - **-128 to +127**

4. **What happens if you add 1 to 127?**
   - **Integer overflow → becomes -128**
   - 01111111 + 1 = 10000000 = -128 in two's complement

---

## Exercise 8: Real-World Application

### Scenario A: Kubernetes Secret

1. **Why Base64 encoding?**
   - Kubernetes stores secrets in YAML/JSON which are text-based. Base64 safely encodes binary/special characters as printable text.

2. **What does "not encrypted" mean?**
   - Base64 is encoding, NOT encryption. Anyone can decode `YWRtaW4xMjM=` back to "admin123". For security, use external secret management.

### Scenario B: IP Subnetting

1. **50 in binary?** → **00110010**
   - 50 = 32 + 16 + 2

2. **How to get network address?**
   - **Bitwise AND** between IP address and subnet mask

### Scenario C: File Permissions

1. **chmod 755 in binary:**
   - Owner: **111** (rwx = 7)
   - Group: **101** (r-x = 5)
   - Other: **101** (r-x = 5)

2. **chmod 644 permissions:**
   - Owner: read + write (rw-)
   - Group: read only (r--)
   - Other: read only (r--)

---

## Exercise 9: Debugging Scenario

1. **Why "Price is WRONG!"?**
   - Floating-point precision issue. 0.1 and 0.2 cannot be exactly represented in binary, so 0.1 + 0.2 ≈ 0.30000000000000004

2. **Fix for e-commerce?**
   - Use integer cents (store 100 for $1.00) or use `decimal.Decimal` in Python for exact arithmetic.

---

## Exercise 10: True or False

| # | Statement | Answer | Explanation |
|---|-----------|--------|-------------|
| 1 | 1 KB always equals 1024 bytes | **F** | KB=1000, KiB=1024 |
| 2 | Hexadecimal F equals decimal 16 | **F** | F = 15 |
| 3 | ASCII is a subset of UTF-8 | **T** | First 128 UTF-8 chars are ASCII |
| 4 | Every file on a computer is stored as binary | **T** | All data is ultimately binary |
| 5 | A 32-bit integer can store any whole number | **F** | Limited to ±2 billion approx |
| 6 | Two's complement uses the leftmost bit as the sign | **T** | MSB indicates sign |
| 7 | UTF-8 always uses 4 bytes per character | **F** | Uses 1-4 bytes (variable) |
| 8 | Port numbers can go up to 65535 | **T** | 16-bit = 0-65535 |

---

## Exercise 11: Powers of 2

| Power | Answer |
|-------|--------|
| 2⁰ | **1** |
| 2¹ | **2** |
| 2² | **4** |
| 2³ | **8** |
| 2⁴ | **16** |
| 2⁵ | **32** |
| 2⁶ | **64** |
| 2⁷ | **128** |
| 2⁸ | **256** |
| 2¹⁰ | **1024** |

---

## Exercise 12: Color Codes

1. **#FF0000?** → **Red** (Full red, no green, no blue)

2. **#00FF00?** → **Green** (No red, full green, no blue)

3. **Yellow hex code?** → **#FFFF00** (Full red + full green)

4. **24-bit RGB colors?** → **16,777,216** (2²⁴ = 16,777,216)

---

## Bonus Challenge Solutions

1. **256Mi in bytes?**
   - 256 × 1024 × 1024 = **268,435,456 bytes**

2. **Why isn't ASCII '0' equal to 0?**
   - ASCII codes 0-31 are control characters. Printable characters start at 32. '0' is at position 48.

3. **What is endianness?**
   - Byte order in multi-byte data. Big-endian stores MSB first, little-endian stores LSB first. Matters when transferring binary data between different architectures (x86 is little-endian, network protocols often use big-endian).

---

*These are the correct answers for self-checking after completing exercises.*
