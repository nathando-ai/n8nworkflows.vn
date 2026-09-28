---
title: "🤖 **Tự Động Phân Loại Tình Huống Lead bằng AI Google Gemini & Trả Lời qua WhatsApp (Không Code!)**"
description: "Tự động phân loại lead từ Typeform thành 'nóng', 'trung tính' hoặc 'lạnh' bằng AI Google Gemini, lưu vào Supabase và gửi phản hồi cá nhân hóa qua WhatsApp 24/7. Giúp đội sales tối ưu hóa thời gian và tăng tỷ lệ chuyển đổi!"
slug: "tieu-dong-phan-loai-lead-ai-gemini-whatsapp-supabase"
tags: [n8n, automation, ai, marketing, whatsapp-business, supabase, google-gemini, typeform]
keywords: [tự động hóa lead, phân loại lead bằng ai, whatsapp business api, supabase tự động hóa, google gemini n8n, workflow marketing no-code]
---

# 🚀 **Tự Động Phân Loại Tình Huống Lead bằng AI Google Gemini & Trả Lời qua WhatsApp**

### **Giải pháp cho các sếp:**
Bạn có bao giờ phải mất **giờ đồng hồ** để phân loại hàng trăm lead mỗi ngày? Hay phải lo lắng rằng những lead "nóng" bị "chìm" trong đống tin nhắn trung tính hoặc tiêu cực? **Workflow này sẽ giúp bạn:**
- **Phân loại tự động** lead thành **nóng (hot)**, **trung tính (neutral)**, hoặc **lạnh (cold)** chỉ trong giây lát.
- **Gửi phản hồi cá nhân hóa** qua WhatsApp để tăng tỷ lệ tương tác.
- **Lưu dữ liệu** vào Supabase để phân tích và theo dõi sau này.
- **Tiết kiệm 100% thời gian** của đội sales cho công việc có giá trị cao hơn.

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian:** Không cần phân loại thủ công, AI làm việc 24/7.
✅ **Tăng tỷ lệ chuyển đổi:** Phản hồi nhanh chóng qua WhatsApp giữ lead "nóng".
✅ **Dữ liệu sạch:** Lead được phân loại chính xác và lưu vào Supabase.
✅ **Cá nhân hóa:** Trả lời tự động nhưng vẫn thân thiện và chuyên nghiệp.
✅ **Tối ưu hóa nguồn lực:** Đội sales chỉ tập trung vào lead "nóng" và "trung tính".
:::

---
### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Typeform** (để nhận lead qua webhook).
2. **API Key của Google Gemini** (đăng ký tại [Google AI Studio](https://aistudio.google.com/)).
3. **Tài khoản WhatsApp Business API** (đăng ký tại [Meta Developer](https://developers.facebook.com/)).
4. **Tài khoản Supabase** (để lưu lead phân loại).
5. **Mã Webhook** từ Typeform (để n8n nhận dữ liệu).
6. **Mã WhatsApp Business** (để gửi phản hồi tự động).
:::

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Bước 1:** Tải file JSON của workflow từ [n8n.io/workflows/4322](https://n8n.io/workflows/4322).
- **Bước 2:** Mở **n8n Editor** và chọn **"Import"** → Chọn file JSON vừa tải.
- **Bước 3:** Nếu copy/paste JSON, chọn **"Create from JSON"** trong menu.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình Webhook (Receive New Lead)**
- **Node:** `Receive New Lead (Typeform)`
- **Cấu hình:**
  - **Path:** `lead-webhook` (không đổi).
  - **HTTP Method:** `POST`.
  - **Credentials:** Không cần (n8n sẽ tự động nhận dữ liệu từ Typeform).
  - **Lưu ý:** Trong Typeform, cấu hình **Webhook** để gửi dữ liệu đến URL:
    ```
    https://[tên-domain-n8n].n8n.io/lead-webhook
    ```
    (Thay `[tên-domain-n8n]` bằng domain của bạn).

##### **B. Cấu hình Google Gemini (Phân loại Tình Huống)**
- **Node:** `Google Gemini Chat Model`
- **Cấu hình:**
  - **API Key:** Điền vào **Credentials** của node này (tạo mới trong n8n với tên `googleGeminiApi`).
  - **Prompt:** Sử dụng **Prompt mặc định** từ tác giả:
    ```
    Classify the sentiment of the message below as Positive, Neutral or Negative:
    "{{$json["message"]}}"
    ```
  - **Lưu ý:** Nếu muốn cải tiến, có thể thêm yêu cầu cụ thể như:
    ```
    Return the result in JSON format: {"sentiment": "Positive/Neutral/Negative", "confidence": 0.9}
    ```

##### **C. Cấu hình Supabase (Lưu Lead)**
- **Nodes:** `Store Hot Lead`, `Store Neutral Lead`, `Store Cold Lead`
- **Cấu hình chung:**
  - **Credentials:** Sử dụng `supabaseApi` (tạo mới trong n8n).
  - **Table Name:** Điền tên bảng tương ứng trong Supabase (ví dụ: `hot_leads`, `neutral_leads`, `cold_leads`).
  - **Columns:** Chọn các cột cần lưu (ví dụ: `id`, `message`, `sentiment`, `created_at`).
  - **Lưu ý:**
    - Đảm bảo **table** đã tồn tại trong Supabase với cấu trúc phù hợp.
    - Nếu muốn thêm trường `sentiment`, tạo cột mới với kiểu dữ liệu `text` hoặc `varchar`.

##### **D. Cấu hình WhatsApp (Gửi Trả Lời)**
- **Node:** `Send WhatsApp Message`
- **Cấu hình:**
  - **Credentials:** Điền `whatsappApi` (tạo mới trong n8n).
  - **Phone Number:** Điền số điện thoại WhatsApp Business (ví dụ: `843xxxxxx`).
  - **Message Template:** Sử dụng template cá nhân hóa như:
    ```
    Xin chào! Tôi là [Tên Bot], cảm ơn bạn đã liên hệ. Tình huống của bạn đã được phân loại là **{{$json["sentiment"]}}**. Chúng tôi sẽ liên hệ lại trong vòng 24 giờ. Nếu cần hỗ trợ ngay, hãy nhắn tin "HỖ TRỢ"!
    ```
  - **Lưu ý:**
    - Đảm bảo **WhatsApp Business API** đã được kích hoạt và có số điện thoại hợp lệ.
    - Nếu muốn gửi tin nhắn khác nhau cho từng loại lead, sử dụng **node `Set`** để điều khiển.

##### **E. Cấu hình Node `Combine Lead Data`**
- **Node:** `Combine Lead Data` (type: `merge`)
- **Cấu hình:**
  - Chọn **input** từ node `Prepare Lead Data` và kết quả từ `Google Gemini Chat Model`.
  - **Lưu ý:** Node này kết hợp dữ liệu để tạo ra một JSON hoàn chỉnh trước khi gửi WhatsApp.

---
#### **3. Kích hoạt ⚡️**
- **Bước 1:** **Test Run** với dữ liệu mẫu:
  - Gửi một lead mẫu từ Typeform (hoặc sử dụng **n8n Test Tab**).
  - Kiểm tra:
    - Lead có được phân loại chính xác không?
    - Tin nhắn WhatsApp có được gửi không?
    - Dữ liệu có được lưu vào Supabase không?
- **Bước 2:** Nếu test thành công, **bật Active** workflow.

---
### ✍️ **Mẹo & gợi ý nâng cao**
:::info[CẢI TIẾN & MỞ RỘNG]
1. **Thêm Slack/Telegram Notifications:**
   - Sử dụng node `slack` hoặc `telegram` để thông báo khi có lead "nóng" mới.
   - Ví dụ: Khi lead có `sentiment = "Positive"`, gửi tin nhắn Slack:
     ```
     🚨 **New Hot Lead!** 🚨
     Message: {{json["message"]}}
     Phone: {{json["phone"]}}
     ```

2. **Lưu Log vào Google Sheets:**
   - Thêm node `googleSheets` sau `Store Hot Lead` để ghi lại tất cả hoạt động.
   - Cấu hình để tự động cập nhật bảng theo dõi lead.

3. **Tự động Gửi Email cho Lead "Nóng":**
   - Sử dụng node `email` (ví dụ: Gmail) để gửi email xác nhận cho lead "nóng".
   - Ví dụ:
     ```
     Chào [Tên],
     Tình huống của bạn đã được phân loại là **nóng** và chúng tôi sẽ liên hệ trong 1 giờ.
     ```

4. **Cải tiến Prompt cho Gemini:**
   - Thêm yêu cầu cụ thể như:
     ```
     Classify sentiment as Positive (0.7+ confidence), Neutral (0.4-0.69), or Negative (<0.4).
     Also extract keywords like "urgent", "problem", or "question" if present.
     ```

5. **Sử dụng Supabase để Trả Lời Lead:**
   - Thay vì chỉ lưu lead, có thể thêm logic để **trả lời tự động** từ Supabase.
   - Ví dụ: Khi lead "nóng" được lưu, tự động gửi tin nhắn WhatsApp từ một danh sách câu trả lời sẵn có.
:::

---
### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa quy trình phân loại lead**, **tăng tỷ lệ chuyển đổi** và **tối ưu hóa thời gian** của đội sales. Với **Google Gemini**, lead được phân loại chính xác; **Supabase** lưu trữ dữ liệu sạch; và **WhatsApp Business API** đảm bảo phản hồi nhanh chóng.

**Hành động ngay:**
1. **Cài đặt n8n trên VPS** (Self-hosted) để workflow hoạt động 24/7.
2. **Import workflow** và cấu hình theo hướng dẫn trên.
3. **Test và bật Active** để bắt đầu tự động hóa!

---
:::success[💡 **Lời khuyên cuối cùng**]
Nếu gặp khó khăn trong quá trình cấu hình, hãy tham khảo:
- [Hướng dẫn cài đặt WhatsApp Business API](https://developers.facebook.com/docs/whatsapp/cloud-api/get-started)
- [Tutorial Supabase cơ bản](https://supabase.com/docs)
- [Cách sử dụng Google Gemini trong n8n](https://n8n.io/docs/integrations/nodes/n8n-nodes-base.lmChatGoogleGemini)

**Chúc các sếp thành công!** 🚀