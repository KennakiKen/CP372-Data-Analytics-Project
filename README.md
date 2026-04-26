
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
## Analytical
- ทำ A/B Testing Grouping ระหว่างกลุ่ม OTA กับ Direct เพื่อดูส่วนต่าง
- คำนวณ Opportunity Gain จาก Suite จาก OTA เป็น Direct
- ทำ Platform Efficiency Matrix เพื่อจัดเกรด Platform ที่ควร เพิ่มหรือลดงบ

# Section 3: Data Execution & EDA
## Data Schema & Relationships
ข้อมูลถูกจัดลำดับโดยมีตาราง fact_booking เป็นศูนย์กลางเชื่อมโยงกับตารางอื่นๆ ด้วยรหัส ID
- ตารางหลัก (Fact Tables): เก็บข้อมูลธุรกรรมจริง คือ fact_booking (1000 rows) และ fact_marketing_spend (100 rows)
- ตารางรายละเอียด (Dimension Tables): ให้ข้อมูลขยายความ ได้แก่ dim_channels (ช่องทาง), dim_rate_codes (ประเภทราคา), dim_room_types (ประเภทห้องพัก), และ dim_segments (กลุ่มลูกค้า)

# Data Dictionary: Hotel Booking & Marketing Dataset
ในการสร้างชุดข้อมูลนี้ ได้มีการใช้ Prompt 
```
สร้างฐานข้อมูลจำลองสำหรับโรงแรม เพื่อวิเคราะห์ Channel Profitability ประกอบด้วยตาราง fact_bookings 1000 แถว ที่มีข้อมูลการเงิน (Gross Revenue, Commission, Net Revenue), ตาราง dim_channels ที่ระบุรูปแบบค่าคอมมิชชั่น (Percentage, Flat Fee, Net Rate), ตาราง dim_rate_codes ที่จำแนกประเภทราคา และตาราง fact_marketing_spend เพื่อคำนวณต้นทุนการตลาดของช่องทาง Direct โดยข้อมูลต้องมีความสัมพันธ์กันอย่างถูกต้องเพื่อใช้วิเคราะห์ ADR, Occupancy และ COA%
```


## 1. Table: fact_booking
ตารางหลักที่เก็บข้อมูลธุรกรรมการจองห้องพัก (Main Fact Table)

| Column | Data Type | Description | Example |
| :--- | :--- | :--- | :--- |
| **booking_id** | Nominal (String) | รหัสอ้างอิงการจองที่ไม่ซ้ำกัน (Primary Key) | RES-00001, RES-00002, RES-00003 |
| **guest_id** | Nominal (String) | รหัสอ้างอิงลูกค้า | G0001, G0002, G0003 |
| **booking_date** | Interval (Date) | วันที่ลูกค้าทำรายการจองห้องพัก | 2025-02-10, 2025-01-28, 2025-02-11 |
| **check_in_date** | Interval (Date) | วันที่ลูกค้ามีกำหนดเข้าพัก | 2025-02-14, 2025-01-30, 2025-03-06 |
| **check_out_date** | Interval (Date) | วันที่ลูกค้ามีกำหนดออกจากที่พัก | 2025-02-15, 2025-01-31, 2025-03-09 |
| **room_type_id** | Nominal (String) | รหัสประเภทห้องพัก | RM01, RM02, RM03 |
| **rate_code_id** | Nominal (String) | รหัสเรทราคา | RT01, RT02, RT03 |
| **channel_id** | Nominal (String) | รหัสช่องทางการจอง | CH01, CH02, CH03 |
| **segment_id** | Nominal (String) | รหัสกลุ่มลูกค้า | SG01, SG02, SG03 |
| **status** | Nominal (String) | สถานะการจอง | Checked-Out, Cancelled, No-Show |
| **gross_room_revenue** | Ratio (Numeric) | รายได้ค่าห้องรวมก่อนหักค่าคอมมิชชั่น | 100, 250, 450 |
| **commission_amount** | Ratio (Numeric) | จำนวนเงินค่าคอมมิชชั่นที่จ่ายให้ตัวแทน | 0.0, 20.0, 68.0 |
| **net_room_revenue** | Ratio (Numeric) | รายได้สุทธิที่โรงแรมได้รับจริง | 80.0, 250.0, 332.0 |
| **number_of_rooms** | Ratio (Numeric) | จำนวนห้องพักที่จอง | 1, 2 |
| **adults_count** | Ratio (Numeric) | จำนวนผู้ใหญ่ที่เข้าพัก | 1, 2 |
| **children_count** | Ratio (Numeric) | จำนวนเด็กที่เข้าพัก | 0, 1, 2 |

## 2. Table: fact_marketing_spend
ตารางที่เก็บข้อมูลค่าใช้จ่ายและประสิทธิภาพของแคมเปญการตลาด

| Column | Data Type | Description | Example |
| :--- | :--- | :--- | :--- |
| **spend_id** | Nominal (String) | รหัสอ้างอิงรายการค่าใช้จ่ายการตลาด | SP-0001, SP-0002, SP-0003 |
| **spend_date** | Interval (Date) | วันที่เกิดรายการค่าใช้จ่ายโฆษณา | 2025-01-09, 2025-02-18, 2025-02-01 |
| **channel_id** | Nominal (String) | รหัสช่องทางที่เกี่ยวข้อง | CH04 |
| **platform** | Nominal (String) | แพลตฟอร์มที่ใช้ลงโฆษณาออนไลน์ | Facebook, Instagram, Google Ads |
| **cost_amount** | Ratio (Numeric) | จำนวนเงินงบประมาณที่ใช้ไปจริง | 967, 361, 583 |
| **clicks** | Ratio (Numeric) | จำนวนคลิกที่ได้รับจากการโฆษณา | 460, 110, 383 |

## 3. Dimension Tables
ตารางสนับสนุนที่ใช้สำหรับจำแนกหมวดหมู่ข้อมูล (Contextual Data)

### dim_channels
| Column | Data Type | Description | Example |
| :--- | :--- | :--- | :--- |
| **channel_name** | Nominal (String) | ชื่อช่องทางการจอง | Booking.com, Expedia, Agoda, Direct Website |
| **channel_type** | Nominal (String) | หมวดหมู่ช่องทาง | OTA, Direct, Offline |

### dim_room_types
| Column | Data Type | Description | Example |
| :--- | :--- | :--- | :--- |
| **room_type_name** | Nominal (String) | ชื่อเรียกประเภทห้องพัก | Standard, Deluxe, Suite |
| **base_price** | Ratio (Numeric) | ราคาตั้งต้นของห้องพัก | 100, 150, 250 |

---

### Hypotheses1: จองผ่าน Direct แม้จะมีต้นทุนแต่ให้ค่า Net ADR สูงกว่าการจองผ่าน OTA อย่างมีนัยสำคัญ
Stacked Bar Chart แสดงความแตกต่างระหว่าง Gross ADR และ Net ADR แยกตามช่องทางการขาย (Channel Name)
- เปรียบเทียบสัดส่วน: แสดงให้เห็นส่วนต่างระหว่างราคาขายหน้าร้าน (Gross) กับรายได้จริงที่โรงแรมได้รับหลังจากหักค่าคอมมิชชันและค่าใช้จ่ายอื่นๆ (Net)

- จุดสังเกต: แม้ช่องทางอย่าง Expedia หรือ Direct Website จะมี Gross ADR สูงที่สุด แต่เมื่อดูที่ Net ADR (แถบสีส้ม) จะเห็นว่า Direct Website ให้รายได้สุทธิต่อห้องสูงที่สุดอย่างชัดเจน ในขณะที่ช่องทาง OTA อื่นๆ มีส่วนต่าง (Gap) ที่กว้างกว่า ซึ่งหมายถึงต้นทุนการขายที่สูงกว่านั่นเอง

เหตุผลที่เลือก: Stacked Bar เหมาะสำหรับการแสดงค่ารวม (Gross) พร้อมกับสัดส่วนภายใน (Net) ทำให้เห็น ต้นทุนแฝง ของแต่ละช่องทางได้ทันทีในแท่งเดียว ช่วยให้ฝ่ายรายได้ตัดสินใจได้ว่าควรผลักดันการจองผ่านช่องทางไหนเพื่อให้ได้กำไรสูงสุด

[<img width="946" height="820" alt="Net ADR Comparison" src="https://github.com/user-attachments/assets/79c59a99-64c6-4038-9309-f2e4e3ed0df3" />](https://github.com/KennakiKen/CP372-Data-Analytics-Project/blob/main/images/Net%20ADR%20Comparison.png)

### Hypotheses2: กลุ่มลูกค้า Leisure จองเเต่ห้องเเพงสุดผ่านช่องทาง OTA เลยเสีย Commission มาก
Stacked Bar Chart แสดงสัดส่วน Commission Amount ของห้องพักประเภท Leisure Suite แยกตามช่องทางการขาย

- เปรียบเทียบการกระจายตัว: แสดงให้เห็นว่ายอดคอมมิชชันส่วนใหญ่มาจากช่องทางใดสำหรับห้องประเภท Suite

- จุดสังเกต: ยอดการจองที่ต้องจ่ายคอมมิชชันกระจุกตัวอยู่ที่ Expedia (สีเขียว) และ Agoda (สีน้ำเงิน) เป็นหลัก ในขณะที่ช่องทาง Direct และ Corporate แทบไม่มีสัดส่วนในกราฟนี้เลย สะท้อนว่าลูกค้ากลุ่ม High-end (ที่จอง Suite) ยังพึ่งพา OTA สูงมาก

เหตุผลที่เลือก: การใช้ Stacked Bar ในลักษณะแท่งเดียวแบบนี้ ช่วยเน้นย้ำเรื่อง "Market Share" ของยอดคอมมิชชันภายในกลุ่มสินค้าเดียว (Leisure Suite) ทำให้เห็นภาพรวมว่าเราเสียเงินค่าคอมมิชชันไปกับเจ้าไหนมากที่สุดเพื่อวางแผนดึงลูกค้ากลุ่มนี้มาจองตรงมากขึ้น






