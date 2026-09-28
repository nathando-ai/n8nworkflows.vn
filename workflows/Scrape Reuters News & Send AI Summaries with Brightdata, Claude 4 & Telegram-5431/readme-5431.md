---
title: "🚀 Tự Động Hoàn Thành: Scrape Tin Tức Reuters & Gửi Tóm Tắt AI qua Telegram (Brightdata + Claude 4)"
description: "Workflow tự động hóa lấy tin tức Reuters theo từ khóa, tóm tắt bằng Claude 4 và gửi kết quả qua Telegram - tiết kiệm 10+ giờ công mỗi tuần cho các sếp nghiên cứu thị trường."
slug: "tieu-dong-hoan-thanh-scrape-reuters-va-tom-tat-ai-telegram"
tags: [n8n, automation, ai-summarization, market-research, brightdata, claude-4, telegram-bot]
keywords: [tự động hóa lấy tin tức Reuters, Claude 4 tóm tắt tin tức, Brightdata API, n8n workflow AI, tự động hóa nghiên cứu thị trường]
---

# 🚀 **Scrape Reuters News & Send AI Summaries với Brightdata + Claude 4 + Telegram**

### **Giải pháp tự động hóa hoàn chỉnh cho các sếp nghiên cứu thị trường**
Hàng ngày, các sếp phải mất **giờ đồng hồ** để:
- Tìm kiếm tin tức Reuters theo từ khóa cụ thể (dầu khí, công nghệ, chính trị...)
- Lọc và đọc hàng chục bài viết dài để tóm tắt nội dung chính
- Gửi kết quả cho đội ngũ hoặc khách hàng

**Workflow này tự động hóa toàn bộ quy trình trong 3 bước:**
1️⃣ **Scrape tin tức Reuters** theo từ khóa và loại tin tức (thời gian thực)
2️⃣ **Tóm tắt bằng Claude 4** (AI mạnh nhất hiện nay) với độ chính xác cao
3️⃣ **Gửi kết quả qua Telegram** ngay lập tức

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 10+ giờ công/tuần** - Không cần tìm kiếm thủ công
✅ **Tóm tắt tin tức chính xác** - Claude 4 hiểu ngữ cảnh và rút gọn nội dung hiệu quả
✅ **Cập nhật thời gian thực** - Scrape tin tức mới nhất từ Reuters
✅ **Gửi kết quả tự động** - Không cần copy/paste qua Telegram
✅ **Hoạt động 24/7** - Không phụ thuộc vào giờ làm việc
:::

---
### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
- **Tài khoản Brightdata** (để scrape Reuters):
  - [Đăng ký Brightdata](https://brightdata.com/) (mã giảm giá: **BRIGHTDATA10** - giảm 10%)
  - **Proxy Residential** (gói từ 500$+/tháng)
- **API Key Claude 4 (Anthropic)**:
  - [Đăng ký Anthropic](https://www.anthropic.com/) (gói Claude 4)
- **Token Telegram Bot**:
  - Tạo bot tại [@BotFather](https://t.me/BotFather) và lấy `API Token`
- **Chat ID Telegram** (để nhận kết quả)
- **n8n Self-hosted** (không dùng phiên bản cloud)
:::

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Phương pháp 1**: Tải file JSON từ [n8n.io/workflows/5431](https://n8n.io/workflows/5431) và import vào n8n Editor
- **Phương pháp 2**: Copy toàn bộ JSON từ link trên và paste vào **Import Workflow** trong n8n

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình Credentials**
| Node | Tham số cần thiết | Ghi chú |
|------|-------------------|---------|
| **Anthropic Chat Model** | `anthropicApi` | Điền `API Key` từ Anthropic |
| **Telegram** | `telegramApi` | Điền `Token` từ BotFather |
| **HTTP Request (Brightdata)** | `Proxy URL` | Cấu hình từ Brightdata Dashboard |

##### **B. Cấu hình Node "On form submission"**
- **Trigger**: Khi form được submit với 2 trường bắt buộc:
  - `Keywords` (ví dụ: "dầu khí", "AI")
  - `News Type` (ví dụ: "Business", "Technology")

##### **C. Cấu hình Node "MCP for Data Fetching" (LangChain Agent)**
- **Prompt mẫu**:
  ```json
  {
    "input": {
      "keywords": "{{ $node["On form submission"].json["keywords"] }}",
      "news_type": "{{ $node["On form submission"].json["news_type"] }}"
    },
    "actions": [
      {
        "name": "scrape_reuters",
        "description": "Scrape Reuters news by keyword",
        "parameters": {
          "keywords": "$input.keywords",
          "news_type": "$input.news_type"
        }
      }
    ]
  }
  ```

##### **D. Node "Data Formatting" (Code)**
- **Mã JavaScript cần chỉnh sửa** (lấy từ node này):
  ```javascript
  // Chỉ giữ lại các trường cần thiết (tựa đề, nội dung, ngày đăng)
  const formattedData = {
    title: item.title,
    summary: item.summary, // Claude 4 sẽ tự tóm tắt
    date: item.date,
    source: "Reuters"
  };
  return formattedData;
  ```

##### **E. Node "sleep tool"**
- Thời gian chờ mặc định là **60 giây** (đảm bảo Brightdata hoàn thành scrape)

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Submit form với `Keywords = "AI"` và `News Type = "Technology"`
   - Kiểm tra Telegram có nhận được kết quả không
2. **Bật Active**:
   - Chuyển trạng thái workflow từ `Inactive` sang `Active`

---
### ✍️ **Mẹo & gợi ý nâng cao**
:::note[CẬP NHẬT THỜI GIAN SCRAPE]
- **Optimize Brightdata**:
  - Sử dụng **Snapshot API** thay vì scrape liên tục để tiết kiệm proxy
  - Thiết lập **thời gian chờ tối thiểu 2 phút** giữa các request
:::

:::tip[KẾT HỢP VỚI SLACK]
- Thay vì Telegram, các sếp có thể gửi kết quả qua **Slack** bằng node `n8n-nodes-base.slack`
- **Mẫu message**:
  ```json
  {
    "text": `📰 Tin tức mới về {{ $node["On form submission"].json["keywords"] }}:\n\n{{ $node["Data Formatting"].json["summary"] }}`,
    "attachments": [
      {
        "title": "{{ $node["Data Formatting"].json["title"] }}",
        "text": `📅 {{ $node["Data Formatting"].json["date"] }}`,
        "mrkdwn_in": ["text", "pretext"]
      }
    ]
  }
  ```
:::

:::info[LƯU LOG & BÁO CÁO]
- **Node StickyNote**: Lưu lại lịch sử scrape và tóm tắt để phân tích sau
- **Node Email (n8n-nodes-base.email)**: Gửi báo cáo hàng tuần cho team
:::

---
### 📌 **Kết luận**
Workflow này **giải phóng hoàn toàn thời gian** của các sếp để tập trung vào phân tích sâu hơn thay vì tìm kiếm tin tức thủ công. Với **Claude 4** và **Brightdata**, độ chính xác và tốc độ xử lý được tối ưu hóa.

**Hành động ngay!**
1. **Đăng ký Brightdata** (mã giảm giá **BRIGHTDATA10**)
2. **Cài n8n Self-hosted** (VPS TinoHost với mã **VPSN8N**)
3. **Import workflow** và bắt đầu tự động hóa!

👉 [Tải workflow ngay](https://n8n.io/workflows/5431) và **tiết kiệm 10+ giờ/tuần**!