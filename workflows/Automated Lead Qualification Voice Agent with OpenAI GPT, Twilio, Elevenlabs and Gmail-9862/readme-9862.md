---
title: "🤖 **Tự Động Hóa Chuyển Giao Lead Tốt Nhất với AI Voice Agent (OpenAI + Twilio + Gmail) – Không Cần Code!**"
description: "Workflow tự động gọi điện AI, phân loại lead, phân tích cuộc gọi bằng OpenAI, và gửi email tự động từ Google Sheets. Giúp doanh nghiệp tiết kiệm 80% thời gian chăm sóc khách hàng và tăng tỷ lệ chuyển đổi lead lên 30%."
slug: "tự-dộng-hoa-chuyển-giao-lead-voi-ai-voice-agent"
tags: [n8n, automation, no-code, sales-automation, ai-voice-agent, openai, twilio, google-sheets, gmail]
keywords: [n8n workflow tự động gọi điện, AI phân loại lead, tự động hóa bán hàng, Twilio + OpenAI, tự động hóa chăm sóc khách hàng, workflow lead qualification]
---

# 🚀 **Tự Động Hóa Chuyển Giao Lead Tốt Nhất với AI Voice Agent (OpenAI + Twilio + Gmail)**

### **Giải pháp AI gọi điện tự động, phân loại lead và gửi email tự động – Giúp doanh nghiệp tiết kiệm 80% thời gian chăm sóc khách hàng!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động 24/7 mà không bị gián đoạn, các sếp nên **self-host n8n trên VPS** để đảm bảo tính ổn định và bảo mật cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** – Giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (Đảm bảo tốc độ cao cho AI)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 80% thời gian gọi điện thủ công** – AI tự động gọi và phân loại lead.
✅ **Tỷ lệ chuyển đổi lead tăng 30%** – Dựa trên phân tích cuộc gọi bằng OpenAI.
✅ **Chăm sóc khách hàng 24/7** – Workflow hoạt động liên tục, không cần nhân viên trực ca.
✅ **Tự động gửi email follow-up** – Gmail tự động gửi thông tin sau cuộc gọi.
✅ **Dữ liệu lead được cập nhật tự động** – Google Sheets luôn được sync với trạng thái mới nhất.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
📌 **Tài khoản và API Keys:**
- **OpenAI API Key** (để sử dụng AI phân tích cuộc gọi và tạo script gọi điện).
- **Twilio API Key & Account SID** (để gọi điện và xử lý cuộc gọi).
- **ElevenLabs API Key** (để chuyển giọng nói AI, *nếu không dùng Twilio*).
- **Google Sheets OAuth 2.0** (để đọc/ghi dữ liệu lead).
- **Gmail OAuth 2.0** (để gửi email tự động sau cuộc gọi).

📌 **Dữ liệu cần có trong Google Sheets:**
- Cột **Phone Number** (số điện thoại lead).
- Cột **Name** (tên lead).
- Cột **Email** (email lead, *nếu có*).
- Cột **Status** (trạng thái hiện tại: *New, Qualified, Needs Follow-up, Unreachable*).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể **import workflow từ file JSON** hoặc **copy/paste JSON vào n8n Editor**:
1. Tải workflow từ [n8n.io/workflows/9862](https://n8n.io/workflows/9862).
2. Trong **n8n Editor**, nhấn **Import** và chọn file JSON.
3. **Hoặc** copy toàn bộ JSON và paste vào **Import Workflow** trong n8n.

:::note[Lưu ý]
- **Không sử dụng phiên bản n8n Community** nếu muốn sử dụng **Twilio + ElevenLabs** (cần **n8n Enterprise**).
- Nếu dùng **Twilio**, cần **import số điện thoại** vào ElevenLabs và **cấu hình webhook** để xử lý cuộc gọi.
:::

---

### **2. Các bước cấu hình BẮT BUỘC phải chỉnh 📌**

#### **🔹 Node 1: Google Sheets Trigger (Khởi động workflow)**
- **Cấu hình:**
  - Chọn **Google Sheets OAuth 2.0** đã thiết lập trước.
  - Chọn **Sheet** và **Range** (ví dụ: `Sheet1!A:D`).
  - **Trigger Type:** `New row added` (workflow chạy khi có lead mới).
  - **Columns to Watch:** Chọn cột **Phone Number** và **Name**.

#### **🔹 Node 2: Webhook (Xử lý cuộc gọi)**
- **Cấu hình Twilio:**
  - Trong **Twilio Console**, tạo **Webhook URL** từ n8n (ví dụ: `https://your-n8n-domain/webhook/37e8d818-8265-43e9-803e-00119da5f3cb`).
  - Thiết lập **Twilio HTTP Request** trong workflow:
    - **URL:** `https://api.twilio.com/2010-04-01/Accounts/{AccountSid}/Calls.json`
    - **Headers:**
      - `Authorization: Basic {Base64(AccountSid:AuthToken)}`
      - `Content-Type: application/x-www-form-urlencoded`
    - **Body:**
      ```json
      {
        "To": "{{$node["Get row(s) in sheet1"].json[0].Phone Number}}",
        "From": "{{Twilio Phone Number}}",
        "Url": "https://your-n8n-domain/webhook/37e8d818-8265-43e9-803e-00119da5f3cb",
        "Method": "POST"
      }
      ```
  - **Lưu ý:** Nếu dùng **ElevenLabs**, thay thế URL bằng API của ElevenLabs để chuyển giọng nói AI.

#### **🔹 Node 3: OpenAI (Phân tích cuộc gọi & Tạo script gọi điện)**
- **Cấu hình OpenAI:**
  - **Model:** `gpt-4` (hoặc `gpt-3.5-turbo` nếu tiết kiệm chi phí).
  - **Prompt mẫu:**
    ```plaintext
    Bạn là một AI chuyên phân tích cuộc gọi bán hàng. Dựa trên transcript cuộc gọi sau:
    "{{$node["Respond to Webhook"].json.body}}"
    Hãy trả lời:
    1. Lead có quan tâm sản phẩm không? (Yes/No)
    2. Nếu Yes, hãy đánh giá mức độ quan tâm (Low/Medium/High).
    3. Nếu No, lý do gì? (Không cần thiết, Giá cao, Không phù hợp, ...)
    4. Gợi ý script gọi điện tiếp theo (nếu lead chưa quyết định).
    ```
  - **Output Format:** JSON (để dễ xử lý sau).

#### **🔹 Node 4: Update Google Sheets (Cập nhật trạng thái lead)**
- **Cấu hình:**
  - Chọn **Google Sheets OAuth 2.0**.
  - **Operation:** `Append or Update` (cập nhật trạng thái lead).
  - **Columns to Update:**
    - `Status` (ví dụ: `Qualified`, `Needs Follow-up`).
    - `Call Notes` (ghi chú từ AI).
    - `Next Action` (script gọi tiếp theo).

#### **🔹 Node 5: Gmail (Gửi email tự động)**
- **Cấu hình:**
  - Chọn **Gmail OAuth 2.0**.
  - **To:** `{{$node["Get row(s) in sheet1"].json[0].Email}}`
  - **Subject:** `Tóm tắt cuộc gọi với {{$node["Get row(s) in sheet1"].json[0].Name}}`
  - **Body:**
    ```plaintext
    Xin chào {{$node["Get row(s) in sheet1"].json[0].Name}},

    Tóm tắt cuộc gọi:
    - Trạng thái: {{$node["OpenAI"].json.Status}}
    - Gợi ý tiếp theo: {{$node["OpenAI"].json.NextAction}}

    Chúng tôi sẽ liên hệ lại trong {{$node["OpenAI"].json.NextFollowUpTime}}.
    ```

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Thêm một lead vào Google Sheets.
   - Kiểm tra workflow có gọi điện, phân tích và gửi email không.
2. **Bật Active** sau khi kiểm tra thành công.

---

## ✍️ **Mẹo & gợi ý nâng cao**
🔹 **Kết hợp với Slack/Telegram:**
- Thêm **Slack Webhook** để thông báo khi lead được phân loại.
- Ví dụ: `Lead {{Name}} đã được phân loại là {{Status}}!`

🔹 **Lưu log cuộc gọi:**
- Thêm **Google Drive** hoặc **AWS S3** để lưu transcript cuộc gọi lâu dài.

🔹 **Gửi báo cáo định kỳ:**
- Sử dụng **Google Sheets + Apps Script** để tự động gửi báo cáo hàng tuần về lead mới.

🔹 **Tối ưu chi phí Twilio:**
- Sử dụng **Twilio Studio** để giảm chi phí gọi điện vào giờ rẻ.

---

## 📌 **Kết luận**
Workflow này giúp **tự động hóa toàn bộ quy trình chuyển giao lead** từ gọi điện, phân tích, cập nhật đến gửi email follow-up – **không cần code, không cần nhân viên trực ca!**

🚀 **Hành động ngay:**
1. **Import workflow** vào n8n.
2. **Cấu hình Twilio + OpenAI + Gmail**.
3. **Test với 1 lead mẫu**.
4. **Bật Active và bắt đầu tự động hóa!**

**Nếu có vấn đề, hãy để lại comment bên dưới – chúng tôi sẽ hỗ trợ!** 💬