---
title: "🚀 Tự động hóa báo cáo thị trường hàng tuần với Claude AI và Slack"
description: "Hướng dẫn tự động thu thập thông tin về thương hiệu và đối thủ cạnh tranh hàng tuần, tổng hợp bằng AI và gửi báo cáo lên Slack hoàn toàn không cần code"
slug: "tu-dong-hoa-bao-cao-thi-truong-hang-tuan-voi-claude-ai-va-slack"
tags: [n8n, automation, no-code, market-research, ai-summarization]
keywords: [n8n workflow, tự động hóa báo cáo thị trường, Claude AI, Slack, tổng hợp thông tin]
---

# 🚀 Tự động hóa báo cáo thị trường hàng tuần với Claude AI và Slack

[Các sếp] có bao giờ phải mất hàng giờ mỗi tuần để theo dõi thông tin về thương hiệu của mình và đối thủ cạnh tranh trên Reddit và web không? Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình này chỉ trong vài phút, tiết kiệm thời gian quý giá và đảm bảo luôn cập nhật thông tin thị trường một cách chính xác và chuyên nghiệp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quá trình thu thập và tổng hợp thông tin hàng tuần
- **Chính xác cao**: Sử dụng AI Claude để tìm kiếm và phân tích thông tin một cách chuyên nghiệp
- **Cá nhân hóa**: Tùy chỉnh danh sách từ khóa theo nhu cầu của thương hiệu
- **Hoạt động liên tục**: Workflow chạy tự động hàng tuần vào thời gian được cài đặt
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Slack với quyền gửi tin nhắn vào kênh mục tiêu
- API Key của Anthropic để truy cập Claude AI
- Danh sách các từ khóa thương hiệu, đối thủ cạnh tranh và chủ đề cần theo dõi
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang [n8n.io/workflows/16086](https://n8n.io/workflows/16086)
2. Nhấn nút "Import" ở góc trên bên phải
3. Trong n8n Editor, nhấn nút "Import from URL" và dán link trên
4. Hoặc copy toàn bộ JSON workflow và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Weekly Trigger at Monday 8am"**:
   - Cấu hình ngày và giờ chạy workflow hàng tuần (mặc định là thứ Hai lúc 8h sáng)
   - Có thể thay đổi theo lịch trình của các sếp

2. **Node "Set Monitoring Parameters"**:
   - Cập nhật các tham số quan trọng:
     - `brandName`: Tên thương hiệu của các sếp
     - `competitors`: Danh sách các đối thủ cạnh tranh (cách nhau bằng dấu phẩy)
     - `topics`: Các chủ đề liên quan đến thương hiệu
     - `slackChannel`: Tên kênh Slack để gửi báo cáo

3. **Node "Post to Claude API" và "Post to Claude for Synthesis"**:
   - Thêm credentials "anthropicApi" với API Key của Anthropic
   - Đảm bảo tài khoản có đủ credit để sử dụng Claude AI

4. **Node "Send Digest to Slack Channel"**:
   - Thêm credentials "slackApi" với thông tin xác thực Slack
   - Kiểm tra quyền truy cập của bot Slack để gửi tin nhắn vào kênh mục tiêu

#### 3. Kích hoạt ⚡️
1. Nhấn nút "Execute Workflow" để test với dữ liệu mẫu
2. Kiểm tra kết quả ở node cuối cùng "Send Digest to Slack Channel"
3. Sau khi xác nhận hoạt động đúng, nhấn nút "Activate" để workflow chạy tự động hàng tuần

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node để lưu trữ lịch sử báo cáo trong Google Sheets hoặc Notion
- Tùy chỉnh prompt cho Claude để thay đổi phong cách báo cáo
- Kết hợp với các công cụ khác như Google Alerts để mở rộng phạm vi theo dõi
- Thiết lập cảnh báo khi phát hiện thông tin quan trọng về thương hiệu

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình thu thập và tổng hợp thông tin thị trường hàng tuần, giảm thiểu công sức thủ công và đảm bảo luôn cập nhật thông tin một cách chuyên nghiệp. Hãy thử ngay và tiết kiệm thời gian quý giá cho các sếp!