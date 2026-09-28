---
title: "🚀 **Tự Động Hóa Đánh Giá Đề Tài YouTube Shorts Viral Hàng Ngày bằng Reddit, RSS & AI DeepSeek – Không Cần Code!**"
description: "Workflow tự động hóa 24/7 phân tích xu hướng từ Reddit và RSS, kết hợp với AI DeepSeek để đánh giá và lọc ra 3 đề tài YouTube Shorts có tiềm năng viral cao nhất cho kênh của các sếp. Giúp tiết kiệm thời gian lên đến 10 giờ/tuần và tối ưu hóa nội dung theo xu hướng thực tế."
slug: "tieu-dong-hoa-danh-gia-de-tai-youtube-shorts-viral"
tags: [n8n, automation, content-creation, ai-summarization, youtube-automation, reddit-rss-scraping, deepseek-ai]
keywords: [tự động hóa youtube shorts, đánh giá đề tài viral, reddit rss automation, ai deepseek cho content, workflow n8n youtube, tự động hóa content creation]
---

# 🚀 **Tự Động Hóa Đề Tài YouTube Shorts Viral Hàng Ngày – AI Đánh Giá Theo Xu Hướng Thực Tế**

## **Nỗi Đau Của Các Sếp Khi Tạo Nội Dung YouTube**
Các sếp đang mất **giờ đồng hồ hàng ngày** để:
- **Tìm kiếm xu hướng** từ Reddit, RSS, TikTok hay Google Trends thủ công.
- **Đánh giá hiệu quả** của các đề tài dựa trên kinh nghiệm cá nhân (thường không chính xác).
- **Lọc ra đề tài phù hợp** với kênh của mình, dẫn đến **tỷ lệ viral thấp** và **tốn thời gian chỉnh sửa** sau khi đăng.
- **Không có hệ thống học tập** từ dữ liệu lịch sử của kênh, khiến nội dung thiếu **đặc trưng riêng** và khó cạnh tranh.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động thu thập xu hướng** từ Reddit (hot posts) và RSS (tin tức thời sự).
✅ **Đánh giá đề tài theo mô hình AI** (DeepSeek R1) dựa trên **lịch sử thành công** của kênh.
✅ **Lọc ra Top 3 đề tài viral** phù hợp nhất, **cá nhân hóa** cho kênh của các sếp.
✅ **Gửi kết quả ngay Telegram** để các sếp có thể **nhận thông báo tức thì** mà không cần theo dõi.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
- **Tiết kiệm 10+ giờ/tuần** (không cần tìm kiếm xu hướng thủ công).
- **Tỷ lệ viral tăng gấp 2-3 lần** (do đề tài được AI đánh giá dựa trên dữ liệu thực tế).
- **Nội dung cá nhân hóa** (không chỉ copy xu hướng chung, mà phù hợp với kênh).
- **Hoạt động 24/7** (không cần can thiệp của con người).
- **Báo cáo tuần định kỳ** (hiểu rõ xu hướng và hiệu suất kênh).
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài Khoản YouTube API OAuth2** (để lấy dữ liệu kênh và video).
2. **API Key OpenRouter** (để sử dụng mô hình AI DeepSeek R1).
3. **Tài Khoản Telegram Bot** (để gửi kết quả tự động).
4. **Data Table (Google Sheets/Excel)** để lưu trữ:
   - **Lịch sử video** (tên, lượt xem, like, comment, tags).
   - **Báo cáo phân tích kênh** (mô hình thành công, xu hướng ưa thích).
   - **Đề tài viral được lọc ra**.
5. **Nguồn RSS** (ví dụ: tin tức tech, giải trí, thể thao).
6. **Subreddit Reddit** (ví dụ: r/YouTube, r/Shorts, r/Trending).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/15253](https://n8n.io/workflows/15253) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON và dán vào **Import Workflow** trong n8n.
- **Cách 3:** Tạo mới workflow và **copy/paste từng node** theo danh sách dưới đây.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này chia thành **2 phần chính**:
- **Phần 1 (Hàng Ngày):** Đánh giá xu hướng và lọc đề tài viral.
- **Phần 2 (Hàng Tuần):** Phân tích mô hình kênh và cập nhật dữ liệu.

##### **A. Cấu Hình API & Credentials**
| **Node** | **Yêu Cầu** | **Lưu Ý** |
|----------|------------|------------|
| **YouTube OAuth2** | API Key + Client ID/Secret | Sử dụng **YouTube Data API v3** (đăng ký tại [Google Cloud Console](https://console.cloud.google.com/)). |
| **OpenRouter API** | API Key | Mô hình AI sử dụng **DeepSeek R1** (đăng ký tại [OpenRouter](https://openrouter.ai/)). |
| **Telegram Bot** | Token Bot + Chat ID | Tạo bot tại [@BotFather](https://t.me/BotFather) và lấy Chat ID từ Telegram. |
| **Data Table (Google Sheets)** | Sheet Name + API Key | Cấu trúc sheet phải phù hợp với các node **dataTable** trong workflow. |

##### **B. Cấu Hình Cụ Thể Các Node Quan Trọng**
1. **Trigger – Daily Trend Scan & Weekly Intelligence Extraction**
   - Đặt lịch chạy:
     - **Hàng ngày:** 8h sáng (thời gian các sếp thường check xu hướng).
     - **Hàng tuần:** Chủ nhật 10h sáng (để phân tích mô hình kênh).

2. **Fetch – News RSS (30) & Fetch – Reddit Hot (50)**
   - **RSS:** Điền URL của nguồn tin tức (ví dụ: [RSS.com](https://rss.com/)).
   - **Reddit:** Điền URL của subreddit (ví dụ: `https://www.reddit.com/r/YouTube/hot.json`).

3. **YouTube Nodes (Get Channel, Get Videos, Get Video Stats)**
   - Điền **Channel ID** của kênh YouTube cần phân tích.
   - Chọn **50 video gần nhất** để AI học mô hình.

4. **AI – Virality Scoring Engine & AI Channel Pattern Analysis**
   - **Prompt AI** đã được tối ưu sẵn, **không cần chỉnh sửa** (nếu muốn cải tiến, các sếp có thể mở node **agent** và sửa prompt).
   - **Input cho AI:**
     - Xu hướng từ RSS/Reddit.
     - Lịch sử video của kênh.
     - Mô hình thành công (từ tuần trước).

5. **Data Table Nodes**
   - **Sheet Name:** Đặt tên rõ ràng (ví dụ: `YouTube_Shorts_Viral_Scoring`).
   - **Columns cần có:**
     - `Video_ID`, `Title`, `Views`, `Likes`, `Comments`, `Tags`, `Publish_Date`.
     - `Trend_Source` (RSS/Reddit), `Viral_Score`, `Recommendation_Status`.

6. **Telegram Delivery**
   - **Format tin nhắn:** Sử dụng node **Code – Format output** để định dạng kết quả.
   - **Gửi Top 3 đề tài** với:
     - Tiêu đề.
     - Điểm viral (0-100).
     - Link nguồn (RSS/Reddit).
     - Gợi ý tags phù hợp.

---
#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chạy node **Trigger – Daily Trend Scan** và kiểm tra:
     - AI có trả về Top 3 đề tài không?
     - Telegram có nhận được thông báo không?
     - Data Table có cập nhật dữ liệu không?
2. **Bật Active** sau khi kiểm tra thành công.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối Slack/Email**
   - Thay vì chỉ Telegram, các sếp có thể **gửi báo cáo hàng tuần qua Slack** hoặc **email** bằng node **email** của n8n.
   - **Cách làm:**
     - Thêm node **HTTP Request** để gọi API của Slack/Email.
     - Sử dụng **Webhook** của Slack hoặc **SMTP** cho email.

2. **Lưu Log & Audit**
   - Thêm node **Sticky Note** để ghi lại:
     - Lịch sử đề tài đã lọc.
     - Lý do đề tài bị loại (nếu AI cho điểm thấp).
   - **Cách làm:**
     - Sử dụng node **Set** để lưu log vào Data Table.
     - Tạo **báo cáo tháng** tự động bằng **Google Data Studio**.

3. **Cập Nhật Mô Hình AI**
   - Nếu muốn cải tiến AI, các sếp có thể:
     - **Thêm prompt mới** vào node **agent**.
     - **Sử dụng mô hình AI khác** (ví dụ: Mistral, Llama 3) thay cho DeepSeek.
   - **Cách làm:**
     - Mở node **OpenRouter Chat Model** và thay đổi `model` thành `mistral/mistral-7b`.
     - Sửa prompt trong node **agent** để phù hợp với mô hình mới.

4. **Tự Động Chỉnh Sửa Tiêu Đề Video**
   - Sau khi AI lọc ra đề tài, các sếp có thể **tự động tạo tiêu đề viral** bằng:
     - Node **Code** để format tiêu đề.
     - Node **YouTube Video Upload** (nếu kết hợp với API YouTube).
   - **Cách làm:**
     - Sử dụng node **Set** để tạo tiêu đề từ xu hướng.
     - Thêm node **HTTP Request** để gọi API YouTube tạo video.

---
### 📌 **Kết Luận**
Workflow này **không chỉ là công cụ tự động hóa**, mà là **công cụ học tập và tối ưu hóa nội dung** cho kênh YouTube của các sếp. Thay vì **chạy theo xu hướng**, nó **học từ dữ liệu thực tế** và **gợi ý đề tài phù hợp nhất** với kênh.

**Hành động ngay:**
1. **Import workflow** và cấu hình API.
2. **Chạy thử** với kênh YouTube của mình.
3. **Tối ưu hóa** bằng cách thêm Slack/Email hoặc cải tiến AI.

**🎁 Đăng ký VPS cho n8n 24/7:**
:::info[**Hạ Tầng Chắc Chắn**]
Để workflow chạy **ổn định 24/7**, các sếp nên **self-host n8n** trên VPS.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%).
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

**Chúc các sếp thành công với kênh YouTube viral!** 🚀🎥