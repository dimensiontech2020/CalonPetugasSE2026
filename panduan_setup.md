Panduan Setup Form Biodata Petugas SE 2026 ke Google Sheets
1. Persiapan Google Spreadsheet
Buat spreadsheet baru di Google Drive
Beri nama: "Biodata Petugas SE 2026"
Pada Sheet1 (tab pertama), isi header baris pertama dengan kolom berikut:
Table
A	B	C	D	E	F	G	H	I	J	K	L	M	N	O	P	Q	R	S	T	U	V	W
Timestamp	Nama Lengkap	NIK	NIP	Jenis Kelamin	Tempat Lahir	Tanggal Lahir	Agama	Status Perkawinan	No HP	Email	Alamat	Status Pegawai	Jabatan	Provinsi	Kabupaten	Kecamatan	No SK	Latitude	Longitude	Accuracy	Waktu Geo	Foto Base64
2. Setup Google Apps Script
Di spreadsheet, klik menu Extensions > Apps Script
Hapus semua kode default, lalu paste kode berikut:
JavaScript
Copy
function doGet(e) {
  return ContentService
    .createTextOutput(JSON.stringify({ status: "active", message: "API aktif" }))
    .setMimeType(ContentService.MimeType.JSON);
}

function doPost(e) {
  try {
    var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();

    var data = {};
    if (e.postData && e.postData.contents) {
      data = JSON.parse(e.postData.contents);
    }

    sheet.appendRow([
      new Date(),
      data.nama_lengkap || "",
      data.nik || "",
      data.nip || "",
      data.jenis_kelamin || "",
      data.tempat_lahir || "",
      data.tanggal_lahir || "",
      data.agama || "",
      data.status_perkawinan || "",
      data.no_hp || "",
      data.email || "",
      data.alamat || "",
      data.status_pegawai || "",
      data.jabatan || "",
      data.provinsi || "",
      data.kabupaten || "",
      data.kecamatan || "",
      data.no_sk || "",
      data.latitude || "",
      data.longitude || "",
      data.accuracy || "",
      data.timestamp || "",
      data.foto_base64 || ""
    ]);

    return ContentService
      .createTextOutput(JSON.stringify({ status: "success", message: "Data berhasil disimpan" }))
      .setMimeType(ContentService.MimeType.JSON);

  } catch (err) {
    return ContentService
      .createTextOutput(JSON.stringify({ status: "error", message: err.message }))
      .setMimeType(ContentService.MimeType.JSON);
  }
}
Klik Save (ikon disk) atau tekan Ctrl+S
Beri nama project: "BiodataPetugasSE2026"
3. Deploy Web App
Klik tombol Deploy (kanan atas) > New deployment
Klik ikon gear ⚙️ pilih Web app
Isi konfigurasi:
Description: Biodata Petugas SE 2026 API
Execute as: Me (your email)
Who has access: Anyone
Klik Deploy
Izinkan permission yang diminta (klik through warning)
Copy URL Web App yang muncul
4. Update URL di File HTML
Buka file form_biodata_petugas_se2026_gsheet.html di text editor
Cari baris: const GAS_URL = "..."
Ganti dengan URL Web App yang baru saja di-copy
Save file
5. Cara Penggunaan
Buka file HTML di browser (bisa langsung double-click)
Isi semua data form
Klik "Ambil Lokasi Saya" untuk geotagging
Upload foto (opsional)
Klik "Simpan ke Google Sheets"
Cek spreadsheet untuk memastikan data masuk
Catatan Penting
CORS: Jika mengalami masalah CORS, pastikan Web App di-deploy dengan "Who has access: Anyone"
Foto: Foto dikirim dalam format base64. Untuk mengubah kembali ke file gambar, copy nilai base64 dan decode menggunakan tool online
Ukuran foto: Maksimal 2MB. Jika foto terlalu besar, Google Sheets mungkin tidak bisa menampung seluruh string base64
Lokasi: Pastikan browser mengizinkan akses lokasi/GPS
Troubleshooting
Data tidak masuk ke spreadsheet?
Cek console browser (F12 > Console) untuk error
Pastikan URL GAS_URL di HTML sudah benar
Coba buka URL Web App langsung di browser, harus muncul JSON {"status":"active"}
Pastikan spreadsheet tidak di-restrict (private tapi Apps Script punya akses)
Error CORS?
Deploy ulang Web App dengan setting "Anyone"
Pastikan tidak ada redirect pada URL
Coba gunakan browser lain (Chrome direkomendasikan)
