---
title: "🤖 Tự Động Tóm Tắt & Đánh Dấu AI Cho Notion: Giảm 80% Thời Gian Làm Báo Cáo"
description: "Workflow này tự động tóm tắt nội dung từ các trang Notion và gán nhãn AI, giúp các sếp tiết kiệm thời gian và cải thiện tổ chức thông tin. Hoàn toàn không cần code!"
slug: "tieu-dong-tom-tat-notion-ai"
tags: [n8n, automation, ai, notion, no-code, langchain]
keywords: [n8n workflow notion, tự động hóa notion, tóm tắt ai, đánh dấu tự động, langchain n8n]
---

# 🚀 **Tự Động Tóm Tắt & Đánh Dấu AI Cho Notion: Giảm 80% Thời Gian Làm Báo Cáo**

### **Nỗi Đau Của Các Sếp**
Hàng ngày, các sếp phải mất **giờ đồng hồ** để:
- Đọc và tóm tắt nội dung từ các trang Notion dài dòng.
- Đánh dấu (tags) để phân loại thông tin theo chủ đề, ưu tiên hoặc dự án.
- Cập nhật lại các trang sau khi đã xử lý.

Kết quả? **Thông tin rối loạn, mất thời gian, và hiệu suất giảm sút.** Giải pháp? **Workflow này tự động hóa toàn bộ quy trình bằng AI!**

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 80% thời gian** trong việc tóm tắt và đánh dấu.
✅ **Tóm tắt chính xác** nhờ AI (gpt-4o-mini) hiểu ngữ cảnh.
✅ **Đánh dấu tự động** theo chủ đề, ưu tiên hoặc từ khóa.
✅ **Hoạt động liên tục** 24/7, không cần can thiệp thủ công.
✅ **Cập nhật Notion tự động**, giữ thông tin luôn mới nhất.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Notion** (để kết nối và cập nhật dữ liệu).
2. **API Key OpenAI** (để sử dụng mô hình AI `gpt-4o-mini`).
3. **Database Notion** (cần có trang hoặc database để lưu trữ kết quả).
4. **Webhook Notion** (để workflow được kích hoạt khi có thay đổi).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/4431).
- Mở **n8n Editor** → Nhấn **"Import"** → Chọn file JSON.
- **Hoặc** copy toàn bộ JSON vào ô **"Import Workflow"** và nhấn **"Import"**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này hoạt động theo **6 node chính**, các sếp cần chú ý cấu hình như sau:

##### **🔹 Node 1: Notion Trigger (n8n-nodes-base.notionTrigger)**
- **Chọn "Database"** (không phải trang).
- **Chọn "Property"** (cột) để theo dõi thay đổi (ví dụ: `Last Edited Time`).
- **Lưu ý:** Workflow sẽ kích hoạt khi có thay đổi trong database.

##### **🔹 Node 2: AI Agent (n8n-nodes-langchain.agent)**
- **Không cần cấu hình thêm** (n8n sẽ tự động sử dụng mô hình AI đã chỉ định).

##### **🔹 Node 3: OpenAI Chat Model (n8n-nodes-langchain.lmChatOpenAi)**
- **Chọn mô hình:** `gpt-4o-mini` (đã được cài đặt sẵn).
- **Điền API Key OpenAI** vào **"OpenAI API Key"** (tìm tại [OpenAI Dashboard](https://platform.openai.com/account/api-keys)).
- **Prompt mẫu** (nếu cần chỉnh sửa):
  ```plaintext
  Tóm tắt nội dung trang Notion này thành 3 câu ngắn gọn. Sau đó, gán 3 nhãn (tags) phù hợp với chủ đề.
  ```

##### **🔹 Node 4: HTTP Request (n8n-nodes-base.httpRequest)**
- **Không cần chỉnh sửa** (n8n sẽ tự động xử lý yêu cầu API).

##### **🔹 Node 5: Code (n8n-nodes-base.code)**
- **Mã JavaScript mặc định** đã xử lý dữ liệu từ AI và chuẩn bị cho bước cập nhật Notion.
- **Không cần chỉnh sửa** (nếu không biết code).

##### **🔹 Node 6: Notion (n8n-nodes-base.notion)**
- **Chọn "Update"** (để cập nhật trang Notion).
- **Chọn database/trang** cần cập nhật.
- **Điền thông tin:**
  - **Property** để cập nhật:
    - `Summary` (tóm tắt từ AI).
    - `Tags` (nhãn từ AI).
  - **Lưu ý:** Đảm bảo các cột này đã tồn tại trong database Notion.

#### **3. Kích Hoạt ⚡️**
- **Test Run:** Nhấn **"Run Workflow"** với một trang mẫu để kiểm tra kết quả.
- **Bật Active:** Sau khi kiểm tra thành công, nhấn **"Active"** để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**
   - Thêm node **Slack/Telegram** để thông báo khi có tóm tắt mới.
   - Cách làm: Sau node **Notion**, thêm node **Slack** với nội dung:
     ```plaintext
     "Tóm tắt mới cho trang: {{$node["Notion"].json["title"]}}
     Tóm tắt: {{$node["Code"].json["summary"]}}
     Nhãn: {{$node["Code"].json["tags"]}}"
     ```

2. **Lưu Log Cho Dữ Liệu**
   - Thêm node **Google Sheets** hoặc **Airtable** để lưu lịch sử tóm tắt.
   - Cách làm: Sau node **Code**, thêm node **Google Sheets** với dữ liệu:
     ```json
     {
       "title": "{{$node["Notion"].json["title"]}}",
       "summary": "{{$node["Code"].json["summary"]}}",
       "tags": "{{$node["Code"].json["tags"]}}",
       "date": "{{$node["Notion Trigger"].json["lastEditedTime"]}}"
     }
     ```

3. **Tự Động Gửi Báo Cáo Định Kỳ**
   - Sử dụng **n8n Cron Trigger** để chạy workflow hàng ngày/tuần.
   - Cách làm: Thêm node **Cron Trigger** trước **Notion Trigger** với lịch:
     ```plaintext
     0 9 * * *  # Làm vào 9h sáng hàng ngày
     ```

4. **Cải Thiện Prompt AI**
   - Nếu kết quả tóm tắt không tốt, chỉnh sửa **prompt** trong node **OpenAI Chat Model**:
     ```plaintext
     Tóm tắt nội dung trang Notion này thành 2-3 câu ngắn gọn, nhấn mạnh điểm chính.
     Sau đó, gán 3 nhãn (tags) theo chủ đề: [Tech, Marketing, Finance, Project].
     Nếu không xác định được chủ đề, gán nhãn "Uncategorized".
     ```

---

### 📌 **Kết Luận**
Workflow **Notion AI Summary & Tags** là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Tiết kiệm thời gian** trong việc tóm tắt và đánh dấu.
✔ **Giảm sai sót** nhờ AI hiểu ngữ cảnh.
✔ **Hoạt động tự động** 24/7, không cần can thiệp.

**Hành động ngay!**
1. **Import workflow** từ [đây](https://n8n.io/workflows/4431).
2. **Cấu hình API Key OpenAI** và kết nối Notion.
3. **Bật Active** và bắt đầu tự động hóa!

**Cần hỗ trợ?** Để lại comment bên dưới hoặc liên hệ với tác giả [Parnain](https://n8n.io/workflows/4431) để được tư vấn chi tiết! 🚀