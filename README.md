# Hashing-TextFile-with-OpenSSL

## Objectives
Part 1: Hashing a Text File with OpenSSL<br>
Part 2: Verifying Hashes
## Background / Scenario
- Hash functions are mathematical algorithms designed to take data as input and generate a fixed-size, unique
string of characters, also known as the hash. Designed to be fast, hash functions are very hard to reverse; it
is very hard to recover the data that created any given hash, based on the hash alone. Another important
property of hash function is that even the smallest change done to the input data yields a completely different
hash.
- While OpenSSL can be used to generate and compare hashes, other tools are available such as <b>gpg</b>, which provide a much better method
for ensuring the downloaded file has not been modified by third parties and in fact the file the publisher meant to publish.
## Required Resources
- CyberOps Workstation virtual machine
## Instructions
#### Part 1: Hashing a Text File with OpenSSL
OpenSSL can be used as a standalone tool for hashing. To create a hash of a text file, follow the steps below:<br>
a. In the CyberOps Workstation virtual machine, open a terminal window.<br>
b. Because the text file to hash is in the <b>/home/analyst/lab.support.files/</b> directory, change to that directory:
```
cd /home/analyst/lab.support.files/
```
c. Type the command below to list the contents of the letter_to_grandma.txt text file on the screen:
```
cat letter_to_grandma.txt
```
<br/>
<img src="https://i.imgur.com/kCuPMjc.png" height="80%" width="80%" alt="cat output"/>
<br />
d. From the terminal window, issue the command below to hash the text file. The command will use <b>SHA-2-
256</b> as the hashing algorithm to generate a hash of the text file: 

```
openssl sha256 letter_to_grandma.txt
```

<br/><img src="https://i.imgur.com/3zDauq7.png" height="80%" width="80%" alt="sha256 output1"/><br/>
<b>Note:</b> The SHA-256 hash itself is displayed after the equal (‘=’) sign.<br>
e. Hash functions are useful for verifying the integrity of the data regardless of whether it is an image, a
song, or a simple text file. The smallest change results in a completely different hash. Hashes can be
calculated before and after transmission, and then compared. If the hashes do not match, then the data was
modified during transmission.<br>
I will now modify the letter_to_grandma.txt text file and recalculate the MD5 hash. Open a command-line text editor like <b>nano</b> and Issue the command below.
```
nano letter_to_grandma.txt
```
<br/><img src="https://i.imgur.com/tjyL4Fh.png" height="80%" width="80%" alt="modified cat "/><br/>
Using nano, change the first sentence from <b>‘Hi Grandma’ to ‘Hi Grandpa’</b>. Press the <b><CONTROL+X></b> keys to save the
modified file. Press <b>‘Y’</b> to confirm the name and save the file. Press the <b><Enter></b> key to exit.<br>
f. Now that the file has been modified and saved, run the same command again to generate an SHA-2-256
hash of the file.
```
openssl sha256 letter_to_grandma.txt
```
<br/><img src="https://i.imgur.com/puKAbqF.png" height="80%" width="80%" alt="modified letter "/><br/>
<b>Note:</b> Notice that the two <b>message digest</b> are entirely different. <br>
g. A hashing algorithm with a longer bit-length, such as <b>SHA-2-512</b>, can also be used. To generate a SHA-2-
512 hash of the letter_to_grandma.txt file, use the command below:
```
openssl sha512 letter_to_grandma.txt
```
<br/><img src="https://i.imgur.com/qSXtfE3.png" height="80%" width="80%" alt="sha512 hash "/><br/>
h. Use sha256sum and sha512sum to generate <b>SHA-2-256 and SHA-2-512</b> hash of the
letter_to_grandma.txt file:
```
sha256sum letter_to_grandma.txt
```
```
sha512sum letter_to_grandma.txt
```
<br/><img src="https://i.imgur.com/YG3NOWF.png" height="50%" width="80%" alt="sha512 hash "/><br/>
<b>Note:</b>The hash generated by OpenSSL using SHA-256 algorithm for a file should match the hash generated by the 256sum command for the same file, because
 both OpenSSL and 256sum use the SHA-256 algorithm.

#### Part 2: Verifying Hashes
As mentioned before, a common use for hashes is to verify file integrity. I will now use SHA2-256 hashes to verify the integrity of sample.img, a file downloaded from the Internet.
a. Along with sample.img, sample.img_SHA256.sig was also downloaded. sample.img_SHA256.sig is a file
containing the SHA-2-256 hash that was computed by the website. First, use the cat command to display the contents of the sample.img_SHA256.sig file:
```
cat sample.img_SHA256.sig
```
Output: `c56c4724c26eb0157963c0d62b76422116be31804a39c82fd44ddf0ca5013e6a`<br>
b. Use SHA256sum to calculate the SHA-2-256 hash of the sample.img file:
```
sha256sum sample.img
```
Output: `c56c4724c26eb0157963c0d62b76422116be31804a39c82fd44ddf0ca5013e6a sample.img`

## Conclusion
- Since the hash matched, we can infer that the file <b>sample.img </b>is authentic and still maintains its integrity.
