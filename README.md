# Fantry — ระบบจองตั๋วแฟนมีตกันบอทผ่าน LINE Mini App

## FANTRY — “ตั๋วจริงใจ เพื่อแฟนตัวจริง" - "Fan + Entry — ระบบที่ให้แฟนได้เข้าอย่างแท้จริง"

### 🔧 แนวคิดหลัก:

> LINE Mini App สำหรับจองบัตร K-pop / Fan Meet ที่ใช้ระบบ **ลงทะเบียน + จองสิทธิแบบสุ่ม (raffle)** เพื่อกันบอท กัน reseller และเพิ่มความเท่าเทียมให้แฟนตัวจริง

### 🧩 ฟีเจอร์หลัก

| ฟีเจอร์                                  | รายละเอียด                                                      |
| ---------------------------------------- | --------------------------------------------------------------- |
| **1. ลงทะเบียนเข้าร่วมสิทธิซื้อบัตร**    | ผู้ใช้กด “เข้าร่วมสิทธิ” ก่อนเวลาจำหน่ายจริง (ล่วงหน้า 3-5 วัน) |
| **2. ยืนยันตัวตนผ่าน LINE / OTP**        | ยืนยันว่าเป็นคนจริง + กำหนดจำกัด 1 LINE ID ต่อ 1 สิทธิ์         |
| **3. ระบบสุ่มสิทธิซื้อ (Raffle)**        | จับฉลากแบบแฟร์ ใครได้สิทธิ์จะได้รับ “ตั๋วเสมือน”                |
| **4. แจ้งเตือนผู้ที่ได้สิทธิ์ผ่าน LINE** | ใช้ Service Message Template: `raffle` + `ticket`               |
| **5. ซื้อผ่าน LINE Pay**                 | ระบบเปิดลิงก์เฉพาะบุคคลภายในเวลาที่กำหนด                        |
| **6. ระบบ Anti-Resell**                  | บัตรผูกกับ LINE ID, ต้องแสดง QR Code ผ่าน Mini App วันเข้างาน   |
| **7. สะสม “แต้มแฟนคลับ”**                | ยิ่งลงทะเบียนบ่อย / แชร์ให้เพื่อน ยิ่งมีโอกาสได้สิทธิในอนาคต    |

### 🔔 ตัวอย่างการส่ง Service Message Template

#### 📩 Template: `raffle`

```json
{
  "type": "raffle",
  "title": "ลุ้นสิทธิ์ซื้อบัตร Fan Meet NCT 127",
  "status": "congratulations",
  "message": "คุณได้รับสิทธิ์ในการซื้อบัตร 🎉 รีบชำระเงินก่อนเวลา 18:00 น.",
  "button": {
    "label": "ชำระเงินผ่าน LINE Pay",
    "url": "https://lin.ee/payment-link-for-user"
  }
}
```

#### 🎫 Template: `ticket`

> ส่งหลังจ่ายเงินสำเร็จ

```json
{
  "type": "ticket",
  "title": "บัตร Fan Meet NCT 127",
  "seat": "Zone B, Seat 21",
  "barcode": "QR1234567890",
  "datetime": "2025-07-15 19:00",
  "location": "IMPACT Arena, เมืองทองธานี",
  "button": {
    "label": "ดูบัตรใน Mini App",
    "url": "https://line.me/ticket-details"
  }
}
```

### 💵 โมเดลรายได้

- ค่าธรรมเนียม 5–10% ต่อการขายบัตร
- บริการเสริมให้ผู้จัดงาน เช่น Dashboard วิเคราะห์แฟนคลับ
- โปรโมตผ่าน LINE OA, Broadcast, หรือ KOL

### 🚀 ข้อดีที่ “เหนือกว่า Web Ticket ปกติ”

- ไม่มี queue ล่ม เพราะใช้งานผ่าน LINE ที่รองรับ user scale ได้
- ป้องกัน bot ง่ายขึ้นด้วย LINE ID / OTP + random draw
- ไม่ต้องสมัครใหม่ เพราะใช้ LINE Login ที่ user ทุกคนมีอยู่แล้ว
- แจ้งเตือนอัตโนมัติ ชัดเจนตรงกล่องข้อความของผู้ใช้

---

### 🧩 **1. Concept & Product Summary**

> Fantry คือระบบจำหน่ายบัตรคอนเสิร์ตและแฟนมีต K-POP ผ่าน LINE Mini App ที่ใช้กลไก “สุ่มสิทธิ” + ยืนยันตัวตนจริง + จ่ายเงินผ่าน LINE Pay เพื่อ **ป้องกันการซื้อซ้ำโดยบอทหรือ reseller** ให้แฟนตัวจริงมีโอกาสซื้อตั๋วอย่างเท่าเทียม

## 💔 **2. Pain Point ในตลาดขายบัตรปัจจุบัน**

| ปัญหา                        | ผลกระทบ                              |
| ---------------------------- | ------------------------------------ |
| 🧠 **บอทกว้านซื้อบัตรทันที** | แฟนคลับซื้อตั๋วไม่ได้แม้กดตรงเวลา    |
| 💸 **รีเซลบัตรโก่งราคาสูง**  | บัตรราคา 2,000 ขายต่อ 8,000 บาท      |
| 🌀 **ระบบล่มช่วงเปิดขาย**    | เว็บไม่เสถียร แฟนคลับหมดศรัทธา       |
| 🔐 **ไม่มีระบบยืนยันตัวตน**  | คนเดียวซื้อบัตร 10 ใบ หลายอีเมล      |
| 😞 **แฟนคลับรู้สึกไม่แฟร์**  | ส่งผลต่อความรู้สึกกับศิลปินและแบรนด์ |

## 🚀 **3. แนวทางแก้ปัญหาโดย Fantry**

| กลไก                                      | ประโยชน์               |
| ----------------------------------------- | ---------------------- |
| ✅ **ลงทะเบียนล่วงหน้า**                  | ลดความแออัดตอนเปิดขาย  |
| 🎲 **สุ่มสิทธิแบบแฟร์ (Raffle)**          | กันบอทและ reseller ได้ |
| 🧍 **จำกัด 1 LINE ID : 1 สิทธิ**          | ลดการกว้านซื้อ         |
| 📲 **จ่ายผ่าน LINE Pay**                  | จ่ายง่าย ไม่โหลดหนัก   |
| 📬 **แจ้งเตือนผ่าน LINE Service Message** | ส่งตรง ไม่พลาดสิทธิ    |

## 📱 **4. Key UX Flow ของผู้ใช้งาน**

- ผู้ใช้เข้าร่วมจองสิทธิผ่าน LINE Mini App
- กดยืนยันตัวตน (LINE ID + OTP)
- รอระบบสุ่มผู้ได้รับสิทธิ
- ผู้ที่ได้รับสิทธิรับแจ้งผ่าน LINE (Template: `raffle`)
- ซื้อบัตรผ่าน LINE Pay ภายในเวลาที่กำหนด
- ได้รับบัตรพร้อม QR Code ผ่าน LINE (Template: `ticket`)

### 🧠 **5. จุดแข็งของ Fantry**

- **ไม่มีเว็บล่ม** เพราะใช้ LINE Platform ที่รองรับ traffic จำนวนมาก
- **UX สั้น ใช้งานผ่านมือถือไม่ต้องโหลดแอป**
- **แจ้งเตือนอัตโนมัติผ่าน LINE Message Template**
- **ผูกบัตรกับ LINE ID** ลดการขายต่อ
- **เชื่อมต่อ ecosystem LINE** ทั้ง OA, LINE Ads, LINE Pay

## 💼 **6. Business Model**

| รายได้                             | รายละเอียด                                           |
| ---------------------------------- | ---------------------------------------------------- |
| 💳 ค่าธรรมเนียมขายบัตร             | เช่น 10 บาท/ใบ หรือ 5% ของราคาบัตร                   |
| 📊 บริการแดชบอร์ดให้ค่ายจัดงาน     | วิเคราะห์กลุ่มแฟน, พฤติกรรมการซื้อ                   |
| 📣 ค่าพื้นที่โปรโมทใน Mini App     | สำหรับศิลปิน/ค่ายอื่นในอนาคต                         |
| 🏆 Fan Club Points & Premium Entry | เสนอ “Fast Lane” สำหรับผู้ใช้ที่มีแต้มสะสมจากกิจกรรม |

## 📈 **7. ขนาดตลาด (เฉพาะไทย)**

- ตลาดคอนเสิร์ตและ Event ปี 2024: **3,200 ล้านบาท**
- ตลาดบัตร K-POP / Fan Meet (เฉพาะไทย): **1,000+ ล้านบาทต่อปี**
- แฟนคลับกลุ่มอายุต่ำกว่า 30 ปี นิยมใช้ LINE > 90%
- LINE OA เป็นช่องทางหลักของศิลปินในไทยอยู่แล้ว

### 🎯 **8. Go-To-Market Strategy**

- ร่วมมือกับค่ายที่มีฐานแฟนไทย เช่น GMMTV, BeOnCloud, Bighit Thailand
- สร้างโปรแกรม “Pre-fan Verification” แบบพิเศษให้ค่าย whitelist แฟนคลับ
- ใช้ Influencer ฝั่ง K-POP / Tiktok / Twitter โปรโมทแคมเปญเปิดจอง
- ใช้ LINE Ads & Broadcast จาก OA สนับสนุนการเปิดขาย

### ✅ **9. ทำไม LINE Mini App คือแพลตฟอร์มที่เหมาะที่สุด**

- คนไทยใช้ LINE เป็น default messaging app ทุกวัย
- ไม่ต้องสมัครใหม่ ไม่ต้องดาวน์โหลด
- Service Message รองรับทุกกิจกรรม: จอง, จ่าย, ได้สิทธิ
- LINE Pay เชื่อมจบในตัว ทำให้บอทอัตโนมัติยากขึ้น
- เหมาะกับกิจกรรมไว จบเร็ว ไม่ต้องเข้าเว็บนอก

### Slide 1: Cover

Fantry "ตั๋วจริงใจ เพื่อแฟนตัวจริง"A fan-first ticketing platform that ensures fair access for real fans, not bots.

### Slide 2: Problem

- The Ticketing Crisis for K-pop & Fan Meet Events
- Bots and scalpers hoard tickets within seconds
- Fans are forced to pay 3x+ for resold tickets
- Web platforms often crash during high-demand sales
- No real identity verification: fans feel cheated

### Slide 3: Insight

"Real fans miss out, while resellers profit. The system feels rigged."

- Fans demand fairness and transparency
- Artists want loyal fans to get access
- The LINE ecosystem is already trusted and used daily in Thailand

### Slide 4: Solution

Fantry — Ticketing, Reimagined for Real Fans

- Raffle-based access: no more fastest-finger-first stress
- Identity verification via LINE ID & OTP
- Secure checkout via LINE Pay
- Transparent, anti-bot, anti-scalping
- Fan notifications directly through LINE Service Messages

### Slide 5: How It Works

1. Fans register for ticket raffle on LINE Mini App
2. Verification via LINE account & OTP
3. Winners are notified via LINE (raffle template)
4. Checkout securely via LINE Pay
5. Digital ticket delivered via LINE (ticket template)

### Slide 6: Why LINE Mini App

- 90%+ Thai users already on LINE
- No downloads or new logins required
- Fast UX, auto-login, and integrated notifications
- Built-in payment with LINE Pay
- Service Message templates perfectly suited for ticket flow

### Slide 7: Product Demo (Optional Visuals)

- Mini App home screen: event list
- Raffle registration UI
- LINE Service Message notification examples
- Ticket QR code and details view

### Slide 8: Business Model

- 5–10% ticketing fee per transaction
- Premium placement for organizers on event listings
- Optional fan loyalty system and upsells
- Custom analytics dashboard for organizers

### Slide 9: Market Opportunity

- Thai Live Event & Fan Meet Market
- มูลค่า Fan Meet/K-pop ในไทย > 1,000M THB/year
- K-pop fanbase is mobile-native and LINE-centric
- Frequent events = repeatable revenue

### Slide 10: Competitive Advantage

- LINE-native: fast, secure, familiar
- Raffle + identity check = real anti-bot system
- No app download friction
- Trusted brand = easier onboarding for organizers

### Slide 11: Call to Action

- Let’s Make Ticketing Fair Again.
- Seeking pilot event partners (labels, venues)
- LINE integration support ready
- Let’s put real fans back in real seats
