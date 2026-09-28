---
title: "🚀 Tự Động Giám Sát Core Web Vitals Bằng Lighthouse, Gemini AI, Telegram Và Google Sheets"
description: "Xây dựng hệ thống tự động kiểm tra tốc độ website với PageSpeed Insights, phân tích lỗi bằng Gemini AI, cảnh báo qua Telegram và lưu trữ dữ liệu lịch sử vào Google Sheets."
slug: "tu-dong-giam-sat-core-web-vitals-lighthouse-gemini-telegram-google-sheets"
tags: [n8n, automation, lighthouse, cwv, gemini-ai, telegram, google-sheets]
keywords: [n8n workflow, core web vitals, pagespeed insights, gemini ai telegram, tu dong hoa seo, kiem tra toc do website]
---

# 🚀 Tự Động Giám Sát Core Web Vitals Bằng Lighthouse, Gemini AI, Telegram Và Google Sheets

Các sếp làm SEO, quản trị website hay chạy agency chắc chắn đều hiểu nỗi khổ khi phải ngồi kiểm tra thủ công tốc độ từng trang web. Việc bỏ sót các chỉ số Core Web Vitals (CWV) kém có thể làm sụt giảm thứ hạng tìm kiếm và trải nghiệm người dùng nghiêm trọng.

Workflow n8n này sinh ra để giải quyết triệt để vấn đề đó! Nó tự động hóa 100% quy trình: gọi API PageSpeed Insights, xử lý dữ liệu, nhờ Gemini AI tóm tắt lỗi, cảnh báo ngay lập tức qua Telegram và lưu vết toàn bộ vào Google Sheets mà không cần tốn một giọt mồ hôi.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Giám sát tự động 24/7:** Chạy định kỳ nhờ lịch trình cài đặt sẵn, không lo bỏ sót biến động hiệu năng.
- **Cảnh báo tức thì:** Gửi tin nhắn qua Telegram ngay khi điểm số Core Web Vitals tụt dưới ngưỡng cho phép.
- **AI thông minh phân tích lỗi:** Sử dụng Google Gemini để tóm tắt các mô tả lỗi kỹ thuật rườm rà thành ngôn ngữ dễ hiểu.
- **Lưu trữ lịch sử trực quan:** Tự động ghi nhận dữ liệu vào Google Sheets để dễ dàng theo dõi xu hướng cải thiện theo thời gian.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động mượt mà, các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản/API Key:** Google PageSpeed Insights API Key (khuyên dùng để không bị giới hạn rate limit).
- **Google Gemini API Key:** Dành cho node AI tóm tắt mô tả lỗi.
- **Telegram Bot Token & Chat ID:** Để nhận thông báo cảnh báo.
- **Google Sheets:** File Google Sheet đã tạo sẵn các cột nhận dữ liệu Core Web Vitals.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow từ n8n hoặc import trực tiếp file JSON vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 8 nodes chính, các sếp cần lưu ý cấu hình kỹ các điểm sau:

- **Schedule Trigger:** Cài đặt tần suất chạy (ví dụ: chạy mỗi ngày 1 lần hoặc hàng tuần tùy nhu cầu).
- **call page speed insights (HTTP Request):** Điền URL website cần kiểm tra và đính kèm Google PageSpeed Insights API Key của các sếp vào phần query parameters hoặc headers.
- **processing data cwv and audits (Code):** Node này dùng Javascript để lọc ra các chỉ số Core Web Vitals quan trọng và gom các mô tả lỗi lại. Các sếp có thể tinh chỉnh ngưỡng điểm số (threshold) tại đây.
- **Google Gemini Chat Model & summarize audit description:** Kết nối credentials Google Palm/Gemini API để AI tiến hành phân tích và tóm tắt các vấn đề kỹ thuật của Lighthouse.
- **If:** Thiết lập điều kiện lọc (chỉ gửi cảnh báo khi có ít nhất một chỉ số CWV rơi xuống dưới ngưỡng tối ưu).
- **Send Notification (Telegram):** Điền Telegram Bot Token và Chat ID của nhóm hoặc cá nhân để nhận alert.
- **Append row in specific sheet (Google Sheets):** Chọn tài khoản Google Sheets OAuth2, liên kết đến file Google Sheet và mapping các trường dữ liệu (LCP, FID, CLS, Score...) vào đúng các cột tương ứng.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** để chạy thử thủ công (Test Run) kiểm tra dữ liệu trả về qua các node.
- Nếu không có lỗi xuất hiện, các sếp gạt công tắc sang **Active** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh nhận tin:** Ngoài Telegram, các sếp có thể gắn thêm node Slack hoặc Discord để team kỹ thuật cùng theo dõi.
- **Báo cáo hàng tuần:** Tạo thêm một nhánh chạy vào cuối tuần để tổng hợp trung bình các chỉ số Core Web Vitals và gửi báo cáo tóm tắt qua email.
- **Lưu log lỗi nâng cao:** Nếu điểm số quá thấp (ví dụ dưới 50 điểm), tự động tạo một task trên Jira hoặc Trello để giục team dev xử lý gấp.

### 📌 Kết luận
Việc tối ưu tốc độ website và duy trì điểm số Core Web Vitals tốt chưa bao giờ dễ dàng đến thế khi đã có "trợ lý ảo" n8n kết hợp cùng Gemini AI. Hãy áp dụng ngay workflow này để nâng cao trải nghiệm người dùng và thăng hạng SEO bền vững cho website của các sếp!