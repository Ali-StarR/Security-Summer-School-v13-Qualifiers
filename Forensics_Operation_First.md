# 🚩 ReadMe: Operation Last Read

**Competiție:** Security Summer School v13 - Calificări  
**Categorie:** Forensics  
**Dificultate:** Entry-Level  
**Autor:** ALISTAR Robert-Mihai  

---

## 1. Description
The goal of this challenge was to analyze a PDF document (`sssforensics.pdf`) to 
discover information or files hidden within it that hide the FLAG.

## 2. Information collection
I started by downloading the file `sssforensics.pdf`. My first approach was to
inspect the file for text strings that might resemble the flag format,using `grep`:

```bash
strings sssforensics.pdf | grep -i "SSS"
```

## 3. False leads
This first investigation returned 3 results of the form `SSS{nu_e_asta_flagul}`.
Later, I tried to analyze the file metadata, but I didn't find anything relevant:

```bash
exiftool sssforensics.pdf
```

I tried the `strings` command again, this time searching for the `=` character,
hoping to come across a Base64 encoded message:

```bash
strings sssforensics.pdf | grep -i "="
```

This trail also did not lead to the finding of the real flag.

## 4. Exploitation
Doing a little more research on hidden files, I realized that the PDF might
contain another file embedded in its structure. 
To check for and automatically extract any hidden files, I used the **Binwalk**
utility, followed by the `-e` parameter:

```bash
binwalk -e sssforensics.pdf
```

The command ran successfully and generated a new folder called 
`_sssforensics.pdf.extracted`. Navigating inside it, I discovered a hidden text
file called `pdf.txt`.

To read the file and get the final solution, I used the command:

```bash
cat pdf.txt
```

## 5. Flag
`SSS{poti_sa_te_ascunzi_dar_nu_te_poti_ascunde}`

## 6. Conclusions / What I learned
This challenge was a great exercise in resilience. I learned not to rely solely on
basic text analysis (`strings`) or metadata (`exiftool`). Discovering and using 
(`binwalk`) showed me how to quickly extract hidden data from seemingly normal 
files.
