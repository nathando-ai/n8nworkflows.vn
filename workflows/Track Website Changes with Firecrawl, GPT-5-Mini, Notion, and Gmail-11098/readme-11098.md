---
title: "🚀 Theo dõi thay đổi website tự động với Firecrawl, GPT-5-Mini, Notion và Gmail"
description: "Hướng dẫn tự động hóa theo dõi thay đổi website hàng ngày với n8n, Firecrawl, GPT và Notion. Nhận báo cáo thay đổi qua email ngay lập tức."
slug: "theo-doi-thay-doi-website-tu-dong-voi-n8n"
tags: [n8n, automation, no-code, firecrawl, notion]
keywords: [n8n workflow, tự động hóa, theo dõi website, firecrawl, gpt, notion]
---

# 🚀 Theo dõi thay đổi website tự động với Firecrawl, GPT-5-Mini, Notion và Gmail

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động theo dõi thay đổi website hàng ngày mà không cần can thiệp thủ công.
- Chính xác: Sử dụng AI phân tích thay đổi thực sự quan trọng, bỏ qua những thay đổi nhỏ không liên quan.
- Cá nhân hóa: Lọc theo tiêu chí quan tâm của bạn (như thay đổi giá, sản phẩm mới...).
- Hoạt động liên tục: Nhận báo cáo thay đổi qua email ngay lập tức khi có cập nhật mới.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Firecrawl API (đăng ký tại [firecrawl.dev](https://firecrawl.dev))
- Tài khoản OpenAI API (lấy tại [platform.openai.com](https://platform.openai.com))
- Tài khoản Notion API (tạo database theo template [ở đây](https://scoutnow.notion.site/Track-Website-Changes-2b0c56764824800a993eca79f4b10bbf))
- Tài khoản Gmail (cho chức năng gửi email báo cáo)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/11098](https://n8n.io/workflows/11098)
2. Click vào nút "Import" để tải file JSON workflow
3. Hoặc copy toàn bộ JSON và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Schedule Trigger**: Cấu hình thời gian chạy workflow (mặc định hàng ngày)
2. **Define Target URLs**: Chỉnh sửa danh sách URL cần theo dõi (dạng JSON array)
   ```json
   [
     "https://example.com",
     "https://anothersite.com"
   ]
   ```
3. **Define What Matters To You**: Xác định tiêu chí quan tâm (ví dụ: "focus on pricing or product updates")
4. **Firecrawl Nodes**: Cấu hình credentials với API key từ Firecrawl
5. **OpenAI Node**: Thêm OpenAI API key
6. **Notion Nodes**:
   - Thêm Notion API key
   - Cập nhật Database ID của bạn
   - Đảm bảo database có cấu trúc phù hợp với template
7. **Gmail Node** (tùy chọn): Cấu hình OAuth2 credentials và email nhận báo cáo

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu với 1-2 URL
2. Kiểm tra kết quả trong Notion database
3. Bật Active workflow sau khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
- Thêm nhiều URL hơn để theo dõi nhiều website cùng lúc
- Tùy chỉnh prompt cho OpenAI để phù hợp với ngành nghề của bạn
- Kết hợp với Slack/Teams để nhận thông báo thay đổi
- Lưu log thay đổi trong Google Sheets để phân tích dài hạn
- Thiết lập báo cáo định kỳ (tuần/tháng) thay vì hàng ngày

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình theo dõi thay đổi website, giảm thiểu công sức thủ công và tập trung vào những thay đổi thực sự quan trọng. Hãy thử ngay và tiết kiệm thời gian quý giá của bạn!