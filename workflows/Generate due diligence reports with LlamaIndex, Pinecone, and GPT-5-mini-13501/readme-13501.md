---
title: "🚀 Tự Động Hóa Báo Cáo Due Diligence Tích Hợp AI (LlamaIndex + Pinecone + GPT-5) - Không Cần Code!"
description: "Workflow tự động hóa hoàn toàn để phân tích và tổng hợp báo cáo due diligence từ tài liệu đầu vào (PDF, Word, Excel...) thành báo cáo PDF chuyên nghiệp với AI GPT-5, Pinecone và LlamaIndex. Giúp các sếp tiết kiệm 100+ giờ công mỗi tháng trong quá trình kiểm tra đầu tư."
slug: "tự-dộng-hoa-báo-cáo-due-diligence-ai"
tags: [n8n, automation, ai-rag, due-diligence, pinecone, openai, self-hosted]
keywords: [n8n workflow due diligence, tự động hóa báo cáo đầu tư, AI GPT-5, LlamaIndex, Pinecone vector database, tự động hóa không code]
---

# 🚀 **Tự Động Hóa Báo Cáo Due Diligence Tích Hợp AI: Từ Tài Liệu → Báo Cáo PDF Chuyên Nghiệp**

### **Nỗi Đau Của Các Sếp Trong Quá Trình Due Diligence**
Mỗi khi chuẩn bị báo cáo đầu tư, các sếp phải:
- **Tốn thời gian vô cùng** để phân tích hàng chục tài liệu (PDF, Word, Excel, email...) từ đối tác.
- **Mất chính xác** khi tổng hợp thông tin thủ công từ nhiều nguồn khác nhau.
- **Không thể cá nhân hóa** báo cáo theo yêu cầu cụ thể của khách hàng.
- **Không hoạt động 24/7**, phụ thuộc vào nhân viên làm việc theo giờ.

**Workflow này giải quyết tất cả!** Dùng AI GPT-5 + Pinecone + LlamaIndex để tự động:
✅ **Phân tích toàn bộ tài liệu** (ngôn ngữ tự nhiên, số liệu tài chính, rủi ro).
✅ **Tạo báo cáo PDF chuyên nghiệp** với cấu trúc chuẩn (company profile, financials, risks, investment thesis).
✅ **Cập nhật liên tục** 24/7, không phụ thuộc vào nhân viên.
✅ **Tiết kiệm 100+ giờ công** mỗi tháng cho đội ngũ phân tích.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7**, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho AI + Pinecone)
:::

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100+ giờ công/tháng** trong việc phân tích tài liệu.
- **Báo cáo chính xác 100%** nhờ AI GPT-5 tổng hợp logic từ nhiều nguồn.
- **Cá nhân hóa báo cáo** theo yêu cầu khách hàng (thêm/bỏ phần tùy ý).
- **Hoạt động tự động 24/7**, không phụ thuộc vào nhân viên.
- **Kết nối với Slack/Email** để thông báo kết quả ngay khi hoàn thành.
- **Lưu trữ báo cáo trên S3** với URL công khai để chia sẻ dễ dàng.
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
### **1. Tài Khoản & API Keys**
| Dịch Vụ               | API Key/Credential          | Ghi Chú                                                                 |
|-----------------------|----------------------------|-------------------------------------------------------------------------|
| **OpenAI**            | `openAiApi`                | API Key từ [OpenAI](https://platform.openai.com/) (để dùng GPT-5-mini). |
| **Pinecone**          | `pineconeApi`              | API Key + Index tên `"poc"` (tạo trước trên [Pinecone](https://pinecone.io/)). |
| **AWS S3**            | `s3`                       | Bucket tên `"poc"` (tạo trước trên AWS S3).                              |
| **LlamaParse**        | `httpHeaderAuth` (Header)  | API Key từ [LlamaParse](https://llamaparse.com/) (để phân tích tài liệu). |

### **2. Cấu Hình N8n**
- **Cài đặt n8n phiên bản mới nhất** (n8n Core 1.30+).
- **Cài đặt nodes bổ sung**:
  ```bash
  npx n8n install @n8n/nodes-langchain
  npx n8n install n8n-nodes-puppeteer
  ```

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Từ File JSON**
1. Tải workflow từ [n8n.io/workflows/13501](https://n8n.io/workflows/13501).
2. Trên trang n8n Editor, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Workflow Name**: `Due Diligence AI Report Generator`.

#### **Phương pháp 2: Copy/Paste JSON**
1. Copy toàn bộ JSON từ [n8n.io/workflows/13501](https://n8n.io/workflows/13501).
2. Trên n8n Editor, nhấn **Import** → Chọn **Paste JSON**.

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **31 node**, nhưng chỉ **5 node quan trọng** cần cấu hình kỹ:

#### **🔹 Node 1: Webhook (Nhận File Upload)**
- **Tên Node**: `Receive Upload Request`
- **Cấu Hình**:
  - **Path**: `/dd-ai` (không đổi).
  - **HTTP Method**: `POST`.
  - **Credentials**: Không cần (sử dụng mặc định).

#### **🔹 Node 2: OpenAI API (GPT-5-mini)**
- **Tên Node**: `OpenAI Chat Model (5-mini)`
- **Cấu Hình**:
  - **Model**: Chọn `gpt-5-mini` (đã cấu hình sẵn).
  - **API Key**: Điền vào `openAiApi` (từ OpenAI).
  - **Temperature**: Giữ mặc định `0.7` (để AI logic hơn).

#### **🔹 Node 3: Pinecone Vector Store**
- **Tên Node**: `Upsert Chunks to Pinecone` & `Retrieve Context from Pinecone`
- **Cấu Hình**:
  - **API Key**: Điền vào `pineconeApi`.
  - **Index Name**: `"poc"` (phải tạo trước trên Pinecone).
  - **Namespace**: Sử dụng `dealId` (tự động tạo từ file upload).

#### **🔹 Node 4: LlamaParse (Phân Tích Tài Liệu)**
- **Tên Node**: `Upload File to LlamaParse`
- **Cấu Hình**:
  - **URL API**: `https://api.llamaparse.com/v1/parse` (mặc định).
  - **Headers**:
    - `Authorization`: `Bearer <API_KEY>` (từ LlamaParse).
    - `Content-Type`: `multipart/form-data`.

#### **🔹 Node 5: S3 (Lưu Báo Cáo PDF)**
- **Tên Node**: `Upload Report PDF to S3`
- **Cấu Hình**:
  - **Bucket Name**: `"poc"` (phải tạo trước trên AWS S3).
  - **Region**: Chọn vùng gần nhất (ví dụ: `ap-southeast-1`).
  - **Credentials**: Điền `s3` (từ AWS S3).

---

### **3. Kích Hoạt ⚡️**
1. **Test Run Dữ Liệu Mẫu**:
   - Gửi một file mẫu (ví dụ: PDF về tài chính của công ty) đến endpoint `/dd-ai` bằng Postman hoặc cURL:
     ```bash
     curl -X POST "http://<n8n-server>/dd-ai" \
     -H "Content-Type: multipart/form-data" \
     -F "files=@sample.pdf"
     ```
   - Kiểm tra **Execution Log** trong n8n để xác nhận workflow chạy thành công.

2. **Bật Active Workflow**:
   - Nhấn **Active** trên workflow để nó bắt đầu xử lý tự động.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Kết Nối Với Slack/Email**
- Thêm **node `n8n-nodes-base.slack`** hoặc **`n8n-nodes-base.email`** sau node `Return API Response` để thông báo kết quả.
- **Ví dụ**:
  ```json
  {
    "name": "Notify Slack",
    "type": "slack",
    "credentials": {
      "slackApi": "slack-webhook-url"
    },
    "keyParameters": {
      "text": "Báo cáo Due Diligence đã hoàn thành! URL: {{ $json.publicUrl }}"
    }
  }
  ```

### **2. Lưu Log Tất Cả Báo Cáo**
- Thêm **node `n8n-nodes-base.googleSheets`** để ghi tất cả kết quả vào bảng Google Sheets:
  ```json
  {
    "name": "Log to Google Sheets",
    "type": "googleSheets",
    "credentials": {
      "googleSheetsApi": "google-sheets-api-key"
    },
    "keyParameters": {
      "sheetName": "Due Diligence Logs",
      "data": {
        "Deal ID": "{{ $json.dealId }}",
        "Public URL": "{{ $json.publicUrl }}",
        "Status": "Completed"
      }
    }
  }
  ```

### **3. Tự Động Gửi Báo Cáo Định Kỳ**
- Sử dụng **node `n8n-nodes-base.cron`** để chạy workflow hàng tuần/month để cập nhật báo cáo:
  ```json
  {
    "name": "Run Weekly Update",
    "type": "cron",
    "keyParameters": {
      "schedule": "0 0 * * 0"  // Thứ 7 hàng tuần
    }
  }
  ```

### **4. Cải Thiện AI với Prompt Tùy Chỉnh**
- Trong node `Prepare Analysis Context`, chỉnh sửa **prompt** để AI tập trung vào phần nào:
  ```javascript
  // Ví dụ: Tăng trọng số cho phần "Rủi ro tài chính"
  const prompt = `
  Analyze the following documents and provide a structured due diligence report.
  Focus heavily on financial risks (weight: 40%) and investment thesis (weight: 30%).
  `;
  ```

---

## 📌 **Kết Luận**
Workflow này **giải phóng hoàn toàn** các sếp khỏi công việc phân tích báo cáo due diligence thủ công. Với **AI GPT-5 + Pinecone + LlamaIndex**, nó tự động:
✔ **Phân tích toàn bộ tài liệu** (PDF, Word, Excel...).
✔ **Tạo báo cáo PDF chuyên nghiệp** với cấu trúc chuẩn.
✔ **Cập nhật liên tục** 24/7.
✔ **Tiết kiệm 100+ giờ công/tháng**.

**Hành động ngay!**
1. **Cài đặt n8n trên VPS** (dùng mã giảm giá **VPSN8N**).
2. **Import workflow** và cấu hình API keys.
3. **Test với file mẫu** và bắt đầu tự động hóa!

👉 **[Tải workflow ngay](https://n8n.io/workflows/13501)** và **bắt đầu tiết kiệm thời gian!** 🚀