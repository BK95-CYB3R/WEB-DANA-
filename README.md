<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DANA Receipt Perfect Balance</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Inter', sans-serif; -webkit-font-smoothing: antialiased; }
        body { background-color: #f5f5f5; display: flex; flex-direction: column; align-items: center; padding: 10px 0; }

        #capture {
            width: 100%;
            max-width: 412px;
            background-color: white; 
            position: relative;
            padding-bottom: 20px;
        }

        /* HEADER BIRU - Dibuat pas di tengah-tengah kartu */
        .blue-header {
            background-color: #108ee9;
            height: 215px; /* Disesuaikan agar berhenti di tengah kartu */
            width: 100%;
            padding: 5px 14px;
            position: absolute;
            top: 0;
            z-index: 1;
        }

        .header-content { display: flex; align-items: center; color: white; padding: 12px 5px; position: relative; z-index: 2; }
        .back-btn { font-size: 28px; margin-right: 15px; font-weight: 300; line-height: 1; }
        .header-title { font-size: 19px; font-weight: 500; }

        /* KARTU PUTIH */
        .card {
            background-color: white;
            background-image: url('bg_pattern.png');
            background-size: 380px auto;
            background-repeat: repeat;
            background-position: center 75%; 
            border-radius: 12px;
            position: relative;
            z-index: 3;
            margin: 60px 16px 0 16px; 
            border: 1px solid rgba(0,0,0,0.06);
            box-shadow: 0 8px 20px rgba(0,0,0,0.08);
            overflow: hidden;
            padding-top: 25px;
        }

        .px-20 { padding: 0 20px; }

        .logo-section { text-align: center; margin-bottom: 22px; } 
        .logo-dana { width: 160px; height: auto; }

        .meta-row {
            display: flex; justify-content: space-between; 
            padding-bottom: 12px; color: #757575; font-size: 12.5px; font-weight: 400;
        }

        .separator {
            width: 100%;
            border-top: 1.5px dashed #e8e8e8;
            margin-bottom: 18px;
        }

        .status-row { display: flex; align-items: center; margin-bottom: 10px; }
        .icon-check { width: 18px; height: 18px; margin-right: 8px; }
        .status-text { color: #828282; font-weight: 500; font-size: 14px; }

        /* Deskripsi dikurangi ukuran dan warnanya diperhalus */
        .description { 
            font-size: 14.5px; 
            font-weight: 700; 
            line-height: 1.4; 
            color: #333; /* Tidak hitam pekat agar tidak mencolok */
            margin-bottom: 25px; 
        }

        .total-box {
            background-color: #f1f9ff; display: flex; justify-content: space-between;
            align-items: center; padding: 14px; border-radius: 8px; margin-bottom: 25px;
        }
        .total-label { font-weight: 700; font-size: 14px; color: #444; }
        .amount { font-weight: 700; font-size: 18px; color: #111; display: flex; align-items: center; }
        .amount::after { content: ''; width: 5px; height: 5px; border-right: 2px solid #ccc; border-bottom: 2px solid #ccc; transform: rotate(45deg); margin-left: 10px; margin-bottom: 2px; }

        .method-row { display: flex; justify-content: space-between; align-items: flex-start; padding-bottom: 20px; }
        .method-label { color: #888; font-size: 13.5px; font-weight: 400; }
        .method-value { text-align: right; font-weight: 500; color: #222; font-size: 13.5px; line-height: 1.3; }

        /* PANEL ADMIN */
        .admin-panel { width: 100%; max-width: 412px; background: #fff; margin-top: 20px; padding: 20px; border-radius: 12px; border: 1px solid #ddd; }
        .input-group { margin-bottom: 12px; }
        .input-group label { display: block; font-size: 11px; font-weight: 700; color: #666; margin-bottom: 4px; }
        .input-group input { width: 100%; padding: 12px; border: 1px solid #ddd; border-radius: 8px; font-size: 14px; outline: none; }
        .btn-save { width: 100%; padding: 15px; background: #108ee9; color: white; border: none; border-radius: 10px; font-weight: 700; cursor: pointer; font-size: 16px; }
    </style>
</head>
<body>

<div id="capture">
    <div class="blue-header">
        <div class="header-content">
            <span class="back-btn">‹</span>
            <span class="header-title">Detail Transaksi</span>
        </div>
    </div>

    <div class="card">
        <div class="px-20">
            <div class="logo-section">
                <img src="logo_dana.png" alt="DANA" class="logo-dana">
            </div>
            <div class="meta-row">
                <span id="txt-waktu">-- --- 2026 • --:--</span>
                <span>ID DANA 0851••••<span id="txt-hp">9152</span></span>
            </div>
        </div>

        <div class="separator"></div>

        <div class="px-20">
            <div class="status-row">
                <img src="centang_ijo.png" alt="check" class="icon-check">
                <span class="status-text">Transaksi berhasil!</span>
            </div>

            <div class="description">
                Kirim Uang <span id="disp-nom1">Rp200.000</span> ke <span id="txt-nama">BAYU KURNIAWAN</span> - <span id="txt-bank">JAGO</span> ••••<span id="txt-rek">5438</span>
            </div>

            <div class="total-box">
                <span class="total-label">Total Bayar</span>
                <span class="amount" id="disp-nom2">Rp200.000</span>
            </div>

            <div class="method-row">
                <span class="method-label">Metode Pembayaran</span>
                <span class="method-value">Saldo DANA<br>(SmartPay)</span>
            </div>
        </div>
    </div>
</div>

<div class="admin-panel">
    <div class="input-group"><label>Waktu Transaksi</label><input type="text" id="in-waktu" oninput="upd()"></div>
    <div class="input-group"><label>Nominal</label><input type="number" id="in-nom" value="200000" oninput="upd()"></div>
    <div class="input-group"><label>Penerima</label><input type="text" id="in-nama" value="BAYU KURNIAWAN" oninput="upd()"></div>
    <div style="display: flex; gap: 10px;">
        <div style="flex: 2;"><label style="font-size:11px; font-weight:700;">Bank</label><input type="text" id="in-bank" value="JAGO" style="width:100%; padding:10px;" oninput="upd()"></div>
        <div style="flex: 1;"><label style="font-size:11px; font-weight:700;">Rek</label><input type="text" id="in-rek" value="5438" maxlength="4" style="width:100%; padding:10px;" oninput="upd()"></div>
    </div>
    <div class="input-group" style="margin-top:10px;"><label>Ekor ID DANA</label><input type="text" id="in-hp" value="9152" maxlength="4" oninput="upd()"></div>
    <button class="btn-save" onclick="save()">SIMPAN KE GALERI</button>
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
        document.getElementById('txt-waktu').innerText = document.getElementById('in-waktu').value;
        document.getElementById('txt-nama').innerText = document.getElementById('in-nama').value;
        document.getElementById('txt-bank').innerText = document.getElementById('in-bank').value;
        document.getElementById('txt-rek').innerText = document.getElementById('in-rek').value;
        document.getElementById('txt-hp').innerText = document.getElementById('in-hp').value;
    }

    function init() {
        const d = new Date();
        const m = ["Jan", "Feb", "Mar", "Apr", "Mei", "Jun", "Jul", "Agu", "Sep", "Okt", "Nov", "Des"];
        const str = d.getDate().toString().padStart(2, '0') + " " + m[d.getMonth()] + " " + d.getFullYear() + " • " + d.getHours().toString().padStart(2, '0') + ":" + d.getMinutes().toString().padStart(2, '0');
        document.getElementById('in-waktu').value = str;
        upd();
    }

    function save() {
        html2canvas(document.getElementById('capture'), { scale: 3 }).then(c => {
            const a = document.createElement('a');
            a.download = 'DANA_Receipt_Perfect.png';
            a.href = c.toDataURL();
            a.click();
        });
    }
    window.onload = init;
</script>

</body>
</html>
