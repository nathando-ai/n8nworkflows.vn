---
title: "🤖 **Tự Động Hóa & Phân Tích Phản Hồi Khách Hàng với AI Qwen3-VL + Tally + PostgreSQL (N8n Workflow)**
description: "Workflow tự động hóa hoàn chỉnh để thu thập, phân tích cảm xúc, phân loại và phân phối phản hồi khách hàng từ Tally.so sang Discord thông qua AI Qwen3-VL, tiết kiệm 80% thời gian phân tích thủ công và cải thiện chất lượng dịch vụ 24/7."
slug: "tu-dong-hoa-phan-tich-phan-hoi-khach-hang-ai-qwen3-vl"
tags: [n8n, automation, ai-chatbot, postgresql, tally-so, discord-bot, qwen3-vl, no-code]
keywords: [n8n workflow phân tích phản hồi, tự động hóa phản hồi khách hàng, ai phân loại cảm xúc, qwen3-vl n8n, tích hợp tally.so discord, lưu trữ phản hồi postgresql]
---

# 🚀 **Tự Động Hóa & Phân Tích Phản Hồi Khách Hàng với AI Qwen3-VL, Tally.so và PostgreSQL**

### **📌 Nỗi Đau Của Các Sếp**
Các sếp thường phải:
- **Tốn thời gian** để thu thập phản hồi từ nhiều kênh (form Tally.so, email, chatbot).
- **Phân tích thủ công** cảm xúc và nội dung phản hồi, dẫn đến sai sót và mất thời gian.
- **Không biết cách phân loại** phản hồi để chuyển giao cho đội ngũ phù hợp (chăm sóc khách hàng, marketing, kỹ thuật).
- **Không có hệ thống lưu trữ** để theo dõi lịch sử phản hồi và rút kinh nghiệm.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Thu thập phản hồi** từ Tally.so (hoặc form khác).
✅ **Phân tích cảm xúc** và **phân loại nội dung** bằng AI Qwen3-VL (hỗ trợ cả hình ảnh và văn bản).
✅ **Lưu trữ dữ liệu** vào PostgreSQL để theo dõi và phân tích dài hạn.
✅ **Phân phối tự động** phản hồi sang Discord (hoặc Slack) theo nhóm (chăm sóc khách hàng, phản hồi tích cực, hỗ trợ ưu tiên).

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
- **Tiết kiệm 80% thời gian** phân tích phản hồi thủ công.
- **Chính xác cao** với AI phân tích cảm xúc và phân loại tự động.
- **Cá nhân hóa phản hồi** bằng cách phân loại vào các kênh Discord/Slack phù hợp.
- **Lưu trữ dữ liệu** để phân tích xu hướng và cải thiện dịch vụ.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
:::info[**Chuẩn Bị Trước Khi Bắt Đầu**]
Để workflow hoạt động, các sếp cần:
1. **Tài Khoản & API Keys**:
   - **Tally.so**: API Key để kết nối với form phản hồi.
   - **PostgreSQL**: Credentials để lưu trữ dữ liệu (tên database, tên table, user, password).
   - **Discord Bot**: Token Bot và ID của các kênh `#general-inquiries`, `#happy-customers`, `#support-urgent`.
   - **LM Studio (Local AI)**: Cài đặt và chạy `Qwen3-VL` trên máy chủ hoặc Docker (cấu hình cổng `1234`).
   - **OpenAI API (nếu không dùng local)**: API Key (nếu không sử dụng LM Studio).

2. **Cấu Trúc Database PostgreSQL**:
   - Table tên `customer_feedback` với các cột:
     ```sql
     CREATE TABLE customer_feedback (
         id SERIAL PRIMARY KEY,
         name VARCHAR(255),
         email VARCHAR(255),
         feedback TEXT,
         sentiment VARCHAR(50),
         category VARCHAR(100),
         keywords TEXT[],
         created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
     );
     ```

3. **LM Studio (Nếu Sử Dụng Local AI)**:
   - Cài đặt [LM Studio](https://lmstudio.ai/) và tải mô hình `Qwen3-VL`.
   - Chạy server trên cổng `1234` và sử dụng IP máy chủ (không dùng `localhost` trong Docker).
   - Ví dụ: `http://192.168.1.100:1234/v1`.
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương Pháp 1: Từ File JSON**
1. Tải workflow từ [n8n.io/workflows/13314](https://n8n.io/workflows/13314) (ấn "Export").
2. Trong n8n Editor, nhấn **"Import"** và chọn file JSON.
3. Chọn **"Create a new workflow"** và nhấn **"Import"**.

#### **Phương Pháp 2: Copy/Paste JSON**
1. Copy toàn bộ mã JSON từ [n8n.io/workflows/13314](https://n8n.io/workflows/13314).
2. Trong n8n Editor, nhấn **"Import"** → **"Paste JSON"** và dán mã.
3. Chọn **"Create a new workflow"** và nhấn **"Import"**.

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **26 node** phức tạp, nhưng chỉ cần chú ý đến các node sau:

#### **🔹 Node "Tally Trigger" (n8n-nodes-tallyforms.tallyTrigger)**
- **Cấu hình**:
  - Chọn **credentials**: `tallyApi`.
  - Điền **URL Webhook** của form Tally.so (cần tạo trước ở Tally.so → Settings → Webhooks).
  - **Field Mapping**: Đảm bảo các trường `name`, `email`, `feedback` và `image` (nếu có) được map chính xác.

#### **🔹 Node "Routing LLM" & "Sentiment LLM" (lmChatOpenAi)**
- **Cấu hình**:
  - Chọn **credentials**: `openAiApi` (nếu dùng OpenAI) hoặc **local IP** (nếu dùng LM Studio).
  - **Model**: Chọn `qwen/qwen3-vl-4b` (đã được cache trong workflow).
  - **Prompt**: Không cần chỉnh sửa (đã tối ưu sẵn).
  - **URL API**: Nếu dùng local, điền `http://<IP_MÁY_CHỦ>:1234/v1`.

#### **🔹 Node "PostgreSQL" (postgres)**
- **Cấu hình**:
  - Chọn **credentials**: `postgres`.
  - **Database**: Tên database của bạn.
  - **Table**: `customer_feedback`.
  - **Query**: Workflow sẽ tự động tạo query INSERT với các cột `name`, `email`, `feedback`, `sentiment`, `category`, `keywords`.

#### **🔹 Node "Discord" (discord)**
- **Cấu hình**:
  - Chọn **credentials**: `discordBotApi`.
  - **Channel IDs**:
    - `#general-inquiries`: ID của kênh phản hồi chung.
    - `#happy-customers`: ID của kênh phản hồi tích cực.
    - `#support-urgent`: ID của kênh hỗ trợ ưu tiên.
  - **Format Embed**: Workflow sẽ tự động tạo embed với thông tin phản hồi.

#### **🔹 Node "Image Keyword Extraction" (code)**
- **Lưu ý**:
  - Node này xử lý hình ảnh (nếu có) trong phản hồi.
  - Nếu không có hình ảnh, node sẽ bỏ qua và chuyển sang node tiếp theo.

#### **🔹 Node "Channel Router" (switch)**
- **Cấu hình**:
  - Đảm bảo các **branch** (`#general-inquiries`, `#happy-customers`, `#support-urgent`) được map đúng với logic phân loại từ AI.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **"Run Workflow"** và gửi một phản hồi mẫu từ form Tally.so.
   - Kiểm tra:
     - Phản hồi có được lưu vào PostgreSQL không?
     - Phản hồi có được phân loại và gửi đến Discord đúng kênh không?

2. **Bật Active**:
   - Sau khi test thành công, nhấn **"Active"** để workflow chạy tự động khi có phản hồi mới.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[**Tối Ưu Hóa Workflow**]
1. **Thêm Logs & Monitoring**:
   - Sử dụng node **StickyNote** để ghi chú các lỗi hoặc cảnh báo.
   - Kết nối với **Google Sheets** hoặc **Airtable** để theo dõi lịch sử phản hồi.

2. **Phân Tích Dữ Liệu**:
   - Sử dụng **PostgreSQL** kết hợp với **pgAdmin** hoặc **Metabase** để tạo báo cáo thống kê về cảm xúc và phân loại phản hồi.

3. **Kết Nối Slack Thay Vì Discord**:
   - Thay node **Discord** bằng node **Slack** (`n8n-nodes-base.slack`) để phân phối phản hồi sang Slack.

4. **Tự Động Gửi Email**:
   - Sử dụng node **Email** (`n8n-nodes-base.email`) để gửi báo cáo tuần/month cho team.

5. **Cập Nhật Prompt AI**:
   - Nếu muốn AI phân tích khác, chỉnh sửa **prompt** trong node `Sentiment Analysis` hoặc `Text Classification`.

6. **Backup Database**:
   - Đặt lịch **backup** định kỳ cho PostgreSQL để tránh mất dữ liệu.
:::

---

## 📌 **Kết Luận**
Workflow này là **giải pháp hoàn chỉnh** để tự động hóa quá trình thu thập, phân tích và phân phối phản hồi khách hàng. Các sếp sẽ:
✔ **Tiết kiệm thời gian** với AI phân tích tự động.
✔ **Cải thiện chất lượng dịch vụ** bằng cách phân loại phản hồi chính xác.
✔ **Theo dõi dữ liệu dài hạn** để rút kinh nghiệm.

**🚀 Hãy áp dụng ngay và bắt đầu tự động hóa phản hồi khách hàng của bạn!**

---
:::info[**Gợi Ý Hạ Tầng Cho n8n**]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💡 Cần hỗ trợ thêm?** Hãy để lại comment hoặc liên hệ với tác giả [Neloy Barman](https://n8n.io/workflows/13314) để được tư vấn chi tiết!