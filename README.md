
# Problem 2: High Distribution Costs (Channel Profitability)
## Section 1: Strategic Alignment

### Background & Pain Points
- ธุรกิจโรงแรมที่จำหน่ายห้องพักผ่านหลายช่องทาง OTA Booking.com, Expedia, Direct Website, GDS และ Walk-in เพื่อเพิ่มยอดการจองและเข้าถึงลูกค้าได้หลากหลายกลุ่ม
- อย่างไรก็ตาม โรงแรมกำลังเผชิญปัญหา High Distribution Costs เนื่องจากต้องจ่ายค่าคอมมิชชั่นในอัตราสูงให้กับช่องทาง OTA ซึ่งแม้ว่าจะสร้างยอดการจองได้มากแต่กลับมีต้นทุนสูง ส่งผลให้กำไรสุทธิลดลง
- นอกจากนี้ โครงสร้าง Channel Mix ที่พึ่งพา OTA สูง ประกอบกับต้นทุนด้าน Marketing ของ Direct Channel ที่ยังไม่มีประสิทธิภาพ ทำให้เกิด Revenue Leakage และลดความสามารถในการทำกำไรโดยรวมของธุรกิจ

### SMART Objectives
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
## Section 2: Analytical Design
### Hypothesis & Method
### Business Problem
โรงแรมมีต้นทุน (Distribution Cost) สูงจากการพึ่งพา OTA ซึ่งมีค่า Commission สูง แม้จะสร้างยอดการจองจำนวนมาก ขณะที่ Direct Channel แม้ไม่มี Commission แต่มีต้นทุนด้าน Marketing สูง 
ส่งผลให้ Net Revenue ลดลงและโครงสร้างกำไรไม่มีประสิทธิภาพ
## Business Goal
เพิ่ม Net Revenue โดยลดต้นทุนจาก Commission อย่างน้อย 10% ภายใน 6 เดือน 
### Key Metrics
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
### Dimension
- Booking Status 
- Booking Channel (Agoda, Booking.com, Direct, Corporate)
- Room Type (Standard, Deluxe, Suite)
- Segment (Leisure, Business, Group)
- Platform (Google, FB, IG) 
### Hypotheses
1. การจองผ่านช่องทาง Direct Website แม้จะมีต้นทุนการตลาด แต่ให้ค่า Net ADR สูงกว่าการจองผ่าน OTA อย่างมีนัยสำคัญ
2. กลุ่มลูกค้า Leisure ที่จองห้องพักประเภทราคาแพง (Suite) มีแนวโน้มที่จะจองผ่าน OTA มากกว่าช่องทางอื่น ซึ่งทำให้โรงแรมเสีย Gross Revenue ส่วนใหญ่ไปกับค่า Commission
3. ต้นทุนการตลาด (Marketing Cost Rate) ของ Direct Website บนบาง Platform (เช่น Google Ads) ต่ำกว่าอัตราค่าคอมมิชชั่นเฉลี่ยของ OTA ในช่วงเวลาที่มี Demand สูง
### Analytical
- ทำ A/B Testing Grouping ระหว่างกลุ่ม OTA กับ Direct เพื่อดูส่วนต่าง
- คำนวณ Opportunity Gain จาก Suite จาก OTA เป็น Direct
- ทำ Platform Efficiency Matrix เพื่อจัดเกรด Platform ที่ควร เพิ่มหรือลดงบ

## Section 3: Data Execution & EDA 
### Data Schema & Relationships
ข้อมูลถูกจัดลำดับโดยมีตาราง fact_booking เป็นศูนย์กลางเชื่อมโยงกับตารางอื่นๆ ด้วยรหัส ID
- ตารางหลัก (Fact Tables): เก็บข้อมูลธุรกรรมจริง คือ fact_booking (1000 rows) และ fact_marketing_spend (100 rows)
- ตารางรายละเอียด (Dimension Tables): ให้ข้อมูลขยายความ ได้แก่ dim_channels (ช่องทาง), dim_rate_codes (ประเภทราคา), dim_room_types (ประเภทห้องพัก), และ dim_segments (กลุ่มลูกค้า)

### Data Dictionary: Hotel Booking & Marketing Dataset
ในการสร้างชุดข้อมูลนี้ ได้มีการใช้ Prompt 
```
สร้างฐานข้อมูลจำลองสำหรับโรงแรม เพื่อวิเคราะห์ Channel Profitability ประกอบด้วยตาราง fact_bookings 1000 แถว ที่มีข้อมูลการเงิน (Gross Revenue, Commission, Net Revenue), ตาราง dim_channels ที่ระบุรูปแบบค่าคอมมิชชั่น (Percentage, Flat Fee, Net Rate), ตาราง dim_rate_codes ที่จำแนกประเภทราคา และตาราง fact_marketing_spend เพื่อคำนวณต้นทุนการตลาดของช่องทาง Direct โดยข้อมูลต้องมีความสัมพันธ์กันอย่างถูกต้องเพื่อใช้วิเคราะห์ ADR, Occupancy และ COA%
```


### 1. Table: fact_booking
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

### 2. Table: fact_marketing_spend
ตารางที่เก็บข้อมูลค่าใช้จ่ายและประสิทธิภาพของแคมเปญการตลาด

| Column | Data Type | Description | Example |
| :--- | :--- | :--- | :--- |
| **spend_id** | Nominal (String) | รหัสอ้างอิงรายการค่าใช้จ่ายการตลาด | SP-0001, SP-0002, SP-0003 |
| **spend_date** | Interval (Date) | วันที่เกิดรายการค่าใช้จ่ายโฆษณา | 2025-01-09, 2025-02-18, 2025-02-01 |
| **channel_id** | Nominal (String) | รหัสช่องทางที่เกี่ยวข้อง | CH04 |
| **platform** | Nominal (String) | แพลตฟอร์มที่ใช้ลงโฆษณาออนไลน์ | Facebook, Instagram, Google Ads |
| **cost_amount** | Ratio (Numeric) | จำนวนเงินงบประมาณที่ใช้ไปจริง | 967, 361, 583 |
| **clicks** | Ratio (Numeric) | จำนวนคลิกที่ได้รับจากการโฆษณา | 460, 110, 383 |

### 3. Dimension Tables
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

# Hotel Data Analysis - EDA Report (Actual Data Stats)

โครงการวิเคราะห์และทำความสะอาดข้อมูลการจองโรงแรม (Hotel Booking Data) เพื่อเตรียมความพร้อมสำหรับการวิเคราะห์ KPI และพฤติกรรมลูกค้า

## 1. Data Overview
* **Rows (จำนวนแถว):** 1,000
* **Columns (จำนวนคอลัมน์):** 26

## 2. Data Quality Check & Cleaning Process

| #  | Step                        | Description                                                                                                                                                         | Column Stats                                                                          |
| -- | --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| 1  | Changed Data Types          | ปรับชนิดข้อมูลของแต่ละคอลัมน์ให้เหมาะสม เช่น วันที่เป็น Date format, รายได้/ต้นทุนเป็น Number และ Channel / Status เป็น Text เพื่อให้คำนวณต้นทุนและรายงานได้ถูกต้อง | **gross_room_revenue** Mean = 498.00 | Max = 1500.00 | Min = 100.00 | Median = 400.00 |
| 2  | Removed guest_id            | ลบคอลัมน์ `guest_id` ออกจากชุดข้อมูล เนื่องจากไม่เกี่ยวข้องกับการวิเคราะห์กำไรของช่องทางการขาย และช่วยลดข้อมูลส่วนเกิน                                              | **base_price** Mean = 167.00 | Max = 250.00 | Min = 100.00 | Median = 150.00          |
| 3  | Validated Commission Values | ตรวจสอบค่าคอมมิชชั่นให้ไม่มีค่าติดลบ และตรงตามรูปแบบของแต่ละ Channel เช่น OTA มีค่า %, Direct อาจไม่มีค่าคอม                                                        | **commission_amount** Mean = 30.05 | Max = 300.00 | Min = 0.00 | Median = 0.00        |
| 4  | Checked Net Revenue Logic   | ตรวจสอบสูตร `net_room_revenue = gross_room_revenue - commission_amount` เพื่อให้มั่นใจว่ารายได้สุทธิถูกต้อง                                                         | **net_room_revenue** Mean = 467.95 | Max = 1500.00 | Min = 80.00 | Median = 400.00    |
| 5  | Standardized Channel Names  | จัดรูปแบบชื่อช่องทางการขายให้เป็นมาตรฐาน เช่น Booking.com / Expedia / Direct Website เพื่อใช้ทำ Dashboard และ Group ได้ง่าย                                         | **default_commission_rate** Mean = 0.11 | Max = 0.20 | Min = 0.00 | Median = 0.17     |
| 6  | Created LOS Metric          | สร้างคอลัมน์ `LOS_nights` จาก Check-out Date - Check-in Date เพื่อดูพฤติกรรมการเข้าพักและกำไรต่อ Booking                                                            | **LOS_nights** Mean = 2.01 | Max = 3.00 | Min = 1.00 | Median = 2.00                  |
| 7  | Created Lead Time           | สร้างคอลัมน์ `BLT_days` จาก Check-in Date - Booking Date เพื่อวิเคราะห์ว่าช่องทางไหนจองล่วงหน้านานหรือใกล้วันเข้าพัก                                                | **BLT_days** Mean = 15.92 | Max = 30.00 | Min = 1.00 | Median = 16.00                 |
| 8  | Cleaned Text Columns        | ลบช่องว่างเกิน / ตัวอักษรพิเศษ / ค่าไม่สม่ำเสมอใน Channel Name, Rate Name, Segment Name เพื่อป้องกันการรวมกลุ่มผิดพลาด                                              | **number_of_rooms** Mean = 1.50 | Max = 2.00 | Min = 1.00 | Median = 2.00             |
| 9  | Feature Engineering         | เพิ่มตัวแปรช่วยวิเคราะห์ เช่น `is_ota`, `is_direct`, `is_commissionable`, `high_cost_channel` เพื่อใช้เปรียบเทียบกำไรแต่ละ Channel                                  | **adults_count** Mean = 1.51 | Max = 2.00 | Min = 1.00 | Median = 2.00                |
| 10 | KPI Calculation             | สร้าง KPI สำคัญ เช่น `ADR`, `Net ADR`, `COA %`, `Commission %`, `Net Revenue per Booking` เพื่อวัดประสิทธิภาพช่องทางขาย                                             | **children_count** Mean = 1.01 | Max = 2.00 | Min = 0.00 | Median = 1.00              |
| 11 | Channel Profitability Prep  | เตรียมข้อมูลเพื่อวิเคราะห์ว่า Channel ไหนสร้างยอดขายสูงแต่กำไรต่ำ และ Channel ไหนยอดขายน้อยแต่กำไรดี                                                                | **channel_type** = OTA / Direct / Offline                                             |

## 3. Key Metrics & KPIs Summary

* **Gross Room Revenue:** รายได้ก่อนหักค่าธรรมเนียม มีค่าเฉลี่ยอยู่ที่ 498.00 ต่อรายการ
* **Net Room Revenue:** รายได้หลังหักคอมมิชชั่น มีค่าเฉลี่ยอยู่ที่ 467.95
* **Commission Cost:** ค่าคอมมิชชั่นเฉลี่ยอยู่ที่ 30.05 ต่อการจอง (โดยมีค่ามัธยฐานเป็น 0 หมายความว่าการจองจำนวนมากเป็นแบบ Direct หรือไม่มีค่าคอมมิชชั่น)
* **Occupancy Profile:** โดยเฉลี่ยมีจำนวนห้องพัก 1.5 ห้องต่อการจอง และผู้ใหญ่ 1.5 คนต่อการจอง

---


### Hypotheses1: จองผ่าน Direct แม้จะมีต้นทุนแต่ให้ค่า Net ADR สูงกว่าการจองผ่าน OTA อย่างมีนัยสำคัญ
Stacked Bar Chart แสดงความแตกต่างระหว่าง Gross ADR และ Net ADR แยกตามช่องทางการขาย (Channel Name)
- เปรียบเทียบสัดส่วน: แสดงให้เห็นส่วนต่างระหว่างราคาขายหน้าร้าน (Gross) กับรายได้จริงที่โรงแรมได้รับหลังจากหักค่าคอมมิชชันและค่าใช้จ่ายอื่นๆ (Net)

- จุดสังเกต: แม้ช่องทางอย่าง Expedia หรือ Direct Website จะมี Gross ADR สูงที่สุด แต่เมื่อดูที่ Net ADR จะเห็นว่า Direct Website ให้รายได้สุทธิต่อห้องสูงที่สุดอย่างชัดเจน ในขณะที่ช่องทาง OTA อื่นๆ มีส่วนต่างที่กว้างกว่า ซึ่งหมายถึงต้นทุนการขายที่สูงกว่านั่นเอง

เหตุผลที่เลือก: Stacked Bar เหมาะสำหรับการแสดงค่ารวม (Gross) พร้อมกับสัดส่วนภายใน (Net) ทำให้เห็น ต้นทุนแฝง ของแต่ละช่องทางได้ทันทีในแท่งเดียว ช่วยให้ฝ่ายรายได้ตัดสินใจได้ว่าควรผลักดันการจองผ่านช่องทางไหนเพื่อให้ได้กำไรสูงสุด

<img src="./images/Net ADR Comparison_2.png" width="auto"/>

### Hypotheses2: กลุ่มลูกค้า Leisure จองเเต่ห้องเเพงสุดผ่านช่องทาง OTA เลยเสีย Commission มาก
Stacked Bar Chart แสดงสัดส่วน Commission Amount ของห้องพักประเภท Leisure Suite แยกตามช่องทางการขาย

- เปรียบเทียบการกระจายตัว: แสดงให้เห็นว่ายอดคอมมิชชันส่วนใหญ่มาจากช่องทางใดสำหรับห้องประเภท Suite

- จุดสังเกต: ยอดการจองที่ต้องจ่ายคอมมิชชันกระจุกตัวอยู่ที่ Expedia และ Agoda เป็นหลัก ในขณะที่ช่องทาง Direct และ Corporate แทบไม่มีสัดส่วนในกราฟนี้เลย สะท้อนว่าลูกค้ากลุ่ม High-end (ที่จอง Suite) ยังพึ่งพา OTA สูงมาก

เหตุผลที่เลือก: การใช้ Stacked Bar ในลักษณะแท่งเดียวแบบนี้ ช่วยเน้นย้ำเรื่อง Market Share ของยอดคอมมิชชันภายในกลุ่มสินค้าเดียว (Leisure Suite) ทำให้เห็นภาพรวมว่าเราเสียเงินค่าคอมมิชชันไปกับเจ้าไหนมากที่สุดเพื่อวางแผนดึงลูกค้ากลุ่มนี้มาจองตรงมากขึ้น

<img src="./images/Leisure Suite Bookings by Channel_3.png" width="auto"/> 

### Hypotheses3: ต้นทุนการตลาด (Marketing Cost Rate) ของ Direct Website บนบาง Platform ต่ำกว่าอัตราค่าคอมมิชชั่นเฉลี่ยของ OTA ในช่วงเวลาที่มี Demand สูง
กราฟ: Stacked Bar Chart แสดงสัดส่วน Commission Amount ของห้องพักประเภท Leisure Suite แยกตามช่องทางการขาย

- เปรียบเทียบการกระจายตัว: แสดงให้เห็นว่ายอดคอมมิชชันส่วนใหญ่มาจากช่องทางใดสำหรับห้องประเภท Suite

- จุดสังเกต: ยอดการจองที่ต้องจ่ายคอมมิชชันกระจุกตัวอยู่ที่ Expedia (สีเขียว) และ Agoda (สีน้ำเงิน) เป็นหลัก ในขณะที่ช่องทาง Direct และ Corporate แทบไม่มีสัดส่วนในกราฟนี้เลย สะท้อนว่าลูกค้ากลุ่ม High-end (ที่จอง Suite) ยังพึ่งพา OTA สูงมาก

เหตุผลที่เลือก: การใช้ Stacked Bar ในลักษณะแท่งเดียวแบบนี้ ช่วยเน้นย้ำเรื่อง "Market Share" ของยอดคอมมิชชันภายในกลุ่มสินค้าเดียว (Leisure Suite) ทำให้เห็นภาพรวมว่าเราเสียเงินค่าคอมมิชชันไปกับเจ้าไหนมากที่สุดเพื่อวางแผนดึงลูกค้ากลุ่มนี้มาจองตรงมากขึ้น

<img src="./images/Marketing Cost vs OTA Commission Benchmark_2.png" width="auto"/> 

## Section 4: Insights & Impact
### Findings (Insights)

### 1: ประสิทธิภาพของรายได้สุทธิ (Net ADR Comparison)
จากการเปรียบเทียบด้วย Stacked Bar Chart พบว่าช่องทาง Direct Website ให้ค่า Net ADR สูงที่สุด (ประมาณ 670) แม้ว่ายอดรายได้รวม (Gross) ของบาง OTA จะสูงกว่า แต่เมื่อหักค่าคอมมิชชั่นออก จะเห็น "Profit Gap" ที่กว้างมากในช่องทาง OTA ในขณะที่ช่องทาง Direct แทบไม่มีส่วนต่างนี้เลย

### 2: การพึ่งพาช่องทางในกลุ่มสินค้าพรีเมียม (Leisure Suite Analysis)
จากกราฟ Stacked Bar Chart พบว่ายอดเงินค่าคอมมิชชั่นในกลุ่มห้อง Suite ส่วนใหญ่กระจุกตัวอยู่ที่ Agoda และ Expedia โดยที่ช่องทาง Direct และ Corporate แทบไม่มีสัดส่วนในกลุ่มนี้เลย

### 3: ความคุ้มค่าของต้นทุนการตลาด (Marketing ROI vs. Benchmark)
จากการใช้ Bar Chart พร้อมเส้น Reference Line (18%) พบว่าค่า Marketing Cost % ของ Google Ads อยู่ต่ำกว่าเส้นมาตรฐาน 18% ของ OTA อย่างเห็นได้ชัด ในขณะที่บางแพลตฟอร์มอาจจะสูงกว่า

### Recommendations

### 1. กลยุทธ์ "Direct-First" เพื่อปิดช่องว่างกำไร (Closing the Profit Gap)
มุ่งเน้นการเปลี่ยนพฤติกรรมลูกค้าจาก จองผ่านตัวแทน เป็น จองตรง โดยใช้ส่วนต่างจากค่าคอมมิชชันมาสร้างความคุ้มค่า
มอบสิทธิประโยชน์พิเศษ (Exclusive Perks) สำหรับผู้ที่จองผ่าน Direct Website ซึ่งสิทธิประโยชน์เหล่านี้มีต้นทุนต่ำกว่าค่าคอมมิชชัน 18-20% ที่ต้องจ่ายให้ OTA

### 2. การรุกตลาดกลุ่ม High-end เพื่อดึงคืนห้อง Suite (Premium Inventory Control)
ลดการพึ่งพา OTA สำหรับห้องพักประเภท Suite และสร้างช่องทางเฉพาะสำหรับลูกค้ากลุ่ม Leisure ที่มีกำลังซื้อสูง
จัดทำแคมเปญ "Suite Secret Deal" โดยส่งรหัสส่วนลดพิเศษผ่าน Email Marketing หรือ Social Media ให้กับฐานลูกค้าเก่าเพื่อให้กลับมาจองตรง นอกจากนี้ควรปรับเงื่อนไขบน OTA ให้ห้อง Suite มีราคาสูงกว่าบนเว็บไซต์ของโรงแรม (Rate Parity Management) เพื่อจูงใจให้ลูกค้ากลุ่มนี้เปรียบเทียบราคาและหันมาจองตรงมากขึ้น

### 3. การจัดสรรงบประมาณโฆษณาตามประสิทธิภาพ (Data-Driven Budget Allocation)
เพิ่มสัดส่วนงบประมาณ (Re-allocate Budget) ไปยังแพลตฟอร์ม Google Ads ที่มีต้นทุนต่ำกว่า 18% อย่างชัดเจน โรงแรมควรเพิ่มงบประมาณในส่วนของ Google Search Ads โดยเน้น "Branded Keywords" (ชื่อโรงแรม) เพื่อดักจับลูกค้าที่รู้จักโรงแรมอยู่แล้วไม่ให้ไหลไปจองผ่าน OTA และควรพิจารณาลดงบประมาณในแพลตฟอร์มที่มี Marketing Cost % สูงกว่าค่าคอมมิชชันของ OTA เพื่อรักษาสมดุลของต้นทุน

## Other file
- data.xlsx: ไฟล์ข้อมูล Dataset ที่ผ่านการ Clean เรียบร้อยแล้ว สามารถนำไปใช้ในโปรแกรม Excel เพื่อทำ Pivot Table สรุปผลอย่างง่าย หรือนำไปเป็น Source ให้กับซอฟต์แวร์ Data Analysis อื่นๆ ได้ทันที

- Booking graph.twb: ไฟล์ Tableau Workbook ที่รวบรวม Dashboard ทั้งหมด คุณสามารถเปิดด้วย Tableau Desktop เพื่อดู Interactive Visualization เช่น การเจาะลึกข้อมูลการจองตามช่วงเวลา (Drill-down analysis) หรือการเปรียบเทียบปัจจัยต่างๆ แบบ Real-time

- images: โฟลเดอร์ที่รวบรวมภาพกราฟที่สำคัญ (Static Plots) เช่น Histogram, Heatmaps และหน้าตา Dashboard เบื้องต้น เพื่อให้ผู้เข้าชมเห็นภาพรวมของ Insight ได้ทันทีโดยไม่ต้องรันโค้ดเอง
