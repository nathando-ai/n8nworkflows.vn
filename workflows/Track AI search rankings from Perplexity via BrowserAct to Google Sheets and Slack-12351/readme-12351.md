---
title: "🚀 Theo dõi xếp hạng tìm kiếm AI từ Perplexity qua BrowserAct đến Google Sheets và Slack"
description: "Tự động hóa theo dõi xếp hạng tìm kiếm AI với workflow n8n, kết hợp BrowserAct, Google Sheets và Slack để tối ưu hóa chiến lược nội dung và tăng cường khả năng hiển thị thương hiệu."
slug: "theo-doi-xep-hang-tim-kiem-ai-tu-dong-hoa"
tags: [n8n, automation, no-code, browseract, google-sheets, slack, ai-search]
keywords: [n8n workflow, tự động hóa, xếp hạng tìm kiếm AI, browseract, google sheets, slack, tối ưu hóa nội dung]
---

# 🚀 Theo dõi xếp hạng tìm kiếm AI từ Perplexity qua BrowserAct đến Google Sheets và Slack

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi phải theo dõi thủ công xếp hạng tìm kiếm AI. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa quy trình theo dõi xếp hạng hàng ngày
- Chính xác: Dữ liệu được thu thập và phân tích một cách tự động, giảm thiểu sai sót
- Cá nhân hóa: Tạo báo cáo xếp hạng tùy chỉnh cho từng thương hiệu
- Hoạt động liên tục: Theo dõi 24/7 mà không cần can thiệp thủ công
- Tích hợp toàn diện: Kết nối liền mạch giữa các công cụ tìm kiếm AI, Google Sheets và Slack
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản BrowserAct với template **GEO Results & Rank Tracking**
- API Key của BrowserAct
- Tài khoản Google với quyền truy cập Google Sheets
- Tài khoản Slack với quyền gửi tin nhắn
- Tài khoản OpenRouter (để sử dụng mô hình Gemini)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/12351](https://n8n.io/workflows/12351)
2. Chọn "Import" và sao chép JSON workflow
3. Trong n8n Editor, chọn "Import from JSON" và dán nội dung đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **BrowserAct**:
   - Đảm bảo đã lưu template **GEO Results & Rank Tracking** trong tài khoản BrowserAct
   - Cấu hình credentials với API Key của BrowserAct
   - Node "Run GEO Results & Rank Tracking workflow" cần được cấu hình với ID của template BrowserAct

2. **Google Sheets**:
   - Tạo một Google Sheet với hai cột: `Company name` và `Working Category`
   - Cấu hình credentials với tài khoản Google có quyền truy cập vào Google Sheets
   - Node "Get Company data" cần được cấu hình với ID của Google Sheet chứa dữ liệu công ty

3. **OpenRouter**:
   - Cấu hình credentials với API Key của OpenRouter
   - Đảm bảo tài khoản OpenRouter có đủ credit để sử dụng mô hình Gemini

4. **Slack**:
   - Cấu hình credentials với token Slack
   - Đảm bảo bot Slack có quyền gửi tin nhắn đến kênh mong muốn

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để đảm bảo workflow hoạt động đúng
2. Sau khi kiểm tra thành công, bật chế độ Active workflow
3. Workflow sẽ tự động chạy hàng ngày theo lịch trình đã đặt

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh báo cáo**: Sửa đổi prompt trong node "Company data analyzer" để thay đổi cách phân tích dữ liệu
2. **Kết hợp với các công cụ khác**: Thêm node để gửi báo cáo qua email hoặc lưu trữ dữ liệu trong cơ sở dữ liệu
3. **Mở rộng phạm vi theo dõi**: Thêm các công cụ tìm kiếm AI khác như Bing, Yahoo để có cái nhìn toàn diện hơn
4. **Tự động hóa cảnh báo**: Cấu hình để gửi cảnh báo khi xếp hạng xuống dưới ngưỡng mong muốn

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc theo dõi xếp hạng tìm kiếm AI, giúp các sếp tiết kiệm thời gian và nguồn lực trong quá trình tối ưu hóa nội dung. Với khả năng tự động hóa hoàn toàn và tích hợp liền mạch với các công cụ phổ biến, workflow này là công cụ không thể thiếu cho bất kỳ doanh nghiệp nào muốn nâng cao khả năng hiển thị thương hiệu trên các công cụ tìm kiếm AI.