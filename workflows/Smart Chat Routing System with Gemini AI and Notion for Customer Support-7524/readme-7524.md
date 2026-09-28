---
title: "🤖 Hệ thống tự động phân loại tin nhắn khách hàng với Gemini AI và Notion"
description: "Tự động phân loại và xử lý tin nhắn khách hàng thông minh với Gemini AI và Notion - Giải pháp tự động hóa hoàn toàn không cần code cho đội ngũ chăm sóc khách hàng"
slug: "he-thong-tu-dong-phan-loai-tin-nhan-khach-hang-voi-gemini-ai-va-notion"
tags: [n8n, automation, no-code, ai, chatbot]
keywords: [n8n workflow, tự động hóa, chatbot, Gemini AI, Notion]
---

# 🤖 Hệ thống tự động phân loại tin nhắn khách hàng với Gemini AI và Notion

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động phân loại tin nhắn khách hàng thành 3 loại chính: Hỗ trợ khách hàng, Câu hỏi chung, Đặt lịch tư vấn
- Tích hợp Gemini AI để xử lý thông minh các yêu cầu
- Lưu trữ và truy xuất thông tin từ Notion để cung cấp dịch vụ khách hàng chuyên nghiệp
- Tiết kiệm thời gian xử lý tin nhắn từ 70-90%
- Cung cấp trải nghiệm khách hàng nhất quán và chuyên nghiệp
- Giảm thiểu lỗi do xử lý thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Cloud với API key cho Google Gemini
- Tài khoản Notion với các database đã cấu hình cho:
  - Thông tin khách hàng
  - Thông tin sản phẩm/dịch vụ
  - Lịch đặt tư vấn
- Webhook endpoint để nhận tin nhắn từ kênh chat (Slack, Telegram, Facebook Messenger...)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang workflow gốc: [Smart Chat Routing System with Gemini AI and Notion for Customer Support](https://n8n.io/workflows/7524)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

**Node quan trọng cần cấu hình:**
1. **When chat message received** (chatTrigger):
   - Cấu hình webhook endpoint để nhận tin nhắn từ kênh chat của bạn
   - Đảm bảo webhook endpoint hoạt động và có thể nhận tin nhắn

2. **Google Gemini Chat Model** (lmChatGoogleGemini):
   - Thêm credentials cho Google Cloud với API key
   - Chọn model Gemini phù hợp (gemini-pro, gemini-1.5-pro...)
   - Cấu hình các tham số như temperature, max tokens...

3. **Notion nodes** (notionTool):
   - Thêm credentials cho Notion
   - Cập nhật ID của các database Notion trong các node tương ứng:
     - Get Customers: Database chứa thông tin khách hàng
     - Get Automations: Database chứa thông tin sản phẩm/dịch vụ
     - Get More Info: Block chứa thông tin bổ sung

4. **Agent nodes** (agent):
   - Cấu hình các prompt cho từng agent:
     - Customer Service Agent: Prompt xử lý vấn đề khách hàng
     - Question Agent: Prompt trả lời câu hỏi chung
     - Booking Agent: Prompt xử lý đặt lịch tư vấn
   - Đảm bảo các prompt bao gồm thông tin cần thiết để xử lý yêu cầu

#### 3. Kích hoạt ⚡️
1. Test run với dữ liệu mẫu để kiểm tra toàn bộ workflow
2. Kiểm tra các node Notion để đảm bảo kết nối và truy xuất dữ liệu đúng
3. Kiểm tra các node Gemini để đảm bảo xử lý yêu cầu theo mong đợi
4. Bật Active workflow sau khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp với các kênh chat khác**: Kết nối workflow với Slack, Telegram, Facebook Messenger để mở rộng phạm vi sử dụng
2. **Cải thiện xử lý lỗi**: Thêm node xử lý lỗi và thông báo khi có lỗi xảy ra trong quá trình xử lý
3. **Lưu log hoạt động**: Thêm node lưu log các tương tác để theo dõi và phân tích hiệu suất
4. **Tự động hóa báo cáo**: Thêm node gửi báo cáo hàng ngày về các tương tác quan trọng

### 📌 Kết luận
Hệ thống tự động phân loại tin nhắn khách hàng với Gemini AI và Notion là giải pháp hoàn hảo cho các doanh nghiệp muốn nâng cao hiệu suất chăm sóc khách hàng mà không cần phải tuyển dụng thêm nhân viên. Với khả năng tự động phân loại và xử lý yêu cầu, doanh nghiệp có thể cung cấp dịch vụ khách hàng nhanh chóng, chính xác và chuyên nghiệp hơn bao giờ hết. Hãy áp dụng ngay để thấy sự khác biệt trong hiệu quả kinh doanh của bạn!