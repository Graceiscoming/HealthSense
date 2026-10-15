# HealthSense

**Predicting Chronic Disease Risk from Daily Lifestyle**

โปรเจกต์รายวิชา CP462 Introduction to Data Science — วิเคราะห์ข้อมูลและสร้างโมเดลทำนายความเสี่ยงโรคเบาหวานจากข้อมูลพื้นฐาน พฤติกรรม และค่าตรวจสุขภาพ เพื่อให้คนรู้ตัวก่อนป่วยจริง

## สมาชิก

- นายวัชรพงศ์ มาลัง (67102010174)
- นาย นราธิป สุวณิชย์ (67102010517)

## ที่มาและเป้าหมาย

โรคเรื้อรัง (เบาหวาน ความดันสูง โรคหัวใจ) เป็นสาเหตุการตายอันดับต้น ๆ และป้องกันได้จากพฤติกรรมการใช้ชีวิต โปรเจกต์นี้ต้องการตอบคำถามว่า *จะทำนายความเสี่ยงของการเป็นโรคเรื้อรังจากข้อมูลประจำวันได้อย่างไร*

ผู้ได้ประโยชน์: ประชาชนทั่วไป, หน่วยงานสาธารณสุข (คัดกรองกลุ่มเสี่ยง), บริษัทประกันสุขภาพ

## ชุดข้อมูล

[Diabetes Prediction Dataset](https://www.kaggle.com/datasets/iammustafatz/diabetes-prediction-dataset) (Kaggle) — 100,000 แถว, 8 features + 1 target (`diabetes`)

`gender`, `age`, `hypertension`, `heart_disease`, `smoking_history`, `bmi`, `HbA1c_level`, `blood_glucose_level`

ดาวน์โหลดอัตโนมัติผ่าน `kagglehub` ใน notebook (เป็น public dataset ไม่ต้องใช้ `kaggle.json`)

## โครงสร้างโปรเจกต์

```
HealthSense/
├── CP462_Project_HealthSense.ipynb   # Notebook หลัก (รันบน Google Colab)
├── HealthSense_Pitching.pdf          # สไลด์นำเสนอ
├── update_report/
│   ├── phase1/
│   │   ├── report.md                 # รายงานความคืบหน้า Phase 1
│   │   └── images/                   # กราฟที่ export จาก notebook
│   └── phase2/
│       ├── Checkpoint.md             # รายละเอียดโครงงาน (ปัญหา, ชุดข้อมูล, feature/target, task)
│       └── checkpoint.pdf
└── README.md
```

## วิธีรัน

1. เปิด notebook บน [Google Colab](https://colab.research.google.com/drive/12yncnUsZLkXPeEovgTwXNsovYEbw8tR1?usp=sharing) หรืออัปโหลด `CP462_Project_HealthSense.ipynb` ขึ้น Colab
2. รันทุก cell ตามลำดับ

> **หมายเหตุ:** cell ติดตั้งฟอนต์ไทยใช้ `apt-get` และ path ฟอนต์ของ Linux จึงรันได้เฉพาะบน Colab (หรือ Linux) ถ้ารันบนเครื่องอื่นต้องปรับหรือข้าม cell นั้น

Dependencies: `pandas`, `numpy`, `matplotlib`, `seaborn`, `kagglehub`

## ความคืบหน้า

| ขั้นตอน | สถานะ |
|---------|-------|
| Problem statement และคำอธิบาย dataset | ✅ เสร็จ |
| Data cleansing (100,000 → 96,146 แถว) | ✅ เสร็จ |
| Exploratory Data Analysis (6 กราฟ) | ✅ เสร็จ |
| Data pre-processing | ⬜ ยังไม่เริ่ม |
| สร้างและเปรียบเทียบโมเดล | ⬜ ยังไม่เริ่ม |
| ประเมินผล (recall, F1, AUC) และสรุป | ⬜ ยังไม่เริ่ม |

## ข้อค้นพบเบื้องต้นจาก EDA

- ข้อมูล **imbalanced** — ผู้ที่เป็นเบาหวานเป็นส่วนน้อยมาก ต้องจัดการตอนสร้างโมเดล
- `blood_glucose_level`, `HbA1c_level`, `age`, `bmi` สัมพันธ์กับ `diabetes` สูงสุด
- ผู้ที่เคยหรือกำลังสูบบุหรี่มีสัดส่วนเบาหวานสูงกว่ากลุ่มที่ไม่เคยสูบ และความเสี่ยงเพิ่มขึ้นตามอายุอย่างชัดเจน
- correlation เป็นความสัมพันธ์เชิงสถิติ ไม่ใช่ความสัมพันธ์เชิงเหตุและผล

รายละเอียดเพิ่มเติมดู [`update_report/phase1/report.md`](update_report/phase1/report.md)

## ขั้นต่อไป

1. Pre-processing: encode categorical, train/test split แบบ stratified
2. จัดการ class imbalance (class weight / SMOTE / undersampling)
3. เปรียบเทียบโมเดล เช่น Logistic Regression, Random Forest, XGBoost
4. ประเมินด้วย metric ที่เหมาะกับข้อมูลไม่สมดุล (recall, F1, AUC)
