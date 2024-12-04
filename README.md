# FreeRTOS Resource Contention Example

Program ini adalah implementasi multitasking menggunakan FreeRTOS pada mikrokontroler STM32. Program ini menampilkan bagaimana dua task (GreenFlashTask dan RedFlashTask) mengakses sumber daya bersama secara bergantian, sekaligus menangani kontensi sumber daya menggunakan indikator LED.

## Fitur
1. **GreenFlashTask**: Mengontrol LED hijau dan mengakses sumber daya bersama.
2. **RedFlashTask**: Mengontrol LED merah dengan prioritas lebih tinggi dan mengakses sumber daya bersama.
3. **Kontensi Sumber Daya**:
   - Jika dua task mencoba mengakses sumber daya secara bersamaan, LED biru akan menyala untuk menunjukkan kontensi.
4. **Prioritas Task**:
   - RedFlashTask memiliki prioritas lebih tinggi dibandingkan GreenFlashTask.

---

## Cara Kerja Program
### 1. **Pengaturan Prioritas**
- **GreenFlashTask** memiliki prioritas normal (`osPriorityNormal`).
- **RedFlashTask** memiliki prioritas tinggi (`osPriorityHigh`).

### 2. **Task Logic**
#### a. **GreenFlashTask**
- **Fungsi**: Mengontrol LED hijau dan mencoba mengakses sumber daya bersama.
- **Alur Kerja**:
  1. LED hijau dinyalakan.
  2. Task mencoba mengakses sumber daya menggunakan fungsi `AccessSharedResource()`.
  3. LED hijau dimatikan.
  4. Task ditunda selama 500 ms.

#### b. **RedFlashTask**
- **Fungsi**: Mengontrol LED merah dan mencoba mengakses sumber daya bersama.
- **Alur Kerja**:
  1. LED merah dinyalakan.
  2. Task mencoba mengakses sumber daya menggunakan fungsi `AccessSharedResource()`.
  3. LED merah dimatikan.
  4. Task ditunda selama 100 ms.

#### c. **Default Task**
- Tidak memiliki fungsi spesifik, hanya aktif sebagai placeholder dan memiliki prioritas terendah.

### 3. **Akses Sumber Daya Bersama**
- **Resource Flag**: Variabel `resource_flag` digunakan untuk menentukan status sumber daya:
  - `1`: Sumber daya bebas.
  - `0`: Sumber daya sedang digunakan.
- **Fungsi `AccessSharedResource()`**:
  - Jika `resource_flag == 1`, task dapat mengakses sumber daya dan mengubah statusnya menjadi `0`.
  - Jika `resource_flag == 0`, terjadi kontensi, dan LED biru menyala untuk menunjukkan konflik.

### 4. **Simulasi Sumber Daya**
- Akses sumber daya disimulasikan dengan fungsi `HAL_Delay(100)`.
- Setelah selesai, `resource_flag` dikembalikan ke `1`, menunjukkan sumber daya kembali bebas.

---

## Cara Menjalankan
1. **Konfigurasi Hardware**:
   - Sambungkan tiga LED (hijau, merah, dan biru) ke pin GPIO yang sesuai:
     - LED Hijau: `GPIOA_PIN_x`.
     - LED Merah: `GPIOA_PIN_y`.
     - LED Biru: `GPIOA_PIN_z`.

2. **Bangun dan Flash**:
   - Import proyek ini ke STM32CubeIDE.
   - Kompilasi dan flash ke mikrokontroler STM32 Anda.

3. **Pengamatan**:
   - LED hijau dan merah akan menyala bergantian.
   - Jika terjadi kontensi sumber daya, LED biru akan menyala.

---



https://github.com/user-attachments/assets/5b0714d8-5f39-4694-9c84-4c2242b464fd


