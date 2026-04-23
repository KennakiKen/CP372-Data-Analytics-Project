# Problem 2: High Distribution Costs (Channel Profitability)
## Background & Pain Points
- ธุรกิจโรงแรมที่จำหน่ายห้องพักผ่านหลายช่องทาง OTA Booking.com, Expedia, Direct Website, GDS และ Walk-in เพื่อเพิ่มยอดการจองและเข้าถึงลูกค้าได้หลากหลายกลุ่ม
- อย่างไรก็ตาม โรงแรมกำลังเผชิญปัญหา High Distribution Costs เนื่องจากต้องจ่ายค่าคอมมิชชั่นในอัตราสูงให้กับช่องทาง OTA ซึ่งแม้ว่าจะสร้างยอดการจองได้มากแต่กลับมีต้นทุนสูง ส่งผลให้กำไรสุทธิลดลง
### Pain Points
- Pain Point 1: พึ่งพา OTA สูง ทำให้ต้นทุนการขายสูงต่อเนื่อง
OTA มียอดจองรวม 573 ครั้ง (57.3%) และสร้างรายได้ 252,900 (54% ของทั้งหมด) แต่มีค่า Commission เฉลี่ย 11–13% ต่อการจอง ส่งผลให้ต้นทุนสะสมสูงและกำไรลดลง
```red
Pain Point 1 — OTA Cost Impact

OTA Booking Share (%)  = (OTA Bookings / Total Bookings) × 100
OTA Revenue Share (%)  = (OTA Revenue / Total Revenue) × 100

Total Commission       = OTA Revenue × Commission Rate

Net OTA Revenue        = OTA Revenue - Total Commission
Effective OTA Cost (%) = (Total Commission / Total Revenue) × 100
```

- Pain Point 2: Direct Channel มีต้นทุนแฝงสูงจาก Marketing
แม้ Direct จะไม่มี Commission แต่มี Marketing Cost สูงถึง 54,886 (47.5% ของรายได้ 115,400) ทำให้ต้นทุนรวมสูงกว่าที่คาด และลดความได้เปรียบด้านกำไร
```red
Direct Revenue = Total Direct Revenue
Marketing Cost = Total Marketing Spend

Marketing Cost Rate (%) = (Marketing Cost / Direct Revenue) × 100
Net Direct Revenue      = Direct Revenue - Marketing Cost

Effective Direct Cost (%) = (Marketing Cost / Total Revenue) × 100
```

- Pain Point 3: โครงสร้างรายได้กระจุกในช่องทางที่มีต้นทุนสูง
รายได้มากกว่า 54% มาจาก OTA ซึ่งเป็นช่องทางที่มีค่าใช้จ่าย (Commission) ขณะที่ Direct ซึ่งไม่มี Commission มีสัดส่วนเพียง 25% ของรายได้ ทำให้โครงสร้างรายได้ไม่เหมาะสมต่อการทำกำไร
```red
OTA Revenue Share (%)    = (OTA Revenue / Total Revenue) × 100
Direct Revenue Share (%) = (Direct Revenue / Total Revenue) × 100

High-Cost Revenue Share (%) = OTA Revenue Share
Low-Cost Revenue Share (%)  = Direct Revenue Share
```
- Pain Point 4: ห้องพรีเมียมถูกขายผ่านช่องทางที่มีต้นทุนสูง
RM03 มีทั้งหมด 340 ห้อง (34%) แต่ถูกขายผ่าน Direct เพียง 77 ห้อง (22%) และกระจายไป OTA จำนวนมาก ส่งผลให้รายได้จากห้องที่ควรทำกำไรสูงถูกหัก Commission อย่างต่อเนื่อง
```red
Premium Room Share (%) = (Premium Room Bookings / Total Bookings) × 100

Direct Premium Share (%) = (Direct Premium Bookings / Total Premium Bookings) × 100
OTA Premium Share (%)    = (OTA Premium Bookings / Total Premium Bookings) × 100

Premium Revenue Leakage (%) = OTA Premium Share × Commission Rate
```

### ผลกระทบทางธุรกิจ
- กำไรสุทธิลดลงอย่างมีนัยสำคัญ
เนื่องจากต้องจ่ายค่า Commission (OTA) และ Marketing Cost (Direct) ในสัดส่วนสูง ทำให้รายได้ที่ได้จริงลดลง
- ต้นทุนการหาลูกค้า (Customer Acquisition Cost) สูงเกินไป
ทั้ง OTA และ Direct มีต้นทุนสูง (Commission + Marketing) ส่งผลให้ได้ลูกค้าในราคาที่แพง
- โครงสร้างรายได้ไม่ยั่งยืน (Unsustainable Revenue Mix)
รายได้ส่วนใหญ่พึ่งพาช่องทางที่มีต้นทุนสูง ทำให้การเติบโตของรายได้ไม่แปลว่ากำไรเพิ่ม
## SMART Objectives
```c#
- S (Specific) 
ลดการพึ่งพา OTA และเพิ่มสัดส่วน Direct Booking 
โดยวิเคราะห์ Booking Channel, Rate Code และ Day Type 
เพื่อปรับ Pricing และ Channel Mix ให้ลด Commission และเพิ่มรายได้สุทธิ

- M (Measurable)
ลด OTA Booking Share จาก 57.3% เหลือไม่เกิน 45% 
และเพิ่ม Net ADR อย่างน้อย 10% 
โดยวัดจากการเปรียบเทียบ Net ADR ก่อนและหลังการปรับกลยุทธ์ 
รวมถึงติดตาม Commission Cost และ Cost of Acquisition (COA%) เป็นตัวชี้วัดสนับสนุน

- A (Achievable)
ใช้ข้อมูลการจองวิเคราะห์พฤติกรรมลูกค้า OTA และ Direct 
เพื่อระบุโอกาสในการ shift demand 
และปรับกลยุทธ์ เช่น การทำ Direct Promotion, Remarketing ไปยังลูกค้าเดิม, 
การปรับ Pricing ตามช่วงเวลาและ demand รวมถึงการปรับ Channel Mix 
เพื่อเพิ่มสัดส่วน Direct Booking และลดต้นทุนจาก Commission

- R (Relevant)
สอดคล้องกับเป้าหมายในการเพิ่ม Net Revenue 
โดยลดต้นทุนจาก Commission และปรับ Channel Mix 
เพื่อเพิ่มประสิทธิภาพในการทำกำไร

- T (Time-bound)
ดำเนินการวิเคราะห์และปรับกลยุทธ์ให้เห็นผลภายใน 6 เดือน 
```

