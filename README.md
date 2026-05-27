<!DOCTYPE html>
<html lang="id">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistem Informasi Hasil TKA 2026 | SD Islam Sultan Agung 4</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap"
        rel="stylesheet">

    <style>
        body {
            font-family: 'Poppins', sans-serif;
            background-color: #ffffff;
            background-image:
                linear-gradient(to right, #f1f5f9 1px, transparent 1px),
                linear-gradient(to bottom, #f1f5f9 1px, transparent 1px);
            background-size: 20px 20px;
            display: flex;
            flex-direction: column;
            min-height: 100vh;
            overflow-x: hidden;
        }

        .fade-in {
            animation: fadeIn 0.3s ease-in-out;
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(5px);
            }

            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
    </style>
</head>

<body>

    <header class="bg-[#254eba] text-white py-6 shadow-md relative z-10">
        <div class="container mx-auto px-4 text-center">
            <h1 class="text-2xl md:text-3xl font-bold tracking-wide">Portal Layanan Pengumuman TKA</h1>
            <p class="text-lg mt-1">SD Islam Sultan Agung 4</p>
            <p class="text-sm font-light mt-1">Dinas Pendidikan Kota Semarang - Tahun 2026</p>
        </div>
    </header>

    <main class="flex-grow container mx-auto px-4 py-8 flex flex-col items-center justify-center">

        <div
            class="w-full max-w-2xl bg-white rounded-xl shadow-[0_0_15px_rgba(0,0,0,0.05)] border border-gray-100 overflow-hidden relative z-10 min-h-[380px]">

            <div id="formTka" class="p-6 md:p-8">
                <div class="text-center mb-8">
                    <h2 class="text-[#1e3a8a] text-xl font-bold">Cek Hasil Tes Kemampuan Akademik (TKA)</h2>
                    <p class="text-gray-500 text-sm mt-2">Masukkan NISN dan Tanggal Lahir Siswa secara benar untuk
                        melihat detail nilai</p>
                </div>

                <form onsubmit="handleTKA(event)" class="space-y-5">
                    <div>
                        <label for="nisnTka" class="block text-sm font-medium text-gray-700 mb-1">Nomor Induk Siswa
                            Nasional (NISN)</label>
                        <input type="text" id="nisnTka" required placeholder="Masukkan 10 digit nomor NISN"
                            class="w-full px-4 py-2.5 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none transition text-gray-700">
                    </div>
                    <div>
                        <label for="ttlTka" class="block text-sm font-medium text-gray-700 mb-1">Tanggal Lahir
                            Siswa</label>
                        <input type="date" id="ttlTka" required
                            class="w-full px-4 py-2.5 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none transition text-gray-700">
                    </div>
                    <button type="submit"
                        class="w-full bg-[#2563eb] hover:bg-blue-700 text-white font-semibold py-3 px-4 rounded-lg shadow-md transition duration-200">
                        Cek Hasil TKA
                    </button>
                </form>
                <div id="errorTka"
                    class="hidden mt-4 p-3 bg-red-50 border border-red-200 text-red-600 rounded-lg text-sm text-center">
                    Data tidak ditemukan. Silakan periksa kembali kombinasi NISN dan Tanggal Lahir Anda.
                </div>
            </div>

            <div id="resultTkaLunas" class="hidden fade-in p-6 md:p-8">
                <h2 class="text-center text-[#1e3a8a] text-xl font-bold mb-6">Detail Hasil Nilai TKA 2026</h2>

                <div class="bg-gray-50 border border-gray-200 rounded-xl p-5 mb-6">
                    <div class="grid grid-cols-3 gap-2 mb-3 border-b border-gray-200 pb-3">
                        <span class="text-gray-500 text-sm">Nama Lengkap</span>
                        <span class="text-gray-900 font-bold col-span-2 uppercase" id="resNamaTkaL"></span>
                    </div>
                    <div class="grid grid-cols-3 gap-2">
                        <span class="text-gray-500 text-sm">NISN</span>
                        <span class="text-gray-900 col-span-2 font-medium" id="resNisnTkaL"></span>
                    </div>
                </div>

                <div class="flex flex-row justify-between gap-4 mb-8">
                    <div class="flex-1 bg-blue-50 rounded-xl p-4 text-center border border-blue-100">
                        <p class="text-xs text-gray-500 uppercase tracking-wider mb-1">Matematika</p>
                        <p class="text-3xl font-bold text-[#1e3a8a]" id="resMtkTka"></p>
                        <p class="text-sm font-medium text-blue-600 mt-1" id="resMtkKetTka"></p>
                    </div>
                    <div class="flex-1 bg-emerald-50 rounded-xl p-4 text-center border border-emerald-100">
                        <p class="text-xs text-gray-500 uppercase tracking-wider mb-1">B. Indonesia</p>
                        <p class="text-3xl font-bold text-emerald-700" id="resIndoTka"></p>
                        <p class="text-sm font-medium text-emerald-600 mt-1" id="resIndoKetTka"></p>
                    </div>
                </div>

                <div class="text-center">
                    <button onclick="resetViews()"
                        class="px-6 py-2 border border-gray-300 rounded-lg text-gray-600 hover:bg-gray-50 transition">Kembali
                        ke Pencarian</button>
                </div>
            </div>

            <div id="resultTkaTerkunci" class="hidden fade-in p-6 md:p-8 text-center">
                <div
                    class="inline-flex items-center justify-center w-15 h-15 p-4 bg-red-100 rounded-full mb-4 text-red-600">
                    <svg class="w-10 h-10" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2">
                        <path stroke-linecap="round" stroke-linejoin="round"
                            d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z" />
                    </svg>
                </div>
                <div class="bg-red-50 border border-red-200 rounded-lg p-2.5 inline-block mb-3">
                    <span class="text-red-700 font-bold text-xs tracking-wider">AKSES BLOKIR: ADMINISTRASI BELUM
                        SELESAI</span>
                </div>
                <h2 class="text-xl font-bold text-gray-800 mb-1" id="resNamaTkaM"></h2>
                <p class="text-sm text-gray-500 mb-4" id="resNisnTkaM"></p>

                <div
                    class="bg-red-50 border-l-4 border-red-500 p-4 text-left rounded-r-lg mb-6 text-red-800 text-sm leading-relaxed">
                    <p class="font-bold mb-1">Nilai Kompetensi Akademik Terkunci</p>
                    <p>Mohon maaf, lembar capaian hasil ujian Tes Kemampuan Akademik (TKA) Kota Semarang milik siswa
                        yang bersangkutan ditangguhkan. Nilai baru dapat terbuka di sistem pendaftaran setelah
                        administrasi keuangan sekolah diselesaikan.</p>
                </div>
                <button onclick="resetViews()"
                    class="px-6 py-2 border border-gray-300 rounded-lg text-gray-600 hover:bg-gray-50 transition">Kembali
                    ke Pencarian</button>
            </div>

        </div>
    </main>

    <footer class="bg-[#1e293b] text-gray-400 text-center py-4 text-xs z-10 w-full mt-auto">
        <p>&copy; 2026 SD Islam Sultan Agung 4 Semarang. Hak Cipta Dilindungi.</p>
    </footer>

    <script>
        // --- DATA 53 SISWA TERBUKA ---
        const databaseSiswa = [
            { nisn: "0135842803", nama: "MUHAMMAD AZMI KANZA MAZAYA", ttl: "2013-11-29", isLunas: true, tkaMtk: "63.33", tkaMtkKet: "Baik", tkaIndo: "76.67", tkaIndoKet: "Baik" },
            { nisn: "0148076661", nama: "Muhammad Rizal Ababil", ttl: "2014-02-12", isLunas: true, tkaMtk: "63.33", tkaMtkKet: "Baik", tkaIndo: "43.33", tkaIndoKet: "Kurang" },
            { nisn: "0147387218", nama: "HABIBAH MAHZA CANTIKA SYAHRUL", ttl: "2014-03-05", isLunas: true, tkaMtk: "46.67", tkaMtkKet: "Memadai", tkaIndo: "80.00", tkaIndoKet: "Baik" },
            { nisn: "0143223416", nama: "Alvaro Gavriel Putra", ttl: "2014-06-02", isLunas: true, tkaMtk: "50.00", tkaMtkKet: "Memadai", tkaIndo: "60.00", tkaIndoKet: "Memadai" },
            { nisn: "0143285427", nama: "NAJWA FEBRIANI", ttl: "2014-02-19", isLunas: true, tkaMtk: "53.33", tkaMtkKet: "Memadai", tkaIndo: "76.67", tkaIndoKet: "Baik" },
            { nisn: "0135147720", nama: "MUHAMMAD FARHAN PURNOMO", ttl: "2013-08-24", isLunas: true, tkaMtk: "56.67", tkaMtkKet: "Baik", tkaIndo: "83.33", tkaIndoKet: "Baik" },
            { nisn: "3135783058", nama: "Muhammad Dzaky Faeyza Eshan", ttl: "2013-10-03", isLunas: true, tkaMtk: "43.33", tkaMtkKet: "Memadai", tkaIndo: "63.33", tkaIndoKet: "Memadai" },
            { nisn: "0138579281", nama: "Azzam El Fatahillah", ttl: "2013-12-04", isLunas: true, tkaMtk: "73.33", tkaMtkKet: "Baik", tkaIndo: "83.33", tkaIndoKet: "Baik" },
            { nisn: "0135156214", nama: "Aqilah Sania Az-Zahra", ttl: "2013-11-13", isLunas: true, tkaMtk: "76.67", tkaMtkKet: "Baik", tkaIndo: "86.67", tkaIndoKet: "Baik" },
            { nisn: "0143282396", nama: "BILQIS AZKA ADZKIA", ttl: "2014-04-27", isLunas: true, tkaMtk: "36.67", tkaMtkKet: "Memadai", tkaIndo: "33.33", tkaIndoKet: "Kurang" },
            { nisn: "3149785202", nama: "Jovita Darla Callista", ttl: "2014-07-10", isLunas: true, tkaMtk: "53.33", tkaMtkKet: "Memadai", tkaIndo: "83.33", tkaIndoKet: "Baik" },
            { nisn: "0144985290", nama: "NISWA SHABIRA RAMADHANI", ttl: "2014-07-15", isLunas: true, tkaMtk: "46.67", tkaMtkKet: "Memadai", tkaIndo: "70.00", tkaIndoKet: "Memadai" },
            { nisn: "0148574434", nama: "SABILILLAH RASYA BRAWIJAYA", ttl: "2014-06-03", isLunas: true, tkaMtk: "60.00", tkaMtkKet: "Baik", tkaIndo: "76.67", tkaIndoKet: "Baik" },
            { nisn: "3132455130", nama: "SYIFA AMIRA RAMADHANI", ttl: "2013-07-25", isLunas: true, tkaMtk: "70.00", tkaMtkKet: "Baik", tkaIndo: "86.67", tkaIndoKet: "Baik" },
            { nisn: "0133335301", nama: "Alfatin Shiddiqiyyah", ttl: "2013-09-16", isLunas: true, tkaMtk: "70.00", tkaMtkKet: "Baik", tkaIndo: "76.67", tkaIndoKet: "Baik" },
            { nisn: "0138334867", nama: "Allena Hasiana tondang", ttl: "2013-10-07", isLunas: true, tkaMtk: "40.00", tkaMtkKet: "Memadai", tkaIndo: "63.33", tkaIndoKet: "Memadai" },
            { nisn: "0132748560", nama: "Mohammad Rafi Saputra", ttl: "2013-04-01", isLunas: true, tkaMtk: "46.67", tkaMtkKet: "Memadai", tkaIndo: "76.67", tkaIndoKet: "Baik" },
            { nisn: "3140534208", nama: "Namia Saufa Tatung", ttl: "2014-08-21", isLunas: true, tkaMtk: "50.00", tkaMtkKet: "Memadai", tkaIndo: "66.67", tkaIndoKet: "Memadai" },
            { nisn: "3137491418", nama: "Azkafa Imammil Hakim", ttl: "2013-12-13", isLunas: true, tkaMtk: "76.67", tkaMtkKet: "Baik", tkaIndo: "70.00", tkaIndoKet: "Memadai" },
            { nisn: "0141988810", nama: "Muhammad Nur Fa'iz", ttl: "2014-05-13", isLunas: true, tkaMtk: "40.00", tkaMtkKet: "Memadai", tkaIndo: "66.67", tkaIndoKet: "Memadai" },
            { nisn: "0142739625", nama: "VIRZHA SATRIA ANAMSYAH", ttl: "2014-06-04", isLunas: true, tkaMtk: "50.00", tkaMtkKet: "Memadai", tkaIndo: "56.67", tkaIndoKet: "Memadai" },
            { nisn: "0142658145", nama: "GIUSEPPE MEAZZA NUGROHO", ttl: "2014-02-23", isLunas: true, tkaMtk: "50.00", tkaMtkKet: "Memadai", tkaIndo: "70.00", tkaIndoKet: "Memadai" },
            { nisn: "0134745525", nama: "KINAN MEISYA LISTIYANI", ttl: "2013-05-13", isLunas: true, tkaMtk: "40.00", tkaMtkKet: "Memadai", tkaIndo: "73.33", tkaIndoKet: "Memadai" },
            { nisn: "0142491633", nama: "FIEBYA AZ ZAHRA SYARAFANA", ttl: "2014-02-07", isLunas: true, tkaMtk: "83.33", tkaMtkKet: "Baik", tkaIndo: "83.33", tkaIndoKet: "Baik" },
            { nisn: "0131070979", nama: "WILDAN TAUFIQURROHMAN SETYAWAN", ttl: "2013-04-07", isLunas: true, tkaMtk: "36.67", tkaMtkKet: "Memadai", tkaIndo: "56.67", tkaIndoKet: "Memadai" },
            { nisn: "0136760226", nama: "Devin Azka Abidin", ttl: "2013-09-27", isLunas: true, tkaMtk: "73.33", tkaMtkKet: "Baik", tkaIndo: "76.67", tkaIndoKet: "Baik" },
            { nisn: "0137551333", nama: "MUHAMMAD RASKA YUDHA", ttl: "2013-06-23", isLunas: true, tkaMtk: "53.33", tkaMtkKet: "Memadai", tkaIndo: "70.00", tkaIndoKet: "Memadai" },
            { nisn: "0139213089", nama: "JIHAN MIRZA LIANA", ttl: "2013-11-18", isLunas: true, tkaMtk: "30.00", tkaMtkKet: "Kurang", tkaIndo: "60.00", tkaIndoKet: "Memadai" },
            { nisn: "0147335009", nama: "Syaffira Kayla Krissandewa", ttl: "2014-08-22", isLunas: true, tkaMtk: "66.67", tkaMtkKet: "Baik", tkaIndo: "76.67", tkaIndoKet: "Baik" },
            { nisn: "3149998747", nama: "GAYATRI CONDRORINI", ttl: "2014-01-08", isLunas: true, tkaMtk: "66.67", tkaMtkKet: "Baik", tkaIndo: "80.00", tkaIndoKet: "Baik" },
            { nisn: "0138534800", nama: "DAMIA DEWI KHAIRUNISA", ttl: "2013-06-26", isLunas: true, tkaMtk: "53.33", tkaMtkKet: "Memadai", tkaIndo: "76.67", tkaIndoKet: "Baik" },
            { nisn: "0145016379", nama: "MUHAMMAD DZAKY SAPUTRA", ttl: "2014-04-25", isLunas: true, tkaMtk: "36.67", tkaMtkKet: "Memadai", tkaIndo: "50.00", tkaIndoKet: "Memadai" },
            { nisn: "0144945158", nama: "LATFIA PERMATASARI", ttl: "2014-03-01", isLunas: true, tkaMtk: "26.67", tkaMtkKet: "Kurang", tkaIndo: "80.00", tkaIndoKet: "Baik" },
            { nisn: "0141926348", nama: "AFFAN BAKHTIAR", ttl: "2014-03-21", isLunas: true, tkaMtk: "63.33", tkaMtkKet: "Baik", tkaIndo: "50.00", tkaIndoKet: "Memadai" },
            { nisn: "0131024281", nama: "Aqila Yusra Jihantoro", ttl: "2013-08-28", isLunas: true, tkaMtk: "50.00", tkaMtkKet: "Memadai", tkaIndo: "76.67", tkaIndoKet: "Baik" },
            { nisn: "0147027600", nama: "NAVYSHA AQILLA MAULIDA AZZAHRA", ttl: "2014-01-26", isLunas: true, tkaMtk: "66.67", tkaMtkKet: "Baik", tkaIndo: "86.67", tkaIndoKet: "Baik" },
            { nisn: "0146304412", nama: "ADZKIA KHAIRUNNISA", ttl: "2014-06-25", isLunas: true, tkaMtk: "20.00", tkaMtkKet: "Kurang", tkaIndo: "40.00", tkaIndoKet: "Kurang" },
            { nisn: "3141762816", nama: "Alesha Davina Aditya Maharani", ttl: "2014-05-16", isLunas: true, tkaMtk: "90.00", tkaMtkKet: "Baik", tkaIndo: "90.00", tkaIndoKet: "Baik" },
            { nisn: "0139979532", nama: "Mochammad Ghias Maulana", ttl: "2013-11-27", isLunas: true, tkaMtk: "56.67", tkaMtkKet: "Baik", tkaIndo: "66.67", tkaIndoKet: "Memadai" },
            { nisn: "0139235906", nama: "AZKA KUSUMA RAFLI", ttl: "2013-06-19", isLunas: true, tkaMtk: "43.33", tkaMtkKet: "Memadai", tkaIndo: "66.67", tkaIndoKet: "Memadai" },
            { nisn: "0139361226", nama: "FAHRI TSAQIF ARRASYID", ttl: "2013-12-09", isLunas: true, tkaMtk: "60.00", tkaMtkKet: "Baik", tkaIndo: "93.33", tkaIndoKet: "Baik" },
            { nisn: "0139957550", nama: "Jovita Darla Callista", ttl: "2013-11-23", isLunas: true, tkaMtk: "56.67", tkaMtkKet: "Baik", tkaIndo: "90.00", tkaIndoKet: "Baik" },
            { nisn: "3137169358", nama: "Abdillah Gustan Satvik", ttl: "2013-12-17", isLunas: true, tkaMtk: "60.00", tkaMtkKet: "Baik", tkaIndo: "83.33", tkaIndoKet: "Baik" },
            { nisn: "0134713573", nama: "IFFA IZZA HISANIYA", ttl: "2013-09-22", isLunas: true, tkaMtk: "66.67", tkaMtkKet: "Baik", tkaIndo: "73.33", tkaIndoKet: "Memadai" },
            { nisn: "0133464886", nama: "MAULANA DZAKWAN HAFIZUDDIN", ttl: "2013-03-23", isLunas: true, tkaMtk: "60.00", tkaMtkKet: "Baik", tkaIndo: "66.67", tkaIndoKet: "Memadai" },
            { nisn: "0136027543", nama: "SHALSHA EDHITA NOVI PRIMADANI", ttl: "2013-11-08", isLunas: true, tkaMtk: "53.33", tkaMtkKet: "Memadai", tkaIndo: "60.00", tkaIndoKet: "Memadai" },
            { nisn: "0145176473", nama: "MUHAMMAD NOOR AL HUDA", ttl: "2014-02-07", isLunas: true, tkaMtk: "60.00", tkaMtkKet: "Baik", tkaIndo: "70.00", tkaIndoKet: "Memadai" },
            { nisn: "0147798028", nama: "NADIYA DZAKIRA", ttl: "2014-03-26", isLunas: true, tkaMtk: "63.33", tkaMtkKet: "Baik", tkaIndo: "80.00", tkaIndoKet: "Baik" },
            { nisn: "3142071602", nama: "Talita Uswah Zaenada", ttl: "2014-06-08", isLunas: true, tkaMtk: "56.67", tkaMtkKet: "Baik", tkaIndo: "70.00", tkaIndoKet: "Memadai" },
            { nisn: "0144813932", nama: "MUHAMMAD EMYR FIRDAUS", ttl: "2014-03-06", isLunas: true, tkaMtk: "46.67", tkaMtkKet: "Memadai", tkaIndo: "80.00", tkaIndoKet: "Baik" },
            { nisn: "0144403569", nama: "NAJWA ASSYIFA", ttl: "2014-09-10", isLunas: true, tkaMtk: "73.33", tkaMtkKet: "Baik", tkaIndo: "90.00", tkaIndoKet: "Baik" },
            { nisn: "0136035834", nama: "ABDUL KHALIK", ttl: "2013-04-28", isLunas: true, tkaMtk: "86.67", tkaMtkKet: "Baik", tkaIndo: "90.00", tkaIndoKet: "Baik" },
            { nisn: "0141298962", nama: "AL MAY RAIHAN DZAKY PRAYITNO", ttl: "2014-05-24", isLunas: true, tkaMtk: "63.33", tkaMtkKet: "Baik", tkaIndo: "73.33", tkaIndoKet: "Memadai" }
        ];

        // --- HANDLER CEK NILAI TKA ---
        function handleTKA(e) {
            e.preventDefault();
            const inputNisn = document.getElementById('nisnTka').value.trim();
            const inputTtl = document.getElementById('ttlTka').value;

            // Cari kecocokan data siswa di database terenkripsi
            const siswa = databaseSiswa.find(s => s.nisn === inputNisn && s.ttl === inputTtl);

            if (siswa) {
                document.getElementById('errorTka').classList.add('hidden');
                document.getElementById('formTka').classList.add('hidden');

                if (siswa.isLunas) {
                    // JIKA LUNAS -> NILAI TERBUKA (BOX HIJAU/BIRU)
                    document.getElementById('resNamaTkaL').innerText = siswa.nama;
                    document.getElementById('resNisnTkaL').innerText = siswa.nisn;
                    document.getElementById('resMtkTka').innerText = siswa.tkaMtk;
                    document.getElementById('resMtkKetTka').innerText = `(${siswa.tkaMtkKet})`;
                    document.getElementById('resIndoTka').innerText = siswa.tkaIndo;
                    document.getElementById('resIndoKetTka').innerText = `(${siswa.tkaIndoKet})`;
                    document.getElementById('resultTkaLunas').classList.remove('hidden');
                } else {
                    // JIKA BELUM LUNAS -> AKSES DIBLOKIR (BOX MERAH GEMBOK)
                    document.getElementById('resNamaTkaM').innerText = siswa.nama;
                    document.getElementById('resNisnTkaM').innerText = `NISN: ${siswa.nisn}`;
                    document.getElementById('resultTkaTerkunci').classList.remove('hidden');
                }
            } else {
                // JIKA DATA TIDAK COCOK / SALAH INPUT
                document.getElementById('errorTka').classList.remove('hidden');
            }
        }

        // --- RE-SET KE LAYAR PENCARIAN AWAL ---
        function resetViews() {
            document.getElementById('nisnTka').value = '';
            document.getElementById('ttlTka').value = '';

            document.getElementById('errorTka').classList.add('hidden');
            document.getElementById('resultTkaLunas').classList.add('hidden');
            document.getElementById('resultTkaTerkunci').classList.add('hidden');

            document.getElementById('formTka').classList.remove('hidden');
        }
    </script>
</body>

</html>
