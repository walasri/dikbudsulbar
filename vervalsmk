<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Verifikasi Data Kondisi Listrik & Internet SMK</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f0f4f8; /* Light blue-gray background */
        }
        .form-section {
            background-color: white;
            padding: 2rem;
            border-radius: 0.75rem; /* Increased border radius */
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
            margin-bottom: 2rem;
        }
        .form-input, .form-select {
            border-radius: 0.5rem; /* Rounded inputs */
            border: 1px solid #cbd5e1; /* Softer border */
            padding: 0.75rem 1rem;
            transition: border-color 0.2s ease-in-out, box-shadow 0.2s ease-in-out;
        }
        .form-input:focus, .form-select:focus {
            border-color: #3b82f6; /* Blue border on focus */
            box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.25);
            outline: none;
        }
        .btn-primary {
            background-color: #3b82f6; /* Blue */
            color: white;
            padding: 0.75rem 1.5rem;
            border-radius: 0.5rem;
            font-weight: 500;
            transition: background-color 0.2s ease-in-out;
        }
        .btn-primary:hover {
            background-color: #2563eb; /* Darker blue */
        }
        .table-container {
            overflow-x: auto; /* Allow horizontal scrolling for table on small screens */
        }
        th, td {
            padding: 0.75rem 1rem;
            border: 1px solid #e2e8f0; /* Light gray border for table cells */
            text-align: left;
        }
        th {
            background-color: #f1f5f9; /* Very light gray for table header */
            font-weight: 600;
        }
        .modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0,0,0,0.5);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 1000;
            opacity: 0;
            visibility: hidden;
            transition: opacity 0.3s ease, visibility 0.3s ease;
        }
        .modal-content {
            background-color: white;
            padding: 2rem;
            border-radius: 0.75rem;
            box-shadow: 0 10px 25px rgba(0,0,0,0.1);
            width: 90%;
            max-width: 500px;
        }
        .modal.active {
            opacity: 1;
            visibility: visible;
        }
        .loading-spinner {
            border: 4px solid rgba(0, 0, 0, 0.1);
            border-left-color: #3b82f6;
            border-radius: 50%;
            width: 24px;
            height: 24px;
            animation: spin 1s linear infinite;
        }
        @keyframes spin {
            to { transform: rotate(360deg); }
        }
    </style>
</head>
<body class="p-4 md:p-8">
    <div class="container mx-auto max-w-5xl">
        <header class="text-center mb-8">
            <h1 class="text-3xl md:text-4xl font-bold text-gray-800">Verifikasi Data Kondisi Listrik & Internet SMK</h1>
            <p class="text-gray-600 mt-2">DINAS PENDIDIKAN DAN KEBUDAYAAN PROVINSI SULAWESI BARAT</p>
            <p class="text-sm text-gray-500 mt-1" id="userIdDisplay">User ID: Memuat...</p>
        </header>

        <form id="dataForm" class="form-section">
            <h2 class="text-2xl font-semibold text-gray-700 mb-6 border-b pb-3">Informasi Sekolah</h2>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-6">
                <div>
                    <label for="namaSekolah" class="block text-sm font-medium text-gray-700 mb-1">Nama Sekolah</label>
                    <input type="text" id="namaSekolah" name="namaSekolah" class="form-input w-full" required>
                </div>
                <div>
                    <label for="npsn" class="block text-sm font-medium text-gray-700 mb-1">NPSN</label>
                    <input type="text" id="npsn" name="npsn" class="form-input w-full" required>
                </div>
                <div>
                    <label for="alamatSekolah" class="block text-sm font-medium text-gray-700 mb-1">Alamat Sekolah</label>
                    <input type="text" id="alamatSekolah" name="alamatSekolah" class="form-input w-full">
                </div>
                <div>
                    <label for="kota" class="block text-sm font-medium text-gray-700 mb-1">Kota/Kabupaten</label>
                    <input type="text" id="kota" name="kota" class="form-input w-full">
                </div>
                <div>
                    <label for="provinsi" class="block text-sm font-medium text-gray-700 mb-1">Provinsi</label>
                    <input type="text" id="provinsi" name="provinsi" class="form-input w-full">
                </div>
            </div>

            <h2 class="text-2xl font-semibold text-gray-700 mb-6 mt-8 border-b pb-3">Kondisi Listrik</h2>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-6">
                <div>
                    <label for="listrikTersedia" class="block text-sm font-medium text-gray-700 mb-1">Listrik Tersedia?</label>
                    <select id="listrikTersedia" name="listrikTersedia" class="form-select w-full" onchange="toggleListrikDetails()">
                        <option value="ya">Ya</option>
                        <option value="tidak">Tidak</option>
                    </select>
                </div>
            </div>
            <div id="listrikDetails" class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-6">
                <div>
                    <label for="sumberListrik" class="block text-sm font-medium text-gray-700 mb-1">Sumber Listrik (bisa pilih lebih dari satu)</label>
                    <div class="space-y-2 mt-1">
                        <label class="flex items-center"><input type="checkbox" name="sumberListrik" value="PLN" class="form-checkbox rounded mr-2"> PLN</label>
                        <label class="flex items-center"><input type="checkbox" name="sumberListrik" value="Genset" class="form-checkbox rounded mr-2"> Genset</label>
                        <label class="flex items-center"><input type="checkbox" name="sumberListrik" value="Solar Panel" class="form-checkbox rounded mr-2"> Panel Surya</label>
                        <label class="flex items-center"><input type="checkbox" name="sumberListrik" value="Lainnya" class="form-checkbox rounded mr-2"> Lainnya</label>
                    </div>
                </div>
                <div>
                    <label for="dayaTerpasang" class="block text-sm font-medium text-gray-700 mb-1">Daya Terpasang (VA)</label>
                    <input type="number" id="dayaTerpasang" name="dayaTerpasang" class="form-input w-full">
                </div>
                <div>
                    <label for="listrikCukup" class="block text-sm font-medium text-gray-700 mb-1">Listrik Cukup untuk Kebutuhan Harian?</label>
                    <select id="listrikCukup" name="listrikCukup" class="form-select w-full">
                        <option value="ya">Ya</option>
                        <option value="tidak">Tidak</option>
                    </select>
                </div>
                <div class="md:col-span-2">
                    <label for="catatanListrik" class="block text-sm font-medium text-gray-700 mb-1">Catatan Tambahan Listrik</label>
                    <textarea id="catatanListrik" name="catatanListrik" rows="3" class="form-input w-full"></textarea>
                </div>
            </div>

            <h2 class="text-2xl font-semibold text-gray-700 mb-6 mt-8 border-b pb-3">Kondisi Internet</h2>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-6">
                <div>
                    <label for="internetTersedia" class="block text-sm font-medium text-gray-700 mb-1">Internet Tersedia?</label>
                    <select id="internetTersedia" name="internetTersedia" class="form-select w-full" onchange="toggleInternetDetails()">
                        <option value="ya">Ya</option>
                        <option value="tidak">Tidak</option>
                    </select>
                </div>
            </div>
            <div id="internetDetails" class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-6">
                <div>
                    <label for="namaPenyedia" class="block text-sm font-medium text-gray-700 mb-1">Nama Penyedia Layanan</label>
                    <input type="text" id="namaPenyedia" name="namaPenyedia" class="form-input w-full">
                </div>
                <div>
                    <label for="jenisKoneksi" class="block text-sm font-medium text-gray-700 mb-1">Jenis Koneksi</label>
                    <select id="jenisKoneksi" name="jenisKoneksi" class="form-select w-full">
                        <option value="Fiber Optik">Fiber Optik</option>
                        <option value="DSL">DSL</option>
                        <option value="Satelit">Satelit</option>
                        <option value="Seluler (Mobile)">Seluler (Mobile)</option>
                        <option value="Lainnya">Lainnya</option>
                    </select>
                </div>
                <div>
                    <label for="kecepatanDownload" class="block text-sm font-medium text-gray-700 mb-1">Kecepatan Download (Mbps)</label>
                    <input type="number" id="kecepatanDownload" name="kecepatanDownload" class="form-input w-full" step="0.1">
                </div>
                <div>
                    <label for="kecepatanUpload" class="block text-sm font-medium text-gray-700 mb-1">Kecepatan Upload (Mbps)</label>
                    <input type="number" id="kecepatanUpload" name="kecepatanUpload" class="form-input w-full" step="0.1">
                </div>
                <div>
                    <label for="internetStabil" class="block text-sm font-medium text-gray-700 mb-1">Internet Stabil?</label>
                    <select id="internetStabil" name="internetStabil" class="form-select w-full">
                        <option value="ya">Ya</option>
                        <option value="tidak">Tidak</option>
                    </select>
                </div>
                <div>
                    <label for="internetCukup" class="block text-sm font-medium text-gray-700 mb-1">Internet Cukup untuk Pembelajaran?</label>
                    <select id="internetCukup" name="internetCukup" class="form-select w-full">
                        <option value="ya">Ya</option>
                        <option value="tidak">Tidak</option>
                    </select>
                </div>
                <div class="md:col-span-2">
                    <label for="catatanInternet" class="block text-sm font-medium text-gray-700 mb-1">Catatan Tambahan Internet</label>
                    <textarea id="catatanInternet" name="catatanInternet" rows="3" class="form-input w-full"></textarea>
                </div>
            </div>

            <h2 class="text-2xl font-semibold text-gray-700 mb-6 mt-8 border-b pb-3">Informasi Validator</h2>
             <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-6">
                <div>
                    <label for="namaValidator" class="block text-sm font-medium text-gray-700 mb-1">Nama Validator</label>
                    <input type="text" id="namaValidator" name="namaValidator" class="form-input w-full" required>
                </div>
                <div>
                    <label for="jabatanValidator" class="block text-sm font-medium text-gray-700 mb-1">Jabatan/Posisi Validator</label>
                    <input type="text" id="jabatanValidator" name="jabatanValidator" class="form-input w-full">
                </div>
                <div>
                    <label for="tanggalValidasi" class="block text-sm font-medium text-gray-700 mb-1">Tanggal Validasi</label>
                    <input type="date" id="tanggalValidasi" name="tanggalValidasi" class="form-input w-full" required>
                </div>
            </div>

            <div class="mt-8 text-right">
                <button type="submit" class="btn-primary inline-flex items-center">
                    <span id="submitButtonText">Simpan Data</span>
                    <div id="submitSpinner" class="loading-spinner ml-2 hidden"></div>
                </button>
            </div>
        </form>

        <div class="form-section mt-12">
            <h2 class="text-2xl font-semibold text-gray-700 mb-6 border-b pb-3">Data Tersimpan</h2>
            <div id="loadingData" class="flex items-center text-gray-600">
                <div class="loading-spinner mr-2"></div>
                Memuat data...
            </div>
            <div id="noDataMessage" class="text-gray-600 hidden">Belum ada data tersimpan.</div>
            <div class="table-container mt-4">
                <table id="dataTable" class="min-w-full bg-white hidden">
                    <thead class="bg-gray-50">
                        <tr>
                            <th>Nama Sekolah</th>
                            <th>NPSN</th>
                            <th>Listrik</th>
                            <th>Internet</th>
                            <th>Validator</th>
                            <th>Tgl Validasi</th>
                            <th>Aksi</th>
                        </tr>
                    </thead>
                    <tbody id="dataTableBody">
                        </tbody>
                </table>
            </div>
        </div>
    </div>

    <div id="messageModal" class="modal">
        <div class="modal-content text-center">
            <p id="modalMessageText" class="text-lg mb-4"></p>
            <button id="modalCloseButton" class="btn-primary">Tutup</button>
        </div>
    </div>

    <script type="module">
        // Firebase and App Configuration
        const firebaseConfig = JSON.parse(typeof __firebase_config !== 'undefined' ? __firebase_config : '{}');
        const appId = typeof __app_id !== 'undefined' ? __app_id : 'default-smk-app';

        // Import Firebase modules
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, signInAnonymously, signInWithCustomToken, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, collection, addDoc, getDocs, onSnapshot, doc, deleteDoc, setLogLevel } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

        let app;
        let auth;
        let db;
        let currentUserId = null;
        let isAuthReady = false;

        // Initialize Firebase
        try {
            app = initializeApp(firebaseConfig);
            auth = getAuth(app);
            db = getFirestore(app);
            setLogLevel('debug'); // Enable Firestore logging for debugging
            console.log("Firebase initialized successfully.");
        } catch (error) {
            console.error("Error initializing Firebase:", error);
            showModal("Error initializing Firebase: " + error.message);
            // Disable form if Firebase fails to init
            document.getElementById('dataForm').querySelectorAll('input, select, button, textarea').forEach(el => el.disabled = true);
        }
        
        const userIdDisplay = document.getElementById('userIdDisplay');

        // Firebase Authentication
        onAuthStateChanged(auth, async (user) => {
            if (user) {
                currentUserId = user.uid;
                console.log("User is signed in with UID:", currentUserId);
                userIdDisplay.textContent = `User ID: ${currentUserId}`;
                isAuthReady = true;
                loadData(); // Load data once authenticated
            } else {
                console.log("User is signed out. Attempting to sign in...");
                userIdDisplay.textContent = "User ID: Mengautentikasi...";
                try {
                    if (typeof __initial_auth_token !== 'undefined' && __initial_auth_token) {
                        await signInWithCustomToken(auth, __initial_auth_token);
                        console.log("Signed in with custom token.");
                    } else {
                        await signInAnonymously(auth);
                        console.log("Signed in anonymously.");
                    }
                    // onAuthStateChanged will be triggered again after successful sign-in
                } catch (error) {
                    console.error("Error during sign-in:", error);
                    showModal("Gagal melakukan autentikasi: " + error.message);
                    userIdDisplay.textContent = "User ID: Gagal Autentikasi";
                    isAuthReady = false; // Explicitly set to false on auth failure
                }
            }
        });


        // DOM Elements
        const dataForm = document.getElementById('dataForm');
        const dataTableBody = document.getElementById('dataTableBody');
        const loadingData = document.getElementById('loadingData');
        const noDataMessage = document.getElementById('noDataMessage');
        const dataTable = document.getElementById('dataTable');
        const submitButtonText = document.getElementById('submitButtonText');
        const submitSpinner = document.getElementById('submitSpinner');

        // Modal elements
        const messageModal = document.getElementById('messageModal');
        const modalMessageText = document.getElementById('modalMessageText');
        const modalCloseButton = document.getElementById('modalCloseButton');

        modalCloseButton.addEventListener('click', () => {
            messageModal.classList.remove('active');
        });

        function showModal(message) {
            modalMessageText.textContent = message;
            messageModal.classList.add('active');
        }

        // Toggle visibility of detail sections
        window.toggleListrikDetails = function() {
            const isTersedia = document.getElementById('listrikTersedia').value === 'ya';
            document.getElementById('listrikDetails').style.display = isTersedia ? 'grid' : 'none';
        }
        window.toggleInternetDetails = function() {
            const isTersedia = document.getElementById('internetTersedia').value === 'ya';
            document.getElementById('internetDetails').style.display = isTersedia ? 'grid' : 'none';
        }
        // Initial state for detail sections
        toggleListrikDetails();
        toggleInternetDetails();


        // Firestore collection reference
        const dataCollectionPath = `artifacts/${appId}/public/data/smk_infra_data`;

        // Form Submission
        dataForm.addEventListener('submit', async function(event) {
            event.preventDefault();
            if (!isAuthReady || !currentUserId) {
                showModal("Autentikasi belum siap atau gagal. Silakan coba lagi nanti.");
                console.error("Form submission attempted before auth was ready or with no user ID.");
                return;
            }

            submitButtonText.textContent = 'Menyimpan...';
            submitSpinner.classList.remove('hidden');
            dataForm.querySelector('button[type="submit"]').disabled = true;

            const formData = new FormData(dataForm);
            const data = {};
            formData.forEach((value, key) => {
                if (key === 'sumberListrik') { // Handle checkboxes for sumberListrik
                    if (!data[key]) data[key] = [];
                    data[key].push(value);
                } else {
                    data[key] = value;
                }
            });
            data.submittedBy = currentUserId;
            data.createdAt = new Date().toISOString();

            // Clear fields that are not applicable based on Yes/No selections
            if (data.listrikTersedia === 'tidak') {
                delete data.sumberListrik;
                delete data.dayaTerpasang;
                delete data.listrikCukup;
                delete data.catatanListrik;
            }
            if (data.internetTersedia === 'tidak') {
                delete data.namaPenyedia;
                delete data.jenisKoneksi;
                delete data.kecepatanDownload;
                delete data.kecepatanUpload;
                delete data.internetStabil;
                delete data.internetCukup;
                delete data.catatanInternet;
            }


            try {
                const docRef = await addDoc(collection(db, dataCollectionPath), data);
                console.log("Document written with ID: ", docRef.id);
                showModal("Data berhasil disimpan!");
                dataForm.reset();
                toggleListrikDetails(); // Reset visibility after form reset
                toggleInternetDetails();
            } catch (error) {
                console.error("Error adding document: ", error);
                showModal("Gagal menyimpan data: " + error.message);
            } finally {
                submitButtonText.textContent = 'Simpan Data';
                submitSpinner.classList.add('hidden');
                dataForm.querySelector('button[type="submit"]').disabled = false;
            }
        });

        // Load and Display Data
        function loadData() {
            if (!isAuthReady) {
                console.log("Auth not ready, skipping data load.");
                loadingData.classList.remove('hidden');
                dataTable.classList.add('hidden');
                noDataMessage.classList.add('hidden');
                return;
            }
            if (!db) {
                console.error("Firestore db instance is not available.");
                loadingData.textContent = "Error: Koneksi database gagal.";
                return;
            }

            const dataCollectionRef = collection(db, dataCollectionPath);
            
            onSnapshot(dataCollectionRef, (querySnapshot) => {
                if (!isAuthReady) { // Double check auth readiness inside snapshot callback
                    console.log("Auth became unready during snapshot processing.");
                    return; 
                }
                dataTableBody.innerHTML = ''; // Clear existing data
                if (querySnapshot.empty) {
                    noDataMessage.classList.remove('hidden');
                    dataTable.classList.add('hidden');
                } else {
                    noDataMessage.classList.add('hidden');
                    dataTable.classList.remove('hidden');
                    querySnapshot.forEach((docSnapshot) => {
                        const entry = docSnapshot.data();
                        const row = dataTableBody.insertRow();
                        row.insertCell().textContent = entry.namaSekolah || '-';
                        row.insertCell().textContent = entry.npsn || '-';
                        row.insertCell().textContent = entry.listrikTersedia === 'ya' ? `Ya (${entry.sumberListrik ? (Array.isArray(entry.sumberListrik) ? entry.sumberListrik.join(', ') : entry.sumberListrik) : 'N/A'})` : 'Tidak';
                        row.insertCell().textContent = entry.internetTersedia === 'ya' ? `Ya (${entry.namaPenyedia || 'N/A'})` : 'Tidak';
                        row.insertCell().textContent = entry.namaValidator || '-';
                        row.insertCell().textContent = entry.tanggalValidasi ? new Date(entry.tanggalValidasi).toLocaleDateString('id-ID') : '-';
                        
                        const actionsCell = row.insertCell();
                        const deleteButton = document.createElement('button');
                        deleteButton.textContent = 'Hapus';
                        deleteButton.classList.add('text-red-500', 'hover:text-red-700', 'text-sm', 'font-medium');
                        deleteButton.onclick = async () => {
                            // Custom confirmation dialog
                            showModalWithOptions(`Anda yakin ingin menghapus data untuk ${entry.namaSekolah}?`, async () => {
                                try {
                                    await deleteDoc(doc(db, dataCollectionPath, docSnapshot.id));
                                    console.log("Document successfully deleted!");
                                    showModal("Data berhasil dihapus.");
                                } catch (error) {
                                    console.error("Error removing document: ", error);
                                    showModal("Gagal menghapus data: " + error.message);
                                }
                            });
                        };
                        actionsCell.appendChild(deleteButton);
                    });
                }
                loadingData.classList.add('hidden');
            }, (error) => {
                console.error("Error fetching data: ", error);
                loadingData.textContent = "Gagal memuat data: " + error.message;
                noDataMessage.classList.add('hidden');
                dataTable.classList.add('hidden');
            });
        }
        
        // Custom modal with options (for delete confirmation)
        function showModalWithOptions(message, onConfirm) {
            modalMessageText.innerHTML = `<p>${message}</p>`; // Use innerHTML to allow simple HTML like <p>
            
            // Remove existing buttons if any
            const existingButtons = messageModal.querySelector('.modal-buttons');
            if (existingButtons) {
                existingButtons.remove();
            }

            const buttonContainer = document.createElement('div');
            buttonContainer.classList.add('modal-buttons', 'mt-6', 'flex', 'justify-end', 'space-x-3');

            const confirmButton = document.createElement('button');
            confirmButton.textContent = 'Ya, Hapus';
            confirmButton.classList.add('btn-primary', 'bg-red-500', 'hover:bg-red-700');
            confirmButton.onclick = () => {
                onConfirm();
                messageModal.classList.remove('active');
            };

            const cancelButton = document.createElement('button');
            cancelButton.textContent = 'Batal';
            cancelButton.classList.add('btn-primary', 'bg-gray-300', 'text-gray-800', 'hover:bg-gray-400');
            cancelButton.onclick = () => {
                messageModal.classList.remove('active');
            };
            
            // Ensure modalCloseButton is hidden or repurposed if it's the only one
            modalCloseButton.style.display = 'none';


            buttonContainer.appendChild(cancelButton);
            buttonContainer.appendChild(confirmButton);
            messageModal.querySelector('.modal-content').appendChild(buttonContainer);
            
            messageModal.classList.add('active');
        }


        // Set default date for tanggalValidasi to today
        document.addEventListener('DOMContentLoaded', () => {
            const today = new Date().toISOString().split('T')[0];
            document.getElementById('tanggalValidasi').value = today;
        });

    </script>
</body>
</html>
