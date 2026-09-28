---
title: "🌍 🤖 **Hướng Dẫn Tự Động Hóa Gợi Ý Tour Du Lịch Cá Nhân Hóa với GPT-4o, Pinecone & Lovable UI (N8N)**
description: "Workflow này tự động phân tích nhu cầu du lịch của khách hàng qua form Lovable UI, tra cứu dữ liệu tour trong Pinecone Vector DB, và trả về gợi ý tour cá nhân hóa chi tiết bằng GPT-4o. Giúp doanh nghiệp tiết kiệm 80% thời gian tư vấn và tăng trải nghiệm khách hàng lên 30%."
slug: "huong-dan-tour-personalized-n8n"
tags: [n8n, automation, ai-rag, travel-tech, lovable-ui, pinecone, openai]
keywords: [n8n workflow tour du lịch, tự động hóa gợi ý tour, GPT-4o du lịch, Pinecone vector database, Lovable UI, chatbot du lịch]
---

# 🚀 **Tự Động Hóa Gợi Ý Tour Du Lịch Cá Nhân Hóa với AI (N8N)**

## **Nỗi Đau Của Doanh Nghiệp Du Lịch**
Các sếp trong ngành du lịch thường phải:
- **Tư vấn thủ công** cho từng khách hàng, mất thời gian và dễ mắc sai sót.
- **Không có hệ thống gợi ý thông minh**, dẫn đến trải nghiệm khách hàng không đồng nhất.
- **Khó theo dõi xu hướng** của khách hàng từ các form phản hồi truyền thống.

**Workflow này giải quyết tất cả!** Sử dụng **GPT-4o + Pinecone Vector DB**, hệ thống sẽ:
✅ **Hiểu nhu cầu khách hàng** từ form Lovable UI.
✅ **Tra cứu dữ liệu tour** trong vector database Pinecone.
✅ **Trả về gợi ý tour chi tiết** với lịch trình, chi phí, và hình ảnh.
✅ **Hoạt động 24/7** mà không cần nhân viên.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian tư vấn** với khách hàng.
- **Gợi ý tour chính xác** dựa trên nhu cầu cá nhân (địa điểm, ngân sách, sở thích).
- **Tăng trải nghiệm khách hàng** với lịch trình chi tiết, hình ảnh, và gợi ý bổ sung.
- **Hoạt động tự động** mà không cần can thiệp của nhân viên.
- **Kết nối với Lovable UI** để khách hàng dễ dàng tương tác qua form.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản OpenAI** (API Key) để sử dụng GPT-4o và text-embedding-ada-002.
✔ **Tài khoản Pinecone** (API Key và Environment ID) để lưu trữ vector database.
✔ **Form Lovable UI** đã kết nối với webhook của n8n.
✔ **Dữ liệu tour đã vectorize** trong Pinecone (xem [workflow này](https://n8n.io/workflows/5085-convert-tour-pdfs-to-vector-database-using-google-drive-langchain-and-openai) để chuẩn bị dữ liệu).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/6022](https://n8n.io/workflows/6022) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ link trên và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **9 node** chính, các sếp cần chú ý cấu hình sau:

##### **🔹 Node Webhook (n8n-nodes-base.webhook)**
- **URL Webhook:** Được tự động sinh ra khi import. **Không thay đổi!**
- **Method:** POST (đã cấu hình sẵn).
- **Lưu ý:** Đảm bảo **Lovable UI** đã cấu hình webhook này trong form.

##### **🔹 Node Pinecone Vector Store (n8n-nodes-langchain.vectorStorePinecone)**
- **Credentials:** Chọn `pineconeApi` (đã tạo trước khi import).
- **Environment ID:** Điền ID môi trường Pinecone của bạn.
- **Index Name:** Điền tên index chứa dữ liệu tour (ví dụ: `tour-database`).
- **Lưu ý:** Nếu chưa có dữ liệu, **xem workflow này** để chuẩn bị: [Convert Tour PDFs to Vector DB](https://n8n.io/workflows/5085).

##### **🔹 Node OpenAI Chat Model (n8n-nodes-langchain.lmChatOpenAi)**
- **Credentials:** Chọn `openAiApi`.
- **Model:** Đã cấu hình sẵn là `gpt-4o` (không cần thay đổi).
- **API Key:** Đã tự động lấy từ credentials `openAiApi`.

##### **🔹 Node Embeddings OpenAI (n8n-nodes-langchain.embeddingsOpenAi)**
- **Credentials:** Chọn `openAiApi`.
- **Model:** Đã cấu hình sẵn là `text-embedding-ada-002`.
- **Lưu ý:** Nếu OpenAI thay đổi model, cần cập nhật thủ công.

##### **🔹 Node Tour Recommendation AI Agent (n8n-nodes-langchain.agent)**
- **Không cần cấu hình thêm**, vì nó tự động kết nối với các node khác.
- **Lưu ý:** Đảm bảo **Structured Output Parser** (node cuối) trả về JSON đúng định dạng.

##### **🔹 Node Structured Output Parser (n8n-nodes-langchain.outputParserStructured)**
- **Sample Structure:** Đã định sẵn trong workflow, ví dụ:
  ```json
  {
    "itinerary": [
      {
        "dayNumber": 1,
        "date": "2024-07-15",
        "activities": [
          {
            "id": "1",
            "title": "Kuala Lumpur International Airport",
            "description": "Arrival at KLIA",
            "duration": "1 hour",
            "location": "KLIA",
            "type": "transport"
          }
        ]
      }
    ]
  }
  ```
- **Lưu ý:** Nếu Lovable UI không hiểu JSON, cần **cập nhật schema** trong UI.

#### **3. Kích Hoạt ⚡️**
- **Test Run:** Gửi một request mẫu từ Lovable UI (ví dụ: "Tôi muốn tour 3 ngày ở Hà Nội").
- **Kiểm tra kết quả:** Nếu trả về JSON có cấu trúc, workflow hoạt động.
- **Bật Active:** Chuyển workflow sang **Active** để chạy liên tục.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết nối với Slack/Telegram:**
   - Thêm node **Slack/Telegram** sau `Respond to Webhook` để thông báo kết quả cho team.
2. **Lưu Log Dữ Liệu:**
   - Sử dụng node **Google Sheets** hoặc **Airtable** để ghi lại lịch sử gợi ý tour.
3. **Báo Cáo Định Kỳ:**
   - Tạo một workflow riêng để tổng hợp dữ liệu tour được gợi ý nhiều nhất và gửi báo cáo hàng tuần.
4. **Cập Nhật Dữ Liệu Tour:**
   - Sử dụng **Google Drive + LangChain** để tự động cập nhật dữ liệu tour mới vào Pinecone.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp trong ngành du lịch, đồng thời **tăng trải nghiệm khách hàng** với gợi ý tour cá nhân hóa. **Chỉ cần 1 lần setup**, hệ thống sẽ hoạt động tự động 24/7!

**🚀 Hãy áp dụng ngay và xem kết quả trong vòng 1 giờ!**
Nếu có vấn đề, **đăng ký hỗ trợ** từ [n8n Community](https://community.n8n.io/) hoặc liên hệ với tác giả [Mohan Gopal](https://n8n.io/workflows/6022).

---
**💡 Mẹo cuối:** Nếu muốn **tăng tốc độ**, các sếp có thể **upgrade OpenAI API** để giảm thời gian chờ trả lời.