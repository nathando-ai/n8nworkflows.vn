---
title: "🚀 Tự động hóa HR: Chuyển đổi tin tức nhân sự thành báo cáo cập nhật chính sách hàng tuần với n8n"
description: "Hướng dẫn chi tiết cách tự động hóa quy trình chuyển đổi tin tức HR thành báo cáo cập nhật chính sách hàng tuần bằng n8n, Google Drive, Gemini và GPT-5.2"
slug: "tu-dong-hoa-hr-news-vao-bao-cao-cap-nhat-chinh-sach-hang-tuan"
tags: [n8n, automation, no-code, HR, AI, Google Drive, Gemini, GPT]
keywords: [n8n workflow, tự động hóa HR, báo cáo cập nhật chính sách, AI RAG, Google Drive, Gemini, GPT]
---

# 🚀 Tự động hóa HR: Chuyển đổi tin tức nhân sự thành báo cáo cập nhật chính sách hàng tuần với n8n

[Các sếp HR] có bao giờ cảm thấy mệt mỏi khi phải theo dõi hàng trăm tin tức nhân sự hàng ngày, sau đó phải tổng hợp thông tin quan trọng và so sánh với các chính sách hiện có? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này trong vòng chưa đầy 15 phút!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động tổng hợp tin tức hàng tuần thay vì làm thủ công
- **Chính xác cao**: AI phân tích và so sánh thông tin với chính sách hiện có
- **Cá nhân hóa**: Báo cáo được tùy chỉnh theo nhu cầu cụ thể của bộ phận HR
- **Hoạt động liên tục**: Nhận báo cáo hàng tuần mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Workspace (cho Google Drive và Gmail)
- API Key cho Google Gemini và OpenAI (GPT-5.2)
- RSS feed URL của nguồn tin tức HR mong muốn
- Thư mục Google Drive chứa các chính sách và mẫu hợp đồng
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io](https://n8n.io) và đăng nhập
2. Nhấn vào "Workflows" > "Import from URL"
3. Dán link: `https://n8n.io/workflows/13124`
4. Nhấn "Import"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Config"**:
   - Đặt `newsUrl` thành URL của RSS feed tin tức HR mong muốn
   - Đặt `templatesFolderId` thành ID thư mục Google Drive chứa các chính sách và mẫu hợp đồng
   - Đặt `userEmail` thành địa chỉ email nhận báo cáo hàng tuần
   - Điều chỉnh `maxArticles` để cân bằng giữa chi phí và thời gian chạy

2. **Node "Extract article body"**:
   - Nếu nội dung trích xuất không chính xác, điều chỉnh CSS selector trong node này để phù hợp với cấu trúc trang web nguồn

3. **Node "Gemini chat model" và "OpenAI chat model"**:
   - Đảm bảo đã thiết lập credentials cho cả hai model này
   - Đối với GPT-5.2, hãy chắc chắn model này đã được kích hoạt trong tài khoản OpenAI của bạn

#### 3. Kích hoạt ⚡️
1. Chạy thử workflow với 1-2 bài viết mẫu để kiểm tra chất lượng trích xuất và phân tích
2. Sau khi xác nhận hoạt động ổn định, bật chế độ "Active" cho workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Teams**: Thêm node để gửi báo cáo đến kênh Slack/Teams của bộ phận HR
2. **Lưu log hoạt động**: Thêm node để lưu nhật ký các bài viết đã xử lý vào Google Sheets
3. **Tùy chỉnh báo cáo**: Điều chỉnh prompt trong node "Doc impact analyzer" để phù hợp với nhu cầu cụ thể của tổ chức
4. **Xử lý lỗi tự động**: Thêm node để gửi thông báo lỗi qua email khi workflow gặp sự cố

### 📌 Kết luận
Workflow này giúp các sếp HR tiết kiệm hàng giờ mỗi tuần bằng cách tự động hóa quy trình quan trọng này. Bằng cách kết hợp sức mạnh của n8n, Google Drive, Gemini và GPT-5.2, các sếp có thể nhận được báo cáo cập nhật chính sách hàng tuần một cách nhanh chóng, chính xác và cá nhân hóa. Hãy thử ngay và trải nghiệm sự khác biệt!