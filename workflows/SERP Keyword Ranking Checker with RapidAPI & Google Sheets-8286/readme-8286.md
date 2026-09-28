---
title: "🚀 Tự động hóa kiểm tra xếp hạng từ khóa SERP với RapidAPI & Google Sheets"
description: "Tự động hóa quy trình theo dõi xếp hạng từ khóa trên Google với n8n, lưu kết quả vào Google Sheets - giải pháp hoàn hảo cho SEO và marketing số"
slug: "tu-dong-hoa-kiem-tra-xep-hang-tu-khoa-serp"
tags: [n8n, automation, no-code, seo, google-sheets]
keywords: [n8n workflow, tự động hóa, xếp hạng từ khóa, google sheets, seo]
---

# 🚀 Tự động hóa kiểm tra xếp hạng từ khóa SERP với RapidAPI & Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp SEO khi phải theo dõi thủ công xếp hạng từ khóa trên nhiều quốc gia. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể trong việc theo dõi xếp hạng từ khóa
- Dữ liệu được cập nhật tự động vào Google Sheets hàng ngày
- Theo dõi được xu hướng xếp hạng từ khóa trên nhiều quốc gia
- Tự động báo cáo khi không tìm thấy kết quả
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập vào Google Sheets
- API Key từ RapidAPI (SERP Keyword Ranking Checker)
- Biết cách tạo và cấu hình Google Sheets API credentials trong n8n
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **On form submission**: Cấu hình form với 2 trường bắt buộc là "Keyword" và "Country"
- **Global Storage**: Không cần cấu hình, node này tự động lưu trữ dữ liệu từ form
- **SERP Keyword Ranking Checker**:
  - Chọn credentials RapidAPI đã cấu hình
  - Điền URL endpoint: `https://serp-keyword-ranking-checker.p.rapidapi.com/serp.php`
  - Cấu hình headers:
    ```
    x-rapidapi-key: {{$credentials.rapidApi.apiKey}}
    x-rapidapi-host: serp-keyword-ranking-checker.p.rapidapi.com
    Content-Type: application/x-www-form-urlencoded
    ```
  - Body: `keyword={{$node["On form submission"].json["data"]["Keyword"]}}&country={{$node["On form submission"].json["data"]["Country"]}}`
- **If**: Cấu hình điều kiện kiểm tra: `{{$node["SERP Keyword Ranking Checker"].json.body}} !== null`
- **Google Sheets** (node đầu tiên):
  - Chọn credentials Google Sheets đã cấu hình
  - Chọn operation: "Append"
  - Cấu hình các tham số:
    ```
    Spreadsheet ID: [ID của Google Sheet của bạn]
    Sheet Name: [Tên sheet cần ghi dữ liệu]
    Data: [
      {
        "Keyword": "{{$node["On form submission"].json["data"]["Keyword"]}}",
        "Country": "{{$node["On form submission"].json["data"]["Country"]}}",
        "Status": "No result found"
      }
    ]
    ```
- **Wait**: Cấu hình thời gian chờ 5 giây
- **Google Sheets** (node thứ hai):
  - Chọn credentials Google Sheets đã cấu hình
  - Chọn operation: "Append"
  - Cấu hình các tham số:
    ```
    Spreadsheet ID: [ID của Google Sheet của bạn]
    Sheet Name: [Tên sheet cần ghi dữ liệu]
    Data: [
      {
        "Keyword": "{{$node["On form submission"].json["data"]["Keyword"]}}",
        "Country": "{{$node["On form submission"].json["data"]["Country"]}}",
        "Position": "{{$node["SERP Keyword Ranking Checker"].json.body.position}}",
        "URL": "{{$node["SERP Keyword Ranking Checker"].json.body.url}}",
        "Status": "Found"
      }
    ]
    ```
- **Wait1**: Cấu hình thời gian chờ 5 giây

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi xếp hạng từ khóa thay đổi
- Thêm node gửi email báo cáo hàng tuần với dữ liệu từ Google Sheets
- Tạo nhiều form khác nhau để theo dõi nhiều từ khóa và quốc gia khác nhau
- Thêm node lưu log hoạt động vào Google Sheets để theo dõi lịch sử kiểm tra

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc theo dõi xếp hạng từ khóa trên Google. Dữ liệu được cập nhật tự động vào Google Sheets hàng ngày, giúp việc phân tích và báo cáo trở nên dễ dàng hơn. Hãy áp dụng ngay để tối ưu hóa chiến lược SEO của bạn!