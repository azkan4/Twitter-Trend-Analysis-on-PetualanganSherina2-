
# 🎬 Twitter Trend Analysis on #PetualanganSherina2

Proyek ini mencakup dua bagian utama:

1. 🐦 **Data Crawling** dari Twitter menggunakan `tweet-harvest`  
2. 🕸️ **Analisis Jaringan Sosial** (Social Network Analysis) terhadap data tweet yang terkumpul

---

## 📁 Struktur File

| File                      | Deskripsi                                               |
|---------------------------|----------------------------------------------------------|
| `Crawl data twitter.ipynb` | Script untuk melakukan crawling data tweet               |
| `Analisis.ipynb`           | Script untuk analisis jaringan sosial dari hasil crawling |
| `sherina.csv`              | Dataset hasil crawling tweet dengan kata kunci tertentu  |

---

## 🧾 Data Crawling

Mengambil tweet berdasarkan kata kunci `#PetualanganSherina2` dalam rentang waktu tertentu dan lokasi sekitar Jakarta, lalu menyimpannya dalam file CSV.

### 🛠️ Dependensi

- [`tweet-harvest`](https://www.npmjs.com/package/tweet-harvest)  
- [Node.js](https://nodejs.org)  
- `pandas` (Python)

### 📦 Instalasi

```bash
# Install pandas
pip install pandas

# Install Node.js
sudo apt-get update
sudo apt-get install -y ca-certificates curl gnupg
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg
NODE_MAJOR=20
echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_$NODE_MAJOR.x nodistro main" | sudo tee /etc/apt/sources.list.d/nodesource.list
sudo apt-get update
sudo apt-get install nodejs -y
```

### 🚀 Menjalankan Crawling

```python
filename = 'sherina.csv'
search_keyword = '(#PetualanganSherina2) until:2023-10-1 since:2023-09-28 geocode:-6.19526814800593,106.82299094600958,40km'
limit = 1000

!npx --yes tweet-harvest@latest -o "{filename}" -s "{search_keyword}" -l {limit} --token "YOUR_TWITTER_BEARER_TOKEN"
```

> 🔐 Ganti `YOUR_TWITTER_BEARER_TOKEN` dengan token autentikasi Twitter kamu.

---

### 📥 Output

- File `sherina.csv` dengan delimiter `;`
- Kolom-kolom: `username`, `full_text`, `favorite_count`, `retweet_count`, `reply_count`, `quote_count`, dll.

---

## 📊 Social Network Analysis

Analisis jaringan sosial berdasarkan hubungan antara `username` dan `full_text` dari tweet.

### 🛠️ Dependensi

```bash
pip install pandas matplotlib networkx
```

### 🔍 Analisis yang Dilakukan

- **Jumlah Node**: Berdasarkan jumlah `username` unik
- **Jumlah Edge**: Berdasarkan total interaksi (`like`, `retweet`, `reply`, `quote`)
- **Grafik Network**: Dibuat dari relasi antara `username` ↔ `full_text`

### 📈 Degree Centrality

- Menghitung *degree centrality* untuk mengukur seberapa penting/pengaruh sebuah node
- Menampilkan **10 pengguna paling berpengaruh**
- Menyimpan dan menampilkan visualisasi graf

### 📷 Visualisasi

- Node diberi warna dan ukuran berdasarkan tingkat *degree centrality*
- Label ditampilkan hanya untuk node (user) dengan centrality tertinggi
- Dilengkapi *color bar* untuk representasi tingkat pengaruh

---

## 🧪 Contoh Output

```text
Top 10 influential users by Degree Centrality:
User: abi234, Degree Centrality: 0.050
User: dinaa890, Degree Centrality: 0.045
User: raffa_999, Degree Centrality: 0.044
...
```

---
