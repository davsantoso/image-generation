# Proyek Image Generation — StudioAI

Submission proyek akhir kursus **Belajar Fundamental Generative AI (BFGAI)** oleh David Santoso.

Proyek ini mengeksplorasi kemampuan generasi gambar berbasis AI menggunakan **Stable Diffusion**, mencakup tiga pipeline utama: Text-to-Image, Image-to-Image, dan Inpainting/Outpainting. Hasil akhirnya adalah aplikasi web interaktif bernama **StudioAI** yang dibangun dengan Streamlit.

---

## Fitur

### Pipeline (Notebook)

| Kriteria                   | Fitur                                                                                                      |
| -------------------------- | ---------------------------------------------------------------------------------------------------------- |
| **Text-to-Image**          | Generate gambar dari prompt teks dengan konfigurasi hyperparameter (seed, guidance scale, inference steps) |
| **Batch Inference**        | Generate beberapa gambar sekaligus dari satu prompt                                                        |
| **Scheduler**              | Perbandingan tiga scheduler: Euler A, DPM++, DDIM                                                          |
| **Image-to-Image**         | Base + refiner pipeline untuk menyempurnakan gambar                                                        |
| **Inpainting (Manual)**    | Edit area tertentu pada gambar menggunakan mask manual                                                     |
| **Inpainting (Auto-Mask)** | Segmentasi otomatis area menggunakan model `facebook/maskformer-swin-base-ade`                             |
| **Outpainting**            | Perluas kanvas gambar ke berbagai arah (left, right, top, bottom)                                          |
| **Outpainting Zoom Out**   | Perluas kanvas iteratif ke empat arah sekaligus                                                            |

### Aplikasi Streamlit (StudioAI)

- **Tab Generate**: Input prompt, negative prompt, dan parameter (steps, CFG, seed, scheduler, batch size) untuk menghasilkan gambar.
- **Tab Edit**:
  - **Inpainting**: Gambar mask langsung di atas gambar menggunakan drawable canvas, lalu ganti area tersebut dengan prompt baru.
  - **Outpainting**: Perluas gambar 128px ke segala arah dengan blur background otomatis.
- Tombol **Flush RAM** untuk membersihkan GPU memory.
- Deployment via **Ngrok** public URL.

---

## Model yang Digunakan

| Model                                  | Kegunaan                               |
| -------------------------------------- | -------------------------------------- |
| `runwayml/stable-diffusion-v1-5`       | Text-to-Image dan Image-to-Image       |
| `runwayml/stable-diffusion-inpainting` | Inpainting dan Outpainting             |
| `facebook/maskformer-swin-base-ade`    | Segmentasi otomatis untuk auto-masking |

---

## Struktur Proyek

```
.
├── Pipeline_submission_BFGAI_David_Santoso.ipynb   # Eksplorasi pipeline lengkap
├── Streamlit_submission_BFGAI_David_Santoso.ipynb  # Notebook untuk deploy StudioAI
├── requirements.txt                                # Daftar dependensi
```

File `logic.py` dan `app.py` di-generate secara otomatis saat menjalankan notebook Streamlit.

---

## Cara Menjalankan

### 1. Install Dependensi

```bash
pip install diffusers transformers accelerate torch torchvision Pillow matplotlib numpy
pip install streamlit streamlit_drawable_canvas pyngrok
```

### 2. Jalankan Pipeline Eksplorasi

Buka dan jalankan `Pipeline_submission_BFGAI_David_Santoso.ipynb` di Google Colab (disarankan menggunakan GPU runtime).

### 3. Jalankan Aplikasi Streamlit

Buka `Streamlit_submission_BFGAI_David_Santoso.ipynb`, lalu:

1. Jalankan semua cell untuk men-generate file `logic.py` dan `app.py`.
2. Isi `auth_token` dengan token Ngrok Anda.
3. Jalankan cell deployment — URL publik akan ditampilkan di output.

> **Catatan:** Diperlukan GPU (CUDA) untuk performa optimal. CPU dapat digunakan tetapi jauh lebih lambat.

---

## Tingkatan Implementasi

Proyek ini dibagi menjadi tiga tingkat kesulitan:

- **Basic**: Generate gambar sederhana dari teks dengan seed dan parameter dasar.
- **Skilled**: Batch inference, pemilihan scheduler, dan flush GPU memory.
- **Advanced**: Inpainting dengan mask canvas, outpainting dengan expand kanvas otomatis.

---

## Persyaratan Sistem

- Python 3.10+
- CUDA-compatible GPU (direkomendasikan: VRAM ≥ 8GB)
- Google Colab (T4/A100) atau lingkungan lokal dengan GPU
