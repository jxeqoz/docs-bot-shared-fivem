# คู่มือการตั้งค่า config.json

คัดลอก `config.example.json` เป็น `config.json` แล้วแก้ไขค่าต่างๆ ตามที่ต้องการ

---

## 1. การตั้งค่า Bot

### token
Bot Token จาก Discord Developer Portal

### clientId
Bot Client ID

### guildId
Server ID (ไม่บังคับ)

### submitChannelId
Channel ID ที่จะแสดงปุ่มส่งลิงก์

### embedImageURL
URL รูปภาพที่จะแสดงใน embed (ไม่บังคับ)

### deleteMessageOnReview
ลบข้อความในช่อง admin หลังจากตรวจสอบแล้ว
- `true` = ลบ
- `false` = ไม่ลบ

### showReviewerInDM
แสดงชื่อผู้ตรวจสอบใน DM ที่ส่งให้ผู้ใช้
- `true` = แสดง
- `false` = ไม่แสดง

---

## 2. การตั้งค่า Database

### host
MySQL Host (ปกติใช้ `localhost`)

### port
MySQL Port (ปกติใช้ `3306`)

### username
MySQL Username

### password
MySQL Password

### database
ชื่อ Database

---

## 3. การตั้งค่า Link Categories

แต่ละกิจกรรมต้องมีการตั้งค่าดังนี้:

### id
รหัสกิจกรรม (ต้องไม่ซ้ำกัน)

### name
ชื่อกิจกรรมที่จะแสดง

### description
คำอธิบายกิจกรรม

### submissionChannelId
Channel ID ที่ admin จะตรวจสอบการส่ง

### maxLinks
จำนวนลิงก์สูงสุดที่ส่งได้ต่อครั้ง

### maxSubmissionsPerDay
จำนวนครั้งสูงสุดที่ส่งได้ต่อวัน

### cooldownHours
เวลาคูลดาวเป็นชั่วโมง

### cooldownMinutes
เวลาคูลดาวเป็นนาที

### oneSubmissionPerEvent
กำหนดว่าส่งได้ครั้งเดียวตลอดกิจกรรมหรือไม่
- `true` = ส่งได้ครั้งเดียว
- `false` = ส่งได้หลายครั้ง

### rewards
รางวัลที่จะได้รับ (เป็น array)
```json
[
  { "item": "diamond", "amount": 100 },
  { "item": "gacha_ticket", "amount": 5 }
]
```

---

## 4. การตั้งค่า Validation (ไม่บังคับ)

### enabled
เปิด/ปิดการตรวจสอบลิงก์
- `true` = เปิด
- `false` = ปิด

### autoApprove
อนุมัติอัตโนมัติถ้าผ่านการตรวจสอบ
- `true` = อนุมัติอัตโนมัติ
- `false` = ต้องให้ admin อนุมัติ

### platform
แพลตฟอร์มที่ต้องการตรวจสอบ
- `facebook`
- `tiktok`

### type
ประเภทของโพสต์

สำหรับ Facebook:
- `page_share` = แชร์โพสต์หน้าเพจ
- `page_post` = โพสต์หน้าเพจ
- `group_share` = แชร์ในกลุ่ม
- `group_post` = โพสต์ในกลุ่ม

สำหรับ TikTok:
- `tiktok_video` = วิดีโอ TikTok

### hashtags
Hashtag ที่ต้องมีในโพสต์ (เป็น array)
```json
["#SEACITY", "#seacity"]
```

### groupIds
Group ID ของ Facebook (ใช้เฉพาะ `group_share` และ `group_post`)
```json
["123456789", "987654321"]
```

---

## ตัวอย่าง config.json

```json
{
  "token": "YOUR_BOT_TOKEN_HERE",
  "clientId": "YOUR_CLIENT_ID_HERE",
  "guildId": "YOUR_GUILD_ID_HERE",
  "submitChannelId": "YOUR_SUBMIT_CHANNEL_ID_HERE",
  "embedImageURL": "https://example.com/image.jpg",
  "deleteMessageOnReview": false,
  "showReviewerInDM": false,
  "database": {
    "host": "localhost",
    "port": 3306,
    "username": "root",
    "password": "your_password",
    "database": "es_extendedz"
  },
  "linkCategories": [
    {
      "id": "facebook_post_1",
      "name": "Facebook แชร์โพสต์",
      "description": "ส่งลิงก์ Facebook แชร์โพสต์หน้าเฟส/โพสต์หน้าเฟส + ติด Hashtag",
      "submissionChannelId": "YOUR_ADMIN_CHANNEL_ID_HERE",
      "maxLinks": 1,
      "maxSubmissionsPerDay": 5,
      "cooldownHours": 4,
      "cooldownMinutes": 0,
      "oneSubmissionPerEvent": false,
      "rewards": [
        { "item": "diamond", "amount": 100 },
        { "item": "gacha_ticket", "amount": 5 }
      ],
      "validation": {
        "enabled": true,
        "autoApprove": false,
        "platform": "facebook",
        "type": "page_share",
        "hashtags": ["#SEACITY", "#seacity"]
      }
    }
  ]
}
```
