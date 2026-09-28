---
title: "🚀 Tự động tổng hợp tin tức AI từ RSS, Reddit và HN bằng Claude gửi đến Discord và Slack"
description: "Workflow n8n tự động thu thập, phân tích và tổng hợp tin tức AI hàng ngày từ nhiều nguồn, gửi báo cáo định kỳ đến Discord và Slack với AI Claude"
slug: "tu-dong-tong-hop-tin-tuc-ai-voi-claude"
tags: [n8n, automation, no-code, AI, news, Discord, Slack]
keywords: [n8n workflow, tự động hóa tin tức AI, Claude AI, Discord bot, Slack integration]
---

# 🚀 Tự động tổng hợp tin tức AI từ RSS, Reddit và HN bằng Claude gửi đến Discord và Slack

[Các sếp đang làm thủ công việc tổng hợp tin tức AI hàng ngày từ nhiều nguồn khác nhau? Bị mệt mỏi với việc phải đọc hàng trăm bài viết mỗi ngày? Workflow này sẽ giúp các sếp tiết kiệm thời gian đáng kể bằng cách tự động hóa toàn bộ quy trình từ thu thập tin tức đến tổng hợp báo cáo.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động thu thập và phân tích hàng trăm bài viết mỗi ngày
- **Tin tức cá nhân hóa**: Lọc và sắp xếp tin tức theo độ quan trọng và chủ đề quan tâm
- **Báo cáo chuyên nghiệp**: Nhận báo cáo hàng ngày được tổng hợp bởi AI Claude với định dạng đẹp
- **Hoạt động liên tục**: Chạy tự động hàng ngày vào lúc 6:00 sáng
- **Lưu trữ thông minh**: Tùy chọn lưu trữ tin tức đã xử lý trong cơ sở dữ liệu PostgreSQL
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Anthropic với API key (để sử dụng Claude AI)
- Discord webhook URL (để gửi báo cáo)
- Tùy chọn: Slack webhook URL (nếu muốn gửi báo cáo đến Slack)
- Tùy chọn: PostgreSQL database (nếu muốn lưu trữ lịch sử tin tức)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [trang workflow gốc](https://n8n.io/workflows/13527)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "⚙️ Configure digest settings"**:
   - Điền Discord webhook URL vào trường `discord_webhook_url`
   - Nếu muốn gửi đến Slack, điền Slack webhook URL vào trường `slack_webhook_url`
   - Điều chỉnh các tham số khác như `max_extract_articles`, `max_digest_articles` theo nhu cầu

2. **Node "Claude Sonnet (compiler)" và "Claude Haiku (analyzer)"**:
   - Thêm credential "Anthropic API" với API key của bạn
   - Đảm bảo tài khoản Anthropic có đủ credit để sử dụng

3. **Node "Create run record" và các node PostgreSQL khác**:
   - Nếu không sử dụng PostgreSQL, để `use_postgres` là `false` trong node cấu hình
   - Nếu sử dụng PostgreSQL, tạo các bảng theo schema được cung cấp trong hướng dẫn

#### 3. Kích hoạt ⚡️
1. Click vào nút "Activate" để kích hoạt workflow
2. Để kiểm tra hoạt động, có thể chạy thử với nút "Execute Workflow"
3. Sau khi xác nhận hoạt động ổn định, workflow sẽ tự động chạy hàng ngày vào lúc 6:00 sáng

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh nguồn tin tức**: Chỉnh sửa node "Build feed source list" để thêm/xóa các nguồn tin tức mong muốn
2. **Điều chỉnh trọng số chủ đề**: Trong node "Score and rank articles", điều chỉnh trọng số cho các chủ đề quan tâm
3. **Thay đổi tone báo cáo**: Chỉnh sửa prompt trong node "Compile digest with Claude" để thay đổi tone báo cáo
4. **Kết hợp với các dịch vụ khác**: Thêm node để gửi báo cáo qua email hoặc lưu vào Google Sheets
5. **Theo dõi chi phí**: Kiểm tra bảng `digest_runs` trong PostgreSQL để theo dõi chi phí sử dụng API mỗi ngày

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm hàng giờ mỗi ngày trong việc theo dõi và tổng hợp tin tức AI. Với khả năng tự động hóa toàn bộ quy trình từ thu thập tin tức đến tổng hợp báo cáo, các sếp có thể tập trung vào những việc quan trọng hơn. Hãy thử ngay và trải nghiệm cách làm việc thông minh hơn với n8n!