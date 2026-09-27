# HashScope for Linux, Kali & Debian Forensic Workstations

## 1. Running the Ready-to-Use 64-bit Linux Package

You can download the pre-compiled native Linux release directly from the website:
- **`hashscope-1.2.0.tar.gz`** (103 MB)
- **`hashscope-1.2.0.zip`** (103 MB)

### Quick Run on Kali / Ubuntu:
```bash
# 1. Extract the archive
tar -xzf hashscope-1.2.0.tar.gz
cd hashscope-1.2.0

# 2. Make executable & launch
chmod +x hashscope
./hashscope
```

---

## 2. Compiling the `.deb` Package for Kali / Debian

Because the `.deb` package requires Linux-native packaging utilities (`fpm`), building `.deb` is performed either directly on a Linux machine or via the automated GitHub Actions runner.

On any Linux machine:
```bash
# Clone the repository
git clone https://github.com/tojo54/hashscope.git
cd hashscope

# Install dependencies & build .deb
npm install
npm run build:linux
```
Output will be placed in `dist/hashscope_1.2.0_amd64.deb`.

Install it on Kali / Ubuntu:
```bash
sudo dpkg -i dist/hashscope_1.2.0_amd64.deb
```
