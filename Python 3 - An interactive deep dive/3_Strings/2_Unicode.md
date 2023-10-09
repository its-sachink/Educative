# Unicode

- Unicode is a system designed to represent every character from every language. Unicode represents each letter, character, or ideograph as a 4-byte number. Each number represents a unique character used in at least one of the world’s languages.

- Characters that are used in multiple languages generally have the same number, unless there is a good etymological reason not to. Regardless, there is exactly 1 number per character, and exactly 1 character per number. Every number always means just one thing; there are no “modes” to keep track of. U+0041 is always 'A', even if your language doesn’t have an 'A' in it.

- Four bytes? For every single character‽ That seems awfully wasteful, especially for languages like English and Spanish, which need less than one byte (256 numbers) to express every possible character.

- There is a Unicode encoding that uses four bytes per character. It’s called UTF-32, because 32 bits = 4 bytes. **UTF-32** is a straightforward encoding; it takes each Unicode character (a 4-byte number) and represents the character with that same number. **This has some advantages, the most important being that you can find the Nth character of a string in constant time, because the Nth character starts at the 4×Nth byte.** It also has several disadvantages, the most obvious being that it takes four freaking bytes to store every freaking character.

- **UTF-16 (because 16 bits = 2 bytes)**. UTF-16 encodes every character from 0–65535 as two bytes, then uses some dirty hacks if you actually need to represent the rarely-used “astral plane” Unicode characters beyond 65535. Most obvious advantage: UTF-16 is twice as space-efficient as UTF-32, because every character requires only two bytes to store instead of four bytes (except for the ones that don’t). And you can still easily find the Nth character of a string in constant time.

- To solve this problem, the multi-byte Unicode encodings define a “Byte Order Mark,” which is a special non-printable character that you can include at the beginning of your document to indicate what order your bytes are in. For UTF-16, the Byte Order Mark is U+FEFF. If you receive a UTF-16 document that starts with the bytes FF FE, you know the byte ordering is one way; if it starts with FE FF, you know the byte ordering is reversed.

- **UTF-8 is a variable-length encoding system for Unicode**:
</br>
    - different characters take up a different number of bytes. For ASCII characters (A-Z, &c.) UTF-8 uses just one byte per character. In fact, it uses the exact same bytes; the first 128 characters (0–127) in UTF-8 are indistinguishable from ASCII. “Extended Latin” characters like ñ and ö end up taking two bytes.
    - Disadvantages: because each character can take a different number of bytes, finding the Nth character is an O(N) operation — that is, the longer the string, the longer it takes to find a specific character.