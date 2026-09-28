---
title: "🚀 Tự Động Hóa Phát Triển Thông Tin Khách Hàng Cuộc Họp với Apollo.io & Google Sheets (N8n)"
description: "Workflow tự động hóa hoàn toàn không cần code để enrich thông tin khách hàng tham dự cuộc họp từ Calendly/Cal.com, tra cứu trên Apollo.io, và cập nhật tự động vào Google Sheets. Giúp các sếp tiết kiệm 10+ giờ/tháng và nâng cao chất lượng lead."
slug: "tieu-dong-hoa-phat-trien-thong-tin-khach-hang-cuoc-hop"
tags: [n8n, automation, lead-generation, google-sheets, apollo-io, calendly, calcom]
keywords: [tự động hóa cuộc họp, enrich lead, apollo io n8n, google sheets automation, calendly api, tự động hóa bán hàng]
---

# 🚀 **Tự Động Hóa Phát Triển Thông Tin Khách Hàng Cuộc Họp với Apollo.io & Google Sheets**

## **🔍 Nỗi Đau Của Các Sếp**
Bạn có bao giờ phải:
- **Lặp đi lặp lại** tra cứu thông tin khách hàng từ cuộc họp trên nhiều nền tảng khác nhau?
- **Tốn thời gian** nhập liệu thủ công vào Google Sheets sau mỗi cuộc họp?
- **Mất lead** vì không biết thông tin chi tiết của khách hàng (địa chỉ email, công ty, vị trí,…)?

Workflow này **giải quyết tất cả** bằng cách tự động:
✅ **Nhận thông tin khách hàng** từ Calendly/Cal.com
✅ **Tra cứu & enrich** thông tin trên Apollo.io (tên công ty, vị trí, email,…)
✅ **Cập nhật tự động** vào Google Sheets với định dạng chuyên nghiệp
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** cho việc tra cứu và nhập liệu thủ công.
- **Nâng cao chất lượng lead** với thông tin chi tiết từ Apollo.io.
- **Cập nhật tự động** vào Google Sheets, không lo mất dữ liệu.
- **Hoạt động liên tục** ngay cả khi bạn ngủ.
- **Dễ dàng mở rộng** cho nhiều cuộc họp khác nhau.
:::

---
## **🔧 Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
### **📌 Tài Khoản & API Keys**
| **Dịch Vụ**       | **Liên Hệ** | **Ghi Chú** |
|-------------------|-------------|------------|
| **Calendly**      | [Tạo API Key](https://calendly.com/integrations/api_webhooks) | Cần **Webhook URL** từ n8n |
| **Cal.com**       | [Tạo API Key](https://app.cal.com/settings/developer/api-keys) | Cần **API Key** |
| **Apollo.io**     | [Tạo Token](https://console.apify.com/settings/integrations) | Cần **Apify Token** (để scrape Apollo.io) |
| **Google Sheets** | [Tạo OAuth2](https://developers.google.com/sheets/api/quickstart/python) | Cần **File Google Sheets** (sử dụng template dưới đây) |

### **📄 File Google Sheets Template**
- **Copy template** từ [đây](https://docs.google.com/spreadsheets/d/1TAFZwx7vo9FmzZVXB8S5qWjVUt7T4Lzvje1VVxP_LPY/edit?usp=sharing)
- **Tên Sheet**: Đặt tên theo yêu cầu (ví dụ: `Meeting Attendees Enrichment`)

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương Pháp 1: Import từ File JSON**
1. **Tải workflow** từ [n8n.io](https://n8n.io/workflows/5892) (ấn **Export**).
2. **Mở n8n Editor** → **Import** → Chọn file JSON vừa tải.
3. **Chọn Workspace** (nếu có nhiều workspace).

#### **Phương Pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ JSON** từ [n8n.io](https://n8n.io/workflows/5892) (ấn **Export** → **Copy JSON**).
2. **Mở n8n Editor** → **Create New Workflow** → **Paste JSON**.
3. **Xác nhận** và bắt đầu cấu hình.

---
### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **🔹 Cấu Hình Calendly & Cal.com Trigger**
- **Calendly Trigger**:
  - **Credentials**: Chọn `calendlyApi` (đã cấu hình trước).
  - **Webhook URL**: N8n sẽ tự động tạo, **không cần thay đổi**.
  - **Event Type**: Chọn `Event Created` (hoặc `Event Updated` nếu cần).

- **Cal.com Trigger**:
  - **Credentials**: Chọn `calApi` (đã cấu hình trước).
  - **Event Type**: Chọn `Event Created` (hoặc `Event Rescheduled`).

#### **🔹 Cấu Hình Apollo.io Scrape**
- **Node `Scrape Apollo`**:
  - **Method**: `GET`
  - **URL**: `https://api.apollo.io/v2/search`
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_APOLLY_TOKEN",
      "Content-Type": "application/json"
    }
    ```
  - **Body (JSON)**:
    ```json
    {
      "query": "firstName:{{$json["firstName"]}} lastName:{{$json["lastName"]}}",
      "limit": 10
    }
    ```
  - **Lưu ý**:
    - Thay `YOUR_APOLLY_TOKEN` bằng **Apify Token** từ Apollo.io.
    - **Tham số `$json["firstName"]` và `$json["lastName"]`** sẽ được lấy từ thông tin khách hàng trong cuộc họp.

#### **🔹 Cấu Hình Google Sheets**
- **Node `Google Sheets1` (Lưu thông tin cuộc họp)**:
  - **Credentials**: Chọn `googleSheetsOAuth2Api`.
  - **Sheet Name**: Đặt tên theo template (ví dụ: `Meeting Log`).
  - **Range**: `Sheet1!A1` (hoặc tùy chỉnh theo cột bạn muốn cập nhật).

- **Node `Google Sheets2` (Lưu thông tin enrich)**:
  - **Credentials**: Chọn `googleSheetsOAuth2Api`.
  - **Sheet Name**: Đặt tên khác (ví dụ: `Enriched Leads`).
  - **Range**: `Sheet1!A1` (hoặc tùy chỉnh).

#### **🔹 Node `If Data available?` (Lọc dữ liệu Apollo.io)**
- **Condition**:
  - Kiểm tra nếu `data` từ Apollo.io **không rỗng**.
  - Nếu có dữ liệu, cập nhật vào Google Sheets.

---
### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Tạo một cuộc họp giả trên Calendly/Cal.com.
   - Kiểm tra **Log entry** trong Google Sheets xem có cập nhật không.
2. **Bật Active**:
   - Đảm bảo tất cả **credentials** đều đúng.
   - **Active workflow** và **bật trigger** (Calendly/Cal.com).

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **🔹 Kết Nối với Slack/Telegram**
- **Thêm node `Slack`** sau `Google Sheets2` để thông báo khi có lead mới:
  ```json
  {
    "type": "slack",
    "credentials": ["slackApi"],
    "operation": "postMessage",
    "parameters": {
      "channel": "#leads",
      "text": "🚀 Lead mới enrich: {{$json["company"]}} - {{$json["email"]}}"
    }
  }
  ```

### **🔹 Lưu Log Dữ Liệu**
- **Thêm node `Set`** trước `Google Sheets` để lưu log:
  ```json
  {
    "name": "Log Data",
    "type": "set",
    "parameters": {
      "data": {
        "timestamp": "{{$now}}",
        "meetingId": "{{$json["meetingId"]}}",
        "attendee": "{{$json["attendee"]}}"
      }
    }
  }
  ```

### **🔹 Gửi Báo Cáo Định Kỳ**
- **Sử dụng node `HTTP Request`** kết hợp với **Google Apps Script** để gửi báo cáo hàng tuần qua email.

---
## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc tra cứu và nhập liệu thủ công, đồng thời **nâng cao chất lượng lead** với thông tin chi tiết từ Apollo.io. **Chỉ cần 10 phút cấu hình**, bạn đã có một hệ thống tự động hóa hoàn chỉnh!

### **🚀 Bắt Đầu Ngay Hôm Nay!**
1. **Import workflow** từ [n8n.io](https://n8n.io/workflows/5892).
2. **Cấu hình API keys** theo hướng dẫn.
3. **Bật Active** và **nhận lead enrich tự động**!

**Cần hỗ trợ?** Liên hệ **GainFlow AI** qua:
📧 [Email](mailto:info.gainflow@gmail.com)
📄 [Đăng ký hỗ trợ](https://docs.google.com/forms/d/e/1FAIpQLSfIiXdw4HMcI2HM-Obng13j_RFiKv7X-mjOVm_mcy2ucRA8EA/viewform)

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💡 Lưu ý cuối cùng**: Nếu gặp khó khăn, **không ngần ngại liên hệ GainFlow AI** – họ sẽ hỗ trợ miễn phí! 🚀