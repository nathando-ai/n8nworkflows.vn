---
title: "🤖 Tự Động Xây Dựng Chatbot RAG Trí Tuệ Nhân Tạo Cho Website Công Ty Bằng Apify, Pinecone & Gemini (Không Cần Code)"
description: "Hướng dẫn chi tiết xây dựng chatbot RAG thông minh cho website công ty, tự động scrape dữ liệu từ trang web, lưu trữ vector trong Pinecone, và trả lời câu hỏi bằng Gemini AI. Giúp tiết kiệm thời gian, cải thiện trải nghiệm khách hàng và tối ưu hóa nội dung."
slug: "tay-dong-xay-dung-chatbot-rag-cho-website"
tags: [n8n, automation, ai-rag, chatbot, apify, pinecone, google-gemini, no-code]
keywords: [n8n workflow chatbot, tự động hóa chatbot website, RAG với Gemini AI, scrape website tự động, Pinecone vector database, AI cho doanh nghiệp]
---

# 🚀 **Tự Động Xây Dựng Chatbot RAG Trí Tuệ Nhân Tạo Cho Website Công Ty (Không Cần Code)**

## **🔍 Nỗi Đau Của Các Sếp: Khách Hàng Không Tìm Thấy Thông Tin Mà Bạn Đã Đặt Trên Website**
Các sếp đã từng gặp phải tình huống này chưa?
- Khách hàng liên tục gọi email hoặc chat để hỏi về sản phẩm, dịch vụ, hoặc chính sách mà **đã rõ ràng được đăng trên website**.
- Đội ngũ hỗ trợ phải **lặp đi lặp lại** trả lời những câu hỏi cơ bản, mất thời gian và giảm hiệu quả.
- **Nội dung website không được tối ưu** để AI hiểu và trả lời tự động, dẫn đến trải nghiệm khách hàng kém.

**Giải pháp?** Một **chatbot RAG (Retrieval-Augmented Generation)** thông minh, tự động scrape dữ liệu từ website, lưu trữ và trả lời câu hỏi bằng trí tuệ nhân tạo **Gemini** của Google – **không cần viết một dòng code nào!**

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
✅ **Tiết kiệm thời gian hỗ trợ khách hàng** – Chatbot trả lời tự động 24/7, giảm tải cho đội ngũ.
✅ **Trả lời chính xác & cá nhân hóa** – AI hiểu ngữ cảnh và lấy thông tin từ website thực tế.
✅ **Cập nhật tự động** – Dữ liệu website được scrape định kỳ, chatbot luôn có thông tin mới nhất.
✅ **Tối ưu SEO & nội dung** – Dữ liệu được lưu trữ trong **Pinecone (vector database)**, giúp AI tìm kiếm nhanh chóng.
✅ **Không cần kỹ thuật** – Sử dụng **n8n (self-hosted)** để chạy workflow 24/7, không phụ thuộc vào cloud miễn phí.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Cloud** (để sử dụng **Gemini AI**)
   - Tạo **Google Cloud Project** và **enable Vertex AI API**.
   - Lấy **Google AI API Key** từ [Google AI Studio](https://aistudio.google.com/).
2. **Tài khoản Apify** (để scrape website)
   - Đăng ký tại [Apify](https://apify.com/).
3. **Tài khoản Pinecone** (để lưu trữ vector)
   - Tạo **free account** và lấy **API Key**.
   - Tạo **index** có tên `company-website` (hoặc tên khác tùy ý).
4. **n8n Self-hosted** (để chạy workflow 24/7)
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/14157](https://n8n.io/workflows/14157) và import vào **n8n Editor**.
- **Copy JSON** và dán vào **Create Workflow** trong n8n.

:::note[**Lưu ý quan trọng**]
- **Không chạy workflow ngay lập tức** – Các node có **sticky note màu cam** cần cấu hình trước.
- **Không sử dụng trigger miễn phí** – Nên cài **n8n self-hosted** để workflow hoạt động liên tục.
:::

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **🔹 Cấu Hình Credentials (Tất Cả Các Node AI)**
Các node sau **cần kết nối với API Key** của các dịch vụ:

| **Node** | **Thao Tác Cần Làm** | **Tham Số Cần Điền** |
|----------|----------------------|----------------------|
| **Google Gemini (Embeddings & Chat)** | Kết nối với **Google AI API Key** | `API Key` từ Google Cloud |
| **Pinecone Vector Store** | Kết nối với **Pinecone API Key** | `API Key` + `Index Name` (`company-website`) |
| **Apify Scraper** | Kết nối với **Apify Account** | `API Token` từ Apify |

**Hướng dẫn chi tiết:**
1. **Tạo credentials mới** trong n8n:
   - Vào **Credentials** → **Add Credential** → Chọn loại phù hợp (Google, Pinecone, Apify).
2. **Điền API Key** vào các node tương ứng:
   - **Google Gemini**:
     ```json
     {
       "apiKey": "YOUR_GOOGLE_AI_API_KEY"
     }
     ```
   - **Pinecone**:
     ```json
     {
       "apiKey": "YOUR_PINECONE_API_KEY",
       "environment": "us-west1-gcp-free", // hoặc môi trường khác
       "indexName": "company-website"
     }
     ```
   - **Apify**:
     ```json
     {
       "token": "YOUR_APIFY_API_TOKEN"
     }
     ```

#### **🔹 Cấu Hình Node Apify (Scrape Website)**
1. **Chọn Actor** (công cụ scrape):
   - Tìm actor phù hợp trên [Apify Marketplace](https://apify.com/marketplace) (ví dụ: `web-scraper`).
2. **Điền URL website** vào **JSON Input**:
   ```json
   {
     "startUrls": ["https://website-cua-ban.com"]
   }
   ```
   - Thay `website-cua-ban.com` bằng URL thực tế của công ty.

#### **🔹 Cấu Hình Schedule Trigger (Cập Nhật Dữ liệu)**
- **Mặc định**: Workflow chạy **mỗi ngày** (có thể thay đổi).
- **Nếu muốn chạy một lần**: Thay **Schedule Trigger** bằng **Webhook Trigger** (nhấn nút "Run" thủ công).

#### **🔹 Cấu Hình Chat Trigger (Kích Hoạt Chatbot)**
- Nếu muốn chatbot hoạt động trên **Slack/Telegram/Website**, cần kết nối:
  - **Slack**: Sử dụng node `@n8n/n8n-nodes-slack`.
  - **Telegram**: Sử dụng node `@n8n/n8n-nodes-telegram`.
  - **Website**: Sử dụng node `@n8n/n8n-nodes-webhook`.

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Run Workflow** và kiểm tra các node có hoạt động không.
   - Kiểm tra **Pinecone** có lưu trữ vector thành công không.
2. **Bật Active**:
   - Sau khi kiểm tra xong, **bật Active** để workflow chạy tự động.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **1. Kết Nối Với Slack/Telegram**
- Sử dụng **node Slack/Telegram** để chatbot trả lời trên kênh trực tiếp.
- **Cấu hình**:
  ```json
  {
    "channel": "#chatbot-support",
    "token": "YOUR_SLACK_BOT_TOKEN"
  }
  ```

### **2. Lưu Log & Báo Cáo Hàng Ngày**
- Sử dụng **node `n8n-nodes-base.set`** để lưu log vào **Google Sheets** hoặc **Firebase**.
- **Ví dụ**:
  ```json
  {
    "operation": "createSpreadsheetRow",
    "sheetName": "Chatbot_Logs",
    "data": {
      "Timestamp": "{{ $node["Set"].json["$node["Set"].json"]["timestamp"] }}",
      "Question": "{{ $node["Chat Trigger"].json["question"] }}",
      "Answer": "{{ $node["Gemini Chat"].json["response"] }}"
    }
  }
  ```

### **3. Cập Nhật Dữ liệu Tự Động Theo Lịch**
- Sử dụng **Schedule Trigger** để scrape website **mỗi ngày/lần tuần**.
- **Cấu hình**:
  ```json
  {
    "cron": "0 0 * * *" // Chạy mỗi ngày lúc 00:00
  }
  ```

### **4. Tối Ưu Hóa Prompt cho Gemini**
- Nếu chatbot trả lời không chính xác, **cập nhật prompt** trong node `lmChatGoogleGemini`:
  ```json
  {
    "prompt": "You are a helpful assistant for a company website. Answer questions based on the latest data scraped from the website. If you don't know the answer, say 'I don't have that information.'"
  }
  ```

---

## **📌 Kết Luận**
Với workflow này, các sếp đã có một **chatbot RAG thông minh**, tự động scrape và trả lời câu hỏi từ website **không cần viết code**. Đây là giải pháp **tiết kiệm thời gian, cải thiện trải nghiệm khách hàng** và **tối ưu hóa nội dung** một cách hiệu quả.

**Bắt đầu ngay!**
1. **Import workflow** vào n8n self-hosted.
2. **Cấu hình credentials** (Google, Pinecone, Apify).
3. **Test & bật Active** để chatbot hoạt động.

**🚀 Cần hỗ trợ?** Đăng ký VPS n8n tại [TinoHost](https://tino.vn/vps-n8n?affid=388) với **mã giảm giá VPSN8N** để workflow chạy ổn định 24/7!

---
**#TựĐộngHóa #ChatbotRAG #GeminiAI #Pinecone #Apify #n8nSelfHosted**