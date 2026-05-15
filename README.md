# dyasabela

<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>Notespace · Aplikasi Catatan</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
        }

        body {
            background: linear-gradient(145deg, #f3f5fc 0%, #eef2f9 100%);
            font-family: system-ui, 'Segoe UI', 'Inter', 'Helvetica Neue', sans-serif;
            padding: 1.5rem 1rem 2rem;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        /* container utama seperti kartu kertas */
        .app-container {
            max-width: 1000px;
            width: 100%;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.75);
            backdrop-filter: blur(2px);
            border-radius: 2.5rem;
            box-shadow: 0 20px 35px -12px rgba(0, 0, 0, 0.2), 0 1px 3px rgba(0, 0, 0, 0.05);
            overflow: hidden;
            transition: all 0.2s ease;
        }

        /* header dengan sentuhan kreatif */
        .header {
            background: #ffffffdd;
            backdrop-filter: blur(8px);
            padding: 1.2rem 1.8rem;
            border-bottom: 1px solid rgba(0, 0, 0, 0.05);
            display: flex;
            flex-wrap: wrap;
            justify-content: space-between;
            align-items: baseline;
            gap: 0.8rem;
        }

        .title-section h1 {
            font-size: 1.85rem;
            font-weight: 700;
            background: linear-gradient(135deg, #1F2B4E, #2C3E66);
            background-clip: text;
            -webkit-background-clip: text;
            color: transparent;
            letter-spacing: -0.3px;
        }

        .title-section p {
            font-size: 0.8rem;
            color: #5b6e8c;
            margin-top: 4px;
        }

        .stats {
            background: #eef2fa;
            padding: 0.4rem 1rem;
            border-radius: 40px;
            font-size: 0.85rem;
            font-weight: 500;
            color: #1f2b4e;
            box-shadow: inset 0 0 0 1px rgba(255,255,255,0.7), 0 1px 2px rgba(0,0,0,0.05);
        }

        /* panel input */
        .input-area {
            padding: 1.6rem 1.8rem 1.2rem;
            background: #ffffffcc;
            border-bottom: 1px solid #e4e9f2;
        }

        .note-input {
            width: 100%;
            border: 1px solid #cdd9ed;
            border-radius: 1.5rem;
            padding: 1rem 1.2rem;
            font-size: 1rem;
            font-family: inherit;
            background: white;
            resize: vertical;
            transition: 0.2s;
            box-shadow: 0 1px 2px rgba(0,0,0,0.02);
        }

        .note-input:focus {
            outline: none;
            border-color: #5c7cba;
            box-shadow: 0 0 0 3px rgba(92, 124, 186, 0.2);
        }

        .action-buttons {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            margin-top: 1rem;
            justify-content: flex-end;
        }

        button {
            background: #f0f3fa;
            border: none;
            padding: 0.6rem 1.3rem;
            border-radius: 2rem;
            font-weight: 600;
            font-size: 0.85rem;
            font-family: inherit;
            cursor: pointer;
            transition: 0.2s;
            display: inline-flex;
            align-items: center;
            gap: 6px;
            color: #1f2b4e;
            box-shadow: 0 1px 1px rgba(0,0,0,0.05);
        }

        button i {
            font-style: normal;
            font-weight: 600;
            font-size: 1.1rem;
        }

        .btn-primary {
            background: #2c3e66;
            color: white;
            box-shadow: 0 4px 8px -2px rgba(44, 62, 102, 0.3);
        }

        .btn-primary:hover {
            background: #1f2f52;
            transform: translateY(-1px);
        }

        .btn-secondary:hover {
            background: #e6ecf5;
            transform: translateY(-1px);
        }

        button:active {
            transform: translateY(1px);
        }

        /* daftar catatan */
        .notes-list-container {
            padding: 1.2rem 1.8rem 1.8rem;
            background: #fbfdff;
        }

        .notes-header {
            display: flex;
            justify-content: space-between;
            align-items: baseline;
            margin-bottom: 1rem;
            flex-wrap: wrap;
        }

        .notes-header h2 {
            font-size: 1.3rem;
            font-weight: 600;
            color: #1a263b;
        }

        .clear-btn {
            background: none;
            box-shadow: none;
            color: #b91c1c;
            font-size: 0.75rem;
            padding: 0.3rem 0.8rem;
            background: #fff0f0;
        }

        .clear-btn:hover {
            background: #ffe0e0;
        }

        .notes-grid {
            display: flex;
            flex-direction: column;
            gap: 12px;
        }

        .note-card {
            background: white;
            border-radius: 1.2rem;
            padding: 1rem 1.2rem;
            transition: all 0.2s;
            border: 1px solid #eef2f9;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.02);
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            gap: 12px;
        }

        .note-card:hover {
            border-color: #cddef5;
            box-shadow: 0 8px 18px -10px rgba(0, 0, 0, 0.1);
            background: #ffffff;
        }

        .note-content {
            flex: 1;
            word-break: break-word;
            white-space: pre-wrap;
            line-height: 1.45;
            color: #1f2c44;
            font-size: 0.95rem;
        }

        .note-meta {
            display: flex;
            flex-direction: column;
            align-items: flex-end;
            gap: 8px;
            font-size: 0.7rem;
            color: #7f8fa4;
            min-width: 70px;
        }

        .timestamp {
            font-family: monospace;
            background: #f2f5fb;
            padding: 4px 8px;
            border-radius: 20px;
            font-size: 0.7rem;
        }

        .delete-note {
            background: none;
            padding: 6px 12px;
            font-size: 0.75rem;
            color: #a03e3e;
            box-shadow: none;
            background: #fef2f2;
        }

        .delete-note:hover {
            background: #ffe2e2;
            color: #a00;
        }

        .empty-message {
            text-align: center;
            padding: 2rem 1rem;
            color: #8d9bb0;
            background: #fafcff;
            border-radius: 1.5rem;
            font-style: italic;
        }

        footer {
            text-align: center;
            font-size: 0.7rem;
            padding: 1rem;
            border-top: 1px solid #e9edf4;
            color: #7d8cad;
            background: #ffffffc7;
        }

        @media (max-width: 550px) {
            body {
                padding: 0.8rem;
            }
            .input-area, .notes-list-container {
                padding: 1rem;
            }
            .note-card {
                flex-direction: column;
            }
            .note-meta {
                flex-direction: row;
                justify-content: space-between;
                width: 100%;
                align-items: center;
            }
            .delete-note {
                padding: 4px 12px;
            }
        }

        .toast-msg {
            position: fixed;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%);
            background: #1f2b4ed9;
            backdrop-filter: blur(8px);
            color: white;
            padding: 8px 20px;
            border-radius: 60px;
            font-size: 0.8rem;
            pointer-events: none;
            z-index: 1000;
            transition: opacity 0.2s;
            font-weight: 500;
        }
    </style>
</head>
<body>

<div class="app-container">
    <div class="header">
        <div class="title-section">
            <h1>📘 Notespace</h1>
            <p>catatan cepat, selalu bersamamu</p>
        </div>
        <div class="stats" id="statsCounter">0 catatan</div>
    </div>

    <div class="input-area">
        <textarea id="noteInput" class="note-input" rows="3" placeholder="Tulis catatanmu di sini... misalnya: ✓ Beli bahan masakan, ✓ tugas matematika, ide desain baru..."></textarea>
        <div class="action-buttons">
            <button id="addNoteBtn" class="btn-primary">➕ Tambah catatan</button>
            <button id="resetFormBtn" class="btn-secondary">🗑️ Bersihkan form</button>
        </div>
    </div>

    <div class="notes-list-container">
        <div class="notes-header">
            <h2>📌 Semua catatan</h2>
            <button id="deleteAllBtn" class="clear-btn">Hapus semua</button>
        </div>
        <div id="notesContainer" class="notes-grid">
            <!-- catatan akan dirender dynamic -->
            <div class="empty-message">✨ Belum ada catatan. Mulai dengan menulis di atas!</div>
        </div>
    </div>
    <footer>
        💾 catatan tersimpan secara lokal di perangkatmu — data aman
    </footer>
</div>

<div id="toastMsg" class="toast-msg" style="opacity:0;">Notifikasi</div>

<script>
    (function(){
        // ---------- Storage key ----------
        const STORAGE_KEY = "notespace_notes_app";
        
        // ---------- Data model ----------
        let notes = [];     // setiap note: { id, text, timestamp }

        // DOM elements
        const noteInputEl = document.getElementById('noteInput');
        const addBtn = document.getElementById('addNoteBtn');
        const resetFormBtn = document.getElementById('resetFormBtn');
        const notesContainer = document.getElementById('notesContainer');
        const statsCounter = document.getElementById('statsCounter');
        const deleteAllBtn = document.getElementById('deleteAllBtn');

        // toast helper
        let toastTimeout = null;
        function showToast(message, duration = 2000) {
            const toast = document.getElementById('toastMsg');
            if (toastTimeout) clearTimeout(toastTimeout);
            toast.innerText = message;
            toast.style.opacity = '1';
            toastTimeout = setTimeout(() => {
                toast.style.opacity = '0';
            }, duration);
        }

        // simpan ke localStorage
        function persistNotes() {
            localStorage.setItem(STORAGE_KEY, JSON.stringify(notes));
        }

        // muat data awal
        function loadNotes() {
            const stored = localStorage.getItem(STORAGE_KEY);
            if(stored) {
                try {
                    const parsed = JSON.parse(stored);
                    if(Array.isArray(parsed)) {
                        notes = parsed;
                    } else {
                        notes = [];
                    }
                } catch(e) {
                    notes = [];
                }
            } else {
                // data default contoh agar tidak kosong total (opsional)
                notes = [];
                // uncomment jika ingin demo contoh:
                // notes = [{ id: Date.now()+1, text: "Selamat datang di Notespace! ✨\nKlik 'Tambah catatan' untuk mulai.", timestamp: Date.now() }];
                // persistNotes();
            }
            renderNotes();
        }

        // render seluruh daftar catatan + update stats
        function renderNotes() {
            if(!notesContainer) return;

            if(notes.length === 0) {
                notesContainer.innerHTML = `<div class="empty-message">📭 Tidak ada catatan ...  tulis ide menarikmu ✍️</div>`;
                statsCounter.innerText = `0 catatan`;
                return;
            }

            // urutkan dari yang baru ke lama (descending timestamp)
            const sortedNotes = [...notes].sort((a,b) => b.timestamp - a.timestamp);
            
            let html = '';
            for(let note of sortedNotes) {
                const formattedDate = formatDate(note.timestamp);
                // escape text untuk menghindari XSS (text aman)
                const safeText = escapeHtml(note.text);
                html += `
                    <div class="note-card" data-id="${note.id}">
                        <div class="note-content">${safeText.replace(/\n/g, '<br>')}</div>
                        <div class="note-meta">
                            <span class="timestamp">📅 ${formattedDate}</span>
                            <button class="delete-note" data-id="${note.id}">🗑️ Hapus</button>
                        </div>
                    </div>
                `;
            }
            notesContainer.innerHTML = html;
            statsCounter.innerText = `${notes.length} catatan ${notes.length > 1 ? '' : ''}`;
            
            // attach event listener ke setiap tombol hapus (delegation lebih baik, tapi kita attach setelah render)
            const deleteBtns = document.querySelectorAll('.delete-note');
            deleteBtns.forEach(btn => {
                btn.addEventListener('click', (e) => {
                    e.stopPropagation();
                    const idStr = btn.getAttribute('data-id');
                    if(idStr) {
                        const id = Number(idStr);
                        deleteNoteById(id);
                    }
                });
            });
        }

        // helper escape html sederhana
        function escapeHtml(str) {
            if(!str) return '';
            return str
                .replace(/&/g, '&amp;')
                .replace(/</g, '&lt;')
                .replace(/>/g, '&gt;')
                .replace(/"/g, '&quot;')
                .replace(/'/g, '&#39;');
        }

        // format timestamp menjadi jam:menit tgl/bulan
        function formatDate(timestamp) {
            if(!timestamp) return 'baru saja';
            const date = new Date(timestamp);
            const now = new Date();
            const isToday = date.toDateString() === now.toDateString();
            if(isToday) {
                return date.toLocaleTimeString('id-ID', { hour: '2-digit', minute: '2-digit' });
            } else {
                return `${date.getDate()}/${date.getMonth()+1} ${date.getHours().toString().padStart(2,'0')}:${date.getMinutes().toString().padStart(2,'0')}`;
            }
        }

        // tambah catatan baru
        function addNote() {
            let rawText = noteInputEl.value.trim();
            if(rawText === "") {
                showToast("⚠️ Catatan tidak boleh kosong!", 1500);
                // beri efek getar pada input (opsional)
                noteInputEl.style.borderColor = "#dd8888";
                setTimeout(() => { noteInputEl.style.borderColor = "#cdd9ed"; }, 500);
                return;
            }
            
            const newNote = {
                id: Date.now(),
                text: rawText,
                timestamp: Date.now()
            };
            notes.push(newNote);
            persistNotes();
            renderNotes();
            // reset form setelah berhasil tambah
            noteInputEl.value = "";
            showToast("✅ Catatan berhasil ditambahkan!", 1500);
            noteInputEl.focus();
        }

        // hapus catatan berdasarkan id
        function deleteNoteById(id) {
            const beforeLength = notes.length;
            notes = notes.filter(note => note.id !== id);
            if(notes.length !== beforeLength) {
                persistNotes();
                renderNotes();
                showToast("🗑️ Catatan dihapus", 1200);
            } else {
                showToast("Catatan tidak ditemukan", 1000);
            }
        }

        // hapus semua catatan (konfirmasi)
        function deleteAllNotes() {
            if(notes.length === 0) {
                showToast("Tidak ada catatan untuk dihapus", 1000);
                return;
            }
            const confirmDelete = confirm("⚠️ Hapus SEMUA catatan? Tindakan ini tidak dapat dibatalkan.");
            if(confirmDelete) {
                notes = [];
                persistNotes();
                renderNotes();
                showToast("🧹 Semua catatan telah dihapus", 1500);
            }
        }

        // reset form (bersihkan textarea)
        function resetForm() {
            noteInputEl.value = "";
            noteInputEl.focus();
            showToast("Formulir dibersihkan", 1000);
        }

        // event listener untuk tombol tambah (support enter? optional: shortcut)
        function handleKeyPress(e) {
            // shortcut: Ctrl+Enter atau Cmd+Enter (di textarea) untuk menambah catatan
            if((e.ctrlKey || e.metaKey) && e.key === 'Enter') {
                e.preventDefault();
                addNote();
            }
        }

        // inisialisasi event dan load data
        function init() {
            loadNotes();
            addBtn.addEventListener('click', addNote);
            resetFormBtn.addEventListener('click', resetForm);
            deleteAllBtn.addEventListener('click', deleteAllNotes);
            noteInputEl.addEventListener('keydown', handleKeyPress);
            // optional: jika pengguna menekan enter tanpa modifier hanya pindah baris (biarkan default)
            // fokus ke input saat pertama load
            noteInputEl.focus();
        }

        // jalankan ketika DOM siap
        if(document.readyState === 'loading') {
            document.addEventListener('DOMContentLoaded', init);
        } else {
            init();
        }
    })();
</script>
</body>
</html>s
