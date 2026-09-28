---
title: "🤖 [Hướng dẫn chi tiết] Tự động hóa hỗ trợ khách hàng WhatsApp với GPT-4 Mini, Google Sheets & Rapiwa API"
description: "Tự động hóa hoàn toàn quy trình hỗ trợ khách hàng trên WhatsApp bằng công nghệ AI GPT-4 Mini, kết hợp với Google Sheets và Rapiwa API. Tiết kiệm thời gian, nâng cao trải nghiệm khách hàng và quản lý dữ liệu hiệu quả."
slug: "tu-dong-hoa-ho-tro-khach-hang-whatsapp-voi-gpt-4-mini-google-sheets-rapiwa-api"
tags: [n8n, automation, no-code, whatsapp, ai-chatbot, google-sheets]
keywords: [n8n workflow, tự động hóa, chatbot, whatsapp, google sheets, rapiwa api, gpt-4 mini]
---

# 🤖 Tự động hóa hỗ trợ khách hàng WhatsApp với GPT-4 Mini, Google Sheets & Rapiwa API

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian xử lý yêu cầu khách hàng lên đến 90%
- Tự động hóa hoàn toàn quy trình hỗ trợ khách hàng trên WhatsApp
- Cung cấp thông tin chính xác và nhanh chóng từ cơ sở dữ liệu Google Sheets
- Ghi lại tất cả các tương tác khách hàng để phân tích và cải thiện dịch vụ
- Tăng cường trải nghiệm khách hàng với các câu trả lời tự nhiên và cá nhân hóa
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Rapiwa API (để kết nối và gửi nhận tin nhắn WhatsApp)
- Tài khoản Google API (để truy cập Google Sheets và Google Docs)
- OpenAI API Key (để sử dụng mô hình GPT-4 Mini)
- Dữ liệu sản phẩm, dịch vụ và tài liệu hỗ trợ đã được chuẩn bị trong Google Sheets và Google Docs
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n của bạn, hãy làm theo các bước sau:

1. Truy cập vào n8n Editor của bạn
2. Nhấp vào nút "Import from URL" trên thanh công cụ
3. Dán liên kết sau vào ô nhập liệu: `https://n8n.io/workflows/10716`
4. Nhấp vào nút "Import" để hoàn tất quá trình import

Hoặc bạn cũng có thể tải xuống file JSON từ liên kết trên và import thủ công thông qua giao diện n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

1. **Rapiwa Trigger Node**:
   - Cần cấu hình credentials cho Rapiwa API
   - Đảm bảo tài khoản Rapiwa đã được kích hoạt và có quyền gửi nhận tin nhắn WhatsApp
   - Hướng dẫn cài đặt Rapiwa: [https://www.npmjs.com/package/n8n-nodes-rapiwa](https://www.npmjs.com/package/n8n-nodes-rapiwa)

2. **Google Sheets Nodes**:
   - Cần cấu hình credentials cho Google Sheets API
   - Đảm bảo các Google Sheets chứa dữ liệu sản phẩm, dịch vụ và log hỗ trợ đã được chia sẻ với tài khoản dịch vụ Google
   - Cần cung cấp ID của các Google Sheets tương ứng trong các node:
     - Read Company Information
     - Read Product
     - Read Service
     - Log Customer Issues

3. **Google Docs Node**:
   - Cần cấu hình credentials cho Google Docs API
   - Cung cấp ID của tài liệu Google chứa thông tin tài liệu sản phẩm

4. **OpenAI Nodes**:
   - Cần cung cấp OpenAI API Key
   - Đảm bảo tài khoản OpenAI có đủ credit để sử dụng mô hình GPT-4 Mini
   - Các node OpenAI được cấu hình sẵn với mô hình "gpt-4.1-mini"

5. **HTTP Request Tools**:
   - Các node này được cấu hình để truy cập các tài liệu hỗ trợ trực tuyến của các sản phẩm khác nhau
   - Đảm bảo các liên kết tài liệu sản phẩm vẫn hoạt động và có thể truy cập được

#### 3. Kích hoạt ⚡️
Sau khi đã cấu hình tất cả các node cần thiết, hãy thực hiện các bước sau để kích hoạt workflow:

1. Thực hiện test run với dữ liệu mẫu để đảm bảo workflow hoạt động đúng cách
2. Kiểm tra các node quan trọng để đảm bảo chúng trả về kết quả như mong đợi
3. Kích hoạt workflow bằng cách nhấp vào nút "Active" trên thanh công cụ

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack hoặc Telegram để nhận thông báo khi có yêu cầu hỗ trợ mới
- Thêm node để gửi báo cáo hàng ngày về các yêu cầu hỗ trợ đã xử lý
- Tích hợp với hệ thống CRM để theo dõi và quản lý khách hàng hiệu quả hơn
- Sử dụng tính năng memory của workflow để cung cấp trải nghiệm hỗ trợ liên tục và cá nhân hóa
- Tối ưu hóa các prompt trong node OpenAI để cải thiện chất lượng câu trả lời

### 📌 Kết luận
Workflow này cung cấp một giải pháp toàn diện để tự động hóa hỗ trợ khách hàng trên WhatsApp bằng công nghệ AI tiên tiến. Với khả năng kết nối với nhiều nguồn dữ liệu và hệ thống khác nhau, nó giúp các doanh nghiệp nâng cao hiệu suất hỗ trợ khách hàng, giảm chi phí vận hành và cung cấp trải nghiệm dịch vụ tốt hơn cho khách hàng. Hãy áp dụng ngay workflow này để tối ưu hóa quy trình hỗ trợ khách hàng của bạn!