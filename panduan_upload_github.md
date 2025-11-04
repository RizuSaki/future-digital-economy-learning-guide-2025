# Panduan Upload File ke GitHub

## Metode 1: Upload via GitHub Web Interface (Termudah)

### Langkah-langkah:
1. **Masuk ke Repository**
   - Buka repository GitHub Anda
   - Klik pada folder tempat ingin upload file
   - Atau langsung klik "Add file" → "Upload files"

2. **Upload File**
   - Drag & drop file ke area yang tersedia, ATAU
   - Klik "choose your files" dan pilih file dari komputer
   - Untuk multiple files: pilih semua file sekaligus

3. **Commit Changes**
   - Tambahkan commit message (contoh: "Add new document")
   - Klik "Commit changes"

## Metode 2: Menggunakan Git Command Line

### Prerequisites:
```bash
# Install Git (jika belum ada)
# Windows: Download dari git-scm.com
# Mac: brew install git
# Linux: sudo apt install git
```

### Steps:
```bash
# 1. Clone repository (jika belum)
git clone https://github.com/username/repository-name.git
cd repository-name

# 2. Add files ke staging
git add nama_file.ext

# 3. Commit dengan pesan
git commit -m "Add new file: nama_file.ext"

# 4. Push ke remote repository
git push origin main
```

## Metode 3: Menggunakan GitHub Desktop (GUI)

1. **Download & Install GitHub Desktop**
   - Kunjungi desktop.github.com
   - Download dan install

2. **Add Repository**
   - Klik "Add an Existing Repository"
   - Pilih folder repository dari komputer

3. **Upload Files**
   - Copy file ke folder repository
   - Di GitHub Desktop, akan muncul sebagai changes
   - Add commit message dan commit

4. **Push to GitHub**
   - Klik "Push origin" untuk upload

## Metode 4: GitHub CLI (Command Line)

### Installation:
```bash
# Install GitHub CLI
# Windows: winget install GitHub.cli
# Mac: brew install gh
# Linux: sudo apt install gh
```

### Usage:
```bash
# Login to GitHub
gh auth login

# Clone repository
git clone https://github.com/username/repo.git

# Add file
git add file.txt
git commit -m "Add new file"
git push
```

## Metode 5: Programmatic Upload (API)

### Menggunakan GitHub API:
```python
import requests
import base64

# Setup headers
headers = {
    'Authorization': 'token YOUR_GITHUB_TOKEN',
    'Accept': 'application/vnd.github.v3+json'
}

# Encode file content to base64
with open('file.txt', 'rb') as f:
    content = base64.b64encode(f.read()).decode()

# API request to upload file
data = {
    'message': 'Add new file via API',
    'content': content
}

response = requests.put(
    'https://api.github.com/repos/username/repo/contents/file.txt',
    headers=headers,
    json=data
)

if response.status_code == 201:
    print("File uploaded successfully!")
else:
    print(f"Error: {response.status_code}")
```

## Tips untuk Upload yang Sukses:

### 1. **File Size Limits**
   - Single file: max 100MB via web
   - Multiple files: max 100MB total via web
   - Larger files: gunakan Git LFS atau command line

### 2. **Best Practices**
   - Gunakan commit messages yang deskriptif
   - Add .gitignore untuk exclude files yang tidak perlu
   - Test file di lokal sebelum upload

### 3. **File Types**
   - Supported: Semua jenis file
   - Besar: Gunakan Git LFS untuk files > 100MB
   - Binary: Git dapat handle file binary

### 4. **Branch Management**
   ```bash
   # Create new branch untuk fitur baru
   git checkout -b feature/new-file
   git add .
   git commit -m "Add new file"
   git push origin feature/new-file
   
   # Buat Pull Request di GitHub
   ```

### 5. **Troubleshooting**

#### File Terlalu Besar:
```bash
# Install Git LFS
git lfs install
git lfs track "*.zip" "*.pdf"
git add .gitattributes
git add large_file.zip
git commit -m "Add large file"
git push
```

#### Permission Denied:
```bash
# Setup SSH key
ssh-keygen -t ed25519 -C "your-email@example.com"
# Add key to GitHub Account → Settings → SSH Keys
git remote set-url origin git@github.com:username/repo.git
```

#### Merge Conflicts:
```bash
# Resolve conflicts
git status
# Edit conflicted files
git add resolved_file.txt
git commit -m "Resolve merge conflicts"
git push
```

## Solusi untuk "Core Dump" Error:

Jika mendapat error "core dump", kemungkinan:
1. **File corruption** - Re-create file
2. **System memory** - Restart computer, try smaller files
3. **Browser cache** - Clear cache, try different browser
4. **Network issues** - Try different connection

**Solutions:**
```bash
# Check file integrity
md5sum file.txt  # Linux/Mac
certutil -hashfile file.txt MD5  # Windows

# Try alternative upload method
git add file.txt
git commit -m "Upload problematic file"
git push
```

## Kesimpulan:
Gunakan metode yang paling sesuai dengan kebutuhan Anda:
- **Pemula**: GitHub Web Interface
- **Developers**: Git Command Line
- **Visual users**: GitHub Desktop
- **Automation**: GitHub API/CLI

Pilih metode yang paling nyaman dan sesuai dengan workflow Anda!