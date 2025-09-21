# Workshop RAG Chatbot with LangChain and Streamlit
- Workshop แอปพลิเคชัน RAG (Retrieval-Augmented Generation) chatbot สร้างด้วย Streamlit ออกแบบมาเพื่อตอบคำถามเกี่ยวกับจังหวัดน่านโดยใช้เอกสาร PDF

## 🚀 Streamlit Cloud Deployment

This application is optimized for deployment on Streamlit Cloud. The main changes include:

- **Cloud-Compatible Vector Store**: Uses FAISS by default instead of Qdrant for better cloud compatibility
- **Python Version**: Compatible with Python 3.10+ (required by docling package)
- **Environment Variables**: Configure GROQ_API_KEY in Streamlit Cloud secrets

### Required Environment Variables for Streamlit Cloud:
```
GROQ_API_KEY=your_groq_api_key_here
```

### Deployment Steps:
1. Push your code to GitHub
2. Connect your repository to Streamlit Cloud
3. Set the GROQ_API_KEY in Streamlit Cloud secrets
4. Deploy with main file: `app.py`

## 📁 โครงสร้างโปรเจกต์

```
workshop_rag_rmutl/
├── app.py                    # แอปพลิเคชัน Streamlit หลักแบบรวมไฟล์เดียว
├── pyproject.toml            # การพึ่งพาโปรเจกต์และการกำหนดค่า
├── uv.lock                   # ไฟล์ล็อกการพึ่งพา
├── README.md                 # ไฟล์นี้
├── .gitignore                # ไฟล์ที่ Git จะไม่ติดตาม
├── notebooks/                # Jupyter notebooks 
├── pdf/                      # เอกสาร PDF สำหรับประมวลผล
├── model_cache/              # แคชโมเดล embedding
├── .venv/                    # Virtual environment
└── .devcontainer/            # การตั้งค่า Dev Container
```

## 🛠️ การติดตั้ง

### ข้อกำหนดเบื้องต้น

- Python 3.12+
- Vscode 
- Git 
- GitHub
- pip 
- UV package manager 

### การติดตั้ง UV บน Windows

#### วิธีที่ 1: ติดตั้งผ่าน pip (แนะนำ)
```cmd
pip install uv
```

#### วิธีที่ 2: ติดตั้งผ่าน PowerShell (Windows 10/11)
```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

#### วิธีที่ 3: ติดตั้งผ่าน winget
```cmd
winget install --id=astral-sh.uv -e
```

#### วิธีที่ 4: ติดตั้งผ่าน Chocolatey
```cmd
choco install uv
```

#### วิธีที่ 5: ติดตั้งผ่าน Scoop
```cmd
scoop install uv
```

#### ตรวจสอบการติดตั้ง
```cmd
uv --version
```

### การตั้งค่า

1. **Clone repository**
   ```cmd
   git clone https://github.com/JeerasakAnanta/workshop_rag_rmutl
   cd workshop_rag_rmutl
   ```

2. **ติดตั้ง dependencies ด้วย UV**
   
   **สำหรับ Windows Command Prompt (cmd):**
   ```cmd
   uv sync
   ```
   
   **สำหรับ PowerShell:**
   ```powershell
   uv sync
   ```
   
   **สำหรับ Git Bash:**
   ```bash
   uv sync
   ```

3. **สร้างไฟล์ environment**
   
   **สำหรับ Windows Command Prompt:**
   ```cmd
   copy .env.example .env
   ```
   
   **สำหรับ PowerShell:**
   ```powershell
   Copy-Item .env.example .env
   ```
   
   **สำหรับ Git Bash:**
   ```bash
   cp .env.example .env
   ```
   
   แก้ไข `.env` และเพิ่ม API keys ของคุณ:
   ```
   GROQ_API_KEY=your_groq_api_key_here
   ```

4. **รันแอปพลิเคชัน**
   
   **สำหรับ Windows Command Prompt:**
   ```cmd
   uv run streamlit run app.py
   ```
   
   **สำหรับ PowerShell:**
   ```powershell
   uv run streamlit run app.py
   ```
   
   **สำหรับ Git Bash:**
   ```bash
   uv run streamlit run app.py
   ```

### การแก้ไขปัญหาเฉพาะ Windows

#### ปัญหา Execution Policy ใน PowerShell
หากพบข้อผิดพลาดเกี่ยวกับ Execution Policy:
```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

#### ปัญหา PATH Environment Variable
หาก `uv` command ไม่ทำงาน ให้เพิ่ม UV ไปยัง PATH:
1. เปิด System Properties → Environment Variables
2. เพิ่ม `%USERPROFILE%\.cargo\bin` หรือ `%LOCALAPPDATA%\Programs\uv` ไปยัง PATH
3. รีสตาร์ท Command Prompt หรือ PowerShell

#### ปัญหา Long Path Support
สำหรับ Windows 10/11 ให้เปิดใช้งาน Long Path Support:
1. เปิด Group Policy Editor (gpedit.msc)
2. ไปที่ Computer Configuration → Administrative Templates → System → Filesystem
3. เปิดใช้งาน "Enable Win32 long paths"

#### การใช้ Windows Terminal (แนะนำ)
ติดตั้ง Windows Terminal สำหรับประสบการณ์ที่ดีกว่า:
```cmd
winget install Microsoft.WindowsTerminal
```

## 📱 ภาพรวมหน้า

### 💬 หน้า Chatbot
- **อินเทอร์เฟซแชทหลัก** พร้อมประวัติข้อความ
- **ปุ่มคำถามด่วน** สำหรับคำถามที่พบบ่อย
- **การสนทนาแบบเรียลไทม์** กับระบบ RAG
- **การควบคุมแชท** สำหรับล้างประวัติและคัดลอกการสนทนา

### 📚 หน้าการจัดการเอกสาร
- **ฟังก์ชันการอัปโหลดไฟล์ PDF**
- **การประมวลผลเอกสาร** พร้อมตัวบ่งชี้ความคืบหน้า
- **ตัวอย่างเอกสาร** แสดงเนื้อหาที่ประมวลผลแล้ว
- **การตั้งค่าการกำหนดค่า** สำหรับพารามิเตอร์การประมวลผล
- **สถานะระบบ** และข้อมูลไฟล์

### 📊 หน้าสถิติ
- **เมตริกแบบเรียลไทม์** รวมถึงคำถาม, ข้อความ และเวลาของเซสชัน
- **สถิติเอกสาร** พร้อมข้อมูลไฟล์
- **การวิเคราะห์แชท** พร้อมการกระจายข้อความ
- **การตรวจสอบประสิทธิภาพระบบ**
- **ฟังก์ชันการส่งออก** สำหรับการวิเคราะห์ข้อมูล

## 📓 Jupyter Notebooks

โปรเจกต์นี้รวม Jupyter notebooks สำหรับการเรียนรู้และทำความเข้าใจ RAG:

### 🎯 00_simple_chatbot_demo.ipynb
- การสาธิต chatbot แบบง่าย
- แนะนำการใช้งาน LangChain และ Groq
- การสร้างการสนทนาพื้นฐาน

### 🔍 01_introduction_to_rag_langchain.ipynb
- แนะนำแนวคิด RAG (Retrieval-Augmented Generation)
- การใช้งาน LangChain framework
- การสร้าง chain พื้นฐาน

### 📄 02_data_ingestion_vector_store.ipynb
- การประมวลผลเอกสาร PDF
- การสร้าง vector embeddings
- การจัดเก็บข้อมูลใน vector database

### 🔗 03_build_rag_pipeline.ipynb
- การสร้าง RAG pipeline ที่สมบูรณ์
- การรวม retrieval และ generation
- การปรับแต่งและทดสอบระบบ

### 🖥️ 04_streamlit_ui.ipynb
- การสร้าง UI ด้วย Streamlit
- การออกแบบหน้าเว็บแอปพลิเคชัน
- การรวม UI กับ RAG backend

### 🚀 05_wrapup_advanced_topics.ipynb
- หัวข้อขั้นสูงและการปรับปรุง
- การเพิ่มประสิทธิภาพระบบ
- การขยายฟีเจอร์และสรุปการเรียนรู้

## 🔧 การกำหนดค่า

แอปพลิเคชันใช้ระบบการกำหนดค่าแบบรวมศูนย์ใน `Config` class ใน `app.py` การตั้งค่าหลักรวมถึง:

- **โมเดล**: โมเดล embedding (`all-MiniLM-L6-v2`) และโมเดล LLM (`llama-3.3-70b-versatile`)
- **ฐานข้อมูลเวกเตอร์**: การกำหนดค่า Qdrant/FAISS/Chroma (ในหน่วยความจำหรือถาวร)
- **พารามิเตอร์การค้นหา**: จำนวนเอกสารที่จะดึงมา
- **เส้นทางไฟล์**: ตำแหน่ง PDF เริ่มต้น (`pdf/จังหวัดน่าน.pdf`)
- **การประมวลผลเอกสาร**: การตั้งค่า Docling สำหรับ OCR และการดึงตาราง
- **การแชท**: การตั้งค่าความจำการสนทนาและข้อความระบบ

## 📚 การใช้งาน

### เริ่มต้นใช้งาน

1. **เปิดแอปพลิเคชัน**: รัน `uv run streamlit run app.py`
2. **นำทางหน้า**: ใช้เมนูแถบด้านข้างเพื่อเปลี่ยนหน้า
3. **โหลดเอกสาร**: ไปที่หน้า "การจัดการเอกสาร" เพื่ออัปโหลดหรือโหลด PDF เริ่มต้น
4. **เริ่มแชท**: เปลี่ยนไปที่หน้า "Chatbot" เพื่อเริ่มการสนทนา
5. **ดูสถิติ**: ตรวจสอบหน้า "สถิติ" สำหรับการวิเคราะห์และเมตริก

### การนำทางหน้า

- **เมนูแถบด้านข้าง**: คลิกที่ชื่อหน้าในแถบด้านข้างเพื่อนำทาง
- **สถานะระบบ**: ดูสถานะระบบแบบเรียลไทม์ในแถบด้านข้าง
- **การดำเนินการด่วน**: เข้าถึงฟังก์ชันทั่วไปจากแถบด้านข้าง

### การจัดการเอกสาร

1. **อัปโหลด PDF**: ใช้ตัวอัปโหลดไฟล์ในหน้าการจัดการเอกสาร
2. **ประมวลผลเอกสาร**: คลิก "ประมวลผลเอกสาร" เพื่อดึงและจัดทำดัชนีเนื้อหา
3. **ดูสถานะ**: ติดตามความคืบหน้าของการประมวลผลและจำนวนเอกสาร
4. **ตัวอย่างเนื้อหา**: ดูเอกสารตัวอย่างหลังการประมวลผล

### การแชท

1. **ถามคำถาม**: พิมพ์คำถามในช่องใส่ข้อความแชท
2. **ใช้คำถามด่วน**: คลิกปุ่มคำถามที่กำหนดไว้ล่วงหน้า
3. **ดูประวัติ**: ดูประวัติการสนทนาในอินเทอร์เฟซแชท
4. **จัดการแชท**: ล้างประวัติหรือคัดลอกการสนทนาตามต้องการ

## 🏗️ สถาปัตยกรรม

### ส่วนประกอบหลัก

แอปพลิเคชันนี้ใช้สถาปัตยกรรมแบบรวมไฟล์เดียว (`app.py`) ที่ประกอบด้วย:

- **Config Class**: การจัดการการกำหนดค่าแบบรวมศูนย์พร้อมการตรวจสอบ
- **Data Models**: โครงสร้างข้อมูลสำหรับเอกสาร, ผลการค้นหา และข้อความแชท
- **Services**: 
  - `EmbeddingService`: การแปลงข้อความเป็นเวกเตอร์พร้อมการแคช
  - `VectorStoreService`: การดำเนินการ Qdrant/FAISS/Chroma
  - `LLMService`: การรวม Groq API
  - `RAGService`: บริการหลักสำหรับการประสานงาน RAG pipeline
- **PDF Processing**: การประมวลผลเอกสาร PDF ด้วย Docling และ PyPDF
- **Streamlit UI**: อินเทอร์เฟซผู้ใช้แบบหลายหน้าในไฟล์เดียว

### เทคโนโลยีที่ใช้

- **LangChain**: Framework หลักสำหรับ RAG pipeline
- **Streamlit**: UI framework สำหรับเว็บแอปพลิเคชัน
- **Groq**: LLM provider สำหรับการสร้างข้อความ
- **HuggingFace**: Embedding models
- **Qdrant/FAISS/Chroma**: Vector databases
- **Docling**: การประมวลผลเอกสาร PDF ขั้นสูง
- **UV**: Package manager สำหรับ Python

## 🔍 คู่มือ API

### RAGService

คลาสบริการหลักที่ประสานงาน RAG pipeline:

```python
# โหลดเอกสารจาก PDF
doc_count = rag_service.load_documents_from_pdf(pdf_path)

# ตอบคำถาม
answer = rag_service.answer_question(question)

# สร้าง vector store
vector_store = rag_service.create_vector_store(documents)
```

### Configuration

```python
from app import Config

# เข้าถึงค่าการกำหนดค่า
model_name = Config.EMBEDDING_MODEL
vector_size = Config.VECTOR_SIZE
groq_api_key = Config.GROQ_API_KEY
```

### การใช้งานหลัก

**สำหรับ Linux/macOS:**
```bash
# เริ่มต้นแอปพลิเคชัน
uv run streamlit run app.py

# การตั้งค่าสภาพแวดล้อม
export GROQ_API_KEY="your_api_key_here"
```

**สำหรับ Windows:**

**Command Prompt:**
```cmd
# เริ่มต้นแอปพลิเคชัน
uv run streamlit run app.py

# การตั้งค่าสภาพแวดล้อม
set GROQ_API_KEY=your_api_key_here
```

**PowerShell:**
```powershell
# เริ่มต้นแอปพลิเคชัน
uv run streamlit run app.py

# การตั้งค่าสภาพแวดล้อม
$env:GROQ_API_KEY="your_api_key_here"
```

**Git Bash:**
```bash
# เริ่มต้นแอปพลิเคชัน
uv run streamlit run app.py

# การตั้งค่าสภาพแวดล้อม
export GROQ_API_KEY="your_api_key_here"
```

### การทดสอบระบบ

รันสคริปต์ทดสอบเพื่อตรวจสอบการทำงานของระบบ:

**สำหรับ Linux/macOS:**
```bash
uv run python test_rag.py
```

**สำหรับ Windows:**
```cmd
# Command Prompt
uv run python test_rag.py

# PowerShell
uv run python test_rag.py

# Git Bash
uv run python test_rag.py
```

### ปัญหาที่พบบ่อย

1. **ไม่สามารถตอบคำถามได้**
   - ตรวจสอบการตั้งค่า `GROQ_API_KEY`
   - ติดตั้ง dependencies ที่จำเป็น: `uv add langchain-huggingface`
   - ตรวจสอบว่ามีไฟล์ PDF ในโฟลเดอร์ `pdf/`

2. **Import Error**
   - รัน `uv sync` เพื่อติดตั้ง dependencies ทั้งหมด
   - ตรวจสอบ Python version (ต้องเป็น 3.8+)

3. **Memory Issues**
   - ลดขนาด chunk ใน configuration
   - ใช้ FAISS แทน Qdrant สำหรับหน่วยความจำน้อย

4. **QA chains not initialized**
   - ระบบจะโหลดเอกสารอัตโนมัติเมื่อมีคำถามแรก
   - ใช้ปุ่ม "🔄 โหลดเอกสารใหม่" ใน UI
   - รัน `uv run python test_qa_chains.py` เพื่อทดสอบ

5. **Windows-specific Issues**
   
   **ปัญหา UV ไม่พบ command:**
   ```cmd
   # ตรวจสอบ PATH
   echo %PATH%
   
   # เพิ่ม UV ไปยัง PATH ชั่วคราว
   set PATH=%PATH%;%USERPROFILE%\.cargo\bin
   ```
   
   **ปัญหา Permission Denied:**
   ```cmd
   # รัน Command Prompt เป็น Administrator
   # หรือใช้ PowerShell
   Start-Process powershell -Verb RunAs
   ```
   
   **ปัญหา Antivirus Blocking:**
   - เพิ่มโฟลเดอร์โปรเจกต์ไปยัง Antivirus exclusion list
   - ปิดการสแกนแบบ real-time ชั่วคราว
   
   **ปัญหา Long Path Names:**
   ```cmd
   # เปิดใช้งาน Long Path Support
   reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\FileSystem" /v LongPathsEnabled /t REG_DWORD /d 1
   ```
   
   **ปัญหา PowerShell Execution Policy:**
   ```powershell
   # ตรวจสอบ current policy
   Get-ExecutionPolicy
   
   # เปลี่ยน policy สำหรับ current user
   Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
   ```
   
   **ปัญหา Git Bash vs Command Prompt:**
   - ใช้ Git Bash สำหรับคำสั่ง Unix-style
   - ใช้ Command Prompt หรือ PowerShell สำหรับคำสั่ง Windows-style
   - ตรวจสอบว่าใช้คำสั่งที่ถูกต้องสำหรับ shell ที่เลือก

### การเพิ่มฟีเจอร์ใหม่

1. **การปรับปรุง UI**: แก้ไขใน `app.py` ในส่วน Streamlit interface
2. **การเพิ่มบริการใหม่**: เพิ่มคลาสใหม่ใน `app.py` ตามรูปแบบที่มีอยู่
3. **การปรับปรุงโมเดล**: แก้ไขใน `Config` class สำหรับการตั้งค่าใหม่
4. **การเพิ่มการประมวลผลเอกสาร**: ปรับปรุงฟังก์ชัน PDF processing

### Jupyter Notebooks

โปรเจกต์รวม notebooks สำหรับการเรียนรู้:

- `00_simple_chatbot_demo.ipynb`: การสาธิต chatbot แบบง่าย
- `01_introduction_to_rag_langchain.ipynb`: แนะนำ RAG และ LangChain
- `02_data_ingestion_vector_store.ipynb`: การจัดการข้อมูลและ vector store
- `03_build_rag_pipeline.ipynb`: การสร้าง RAG pipeline
- `04_streamlit_ui.ipynb`: การสร้าง UI ด้วย Streamlit
- `05_wrapup_advanced_topics.ipynb`: หัวข้อขั้นสูงและการสรุป

## 📈 การปรับปรุงประสิทธิภาพ

1. **การแคชโมเดล**: โมเดล embedding ถูกแคชเพื่อหลีกเลี่ยงการโหลดใหม่
2. **การประมวลผลแบบแบทช์**: การเข้ารหัสข้อความประมวลผลในแบทช์ละ 32
3. **การแคช Streamlit**: บริการ RAG ถูกแคชด้วย `@st.cache_resource`
4. **การจัดการหน่วยความจำ**: การประมวลผลและการจัดเก็บเอกสารที่มีประสิทธิภาพ
5. **การโหลดแบบหน้า**: โหลดเฉพาะส่วนประกอบที่จำเป็นต่อหน้า

สำหรับคำถามหรือปัญหา กรุณาติดต่อ:
- อีเมล: jeerasakananta@gmail.com
- GitHub Issues: [สร้าง issue](https://github.com/your-repo/issues)