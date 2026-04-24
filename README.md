
# Problem 2: High Distribution Costs (Channel Profitability)
# Section 1: Strategic Alignment

## Background & Pain Points
- ธุรกิจโรงแรมที่จำหน่ายห้องพักผ่านหลายช่องทาง OTA Booking.com, Expedia, Direct Website, GDS และ Walk-in เพื่อเพิ่มยอดการจองและเข้าถึงลูกค้าได้หลากหลายกลุ่ม
- อย่างไรก็ตาม โรงแรมกำลังเผชิญปัญหา High Distribution Costs เนื่องจากต้องจ่ายค่าคอมมิชชั่นในอัตราสูงให้กับช่องทาง OTA ซึ่งแม้ว่าจะสร้างยอดการจองได้มากแต่กลับมีต้นทุนสูง ส่งผลให้กำไรสุทธิลดลง
- นอกจากนี้ โครงสร้าง Channel Mix ที่พึ่งพา OTA สูง ประกอบกับต้นทุนด้าน Marketing ของ Direct Channel ที่ยังไม่มีประสิทธิภาพ ทำให้เกิด Revenue Leakage และลดความสามารถในการทำกำไรโดยรวมของธุรกิจ

## SMART Objectives
```
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
# Section 2: Analytical Design
## Hypothesis & Method
## Business Problem
โรงแรมมีต้นทุน (Distribution Cost) สูงจากการพึ่งพา OTA ซึ่งมีค่า Commission สูง แม้จะสร้างยอดการจองจำนวนมาก ขณะที่ Direct Channel แม้ไม่มี Commission แต่มีต้นทุนด้าน Marketing สูง 
ส่งผลให้ Net Revenue ลดลงและโครงสร้างกำไรไม่มีประสิทธิภาพ
## Business Goal
เพิ่ม Net Revenue โดยลดต้นทุนจาก Commission อย่างน้อย 10% ภายใน 6 เดือน 
## Key Metrics
```
ADR (Average Daily Rate) = Gross Room Revenue / Rooms Sold
OCC (Occupancy Rate) = (Rooms Sold / Total Rooms) × 100  
Net ADR = (Gross Revenue - Commission Cost) / Rooms Sold
Net RevPAR = (Gross Revenue - Commission Cost) / Total Rooms Available
Direct Revenue Share (%) = Direct Revenue / Total Revenue
```
```red
1 OTA Cost Impact
OTA Booking Share (%)  = (OTA Bookings / Total Bookings) × 100
OTA Revenue Share (%)  = (OTA Revenue / Total Revenue) × 100
Total Commission       = OTA Revenue × Commission Rate
Net OTA Revenue        = OTA Revenue - Total Commission
Effective OTA Cost (%) = (Total Commission / Total Revenue) × 100
```

```red
2 Direct Channel มีต้นทุนแฝงสูงจาก Marketing
Direct Revenue = Total Direct Revenue
Marketing Cost = Total Marketing Spend
Marketing Cost Rate (%) = (Marketing Cost / Direct Revenue) × 100
Net Direct Revenue      = Direct Revenue - Marketing Cost
Effective Direct Cost (%) = (Marketing Cost / Total Revenue) × 100
```
```red
3 โครงสร้างรายได้กระจุกในช่องทางที่มีต้นทุนสูง
OTA Revenue Share (%)    = (OTA Revenue / Total Revenue) × 100
Direct Revenue Share (%) = (Direct Revenue / Total Revenue) × 100
High-Cost Revenue Share (%) = OTA Revenue Share
Low-Cost Revenue Share (%)  = Direct Revenue Share
```
## Dimension
- Booking Status 
- Booking Channel (Agoda, Booking.com, Direct, Corporate)
- Room Type (Standard, Deluxe, Suite)
- Segment (Leisure, Business, Group)
- Platform (Google, FB, IG) 
## Hypotheses
1. การจองผ่านช่องทาง Direct Website แม้จะมีต้นทุนการตลาด แต่ให้ค่า Net ADR สูงกว่าการจองผ่าน OTA อย่างมีนัยสำคัญ
2. กลุ่มลูกค้า Leisure ที่จองห้องพักประเภทราคาแพง (Suite) มีแนวโน้มที่จะจองผ่าน OTA มากกว่าช่องทางอื่น ซึ่งทำให้โรงแรมเสีย Gross Revenue ส่วนใหญ่ไปกับค่า Commission
3. ต้นทุนการตลาด (Marketing Cost Rate) ของ Direct Website บนบาง Platform (เช่น Google Ads) ต่ำกว่าอัตราค่าคอมมิชชั่นเฉลี่ยของ OTA ในช่วงเวลาที่มี Demand สูง
## Analytical Approach
- ทำ A/B Testing Grouping ระหว่างกลุ่ม OTA กับ Direct เพื่อดูส่วนต่าง
- คำนวณ Opportunity Gain จาก Suite จาก OTA เป็น Direct
- ทำ Platform Efficiency Matrix เพื่อจัดเกรด Platform ที่ควร เพิ่มหรือลดงบ

