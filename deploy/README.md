# THEOS-2 Interactive Simulation Kit & AIP Dashboard
### GISTDA Ground Station Sriracha — Educational Web Game

สื่อการเรียนรู้เชิงเกม จำลองกระบวนการทำงานของสถานีรับสัญญาณดาวเทียม THEOS-2 ศรีราชา
ตั้งแต่การรับสัญญาณ (Antenna Tracking) → การชดเชย Doppler → การถอดรหัสภาพและวิเคราะห์ NDVI

**Live demo:** _(ใส่ URL หลัง deploy บน Vercel)_

---

## โครงสร้างไฟล์

```
/
├── index.html      ← เกมทั้งหมด (HTML/CSS/JS แบบ single-file, ไม่มี build step)
├── vercel.json     ← config สำหรับ deploy บน Vercel (headers, clean URLs)
├── .gitignore
└── README.md
```

ไม่มี dependency, ไม่มี build step, ไม่มี backend — เป็น static site ล้วน รันได้ทันทีจากการเปิดไฟล์ `index.html` ในเบราว์เซอร์ หรือ deploy ขึ้น hosting ใดก็ได้ที่รองรับ static file

---

## ขั้นตอน Deploy

### 1. ตั้ง GitHub Repository

```bash
git init
git add .
git commit -m "Initial commit: THEOS-2 ground station simulation game"
git branch -M main
git remote add origin https://github.com/<your-username>/<repo-name>.git
git push -u origin main
```

### 2. Deploy บน Vercel

**วิธีที่ 1 — ผ่านเว็บ (แนะนำ):**
1. เข้า https://vercel.com/new
2. เลือก "Import Git Repository" แล้วเลือก repo ที่เพิ่ง push ไป
3. Framework Preset: เลือก **Other** (ไม่ต้องตั้งค่า Build Command / Output Directory — เป็น static HTML)
4. กด Deploy

**วิธีที่ 2 — ผ่าน Vercel CLI:**
```bash
npm i -g vercel
vercel login
vercel --prod
```

หลัง deploy สำเร็จ Vercel จะให้ URL รูปแบบ `https://<project-name>.vercel.app` — นำ URL นี้ไปสร้าง QR Code สำหรับแปะในเล่ม Proposal

### 3. สร้าง QR Code ชี้ไป URL ที่ deploy แล้ว

ใช้เครื่องมือ QR generator ใดก็ได้ (เช่น https://www.qr-code-generator.com หรือ `qrencode` บน CLI) ชี้ไปยัง URL จาก Vercel โดยตรง ไม่ต้องมี redirect ตัวกลาง เพื่อความเร็วในการโหลดวันนำเสนอ

```bash
# ตัวอย่างถ้ามี qrencode ในเครื่อง
qrencode -o qr-code.png "https://<project-name>.vercel.app"
```

---

## หมายเหตุด้านความเสถียรวันนำเสนอ

- เกมทำงานฝั่ง client ทั้งหมด (ดู Doppler/FSPL/SNR/NDVI คำนวณในเบราว์เซอร์) จึงเปิดเล่นได้แม้ไม่มีอินเทอร์เน็ตหลัง initial load — แนะนำเปิดหน้าเว็บทิ้งไว้ล่วงหน้าก่อนพรีเซนต์ 1 ครั้งเพื่อให้ browser cache ไฟล์ฟอนต์ (Google Fonts) และ asset ทั้งหมดไว้ก่อน
- หากสถานที่นำเสนอไม่มีอินเทอร์เน็ตแน่นอน ให้เปิดจากไฟล์ `index.html` โดยตรงในเครื่อง (double-click หรือ `open index.html`) เป็นแผนสำรอง — ฟอนต์ Google Fonts จะ fallback เป็น system font แทน แต่ gameplay ทำงานปกติทั้งหมด
