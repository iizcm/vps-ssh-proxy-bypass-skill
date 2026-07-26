# PuTTY SOCKS Proxy Recipe (copy-paste utk user Windows non-teknis)

## Step 1 — PuTTY
1. Download PuTTY dari https://www.putty.org/ (file `putty.exe`)
2. Buka PuTTY
3. Di kotak **Host Name (or IP address)**: isi `134.199.170.183`
4. **Port**: `22` (sudah default)
5. Di kiri, klik `+ Connection` → `+ SSH` → **Tunnels**
6. Pilih tombol **Dynamic** (radio button)
7. Di kotak **Source port**: isi `1080`
8. Klik tombol **Add** → muncul tulisan `D1080` di list bawah
9. Di kiri, klik **Session** (paling atas)
10. Di kotak **Saved Sessions**: ketik `VPS-Proxy` → klik **Save**
11. Klik **Open**

## Step 2 — Login
- Jendela hitam muncul. Ketik: `root` (lalu Enter)
- Kalau minta pass → ketik pass VPS (gak kelihat saat diketik, normal)
- ATAU kalau pake key: sebelum Open, di Tunnels kembali ke **Connection → SSH → Auth → Credentials** → browse file `id_ed25519` → Open
- **BIARIN JENDELA INI TERBUKA** (minimize aja, jgn tutup)

## Step 3 — Windows Proxy
1. Windows → klik Start → ketik `proxy` → Enter (Settings → Network & Internet → Proxy)
2. Scroll ke **Manual proxy setup** → toggle **On**
3. Di **SOCKS proxy**: isi `127.0.0.1` dan port `1080`
4. Klik **Save**

## Step 4 — Test
- Buka browser → buka `bitget.com` atau `x.com`
- HARUS lancar (lewat VPS)

## Matiin proxy (kalau mau buka situs lokal biasa lebih kenceng)
- Windows proxy → Manual → toggle **Off**
- ATAU tutup jendela PuTTY

## Troubleshoot
- Bitget tetep timeout? → cek jendela PuTTY masih hidup & login sukses (ada prompt `root@...:~#`)
- Proxy gak ke-detect? → di Windows proxy pastiin SOCKS `127.0.0.1` port `1080`, BUKAN HTTP
- Lemot? → wajar (lewat VPS US), masih jauh lebih oke dr timeout total
