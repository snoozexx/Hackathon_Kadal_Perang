# Hackathon_Kadal_Perang
imphen hackathon team kadal perang, pak edy army

# RodhiGengFirmansyah — Backend IoT + AI Diagnosa Kerusakan dan memberikan rekomendasi perbaikan pada kendaraan

# Clone Repo
git clone --recurse-submodules <repository-url>

# Install Dependencies
pip install -r requirements.txt

## Demo Script (3–5 Menit)
- Langkah 1: Jalankan server:
  - `uvicorn main:app --reload --host 0.0.0.0 --port 8000`
- Langkah 2: Buka `http://localhost:8000/docs` untuk lihat endpoint.
- Langkah 3: Jalankan simulasi:
  - `python simulator.py --scenario 1` (Normal)
  - `python simulator.py --scenario 2` (Warning: RPM tinggi)
  - `python simulator.py --scenario 3` (Critical: Overheat + DTC P0300)
- Langkah 4: Tunjukkan `ai_advice` di output dan `knowledge_base.json` bertambah/ter-update.
- Langkah 5: Buka WebSocket untuk melihat live update:
  - `ws://localhost:8000/ws/TEST-003` di browser (log ke console).
- Langkah 6: Tunjukkan `GET /api/status/{vehicle_id}` untuk data terbaru.

## Quick Start (Panduan)
- Persiapan:
  - Python 3.10+, virtualenv.
  - `pip install -r requirements.txt`
- Konfigurasi `.env`:
  - `ALLOW_ORIGINS=http://localhost:3000`
  - `KB_PATH=./knowledge_base.json`
  - `KOLOSAL_API_KEY=<isi-dari-provider>`
  - `KOLOSAL_BASE_URL=https://api.kolosal.ai/v1`
  - `AI_MODEL=Claude Sonnet 4.5`
- Jalankan server:
  - `uvicorn main:app --reload --host 0.0.0.0 --port 8000`
- Uji cepat:
  - `python simulator.py --scenario 3`
  - `curl -X GET http://localhost:8000/api/status/TEST-003`

-------------------------------------------------------------------------
## FE

# Install Dependencies
cd Hackathon_Kadal_Perang\fe-damage-detection-kadal-perang
npm install

# Jalankan Project
npm run build
npm run dev

-------------------------------------------------------------------------

## Cara Menggunakan Sebagai User yang sudah di deploy
- Masuk ke link ini 
  https://fe-damage-detection-kadal-perang.vercel.app/
  
- Tancapkan sensor OBD2 pada port untuk mengambil data dari ECU kendaraan
- Pilih kendaraan yang ingin di diagnosa
- Klik tombol start atau mulai diagnosa
- Maka akan otomatis mendiagnosa atau mendeteksi kerusakan pada motor nya
- Setelah 15 detik, maka akan tampil chart atau grafik berbagai macam sensor secara real yang di ambil dari motor tsb
- Selain itu juga ada view detail atau summary kerusakan semua nya dan akan di berikan rekomendasi perbaikan nya,
- Di tampilkan juga potensi kerusakan komponen untuk kedepan nya juga, kemudian di tampilkan juga estimasi biaya perbaikan nya
- Terdapat fitur untuk melihat history riwayat kendaraan nya
