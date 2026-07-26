---
name: vps-ssh-proxy-bypass
description: "Bypass ISP-level website blocking (crypto exchanges, X/Twitter, OpenSea, bridges) when VPN apps/extensions/Cloudflare-Warp/ProtonVPN all FAIL because the ISP uses DPI or whitelists only certain tunnels. Technique: turn the user's OWN VPS (which they already SSH into daily, so the ISP does NOT block it) into a local SOCKS proxy via an SSH dynamic tunnel, then point Windows/Edge proxy settings at 127.0.0.1:1080. Guaranteed to work when the VPS is reachable."
---

# VPS SSH SOCKS PROXY — Bypass ISP Site Blocking

## KAPAN PAKAI
- User buka bitget/opensea/x/bridge → `ERR_CONNECTION_TIMED_OUT` / lemot terus.
- User UDAH ganti DNS (8.8.8.8), firewall router jadi Low, flushdns — TETEP block.
- VPN extension (1.1.1.1 Warp, ZenMate) → tetep lemot/block.
- VPN app (ProtonVPN, Warp desktop) → tetep block.
- Ini tandanya **ISP filter di level koneksi** (DPI / whitelist tunnel), BUKAN DNS & BUKAN router firewall. Router ZTE F672Y milik ISP sering auto-reset firewall ke High + blokir 5GHz + blokir tunnel populer.
- SOLUSI PASTI: lewat **VPS sendiri** (user punya 134.199.170.183, SSH tiap hari → ISP gak blokir).

## TEKNIK: SSH DYNAMIC TUNNEL (SOCKS5)
Traffic dibungkus dalam SSH ke VPS → ISP cuma lihat "koneksi SSH ke IP lu" (yg di-allow) → gak tau lu buka bitget.

### PuTTY (Windows) — CARA USER
1. Download PuTTY (putty.org).
2. **Host Name:** `<VPS_IP>` (user: 134.199.170.183), **Port:** 22.
3. Kiri: **Connection → SSH → Tunnels**.
4. Pilih **Dynamic**, isi **Port:** `1080`, klik **Add** (muncul `D1080`).
5. Kiri balik ke **Session** → **Save** (biar gak ulang tiap buka).
6. **Open** → login (user `root` + SSH key atau pass). **BIARIN JENDELA INI TERBUKA** (tutup = proxy mati).

### Windows proxy setting (biar semua app lewat tunnel)
- Settings → **Network & Internet → Proxy** → **Manual proxy** ON.
- **SOCKS:** `127.0.0.1`, port `1080`.
- Save → buka bitget/x → LANCAR.
- (Alternatif cuma browser: Edge/Chrome settings → proxy → sama.)

### Linux/Mac (terminal, gak perlu PuTTY)
```bash
ssh -N -D 1080 -i <key> root@<VPS_IP>   # jalanin di background, biarin hidup
```
Lalu set system/browser SOCKS ke 127.0.0.1:1080.

## PITFALLS (TERBUKTI DI SESSION)
- **Extension VPN gak cukup.** Extension cuma proxy traffic browser & gampang di-detek DPI ISP. App VPN (full enkripsi) lebih kuat tp tetep ke-detect kalau ISP whitelist tunnel. VPS SSH = satu-satunya yg pasti krna IP VPS udah di-allow harian.
- **Jangan muter2 config router.** Firewall Low + DNS 8.8.8.8 bisa bantu KALAU blokirnya di router, tp kalau timeout koneksi (bukan DNS fail) = ISP level → rugi waktu. Langsung ke VPS proxy.
- **Router ZTE ISP:** 5GHz sering di-lock/blokir ISP → speed oke tp situs tetep block. Gak usah pake 5GHz buat bypass. 2.4GHz + proxy.
- **Jendela SSH/PuTTY harus hidup.** Proxy mati kalau session tutup. Biarin minimized.
- **Login pake SSH KEY** (user pake `/c/Users/Asus/.ssh/id_ed25519`), gak pass — lebih aman & gak ke-lock.

## KAPAN TIDAK PERLU SKILL INI
- Cuma DNS error biasa (situx resolve tapi lemot) → cukup ganti DNS.
- User bisa pake hotspot data HP → langsung lancar (berarti murni wifi/ISP blokir, gak usah proxy).

## REFERENSI
- `references/putty-socks-recipe.md` — step PuTTY + Windows proxy verbatim (copy-paste utk user non-teknis).
- VPS user: `134.199.170.183` (RackNerd, key `/c/Users/Asus/.ssh/id_ed25519`, user `root`).
