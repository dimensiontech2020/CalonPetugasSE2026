<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Form Biodata Petugas SE 2026 - BPS</title>

    <!-- Leaflet CSS -->
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" 
          integrity="sha256-p4NxAoJBhIIN+hmNHrzRCf9tD/miZyoHS5obTRR9BMY=" 
          crossorigin=""/>

    <!-- Font Awesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 900px;
            margin: 0 auto;
            background: white;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #1e3c72 0%, #2a5298 100%);
            color: white;
            padding: 30px;
            text-align: center;
            position: relative;
        }

        .header::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: url("data:image/svg+xml,%3Csvg width='60' height='60' viewBox='0 0 60 60' xmlns='http://www.w3.org/2000/svg'%3E%3Cg fill='none' fill-rule='evenodd'%3E%3Cg fill='%23ffffff' fill-opacity='0.05'%3E%3Cpath d='M36 34v-4h-2v4h-4v2h4v4h2v-4h4v-2h-4zm0-30V0h-2v4h-4v2h4v4h2V6h4V4h-4zM6 34v-4H4v4H0v2h4v4h2v-4h4v-2H6zM6 4V0H4v4H0v2h4v4h2V6h4V4H6z'/%3E%3C/g%3E%3C/g%3E%3C/svg%3E");
            opacity: 0.3;
        }

        .header h1 {
            font-size: 28px;
            margin-bottom: 8px;
            position: relative;
        }

        .header p {
            font-size: 14px;
            opacity: 0.9;
            position: relative;
        }

        .logo-bps {
            width: 70px;
            height: 70px;
            background: white;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0 auto 15px;
            font-size: 30px;
            color: #1e3c72;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
            position: relative;
        }

        .form-body {
            padding: 30px;
        }

        .section-title {
            font-size: 18px;
            color: #1e3c72;
            margin-bottom: 20px;
            padding-bottom: 10px;
            border-bottom: 3px solid #e0e0e0;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .section-title i {
            color: #667eea;
        }

        .form-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
            margin-bottom: 25px;
        }

        .form-group {
            display: flex;
            flex-direction: column;
        }

        .form-group.full-width {
            grid-column: 1 / -1;
        }

        .form-group label {
            font-weight: 600;
            color: #333;
            margin-bottom: 8px;
            font-size: 14px;
        }

        .form-group label .required {
            color: #e74c3c;
            margin-left: 3px;
        }

        .form-group input,
        .form-group select,
        .form-group textarea {
            padding: 12px 15px;
            border: 2px solid #e0e0e0;
            border-radius: 10px;
            font-size: 14px;
            transition: all 0.3s ease;
            font-family: inherit;
        }

        .form-group input:focus,
        .form-group select:focus,
        .form-group textarea:focus {
            outline: none;
            border-color: #667eea;
            box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
        }

        .form-group input.error,
        .form-group select.error {
            border-color: #e74c3c;
        }

        .form-group textarea {
            resize: vertical;
            min-height: 80px;
        }

        .map-section {
            margin-bottom: 25px;
        }

        .map-container {
            border-radius: 15px;
            overflow: hidden;
            border: 3px solid #e0e0e0;
            position: relative;
        }

        #map {
            height: 400px;
            width: 100%;
        }

        .map-controls {
            display: flex;
            gap: 10px;
            margin-top: 15px;
            flex-wrap: wrap;
        }

        .btn {
            padding: 12px 24px;
            border: none;
            border-radius: 10px;
            font-size: 14px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            display: inline-flex;
            align-items: center;
            gap: 8px;
        }

        .btn-primary {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
        }

        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 20px rgba(102, 126, 234, 0.4);
        }

        .btn-secondary {
            background: #f0f0f0;
            color: #333;
        }

        .btn-secondary:hover {
            background: #e0e0e0;
        }

        .btn-success {
            background: linear-gradient(135deg, #11998e 0%, #38ef7d 100%);
            color: white;
        }

        .btn-success:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 20px rgba(17, 153, 142, 0.4);
        }

        .coordinate-display {
            background: #f8f9fa;
            padding: 15px;
            border-radius: 10px;
            margin-top: 15px;
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
        }

        .coord-item {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .coord-item i {
            color: #667eea;
            font-size: 18px;
        }

        .coord-item span {
            font-weight: 600;
            color: #333;
        }

        .coord-item small {
            color: #888;
            margin-left: 5px;
        }

        .status-badge {
            display: inline-block;
            padding: 4px 12px;
            border-radius: 20px;
            font-size: 12px;
            font-weight: 600;
            margin-left: 10px;
        }

        .status-pending {
            background: #fff3cd;
            color: #856404;
        }

        .status-success {
            background: #d4edda;
            color: #155724;
        }

        .status-error {
            background: #f8d7da;
            color: #721c24;
        }

        .submit-section {
            text-align: center;
            padding-top: 20px;
            border-top: 2px solid #e0e0e0;
        }

        .btn-submit {
            padding: 15px 50px;
            font-size: 16px;
        }

        .photo-upload {
            border: 3px dashed #ccc;
            border-radius: 15px;
            padding: 30px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .photo-upload:hover {
            border-color: #667eea;
            background: rgba(102, 126, 234, 0.05);
        }

        .photo-upload i {
            font-size: 40px;
            color: #ccc;
            margin-bottom: 10px;
        }

        .photo-upload p {
            color: #888;
            font-size: 14px;
        }

        .photo-upload input[type="file"] {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            opacity: 0;
            cursor: pointer;
        }

        .photo-preview {
            max-width: 150px;
            max-height: 150px;
            border-radius: 10px;
            margin-top: 10px;
            display: none;
        }

        .error-message {
            color: #e74c3c;
            font-size: 12px;
            margin-top: 5px;
            display: none;
        }

        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.5);
            z-index: 1000;
            justify-content: center;
            align-items: center;
        }

        .modal-content {
            background: white;
            padding: 40px;
            border-radius: 20px;
            text-align: center;
            max-width: 400px;
            animation: slideIn 0.3s ease;
        }

        .modal-content i {
            font-size: 60px;
            color: #38ef7d;
            margin-bottom: 20px;
        }

        .modal-content h2 {
            color: #333;
            margin-bottom: 10px;
        }

        .modal-content p {
            color: #888;
            margin-bottom: 20px;
        }

        @keyframes slideIn {
            from {
                transform: translateY(-50px);
                opacity: 0;
            }
            to {
                transform: translateY(0);
                opacity: 1;
            }
        }

        @media (max-width: 768px) {
            .form-grid {
                grid-template-columns: 1fr;
            }

            .coordinate-display {
                grid-template-columns: 1fr;
            }

            .header h1 {
                font-size: 22px;
            }

            .map-controls {
                flex-direction: column;
            }

            .btn {
                width: 100%;
                justify-content: center;
            }
        }

        .loading-spinner {
            display: none;
            width: 20px;
            height: 20px;
            border: 3px solid #f3f3f3;
            border-top: 3px solid #667eea;
            border-radius: 50%;
            animation: spin 1s linear infinite;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        .info-box {
            background: #e3f2fd;
            border-left: 4px solid #2196f3;
            padding: 15px;
            border-radius: 0 10px 10px 0;
            margin-bottom: 20px;
            font-size: 13px;
            color: #1565c0;
        }

        .info-box i {
            margin-right: 8px;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <div class="logo-bps">
                <i class="fas fa-chart-bar"></i>
            </div>
            <h1>FORM BIODATA PETUGAS SE 2026</h1>
            <p>Badan Pusat Statistik Republik Indonesia | Sensus Ekonomi 2026</p>
        </div>

        <div class="form-body">
            <div class="info-box">
                <i class="fas fa-info-circle"></i>
                Harap isi semua data dengan lengkap dan benar. Koordinat lokasi wajib diisi menggunakan fitur geotagging di bawah.
            </div>

            <form id="biodataForm">
                <!-- Data Pribadi -->
                <div class="section-title">
                    <i class="fas fa-user"></i>
                    Data Pribadi
                </div>

                <div class="form-grid">
                    <div class="form-group">
                        <label>Nama Lengkap <span class="required">*</span></label>
                        <input type="text" name="nama_lengkap" placeholder="Masukkan nama lengkap" required>
                        <span class="error-message">Nama lengkap wajib diisi</span>
                    </div>

                    <div class="form-group">
                        <label>NIK <span class="required">*</span></label>
                        <input type="text" name="nik" placeholder="16 digit NIK" maxlength="16" pattern="[0-9]{16}" required>
                        <span class="error-message">NIK harus 16 digit angka</span>
                    </div>

                    <div class="form-group">
                        <label>NIP (jika PNS)</label>
                        <input type="text" name="nip" placeholder="Masukkan NIP (opsional)">
                    </div>

                    <div class="form-group">
                        <label>Jenis Kelamin <span class="required">*</span></label>
                        <select name="jenis_kelamin" required>
                            <option value="">-- Pilih Jenis Kelamin --</option>
                            <option value="Laki-laki">Laki-laki</option>
                            <option value="Perempuan">Perempuan</option>
                        </select>
                        <span class="error-message">Pilih jenis kelamin</span>
                    </div>

                    <div class="form-group">
                        <label>Tempat Lahir <span class="required">*</span></label>
                        <input type="text" name="tempat_lahir" placeholder="Kota kelahiran" required>
                        <span class="error-message">Tempat lahir wajib diisi</span>
                    </div>

                    <div class="form-group">
                        <label>Tanggal Lahir <span class="required">*</span></label>
                        <input type="date" name="tanggal_lahir" required>
                        <span class="error-message">Tanggal lahir wajib diisi</span>
                    </div>

                    <div class="form-group">
                        <label>Agama <span class="required">*</span></label>
                        <select name="agama" required>
                            <option value="">-- Pilih Agama --</option>
                            <option value="Islam">Islam</option>
                            <option value="Kristen">Kristen</option>
                            <option value="Katolik">Katolik</option>
                            <option value="Hindu">Hindu</option>
                            <option value="Buddha">Buddha</option>
                            <option value="Konghucu">Konghucu</option>
                            <option value="Lainnya">Lainnya</option>
                        </select>
                        <span class="error-message">Pilih agama</span>
                    </div>

                    <div class="form-group">
                        <label>Status Perkawinan <span class="required">*</span></label>
                        <select name="status_perkawinan" required>
                            <option value="">-- Pilih Status --</option>
                            <option value="Belum Kawin">Belum Kawin</option>
                            <option value="Kawin">Kawin</option>
                            <option value="Cerai Hidup">Cerai Hidup</option>
                            <option value="Cerai Mati">Cerai Mati</option>
                        </select>
                        <span class="error-message">Pilih status perkawinan</span>
                    </div>
                </div>

                <!-- Kontak -->
                <div class="section-title">
                    <i class="fas fa-address-book"></i>
                    Informasi Kontak
                </div>

                <div class="form-grid">
                    <div class="form-group">
                        <label>Nomor HP (WhatsApp) <span class="required">*</span></label>
                        <input type="tel" name="no_hp" placeholder="08xxxxxxxxxx" pattern="[0-9]{10,13}" required>
                        <span class="error-message">Nomor HP tidak valid</span>
                    </div>

                    <div class="form-group">
                        <label>Email <span class="required">*</span></label>
                        <input type="email" name="email" placeholder="email@example.com" required>
                        <span class="error-message">Email tidak valid</span>
                    </div>

                    <div class="form-group full-width">
                        <label>Alamat Lengkap <span class="required">*</span></label>
                        <textarea name="alamat" placeholder="Jalan, RT/RW, Kelurahan, Kecamatan, Kabupaten/Kota, Provinsi, Kode Pos" required></textarea>
                        <span class="error-message">Alamat wajib diisi</span>
                    </div>
                </div>

                <!-- Data Kepegawaian -->
                <div class="section-title">
                    <i class="fas fa-briefcase"></i>
                    Data Kepegawaian SE 2026
                </div>

                <div class="form-grid">
                    <div class="form-group">
                        <label>Status Kepegawaian <span class="required">*</span></label>
                        <select name="status_pegawai" required>
                            <option value="">-- Pilih Status --</option>
                            <option value="PNS BPS">PNS BPS</option>
                            <option value="PPNPN">PPNPN</option>
                            <option value="Mitra Statistik">Mitra Statistik</option>
                            <option value="Petugas Lapangan">Petugas Lapangan</option>
                            <option value="Lainnya">Lainnya</option>
                        </select>
                        <span class="error-message">Pilih status kepegawaian</span>
                    </div>

                    <div class="form-group">
                        <label>Jabatan <span class="required">*</span></label>
                        <select name="jabatan" required>
                            <option value="">-- Pilih Jabatan --</option>
                            <option value="Pengawas">Pengawas</option>
                            <option value="Ketua Tim">Ketua Tim</option>
                            <option value="Petugas Cacah">Petugas Cacah</option>
                            <option value="Petugas Entry">Petugas Entry</option>
                            <option value="Petugas Pemeriksa">Petugas Pemeriksa</option>
                            <option value="Koordinator">Koordinator</option>
                        </select>
                        <span class="error-message">Pilih jabatan</span>
                    </div>

                    <div class="form-group">
                        <label>Wilayah Kerja (Provinsi) <span class="required">*</span></label>
                        <select name="provinsi" required>
                            <option value="">-- Pilih Provinsi --</option>
                            <option value="Aceh">Aceh</option>
                            <option value="Sumatera Utara">Sumatera Utara</option>
                            <option value="Sumatera Barat">Sumatera Barat</option>
                            <option value="Riau">Riau</option>
                            <option value="Jambi">Jambi</option>
                            <option value="Sumatera Selatan">Sumatera Selatan</option>
                            <option value="Bengkulu">Bengkulu</option>
                            <option value="Lampung">Lampung</option>
                            <option value="Kep. Bangka Belitung">Kep. Bangka Belitung</option>
                            <option value="Kep. Riau">Kep. Riau</option>
                            <option value="DKI Jakarta">DKI Jakarta</option>
                            <option value="Jawa Barat">Jawa Barat</option>
                            <option value="Jawa Tengah">Jawa Tengah</option>
                            <option value="DI Yogyakarta">DI Yogyakarta</option>
                            <option value="Jawa Timur">Jawa Timur</option>
                            <option value="Banten">Banten</option>
                            <option value="Bali">Bali</option>
                            <option value="Nusa Tenggara Barat">Nusa Tenggara Barat</option>
                            <option value="Nusa Tenggara Timur">Nusa Tenggara Timur</option>
                            <option value="Kalimantan Barat">Kalimantan Barat</option>
                            <option value="Kalimantan Tengah">Kalimantan Tengah</option>
                            <option value="Kalimantan Selatan">Kalimantan Selatan</option>
                            <option value="Kalimantan Timur">Kalimantan Timur</option>
                            <option value="Kalimantan Utara">Kalimantan Utara</option>
                            <option value="Sulawesi Utara">Sulawesi Utara</option>
                            <option value="Sulawesi Tengah">Sulawesi Tengah</option>
                            <option value="Sulawesi Selatan">Sulawesi Selatan</option>
                            <option value="Sulawesi Tenggara">Sulawesi Tenggara</option>
                            <option value="Gorontalo">Gorontalo</option>
                            <option value="Sulawesi Barat">Sulawesi Barat</option>
                            <option value="Maluku">Maluku</option>
                            <option value="Maluku Utara">Maluku Utara</option>
                            <option value="Papua">Papua</option>
                            <option value="Papua Barat">Papua Barat</option>
                            <option value="Papua Selatan">Papua Selatan</option>
                            <option value="Papua Tengah">Papua Tengah</option>
                            <option value="Papua Pegunungan">Papua Pegunungan</option>
                            <option value="Papua Barat Daya">Papua Barat Daya</option>
                        </select>
                        <span class="error-message">Pilih provinsi</span>
                    </div>

                    <div class="form-group">
                        <label>Kabupaten/Kota <span class="required">*</span></label>
                        <input type="text" name="kabupaten" placeholder="Nama kabupaten/kota" required>
                        <span class="error-message">Kabupaten/Kota wajib diisi</span>
                    </div>

                    <div class="form-group">
                        <label>Kecamatan <span class="required">*</span></label>
                        <input type="text" name="kecamatan" placeholder="Nama kecamatan" required>
                        <span class="error-message">Kecamatan wajib diisi</span>
                    </div>

                    <div class="form-group">
                        <label>No. SK Penugasan</label>
                        <input type="text" name="no_sk" placeholder="Nomor SK penugasan (jika ada)">
                    </div>
                </div>

                <!-- Foto -->
                <div class="section-title">
                    <i class="fas fa-camera"></i>
                    Foto Diri
                </div>

                <div class="form-group full-width">
                    <div class="photo-upload" id="photoUpload">
                        <i class="fas fa-cloud-upload-alt"></i>
                        <p><strong>Klik atau seret foto diri ke sini</strong></p>
                        <p>Format: JPG, PNG (Maks. 2MB)</p>
                        <input type="file" name="foto" accept="image/*" id="fotoInput">
                        <img id="photoPreview" class="photo-preview" alt="Preview">
                    </div>
                </div>

                <!-- Geotagging -->
                <div class="section-title">
                    <i class="fas fa-map-marker-alt"></i>
                    Geotagging Lokasi
                    <span class="status-badge status-pending" id="geoStatus">Belum Ditentukan</span>
                </div>

                <div class="info-box">
                    <i class="fas fa-map-pin"></i>
                    Klik tombol "Ambil Lokasi Saya" untuk mendapatkan koordinat GPS secara otomatis, atau klik langsung pada peta untuk menentukan lokasi manual.
                </div>

                <div class="map-section">
                    <div class="map-container">
                        <div id="map"></div>
                    </div>

                    <div class="map-controls">
                        <button type="button" class="btn btn-primary" id="btnGetLocation">
                            <i class="fas fa-location-arrow"></i>
                            Ambil Lokasi Saya
                            <div class="loading-spinner" id="locationSpinner"></div>
                        </button>
                        <button type="button" class="btn btn-secondary" id="btnResetMap">
                            <i class="fas fa-undo"></i>
                            Reset Peta
                        </button>
                    </div>

                    <div class="coordinate-display">
                        <div class="coord-item">
                            <i class="fas fa-globe"></i>
                            <div>
                                <div>Latitude</div>
                                <span id="latValue">-</span>
                                <small id="latDms"></small>
                            </div>
                        </div>
                        <div class="coord-item">
                            <i class="fas fa-globe-americas"></i>
                            <div>
                                <div>Longitude</div>
                                <span id="lngValue">-</span>
                                <small id="lngDms"></small>
                            </div>
                        </div>
                        <div class="coord-item">
                            <i class="fas fa-compass"></i>
                            <div>
                                <div>Akurasi</div>
                                <span id="accuracyValue">-</span>
                                <small>meter</small>
                            </div>
                        </div>
                        <div class="coord-item">
                            <i class="fas fa-clock"></i>
                            <div>
                                <div>Waktu</div>
                                <span id="timestampValue">-</span>
                            </div>
                        </div>
                    </div>

                    <input type="hidden" name="latitude" id="latitude">
                    <input type="hidden" name="longitude" id="longitude">
                    <input type="hidden" name="accuracy" id="accuracy">
                    <input type="hidden" name="timestamp" id="timestamp">
                </div>

                <div class="submit-section">
                    <button type="submit" class="btn btn-success btn-submit">
                        <i class="fas fa-paper-plane"></i>
                        Simpan Biodata
                    </button>
                </div>
            </form>
        </div>
    </div>

    <!-- Modal Sukses -->
    <div class="modal" id="successModal">
        <div class="modal-content">
            <i class="fas fa-check-circle"></i>
            <h2>Berhasil Disimpan!</h2>
            <p>Data biodata dan lokasi geotagging telah berhasil disimpan.</p>
            <button class="btn btn-primary" onclick="closeModal()">
                <i class="fas fa-check"></i>
                OK
            </button>
        </div>
    </div>

    <!-- Leaflet JS -->
    <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js" 
            integrity="sha256-20nQCchB9co0qIjJZRGuk2/Z9VM+kNiyxNV1lvTlZBo=" 
            crossorigin=""></script>

    <script>
        // Inisialisasi peta
        const map = L.map('map').setView([-2.5489, 118.0149], 5);

        // Tambah layer OpenStreetMap
        L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
            attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors',
            maxZoom: 19
        }).addTo(map);

        let marker = null;
        let circle = null;

        // Fungsi untuk update tampilan koordinat
        function updateCoordinateDisplay(lat, lng, accuracy = null, timestamp = null) {
            document.getElementById('latValue').textContent = lat.toFixed(6);
            document.getElementById('lngValue').textContent = lng.toFixed(6);

            // Konversi ke DMS
            document.getElementById('latDms').textContent = convertToDMS(lat, 'lat');
            document.getElementById('lngDms').textContent = convertToDMS(lng, 'lng');

            if (accuracy !== null) {
                document.getElementById('accuracyValue').textContent = accuracy.toFixed(1);
            }

            if (timestamp !== null) {
                const date = new Date(timestamp);
                document.getElementById('timestampValue').textContent = date.toLocaleString('id-ID');
            }

            // Update hidden inputs
            document.getElementById('latitude').value = lat;
            document.getElementById('longitude').value = lng;
            if (accuracy !== null) document.getElementById('accuracy').value = accuracy;
            if (timestamp !== null) document.getElementById('timestamp').value = timestamp;
        }

        // Konversi ke DMS
        function convertToDMS(coord, type) {
            const absolute = Math.abs(coord);
            const degrees = Math.floor(absolute);
            const minutesNotTruncated = (absolute - degrees) * 60;
            const minutes = Math.floor(minutesNotTruncated);
            const seconds = ((minutesNotTruncated - minutes) * 60).toFixed(2);

            let direction = '';
            if (type === 'lat') {
                direction = coord >= 0 ? 'N' : 'S';
            } else {
                direction = coord >= 0 ? 'E' : 'W';
            }

            return `${degrees}° ${minutes}' ${seconds}" ${direction}`;
        }

        // Fungsi untuk menambah marker
        function addMarker(lat, lng, accuracy = null) {
            // Hapus marker dan circle lama
            if (marker) map.removeLayer(marker);
            if (circle) map.removeLayer(circle);

            // Tambah marker baru
            marker = L.marker([lat, lng], {
                draggable: true
            }).addTo(map);

            // Tambah circle untuk akurasi
            if (accuracy) {
                circle = L.circle([lat, lng], {
                    radius: accuracy,
                    color: '#667eea',
                    fillColor: '#667eea',
                    fillOpacity: 0.1
                }).addTo(map);
            }

            // Popup
            marker.bindPopup(`
                <b>Lokasi Terpilih</b><br>
                Lat: ${lat.toFixed(6)}<br>
                Lng: ${lng.toFixed(6)}<br>
                ${accuracy ? `Akurasi: ${accuracy.toFixed(1)} m` : ''}
            `).openPopup();

            // Event drag marker
            marker.on('dragend', function(e) {
                const pos = e.target.getLatLng();
                updateCoordinateDisplay(pos.lat, pos.lng);
                if (circle) {
                    circle.setLatLng([pos.lat, pos.lng]);
                }
            });

            // Update status
            const statusBadge = document.getElementById('geoStatus');
            statusBadge.textContent = 'Lokasi Tertentukan';
            statusBadge.className = 'status-badge status-success';
        }

        // Klik pada peta
        map.on('click', function(e) {
            const lat = e.latlng.lat;
            const lng = e.latlng.lng;
            addMarker(lat, lng);
            updateCoordinateDisplay(lat, lng);
        });

        // Ambil lokasi pengguna
        document.getElementById('btnGetLocation').addEventListener('click', function() {
            const spinner = document.getElementById('locationSpinner');
            const btn = this;

            if (!navigator.geolocation) {
                alert('Browser Anda tidak mendukung geolokasi.');
                return;
            }

            spinner.style.display = 'inline-block';
            btn.disabled = true;

            navigator.geolocation.getCurrentPosition(
                function(position) {
                    const lat = position.coords.latitude;
                    const lng = position.coords.longitude;
                    const accuracy = position.coords.accuracy;
                    const timestamp = position.timestamp;

                    // Update peta
                    map.setView([lat, lng], 16);
                    addMarker(lat, lng, accuracy);
                    updateCoordinateDisplay(lat, lng, accuracy, timestamp);

                    spinner.style.display = 'none';
                    btn.disabled = false;
                },
                function(error) {
                    let message = 'Gagal mendapatkan lokasi.';
                    switch(error.code) {
                        case error.PERMISSION_DENIED:
                            message = 'Akses lokasi ditolak. Mohon izinkan akses lokasi di browser Anda.';
                            break;
                        case error.POSITION_UNAVAILABLE:
                            message = 'Informasi lokasi tidak tersedia.';
                            break;
                        case error.TIMEOUT:
                            message = 'Waktu permintaan lokasi habis.';
                            break;
                    }
                    alert(message);
                    spinner.style.display = 'none';
                    btn.disabled = false;
                },
                {
                    enableHighAccuracy: true,
                    timeout: 10000,
                    maximumAge: 0
                }
            );
        });

        // Reset peta
        document.getElementById('btnResetMap').addEventListener('click', function() {
            if (marker) map.removeLayer(marker);
            if (circle) map.removeLayer(circle);
            marker = null;
            circle = null;

            map.setView([-2.5489, 118.0149], 5);

            document.getElementById('latValue').textContent = '-';
            document.getElementById('lngValue').textContent = '-';
            document.getElementById('latDms').textContent = '';
            document.getElementById('lngDms').textContent = '';
            document.getElementById('accuracyValue').textContent = '-';
            document.getElementById('timestampValue').textContent = '-';

            document.getElementById('latitude').value = '';
            document.getElementById('longitude').value = '';
            document.getElementById('accuracy').value = '';
            document.getElementById('timestamp').value = '';

            const statusBadge = document.getElementById('geoStatus');
            statusBadge.textContent = 'Belum Ditentukan';
            statusBadge.className = 'status-badge status-pending';
        });

        // Preview foto
        document.getElementById('fotoInput').addEventListener('change', function(e) {
            const file = e.target.files[0];
            if (file) {
                if (file.size > 2 * 1024 * 1024) {
                    alert('Ukuran file maksimal 2MB');
                    this.value = '';
                    return;
                }

                const reader = new FileReader();
                reader.onload = function(e) {
                    const preview = document.getElementById('photoPreview');
                    preview.src = e.target.result;
                    preview.style.display = 'block';
                };
                reader.readAsDataURL(file);
            }
        });

        // Validasi form
        function validateForm() {
            let isValid = true;
            const requiredFields = document.querySelectorAll('[required]');

            requiredFields.forEach(field => {
                const formGroup = field.closest('.form-group');
                const errorMsg = formGroup.querySelector('.error-message');

                if (!field.value.trim()) {
                    field.classList.add('error');
                    if (errorMsg) errorMsg.style.display = 'block';
                    isValid = false;
                } else {
                    field.classList.remove('error');
                    if (errorMsg) errorMsg.style.display = 'none';
                }

                // Validasi NIK
                if (field.name === 'nik' && field.value.length !== 16) {
                    field.classList.add('error');
                    if (errorMsg) errorMsg.style.display = 'block';
                    isValid = false;
                }

                // Validasi email
                if (field.name === 'email' && field.value) {
                    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
                    if (!emailRegex.test(field.value)) {
                        field.classList.add('error');
                        if (errorMsg) errorMsg.style.display = 'block';
                        isValid = false;
                    }
                }
            });

            // Validasi lokasi
            if (!document.getElementById('latitude').value) {
                alert('Mohon tentukan lokasi menggunakan fitur geotagging terlebih dahulu.');
                isValid = false;
            }

            return isValid;
        }

        // Submit form
        document.getElementById('biodataForm').addEventListener('submit', function(e) {
            e.preventDefault();

            if (!validateForm()) return;

            // Di sini biasanya akan mengirim data ke server
            // Untuk demo, kita tampilkan modal sukses

            const formData = new FormData(this);
            const data = {};
            formData.forEach((value, key) => {
                data[key] = value;
            });

            console.log('Data yang akan dikirim:', data);

            // Tampilkan modal sukses
            document.getElementById('successModal').style.display = 'flex';
        });

        // Tutup modal
        function closeModal() {
            document.getElementById('successModal').style.display = 'none';
            // Reset form
            document.getElementById('biodataForm').reset();
            document.getElementById('btnResetMap').click();
            document.getElementById('photoPreview').style.display = 'none';
        }

        // Hilangkan error saat input
        document.querySelectorAll('input, select, textarea').forEach(field => {
            field.addEventListener('input', function() {
                this.classList.remove('error');
                const formGroup = this.closest('.form-group');
                const errorMsg = formGroup.querySelector('.error-message');
                if (errorMsg) errorMsg.style.display = 'none';
            });
        });

        // Coba ambil lokasi otomatis saat halaman dimuat
        window.addEventListener('load', function() {
            if (navigator.geolocation) {
                navigator.geolocation.getCurrentPosition(
                    function(position) {
                        const lat = position.coords.latitude;
                        const lng = position.coords.longitude;
                        const accuracy = position.coords.accuracy;
                        const timestamp = position.timestamp;

                        map.setView([lat, lng], 16);
                        addMarker(lat, lng, accuracy);
                        updateCoordinateDisplay(lat, lng, accuracy, timestamp);
                    },
                    function() {
                        // Gagal, biarkan default
                    },
                    {
                        enableHighAccuracy: true,
                        timeout: 5000,
                        maximumAge: 0
                    }
                );
            }
        });
    </script>
</body>
</html>
