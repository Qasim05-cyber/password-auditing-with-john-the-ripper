# Password Auditing with John the Ripper

I started with the wordlist that came with John the Ripper to see how far it could get on its own. The first pass was over almost as soon as I started it. That made me curious about how many more guesses would land if I let John keep going.

## What I found

- John loaded **584 password hashes** across **127 salts** and identified the format as `descrypt`.
- The built-in wordlist recovered **13 passwords**. Running the same list again recovered **zero** new ones, and John reported **571 hashes remaining** at that point.
- The default run recovered **59 more** in **1 minute and 23 seconds** before I stopped it. That put the two runs at **72 recoveries total**.

## Environment

| Tool or file | What I used it for |
| --- | --- |
| Windows Command Prompt | Ran the audit and checked the output |
| John the Ripper 1.9.0 Jumbo (64-bit) | Loaded the hashes and tested password guesses |
| `hackme.txt` | Sample password hashes supplied for the exercise |
| `password.lst` | The wordlist included with John |

I ran everything locally against the sample data.

## 1. Checking my setup

Before running anything, I used `dir john.exe password.lst hackme.txt` to make sure all three files were in the same `run` folder.

![Command Prompt showing the executable, wordlist, and sample hash file](01_environment_verification.png)

## 2. Trying the built-in wordlist

```cmd
john.exe --wordlist=password.lst hackme.txt
```

This was the result that caught my attention first. The included wordlist was enough to recover 13 passwords. I ran the same command again and got zero new results. Seeing both runs together made it easy to tell what the wordlist had actually added.

![Dictionary attack output showing 13 recoveries and zero new results on the rerun](02_dictionary_attack.png)

## 3. Letting John keep guessing

```cmd
john.exe hackme.txt
```

This time I left the mode unspecified and let John run with its default settings. I stopped it after 1 minute and 23 seconds, when the status line showed `59g`. I checked `john.pot` afterward to see what John had saved. The results screenshots show entries from the sample dataset.

![Default session output showing 59 recoveries before I stopped the run](03_password_cracking_session.png)

## What I would improve

Next time I'd give each mode the same time limit and start it with the same hash file and an empty results file. John saved the first 13 recoveries in `john.pot`, so the default run started with 571 hashes left to test. Starting both runs from scratch would show me how each mode does on its own.

## What I learned

Seeing the same wordlist go from 13 results to zero on a rerun made me pay closer attention to what John had already saved. Now I check both the status line and the saved results before I write down what a run found.

**Tools:** John the Ripper · Windows Command Prompt
