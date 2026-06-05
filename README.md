# bk-data — Snapshot ข้อมูลฐานกลางโรงเรียนชุมชนวัดบางโค

ไฟล์ `data.json` คือ snapshot ข้อมูลอ้างอิง (ห้องเรียน / ครู / นักเรียนแยกห้อง) ปีการศึกษา 2569
ดึงอัตโนมัติจากระบบฐานข้อมูล bk2 (Google Apps Script) ทุก ~15 นาที โดย GitHub Actions
แล้วเสิร์ฟผ่าน GitHub Pages (CDN) เพื่อให้เว็บแอปโหลด "ข้อมูลอ่าน" ได้เร็วระดับ ~100ms

## URL ใช้งาน
```
https://krubk12-collab.github.io/bk-data/data.json
```

## โครงสร้าง data.json
```jsonc
{
  "ok": true,
  "version": "2026-06-05T13:34:14.605Z",   // เวลาที่ snapshot ถูกสร้าง
  "academic_year": 2569,
  "classes":   [{ "class_id", "class_name", "level", "education_level" }],
  "teachers":  [{ "teacher_id", "name" }],
  "studentsByClass": {
    "C17": [{ "student_id", "student_number", "prefix", "first_name", "last_name", "full_name", "nickname", "gender" }]
  }
}
```

## หมายเหตุ
- **ข้อมูลกรอกที่ Google Sheets เหมือนเดิม** — ที่นี่เป็นแค่สำเนาอ่านเร็ว
- ข้อมูลอาจช้ากว่าของจริงสูงสุด ~15 นาที (ตามรอบ Actions) — ส่วนการเช็คชื่อสด ๆ เว็บยังยิงผ่าน GAS ตรง
- อยากรีเฟรชทันที: แท็บ **Actions → Refresh snapshot → Run workflow**
- ⚠️ ถ้า repo เงียบเกิน 60 วัน GitHub จะปิด schedule อัตโนมัติ — เปิดใหม่ได้ที่แท็บ Actions
