# 🚩 ReadMe: Operation 1337 Nitffler

**Competiție:** Security Summer School v13 - Calificări  
**Categorie:** Forensics  
**Dificultate:** Entry-Level  
**Autor:** ALISTAR Robert-Mihai  

---

## 1. Description

A packet capture (`.pcap`) file. The goal was to analyze network traffic to
identify and extract the hidden flag.

## 2. Information collection

The first thing I did was download the file. Recognizing the extension (`.pcap`) as
specific to network traffic, I decided to use Wireshark for analysis.

I opened the terminal and launched the application using the command:

```bash
wireshark captured.pcap
```

## 3. False leads

At first, I tried to manually parse each packet in the hope of finding the flag
directly in the data section. This approach was time-consuming and did not provide
any immediate results.


## 4. Exploitation

Upon closer inspection, I noticed that packet number 8 used the HTTP protocol 
and contained a GET request for a file named (`08347211akamai.tar.gz`). I realized 
that the flag could be extracted from this object transferred over the network:

1. In Wireshark, I went to the File -> Export Objects -> HTTP menu.
2. I selected the file (`08347211akamai.tar.gz`) from the list and saved it.
3. I went back to the terminal to unzip the file using the command:


```bash
tar -xvf 08347211akamai.tar.gz
```

4. After unzipping, a text file named flag.txt appeared.
5. I viewed the contents of the file to get the final code.

```bash
cat flag.txt
```


## 5. Flag
`SSS{prind_pachet_pe_retea}`

## 6. Conclusions / What I learned
This challenge highlighted the importance of monitoring unencrypted HTTP traffic. 
I learned to use Wireshark to identify and extract network objects, and I also
remembered the utility (`tar`) used for unzipping.
