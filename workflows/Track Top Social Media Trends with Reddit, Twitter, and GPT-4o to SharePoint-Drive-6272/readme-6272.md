---
title: "🚀 Theo dõi xu hướng mạng xã hội hàng đầu với Reddit, Twitter và GPT-4o lên SharePoint"
description: "Tự động thu thập xu hướng từ Reddit và Twitter, phân tích bằng AI GPT-4o và lưu kết quả vào SharePoint - giải pháp toàn diện cho nghiên cứu thị trường và quản lý nội dung"
slug: "theo-doi-xu-huong-mang-xa-hoi-reddit-twitter-gpt4o-sharepoint"
tags: [n8n, automation, no-code, market-research, ai-summarization]
keywords: [n8n workflow, tự động hóa, nghiên cứu thị trường, AI phân tích, SharePoint]
---

# 🚀 Theo dõi xu hướng mạng xã hội hàng đầu với Reddit, Twitter và GPT-4o lên SharePoint

[Các sếp] có bao giờ cảm thấy mệt mỏi khi phải theo dõi xu hướng mạng xã hội thủ công? Khi phải chuyển qua lại giữa nhiều nền tảng, ghi chú từng bài viết, sau đó phân tích và tổng hợp dữ liệu? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ thu thập dữ liệu đến lưu trữ kết quả chỉ trong vài phút mỗi ngày!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động thu thập dữ liệu từ nhiều nguồn trong 1 lần chạy
- **Phân tích thông minh**: Sử dụng AI GPT-4o để đánh giá và xếp hạng xu hướng
- **Lưu trữ chuyên nghiệp**: Tạo file Excel tự động và lưu lên SharePoint
- **Hoạt động liên tục**: Chạy định kỳ theo lịch hoặc theo yêu cầu
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Reddit (để lấy OAuth2 credentials)
- Tài khoản Twitter/X (nếu sử dụng API trends)
- API key OpenAI (cho GPT-4o)
- Tài khoản Microsoft 365 (để lấy SharePoint OAuth2 credentials)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/6272](https://n8n.io/workflows/6272)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file vừa tải về

Hoặc, các sếp có thể copy/paste JSON sau vào n8n Editor:

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

**1. Cấu hình nguồn dữ liệu (Data Sources Branch)**
- **Reddit API**: Chỉnh sửa URL để lấy dữ liệu từ subreddit mong muốn (ví dụ: `/r/tech/hot`)
- **Get Twitter Trends**: Thay đổi endpoint hoặc tham số nếu cần lấy dữ liệu từ khu vực khác
- **Merge Data**: Kết nối thêm bất kỳ node HTTP nào để thêm nguồn dữ liệu mới

**2. Cấu hình AI phân tích (AI Analysis Branch)**
- **AI Agent**: Chỉnh sửa prompt để thay đổi logic xếp hạng, số lượng xu hướng trả về hoặc định dạng đầu ra
- **Aggregate Content**: Điều chỉnh logic slice/limit để phân tích nhiều hoặc ít bài viết hơn

**3. Cấu hình lưu trữ (Storage Branch)**
- **Microsoft SharePoint**: Cập nhật folder ID hoặc tên file nếu cần
- **Create Excel**: Có thể thay thế bằng node CSV hoặc Google Sheets nếu cần

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong, click vào nút "Activate" để kích hoạt workflow
2. Test run bằng cách click vào nút "Execute workflow" để kiểm tra kết quả
3. Để chạy định kỳ, các sếp có thể thiết lập lịch trình trong n8n hoặc sử dụng các công cụ lập lịch bên ngoài

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm nguồn dữ liệu**: Kết nối với các nền tảng khác như YouTube, TikTok, Instagram
- **Tùy chỉnh báo cáo**: Thay đổi định dạng Excel để phù hợp với nhu cầu báo cáo của công ty
- **Thông báo kết quả**: Kết nối với Slack/Teams để nhận thông báo khi workflow hoàn thành
- **Lưu log hoạt động**: Thêm node để lưu nhật ký hoạt động của workflow

### 📌 Kết luận
Workflow này mang lại giải pháp toàn diện cho việc theo dõi xu hướng mạng xã hội, từ thu thập dữ liệu đến phân tích và lưu trữ kết quả. Với sự hỗ trợ của AI GPT-4o, các sếp có thể nhận được những thông tin chất lượng cao để đưa ra quyết định chiến lược hiệu quả. Hãy thử ngay và tiết kiệm thời gian quý giá của các sếp!