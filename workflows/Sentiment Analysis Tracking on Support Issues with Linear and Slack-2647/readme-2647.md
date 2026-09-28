---
title: "🚀 Theo dõi Phân tích Cảm xúc trên Vấn đề Hỗ trợ với Linear và Slack"
description: "Tự động hóa theo dõi và phân tích cảm xúc trên các vấn đề hỗ trợ từ Linear, lưu kết quả vào Airtable và thông báo qua Slack khi cảm xúc trở nên tiêu cực"
slug: "theo-doi-phan-tich-cam-xuc-linear-slack"
tags: [n8n, automation, no-code, linear, airtable, slack]
keywords: [n8n workflow, tự động hóa, phân tích cảm xúc, linear, airtable, slack]
---

# 🚀 Theo dõi Phân tích Cảm xúc trên Vấn đề Hỗ trợ với Linear và Slack

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi phải theo dõi thủ công các vấn đề hỗ trợ, kiểm tra cảm xúc và phản hồi kịp thời. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động theo dõi các vấn đề hỗ trợ trên Linear mỗi 30 phút
- Phân tích cảm xúc tự động cho các cuộc trò chuyện hỗ trợ
- Lưu trữ kết quả phân tích trong Airtable để theo dõi
- Thông báo kịp thời qua Slack khi cảm xúc trở nên tiêu cực
- Giảm thời gian phản hồi và cải thiện trải nghiệm khách hàng
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Linear với quyền truy cập API
- Tài khoản Airtable với bảng đã tạo (hoặc sử dụng mẫu)
- Tài khoản Slack với quyền gửi tin nhắn
- API Key từ OpenAI cho phân tích cảm xúc
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/2647](https://n8n.io/workflows/2647)
2. Nhấn nút "Import" để tải xuống file JSON
3. Trong n8n Editor, nhấn "Import from File" và chọn file đã tải xuống

Hoặc copy/paste JSON sau vào n8n Editor:

```json
{
  "nodes": [
    // Danh sách các nodes từ workflow gốc
  ],
  "connections": [
    // Danh sách các kết nối giữa nodes
  ]
}
```

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

1. **Node "Fetch Active Linear Issues" (GraphQL)**
   - Cấu hình credentials: `httpHeaderAuth` với API Key của Linear
   - Chỉnh sửa query GraphQL để lọc các vấn đề phù hợp với nhu cầu của bạn

2. **Node "OpenAI Chat Model" (lmChatOpenAi)**
   - Cấu hình credentials: `openAiApi` với API Key của OpenAI
   - Đảm bảo tài khoản OpenAI có đủ credit để thực hiện phân tích

3. **Node "Get Existing Sentiment" và "Update Row" (Airtable)**
   - Cấu hình credentials: `airtableTokenApi` với API Key của Airtable
   - Chỉnh sửa ID bảng và tên bảng trong Airtable
   - Đảm bảo cấu trúc bảng phù hợp với workflow (các cột: Issue ID, Current Sentiment, Previous Sentiment, Last Modified)

4. **Node "Report Issue Negative Transition" (Slack)**
   - Cấu hình credentials: `slackApi` với token Slack
   - Chỉnh sửa channel ID để gửi thông báo đến kênh phù hợp

5. **Node "Airtable Trigger"**
   - Cấu hình để theo dõi bảng Airtable đã chỉ định
   - Đảm bảo trigger được kích hoạt khi có thay đổi trong bảng

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, nhấn nút "Activate" để kích hoạt workflow
2. Thử chạy với dữ liệu mẫu để kiểm tra hoạt động
3. Sau khi xác nhận hoạt động ổn định, bật chế độ "Active" để workflow chạy tự động

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh thời gian kiểm tra**: Thay đổi khoảng thời gian trong node "Schedule Trigger" để phù hợp với nhu cầu của bạn
2. **Kết hợp với các công cụ khác**: Thêm node để gửi email thông báo hoặc cập nhật trạng thái trong các công cụ quản lý dự án khác
3. **Phân tích nâng cao**: Sử dụng các node khác của LangChain để thực hiện phân tích sâu hơn về các vấn đề hỗ trợ
4. **Báo cáo định kỳ**: Thêm node để tạo báo cáo tổng hợp cảm xúc hàng ngày và gửi qua email

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quá trình theo dõi và phân tích cảm xúc trên các vấn đề hỗ trợ, giảm thiểu thời gian phản hồi và cải thiện trải nghiệm khách hàng. Bằng cách tích hợp Linear, Airtable và Slack, workflow này cung cấp một giải pháp toàn diện để quản lý và theo dõi các vấn đề hỗ trợ một cách hiệu quả.