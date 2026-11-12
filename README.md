# ระบบลงทะเบียนนักศึกษา (Supabase + HTML)

เว็บลงทะเบียนแบบ static ไม่ต้องมี backend ใช้ Supabase เป็นฐานข้อมูล และ deploy ฟรีบน GitHub Pages

## ไฟล์ในโปรเจกต์ (มีแค่นี้ ไม่ต้องมีไฟล์อื่น)

```
├── index.html   # หน้าลงทะเบียน (สไตล์และค่าเชื่อมต่ออยู่ในไฟล์นี้แล้ว)
├── admin.html   # หน้าดูข้อมูลสำหรับ admin (สไตล์และค่าเชื่อมต่ออยู่ในไฟล์นี้แล้ว)
├── schema.sql   # คำสั่งสร้างตารางและสิทธิ์ใน Supabase
└── README.md
```

> ถ้าเคยอัปโหลด `style.css` และ `config.js` ไว้ ลบทิ้งได้ ไม่ได้ใช้แล้ว

## ฟีเจอร์
- **หน้าลงทะเบียน**: ชื่อ, นามสกุล, อายุ, แผนก, สาขา, เลขนักศึกษา, ระดับชั้น, คติประจำใจ พร้อมบัตรตัวอย่างที่เปลี่ยนตามที่พิมพ์
- **หน้า admin**: ล็อกอิน, สรุปจำนวน, ค้นหา, กรองตามระดับชั้น, ลบ, ดาวน์โหลด CSV (เปิดภาษาไทยใน Excel ได้), ใช้ได้บนมือถือ
- **ความปลอดภัย**: คนทั่วไปเพิ่มข้อมูลได้อย่างเดียว ดู/ลบได้เฉพาะ admin (Row Level Security)

## วิธีตั้งค่า

1. **Supabase**: สร้างโปรเจกต์ แล้วเปิด SQL Editor รันไฟล์ `schema.sql`
2. **ใส่ค่าเชื่อมต่อ**: เปิด `index.html` และ `admin.html` แก้ `SUPABASE_URL` และ `SUPABASE_ANON_KEY` ให้เป็นของโปรเจกต์คุณ (Project Settings → API) ใช้เฉพาะ anon / publishable key ห้ามใส่ `service_role`
3. **สร้าง admin**:
   - Authentication → Users → Add user (ติ๊ก Auto Confirm User)
   - เปิด `admin.html` ล็อกอิน จะมีคำสั่ง SQL แสดงให้คัดลอก นำไปรันใน SQL Editor แล้วรีเฟรช
4. **Deploy**: push ขึ้น GitHub → Settings → Pages → Branch `main` / root → Save
   - หน้าลงทะเบียน: `https://<username>.github.io/<repo>/`
   - หน้า admin: `https://<username>.github.io/<repo>/admin.html`

## ปรับแต่ง
- ตัวเลือกระดับชั้น: แก้ที่ `<select id="grade_level">` ใน `index.html`
- สีหลัก: แก้ตัวแปร `--cobalt` และ `--sun` ที่ต้น `<style>` ของทั้งสองไฟล์
