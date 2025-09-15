# Pretest-DataSci-Chatbot

# Medical Symptom Chatbot (RAG)

นี่คือโปรเจกต์ **RAG-based Chatbot** สำหรับประเมินอาการเบื้องต้นจากข้อมูล forum ของ Agnos Health 
โดยใช้ **Selenium**, **Pandas**, **Sentence Transformers**, **FAISS**, และ **Gradio** 
เพื่อสร้างระบบถาม-ตอบอาการทางการแพทย์

---

## 🔹 ฟีเจอร์หลัก
1. ดึงข้อมูลจาก [Agnos Health Forum](https://www.agnoshealth.com) โดยอัตโนมัติ (Selenium + XPATH) **ในโปรเจกต์นี้จะดึงข้อมูลมาเพียง 5 หน้าจากทั้งหมด
2. ทำความสะอาดข้อมูลและจัดเก็บใน CSV สำหรับ RAG
3. สร้าง embeddings ของข้อความ (Question + Answers + Symptoms + Keywords) ด้วย **SentenceTransformers**
4. ใช้ **FAISS** สำหรับค้นหาความใกล้เคียงของอาการ
5. แสดงผลผ่าน **Gradio interface** พร้อมไฮไลต์คำสำคัญ

---

## 🛠️ การติดตั้ง

1. Code นี้สำหรับ Google Colab (ง่ายที่สุด คือการ Download files Complete_test_DataSci.ipynb เปิดใน Google Colab ได้เลย)
```
!apt-get update
!apt install chromium-chromedriver -y
!pip install selenium pandas sentence-transformers faiss-cpu langchain gradio
```
2. สำหรับ Local Python
```pip install selenium pandas sentence-transformers faiss-cpu langchain gradio```
หมายเหตุ: ต้องติดตั้ง Chrome WebDriver ให้ตรงกับเวอร์ชัน Chrome ของคุณ


---

## 💻 การใช้งาน
1. รันสคริปต์ดึงข้อมูล Forum (รันสคริปต์ scraping)
python scrape_agnos_forum.py จะได้ไฟล์ agnos_forum_xpath.csv

2. เตรียม Dataset สำหรับ RAG
python prepare_rag_dataset.py จะได้ไฟล์ rag_ready_agnos.csv

3. รัน Chatbot ผ่าน Gradio
python run_rag_chatbot.py


เปิดหน้าเว็บ Gradio สำหรับถาม-ตอบอาการ

## 📝 ตัวอย่างการถาม-ตอบ
User: ผมเวียนหัวตอนเช้า ไม่มีแรง
Bot: จากการประเมินอาการเบื้องต้น พบอาการใกล้เคียง 3 อาการ ดังนี้:
🔹 จากการประเมินอาการเบื้องต้น คาดว่ามี/เป็น: อ่อนเพลีย
คำแนะนำ: **เวียนหัว** ควรพักผ่อนเพียงพอ | ดื่มน้ำเยอะ ๆ | ปรึกษาแพทย์หากอาการไม่ดีขึ้น
...
หมายเหตุ: แชทบอทนี้เป็นการประเมินเบื้องต้นเท่านั้น

## 📂 โครงสร้างไฟล์
├── scrape_agnos_forum.py      # สคริปต์ดึงข้อมูลจากเว็บ
├── prepare_rag_dataset.py     # ทำความสะอาดและรวมข้อความสำหรับ RAG
├── run_rag_chatbot.py         # สร้าง embeddings + FAISS + Gradio interface
├── agnos_forum_xpath.csv      # CSV ข้อมูล raw forum
├── rag_ready_agnos.csv        # CSV พร้อมใช้งานสำหรับ RAG
└── README.md

เนื่องจากมีเวลาทำที่จำกัดสำหรับโปรเจกต์นี้ อาจจะทำนายผลได้ยังไม่แม่นยำมาก
การพัฒนาขั้นต่อไป สามารถสร้างโมเดลจาก Dataset ที่ดึงมาแล้ว Train & Test ให้การทำนายแม่นยำมากขึ้น
จะทำให้การวิเคราะห์อาการของโรคได้ใกล้เคียงกับอาการของโรคจริงมากขึ้น




