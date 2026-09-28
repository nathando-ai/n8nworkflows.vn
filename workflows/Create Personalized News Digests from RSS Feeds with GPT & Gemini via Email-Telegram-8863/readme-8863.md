---
title: "📰 **Tự Động Hoá Tóm Tắt Tin Tức Cá Nhân Hóa Từ RSS Feeds Với GPT & Gemini (Gửi Email + Telegram)**"
description: "Workflow này tự động lấy tin tức từ RSS feeds, tóm tắt bằng AI (OpenAI GPT-4.1 Mini + Google Gemini), và gửi báo cáo hàng ngày cá nhân hóa qua Email và Telegram. Giúp các sếp tiết kiệm thời gian theo dõi tin tức quan trọng, tránh mất thông tin quan trọng."
slug: "tieu-dong-hoa-tom-tat-tin-tuc-rss-voi-gpt-gemini-email-telegram"
tags: [n8n, automation, no-code, content-creation, ai-powered, rss-feed, email-automation, telegram-bot, openai, google-gemini]
keywords: [n8n workflow rss feed, tự động hóa tin tức hàng ngày, gpt-4.1 mini gemini, gửi báo cáo tin tức email telegram, scrapegraphai, ai tóm tắt bài báo]
---

# 🚀 **Tự Động Hoá Tóm Tắt Tin Tức Cá Nhân Hóa Từ RSS Feeds Với GPT & Gemini**

## **Nỗi Đau Của Các Sếp**
Trong thời đại thông tin quá tải, các sếp thường phải mất **giờ đồng hồ** mỗi ngày để:
- Quét qua nhiều nguồn tin tức (RSS feeds, blog, báo điện tử).
- Lọc ra những tin tức **thực sự quan trọng** cho công việc.
- Tóm tắt và chia sẻ với đồng nghiệp một cách **cá nhân hóa**.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Lấy tin tức mới nhất** từ RSS feeds trong 24h.
✅ **Tóm tắt bằng AI** (OpenAI GPT-4.1 Mini + Google Gemini) để rút gọn nội dung.
✅ **Gửi báo cáo hàng ngày** qua **Email** và **Telegram**, giúp các sếp **không bỏ lỡ bất kỳ tin tức quan trọng nào**.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần quét tin tức thủ công hàng ngày.
- **Tóm tắt thông minh**: AI rút gọn nội dung **không mất ý nghĩa**.
- **Cá nhân hóa**: Báo cáo được gửi **đặc biệt** qua Email và Telegram.
- **Hoạt động liên tục**: Workflow chạy **mỗi ngày tự động** (không cần can thiệp).
- **Dễ dàng mở rộng**: Thêm nhiều nguồn RSS hoặc thay đổi AI theo nhu cầu.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản và API Keys**:
- **ScrapeGraphAI** (miễn phí) → [Đăng ký tại đây](https://dashboard.scrapegraphai.com/?via=n3witalia)
- **OpenAI API Key** (để sử dụng GPT-4.1 Mini)
- **Google Gemini API Key** (để sử dụng Google AI)
- **Gmail OAuth2** (để gửi Email tự động)
- **Telegram Bot Token** + **Chat ID** (để gửi tin nhắn Telegram)

✔ **URL của RSS Feeds** (ví dụ: RSS của một trang tin tức như BBC, Reuters, hoặc blog cá nhân).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/8863](https://n8n.io/workflows/8863) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ link trên và **paste** vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này có **16 node**, nhưng các bước quan trọng nhất cần chú ý:

##### **🔹 Node "RSS Read" (Lấy tin tức từ RSS)**
- **Tham số cần thiết**:
  - **URL_FEED**: Điền URL của RSS feed (ví dụ: `https://feeds.bbci.co.uk/news/rss.xml`).
  - **Limit**: Đặt số lượng bài viết muốn lấy (ví dụ: **10 bài mới nhất trong 24h**).

##### **🔹 Node "ScrapeGraphAI" (Chuyển bài viết thành Markdown)**
- **Tham số cần thiết**:
  - **API Key**: Điền **ScrapeGraphAI API Key** (từ tài khoản đăng ký).
  - **Resource**: Đặt là `markdownify` (để chuyển bài viết thành Markdown).

##### **🔹 Node "OpenAI Chat Model" & "Google Gemini Chat Model" (Tóm tắt bằng AI)**
- **Tham số cần thiết**:
  - **OpenAI API Key**: Điền vào **openAiApi** (từ tài khoản OpenAI).
  - **Google Gemini API Key**: Điền vào **googlePalmApi** (từ tài khoản Google Cloud).
  - **Model**:
    - **GPT-4.1 Mini** (để tóm tắt nhanh).
    - **Google Gemini** (để so sánh chất lượng tóm tắt).

##### **🔹 Node "Send a message" (Gửi Email)**
- **Tham số cần thiết**:
  - **Gmail OAuth2**: Đăng nhập tài khoản Gmail và cấp quyền cho n8n.
  - **Người nhận (To)**: Điền Email của mình hoặc đồng nghiệp.
  - **Tiêu đề Email**: Có thể tự động hóa (ví dụ: **"Báo cáo tin tức hàng ngày - [Ngày tháng]"**).
  - **Nội dung Email**: Sử dụng **HTML template** để đẹp mắt.

##### **🔹 Node "Send to Telegram" (Gửi báo cáo Telegram)**
- **Tham số cần thiết**:
  - **Telegram Bot Token**: Tạo bot trên [@BotFather](https://t.me/BotFather) và lấy **API Token**.
  - **Chat ID**: Lấy từ [@userinfobot](https://t.me/userinfobot) (gửi tin nhắn `/start` và copy ID).
  - **Message**: Nội dung báo cáo sẽ được gửi dưới dạng **text hoặc HTML**.

##### **🔹 Node "Aggregate" (Kết hợp tất cả tin tức)**
- **Lưu ý**: Node này **kết hợp** tất cả tin tức trước khi gửi, giúp tránh trùng lặp.

---

#### **3. Kích Hoạt ⚡️**
- **Test Run**: Chạy **manual trigger** để kiểm tra workflow với **dữ liệu mẫu**.
- **Bật Active**: Sau khi kiểm tra thành công, **bật Active** để workflow chạy tự động hàng ngày.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm nhiều nguồn RSS**:
   - Mở rộng **RSS Read** để lấy tin từ **nhiều trang** (ví dụ: TechCrunch, Forbes, VnExpress).
2. **Lưu log tin tức**:
   - Thêm **Google Sheets** hoặc **Notion** để lưu lịch sử tin tức.
3. **Gửi báo cáo định kỳ**:
   - Sử dụng **n8n Cron Trigger** để chạy workflow **mỗi ngày 8h sáng**.
4. **Cải thiện chất lượng tóm tắt**:
   - Thử **Google Gemini Pro** thay vì Mini nếu muốn tóm tắt **chất lượng cao hơn**.
5. **Thêm Slack Notification**:
   - Thêm node **Slack** để báo động khi có tin tức **quan trọng**.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Tiết kiệm thời gian** theo dõi tin tức.
✔ **Nhận báo cáo cá nhân hóa** qua Email và Telegram.
✔ **Sử dụng AI tóm tắt** mà không cần viết code.

**Hãy import ngay và tự động hóa cuộc sống công việc của mình!** 🚀

---
**🔗 [Tải workflow nguyên bản tại đây](https://n8n.io/workflows/8863)**
**💬 Có thắc mắc? Hãy comment bên dưới!**