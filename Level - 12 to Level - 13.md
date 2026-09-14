
Connecting to ssh level 12 using the credentials from Prv. level

ssh bandit12@bandit.labs.overthewire.org -p 2220
Password String Intentionally Omitted

## Level Goal

The password for the next level is stored in the file **data.txt**, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work. Use mkdir with a hard to guess directory name. Or better, use the command “mktemp -d”. Then copy the datafile using cp, and rename it using mv (read the manpages!)

## Commands you may need to solve this level

grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd, mkdir, cp, mv, file

## Helpful Reading Material

- [Hex dump on Wikipedia](https://en.wikipedia.org/wiki/Hex_dump)


cd /tmp/dyhwqevajfdw  (tmp workspace)


Password String Intentionally Omitted (pwd for next level)




🔎 1. `file`

- **Use Case:** Determines the true file type of a target, ignoring whatever extension (like `.txt`) it has. This is your most critical tool for this level.
- **Syntax:**
    
    bash
    
    ```
    file filename
    ```


💻 2. `xxd`

- **Use Case:** Generates a hexadecimal dump of a binary file, or reverses a hex dump back into its original binary layout. 
- **Syntax:**
    - _Create Hex Dump:_ `xxd filename`
    - _Reverse Hex to Binary:_ `xxd -r hex_file_input output_file` 

📁 3. `mkdir`

- **Use Case:** Creates a new, empty directory. Since you cannot modify files directly in the home folder of this level, you must create a workspace inside `/tmp`.
- **Syntax:**
    
    bash
    
    ```
    mkdir /tmp/your_folder_name
    ```


📋 4. `cp`

- **Use Case:** Copies a file from one location to another. You will use this to copy `data.txt` into your temporary directory.
- **Syntax:**
    
    bash
    
    ```
    cp source_file destination_folder/
    ```


📦 5. `mv`

- **Use Case:** Moves a file to a new location, or renames a file. In this level, you will use it constantly to change file extensions (e.g., renaming a file to `.gz` so the decompression tools will accept it).
- **Syntax:**
    
    bash
    
    ```
    mv old_name new_name
    ```
    


🗜️ 6. `gzip`

- **Use Case:** Compresses or decompresses files using Lempel-Ziv coding (`.gz`). The tool is strict and usually requires the file to have a `.gz` extension to decompress it. 
- **Syntax:**
    - _Decompress:_ `gzip -d filename.gz` 

🗜️ 7. `bzip2`

- **Use Case:** Compresses or decompresses files using the Burrows-Wheeler algorithm (`.bz2`). 
- **Syntax:**
    - _Decompress:_ `bzip2 -d filename.bz2`

📦 8. `tar`

- **Use Case:** Unpacks tape archive bundles (`.tar`). It can handle raw text archives or compressed archives depending on the flags used. 
- **Syntax:**
    - _Extract:_ `tar -xvf filename.tar` 

---

🔄 The Quick-Reference Utilities

You already mastered these in previous levels, but they remain in your toolkit to help you clean up or view the final output:

- **`strings`**: Extracts printable text strings from binary blobs.
    - `strings filename` 
- **`base64`**: Decodes or encodes base64 structures.
    - `base64 -d filename`
- **`tr`**: Translates or replaces character sets.
    - `cat filename | tr 'a' 'b'` 
- **`grep`**: Searches for text matching a pattern.
    - `grep "pattern" filename` 
- **`sort`**: Alphabetically sorts text lines.
    - `sort filename` 
- **`uniq`**: Filters out duplicate text lines.
    - `sort filename | uniq` 

---


📝 Summary of Bandit Level 12

This level is designed to teach you how to analyze and reverse-engineer heavily nested, multi-layered file archives without relying on file extensions.

---

🗝️ Core Takeaways & The "Why" Behind the Failure

1. Why `bzip2` failed when you renamed `thechittixyz` to `.bz2`

You encountered the error `bzip2: thechittixyz.bz2 is not a bzip2 file`. This happened because of how `gzip` treats internal archive metadata:

- **The "Was Name" Feature:** When `gzip -d thechittixyz.gz` executed, it looked inside the archive and saw that the original developer had named the inner payload `data2.bin`.
- **The Silent Extraction:** Instead of updating your existing file or naming it `thechittixyz`, **`gzip` deleted your original `.gz` file** and extracted a brand new file named **`data2.bin`** into your folder.
- **The Mismatch:** You ran a command targeting your old filename string, missing the newly spawned `data2.bin`. Running a decompression tool on a file that has already been unpacked causes the tool to fail immediately.

2. Extensions Mean Nothing to Linux

Windows uses extensions (`.zip`, `.exe`) to figure out how to open a file. Linux does not care. To the Linux kernel, a file extension is just basic text at the end of a filename.

- If a file contains `gzip` binary signatures inside it, renaming it to `.bz2` will not magically convert it into a `bzip2` archive.
- You must always use the **`file`** command to look past the extension and read the file's true physical identity.

3. Compression Suffix Strictness

While Linux itself doesn't care about extensions, the individual extraction programs _are_ strict.

- `gzip` will completely refuse to touch a file unless its filename explicitly ends in `.gz` (which is why `.gzip` threw an error).
- `bzip2` strictly requires `.bz2` or `.bz`.
- `tar` is more flexible and can often read files without a specific suffix, but keeping `.tar` makes it easy to track. 

---

🛠️ Step-by-Step Command Syntax Reference

Here is the exact progression of tools and commands you used to peel back the architecture of the file, layer by layer:

| Step   | Goal / Action                  | Exact Syntax Example             |
| ------ | ------------------------------ | -------------------------------- |
| **1**  | Create a safe workspace        | `mkdir /tmp/dyhwqevajfdw`        |
| **2**  | Copy the file over             | `cp data.txt /tmp/dyhwqevajfdw/` |
| **3**  | Turn text hex back into binary | `xxd -r data.txt data.bin`       |
| **4**  | Check true data type           | `file data.bin`                  |
| **5**  | Rename for Gzip compatibility  | `mv data.bin data.gz`            |
| **6**  | Unpack Gzip file               | `gzip -d data.gz`                |
| **7**  | Rename for Bzip2 compatibility | `mv data2.bin data2.bz2`         |
| **8**  | Unpack Bzip2 file              | `bzip2 -d data2.bz2`             |
| **9**  | Unpack a POSIX Tar file        | `tar -xvf data5.tar`             |
| **10** | Read the final cleartext       | `cat data8`                      |






SOC angle: Malware is frequently delivered inside nested 
compressed archives to bypass email filters and AV scanners. 
Knowing how to peel back layers using file, xxd, gzip, 
bzip2, and tar is a direct incident response skill.
















