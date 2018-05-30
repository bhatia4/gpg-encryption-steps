# gpg-encryption-steps
Encryption/Decryption steps using GNU Privacy Guard (GPG)

Purpose of this document was to bring together disparate information (on various diferrent sites, forums and other webpages) on how to encrypt and decrypt files using GNU Privacy Guard (GPG). Hope this helps you.<br/>

Basic Premise:
We will encrypt/decrypt using asymmetric cryptography which involves a public key to encrypt and a private key (with passphrase) to decrypt. 
As stated on GPG site: A public and private key each have a specific role when encrypting and decrypting documents. A public key may be thought of as an open safe. When a correspondent encrypts a document using a public key, that document is put in the safe, the safe shut, and the combination lock spun several times. The corresponding private key is the combination that can reopen the safe and retrieve the document. In other words, only the person who holds the private key can recover a document encrypted using the associated public key.

The procedure for encrypting and decrypting documents is straightforward with this mental model. If you want to encrypt a message to Alice, you encrypt it using Alice's public key, and she decrypts it with her private key. If Alice wants to send you a message, she encrypts it using your public key, and you decrypt it with your key.

<br/>Pre-requisite:
Make sure to download gpg tool from https://www.gnupg.org/ and see if you have access to either gpg or gpg2 via command line.

<br/>Steps:<br/>

<b>Step 1 A</b>: First time only, generate key pair. You will be asked for userID in the form "First Lastname (comment or initials) <email.address>".
If you are on linux env, then prior to this step you may also want to install rng-tools, which is a set of utilities related to random number generation in kernel. Any private information has been replaced with asterix (*).
<pre>
  gpg --gen-key
Please select what kind of key you want:
   (1) RSA and RSA (default)
   (2) DSA and Elgamal
   (3) DSA (sign only)
   (4) RSA (sign only)
Your selection? 1

RSA keys may be between 1024 and 4096 bits long.
What keysize do you want? (2048) 4096

Requested keysize is 4096 bits
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0) 2w

Key expires at Wed 13 Jun 2018 08:17:08 AM EDT
Is this correct? (y/N) Y

You need a user ID to identify your key; the software constructs the user ID
from the Real Name, Comment and Email Address in this form:
    "Heinrich Heine (Der Dichter) <heinrichh@duesseldorf.de>"

Real name: Kenny Rogers
Email address: kenny.rogers99@gmail.com
Comment: KSB
You selected this USER-ID:
    "Kenny Rogers (KGB) &lt;kenny.rogers99@gmail.com&gt;"

Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? O

You need a Passphrase to protect your secret key.
Enter passphrase: *************

+++++
.............+++++
We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
+++++
...........+++++
gpg: key 8CF28AFF marked as ultimately trusted
public and secret key created and signed.

gpg: checking the trustdb
gpg: 3 marginal(s) needed, 1 complete(s) needed, PGP trust model
gpg: depth: 0  valid:   2  signed:   0  trust: 0-, 0q, 0n, 0m, 0f, 2u
gpg: next trustdb check due at 2018-06-13
pub   4096R/******** 2018-05-30 [expires: 2018-06-13]
      Key fingerprint = **** **** **** **** ****  **** **** **** **** ****
uid                  Kenny Rogers (KGB) &lt;kenny.rogers99@gmail.com&gt;
sub   4096R/******** 2018-05-30 [expires: 2018-06-13]
</pre>

<b>Step 1 B</b>: List all keys from the public keyrings
<pre>  gpg --list-keys </pre>

<b>Step 2</b>: Have a input file ready for encryption (in our steps its input.txt but it can be an input file, even binary)

Step 3: using gpg to encrypt input.txt and output it as file doc.gpg (; arguments "--encrypt" to encrypt given input file & "--output file" write output to file)
<pre>  gpg --output doc.gpg --encrypt input.txt </pre>

gpg --decrypt doc.gpg --encrypt input.txt

More info on GPG at: 
https://www.gnupg.org/
https://www.gnupg.org/faq/gnupg-faq.html
https://www.gnupg.org/gph/en/manual/x110.html
https://www.gnupg.org/documentation/manpage.html
