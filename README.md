# Sweet Draw

Sweet Draw is a powerful online drawing application built with React, TypeScript, and HTML5 Canvas, backed by a serverless Google Apps Script, Google Sheets (Database), and Google Drive (Storage) infrastructure.

## Features

- **Real Drawing Engine:** HTML5 Canvas-based toolset (Pencil, Brush, Eraser, etc.).
- **True Layer System:** Each layer runs on its own independent `<canvas>` element for true composition and ordering.
- **Serverless Backend:** Uses Google Apps Script as the API. No Supabase or Firebase required.
- **Database & Storage:** Google Sheets is used as the relational database, while Google Drive stores large JSON canvas states and exported images.

## Setup Instructions

Follow these exact steps to run the project.

### ขั้นตอนที่ 1: สร้าง Google Spreadsheet
1. ไปที่ Google Sheets และสร้าง Spreadsheet ใหม่ชื่อ `SweetDrawDB`
2. หรือใช้ Spreadsheet ของคุณเอง

### ขั้นตอนที่ 2: สร้าง Google Apps Script
1. ใน Google Sheets ไปที่เมนู `Extensions > Apps Script`
2. คัดลอกไฟล์ทั้งหมดจากโฟลเดอร์ `google-apps-script/` ไปยังโปรเจกต์ Apps Script:
   - `Code.gs`
   - `Database.gs`
   - `Drive.gs`
   - `Auth.gs`
   - `Utils.gs`

### ขั้นตอนที่ 3: ตั้งค่า Database
1. ใน Apps Script Editor เปิดไฟล์ `Database.gs`
2. เลือกฟังก์ชัน `setupDatabase` จากแถบเมนูด้านบน
3. กดปุ่ม `Run` (ให้สิทธิ์อนุญาตหากมีการร้องขอ)
4. รอจนทำงานเสร็จ คุณจะเห็นว่าชีตที่จำเป็นถูกสร้างใน Spreadsheet ของคุณ

### ขั้นตอนที่ 4: ตั้งค่า Drive
1. ใน Apps Script Editor เปิดไฟล์ `Drive.gs`
2. เลือกฟังก์ชัน `setupDrive` จากแถบเมนู
3. กดปุ่ม `Run`
4. สิ่งนี้จะสร้างโฟลเดอร์ `SweetDraw` และโฟลเดอร์ย่อยใน Google Drive ของคุณ

### ขั้นตอนที่ 5: Deploy เป็น Web App
1. กดปุ่ม `Deploy > New deployment` ที่มุมขวาบน
2. เลือก `Select type > Web app`
3. ตั้งค่า:
   - **Execute as:** Me (อีเมลของคุณ)
   - **Who has access:** Anyone
4. กด `Deploy`
5. คัดลอก **Web app URL** ที่ได้มา (เช่น `https://script.google.com/macros/s/XYZ/exec`)

### ขั้นตอนที่ 6: ตั้งค่า Environment Variables
1. ในโปรเจกต์ (Frontend) ให้ก็อปปี้ไฟล์ `.env.example` เป็น `.env.local`
2. นำ URL ที่ได้จากขั้นตอนที่ 5 มาใส่:
   ```
   VITE_GOOGLE_SCRIPT_URL=https://script.google.com/macros/s/XYZ/exec
   ```

### ขั้นตอนที่ 7: Install & Run
```bash
npm install
npm run dev
```

## หมายเหตุ / ข้อจำกัด
- **ส่วนที่ทำงานจริง:** Frontend React, Canvas Engine เบื้องต้น (Brush, Eraser), Backend API, ระบบฐานข้อมูลใน Google Sheets, และโฟลเดอร์ใน Google Drive.
- **ส่วนที่ยังต้องพัฒนาเพิ่ม:** UI ของหน้า Login, Gallery, Admin Dashboard, เครื่องมือวาดรูปขั้นสูง (Shapes, Text), และระบบ Export ไฟล์ภาพยังไม่ได้เชื่อมต่อสมบูรณ์ (เนื่องจากข้อจำกัดด้านเวลา).
- **การจัดเก็บรหัสผ่าน:** ใช้ SHA-256 Hashing ในฝั่ง Apps Script เพื่อไม่ให้รหัสผ่านถูกบันทึกเป็น Plain Text.

Enjoy drawing!
