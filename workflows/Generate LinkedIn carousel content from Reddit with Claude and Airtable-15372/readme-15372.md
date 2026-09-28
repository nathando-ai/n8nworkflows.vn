---
title: "🚀 Tự động hóa tạo nội dung LinkedIn Carousel từ Reddit với Claude và Airtable"
description: "Biến các bài viết hot trên Reddit thành nội dung LinkedIn Carousel chuyên nghiệp tự động hàng tuần bằng AI Claude Sonnet và lưu trữ vào Airtable."
slug: "tao-linkedin-carousel-tu-reddit-claude-airtable"
tags: [n8n, automation, no-code, ai-agents, content-creation, reddit, airtable, anthropic]
keywords: [n8n workflow, tạo nội dung linkedin, ai agent claude, reddit scraping apify, airtable automation, linkedin carousel]
---

# 🚀 Tự động hóa tạo nội dung LinkedIn Carousel từ Reddit với Claude và Airtable

Các sếp có đang cảm thấy mệt mỏi mỗi tuần khi phải vắt óc suy nghĩ ý tưởng viết bài LinkedIn, săn lùng các xu hướng mới trên mạng xã hội để làm nội dung Carousel (bài viết dạng slide ảnh) thu hút tương tác? Việc tổng hợp thủ công từ Reddit, phân tích bình luận rồi thiết kế từng slide thực sự ngốn rất nhiều thời gian.

Giải pháp đây rồi! Workflow n8n này sẽ tự động hóa toàn bộ quy trình: quét các bài post nổi bật trên các subreddit mục tiêu qua **Apify**, sử dụng sức mạnh AI thông minh của **Claude Sonnet** để phân tích nội dung kèm bình luận, tự động viết bài đăng LinkedIn kèm cấu trúc thiết kế Carousel, và lưu thẳng vào **Airtable** để các sếp duyệt và xuất bản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian nghiên cứu:** Tự động bắt trọn các xu hướng hot nhất từ cộng đồng Reddit theo lịch trình định sẵn.
- **Nội dung chất lượng cao, có chiều sâu:** AI Claude kết hợp phân tích cả bài viết và các bình luận (comments) thảo luận sôi nổi để tạo ra góc nhìn đa chiều, sắc bén.
- **Sẵn sàng xuất bản:** Tự động tạo sẵn caption cho LinkedIn và văn bản/cấu trúc từng slide Carousel rõ ràng.
- **Quản lý tập trung:** Lưu trữ toàn bộ ý tưởng và nội dung đã tạo vào bảng Airtable gọn gàng, trực quan.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Apify** kèm API Key (để cào dữ liệu Reddit).
- **Tài khoản Anthropic (Claude)** kèm API Key (cho AI Agent).
- **Tài khoản Airtable** kèm Personal Access Token và một Base/Table sẵn sàng nhận dữ liệu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần cấu hình chính xác các điểm mấu chốt sau:
- **Node `Every Monday at 10am` (Schedule Trigger):** Điều chỉnh lịch chạy (thời gian, tần suất) tùy theo chiến lược đăng bài của các sếp.
- **Node `Set Target Subreddits` (Set):** Cấu hình danh sách các subreddit mục tiêu muốn theo dõi (phân cách bằng dấu cách) trong phần cài đặt trường dữ liệu.
- **Nodes `Fetch Reddit Posts via Apify` & `Fetch AI Comments via Apify` (HTTP Request):** Nhập **Apify API Key** vào mục Credentials cho cả hai node này để kết nối với các Apify actor cào dữ liệu.
- **Node `Claude Sonnet Model` (lmChatAnthropic):** Kết nối **Anthropic credentials** và đảm bảo model đang chọn là `Claude Sonnet 4.6` (hoặc phiên bản tương đương).
- **Node `Save Carousel to Airtable` (airtable):** Kết nối **Airtable credentials**, sau đó trỏ chính xác đến Base và Table mà các sếp đã chuẩn bị sẵn để lưu nội dung Carousel.
- **Nodes `Filter Posts Branch 1` & `Filter Posts Branch 2` (Filter):** Rà soát lại các điều kiện lọc bài viết (theo điểm số, từ khóa, flair...) cho phù hợp với tiêu chuẩn nội dung của doanh nghiệp.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Test workflow** để chạy thử nghiệm xem dữ liệu từ Reddit có được cào về và AI xử lý mượt mà vào Airtable hay không.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm một node **Slack** hoặc **Telegram** ngay sau bước lưu Airtable để bắn tin nhắn thông báo về điện thoại mỗi khi có một Carousel mới được tạo xong.
- **Mở rộng nguồn dữ liệu:** Không chỉ Reddit, các sếp có thể kết hợp thêm các nguồn tin tức RSS, Twitter/X để đa dạng hóa ý tưởng content.
- **Tự động đăng bài:** Kết nối thẳng Airtable với các công cụ lập lịch đăng bài lên LinkedIn để automation đạt mức tối đa 100% không chạm tay.

### 📌 Kết luận
Việc sản xuất nội dung mạng xã hội chuyên nghiệp chưa bao giờ dễ dàng đến thế khi kết hợp sức mạnh của n8n, Reddit và AI Claude. Hãy triển khai ngay workflow này để nâng tầm kênh LinkedIn của các sếp ngay hôm nay!