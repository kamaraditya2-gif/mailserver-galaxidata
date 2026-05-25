# Status Setup Mailserver Galaxidata

> Tanggal: 2026-05-20

## Tugas Selesai

- [x] Copy file config galaxidata ke direktori baru (`mailserver-galaxidata/config/`)
- [x] Buat `docker-compose.yml` untuk galaxidata
- [x] Buat `mailserver.env` untuk galaxidata
- [x] Buat config OpenDKIM untuk galaxidata
- [x] Bersihkan config daddys dari galaxidata existing
- [x] Update FRP config (`/opt/frp/frpc.toml`)
- [x] Restart frpc service (aktif & running)
- [x] Update nginx config public VPS (`172.232.228.53`)
- [x] Bersihkan config nginx duplikat di VPS

## Catatan Penting

### FRP Status
- `galaxi-webmail` → proxy success
- `daddys-smtp-submission`, `daddys-imap-ssl` → proxy success
- Beberapa port mail (IMAP, POP3S, SMTPS, IMAPS, submission) mengalami `port not allowed` — ini karena batasan FRP server di public VPS.

### Nginx Public VPS
- Config utama: `/etc/nginx/sites-available/default` (symlink ke enabled)
- Config duplikat (`daddysgsshop`, `mail`) sudah dihapus dari `sites-enabled`
- Nginx test: **OK**
- Nginx reload: **OK**

### SSL Certificates (VPS)
- `daddysgsshop.dpdns.org` ✅
- `mail.daddysgsshop.dpdns.org` ✅
- `galaxidata.com` / `mail.galaxidata.com` — belum ada cert (config HTTP only)

### Langkah Selanjutnya (Opsional)
1. Jalankan Docker Compose mailserver galaxidata:
   ```bash
   cd /home/webapp/projects/mailserver-galaxidata
   docker compose up -d
   ```
2. Setup SSL untuk `galaxidata.com` via certbot jika domain sudah pointing ke VPS.
3. Periksa apakah FRP server di public VPS perlu di-update untuk mengizinkan port mail tambahan.
