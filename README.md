# Final-Project: การวิเคราะห์และทำนายค่าพลังนักเตะในเกม EA SPORTS FC 26
### (Analysis and Prediction of Player Ratings in EA SPORTS FC 26)

> **รายวิชา:** 1145 201 คณิตศาสตร์สำหรับวิทยาการข้อมูล (Mathematics for Data Science)  
> **ภาคการศึกษา:** 1/2569

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python&logoColor=white)](https://www.python.org/)
[![Scikit-Learn](https://img.shields.io/badge/scikit--learn-F7931E?logo=scikit-learn&logoColor=white)](https://scikit-learn.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter&logoColor=white)](https://jupyter.org/)

---

## 📌 ภาพรวมโครงงาน (Project Overview & Problem Statement)

โครงงานนี้มีเป้าหมายเพื่อจำแนกและทำนายระดับค่าพลังนักเตะ (Overall Rating) ในเกม EA SPORTS FC 26 โดยอาศัยข้อมูลค่าพลังย่อย สไตล์การเล่น และข้อมูลทางกายภาพของนักเตะ โดยประยุกต์ใช้แนวคิดทางคณิตศาสตร์ สถิติ และวิทยาการข้อมูลอย่างเป็นระบบ ตั้งแต่การวิเคราะห์ข้อมูลด้วย **Linear Algebra (PCA)**, การทดสอบสมมติฐานทางสถิติ (**ANOVA & Chi-Square**), การวิเคราะห์ **Bias-Variance Trade-off** ตลอดจนการประเมินและคัดเลือกโมเดลด้วย **5-Fold Stratified Cross-Validation**

---

## 👥 สมาชิกในกลุ่มและหน้าที่รับผิดชอบ (Team Members & Roles)

| ลำดับ | รหัสนักศึกษา | ชื่อ - นามสกุล | หน้าที่หลักและส่วนงานที่รับผิดชอบ |
| :---: | :----------- | :------------------- | :------------------------------------------------ |
| 1 | 68114540377 | นายปรเมศ กองสุวรรณ์ | **Part 1, Part 2, Part 3** (Data Preprocessing, EDA, Hypothesis Testing, PCA) |
| 2 | 68114540573 | นายวิศรุต ปู่แก้ว | **Part 4, Part 5, Part 6** (Model Building, Cross-Validation, Evaluation & Conclusion) |

---

## 🎯 การครอบคลุมผลลัพธ์การเรียนรู้ (Course Learning Outcomes: CLO)

| สัปดาห์ | หมวดการเรียนรู้ (CLO) | หัวข้อเนื้อหา (Topics) | การประยุกต์ใช้จริงในโครงงาน | สถานะ |
| :---: | :--- | :--- | :--- | :---: |
| **Week 4** | **CLO1: Linear Algebra** | Covariance Matrix, Eigendecomposition & PCA | ประยุกต์ใช้ PCA เพื่อวิเคราะห์โครงสร้างของข้อมูล ลดมิติข้อมูล พร้อมแสดง Explained Variance, Scree Plot และการกระจายตัวของข้อมูลบน PC1 และ PC2 | ✅ |
| **Week 6–7** | **CLO2: Statistical Learning & EDA** | Distribution, Hypothesis Testing, Bias-Variance | วิเคราะห์การกระจายตัวด้วย Histogram และ Boxplot ทดสอบสมมติฐานทางสถิติ และจัดการ Missing values เช่น คอลัมน์ `playStyles` | ✅ |
| **Week 11–13** | **CLO3: Model Building** | Classification Pipeline, Logistic Regression, KNN | สร้าง Pipeline ร่วมกับ `StandardScaler` พัฒนาโมเดลเพื่อจำแนกกลุ่มระดับค่าพลังนักเตะ | ✅ |
| **Week 14** | **CLO4: Model Selection & CV** | 5-Fold Stratified CV, Model Comparison | เปรียบเทียบประสิทธิภาพของโมเดลจำแนกประเภท และคัดเลือกโมเดลที่ดีที่สุดจาก Mean CV Accuracy | ✅ |

---

## 📖 ข้อมูลชุดข้อมูล (Dataset Overview)

* **ชื่อชุดข้อมูล:** EA SPORTS FC 26 Players Dataset
* **แหล่งที่มา:** (https://www.kaggle.com/datasets/justdhia/ea-sports-fc-26-player-ratings)
* **ขนาดข้อมูลดิบ:** 14,412 แถว, 56 คอลัมน์
* **ขนาดข้อมูลหลังทำความสะอาด (Cleaned Data):** 14,412 แถว, 0 Missing Values
* **ตัวแปรเป้าหมาย (Target):** `overall` (ค่าพลังรวมของนักเตะ)

---

## 🗂️ พจนานุกรมข้อมูล (Data Dictionary)

| ชื่อตัวแปร (Feature) | ประเภทข้อมูล | คำอธิบายความหมาย |
| :--- | :---: | :--- |
| `commonName` | Categorical | ชื่อเรียกของนักเตะ |
| `age` | Numerical | อายุของนักเตะ |
| `height_cm` | Numerical | ส่วนสูง (เซนติเมตร) |
| `weight_kg` | Numerical | น้ำหนัก (กิโลกรัม) |
| `pace` | Numerical | ความเร็ว |
| `shooting` | Numerical | การยิงประตู |
| `passing` | Numerical | การจ่ายบอล |
| `dribbling` | Numerical | การเลี้ยงบอล |
| `defending` | Numerical | การเล่นเกมรับ |
| `physicality` | Numerical | ความแข็งแกร่งทางร่างกาย |
| `playStyles` | Categorical | สไตล์การเล่นพิเศษของนักเตะ |
| `playStylesPlus` | Categorical | สไตล์การเล่นขั้นสูง (PlayStyles+) |
| `overall` | Numerical / Categorical | ค่าพลังรวม (ตัวแปรเป้าหมาย) |

---

## 🏆 ผลการทดลองและเปรียบเทียบแบบจำลอง (Key Findings & Results)

*(ข้อมูลส่วนนี้จะถูกอัปเดตเมื่อการทดสอบใน Part 4-6 เสร็จสิ้น)*

| โมเดล (Classification Model) | Mean CV Accuracy | Standard Deviation (±) | Test Accuracy | Macro F1-Score |
| :--- | :---: | :---: | :---: | :---: |
| 🌲 **Random Forest Classifier (Best Model)** | **--.--%** | **±-.--%** | **--.--%** | **-.--** |
| 📈 Logistic Regression (Multi-class) | --.--% | ±-.--% | --.--% | -.-- |
| 📍 K-Nearest Neighbors | --.--% | ±-.--% | --.--% | -.-- |

> **สรุปผลการทดลอง:**  
> *(รอสรุปผลเปรียบเทียบโมเดลเมื่อสิ้นสุดโครงงาน)*

---

## 📁 โครงสร้างโปรเจกต์ (Repository Structure)

```text
math-ds-fc26-project/
├── data/
│   └── ea_fc26_outfield.csv           # ชุดข้อมูลที่ใช้ในโครงงาน
├── notebook/
│   └── ea-fc26-analytics-project.ipynb  # Jupyter Notebook ฉบับสมบูรณ์ (Part 1 - 6)
├── requirements.txt                       # ไลบรารีและเวอร์ชันที่ใช้ในโครงงาน
└── README.md                              # รายละเอียดโครงงาน
```
---

## ⚙️ วิธีการติดตั้งและรันโค้ด (Getting Started)

### 1. Clone Repository
```bash
git clone https://github.com/poramet-sudo/ea-fc26-analytics-project.git
cd math-ds-fc26-project
```

### 2. สร้างและเปิดใช้งาน Virtual Environment
```bash
python -m venv venv

# สำหรับ Windows PowerShell:
.\venv\Scripts\Activate.ps1

# สำหรับ macOS / Linux:
source venv/bin/activate
```

### 3. ติดตั้งไลบรารีที่จำเป็น
```bash
pip install notebook numpy pandas scipy matplotlib seaborn scikit-learn statsmodels
```

หรือ 

```bash
pip install -r requirements.txt
```

> กรณีมีไฟล์ `requirements.txt`


### 4. เปิดใช้งาน Jupyter Notebook
```bash
jupyter notebook
```

---