# Module 01 — How the computer represents things

**Goal:** understand that everything inside the computer (number, text, image, program) is
a sequence of bytes, and that the meaning depends on who interprets it.

**Prerequisites:** module 00 (lab working).

**Why it matters for the course:** almost every attack exploits a difference in
interpretation. The attacker sends bytes that one side reads as data and the other runs as
a command, or that the validation reads as an image and the server runs as a script.
Whoever sees the bytes behind the meaning sees these gaps.

---

## Lesson 1.1 — Everything is a number: bits, bytes and hexadecimal

**Anchor concept:** the computer stores only bits (0 and 1), grouped into bytes of 8 bits,
worth 0 to 255. Hexadecimal is just a compact way to write bytes: two hex digits are one
byte.

### Opening

1. If the computer only understands 0 and 1, how does it store the number 200?
   - A good answer contains: some idea of a combination of 0s and 1s in positions, each
     position with a weight. No need to do the math.
2. With 8 switches (on or off), how many different combinations can you make?
   - A good answer contains: 256 (2⁸), or the reasoning of doubling with each switch. If
     the student lands on "a lot", climb the ladder until they find 256.
3. Why do you think programmers write `FF` instead of `11111111`?
   - A good answer contains: it is shorter and easier to read. Each hex digit represents
     4 bits.

### Mission

With Claude, the student builds a converter in Python: it receives a number from 0 to 255
and shows the number in decimal, binary (8 digits) and hexadecimal (2 digits).

Specification questions:
1. What does the program do if it receives 300? And −1? And "abc"?
   - A good answer contains: an explicit decision for inputs out of range, such as
     refusing with a message.
2. How should the output look on screen?
   - A good answer contains: a concrete example of the output, such as
     `200 = 11001000 = C8`.
3. Which numbers will you use to test, and why those?
   - A good answer contains: edge cases, such as 0, 255 and one in the middle. If the
     student picks only "normal" numbers, ask what happens at the ends.

### Verification

1. Before running: what is the binary of 255? And of 128? Then check in the program.
   - A good answer contains: `11111111` and `10000000`, or correct reasoning even with an
     arithmetic slip.
2. Why is 255 the largest number that fits in a byte?
   - A good answer contains: there are 8 bits, all on; 256 combinations, counting from
     zero.
3. What happens to 255 + 1 if the result has to fit in a byte? Ask Claude how to test
   this in Python and explain the result.
   - A good answer contains: the value "wraps around" to 0 (overflow). Python does not
     limit integers, so the test has to force a byte, for example with `% 256` or
     `bytes([256])`, which raises an error. The student must explain the difference
     between the two.

### Tool

The system calculator in programmer mode, and the command `printf '%x\n' 200` in the
shell. Question: "Now that you built the converter, what does the calculator in programmer
mode do that your program also does?"

### Explain back

"Explain what a byte is and why hexadecimal exists." Criterion: 8 bits, values from 0 to
255, and hex as a compact form, with two digits per byte.

### For Socrates

- **Common mistakes:** thinking hexadecimal is "another data type". It is just another way
  to write the same number. Ask: "Are C8 and 200 different numbers?"
- **Bridge to security:** integer overflow has caused real vulnerabilities; memory dumps,
  hashes and keys are read in hex (modules 2.2 and 24).

---

## Lesson 1.2 — Text is a number too: encoding

**Anchor concept:** text is stored as numbers, through an encoding table (ASCII, UTF-8).
The same byte can become different letters depending on the table used to read it.

### Opening

1. If everything is a number, how does the computer store the letter "A"?
   - A good answer contains: some idea of a table that maps each letter to a number.
2. Have you ever seen text with "Ã§" where there should be "ç"? What do you think
   happened?
   - A good answer contains: the text was saved one way and read another. The word
     "encoding" is not required.

### Mission

With Claude, the student builds a program that receives a word and shows, for each
character, the character and the bytes that represent it in UTF-8, in hex.

Specification questions:
1. Which test word will you use, and why that one?
   - A good answer contains: a word with an accent or a "ç". If the student picks only
     unaccented letters, ask what happens with "ação" (Portuguese for "action": 4
     characters, two of them accented).
2. In what format does the output show each character?
   - A good answer contains: an example, such as `ç -> C3 A7`.

### Verification

1. Before running with "ação": how many bytes do you predict? Run it and compare.
   - A good answer contains: a prediction; then the observation that accented letters
     take 2 bytes in UTF-8, so it is 6 bytes for 4 characters.
2. Ask Claude to read the bytes of "ação" as if they were Latin-1 (another table). What
   shows up, and why?
   - A good answer contains: "aÃ§Ã£o", because each byte was read as a separate character
     in the other table. It is the explanation for the "Ã§" from the Opening.
3. Is a password "ação" typed on a UTF-8 system and checked on a Latin-1 system the same
   password?
   - A good answer contains: no; the bytes compared are different. Or the student notices
     it depends on how each side converts, which is already a good intuition.

### Tool

The `xxd` command (or `hexdump -C`): `echo -n "ação" | xxd`. Question: "What did `xxd`
show that your program also shows?"

### Explain back

"Explain why 'Ã§' sometimes shows up where 'ç' should be." Criterion: text becomes bytes
through a table; saving with one table and reading with another swaps the characters.

### For Socrates

- **Common mistakes:** thinking a character is always one byte. Verification question 1
  undoes this.
- **Bridge to security:** different encodings are used to bypass filters (a filter looks
  for `<script>` and the attacker sends the same text encoded another way). Comes back in
  injection (26) and XSS (28.2).

---

## Lesson 1.3 — Files and formats: the extension lies

**Anchor concept:** a file is just a sequence of bytes. What tells the real type is the
first bytes (the signature, or *magic bytes*); the extension in the name is just a label
anyone can change.

### Opening

1. If you rename `photo.png` to `photo.txt`, does the image become text?
   - A good answer contains: no, only the name changed; the content stays the same.
2. So how can a program know a file is an image without looking at the name?
   - A good answer contains: by looking at the content. If the student gets to "something
     at the start of the file", great.

### Mission

With Claude, the student builds a mini file identifier: it reads the first bytes of a
file, shows those bytes in hex and says whether the file is PNG, PDF, ZIP or "unknown",
by comparing with the signatures.

Specification questions:
1. How many bytes from the start will you read, and why?
   - A good answer contains: a justified number, such as "8, because the PNG signature is
     8 bytes". The student may ask Claude for the signatures, but must decide how many
     bytes to read.
2. What does the program do with an empty file, or one that does not exist?
   - A good answer contains: an explicit decision.
3. Which files will you use to test?
   - A good answer contains: one of each type, plus one with its extension changed.

### Verification

1. Rename a PNG to `.pdf` and run the identifier. What do you predict?
   - A good answer contains: the program says PNG, because it looks at the bytes and not
     the name.
2. Now create a text file that starts with the bytes of the PNG signature and has anything
   after them. What does the identifier say? Is it right?
   - A good answer contains: it says PNG and it is wrong; the signature can be faked too.
     The first bytes are a clue, not proof.
3. A site accepts uploads of "images only" and checks only the extension. What does an
   attacker do?
   - A good answer contains: sends a dangerous file (a script, for example) with an image
     extension. Even better if the student says that checking only the magic bytes is not
     enough either.

### Tool

The `file` command: `file photo.png`. Question: "Does `file` look at the name or the
bytes? How would you test that?" The student tests it with the renamed file.

### Explain back

"Explain why trusting a file's extension is dangerous." Criterion: the extension is just a
name and can be changed; the type is in the bytes; and even the bytes can be forged.

### For Socrates

- **Common mistakes:** concluding that magic bytes solve everything. Verification question
  2 exists to undo this.
- **Bridge to security:** upload validation, polyglot files (valid in two formats at the
  same time), phishing attachments. Comes back in application security (Phase 6).

---

## Lesson 1.4 — From code to program: compiled and interpreted

**Anchor concept:** the processor only runs machine instructions (bytes). A compiler
translates the source code into those instructions before running; an interpreter reads
the code and runs it as it reads. In both cases, what runs is what the processor receives,
not what is written in the source code.

### Opening

1. You wrote `print("hi")` in Python. Does the processor understand that line?
   - A good answer contains: not directly; something translates it into what the processor
     understands.
2. What is the difference between a translator who translates a whole book beforehand and
   an interpreter who translates a conversation live?
   - A good answer contains: one does everything first and delivers it ready; the other
     translates while it happens. It is the analogy for compiled and interpreted.

### Mission

With Claude, the student writes the same small program in two languages, C and Python
(add two numbers and show the result). Compiles the C one with `gcc` and runs both.

Specification questions:
1. What exactly must the two programs do for the comparison to hold?
   - A good answer contains: the same behavior, with the same input and the same output.
2. After compiling the C, which files do you expect to exist in the folder?
   - A good answer contains: the `.c` source and a new executable.

### Verification

1. Open the C executable with `xxd | head`. What do you see? Can you read the source code
   there?
   - A good answer contains: bytes, mostly unreadable, maybe some loose text; the source
     code is not there. If the student notices `ELF` at the start, connect it to the magic
     bytes from lesson 1.3.
2. Delete the `.c` and run the executable. Does it work? And if you delete the `.py`, does
   the Python program run?
   - A good answer contains: the executable runs without the source; Python needs the
     `.py` and the interpreter.
3. If someone sends you only an executable, how do you know what it does?
   - A good answer contains: you cannot tell just by looking at the name; you would have
     to analyze the bytes or run it in an isolated environment. Connect it to the lab from
     module 00.

### Tool

The `strings` command (shows the readable text inside a binary) and `file` on the
executable. Question: "What does `strings` tell you about an unknown executable, and what
does it not tell you?"

### Explain back

"Explain the difference between compiled and interpreted, and why receiving an unknown
executable is risky." Criterion: compiled is translated beforehand and runs without the
source; interpreted needs the source and the interpreter; an executable does not show what
it does.

### For Socrates

- **Common mistakes:** thinking Python "is not compiled at all" (it generates bytecode,
  the `.pyc`). Only go deeper if the student asks; the anchor concept does not depend on
  it.
- **Bridge to security:** malware analysis, `strings` as a first triage, supply chain (is
  the binary you downloaded the same one that was compiled from the source?). Comes back in
  30 (supply chain) and 39.3 (models and plugins).
