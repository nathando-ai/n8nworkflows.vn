---
title: "🚀 Tự Động Theo Dõi Xu Hướng Từ Khóa Trên Reddit & Gửi Báo Cáo Qua Email Với Apify"
description: "Hướng dẫn xây dựng workflow n8n tự động quét từ khóa trên Reddit bằng Apify, sắp xếp nội dung thịnh hành và gửi báo cáo qua Gmail mỗi ngày."
slug: "tu-dong-theo-doi-xu-huong-reddit-va-gui-bao-cao-email"
tags: [n8n, automation, reddit, apify, market-research, gmail]
keywords: [n8n workflow, theo doi xu huong reddit, apify reddit scraper, tu dong hoa email, nghien cuu thi truong]
---

# 🚀 Tự Động Theo Dõi Xu Hướng Từ Khóa Trên Reddit & Gửi Báo Cáo Qua Email Với Apify

Việc theo dõi các cuộc thảo luận, xu hướng hoặc phản hồi của khách hàng trên Reddit là một "mỏ vàng" cho nghiên cứu thị trường (Market Research). Tuy nhiên, nếu phải thủ công tìm kiếm hàng loạt từ khóa, lọc các bài viết có lượng tương tác cao và tổng hợp lại mỗi ngày thì sẽ ngốn rất nhiều thời gian của các sếp.

Workflow n8n này sẽ giải quyết triệt để nỗi đau đó bằng cách tự động hóa 100 quy trình: quét từ khóa trên Reddit thông qua Apify, lọc và xếp hạng bài viết theo điểm số (score/upvotes), sau đó gửi báo cáo chi tiết qua Gmail và lưu trữ vào Data Table để tiện theo dõi lịch sử.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian:** Không còn cảnh lướt Reddit thủ công hàng giờ để tìm insight.
- **Báo cáo tự động định kỳ:** Nhận email tổng hợp các bài viết hot nhất liên quan đến từ khóa của doanh nghiệp mỗi ngày/tuần.
- **Dữ liệu được lưu trữ bài bản:** Mọi kết quả đều được đồng bộ vào n8n Data Table giúp dễ dàng tra cứu, phân tích lịch sử.
- **Tùy chỉnh linh hoạt:** Dễ dàng điều chỉnh thuật toán sắp xếp bài viết theo upvotes, bình luận hoặc độ mới.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản Apify:** Cần có API Key để gọi Apify Actor chuyên thu thập dữ liệu Reddit.
- **Tài khoản Gmail:** Đã kết nối OAuth2 với n8n để gửi email báo cáo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này hoặc sao chép toàn bộ mã nguồn JSON, sau đó dán trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình chính xác các node sau để workflow chạy mượt mà:

- **Reddit Schedule Trigger:** Cài đặt tần suất chạy mong muốn (ví dụ: Chạy mỗi ngày một lần vào 8 giờ sáng).
- **Get Reddit Query Rows (Data Table):** Tạo một Data Table chứa danh sách các từ khóa/cụm từ tìm kiếm trên Reddit mà các sếp muốn theo dõi, sau đó trỏ node này về bảng đó.
- **Fetch Reddit Posts via Apify1 (HTTP Request):** 
  - Thêm **Apify API Key** vào phần credentials.
  - Cấu hình URL endpoint của Apify Actor chuyên scrape Reddit và truyền query động vào body/params.
- **Sort Reddit Posts by Score & Rank Reddit Posts1 (Code):** Hai node code này dùng để xử lý, làm sạch và sắp xếp các bài viết dựa trên điểm số (upvotes/score) hoặc mức độ tương tác. Các sếp có thể tùy chỉnh lại logic code nếu muốn ưu tiên tiêu chí khác.
- **Send Reddit Report Email (Gmail):** Kết nối tài khoản Gmail của các sếp, cấu hình địa chỉ email người nhận và định dạng nội dung email báo cáo hiển thị trực quan.
- **Push Results to Data Table:** Trỏ tới Data Table lưu trữ kết quả để hệ thống tự động ghi lại dữ liệu sau mỗi lần chạy.

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** hoặc **Execute Workflow** để chạy thử nghiệm xem dữ liệu có trả về đúng ý không.
- Nếu mọi thứ xanh mướt, hãy gạt công tắc sang **Active** để hệ thống tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram:** Thay vì chỉ gửi email, các sếp có thể nối thêm node Slack hoặc Telegram để bắn thông báo ngay lập tức vào nhóm chat khi có bài viết "triệu view" về sản phẩm của công ty.
- **Phân tích cảm xúc (Sentiment Analysis):** Kết hợp thêm một AI Agent hoặc OpenAI Node để phân tích xem các bài viết bàn về từ khóa của các sếp mang sắc thái tích cực, tiêu cực hay trung lập.
- **Lưu trữ nâng cao:** Thay vì dùng n8n Data Table mặc định, các sếp có thể đẩy dữ liệu lên Google Sheets hoặc Notion để các thành viên khác trong team cùng xem.

### 📌 Kết luận
Workflow theo dõi xu hướng Reddit tự động này là trợ thủ đắc lực cho các marketer, product manager và chủ doanh nghiệp muốn nắm bắt insight thị trường nhanh chóng mà không tốn công sức. Hãy áp dụng ngay vào hệ thống của các sếp để tối ưu hóa hiệu suất làm việc!