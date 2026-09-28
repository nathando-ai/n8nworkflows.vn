---
title: "🚀 Tự Động Hóa Báo Cáo Tin Tức Kỹ Thuật Hàng Ngày Cá Nhân Hóa Với Google Gemini AI & RSS Feeds"
description: "Workflow tự động hóa thu thập, phân tích và gửi báo cáo tin tức kỹ thuật hàng ngày cá nhân hóa qua email, tiết kiệm thời gian và tối ưu hóa thông tin quan trọng cho các sếp và chuyên gia IT. Dùng Google Gemini AI để lọc và tổng hợp nội dung phù hợp với sở thích cá nhân."
slug: "tieu-dong-hoa-bao-cao-tin-tuc-ky-thuat-hang-ngay-ca-nhan-hoa"
tags: [n8n, automation, no-code, ai-summarization, google-gemini, email-automation]
keywords: [n8n workflow tự động hóa, báo cáo tin tức hàng ngày, google gemini ai, rss feeds, tự động hóa email, công cụ tăng năng suất]
---

# 🚀 **Tự Động Hóa Báo Cáo Tin Tức Kỹ Thuật Hàng Ngày Cá Nhân Hóa Với Google Gemini AI**

### **Giải pháp cho các sếp và chuyên gia IT: Tiết kiệm 2+ giờ mỗi ngày để đọc tin tức kỹ thuật**
Hàng ngày, các sếp và chuyên gia IT phải mất thời gian quét qua hàng trăm bài viết trên các trang tin, diễn đàn và RSS feeds để tìm kiếm thông tin quan trọng. **Workflow này tự động hóa toàn bộ quá trình** bằng cách:
- Thu thập tin tức từ các nguồn RSS được chọn.
- Sử dụng **Google Gemini AI** để phân tích và lọc nội dung phù hợp với sở thích cá nhân.
- Gửi báo cáo tin tức hàng ngày **cá nhân hóa** qua email với định dạng chuyên nghiệp.

Không cần viết code, chỉ cần **cấu hình vài bước** là workflow sẽ hoạt động 24/7, giúp các sếp **tập trung vào công việc chiến lược** thay vì mất thời gian vào việc tìm kiếm thông tin.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần quét thủ công hàng trăm bài viết mỗi ngày.
- **Tin tức cá nhân hóa**: AI lọc và tổng hợp nội dung phù hợp với sở thích cá nhân.
- **Định dạng chuyên nghiệp**: Báo cáo được gửi dưới dạng email với cấu trúc rõ ràng.
- **Hoạt động liên tục**: Workflow chạy tự động hàng ngày, không phụ thuộc vào thời gian làm việc.
- **Tối ưu hóa thông tin**: Chỉ lấy những tin tức quan trọng nhất, giảm bớt thông tin rác.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Cloud** (để sử dụng **Google Gemini API**):
   - API Key từ [Google Cloud Console](https://console.cloud.google.com/).
   - Credential `googlePalmApi` trong n8n (cấu hình trong **n8n Settings > Credentials**).
2. **Tài khoản email SMTP** (để gửi email tự động):
   - Thông tin SMTP (Server, Port, Username, Password) từ nhà cung cấp email (Gmail, Outlook, Zoho Mail...).
   - Credential `smtp` trong n8n.
3. **Danh sách RSS feeds** của các trang tin kỹ thuật mà các sếp quan tâm (ví dụ: Hacker News, TechCrunch, GitHub Blog...).
4. **Email nhận báo cáo**: Địa chỉ email của cá nhân hoặc nhóm để nhận tin tức hàng ngày.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [đây](https://n8n.io/workflows/10196) (hoặc sao chép từ link gốc).
- Mở **n8n Editor** → Nhấn **Import** → Chọn file JSON hoặc dán JSON vào ô nhập liệu.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **15 node**, các sếp cần chú ý cấu hình các node sau:

##### **📅 Schedule Trigger (Động cơ kích hoạt hàng ngày)**
- **Thời gian chạy**: Đặt lại thành **9:00 AM** (hoặc thời gian phù hợp) trong tab **Schedule** của node này.
- **Lưu ý**: Nếu muốn chạy nhiều lần trong ngày, chỉnh **cron expression** (ví dụ: `0 9 * * *` cho 9h sáng hàng ngày).

##### **📰 RSS Feed Sources (Nguồn tin tức)**
- **Node "Tech News Sites"** và **"Tools Subredit and Sites"**:
  - Thay đổi **URL RSS** của các trang tin mà các sếp quan tâm.
  - Ví dụ:
    - TechCrunch: `https://techcrunch.com/feed/`
    - Hacker News: `https://news.ycombinator.com/rss`
    - GitHub Blog: `https://github.blog/feed/`
  - **Lưu ý**: Nếu muốn thêm/loại bỏ nguồn, chỉnh sửa trong **Set** node tương ứng.

##### **🤖 Google Gemini AI (Phân tích và lọc tin tức)**
- **Node "Upload a file"**:
  - Đảm bảo **Google Gemini API Key** đã được cấu hình trong `googlePalmApi`.
  - **Lưu ý**: Nếu API Key hết hạn, workflow sẽ không hoạt động. Các sếp cần **cập nhật API Key** trong **n8n Credentials**.
- **Node "Analyze document"**:
  - **Thay đổi prompt** để AI lọc tin tức phù hợp với sở thích cá nhân.
  - Ví dụ:
    ```json
    "text": "Analyze the following RSS feed content and summarize the top 5 most relevant articles for a tech professional interested in AI, cloud computing, and DevOps. Return only the titles, links, and a 2-sentence summary for each."
    ```
  - **Lưu ý**: Các sếp có thể điều chỉnh prompt để phù hợp với lĩnh vực chuyên môn (ví dụ: Blockchain, Cybersecurity...).

##### **📧 Send Email (Gửi báo cáo)**
- **Node "Send email"**:
  - **Cấu hình SMTP**:
    - **Server**: `smtp.gmail.com` (nếu dùng Gmail) hoặc `smtp.zoho.com` (nếu dùng Zoho Mail).
    - **Port**: `587` (cho TLS) hoặc `465` (cho SSL).
    - **Username/Password**: Thông tin đăng nhập email.
  - **Thông tin gửi email**:
    - **From**: Địa chỉ email gửi (ví dụ: `newsletter@domain.com`).
    - **To**: Địa chỉ email nhận (ví dụ: `sếp@example.com`).
    - **Subject**: Tiêu đề email (ví dụ: `Daily Tech Newsletter - [Ngày tháng]`).
  - **Lưu ý**: Nếu dùng Gmail, các sếp cần **bật "Less Secure Apps"** hoặc sử dụng **App Password** (nếu đã khóa bảo mật 2FA).

##### **🔄 Các node khác cần chú ý**
- **Merge Both List**: Đảm bảo hai danh sách RSS (Tech News và Tools) được hợp nhất đúng.
- **Convert To CSV**: Workflow tự động chuyển đổi dữ liệu thành file CSV để AI xử lý.
- **Code (JavaScript)**: Node này được sử dụng để **định dạng email** trước khi gửi. Các sếp có thể chỉnh sửa mã JavaScript để thay đổi cách hiển thị tin tức (ví dụ: thêm logo, thay đổi màu sắc...).

#### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Chọn **Run Workflow** để kiểm tra nếu tất cả cấu hình đúng.
  - Kiểm tra email nhận để đảm bảo nội dung được gửi đúng.
- **Bật Active**:
  - Sau khi test thành công, chuyển **Status** từ **Inactive** sang **Active**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm Slack/Telegram Notification**:
   - Sử dụng node **Slack Send Message** hoặc **Telegram Bot Send Message** để thông báo khi báo cáo được gửi.
   - Cấu hình trong **n8n Credentials** với token API của Slack/Telegram.

2. **Lưu Log cho Dữ liệu**:
   - Thêm node **Google Sheets** hoặc **Airtable** để lưu lịch sử tin tức đã gửi.
   - Có thể sử dụng để theo dõi phản hồi hoặc cập nhật sở thích của các sếp.

3. **Tự động Gửi Báo Cáo Định Kỳ**:
   - Nếu muốn gửi báo cáo vào thời gian khác (ví dụ: 7h sáng), chỉnh sửa **cron expression** trong **Schedule Trigger**.

4. **Tăng Cường Cá Nhân Hóa**:
   - Sử dụng **Google Gemini API** để phân tích **lịch sử email** của các sếp và điều chỉnh nội dung tin tức theo sở thích thay đổi.
   - Ví dụ: Nếu các sếp thường mở email về tin tức AI, workflow có thể tăng trọng số cho nội dung AI trong báo cáo tiếp theo.

5. **Dùng cho Nhóm Nhiều Người**:
   - Thay vì gửi email cá nhân, các sếp có thể cấu hình để gửi **báo cáo chung** cho nhóm (ví dụ: `team@domain.com`).
   - Sử dụng **node Email Send** với **CC/BCC** để gửi cho nhiều người cùng lúc.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp và chuyên gia IT muốn **tự động hóa việc theo dõi tin tức kỹ thuật hàng ngày** mà không cần mất thời gian quét thủ công. Với **Google Gemini AI**, báo cáo được **cá nhân hóa** và **tối ưu hóa** để chỉ lấy những tin tức quan trọng nhất.

**Hành động ngay hôm nay**:
1. **Cài đặt n8n** trên VPS (nếu chưa có).
2. **Import workflow** và cấu hình các node theo hướng dẫn.
3. **Test và bật Active** để nhận báo cáo tin tức hàng ngày!

**Chia sẻ và cải tiến**: Nếu các sếp có ý tưởng cải tiến (ví dụ: thêm nguồn tin mới, thay đổi định dạng email), hãy chia sẻ để cộng đồng n8n Việt Nam cùng phát triển! 🚀

---
**📌 Lưu ý cuối cùng**:
- Nếu gặp vấn đề với **Google Gemini API**, các sếp có thể thử **mô hình AI khác** như **LLM Node** trong n8n (nếu có).
- Để **tối ưu hóa chi phí**, các sếp nên **xác định số lượng tin tức cần lấy** trong prompt của Google Gemini để tránh xử lý quá nhiều dữ liệu.