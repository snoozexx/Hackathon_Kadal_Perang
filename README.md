# Hackathon_Kadal_Perang
imphen hackathon team kadal perang, pak edy army

# OtoSense — Backend IoT + AI Pemeliharaan Armada

## Elevator Pitch
- UMKM dengan armada kendaraan sering kehilangan waktu dan biaya karena kerusakan tak terdeteksi.
- OtoSense menggabungkan telemetry kendaraan real-time dengan AI untuk: mendeteksi anomali, memberi diagnosa cepat, dan estimasi biaya perbaikan.
- Hasilnya: downtime turun, biaya perawatan terkontrol, dan operasional lebih aman.

## Problem & Insight
- Masalah: Diagnosa lambat, tidak adanya peringatan dini, dan sulitnya estimasi biaya.
- Insight: Data OBD/telemetry + pengetahuan mekanik bisa dipakai untuk rekomendasi yang actionable.
- Solusi kami: Aturan sederhana untuk status cepat, lalu AI menganalisis DTC + sensor guna memberi ringkasan, urgensi, dan estimasi biaya.

## Value Proposition
- Peringatan real-time untuk kondisi kritikal (overheat, overspeed, low battery, AFR issue).
- Diagnosa AI berbahasa Indonesia yang mudah dipahami driver/owner.
- Knowledge Base lokal untuk caching hasil (hemat panggilan AI, konsisten, cepat).

## Fitur Utama
- HTTP API untuk ingest telemetry dan ambil status terakhir.
- WebSocket broadcast untuk live monitoring per kendaraan atau global.
- Integrasi AI (Kolosal/OpenAI client) dengan output JSON terstruktur.
- Penyimpanan pengetahuan lokal `knowledge_base.json` dengan TTL 20 menit.

## Arsitektur Singkat
- `main.py`: HTTP + WebSocket server, orkestrasi status dan AI.
- `models.py`: Skema data Pydantic (`TelemetryIn`, `TelemetryOut`, `AIAdvice`).
- `services/api_client.py`: Pemanggilan AI + normalisasi hasil.
- `services/ai_service.py`: Analisis kerusakan, parse biaya, dan cache KB atomik.
- `knowledge_base.json`: Cache pengetahuan DTC.
- `simulator.py`: Skenario pengujian cepat.
- `test.py`: Contoh panggilan langsung ke Kolosal API.

## Tech Stack
- Python 3.10+, FastAPI, Uvicorn, Pydantic, Requests, dotenv
- OpenAI SDK (dipakai untuk akses Kolosal AI via `base_url`)
- Dependensi: lihat `requirements.txt`

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

