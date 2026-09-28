---
title: "🚀 TalentFlow AI: Đánh giá ứng viên tự động từ GitHub, LinkedIn bằng trí tuệ nhân tạo"
description: "Workflow n8n tự động hóa đánh giá ứng viên từ hồ sơ, GitHub, LinkedIn và LeetCode bằng AI, tiết kiệm 90% thời gian tuyển dụng và giảm thiểu rủi ro tuyển dụng sai người"
slug: "talentflow-ai-danh-gia-ung-vien-tu-dong"
tags: [n8n, automation, ai, recruitment, no-code]
keywords: [n8n workflow, tự động hóa tuyển dụng, đánh giá ứng viên, AI tuyển dụng, LangChain]
---

# 🚀 TalentFlow AI: Đánh giá ứng viên tự động từ GitHub, LinkedIn bằng trí tuệ nhân tạo

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi tuyển dụng thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm **90% thời gian tuyển dụng** bằng cách tự động hóa đánh giá ứng viên
- Giảm thiểu **rủi ro tuyển dụng sai người** nhờ phân tích chi tiết từ GitHub, LinkedIn
- **Cá nhân hóa** quá trình tuyển dụng với báo cáo đánh giá chi tiết cho mỗi ứng viên
- **Hoạt động liên tục** 24/7 mà không cần can thiệp thủ công
- **Tích hợp hoàn hảo** với các công cụ tuyển dụng hiện có như JotForm
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản **JotForm** để nhận thông tin ứng viên
- Tài khoản **Google Sheets** để lưu trữ kết quả đánh giá
- **API Key OpenRouter** để sử dụng các model AI
- **PDF.co API Key** để chuyển đổi file PDF thành text
- **Credentials** cho các node LangChain (OpenRouter Chat Model)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/5099)
2. Chọn "Download" để tải file JSON
3. Trong n8n Editor, chọn "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

**1. Node "Trigger: New Job Application" (JotForm Trigger)**
- Cần cấu hình **JotForm Credentials** và chọn form tuyển dụng cụ thể
- Đảm bảo các trường thông tin cần thiết (LinkedIn, GitHub, LeetCode username) được bao gồm trong form

**2. Node "OpenRouter Chat Model" (x4)**
- Cần cấu hình **OpenRouter Credentials**
- Chọn model AI phù hợp (ví dụ: "mistralai/mistral-large")
- Đặt **temperature** phù hợp (thường 0.7-0.9 cho đánh giá ứng viên)

**3. Node "Convert Pdf to Text(return text file link)" (PDFco API)**
- Cần cấu hình **PDF.co Credentials**
- Đảm bảo API key có quyền chuyển đổi PDF sang text

**4. Node "Append Candidate Data to Google Sheet" (Google Sheets)**
- Cần cấu hình **Google Sheets Credentials**
- Chỉ định **Spreadsheet ID** và **Sheet Name** để lưu kết quả

**5. Các node "Validate" (LinkedIn, GitHub, Leetcode Username)**
- Cần cấu hình biểu thức điều kiện để kiểm tra tính hợp lệ của username
- Ví dụ cho LinkedIn: `{{ $node["Fetch JotForm Data"].json["linkedinUsername"] }} !== ""`

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node quan trọng, chọn "Execute Workflow" để test với dữ liệu mẫu
2. Kiểm tra kết quả trên Google Sheets để đảm bảo dữ liệu được lưu đúng
3. Chuyển workflow sang trạng thái "Active" để bắt đầu hoạt động tự động

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp Slack/Teams**: Thêm node gửi thông báo đánh giá ứng viên qua Slack/Teams ngay sau khi hoàn thành
2. **Lưu log đánh giá**: Thêm node lưu log đánh giá vào Google Drive hoặc Notion để theo dõi lịch sử
3. **Gửi báo cáo định kỳ**: Tạo workflow phụ để gửi báo cáo tổng hợp đánh giá ứng viên hàng tuần
4. **Tích hợp với ATS**: Kết nối với các hệ thống quản lý tuyển dụng như Greenhouse, Lever để tự động cập nhật trạng thái ứng viên

### 📌 Kết luận
TalentFlow AI giúp các sếp tuyển dụng tiết kiệm thời gian đáng kể, giảm thiểu rủi ro tuyển dụng sai người và cá nhân hóa quá trình đánh giá ứng viên. Với khả năng tích hợp mạnh mẽ và sử dụng trí tuệ nhân tạo, workflow này là công cụ không thể thiếu cho bất kỳ công ty nào muốn nâng cao hiệu quả tuyển dụng.