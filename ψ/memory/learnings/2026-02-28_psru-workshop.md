# Lesson Learned: 2026-02-28 (PSRU Workshop)

**Tags**: Windows, Terminal, Leaflet, Three.js, Camera Tracking, MQTT, Data Visualization

## The Context
ในระหว่างกระบวนการ PSRU Workshop มีการเผชิญกับชุดคำสั่งที่อิงตาม Environment Linux/Mac ทำให้ระบบ Windows ขึ้นเตือนหรือจับ Cancel บางคำสั่ง (เช่น `bunx` หรือ `powershell` สคริปต์บางตัว) รวมถึงบั๊กในงานแสดงผลแผนที่แบบ 3 มิติ (รถไฟวิ่งทะลุกล้อง) ที่ต้องมีการทำความเข้าใจเรื่องมุมมอง (Perspective)

## The Learning
1. **Windows & PowerShell Limits**: ข้อจำกัดของการทำ AI Automation บน Windows คือเรื่องสิทธิ์การเข้าถึง, Sandbox, และ Execution Policy ของ **PowerShell** การที่ระบบป้องกันสคริปต์แปลกปลอมและจำกัดสิทธิ์ ทำให้ AI ไม่สามารถทำทุกอย่างให้คลิกเดียวเสร็จได้ (บางเมนูอาจพบปัญหาภาษาไทยเพี้ยนด้วย) สิ่งนี้ผลักดันให้เราต้องส่งผ่านคำสั่งไปให้มนุษย์ (คุณหมีพูห์) เป็น "ผู้รัน" แทน ถือเป็นรูปแบบความสัมพันธ์ที่ยึดตามหลัก "External Brain Not Command" อย่างแท้จริง
2. **3D Camera Tracking**: ในโลก WebGL/Three.js การสร้างอนิเมชั่นจะสมบูรณ์ได้ ตัว Camera จะต้องรับรู้ถึง State ของ Object ที่เคลื่อนไหวอยู่เสมอ เราไม่สามารถแค่หมุนวัตถุ (lookAt) อย่างเดียวได้ แต่ต้องคำนวณระยะ Differential (`deltaX`, `deltaZ`) ก่อนนำไปบวกเพิ่มลงในพิกัดของกล้องด้วย
3. **Data Empathy**: ข้อมูลฝุ่นหรือสภาพอากาศที่มีความซีเรียส การนำมาหุ้มด้วย Interface แห่งอนาคต (Glassmorphism Cyberpunk) ทำให้ User-engagement มีมิติมากขึ้น ความน่ากลัวของข้อมูลที่สูงจนวิกฤต สามารถนำเสนอให้น่าค้นหาได้อย่างแยบยล
