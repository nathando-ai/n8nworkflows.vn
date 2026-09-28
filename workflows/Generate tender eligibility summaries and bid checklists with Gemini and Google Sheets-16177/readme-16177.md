---
title: "🚀 Tự động hóa phân tích hồ sơ thầu & tạo checklist dự thầu với Gemini & Google Sheets"
description: "Hướng dẫn chi tiết workflow n8n tự động giám sát thầu, sử dụng AI Gemini phân tích độ phù hợp, tạo checklist và đồng bộ dữ liệu lên Google Sheets, Supabase, Slack, Gmail."
slug: "tu-dong-hoa-phan-tich-ho-so-thau-gemini-google-sheets"
tags: [n8n, automation, google-gemini, google-sheets, supabase, slack]
keywords: [n8n workflow, tự động hóa đấu thầu, phân tích thầu ai, google sheets, gemini api, supabase]
---

# 🚀 Tự động hóa phân tích hồ sơ thầu & tạo checklist dự thầu với Gemini & Google Sheets

Việc theo dõi, đọc hiểu và phân tích hàng loạt hồ sơ mời thầu (tender) thủ công thường ngốn rất nhiều thời gian của đội ngũ kinh doanh và dự án. Các sếp thường xuyên đối mặt với rủi ro bỏ lỡ gói thầu tiềm năng hoặc mất hàng giờ để đối chiếu điều kiện tham gia. 

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code (No-code), giúp các sếp tự động hóa toàn bộ quy trình: từ quét dữ liệu thầu mới, lọc trùng, nhờ **Google Gemini AI** phân tích độ phù hợp (Eligibility Summary) và tạo danh sách việc cần làm (Bid Checklist), cho đến lưu trữ vào Google Sheets/Supabase và bắn thông báo tức thì qua Slack/Gmail.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Không cần thủ công rà soát từng gói thầu hay copy-paste dữ liệu nữa.
- **AI phân tích thông minh:** Gemini tự động đánh giá năng lực đáp ứng (eligibility) và lập danh sách các việc cần chuẩn bị (checklist) cực kỳ chi tiết.
- **Đồng bộ đa nền tảng:** Lưu trữ dữ liệu hồ sơ thầu và checklist gọn gàng vào cả Google Sheets lẫn cơ sở dữ liệu Supabase.
- **Cảnh báo tức thì:** Đội ngũ nhận được thông báo ngay lập tức qua Slack và Gmail để kịp thời xử lý hồ sơ thầu.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI LÊN ĐỒ]
Để workflow chạy mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và credentials sau:
- **n8n Instance** (Self-hosted hoặc Cloud).
- **Google Sheets & Google Drive Credentials** (OAuth2).
- **Supabase Account & API Key** (để lưu trữ dữ liệu thầu và checklist).
- **Google Gemini (Google Palm) API Key** (để AI phân tích hồ sơ thầu).
- **Slack Bot Token / Webhook** (để gửi thông báo team).
- **Gmail OAuth2 Credentials** (để gửi email cảnh báo thầu).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ mã JSON từ nguồn cấp.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Dán (Paste) hoặc Import file JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình và map lại các credentials cho các node cốt lõi sau:
- **Trigger Tender Monitoring Schedule**: Thiết lập lịch chạy tự động (ví dụ: mỗi giờ hoặc mỗi ngày một lần).
- **Lookup Tender in Google Sheets** & **Create Tender Master Row in Google Sheets**: Kết nối tài khoản Google Sheets của các sếp, trỏ đến đúng file Sheet quản lý thầu.
- **Lookup Tender in Supabase** & **Create Tender Master Record in Supabase**: Điền Supabase API Key và trỏ tới bảng (table) phù hợp.
- **Generate Tender Eligibility and Bid Checklist**: Nhập **Google Gemini API Key** và kiểm tra prompt hệ thống để đảm bảo AI trả về cấu trúc JSON chuẩn xác.
- **Send Tender Alert to Slack**: Cấu hình Slack Credentials và kênh (channel) nhận thông báo thầu mới.
- **Send Tender Alert by Email**: Kết nối Gmail Credentials và cấu hình email người nhận.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử với tập dữ liệu mẫu ở node `Seed Dummy Tender Dataset` để kiểm tra toàn bộ luồng dữ liệu.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Có thể tích hợp thêm node Telegram hoặc Zalo OA để bắn tin nhắn thông báo thầu tới điện thoại cá nhân của sếp hoặc đội ngũ sale.
- **Tự động tạo thư mục Drive:** Kết hợp node Google Drive để tự động tạo thư mục lưu trữ tài liệu cho từng gói thầu mới trúng tuyển/phê duyệt.
- **Lưu lịch sử chạy (Logging):** Thêm bước ghi log lỗi vào một Sheet riêng để dễ dàng theo dõi nếu có lỗi phát sinh từ API của Gemini hoặc Supabase.

### 📌 Kết luận
Workflow này là một "vũ khí" tối tân giúp tự động hóa khâu săn thầu và đánh giá sơ bộ dự án, tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần. Hãy cài đặt ngay để tối ưu hóa năng suất cho đội ngũ đấu thầu của các sếp!