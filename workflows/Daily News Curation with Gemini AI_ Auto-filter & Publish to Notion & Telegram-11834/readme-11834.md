---
title: "🌐 Tự Động Hóa Tóm Tắt Tin Tức Hàng Ngày với Gemini AI: Lọc & Xuất Báo Cáo Notion + Telegram (N8N)"
description: "Workflow tự động hóa lấy tin tức từ RSS/Reddit, tóm tắt bằng AI Gemini, lọc nội dung mới 24h, xuất báo cáo vào Notion và gửi thông báo Telegram - tiết kiệm 5+ giờ công mỗi ngày cho các sếp marketing & nghiên cứu thị trường."
slug: "tieu-dong-hoa-tom-tat-tin-tuc-hang-ngay-gemini-ai-notion-telegram"
tags: [n8n, automation, ai-summarization, notion, telegram, market-research, gemini-ai]
keywords: [n8n workflow tự động hóa tin tức, gemini ai tóm tắt tin tức, xuất báo cáo notion từ rss, tự động hóa nghiên cứu thị trường, tự động hóa telegram notification]
---

# 🚀 **Tự Động Hóa Tóm Tắt Tin Tức Hàng Ngày với Gemini AI: Lọc & Xuất Báo Cáo Notion + Telegram**

Hàng ngày, các sếp marketing, nghiên cứu thị trường hoặc quản lý nội dung phải mất **5-10 giờ** để:
- Quét nhiều nguồn tin tức (RSS, Reddit, blog, GitHub releases).
- Lọc nội dung mới và có giá trị trong vòng **24h**.
- Tóm tắt nội dung dài bằng trí tuệ nhân tạo.
- Xuất báo cáo vào Notion để theo dõi.
- Gửi thông báo Telegram cho team.

**Workflow này giải quyết tất cả vấn đề trên bằng AI Gemini + n8n, giúp các sếp:**
✅ **Tiết kiệm 80% thời gian** so với làm thủ công.
✅ **Chính xác 100%** với lọc tự động theo keyword và thời gian.
✅ **Cá nhân hóa** báo cáo với Notion và thông báo Telegram thực thời.
✅ **Hoạt động liên tục** 24/7 mà không cần can thiệp.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và độ tin cậy cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động lấy tin tức** từ 4 nguồn chính: n8n Blog, Community Announcements, GitHub Releases, và Reddit.
- **Lọc nội dung mới trong 24h** bằng logic tự động (không trùng lặp, không cũ).
- **Tóm tắt bằng AI Gemini** với chất lượng cao, tiết kiệm thời gian đọc.
- **Xuất báo cáo vào Notion** với định dạng chuyên nghiệp (dùng Database "Content DB").
- **Gửi thông báo Telegram** cho team khi có tin tức mới.
- **Hoạt động tự động hàng ngày** theo lịch trình (không cần kích hoạt thủ công).
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Notion** (để xuất báo cáo vào Database "Content DB").
2. **Tài khoản Telegram** (để gửi thông báo).
3. **API Key của Google Gemini** (đăng ký tại [Google AI Studio](https://aistudio.google/)).
4. **Credentials cho các nguồn RSS/HTTP**:
   - RSS Feed của n8n Blog (ví dụ: `https://n8n.io/blog/feed/`).
   - RSS Feed của Reddit (ví dụ: `https://www.reddit.com/r/n8n/.rss`).
   - URL API của GitHub Releases (ví dụ: `https://api.github.com/repos/n8n-io/n8n/releases/latest`).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/11834](https://n8n.io/workflows/11834) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ link trên và paste vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Dưới đây là **các node quan trọng** cần cấu hình:

##### **A. Cấu hình nguồn tin tức (RSS/HTTP)**
| Node | Tham số cần chỉnh | Ghi chú |
|------|-------------------|---------|
| **n8n Blog RSS** | `URL` | Điền URL RSS của blog n8n (ví dụ: `https://n8n.io/blog/feed/`). |
| **n8n Community Announcements** | `URL` | Điền URL RSS của nhóm Discord/Community (ví dụ: `https://discord.com/invite/rss`). |
| **GitHub n8n Releases** | `URL` | Điền `https://api.github.com/repos/n8n-io/n8n/releases/latest`. |
| **Reddit n8n News** | `URL` | Điền `https://www.reddit.com/r/n8n/.rss`. |

##### **B. Cấu hình AI Gemini (Tóm tắt tin tức)**
- **Node**: `Editor-in-Chief (AI Agent)`
- **Tham số cần chỉnh**:
  - `API Key`: Điền API Key của Google Gemini (tạo tại [Google AI Studio](https://aistudio.google/)).
  - `Prompt`: Sử dụng mặc định hoặc tùy chỉnh:
    ```json
    "Tóm tắt tin tức này trong 3 câu ngắn gọn, nhấn mạnh điểm mới và ý nghĩa cho n8n. Không bao gồm thông tin cũ hơn 24h."
    ```

##### **C. Cấu hình Notion (Xuất báo cáo)**
- **Node**: `Add to Notion (Content DB)`
- **Tham số cần chỉnh**:
  - **Database Name**: Điền tên Database Notion (ví dụ: `Content DB`).
  - **Properties**:
    - `Title`: `{{ $node["Parse & Chunk Output (Notion Guardrail)"].json["title"] }}`
    - `Summary`: `{{ $node["Editor-in-Chief (AI Agent)"].json["summary"] }}`
    - `Source`: `{{ $node["Merge All Sources"].json["source"] }}`
    - `Timestamp`: `{{ $node["Daily Schedule"].json["$date"] }}`

##### **D. Cấu hình Telegram (Gửi thông báo)**
- **Node**: `Telegram Notification`
- **Tham số cần chỉnh**:
  - **Bot Token**: Tạo bot Telegram tại [@BotFather](https://t.me/BotFather) và điền token.
  - **Chat ID**: Chat ID của nhóm/người nhận (lấy bằng cách gửi tin nhắn cho bot và copy link).
  - **Message Template**:
    ```json
    "Có {{ $node["Batch Items"].json["count"] }} tin tức mới trong 24h. Xem chi tiết tại Notion: [Notion Link]."
    ```

##### **E. Cấu hình lịch trình (Daily Schedule)**
- **Node**: `Daily Schedule`
- **Tham số cần chỉnh**:
  - **Time**: Chọn giờ muốn chạy (ví dụ: `09:00 AM`).
  - **Time Zone**: Chọn múi giờ phù hợp (ví dụ: `Asia/Ho_Chi_Minh`).

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chạy workflow với **1-2 tin tức mẫu** để kiểm tra:
     - AI có tóm tắt đúng không?
     - Notion có xuất báo cáo không?
     - Telegram có gửi thông báo không?
2. **Bật Active**:
   - Sau khi kiểm tra thành công, chuyển trạng thái workflow sang **Active**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tùy chỉnh keyword lọc**:
   - Trong node `Keyword Pre-filter`, các sếp có thể thêm logic lọc thêm (ví dụ: chỉ lấy tin tức liên quan đến `n8n`, `automation`, `AI`).
   - Ví dụ mã JavaScript:
     ```javascript
     return item.json.title.includes("n8n") || item.json.title.includes("automation");
     ```

2. **Lưu log hoạt động**:
   - Thêm node `stickyNote` để ghi log mỗi khi workflow chạy thành công/thất bại.
   - Ví dụ:
     ```json
     "Log: Workflow chạy thành công vào {{ $node["Daily Schedule"].json["$date"] }}."
     ```

3. **Gửi báo cáo định kỳ**:
   - Sử dụng node `scheduleTrigger` để chạy workflow **hàng tuần** (ví dụ: Chủ Nhật) để tổng hợp báo cáo tuần.

4. **Kết hợp với Slack**:
   - Thay vì Telegram, các sếp có thể gửi thông báo đến Slack bằng node `slack`.

5. **Tăng độ tin cậy với logic kiểm tra**:
   - Thêm node `if` để kiểm tra nếu AI Gemini trả về kết quả trống, workflow sẽ **dừng** và ghi log.

---

### 📌 **Kết luận**
Workflow **Daily News Curation with Gemini AI** là giải pháp **tự động hóa hoàn chỉnh** cho việc nghiên cứu thị trường, quản lý tin tức và xuất báo cáo. Với **Gemini AI**, các sếp không chỉ tiết kiệm thời gian mà còn **nhận được tin tức được tóm tắt và lọc chính xác**, xuất vào Notion và thông báo Telegram một cách tự động.

**Hành động ngay hôm nay**:
1. Import workflow vào n8n.
2. Cấu hình các node theo hướng dẫn.
3. **Bật Active** và bắt đầu tự động hóa!

👉 **Cần hỗ trợ?** Đăng ký VPS n8n tại [TinoHost](https://tino.vn/vps-n8n?affid=388) để chạy workflow 24/7 mà không lo gián đoạn!