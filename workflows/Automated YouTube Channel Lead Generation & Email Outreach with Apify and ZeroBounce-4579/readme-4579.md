---
title: "🚀 Tự Động Hóa Theo Dõi Ranking Keyword YouTube & Email Outreach với Apify & ZeroBounce (n8n)"
description: "Workflow tự động hóa theo dõi xếp hạng keyword từ Airtable, so sánh với dữ liệu mới từ Firecrawl API, cập nhật tự động và thông báo ngay khi có thay đổi trên Slack. Giúp các sếp SEO tiết kiệm thời gian và tối ưu chiến lược nội dung."
slug: "tieu-dong-hoa-theo-doi-ranking-keyword-youTube"
tags: [n8n, automation, seo, airtable, slack, api, seo-automation]
keywords: [n8n workflow seo, tự động hóa theo dõi keyword, firecrawl api, airtable automation, alert seo ranking]
---

# 🚀 **Tự Động Hóa Theo Dõi Ranking Keyword & Thông Báo Thay Đổi Trên Slack (n8n)**

## 🔍 **Nỗi Đau Của Các Sếp SEO**
Hàng ngày, các sếp SEO phải **tốn thời gian thủ công** để:
- Theo dõi xếp hạng keyword trên Google/YouTube.
- So sánh dữ liệu cũ với mới để phát hiện thay đổi.
- Cập nhật thủ công vào bảng Airtable.
- Thông báo cho team khi có sự thay đổi quan trọng.

**Kết quả?** Thời gian bị "chôn vùi" trong công việc lặp lại, còn chiến lược SEO không được tối ưu kịp thời.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** theo dõi thủ công.
- **Cập nhật tự động** xếp hạng keyword vào Airtable.
- **Thông báo ngay** khi có thay đổi trên Slack (đã tăng/giảm rank).
- **Dữ liệu chính xác** từ API Firecrawl (không phụ thuộc vào công cụ thủ công).
- **Hoạt động 24/7** mà không cần can thiệp.
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Airtable Account** với:
   - Một bảng chứa các keyword (cột: `Keyword`, `Target URL`, `Current Rank`).
   - **Token API Airtable** (tạo tại [Airtable API Docs](https://airtable.com/api)).
2. **Slack Workspace** với:
   - **Token API Slack** (tạo tại [Slack API](https://api.slack.com/)).
   - Một channel để nhận thông báo.
3. **Firecrawl API Key** (miễn phí tại [Firecrawl](https://firecrawl.dev/)).
4. **n8n Workflow Editor** (cài đặt tại [n8n.io](https://n8n.io/)).

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n Workflow](https://n8n.io/workflows/4579) hoặc copy toàn bộ JSON từ [đây](https://github.com/n8n-io/workflows/blob/main/workflows/4579.json).
- Mở **n8n Editor** → Nhấn `Import` → Dán JSON hoặc tải file JSON.
- **Không cần chỉnh sửa** cấu trúc cơ bản, chỉ cần cấu hình credentials sau.

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
#### **A. Cấu Hình Airtable Trigger (`Fetch Keywords from Airtable`)**
- **Credentials**: Chọn `airtableTokenApi` (đã tạo trước).
- **Table Name**: Nhập tên bảng Airtable chứa keyword (ví dụ: `Keyword_Tracker`).
- **View Name**: Chọn view để lấy dữ liệu (nếu có).
- **Fields**: Chắc chắn chọn:
  - `Keyword` (text)
  - `Target URL` (text)
  - `Current Rank` (number)

#### **B. Cấu Hình HTTP Request (`Check Rank via Firecrawl`)**
- **URL**: `https://api.firecrawl.dev/v1/search`
- **Method**: `POST`
- **Headers**:
  - `Authorization`: `Bearer <FIRECRAWL_API_KEY>` (điền key từ Firecrawl).
  - `Content-Type`: `application/json`
- **Body (JSON)**:
  ```json
  {
    "keyword": "{{$node["Fetch Keywords from Airtable"].json["Keyword"]}}",
    "country": "US",  // Thay đổi theo nhu cầu
    "language": "en"
  }
  ```
  - `$node["Fetch Keywords from Airtable"].json["Keyword"]` là biến lấy từ Airtable.

#### **C. Cấu Hình Code Node (`Compare Ranks`)**
- **Code JavaScript**:
  ```javascript
  // Thêm field `rankChanged` vào dữ liệu
  $input.all().forEach(item => {
    const currentRank = item.Airtable.CurrentRank;
    const newRank = item.Firecrawl.newRank; // Giả sử Firecrawl trả về field này

    item.rankChanged = currentRank !== newRank;
    item.NewRank = newRank;
    item.RankChangedDate = new Date().toISOString();
  });
  ```
  - **Lưu ý**: Cần kiểm tra cấu trúc trả về từ Firecrawl để điều chỉnh tên field `newRank`.

#### **D. Cấu Hình Slack Notification (`Send Slack Notification`)**
- **Credentials**: Chọn `slackApi`.
- **Channel**: Nhập `#seo-alerts` (hoặc channel khác).
- **Message Format**:
  ```json
  {
    "text": `:bar_chart: Keyword *{{$node["Fetch Keywords from Airtable"].json["Keyword"]}}* đã thay đổi rank!\n
    🔗 URL: <{{$node["Fetch Keywords from Airtable"].json["Target URL"]}}|\
    {{$node["Fetch Keywords from Airtable"].json["Target URL"]}}>\n
    📊 Trước: *{{$node["Fetch Keywords from Airtable"].json["Current Rank"]}}*\n
    🆕 Sau: *{{$node["Compare Ranks"].json["NewRank"]}}*\n
    🕒 Thời gian: <{{$node["Compare Ranks"].json["RankChangedDate"]}}|{{$node["Compare Ranks"].json["RankChangedDate"]}}>`,
    "blocks": [
      {
        "type": "section",
        "text": {
          "type": "mrkdwn",
          "text": ":bell: *Thông báo xếp hạng keyword đã thay đổi!*"
        }
      },
      {
        "type": "divider"
      },
      {
        "type": "section",
        "fields": [
          {
            "type": "mrkdwn",
            "text": "*Keyword:*"
          },
          {
            "type": "mrkdwn",
            "text": "{{$node["Fetch Keywords from Airtable"].json["Keyword"]}}"
          }
        ]
      },
      {
        "type": "section",
        "fields": [
          {
            "type": "mrkdwn",
            "text": "*Trước:*"
          },
          {
            "type": "mrkdwn",
            "text": "{{$node["Fetch Keywords from Airtable"].json["Current Rank"]}}"
          }
        ]
      },
      {
        "type": "section",
        "fields": [
          {
            "type": "mrkdwn",
            "text": "*Sau:*"
          },
          {
            "type": "mrkdwn",
            "text": "{{$node["Compare Ranks"].json["NewRank"]}}"
          }
        ]
      }
    ]
  }
  ```

---

### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn `Run Workflow` và chọn một record từ Airtable để kiểm tra.
   - Kiểm tra Slack có nhận được thông báo không.
2. **Bật Active**:
   - Sau khi test thành công, chuyển trạng thái workflow sang `Active`.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Hợp với Email Outreach**:
   - Thêm node `n8n-nodes-base.email` để tự động gửi email cho team khi có rank tăng cao.
   - Ví dụ: Nếu `NewRank < CurrentRank`, gửi email với nội dung:
     ```json
     {
       "to": "team@example.com",
       "subject": "🎉 Keyword *{{$node["Keyword"]}}* đã tăng rank!",
       "text": "Keyword *{{$node["Keyword"]}}* đã tăng từ *{{$node["CurrentRank"]}}* lên *{{$node["NewRank"]}}*!"
     }
     ```

2. **Lưu Log Lịch Sử**:
   - Thêm node `n8n-nodes-base.googleSheets` để ghi lịch sử thay đổi vào Google Sheets.
   - Cấu hình:
     - **Spreadsheet ID**: ID của file Google Sheets.
     - **Range**: `Sheet1!A1` (để ghi dữ liệu mới vào hàng mới).

3. **Thông Báo qua Telegram**:
   - Thay thế node Slack bằng `n8n-nodes-base.telegram` để nhận thông báo trên Telegram.
   - Cấu hình:
     - **Token API Telegram**: Tạo tại [BotFather](https://t.me/BotFather).
     - **Chat ID**: ID của chat nhóm/private (tìm bằng cách gửi tin nhắn cho bot và copy link).

4. **Tự Động Cập Nhật Airtable với Chi Tiết**:
   - Trong node `Update Airtable Record`, thêm các field như:
     - `Notes`: `"Rank đã thay đổi do update algorithm Google."`
     - `LastUpdated`: `{{$node["Compare Ranks"].json["RankChangedDate"]}}`

---

## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp SEO để tập trung vào chiến lược nội dung và content marketing thay vì công việc lặp lại. Với **tự động hóa theo dõi ranking**, cập nhật Airtable và thông báo Slack**, các sếp có thể:
✅ **Nhận thông báo ngay** khi có thay đổi quan trọng.
✅ **Cập nhật dữ liệu chính xác** mà không cần thủ công.
✅ **Tối ưu chiến lược SEO** dựa trên dữ liệu thời gian thực.

**Hành động ngay!** Import workflow này và **bắt đầu theo dõi ranking 24/7** mà không cần can thiệp.

---
**Cần hỗ trợ?** Liên hệ với tác giả Yaron Been qua:
- [LinkedIn](https://www.linkedin.com/in/yaronbeen/)
- Email: Yaron@nofluff.online
- YouTube: [@YaronBeen](https://www.youtube.com/@YaronBeen/videos)