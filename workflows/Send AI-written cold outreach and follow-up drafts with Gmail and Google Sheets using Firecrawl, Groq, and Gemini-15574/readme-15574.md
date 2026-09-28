---
title: "🚀 Tự Động Hóa Cold Outreach & Follow-Up AI-Powered với Gmail, Google Sheets, Firecrawl & Gemini (N8N)"
description: "Workflow này tự động hóa toàn bộ chu kỳ cold email từ việc thu thập thông tin website prospect đến viết email cá nhân hóa và quản lý follow-up, tiết kiệm 80% thời gian nghiên cứu thủ công. Sử dụng AI Gemini, Groq, và Firecrawl để tối ưu hóa hiệu suất outreach cho doanh nghiệp."
slug: "tieu-dong-hoa-cold-outreach-ai-gmail-google-sheets"
tags: [n8n, automation, no-code, lead-nurturing, ai-summarization, cold-email, firecrawl, google-gemini, groq]
keywords: [n8n workflow cold email, tự động hóa outreach, AI viết email cá nhân hóa, Firecrawl crawl website, Gemini AI cold outreach, Groq API, Gmail automation]
---

# 🚀 **Tự Động Hóa Cold Outreach & Follow-Up AI-Powered với Gmail, Google Sheets, Firecrawl & Gemini**

## **Giới Thiệu**
Bạn có bao giờ cảm thấy mệt mỏi vì phải dành **80% thời gian** cho việc nghiên cứu thủ công, viết email cá nhân hóa, và theo dõi follow-up cho từng lead? **Workflow này giải quyết vấn đề đó** bằng cách tự động hóa **toàn bộ chu kỳ cold outreach** từ việc **crawl website prospect** đến **viết email AI-powered** và **quản lý follow-up** một cách thông minh.

Với sự kết hợp của **AI Gemini (Google)**, **Groq API** (tối ưu hóa tốc độ), **Firecrawl** (crawl website hiệu quả), và **Gmail API**, workflow này giúp bạn:
✅ **Tiết kiệm 100% thời gian nghiên cứu** (không cần copy-paste thông tin từ website).
✅ **Viết email cá nhân hóa** dựa trên nội dung website prospect.
✅ **Tự động tìm kiếm và xác minh email** trước khi gửi.
✅ **Quản lý follow-up** một cách tự động, dựa trên lịch sử email.
✅ **Tối ưu hóa chi phí API** bằng cách sử dụng Groq cho việc lọc URL và Gemini cho việc viết email.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** so với cách làm thủ công.
- **Email cá nhân hóa 100%** dựa trên thông tin từ website prospect.
- **Tự động xác minh email** trước khi gửi, giảm tỷ lệ bounce.
- **Quản lý follow-up tự động**, không cần can thiệp thủ công.
- **Tối ưu hóa chi phí API** bằng cách phân công nhiệm vụ cho các mô hình AI phù hợp (Groq cho lọc URL, Gemini cho viết email).
- **Không bị giới hạn số lượng lead** (tùy thuộc vào tài nguyên VPS).
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
### **1. Tài khoản & API Keys**
| **Tài khoản / API Key** | **Mục đích sử dụng** |
|--------------------------|----------------------|
| **Google Sheets OAuth2** | Đọc/ghi dữ liệu lead trong bảng Google Sheets. |
| **Firecrawl API** | Crawl website prospect, tìm URL chiến lược và scrape nội dung. |
| **Groq API** | Lọc URL hiệu quả (tốc độ cao, chi phí thấp). |
| **Google Gemini API** | Viết email cold outreach và follow-up. |
| **Gmail OAuth2** | Tạo draft email và lấy lịch sử email thread. |
| **VerifiEmail API** | Xác minh tính hợp lệ của email trước khi gửi. |

### **2. Bảng Google Sheets chuẩn bị**
Tạo một **bảng Google Sheets** với các cột sau:
| **Cột** | **Mô tả** |
|---------|-----------|
| `domain` | Domain của prospect (ví dụ: `example.com`). |
| `niche` | Ngành nghề của prospect (ví dụ: "SaaS", "E-commerce"). |
| `region` | Khu vực (ví dụ: "Việt Nam", "USA"). |
| `email` | Email của prospect (nếu có). |
| `status` | Trạng thái lead (`pending`, `emailed`, `no_email`, `unsubscribed`). |
| `follow_ups` | Số lượng follow-up đã thực hiện (đặt ban đầu là `0`). |

**Ví dụ:**
| domain       | niche    | region   | email          | status    | follow_ups |
|--------------|----------|----------|----------------|-----------|------------|
| example.com  | SaaS     | USA      | contact@example | pending   | 0          |

---

## 🚀 **Cách import & lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/15574](https://n8n.io/workflows/15574) hoặc copy/paste JSON vào **n8n Editor**.
- **Chọn phiên bản phù hợp**:
  - **Version A (Standard)**: Sử dụng các node mặc định (không cần cài thêm).
  - **Version B (Do...While)**: Sử dụng node `n8n-nodes-do-while` (cần cài thêm).

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
#### **A. Cấu hình Credentials**
Mỗi node sử dụng API cần **credentials** riêng. Các sếp phải:
1. **Tạo credentials** trong **Settings → Credentials** của n8n:
   - **Google Sheets OAuth2**: Tạo từ [Google Cloud Console](https://console.cloud.google.com/).
   - **Firecrawl API**: Mua API key từ [Firecrawl](https://firecrawl.io/).
   - **Groq API**: Mua API key từ [Groq](https://groq.com/).
   - **Google Gemini API**: Tạo từ [Google AI Studio](https://aistudio.google.com/).
   - **Gmail OAuth2**: Tạo từ [Google Cloud Console](https://console.cloud.google.com/).
   - **VerifiEmail API**: Mua API key từ [VerifiEmail](https://verifiemail.com/).

2. **Gán credentials** cho các node tương ứng:
   - Node `🧠 Gemini (Cold Email)` và `🧠 Gemini (Follow-Up)` → Gán `googlePalmApi`.
   - Node `⚡ Groq LLM` → Gán `groqApi`.
   - Node `✅ Verify Email` → Gán `verifiEmailApi`.

#### **B. Cấu hình Google Sheets**
- **Thay đổi `documentId`** trong các node `googleSheets` bằng **ID của bảng Google Sheets** của các sếp.
  - **Cách lấy ID**: Mở bảng Google Sheets → URL sẽ có dạng:
    `https://docs.google.com/spreadsheets/d/[ID]/edit`
    → **ID** là chuỗi sau `/d/` và trước `/edit`.

#### **C. Tùy chỉnh Prompt AI**
- Mở node `✍️ Write Cold Email` và `✍️ Write Follow-Up Email` → **Chỉnh sửa prompt** để phù hợp với:
  - **Tên công ty** của các sếp.
  - **Giá trị cung cấp** (offer).
  - **Tôn giọng** (chuyên nghiệp, thân thiện, ngắn gọn...).

#### **D. Chọn phiên bản phù hợp**
- **Version A (Standard)**: Xóa tất cả node có `[v2]` (phải bên phải).
- **Version B (Do...While)**: Xóa tất cả node không có `[v2]` (phải bên trái) và **cài node `n8n-nodes-do-while`** trước.

---

### **3. Kích hoạt ⚡️**
1. **Test run** với **1 lead mẫu**:
   - Thêm **1 hàng** vào bảng Google Sheets với `status = pending`.
   - Chọn **Manual Trigger** → **Execute** để kiểm tra workflow.
2. **Bật Active workflow** khi đã kiểm tra xong.

---

## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Tối ưu hóa chi phí API**
- **Groq** chỉ được sử dụng cho việc **lọc URL** (nhanh, rẻ).
- **Gemini** chỉ được sử dụng cho việc **viết email** (tốn kém hơn).
- **Firecrawl** có thể **lọc URL trước** bằng cách sử dụng **sitemap** để giảm số lượng trang scrape.

### **2. Gửi thông báo Slack/Telegram khi hoàn thành**
- Thêm node **Slack/Telegram Webhook** sau **Manual Trigger** để nhận thông báo khi workflow hoàn thành.

### **3. Lưu log hoạt động**
- Thêm node **Google Sheets** sau **Create Cold Email Draft** để ghi log:
  - Thời gian gửi.
  - Trạng thái (thành công/thất bại).
  - Nội dung email (nếu cần).

### **4. Tự động chạy định kỳ**
- Sử dụng **n8n Cloud Scheduler** hoặc **cron job** trên VPS để chạy workflow **hàng ngày/lần tuần**.

### **5. Kết hợp với CRM**
- Nếu sử dụng **HubSpot, Salesforce, hoặc Pipedrive**, có thể **sync dữ liệu lead** từ CRM vào Google Sheets để workflow tự động xử lý.

---

## 📌 **Kết luận**
Workflow này **giải phóng 80% thời gian** của các sếp khỏi việc nghiên cứu thủ công và viết email, đồng thời **tăng hiệu suất outreach** bằng cách tự động hóa **toàn bộ chu kỳ cold email và follow-up**.

**Hành động ngay:**
1. **Cài n8n trên VPS** (dùng mã giảm giá **VPSN8N**).
2. **Import workflow** và cấu hình credentials.
3. **Test với 1 lead** và bắt đầu tự động hóa outreach!

👉 **Bắt đầu tự động hóa outreach AI-powered ngay hôm nay!** 🚀