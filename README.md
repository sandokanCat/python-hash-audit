# 🪓 python-hash-audit

![Red Team Tool](https://img.shields.io/badge/Red%20Team-Tool-critical?style=for-the-badge&logo=protonmail&logoColor=white)

**Academic hash dictionary attack tool using password+salt combinations**  
Supports 14+ algorithms, multi-hash mode, custom wordlists, JSON output, and stdin piping.  
Parallelized via multiprocessing with progress bar.

> Designed for cybersecurity students and Red Team labs.

---

## ⚡ Quick Start

```bash
# 1. Clone the repo
git clone https://github.com/sandokanCat/python-hash-audit.git
cd python-hash-audit

# 2. Install dependencies
pip install -r requirements.txt

# 3. Try to crack a simple MD5 hash
python hash_dictionary_audit.py --target-hash 5f4dcc3b5aa765d61d8327deb882cf99
```

---

## 🧠 Features

- 🔒 Supports 14+ algorithms from the hashlib module:
  - md5, sha1, sha256, sha512, sha224, sha384, sha3_*, blake2*, shake_*
- 🧂 Brute-forces all combinations of:
  - password + salt (ps)
  - salt + password (sp)
  - Or both (--mode both, default)
- 🧵 Multithreading with --threads (via multiprocessing)
- 📥 Accepts hash input from:
  - --target-hash, --hash-file, or --stdin-mode
- 🗂️ Supports custom wordlist injection (--custom-wordlist)
- 💾 Optional output to:
  - Text log file (--save)
  - Structured JSON file (--json)
- 📄 Hash length detection via --hash-length
- 🔇 Quiet mode and log to file (--quiet, --log)
- 🆓 No external dependencies except tqdm

> ☝️ The tool prioritizes the custom wordlist first. If it fails, it falls back to built-in lists.

---

## ⚙️ Arguments Overview

| Argument                  | Description                                     |
| ------------------------- | ----------------------------------------------- |
| `-x`, `--target-hash`     | Crack a single hash manually                    |
| `-f`, `--hash-file`       | File with one hash per line                     |
| `-d`, `--stdin-mode`      | Read hashes from `stdin`                        |
| `-n`, `--hash-length`     | Infer algorithm(s) from hash length             |
| `-a`, `--algo`            | Force specific algorithm                        |
| `-w`, `--custom-wordlist` | Use a custom wordlist first                     |
| `-m`, `--mode`            | Combination mode: `ps`, `sp`, or `both`         |
| `-t`, `--threads`         | Number of parallel processes                    |
| `-s`, `--save`            | Save successful cracks to file (with timestamp) |
| `-j`, `--json`            | Export results to JSON                          |
| `-l`, `--log`             | Set log file path                               |
| `-q`, `--quiet`           | Suppress verbose output                         |
| `-v`, `--version`         | Show script version and exit                    |
| `-h`, `--help`            | Show this help message and exit                 |

---

## 🛠️ Usage Examples

```bash
# Basic usage
python hash_dictionary_audit.py --target-hash 5f4dcc3b5aa765d61d8327deb882cf99

# From file with algorithm guessing
python hash_dictionary_audit.py --hash-file hashes.txt --hash-length 32

# Using a custom wordlist
python hash_dictionary_audit.py --target-hash <HASH> --custom-wordlist mylist.txt

# Save cracked result to a text file
python hash_dictionary_audit.py -x <HASH> --save cracked.txt

# Save structured result to JSON
python hash_dictionary_audit.py -x <HASH> --json result.json

# Full combo: file input, force algorithm, custom wordlist, JSON + threads
python hash_dictionary_audit.py -f hashes.txt -a md5 -w custom.txt -t 4 --json out.json
```

> ⚠️ You must provide exactly one input source: --target-hash, --hash-file, or --stdin-mode.

### 🔄 Supported Algorithms

| Algorithm     | Hash Length (hex) |
|---------------|-------------------|
| md5           | 32                |
| sha1          | 40                |
| sha224        | 56                |
| sha256        | 64                |
| sha3_256      | 64                |
| blake2s       | 64                |
| sha384        | 96                |
| sha3_384      | 96                |
| sha512        | 128               |
| sha3_512      | 128               |
| blake2b       | 128               |

### 🔁 Using stdin mode

```bash
echo "098f6bcd4621d373cade4e832627b4f6" | python hash_dictionary_audit.py --stdin-mode
```

---

## 📁 Folder Structure

```bash
python-hash-audit/
├── hash_dictionary_audit.py     # Main script
├── requirements.txt  # Dependencies (only tqdm)
└── wordlist/
    ├── 10k-most-common.txt
    └── rockyou.txt
```

---

## 🔧 Install

Only one dependency is required:

```bash
pip install tqdm
# or
pip install -r requirements.txt
```

> ⚙️ Requires Python 3.6+ (Recommended: 3.11+)

### 🧪 Tested On

- ✅ Python 3.11.4 (Linux, Windows)
- ✅ tqdm 4.66.x
- ❗ Avoid running with Python < 3.6

---

## 📄 Output Example

```text
✅ SUCCESS! (SHA1)
🔑 Full password: 'academy123salt'
🔍 Generated Hash: 2c1743a391305fbf367df8e4f069f9f9a36c1d19
💾 Saved to 'results.txt'
```

Or in JSON mode:

```json
{
  "found": true,
  "hash": "2c1743a391305fbf367df8e4f069f9f9a36c1d19",
  "algorithm": "sha1",
  "password": "academy123salt",
  "generated": "2c1743a391305fbf367df8e4f069f9f9a36c1d19",
  "elapsed_seconds": 0.94
}
```

---

## ✅ Best Practices

- Use --hash-length when you don’t know the algorithm.
- Prefer --json for automation and reporting.
- Provide smaller custom wordlists for focused attacks.
- Use --quiet when integrating into pipelines or scripts.

> Extremely large wordlists may require high RAM or long processing time.

---

## 🤝 Contributing

[Contributions are welcome!](./CONTRIBUTING.md)
Keep code **modular, readable, and tested**.
Pull requests should include a clear description and working example.

---

## 📝 License

MIT © 2026 [sandokan.cat](https://sandokan.cat)

> *Use it. Modify it. Share it. Attribution is appreciated.*

<div align="center">
    <a href="./LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green?logo=opensourceinitiative&logoColor=white" alt="MIT License">
    </a>
</div>

---

## 🔮 Planned Features

- [ ] GPU support (via PyOpenCL or hashcat bridge)
- [ ] Wordlist resume (for large datasets)
- [ ] Salt file mode (e.g. separate file with salts)
- [ ] API-ready modular version

---

## ⚠️ Disclaimer

This tool is for **educational and ethical purposes only.**

> 🛡️ This script **does not include any hashes**. You are responsible for supplying your own, in a legal and responsible context.  
> Do **not** use this tool against any data you do not own or have explicit permission to audit.

**Misuse of this tool is your responsibility.**  
Always operate within the boundaries of the law and ethical hacking guidelines.

---

> *"Brute force is a last resort, but understanding it is a first step."*
