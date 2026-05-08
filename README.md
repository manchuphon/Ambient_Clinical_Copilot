# Demo Script — Thai Clinical Copilot (3 minutes)

## Setup ก่อน demo
- [ ] เปิด browser ไว้ที่ localhost:3000 หรือ Vercel URL
- [ ] audio files 3 ไฟล์อยู่ใน demo/audio/ พร้อมแล้ว
- [ ] screenshot backup ทุกหน้าอยู่ใน demo/screenshots/
- [ ] ถ้า API fail → ใช้ fallback response (built-in อัตโนมัติ)

---

## Scene 1: Dialect Test (60 วินาที)
**ไฟล์:** `demo/audio/scene1-dialect.mp3`

**สคริปต์เสียง:**
> "Doctor: วันนี้มาด้วยอาการอะไรครับ
> Patient: เจ็บแอวมาหลายวันแล้วหมอ ยกของหนักไม่ได้เลย
> Doctor: ปวดร้าวลงขาไหมครับ
> Patient: ไม่ร้าวหมอ แค่ปวดตรงเอวครับ
> Doctor: เดี๋ยวให้ para PRN แล้วนัด X-ray ด้วยนะครับ"

**Expected output:**
- Subjective: Lower back pain, several days, unable to lift
- ICD-10: M54.5 — 94% (สีเขียว)
- NHSO: ✓ อยู่ในสิทธิบัตรทอง
- Plan: Paracetamol PRN (dose: [NOT SPECIFIED])

**Talking point:**
> "ระบบเข้าใจ 'เจ็บแอว' ภาษาอีสานว่าคือ lower back pain
> และ map ไปที่ ICD-10 M54.5 ได้อัตโนมัติ
> โดยไม่ต้องให้แพทย์พิมพ์รหัสเอง"

---

## Scene 2: Responsible AI (60 วินาที)
**ไฟล์:** `demo/audio/scene2-safety.mp3`

**สคริปต์เสียง:**
> "Doctor: เดี๋ยวให้ยาพาราไปกินนะ รับประทานเมื่อมีอาการปวด"

**Expected output:**
- Plan: Paracetamol prescribed PRN
- Dose: **[NOT SPECIFIED]** (สีแดง)

**Talking point:**
> "นี่คือ Responsible AI
> ระบบรู้ว่าขนาดยามาตรฐานคือ 500mg
> แต่ไม่เดา เพราะคนไข้เด็กหรือโรคไตต้องการขนาดต่างกัน
> กรรมการ OpenAI จะชอบ moment นี้มาก"

---

## Scene 3: Code-switching (60 วินาที)
**ไฟล์:** `demo/audio/scene3-codeswitching.mp3`

**สคริปต์เสียง:**
> "Doctor: ผล X-ray ออกมาแล้ว มี herniated disc ที่ L4-L5
> เดี๋ยว refer ไป ortho นะครับ แล้วให้ NSAIDs ไปด้วย"

**Expected output:**
- Assessment: Herniated intervertebral disc L4-L5 [NEEDS REVIEW]
- ICD-10: M51.1 — 91%
- Plan: Referral to orthopedics, NSAIDs prescribed (dose: [NOT SPECIFIED])

**Talking point:**
> "หมอพูดภาษาผสม ทั้ง 'herniated disc' และ 'refer ortho'
> ระบบเข้าใจทั้งหมด และสร้าง SOAP Note มาตรฐานได้ทันที"

---

