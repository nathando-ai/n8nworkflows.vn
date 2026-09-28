---
title: "🚀 Tự Động Hóa Chăm Sóc Lead AI Cho Công Ty Tư Vấn Marketing - Google Gemini + Outlook + Sheets"
description: "Workflow tự động hóa 100% không code giúp công ty tư vấn marketing tự động chăm sóc lead từ form đăng ký, chỉnh sửa hình ảnh AI, gửi email cá nhân hóa và theo dõi phản hồi tự động. Giúp tiết kiệm 80% thời gian chăm sóc lead thủ công."
slug: "tieu-dong-hoa-cham-soc-lead-ai-google-gemini-outlook-sheets"
tags: [n8n, automation, lead nurturing, ai-chatbot, google-gemini, microsoft-outlook, google-sheets]
keywords: [tự động hóa lead nurturing, workflow n8n ai, chatbot google gemini, tự động gửi email cá nhân hóa, chăm sóc lead không code]
---

# 🚀 **Tự Động Hóa Chăm Sóc Lead AI Cho Công Ty Tư Vấn Marketing**

Hiện nay, các công ty tư vấn marketing phải mất hàng giờ mỗi ngày để chăm sóc lead thủ công: gửi email cá nhân hóa, chỉnh sửa hình ảnh, theo dõi phản hồi và cập nhật trạng thái. **Workflow này tự động hóa toàn bộ quy trình đó chỉ trong 15 phút thiết lập!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian chăm sóc lead**: AI tự động viết email, chỉnh sửa hình ảnh và theo dõi phản hồi.
- **Email cá nhân hóa 100%**: Dựa trên mô tả hình ảnh và thông tin công ty của lead.
- **Tự động phân loại lead**: Tag "Interested" cho lead đã phản hồi, tự động gửi follow-up cho lead chưa phản hồi.
- **Hoạt động 24/7**: Không cần can thiệp thủ công, hệ thống chạy tự động sau khi thiết lập.
- **Tăng tỷ lệ chuyển đổi**: Email AI viết có độ chuyên nghiệp cao hơn so với email thủ công.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
- **Tài khoản Google Cloud** (để sử dụng **Google Gemini API**).
- **Tài khoản Microsoft 365** (để kết nối **Outlook**).
- **Google Sheets** (để lưu trữ lead với các cột: **Name, Company, Email, Time, Status**).
- **Link lịch hẹn** (ví dụ: [Calendly](https://cal.com/)).
- **Danh sách ý tưởng tự động hóa** (cập nhật trong node **"Automation Ideas Library"**).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/11616](https://n8n.io/workflows/11616) và import vào **n8n Editor**.
- **Hoặc** copy toàn bộ JSON từ file và dán vào **Import Workflow** trong n8n.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Node "Property Photo Upload Form" (formTrigger)**
- **Không cần cấu hình**: Node này chỉ bắt đầu workflow khi lead gửi form.

#### **🔹 Node "Edit an image" (googleGemini)**
- **Cần thiết**: Cập nhật **Google Palm API Key** trong **Credentials**.
- **Prompt chỉnh sửa hình ảnh**:
  ```plaintext
  =BASED OFF OF THIS DESCRIPTION, EDIT THE IMAGE: {{ $json['Description:'] }}
  KEEP CAMERA ANGLE AND LIGHTING THE SAME UNLESS SPECIFIED ABOVE
  ```
- **Lưu ý**: Nếu hình ảnh không được chỉnh sửa, kiểm tra **API Key** và **thông tin input** từ form.

#### **🔹 Node "Send a message" (microsoftOutlook)**
- **Cần thiết**: Kết nối **Outlook OAuth2** trong **Credentials**.
- **Email mẫu**: Cập nhật **signature** và **link lịch hẹn** (ví dụ: `https://cal.com/quartersmart/intro`).

#### **🔹 Node "Append or update row in sheet" (googleSheets)**
- **Cần thiết**: Kết nối **Google Sheets OAuth2** và chọn **Sheet Name**.
- **Cột bắt buộc**: **Name, Company, Email, Time, Status**.

#### **🔹 Node "AI Sales Agent - Idea Picker & Email Writer" (agent)**
- **Cần thiết**: Cập nhật **Automation Ideas Library** (node **"Automation Ideas Library"**).
- **Ví dụ**:
  ```json
  [
    "Suggest a free audit for their website",
    "Offer a 15-minute consultation call",
    "Share a case study relevant to their industry"
  ]
  ```

#### **🔹 Node "Google Gemini Chat Model" (lmChatGoogleGemini)**
- **Cần thiết**: Đảm bảo **Google Palm API Key** đã được cập nhật.
- **Prompt mặc định**:
  ```plaintext
  Analyze the lead's company and suggest the best automation idea from the list.
  ```

#### **🔹 Node "Wait 48 Hours" (wait)**
- **Không cần chỉnh**: Node này tự động chờ 48 giờ trước khi gửi follow-up.

#### **🔹 Node "Check for Reply Logic" (code)**
- **Không cần chỉnh**: Node này tự động kiểm tra phản hồi từ Outlook.

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với một lead mẫu để kiểm tra workflow.
2. **Bật Active** workflow sau khi kiểm tra thành công.

---

## ✍️ **Mẹo & gợi ý nâng cao**
- **Kết hợp với Slack/Telegram**: Thêm node **Slack/Telegram Webhook** để thông báo khi lead mới hoặc phản hồi.
- **Lưu log hoạt động**: Sử dụng **Google Sheets** để ghi lại tất cả hoạt động của workflow.
- **Gửi báo cáo định kỳ**: Tạo một **Google Sheet Dashboard** để theo dõi tỷ lệ chuyển đổi.
- **Tùy chỉnh AI hơn**: Cập nhật **prompt** trong node **Google Gemini** để AI viết email phù hợp với phong cách của công ty.

---

## 📌 **Kết luận**
Workflow này **giải phóng công ty tư vấn marketing khỏi công việc chăm sóc lead thủ công**, giúp tập trung vào chiến lược marketing cao cấp. **Chỉ cần 15 phút thiết lập, hệ thống sẽ tự động hóa toàn bộ quy trình chăm sóc lead!**

👉 **Bắt đầu ngay** bằng cách import workflow và kết nối các tài khoản cần thiết. Nếu có vấn đề, hãy để lại comment dưới đây! 🚀