---
title: "🚀 Hệ thống tự động phân loại và xử lý truy vấn AI thông minh giữa Gemini và GPT"
description: "Workflow n8n giúp tự động phân loại độ phức tạp của truy vấn và chuyển hướng đến mô hình AI phù hợp nhất (Gemini 2.5 Pro cho truy vấn phức tạp, GPT-4.1 Nano cho truy vấn đơn giản), tối ưu hóa chi phí và hiệu suất."
slug: "he-thong-tu-dong-phan-loai-va-xu-ly-truy-van-ai-gemini-gpt"
tags: [n8n, automation, no-code, AI, LangChain]
keywords: [n8n workflow, tự động hóa, AI, Gemini, GPT, LangChain]
---

# 🚀 Hệ thống tự động phân loại và xử lý truy vấn AI thông minh giữa Gemini và GPT

[Các sếp đang gặp khó khăn khi phải tự động xử lý hàng nghìn truy vấn từ khách hàng, nhân viên hoặc hệ thống khác. Mỗi truy vấn có độ phức tạp khác nhau, đòi hỏi phải sử dụng mô hình AI phù hợp. Workflow này sẽ giúp các sếp tự động phân loại truy vấn và chuyển hướng đến mô hình AI phù hợp nhất (Gemini 2.5 Pro cho truy vấn phức tạp, GPT-4.1 Nano cho truy vấn đơn giản), tối ưu hóa chi phí và hiệu suất.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động phân loại và xử lý truy vấn mà không cần can thiệp thủ công.
- **Tối ưu chi phí**: Sử dụng mô hình AI phù hợp nhất cho từng truy vấn, giảm thiểu chi phí sử dụng API.
- **Hiệu suất cao**: Đảm bảo thời gian phản hồi nhanh chóng và chính xác cho từng loại truy vấn.
- **Tích hợp dễ dàng**: Kết nối với nhiều nền tảng chat khác nhau như Slack, Telegram, hoặc các hệ thống khách hàng khác.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n với các node LangChain đã được kích hoạt.
- API keys từ Google Gemini và OpenAI.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/9247](https://n8n.io/workflows/9247).
3. Hoặc tải file JSON về và import từ máy tính.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "When chat message received"**:
   - Cấu hình để nhận tin nhắn từ các nền tảng chat khác nhau (Slack, Telegram, hoặc các hệ thống khách hàng khác).

2. **Node "Model Selector"**:
   - Đảm bảo node này chỉ xuất ra 1 (phức tạp) hoặc 2 (đơn giản).
   - Có thể điều chỉnh prompt để cải thiện độ chính xác của phân loại.

3. **Node "Main Agent"**:
   - Đảm bảo node này bao gồm ngày hiện tại trong prompt để cung cấp thông tin mới nhất.

4. **Node "4.1 nano" (lmChatOpenAi)**:
   - Thêm credentials OpenAI API.
   - Đảm bảo model được chọn là "gpt-4.1-nano".

5. **Node "2.5 pro" và "2.0 flash" (lmChatGoogleGemini)**:
   - Thêm credentials Google PaLM API.

#### 3. Kích hoạt ⚡️
1. Kiểm tra từng node bằng cách gửi dữ liệu mẫu để đảm bảo chúng hoạt động đúng.
2. Bật chế độ Active cho workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Kết nối workflow với các nền tảng chat phổ biến để tạo ra một trợ lý AI thông minh.
- **Lưu log truy vấn**: Lưu lại các truy vấn và phản hồi để phân tích và cải thiện hiệu suất của hệ thống.
- **Gửi báo cáo định kỳ**: Tự động gửi báo cáo về hiệu suất và chi phí sử dụng API hàng tuần hoặc hàng tháng.
- **Tích hợp với các hệ thống CRM**: Kết nối với các hệ thống quản lý quan hệ khách hàng để lưu trữ và quản lý thông tin khách hàng một cách hiệu quả.

### 📌 Kết luận
Workflow này giúp các sếp tự động phân loại và xử lý truy vấn AI một cách thông minh, tối ưu hóa chi phí và hiệu suất. Hãy áp dụng ngay để nâng cao trải nghiệm khách hàng và tăng hiệu quả làm việc của đội ngũ!