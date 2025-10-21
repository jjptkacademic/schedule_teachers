# Teacher Mark Files

ไฟล์สำหรับเพิ่มวิชานอกกฎสำหรับครู (เช่น งานพิเศษ ประชุม วิชาเสริม)

## 🎯 Client-Side Processing

**Teacher marks ทำงานฝั่ง browser!**
- ✅ แก้ไขไฟล์ `.md` แล้วรีเฟรชหน้า browser ได้เลย
- ✅ ไม่ต้องรัน Python ใหม่
- ✅ Deploy แค่คัดลอก `teacher-mark/` folder ไปพร้อม HTML

## รูปแบบไฟล์

- ชื่อไฟล์: `T{teacher_id}-mark.md` (เช่น `T1-mark.md`, `T15-mark.md`)
- ตารางเดียวต่อครู ไม่ต้องมี header ชั้นเรียน
- ไฟล์ต้องอยู่ใน `teacher-mark/` folder เดียวกับ `output/`

## ตัวอย่างการใช้งาน

```markdown
# ตาราง Teacher Mark สำหรับครู ID 1

| วัน\คาบ | P1 | P2 | P3 | P4 | P6 | P7 | P8 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| จันทร์ |  |  |  |  |  |  | SP01 , งานพิเศษ , ม.1/1 |
| อังคาร |  |  |  |  |  |  |  |
| พุธ |  |  |  |  |  |  |  |
| พฤหัส |  |  |  |  |  |  |  |
| ศุกร์ | SP02 , ชุมนุม , ม.2/1 |  |  |  |  |  |  |
```

## รูปแบบข้อมูลในช่อง

`subject_code , subject_name , class_name`

ตัวอย่าง: `SP01 , งานพิเศษ , ม.1/1`

## คุณสมบัติพิเศษ

1. **Client-Side Loading**: โหลดและแสดงผลใน browser ด้วย JavaScript
2. **อนุญาตให้มีผู้สอนซ้ำ**: ครูหลายคนสอนวิชาเดียวกันในเวลาเดียวกันได้
3. **เช็คการชนอัตโนมัติ**: JavaScript ตรวจสอบว่า mark ชนกับตารางระบบหรือไม่
4. **คำนวณชั่วโมงทันที**: แสดง `X ชั่วโมง (ระบบ) + Y ชั่วโมง (Manual) = Z ชั่วโมง (รวม)`
5. **แสดงในช่องสีเหลือง**: ช่อง manual เป็นสีเหลืองพาสเทลพร้อมขอบทอง
6. **เตือนการชน**: แสดง warning box สีส้มถ้า mark ซ้อนกับตารางจริง

## วิธีใช้งาน

1. แก้ไขไฟล์ `T{teacher_id}-mark.md` ที่ต้องการ
2. บันทึกไฟล์
3. เปิด `output/schedule_teachers.html` ใน browser
4. รีเฟรชหน้า (F5) เพื่อดูการเปลี่ยนแปลง

## การ Deploy

```
your-server/
├── output/
│   ├── schedule.html
│   └── schedule_teachers.html
└── teacher-mark/
    ├── T1-mark.md
    ├── T2-mark.md
    └── ...
```

**หมายเหตุ:** ต้องเปิดผ่าน web server (เช่น Apache, Nginx, Python HTTP server) เพื่อให้ fetch API ทำงานได้

## ข้อจำกัด

- ต้องใช้ web server (ไม่รองรับ `file://` protocol)
- Browser ต้องรองรับ `async/await` และ `fetch API`
- ช่องว่าง = ไม่มีการเพิ่มวิชา
- ถ้า mark ชนกับตารางจริง จะแสดงเตือน แต่ไม่บล็อก
