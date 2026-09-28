---
title: "🚀 Tự Động Hóa Xác Minh Lead Bảo Hiểm với Vapi, GPT-4 & Airtable - Giảm Thời Gian Chuyển Dổi Lead 90%"
description: "Workflow tự động hóa 100% không code giúp doanh nghiệp bảo hiểm gọi điện AI tự động, phân tích lead, tạo đề xuất bảo hiểm cá nhân hóa bằng GPT-4 và gửi email tự động - giảm thời gian xử lý lead từ 24h xuống dưới 1h."
slug: "tu-dong-hoa-xac-minh-lead-bao-hiem-voi-vapi-gpt4-airtable"
tags: [n8n, automation, no-code, lead-generation, ai-chatbot, insurance, gpt-4, airtable, vapi]
keywords: [n8n workflow bảo hiểm, tự động hóa lead bảo hiểm, gọi điện AI tự động, GPT-4 tạo đề xuất bảo hiểm, Airtable quản lý lead, giảm thời gian chuyển đổi lead]
---

# 🚀 **Tự Động Hóa Xác Minh Lead Bảo Hiểm với Vapi + GPT-4 + Airtable**

## **Giải pháp cho doanh nghiệp bảo hiểm: Giảm thời gian xử lý lead từ 24h xuống dưới 1h!**

Hiện nay, các doanh nghiệp bảo hiểm thường gặp khó khăn khi phải **tự gọi điện, thu thập thông tin lead thủ công** và sau đó phải **tạo đề xuất bảo hiểm cá nhân hóa** bằng tay. Quá trình này tốn thời gian, dễ sai sót và làm giảm hiệu quả chuyển đổi lead.

**Workflow này tự động hóa toàn bộ quy trình:**
✅ **Gọi điện AI tự động** (Vapi) để thu thập thông tin chi tiết từ lead.
✅ **Xác minh lead** dựa trên yêu cầu bảo hiểm (đã mua hay chưa).
✅ **Tạo đề xuất bảo hiểm cá nhân hóa** bằng GPT-4 (nếu lead hợp lệ).
✅ **Gửi email tự động** đề xuất đến khách hàng.
✅ **Cập nhật Airtable** và thông báo Slack cho team khi lead không hợp lệ.

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian** trong việc gọi điện và phân tích lead.
- **Tăng tỷ lệ chuyển đổi lead** nhờ đề xuất bảo hiểm cá nhân hóa.
- **Giảm sai sót** khi thu thập và phân tích thông tin.
- **Hoạt động 24/7** mà không cần nhân viên theo dõi.
- **Tối ưu chi phí** bằng cách loại bỏ lead không hợp lệ sớm.
:::

---
### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
✔ **Tài khoản Vapi** (để gọi điện AI tự động).
✔ **Tài khoản OpenAI (GPT-4)** (để tạo đề xuất bảo hiểm).
✔ **Airtable** (để lưu trữ và quản lý lead).
✔ **Gmail** (để gửi đề xuất bảo hiểm cho khách hàng).
✔ **Slack** (để thông báo lead không hợp lệ hoặc lỗi hệ thống).
✔ **API Key** của các dịch vụ trên (n8n sẽ yêu cầu khi cấu hình).
:::

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/11794](https://n8n.io/workflows/11794) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON và chọn **"Import"**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **12 node chính**, các sếp cần chú ý cấu hình như sau:

##### **🔹 Node "On form submission" (formTrigger)**
- **Cấu hình form** trên trang web hoặc Google Form để bắt đầu workflow.
- **Tham số cần điền:**
  - `Name`, `Email`, `Phone` (cần phải có trong form).

##### **🔹 Node "Create a record" (Airtable)**
- **Chọn credentials:** `airtableTokenApi`
- **Cấu hình:**
  - **Table Name:** Chọn bảng lưu lead (ví dụ: "Insurance Leads").
  - **Fields:** Đảm bảo có các trường `Name`, `Email`, `Phone`, `Status` (Default: "Unqualified").

##### **🔹 Node "Vapi call" (httpRequest)**
- **Chọn credentials:** `httpBasicAuth` (đăng ký API key trên Vapi).
- **Cấu hình:**
  - **URL:** `https://api.vapi.ai/v1/calls` (hoặc URL chính thức của Vapi).
  - **Headers:**
    ```json
    {
      "Authorization": "Bearer YOUR_VAPI_API_KEY",
      "Content-Type": "application/json"
    }
    ```
  - **Body (JSON):**
    ```json
    {
      "phone": "{{$node["On form submission"].json["phone"]}}",
      "message": "Xin chào, tôi là AI của công ty bảo hiểm. Vui lòng cho tôi biết loại bảo hiểm bạn quan tâm?",
      "language": "vi"
    }
    ```

##### **🔹 Node "Post call" (webhook)**
- **Chọn credentials:** Không cần (sử dụng path mặc định).
- **Path:** `cf226daa-a404-4c24-a44a-33526891e5f2` (được cung cấp trong workflow gốc).
- **HTTP Method:** `POST`.

##### **🔹 Node "Is Qualified?" (if)**
- **Cấu hình điều kiện:**
  - Nếu `Type of Insurance` (trong response từ Vapi) **không rỗng** → Lead **hợp lệ**.
  - Nếu rỗng → Lead **không hợp lệ**.

##### **🔹 Node "Prepare Blueprint" (OpenAI)**
- **Chọn credentials:** `openAiApi`
- **Cấu hình:**
  - **Model:** `gpt-4` (hoặc `gpt-4-turbo` nếu có).
  - **Prompt (tham khảo):**
    ```text
    Tôi là AI của công ty bảo hiểm. Hãy tạo một đề xuất bảo hiểm chi tiết cho khách hàng {{$node["On form submission"].json["name"]}} với yêu cầu là {{$node["Vapi call"].json["type_of_insurance"]}}. Đề xuất phải bao gồm:
    1. Loại bảo hiểm (ví dụ: Bảo hiểm sức khỏe, tài sản, ô tô).
    2. Mức bảo hiểm (tối thiểu 500 triệu VND).
    3. Các điều kiện và lợi ích.
    4. Giới thiệu công ty và dịch vụ hỗ trợ.
    ```
  - **Temperature:** `0.7` (để kết quả sáng tạo nhưng logic).

##### **🔹 Node "Send a message" (Gmail)**
- **Chọn credentials:** `gmailOAuth2`
- **Cấu hình:**
  - **To:** `{{$node["On form submission"].json["email"]}}`
  - **Subject:** `Đề xuất bảo hiểm cá nhân hóa cho bạn`
  - **Body (HTML):**
    ```html
    <p>Xin chào {{$node["On form submission"].json["name"]}},</p>
    <p>Dưới đây là đề xuất bảo hiểm chi tiết dành riêng cho bạn:</p>
    <p>{{$node["Prepare Blueprint"].json["content"]}}</p>
    <p>Chúng tôi sẵn sàng hỗ trợ nếu bạn có bất kỳ câu hỏi nào!</p>
    ```

##### **🔹 Node "Send a message1" (Slack) - Cho lead không hợp lệ**
- **Chọn credentials:** `slackOAuth2Api`
- **Cấu hình:**
  - **Channel:** `#insurance-leads` (hoặc channel tùy chỉnh).
  - **Message:**
    ```text
    *Lead không hợp lệ:* {{$node["On form submission"].json["name"]}} (Email: {{$node["On form submission"].json["email"]}})
    *Lý do:* Không cung cấp loại bảo hiểm cụ thể.
    ```

##### **🔹 Node "Error Handling" (Slack) - Cho lỗi hệ thống**
- **Chọn credentials:** `slackOAuth2Api`
- **Cấu hình:**
  - **Channel:** `#system-errors`
  - **Message:**
    ```text
    *Lỗi trong workflow:* {{$node["Prepare Blueprint"].error}}
    *Lead:* {{$node["On form submission"].json["name"]}}
    ```

---
### ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
- **Kết hợp với CRM khác:** Nếu sử dụng HubSpot hoặc Salesforce, thay thế Airtable bằng node tương ứng.
- **Lưu log chi tiết:** Sử dụng node **StickyNote** để lưu lại toàn bộ lịch sử cuộc gọi và phản hồi của lead.
- **Gửi báo cáo định kỳ:** Tạo một workflow riêng để tổng hợp số liệu lead hợp lệ/không hợp lệ và gửi báo cáo hàng tuần qua email.
- **Tối ưu GPT-4:** Đặt **system prompt** cụ thể hơn để đề xuất bảo hiểm phù hợp với từng loại khách hàng (ví dụ: doanh nghiệp vs cá nhân).
- **Thông báo SMS:** Sử dụng node **Twilio** để gửi tin nhắn xác nhận đề xuất đã được gửi.
:::

---
### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho team marketing và sales bằng cách tự động hóa toàn bộ quy trình từ **gọi điện AI** đến **tạo đề xuất bảo hiểm cá nhân hóa**. Các sếp chỉ cần **cấu hình 1 lần**, workflow sẽ hoạt động **24/7** mà không cần can thiệp.

**🚀 Hãy áp dụng ngay và giảm thời gian chuyển đổi lead xuống dưới 1h!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::