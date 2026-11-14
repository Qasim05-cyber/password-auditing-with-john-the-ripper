# Password Security Auditing with John the Ripper

I used John the Ripper on a sample password-hash file to compare a dictionary-based attack with a longer password-cracking session. My goal was to see how quickly common passwords could be recovered and what the results say about password strength.

All testing was performed locally against the sample hashes supplied for this exercise.

## Environment

- **System:** Windows, Command Prompt
- **Tool:** John the Ripper 1.9.0 Jumbo (64-bit)
- **Input:** `hackme.txt` (sample password hashes)
- **Wordlist:** `password.lst` (included with John the Ripper)

I verified that the executable, wordlist, and sample hash file were all in the `run` directory before starting.

![Verified John the Ripper files in Command Prompt](images/01_environment_verification.png)

## 1. Dictionary attack

I started by running:

```cmd
john.exe --wordlist=password.lst hackme.txt
```

John loaded **584 password hashes** and recovered **13 passwords** using the supplied wordlist. This showed how quickly a dictionary attack can find passwords that match known guesses.

![Dictionary attack output](images/02_dictionary_attack.png)

## 2. Additional password-cracking session

Next, I ran John without specifying a wordlist:

```cmd
john.exe hackme.txt
```

I let it run briefly, then stopped it with **Ctrl+C**. The output showed **59 passwords cracked during this session**, which lasted about **1 minute and 23 seconds**. John's default cracking behavior is not necessarily the same as a pure exhaustive brute-force attack.

![Second password-cracking session](images/03_password_cracking_session.png)

The screenshots mask the recovered sample passwords and usernames while preserving the result counts.

## 3. Verifying the results

I opened `john.pot` to check that John saved the recovered hashes and passwords. I kept that file and its screenshot out of the public repository because they contain recovered credentials, even though the data was provided for testing.

## What I found

The wordlist recovered some passwords quickly, while the second session found more candidates after additional guessing. A larger wordlist can improve coverage, but it does not automatically make cracking faster. Passwords that are longer, less predictable, and unique are harder to guess than common words or simple variations.

## What I learned

The biggest takeaway for me was how much password predictability matters. I could see the difference between checking a fixed list of guesses and letting John continue trying other candidates. I also learned how to verify the output rather than just relying on what the terminal displayed.

**Tools:** John the Ripper · Windows Command Prompt · Password hash auditing
