---
title: "🚀 Tự động hóa trích xuất và lưu trữ bình luận YouTube vào Google Sheets bằng n8n"
description: "Hướng dẫn chi tiết cách sử dụng workflow n8n để crawl bình luận YouTube hàng loạt, lọc dữ liệu thông minh và lưu tự động vào Google Sheets."
slug: "trich-xuat-binh-luan-youtube-google-sheets"
tags: [n8n, automation, youtube, google-sheets, market-research, no-code]
keywords: [n8n workflow, crawl bình luận youtube, lưu bình luận youtube vào google sheets, tự động hóa marketing, agent circle]
---

# 🚀 Tự động hóa trích xuất và lưu trữ bình luận YouTube vào Google Sheets

Các sếp làm sáng tạo nội dung (YouTube Creator), Marketer hay Data Analyst chắc hẳn đều hiểu cảm giác "nản" thế nào khi phải ngồi thủ công copy từng bình luận (comment) của người xem để phân tích insight, đo lường mức độ tương tác hay nghiên cứu thị trường. Việc này vừa tốn hàng giờ đồng hồ, vừa dễ bỏ sót dữ liệu quan trọng.

Giải pháp là đây! Workflow n8n được thiết kế bởi **Agent Circle** sẽ giúp các sếp tự động hóa 100% quy trình này: quét danh sách video YouTube, lấy toàn bộ bình luận, kiểm tra trạng thái và lưu trữ ngăn nắp vào Google Sheets một cách mượt mà.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần copy/paste thủ công, hàng ngàn bình luận được thu thập chỉ trong vài phút.
- **Dữ liệu tổ chức khoa học:** Tự động phân loại, lưu trữ vào các sheet riêng biệt và cập nhật trạng thái (Ready -> Finished) tránh trùng lặp.
- **Phân tích Insight chính xác:** Dễ dàng tổng hợp phản hồi của khán giả để cải thiện nội dung video hoặc chạy chiến dịch marketing.
- **Hoạt động linh hoạt:** Có thể chạy thủ công theo nhu cầu hoặc dễ dàng nâng cấp lên trigger tự động hàng ngày/hàng tuần.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Account** (để kết nối Google Sheets).
- **YouTube API Credentials / Google Cloud Console** (OAuth2 hoặc API Key đã bật quyền truy cập YouTube Data API v3 và Google Sheets API).
- **Bản mẫu Google Sheets:** [YouTube - Get Video Comments Template](https://docs.google.com/spreadsheets/d/1F5yEhjBWu3fnwgHGLsPLD9_tWRqUnxu4p0DEvUTae1Y/edit?gid=426418282#gid=426418282) (Hãy bấm Copy/Duplicate về tài khoản Google Drive của các sếp).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy đoạn JSON trực tiếp.
- Vào giao diện n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc dán trực tiếp).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node sau để workflow chạy trơn tru:
- **Google Sheets - Get Video URLs**, **Google Sheets - Insert/Update Comment**, **Google Sheets - Update Status**, **Google Sheets - Update Status - Error**: Kết nối với tài khoản Google Sheets của các sếp (chọn đúng file template đã duplicate và trỏ đúng tên tab: tab `Video URLs` cho các node quản lý link, tab `Results` cho node lưu comment).
- **HTTP Request - Get Comments**: Cấu hình kết nối `youTubeOAuth2Api` hoặc API Key hợp lệ để gọi YouTube API lấy dữ liệu bình luận.
- **Tab Google Sheets chuẩn bị dữ liệu**: 
  - Tại tab **Video URLs**: Điền các link video YouTube vào **Cột B** và đổi trạng thái ở **Cột A** thành **Ready** cho những video các sếp muốn crawl.

#### 3. Kích hoạt ⚡️
- Bấm **Test Workflow** (qua node `Test Workflow`) để chạy thử nghiệm xem dữ liệu có đổ về Google Sheets hay không.
- Sau khi test thành công, bật nút **Active** ở góc trên bên phải để kích hoạt workflow chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động hóa hoàn toàn:** Thay thế node `Test Workflow` (Manual Trigger) bằng **Google Sheets Trigger** hoặc **Schedule Trigger** để hệ thống tự quét video mới mỗi ngày mà không cần bấm tay.
- **Tích hợp AI phân tích:** Nối thêm một node AI Agent (OpenAI/Anthropic) sau bước lấy comment để tự động phân tích cảm xúc (Sentiment Analysis) xem người dùng khen hay chê.
- **Gửi thông báo:** Thêm node Telegram hoặc Slack để nhận thông báo ngay khi workflow chạy xong một batch video.

### 📌 Kết luận
Workflow này là trợ thủ đắc lực giúp các nhà sáng tạo và đội ngũ marketing khai thác tối đa kho báu dữ liệu từ bình luận YouTube. Hãy import ngay vào n8n của các sếp và tối ưu hóa quy trình làm việc ngay hôm nay!