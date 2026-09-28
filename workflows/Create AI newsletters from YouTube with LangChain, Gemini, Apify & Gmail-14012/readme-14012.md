---
title: "🚀 Tự Động Hóa Tạo Newsletter AI Từ YouTube: Từ Video → Email Chuyên Nghiệp Với Gemini, LangChain & Gmail"
description: "Workflow n8n tự động chuyển đổi video YouTube thành newsletter email chuyên nghiệp, tự động hóa toàn bộ quy trình từ lấy transcript, phân tích màu sắc thương hiệu, viết nội dung, thiết kế HTML đến gửi email cho tất cả người đăng ký. Giúp tiết kiệm 10+ giờ/lần và đảm bảo tính nhất quán thương hiệu."
slug: "tay-dong-hoa-tao-newsletter-ai-tu-youtube"
tags: [n8n, automation, no-code, ai-multimodal, gmail, google-sheets, langchain, gemini-ai]
keywords: [tự động hóa newsletter youtube, gemini ai newsletter, langchain n8n, gửi email bulk từ youtube, tự động hóa nội dung marketing]
---

# 🚀 **Tự Động Hóa Tạo Newsletter AI Từ YouTube: Từ Video → Email Chuyên Nghiệp**

Hãy tưởng tượng: **Một video YouTube của bạn** được tự động chuyển thành một **newsletter email đẹp mắt, chuyên nghiệp**, với nội dung được tóm tắt, thiết kế phù hợp với thương hiệu, và gửi đến tất cả người đăng ký chỉ trong **vài giây**—không cần viết một chữ nào! Đây chính là công cụ **Create AI Newsletters from YouTube** trên n8n, kết hợp **Gemini AI, LangChain, Apify và Gmail**, giúp các sếp tiết kiệm **10+ giờ/lần** và nâng cao hiệu quả marketing.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quy trình từ lấy transcript đến gửi email (không cần viết thủ công).
- **Nội dung chuyên nghiệp**: AI tóm tắt video thành **3 phần chính** (điểm chính, chi tiết, kết luận) với **tôn chỉ báo chí**.
- **Thiết kế nhất quán**: Email tự động áp dụng **màu sắc thương hiệu** từ website, giữ trật tự và hình ảnh.
- **Gửi bulk hiệu quả**: Chia nhỏ danh sách người đăng ký thành batch để gửi mà không bị chặn spam.
- **Lưu trữ và theo dõi**: Giữ bản nháp newsletter trong Google Sheets để quản lý và cải tiến.
:::

---
## 🎯 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n Self-hosted** (khuyến nghị cài trên VPS để hoạt động 24/7).
2. **API Keys và Credentials**:
   - **Gmail OAuth2**: Để gửi email bulk (cần kích hoạt "Less Secure Apps" hoặc sử dụng OAuth2).
   - **Google Sheets OAuth2 API**: Để đọc/writing dữ liệu từ bảng tính.
   - **Google Palm API (Gemini)**: Để sử dụng mô hình AI Gemini của Google.
3. **Dữ liệu đầu vào**:
   - **Danh sách người đăng ký**: Bảng Google Sheets chứa email của người đăng ký.
   - **Thông tin thương hiệu**: Tên thương hiệu, website, và màu sắc thương hiệu (nếu có).
   - **Link video YouTube**: Để lấy transcript và thumbnail.
4. **Template Google Sheets**:
   - Sử dụng [template đã cung cấp](https://docs.google.com/spreadsheets/d/1hvB5Zif52eCLv_X7E_OifQv9OI5usn-CQ50-TsZTMQA/edit?usp=sharing) để lưu trữ bản nháp newsletter.
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Bước 1**: Tải workflow từ [link gốc](https://n8n.io/workflows/14012) hoặc copy JSON từ file.
- **Bước 2**: Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON và chọn **"Import"**.
- **Bước 3**: Chọn **"Active"** để bật workflow.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **21 node** phức tạp, nhưng chỉ cần chú ý đến các phần sau:

#### **A. Cấu hình Credentials (Bắt buộc)**
| Node | Yêu cầu cấu hình |
|------|------------------|
| **Gmail** (`Sending Emails to all the Subscribers`) | Thêm **gmailOAuth2** với tài khoản Gmail muốn gửi email. |
| **Google Sheets** (`Get row(s) in sheet`, `Save Newsletter Draft in Google Sheet`) | Thêm **googleSheetsOAuth2Api** với quyền đọc/giới thiệu bảng tính. |
| **Google Gemini** (`Google Gemini Chat Model`, `Google Gemini Chat Model1`) | Thêm **googlePalmApi** với API Key từ [Google AI Studio](https://makersuite.google.com/). |

#### **B. Cấu hình Input Form (Trigger)**
- Node **"On form submission"** cần liên kết với một **form Google Form** hoặc **webhook** để nhận:
  - **Brand Name** (tên thương hiệu).
  - **Brand Website** (để phân tích màu sắc).
  - **YouTube Video Link** (để lấy transcript và thumbnail).

#### **C. Cấu hình AI Agents**
- **AI Agent2** (tóm tắt nội dung): Cần cấu hình **prompt** để AI viết 3 phần chính (điểm chính, chi tiết, kết luận).
- **Convert Newsletter to HTML (AI)**: Cần thiết lập **mẫu HTML** và **màu sắc thương hiệu** (được lấy từ website).

#### **D. Cấu hình Batching (Gửi Email)**
- Node **"Split In Batches"** sẽ chia danh sách người đăng ký thành batch (ví dụ: 50 email/lần) để tránh bị chặn spam.
- Node **"Loop Over Items"** sẽ lặp qua từng batch và gửi email.

---
### **3. Kích hoạt ⚡️**
- **Test Run**: Nhập một **link video YouTube** vào form trigger và chạy workflow để kiểm tra.
- **Bật Active**: Sau khi kiểm tra thành công, nhấn **"Active"** để workflow hoạt động tự động khi có form submission.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết hợp với Slack/Telegram**: Sau khi gửi email thành công, workflow có thể gửi thông báo lên Slack/Telegram để theo dõi.
2. **Lưu log hoạt động**: Sử dụng node **Sticky Note** hoặc **Google Sheets** để ghi lại lịch sử gửi email và phản hồi.
3. **Tự động hóa định kỳ**: Sử dụng **n8n Cron Trigger** để chạy workflow hàng tuần/month cho các video mới.
4. **Cải tiến nội dung**: Sau khi gửi, AI có thể phân tích **tỷ lệ mở email** và đề xuất cải tiến nội dung cho lần sau.
5. **Thêm hình ảnh động**: Nếu video có hình ảnh nổi bật, có thể tự động chèn vào email bằng **node HTTP Request** + **Information Extractor**.
:::

---
## 📌 **Kết luận**
Workflow **"Create AI Newsletters from YouTube"** là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa **tất cả quy trình từ video đến email**, tiết kiệm thời gian và nâng cao hiệu quả marketing. **Không cần viết code**, chỉ cần **cấu hình và chạy**—AI sẽ làm tất cả!

👉 **Bắt đầu ngay**:
1. **Cài n8n trên VPS** (khuyến nghị [TinoHost](https://tino.vn/vps-n8n?affid=388) với mã giảm **VPSN8N**).
2. **Import workflow** và cấu hình credentials.
3. **Nhập link video YouTube** và xem AI làm việc!

**Hãy thử và cảm nhận sự khác biệt trong cách làm việc của mình!** 🚀