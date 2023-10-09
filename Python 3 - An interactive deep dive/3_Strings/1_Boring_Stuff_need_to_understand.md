# Some Boring Stuff You Need To Understand Before You Can Dive In

- Every piece of text you’ve ever seen on a computer screen is actually stored in a particular **character encoding.** Very roughly speaking, the character encoding provides a mapping between the stuff you see on your screen and the stuff your computer actually stores in memory and on disk.

- Many characters are common to multiple encodings, but each encoding may use a different sequence of bytes to actually store those characters in memory or on disk. So you can think of the character encoding as a kind of decryption key. **Whenever someone gives you a sequence of bytes — a file, a web page, whatever — and claims it’s “text,” you need to know what character encoding they used so you can decode the bytes into characters.**

- Surely you’ve seen web pages like this, with strange question-mark-like characters where apostrophes should be. That usually means the page author didn’t declare their character encoding correctly, your browser was left guessing, and the result was a mix of expected and unexpected characters.

- For instance, you’re probably familiar with the ascii encoding, which stores English characters as numbers ranging from 0 to 127. (65 is capital “A”, 97 is lowercase “a”, &c.) English has a very simple alphabet, so it can be completely expressed in less than 128 numbers.

- Then there are languages like Chinese, Japanese, and Korean, which have so many characters that they require multiple-byte character sets. That is, each “character” is represented by a two-byte number from 0–65535.

- Well, systems had to be designed to carry encoding information along with every piece of “plain text.” Remember, it’s the decryption key that maps computer-readable numbers to human-readable characters. A missing decryption key means garbled text, gibberish, or worse.

- Now think about trying to store multiple pieces of text in the same place, like in the same database table that holds all the email you’ve ever received. You still need to store the character encoding alongside each piece of text so you can display it properly.