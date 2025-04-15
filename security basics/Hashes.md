[[hash]] [[Hashes]] #hash #hashes
Hashcat is used to find the different modes of hashes: https://hashcat.net/wiki/doku.php?id=example_hashes

online hash identifiers: 
- https://hashes.com/en/tools/hash_identifier
- https://gitlab.com/kalilinux/packages/hash-identifier/-/tree/kali/master
  
  
CLI for finding hash values: 
- ``user@TryHackMe$ wget https://gitlab.com/kalilinux/packages/hash-identifier/-/raw/kali/master/hash-id.py
- $ python3 hash-id.py  ``
[[hash idetifier]]


wordlists: https://github.com/danielmiessler/SecLists     [[wordlist]]

John the ripper docs, wiki and rules: https://www.openwall.com/john/doc/RULES.shtml [[john the ripper]]

To show already cracked hashes in john the ripper: john --show [filename]