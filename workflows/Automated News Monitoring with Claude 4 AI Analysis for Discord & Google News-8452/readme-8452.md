---
title: "🚀 Tự Động Hóa Theo Dõi Tin Tức Tối Tiến Với AI Claude 4 + Discord (Không Cần Code)"
description: "Workflow tự động hóa theo dõi tin tức từ Google News, phân tích sâu bằng AI Claude 4 Sonnet, và gửi báo cáo định kỳ lên Discord với định dạng chuyên nghiệp. Giúp các sếp tiết kiệm 10+ giờ/tuần theo dõi thị trường, cạnh tranh và cập nhật thông tin thời gian thực."
slug: "tieu-dong-ho-tin-tuc-voi-claude-4-discord"
tags: [n8n, automation, ai-summarization, google-news, discord-bot, self-hosted]
keywords: [n8n workflow tin tức, tự động hóa theo dõi tin tức, Claude 4 AI, báo cáo thị trường tự động, Discord bot tin tức, SerpAPI Firecrawl]
---

# 🚀 **Tự Động Hóa Theo Dõi Tin Tức Tối Tiến Với AI Claude 4 + Discord (Không Cần Code)**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp**
Hàng ngày, các sếp phải mất **10-15 giờ** để:
- Theo dõi tin tức từ nhiều nguồn khác nhau (Google News, website chuyên ngành, báo chí).
- Lọc ra những tin tức **có giá trị thực sự** trong luồng thông tin dồi dào.
- Tóm tắt và phân tích nội dung để **cập nhật cho đội ngũ** một cách hiệu quả.
- Gặp khó khăn khi **gửi báo cáo định kỳ** lên Discord/Slack vì giới hạn ký tự hoặc định dạng không chuyên nghiệp.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động hóa theo dõi tin tức** từ Google News theo chủ đề đã chỉ định (được quản lý trên Google Sheets).
✅ **Phân tích sâu bằng AI Claude 4 Sonnet** để tóm tắt, trích xuất **khái niệm chính** và **đánh giá tác động** của mỗi tin tức.
✅ **Gửi báo cáo định kỳ lên Discord** với định dạng chuyên nghiệp, chia nhỏ thành nhiều tin nhắn (tuân thủ giới hạn 2000 ký tự của Discord).
✅ **Cập nhật tự động hàng tuần** (hoặc theo lịch bạn thiết lập) mà **không cần can thiệp thủ công**.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10-15 giờ/tuần** theo dõi tin tức thủ công.
- **Cập nhật thông tin thị trường thời gian thực** với phân tích AI chuyên nghiệp.
- **Báo cáo định kỳ tự động** lên Discord với định dạng sạch sẽ, dễ đọc.
- **Theo dõi nhiều chủ đề cùng lúc** (kinh doanh, công nghệ, tài chính, du lịch...) mà không lo bỏ lỡ tin tức quan trọng.
- **Tăng cường cạnh tranh** bằng thông tin phân tích sâu từ AI Claude 4.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n Self-hosted** (cài trên VPS để chạy 24/7).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

2. **Các API Key & Credentials sau:**
   | Dịch vụ/API          | Mô tả                                                                 | Lấy tại |
   |----------------------|-------------------------------------------------------------------------|---------|
   | **SerpAPI**          | API để lấy tin tức từ Google News.                                     | [serpapi.com](https://serpapi.com/) |
   | **Firecrawl**        | API để trích xuất nội dung đầy đủ từ bài viết.                        | [firecrawl.io](https://firecrawl.io/) |
   | **Anthropic (Claude)** | API Claude 4 Sonnet để phân tích và tóm tắt tin tức.                  | [anthropic.com](https://www.anthropic.com/) |
   | **Google Sheets**     | Để lưu trữ danh sách **query** (từ khóa theo dõi).                     | [Google Workspace](https://workspace.google.com/) |
   | **Discord Bot**      | Bot Discord để gửi báo cáo tự động.                                   | [Discord Developer Portal](https://discord.com/developers/applications) |

3. **Google Sheets cấu trúc:**
   - Tạo một bảng mới với **Sheet tên "Query"** và cột:
     - `Query` (vd: "tin tức thị trường công nghệ Việt Nam")
     - `Frequency` (vd: "weekly" - theo tuần)
   - Mỗi hàng là một chủ đề theo dõi.

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/8452](https://n8n.io/workflows/8452) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/8452) và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **16 node**, nhưng các node quan trọng cần cấu hình kỹ như sau:

##### **🔹 Node 1: Schedule Trigger (Lịch Triggers)**
- **Cấu hình:**
  - Chọn **cron expression** phù hợp (vd: `0 9 * * 1` để chạy hàng tuần thứ 2 lúc 9h sáng).
  - **Lưu ý:** Nếu muốn chạy hàng ngày, thay bằng `0 9 * * *`.

##### **🔹 Node 2: Get Query (Lấy Query từ Google Sheets)**
- **Cấu hình:**
  - Chọn **credentials**: `googleSheetsOAuth2Api`.
  - Điền **Sheet Name**: `Query`.
  - Chọn **Range**: `A1:B` (giả sử cột A là `Query`, cột B là `Frequency`).

##### **🔹 Node 3-5: Search GNews & Scrape Article (Theo Dõi & Trích Xuất Tin Tức)**
- **Cấu hình SerpAPI (`Search GNews`):**
  - **Credentials**: `serpApi`.
  - **Key Parameters**:
    - `q`: Được lấy từ `query` trong Google Sheets.
    - `hl`: `vi` (để lấy kết quả tiếng Việt).
    - `gl`: `vn` (địa lý Việt Nam).
  - **Lưu ý:** Nếu API rate limit, tăng `num` từ 10 xuống 5 để giảm tải.

- **Cấu hình Firecrawl (`Scrape article 1/2/3`):**
  - **Credentials**: `firecrawlApi`.
  - **Key Parameters**:
    - `url`: Được lấy từ URL của bài viết (node `Return URL only`).
    - `selectors`: Cấu hình để lấy nội dung chính (vd: `body > article > p`).
  - **Lưu ý:** Nếu website có bảo vệ, Firecrawl sẽ tự động retry.

##### **🔹 Node 6: Anthropic Chat Model (Claude 4 Sonnet)**
- **Cấu hình:**
  - **Credentials**: `anthropicApi`.
  - **Model**: `claude-sonnet-4-20250514` (đã được thiết lập sẵn).
  - **Prompt mẫu** (có thể chỉnh sửa trong node `Rédaction veille`):
    ```
    Tóm tắt bài viết này trong 3 phần:
    1. Tóm tắt ngắn (1-2 câu).
    2. Khái niệm chính (3 điểm).
    3. Đánh giá tác động (nếu có).
    Đảm bảo nội dung chuyên nghiệp và không có sai lệch.
    ```

##### **🔹 Node 7-9: Discord Bot (Gửi Báo Cáo)**
- **Cấu hình:**
  - **Credentials**: `discordBotApi`.
  - **Key Parameters**:
    - `channelId`: ID của channel Discord muốn gửi báo cáo.
    - **Content**: Được lấy từ node `Découpage message discord` (đã chia nhỏ tin nhắn).
  - **Lưu ý:**
    - Bot cần quyền **send messages** trong channel.
    - Nếu tin nhắn quá dài, nó sẽ tự động chia nhỏ (tuân thủ giới hạn 2000 ký tự).

##### **🔹 Node 10-11: Aggregate & Code (Định Hình Báo Cáo)**
- **Node `Compilation données veilles` (Aggregate):**
  - Gộp tất cả tin tức theo chủ đề.
- **Node `Découpage message discord` (Code):**
  - Chia tin nhắn thành nhiều phần nếu quá dài.

---
#### **3. Kích Hoạt ⚡️**
1. **Test Run:**
   - Chạy **manual test** với một query mẫu (vd: "tin tức thị trường công nghệ").
   - Kiểm tra:
     - AI có tóm tắt đúng không?
     - Discord có nhận được báo cáo không?
2. **Bật Active:**
   - Sau khi test thành công, **bật node Schedule Trigger** để workflow chạy tự động.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[TIPS THỰC TIỆN]
1. **Thêm Slack/Telegram:**
   - Sử dụng node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram` để gửi báo cáo song song với Discord.

2. **Lưu Log:**
   - Thêm node `n8n-nodes-base.fileSystem` để lưu báo cáo vào Google Drive hoặc VPS.

3. **Báo Cáo Định Kỳ Email:**
   - Sử dụng node `n8n-nodes-base.email` để gửi báo cáo hàng tuần cho team.

4. **Tăng Cường AI:**
   - Chỉnh sửa **prompt** trong node Claude để phù hợp với ngành nghề (vd: phân tích thị trường tài chính, du lịch...).

5. **Theo Dõi Nhiều Chủ Đề:**
   - Thêm nhiều hàng vào Google Sheets để theo dõi **nhiều chủ đề cùng lúc** (kinh doanh, công nghệ, tài chính...).
:::

---
### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **quyết định chiến lược** thay vì mất công theo dõi tin tức thủ công. Với **AI Claude 4 Sonnet**, báo cáo không chỉ đơn giản là tóm tắt mà còn **phân tích sâu** về tác động của tin tức đến doanh nghiệp.

**Hành động ngay:**
1. **Cài n8n trên VPS** (đăng ký mã giảm giá **VPSN8N**).
2. **Import workflow** và cấu hình API.
3. **Bật lịch tự động** và bắt đầu nhận báo cáo hàng tuần!

**🚀 Cập nhật liên tục, cạnh tranh hiệu quả!**