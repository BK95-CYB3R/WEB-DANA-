<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>DANA Receipt Fix GitHub</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Inter', sans-serif; -webkit-font-smoothing: antialiased; }
        body { background-color: #f2f2f2; display: flex; flex-direction: column; align-items: center; width: 100%; overflow-x: hidden; }

        #capture {
            width: 100%;
            max-width: 412px;
            background-color: white; 
            position: relative;
            padding-bottom: 25px;
        }

        /* Header Biru Super Rapat */
        .blue-header {
            background-color: #108ee9;
            height: 155px; 
            width: 100%;
            position: absolute;
            top: 0;
            z-index: 1;
        }

        .header-content { 
            display: flex; 
            align-items: center; 
            color: white; 
            padding: 10px 18px; 
            position: relative; 
            z-index: 2; 
        }
        .back-btn { font-size: 26px; margin-right: 12px; font-weight: 300; }
        .header-title { font-size: 18px; font-weight: 500; }

        /* Kartu dengan Watermark Inline */
        .card {
            background-color: white;
            /* Watermark Pola Dana (Inline SVG agar tidak hilang) */
            background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='100' height='40' viewBox='0 0 100 40'%3E%3Ctext x='10' y='30' fill='%23108ee9' font-family='Arial' font-size='12' font-weight='bold' opacity='0.04' transform='rotate(-20 50 20)'%3EDANA%3C/text%3E%3C/svg%3E");
            background-size: 180px auto;
            background-position: calc(100% + 40px) 40%;
            border-radius: 14px;
            position: relative;
            z-index: 3;
            margin: 10px 16px 0 16px; 
            box-shadow: 0 4px 20px rgba(0,0,0,0.06);
            overflow: hidden;
            padding-top: 25px;
        }

        .px-20 { padding: 0 22px; }

        /* Logo Dana Inline SVG */
        .logo-section { text-align: center; margin-bottom: 20px; } 
        .logo-dana-svg { width: 140px; fill: #108ee9; }

        .meta-row {
            display: flex; 
            justify-content: space-between; 
            padding-bottom: 12px; 
            color: #888; 
            font-size: 12px;
        }

        .separator {
            width: 100%;
            border-top: 2px dashed #f0f0f0;
            margin-bottom: 18px;
            background: white;
        }

        .status-row { display: flex; align-items: center; margin-bottom: 10px; }
        .status-text { color: #828282; font-weight: 500; font-size: 14px; }
        .check-circle { width: 18px; height: 18px; background: #2ecc71; border-radius: 50%; color: white; display: flex; align-items: center; justify-content: center; font-size: 11px; margin-right: 8px; font-weight: bold; }

        .description { 
            font-size: 14.5px; 
            font-weight: 700; 
            line-height: 1.45; 
            color: #3d3d3d; /* Hitam lebih soft */
            margin-bottom: 22px; 
            letter-spacing: -0.2px;
        }

        /* Total Bayar */
        .total-box {
            background-color: #f1f9ff; 
            display: flex; 
            justify-content: space-between;
            align-items: center; 
            padding: 15px 16px; 
            border-radius: 10px; 
            margin-bottom: 22px;
        }
        .total-label { font-weight: 700; font-size: 13.5px; color: #333; }
        .amount-container { display: flex; align-items: center; }
        .amount { font-weight: 700; font-size: 16.5px; color: #222; letter-spacing: -0.3px; }
        .icon-v { color: #b0b0b0; font-size: 10px; margin-left: 8px; }

        .method-row { display: flex; justify-content: space-between; padding-bottom: 15px; }
        .method-label { color: #888; font-size: 13.5px; }
        .method-value { text-align: right; font-weight: 500; color: #333; font-size: 13.5px; line-height: 1.4; }

        /* Admin Panel Responsif */
        .admin-panel { width: 100%; max-width: 412px; background: white; padding: 20px; border-top: 1px solid #ddd; margin-top: 10px; }
        .input-group { margin-bottom: 12px; }
        .input-group label { display: block; font-size: 11px; font-weight: 700; color: #666; margin-bottom: 4px; }
        .input-group input { width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 8px; font-size: 14px; }
        .btn-save { width: 100%; padding: 15px; background: #108ee9; color: white; border: none; border-radius: 10px; font-weight: 700; cursor: pointer; }
    </style>
</head>
<body>

<div id="capture">
    <div class="blue-header"></div>
    <div class="header-content">
        <span class="back-btn">‹</span>
        <span class="header-title">Detail Transaksi</span>
    </div>

    <div class="card">
        <div class="px-20">
            <div class="logo-section">
                <svg class="logo-dana-svg" viewBox="0 0 300 100">
                    <path d="M38.8,73.4c-14.7,0-26.6-11.9-26.6-26.6s11.9-26.6,26.6-26.6s26.6,11.9,26.6,26.6S53.5,73.4,38.8,73.4z M102,30.5h16.2v39h-16.2V30.5z M144.3,30.5h16.2v39h-16.2V30.5z M186.6,30.5h16.2v39h-16.2V30.5z M228.9,30.5h16.2v39h-16.2V30.5z"/>
                    <text x="75" y="65" font-family="Arial" font-size="45" font-weight="900" fill="#108ee9">DANA</text>
                </svg>
            </div>
            <div class="meta-row">
                <span id="txt-waktu">-- --- 2026 • --:--</span>
                <span>ID DANA <span id="id-f">0851</span>••••<span id="id-b">9152</span></span>
            </div>
        </div>

        <div class="separator"></div>

        <div class="px-20">
            <div class="status-row">
                <div class="check-circle">✓</div>
                <span class="status-text">Transaksi berhasil!</span>
            </div>

            <div class="description">
                Kirim Uang <span id="disp-nom1">Rp0</span> ke <span id="txt-nama">...</span> - <span id="txt-bank">BANK</span> ••••<span id="txt-rek">0000</span>
            </div>

            <div class="total-box">
                <span class="total-label">Total Bayar</span>
                <div class="amount-container">
                    <span class="amount" id="disp-nom2">Rp0</span>
                    <span class="icon-v">▼</span>
                </div>
            </div>

            <div class="method-row">
                <span class="method-label">Metode Pembayaran</span>
                <span class="method-value">Saldo DANA<br>(SmartPay)</span>
            </div>
        </div>
    </div>
</div>

<div class="admin-panel">
    <div class="input-group"><label>NOMINAL</label><input type="number" id="in-nom" value="1500000" oninput="upd()"></div>
    <div class="input-group"><label>NAMA</label><input type="text" id="in-nama" value="BAYU KURNIAWAN" oninput="upd()"></div>
    <div class="input-group"><label>ID DANA DEPAN/BELAKANG</label>
        <div style="display:flex; gap:5px;">
            <input type="text" id="in-id-f" value="0851" maxlength="4">
            <input type="text" id="in-id-b" value="9152" maxlength="4">
        </div>
    </div>
    <button class="btn-save" onclick="save()">SIMPAN GAMBAR</button>
</div>

<script>
    function formatRupiah(angka) {
        return "Rp" + new Intl.NumberFormat('id-ID').format(angka);
    }

    function upd() {
        const nom = document.getElementById('in-nom').value;
        const formatted = formatRupiah(nom);
        document.getElementById('disp-nom1').innerText = formatted;
        document.getElementById('disp-nom2').innerText = formatted;
        document.getElementById('txt-nama').innerText = document.getElementById('in-nama').value;
        document.getElementById('id-f').innerText = document.getElementById('in-id-f').value;
        document.getElementById('id-b').innerText = document.getElementById('in-id-b').value;
    }

    function save() {
        html2canvas(document.querySelector("#capture"), {
            scale: 3,
            useCORS: true,
            allowTaint: true,
            backgroundColor: "#f2f2f2"
        }).then(canvas => {
            const link = document.createElement('a');
            link.download = 'Receipt_DANA.png';
            link.href = canvas.toDataURL();
            link.click();
        });
    }

    // Set waktu otomatis saat load
    const d = new Date();
    const m = ["Jan", "Feb", "Mar", "Apr", "Mei", "Jun", "Jul", "Agu", "Sep", "Okt", "Nov", "Des"];
    document.getElementById('txt-waktu').innerText = d.getDate() + " " + m[d.getMonth()] + " 2026 • " + d.getHours().toString().padStart(2,'0') + ":" + d.getMinutes().toString().padStart(2,'0');
    upd();
</script>

</body>
</html>
