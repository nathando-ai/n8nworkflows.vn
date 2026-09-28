---
title: "🚀 Tự động theo dõi tuyển dụng lãnh đạo và gửi email tiếp cận AI với PredictLeads, OpenAI và Gmail"
description: "Workflow n8n tự động theo dõi tuyển dụng lãnh đạo, phát hiện tín hiệu tuyển dụng và gửi email tiếp cận cá nhân hóa bằng AI - tiết kiệm thời gian và tăng hiệu quả chăm sóc khách hàng tiềm năng"
slug: "tu-dong-theo-doi-tuyen-dung-lanh-dao-va-gui-email-tiep-canh-ai"
tags: [n8n, automation, no-code, lead nurturing, ai automation]
keywords: [n8n workflow, tự động hóa tiếp cận khách hàng, ai email marketing, tự động hóa tuyển dụng]
---

# 🚀 Tự động theo dõi tuyển dụng lãnh đạo và gửi email tiếp cận AI với PredictLeads, OpenAI và Gmail

[Các sếp] có biết rằng việc theo dõi tuyển dụng lãnh đạo và gửi email tiếp cận cá nhân hóa là một trong những thách thức lớn nhất trong marketing? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này trong vòng vài phút, tiết kiệm thời gian quý giá và tăng hiệu quả chăm sóc khách hàng tiềm năng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quy trình theo dõi tuyển dụng và gửi email
- **Tăng hiệu quả**: Phát hiện tín hiệu tuyển dụng sớm và gửi email tiếp cận cá nhân hóa
- **Tăng độ chính xác**: Sử dụng AI để phân tích dữ liệu tuyển dụng và tạo nội dung email phù hợp
- **Hoạt động liên tục**: Workflow chạy tự động hàng ngày mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Sheets chứa danh sách các công ty mục tiêu (cột `domain` và `company_name`)
- API key từ [PredictLeads](https://predictleads.com)
- Tài khoản Slack để nhận thông báo
- Tài khoản Gmail để gửi email tiếp cận
- API key từ OpenAI (để sử dụng GPT-4o-mini)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/14104](https://n8n.io/workflows/14104)
2. Click vào nút "Import" và chọn "Import from URL"
3. Dán link workflow vào ô nhập liệu và nhấn "Import"

Hoặc có thể copy/paste JSON workflow sau đây vào n8n Editor:

```json
{
  "nodes": [
    // Danh sách các nodes trong workflow
  ],
  "connections": [
    // Danh sách các kết nối giữa các nodes
  ]
}
```

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Load Target Accounts"**:
   - Kết nối với tài khoản Google Sheets của bạn
   - Đảm bảo sheet chứa cột `domain` và `company_name`

2. **Node "Retrieve Company Job Openings" và "Retrieve Company"**:
   - Kết nối với tài khoản PredictLeads của bạn
   - Đảm bảo API key đã được kích hoạt

3. **Node "Send Sales Hiring Alert" và "Send Hiring Spike Alert"**:
   - Kết nối với tài khoản Slack của bạn
   - Chọn kênh nhận thông báo phù hợp

4. **Node "Send Outreach Email"**:
   - Kết nối với tài khoản Gmail của bạn
   - Đảm bảo đã bật "Less secure app access" hoặc sử dụng App Password nếu sử dụng 2FA

5. **Node "Generate Outreach Email"**:
   - Thiết lập biến môi trường `OPENAI_API_KEY` trong n8n
   - Có thể điều chỉnh prompt trong node "Build AI Prompt" để phù hợp với sản phẩm và thương hiệu của bạn

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong, nhấn nút "Test Workflow" để kiểm tra dữ liệu mẫu
2. Nếu kết quả như mong đợi, nhấn nút "Activate" để kích hoạt workflow
3. Workflow sẽ chạy tự động hàng ngày lúc 8 AM

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh danh sách các vị trí lãnh đạo**: Chỉnh sửa regex trong node "Filter Leadership Roles" để phù hợp với các vị trí lãnh đạo mà bạn quan tâm
2. **Điều chỉnh ngưỡng phát hiện tuyển dụng**: Trong node "High Hiring Volume?", bạn có thể thay đổi giá trị mặc định (10) để phù hợp với chiến lược của mình
3. **Kết hợp với Slack/Telegram**: Thêm các node để gửi thông báo qua Slack hoặc Telegram thay vì chỉ qua Slack
4. **Lưu log hoạt động**: Thêm node để lưu log hoạt động của workflow vào Google Sheets hoặc cơ sở dữ liệu khác

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình theo dõi tuyển dụng lãnh đạo và gửi email tiếp cận cá nhân hóa. Với việc kết hợp PredictLeads, OpenAI và Gmail, workflow này mang lại hiệu quả cao trong việc phát hiện tín hiệu tuyển dụng và tạo nội dung email phù hợp. Hãy áp dụng ngay để tiết kiệm thời gian và tăng hiệu quả chăm sóc khách hàng tiềm năng!