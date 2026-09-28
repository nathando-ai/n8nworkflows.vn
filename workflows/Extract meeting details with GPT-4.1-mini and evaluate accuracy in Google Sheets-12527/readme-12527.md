---
title: "🚀 Tự động trích xuất chi tiết cuộc họp bằng AI & Đánh giá độ chính xác với Google Sheets"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n sử dụng GPT-4.1-mini để trích xuất thông tin cuộc họp từ ngôn ngữ tự nhiên, tích hợp kiểm thử tự động với Google Sheets."
slug: "trich-xuat-chi-tiet-cuoc-hop-ai-google-sheets"
tags: [n8n, automation, ai, openai, google-sheets, subworkflow]
keywords: [n8n workflow, trích xuất cuộc họp ai, gpt-4.1-mini, google sheets evaluation, n8n ai agent]
---

# 🚀 Tự động trích xuất chi tiết cuộc họp bằng AI & Đánh giá độ chính xác với Google Sheets

Các sếp có bao giờ mệt mỏi khi phải đọc hàng loạt tin nhắn, email lộn xộn để thủ công copy ngày giờ, link họp, và thành viên tham gia vào lịch? Việc này vừa tốn thời gian, dễ sót việc lại cực kỳ nhàm chán. 

Bài viết này sẽ hướng dẫn các sếp triển khai một Subworkflow n8n thông minh sử dụng **AI Agent (GPT-4.1-mini)** để tự động hóa 100% quy trình trích xuất thông tin cuộc họp từ ngôn ngữ tự nhiên, đồng thời tích hợp khung kiểm thử (Evaluation Framework) tự động chấm điểm độ chính xác trực tiếp lên Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Biến mọi tin nhắn/văn bản thô thành dữ liệu cấu trúc (JSON) chuẩn chỉnh: tiêu đề, ngày, giờ, địa điểm, link họp, thành viên và ghi chú.
- **Kiến trúc Subworkflow tái sử dụng**: Có thể gọi subworkflow này từ bất kỳ workflow chính nào khác trong hệ thống của bạn.
- **Khung đánh giá chất lượng (Evaluation)**: Tự động so sánh kết quả thực tế của AI với dữ liệu chuẩn trên Google Sheets, chấm điểm từ 1-5 để cải thiện prompt liên tục.
- **Xử lý lỗi thông minh**: Validate dữ liệu đầu ra từ AI, ngăn chặn lỗi ngầm và bắt lỗi chi tiết để debug nhanh chóng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- Tài khoản OpenAI có cấu hình API Key (hỗ trợ các model OpenAI Chat Model).
- Tài khoản Google Sheets để lưu trữ và chạy bộ dữ liệu kiểm thử (Evaluation dataset).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow từ nguồn gốc hoặc file mẫu, sau đó dán trực tiếp vào giao diện n8n Editor của mình. Workflow bao gồm 16 nodes được thiết kế mạch lạc từ khâu trigger, AI xử lý, validate đến đánh giá kết quả.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động mượt mà, các sếp cần cấu hình chính xác các điểm sau:
- **Node `extract_meeting_details` & `OpenAI Chat Model`**: Chọn đúng OpenAI Credentials và trỏ vào model `gpt-4.1-mini` (hoặc model tương đương).
- **Node `load_eval_data` & `record_eval_output`**: 
  - Tạo bản sao từ [Google Sheets Test Dataset mẫu](https://docs.google.com/spreadsheets/d/1U89nPsasM2WNv1D7gEYINhDwylyxYw7BOd_i8ipFC0M/edit?usp=sharing).
  - Thay thế Document ID mẫu trong tham số của 2 node này bằng Spreadsheet ID của sếp.
  - Cấu hình Google Sheets OAuth2 API credentials.
- **Node `normalize_eval_data`**: Kiểm tra lại múi giờ mặc định (`timezone`) và thời gian giả lập (`now`) sao cho khớp với dữ liệu test trong Google Sheet.

#### 3. Kích hoạt ⚡️
- **Test Trích xuất thông thường**: Sử dụng dữ liệu mẫu được ghim (pinned data) tại node `trigger` và bấm Test Step để xem AI bóc tách thông tin.
- **Test Chế độ Đánh giá (Evaluation)**: Chọn "Execute workflow" -> chọn chạy từ node `load_eval_data` để hệ thống tự động chấm điểm dựa trên Google Sheet.
- Khi mọi thứ mượt mà, gạt công tắc sang **Active** để đưa vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh nhận tin**: Kết nối node trigger với Telegram Bot, Slack, hoặc Webhook nhận email để tự động bóc lịch họp ngay khi khách hàng gửi tin nhắn.
- **Lưu Log lỗi chuyên sâu**: Kết hợp node `handle_error` với một kênh Slack/Telegram cá nhân để nhận thông báo ngay lập tức nếu AI trả về lỗi định dạng hoặc thiếu dữ liệu.
- **Tối ưu Prompt**: Tinh chỉnh prompt trong Structured Output Parser hoặc node `evaluate_match` để AI hiểu sâu hơn về văn phong đặc thù của công ty các sếp.

### 📌 Kết luận
Việc tự động hóa trích xuất thông tin cuộc họp kết hợp khung đánh giá độ chính xác bằng AI sẽ giúp doanh nghiệp tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần. Hãy import workflow ngay và tối ưu hóa quy trình vận hành của các sếp từ hôm nay!