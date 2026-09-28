---
title: "🚀 Tự Động Hoá Tạo Tạp Chí Tin Tức Được Lọc Sàng Từ Reddit Với GPT-4o Mini & Gmail"
description: "Workflow này tự động thu thập, phân tích và tổng hợp các bài viết từ subreddit theo chủ đề cụ thể, sau đó biến chúng thành một bản tin email chuyên nghiệp với sự trợ giúp của AI. Giúp tiết kiệm thời gian lên đến 80% so với cách làm thủ công, đồng thời đảm bảo nội dung luôn được cá nhân hóa và cập nhật liên tục."
slug: "tu-dong-hoa-tao-tap-chi-tin-tuc-reddit-gpt-4o-mini"
tags: [n8n, automation, no-code, ai-multimodal, redittogmail, gpt-4o-mini]
keywords: [n8n workflow reddit, tự động hóa newsletter, gpt-4o mini tự động hóa, tạo bản tin từ reddit, tự động hóa nội dung marketing]
---

# 🚀 **Tự Động Hoá Tạo Tạp Chí Tin Tức Được Lọc Sàng Từ Reddit Với GPT-4o Mini & Gmail**

## **📌 Giới Thiệu**
Bạn đã bao giờ phải mất nhiều giờ mỗi tuần để thu thập, đọc và tổng hợp tin tức từ Reddit để tạo ra một bản tin định kỳ? Hoặc bạn muốn theo dõi các chiến lược marketing mới nhất nhưng lại không có thời gian để lọc ra những nội dung thực sự hữu ích? **Workflow này giải quyết tất cả những vấn đề đó!**

Với **n8n**, bạn có thể tự động hóa toàn bộ quy trình:
✅ **Thu thập** tất cả bài viết mới từ subreddit bạn quan tâm (ví dụ: *microsaas* về chiến lược thu hút khách hàng mới).
✅ **Lọc** nội dung theo chủ đề cụ thể (ví dụ: "Strategies and tactics to get new customers").
✅ **Tổng hợp** bài viết và bình luận thành các đoạn tóm tắt ngắn gọn bằng **GPT-4o Mini**.
✅ **Gửi** bản tin email chuyên nghiệp đến hộp thư của bạn (hoặc nhóm nhân viên) **mỗi ngày/tuần** mà không cần can thiệp thủ công.

Kết quả? **Một bản tin tin tức được cá nhân hóa, cập nhật liên tục, và tiết kiệm thời gian lên đến 80% so với cách làm thủ công.**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải thủ công tìm kiếm, đọc và tổng hợp tin tức từ Reddit.
- **Nội dung cá nhân hóa**: AI tự động lọc ra những bài viết liên quan đến chủ đề bạn quan tâm.
- **Bản tin chuyên nghiệp**: Dữ liệu được tổng hợp thành email có định dạng HTML, dễ đọc và chia sẻ.
- **Hoạt động liên tục**: Workflow chạy tự động hàng ngày/tuần, không cần can thiệp.
- **Tăng cường hiệu suất**: Dữ liệu được sắp xếp theo độ phổ biến (ups/comments) và thời gian mới nhất.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Reddit** (để lấy dữ liệu):
   - Cài đặt **OAuth2** trong n8n (node **Get many posts** và **Get post comments**).
   - Xác minh quyền truy cập vào subreddit (ví dụ: *microsaas*).

2. **API Key OpenAI**:
   - Đăng ký tài khoản [OpenAI](https://platform.openai.com/) và lấy **API Key**.
   - Cấu hình trong các node: **filter topic of interest**, **Summarize post + comments**, **create newsletter**.
   - **Model**: Chọn **gpt-4o-mini** (rẻ và hiệu quả).

3. **Tài khoản Gmail**:
   - Cài đặt **OAuth2 Gmail** trong node **Send a message**.
   - Đảm bảo email này có quyền gửi email (không bị chặn bởi Google).

4. **Tham số cấu hình**:
   - **Subreddit**: Tên subreddit muốn theo dõi (ví dụ: *microsaas*).
   - **Chủ đề quan tâm**: Ví dụ: *"Strategies and tactics to get new customers"*.
   - **Email nhận**: Địa chỉ email để gửi bản tin (ví dụ: *your-email@gmail.com*).
   - **Tiêu đề email**: Bạn có thể thay đổi từ mặc định *"Reddit Digest"*.

---
---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [liên kết gốc](https://n8n.io/workflows/7709) hoặc copy/paste mã JSON vào **n8n Editor**.
- **Cách import**:
  1. Mở **n8n Editor** (trên máy chủ self-hosted hoặc n8n.cloud).
  2. Nhấn **Import** → Chọn file JSON hoặc dán mã JSON vào ô **Import Workflow**.
  3. Chọn **Import** để hoàn tất.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **17 node**, nhưng chỉ có **5 node cần cấu hình chính**:
- **Get many posts** (Reddit)
- **Set topic of interest** (Set chủ đề)
- **filter topic of interest** (OpenAI)
- **Send a message** (Gmail)
- **Create Newsletter** (OpenAI)

##### **🔹 Node 1: Get many posts (Reddit)**
- **Subreddit**: Điền `microsaas` (hoặc subreddit khác bạn muốn theo dõi).
- **Filters**:
  - **Category**: Chọn `new` (lấy bài viết mới nhất).
  - **Sort**: Chọn `top` (sắp xếp theo độ phổ biến).
- **Lưu ý**:
  - Đảm bảo subreddit có **bài viết mới** để workflow không trả về kết quả trống.
  - Nếu subreddit không có bài viết mới, hãy thử subreddit khác như *growthhacking* hoặc *startups*.

##### **🔹 Node 2: Set topic of interest**
- **Topic**: Điền chủ đề cụ thể (ví dụ: *"Strategies and tactics to get new customers"*).
- **Lưu ý**:
  - Chủ đề càng **narrow** (chỉnh xác), AI càng lọc ra nội dung tốt hơn.
  - Tránh chủ đề quá rộng (ví dụ: *"Marketing"* → AI sẽ lọc ra nhiều nội dung không liên quan).

##### **🔹 Node 3: filter topic of interest (OpenAI)**
- **Model**: Chọn `gpt-4o-mini`.
- **Messages**:
  - Prompt mặc định đã được tối ưu, **không cần chỉnh sửa** trừ khi bạn muốn thay đổi cách AI đánh giá bài viết.
- **Lưu ý**:
  - Đảm bảo **API Key OpenAI** được điền đúng trong **Credentials**.

##### **🔹 Node 4: Create Newsletter (OpenAI)**
- **Model**: Chọn `gpt-4o-mini`.
- **Messages**:
  - Prompt đã được thiết kế để tạo **HTML email** chuyên nghiệp.
  - Nếu muốn thay đổi phong cách (ví dụ: thêm logo, thay đổi màu sắc), chỉnh sửa phần `messages` trong node này.
- **Lưu ý**:
  - Đảm bảo dữ liệu đầu vào (bài viết và bình luận) được **tóm tắt** trước khi gửi đến node này.

##### **🔹 Node 5: Send a message (Gmail)**
- **To**: Điền email nhận (ví dụ: `your-email@gmail.com`).
- **Subject**: Thay đổi từ mặc định *"Reddit Digest"* nếu muốn (ví dụ: *"Tin tức mới nhất về Microsaas"*).
- **Message**: Đã tự động lấy nội dung từ node **Create Newsletter**.
- **Lưu ý**:
  - **Không gửi đến danh sách email** ngay từ đầu (test với email cá nhân trước).
  - Đảm bảo **OAuth2 Gmail** được cấu hình đúng.

##### **🔹 Các node khác (không cần chỉnh sửa)**
- **Loop Over Items**: Chia bài viết thành batch để xử lý hiệu quả.
- **Get post comments**: Lấy bình luận cho mỗi bài viết.
- **clean comments / merge comments**: Xử lý dữ liệu bình luận thành dạng JSON.
- **Summarize post + comments**: Tóm tắt bài viết và bình luận bằng AI.
- **Select Top 10 Post**: Lọc ra 10 bài viết phổ biến nhất.
- **String to Json**: Chuyển đổi dữ liệu thành JSON chuẩn.

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Execute Workflow** để chạy thử với dữ liệu mẫu.
   - Kiểm tra **log** trong n8n để xem có lỗi nào không.
2. **Bật Active**:
   - Sau khi cấu hình xong, chuyển **Active** từ `false` sang `true`.
   - **Lưu ý**: Workflow sẽ chạy **mỗi khi được kích hoạt thủ công** (do node **manualTrigger**).
   - **Nếu muốn chạy tự động**:
     - Thay thế node **manualTrigger** bằng **Schedule Trigger** (cài đặt trong n8n).
     - Chọn thời gian chạy (ví dụ: hàng ngày lúc 8h sáng).

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tự động gửi bản tin hàng tuần**:
   - Thay thế node **manualTrigger** bằng **Schedule Trigger** và cấu hình chạy vào thứ 7 hàng tuần.
   - Ví dụ: `0 0 * * 0` (lúc 00:00 thứ 7).

2. **Gửi bản tin đến nhóm Slack/Telegram**:
   - Thay node **Send a message (Gmail)** bằng **Slack Webhook** hoặc **Telegram Bot**.
   - Cấu hình trong node **Webhook** để gửi tin nhắn thay vì email.

3. **Lưu log vào Google Sheets**:
   - Thêm node **Google Sheets** sau node **Send a message** để ghi lại lịch sử gửi email.
   - Dùng để theo dõi hiệu suất và thống kê.

4. **Thay đổi chủ đề tự động**:
   - Sử dụng node **Code** để thay đổi `topic_of_interest` dựa trên ngày tháng (ví dụ: chủ đề khác nhau cho từng tháng).

5. **Tăng cường tính cá nhân hóa**:
   - Thêm node **OpenAI** để AI tự động viết **đoạn giới thiệu** cho bản tin (ví dụ: *"Chào [Tên], đây là bản tin tin tức mới nhất về..."*).

6. **Xử lý lỗi khi Reddit không có bài viết mới**:
   - Thêm node **If** để kiểm tra nếu workflow không lấy được bài viết, thì gửi email thông báo:
     *"Không có bài viết mới trong subreddit [Tên Subreddit] hôm nay."*

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho những người muốn tự động hóa việc thu thập và tổng hợp tin tức từ Reddit thành bản tin email chuyên nghiệp. Với **n8n + GPT-4o Mini**, bạn không chỉ tiết kiệm thời gian mà còn nhận được **nội dung được lọc sàng và cá nhân hóa** hàng ngày.

**Hành động ngay!**
1. **Cài đặt n8n trên VPS** (để workflow chạy 24/7).
2. **Cấu hình các API Key** (Reddit, OpenAI, Gmail).
3. **Chạy thử workflow** và điều chỉnh chủ đề/subreddit.
4. **Bật tự động hóa** và bắt đầu nhận bản tin mỗi ngày!

👉 **Bạn có thể tùy chỉnh workflow này cho nhiều mục đích khác**:
- Theo dõi **tin tức công nghệ** (subreddit *technology*).
- Nhận **các chiến lược marketing** (subreddit *marketing*).
- Lọc **tin tức về startup** (subreddit *startups*).

**Hãy bắt đầu tự động hóa ngay hôm nay!** 🚀