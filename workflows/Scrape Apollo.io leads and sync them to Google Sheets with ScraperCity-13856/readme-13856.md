---
title: "🚀 Tự động scrape leads Apollo.io & đồng bộ Google Sheets với ScraperCity"
description: "Giải pháp không code giúp lấy dữ liệu lead từ Apollo.io qua ScraperCity và lưu ngay vào Google Sheets, tiết kiệm thời gian và tăng độ chính xác."
slug: "scrape-apollo-leads-google-sheets"
tags: [n8n, automation, no-code, lead-generation, google-sheets, web-scraping]
keywords: [n8n workflow, tự động hóa, lead generation, Apollo.io, ScraperCity, Google Sheets]
---

# 🚀 Tự động scrape leads Apollo.io & đồng bộ Google Sheets với ScraperCity

Bạn đã từng phải **chép dán hàng loạt lead** từ Apollo.io sang bảng tính, mất hàng giờ và vẫn còn lo lắng về lỗi trùng lặp?  
Việc này không chỉ tốn thời gian mà còn dễ gây sai sót, ảnh hưởng tới chiến dịch outreach của bạn.

**Workflow này** sẽ **tự động**:

1. Gửi yêu cầu tới ScraperCity để lấy danh sách lead từ Apollo.io.  
2. Xử lý, loại bỏ trùng lặp và chia thành các batch nhỏ.  
3. Ghi trực tiếp vào Google Sheets, luôn luôn cập nhật mới nhất.  

> **Không cần viết một dòng code nào** – chỉ cần cấu hình các node có sẵn trong n8n.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động lấy hàng nghìn lead trong vài phút.  
- **Độ chính xác cao**: Loại bỏ trùng lặp, chuẩn hoá dữ liệu trước khi lưu.  
- **Cập nhật liên tục**: Khi chạy lại workflow, chỉ có lead mới được thêm.  
- **Không cần code**: Tất cả được cấu hình bằng giao diện kéo‑thả của n8n.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản ScraperCity** (API Key).  
- **Tài khoản Apollo.io** (để tạo “scraper” trong ScraperCity).  
- **Google Account** với quyền **Google Sheets API** (tạo Credential OAuth2 hoặc Service Account).  
- **n8n** đã cài đặt (Self‑hosted hoặc Cloud).  
- (Tùy chọn) **Slack/Telegram** nếu muốn nhận thông báo lỗi.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Vào **n8n → Workflows → Import**.  
2. Tải file `scrape-apollo-leads-google-sheets.json` (được cung cấp ở cuối README) **hoặc** copy toàn bộ JSON và dán vào ô **Import from JSON**.  
3. Nhấn **Import** → Workflow sẽ xuất hiện trong danh sách.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là danh sách các node quan trọng và cách cấu hình:

| Node | Mô tả | Cấu hình cần thay đổi |
|------|------|----------------------|
| **Manual Trigger** | Bắt đầu workflow thủ công hoặc theo schedule. | Đặt **Cron** nếu muốn chạy tự động (ví dụ: mỗi ngày 08:00). |
| **Set** (Prepare Request) | Đặt các biến như `apiKey`, `scraperId`, `pageSize`. | - `apiKey`: API Key ScraperCity.<br>- `scraperId`: ID scraper Apollo.io trong ScraperCity.<br>- `pageSize`: Số lead mỗi batch (max 100). |
| **HTTP Request** (ScraperCity) | Gửi GET/POST tới `https://api.scrapercity.com/v1/scrape`. | - **Authentication**: Header `Authorization: Bearer {{ $json["apiKey"] }}`.<br>- **Query Params**: `scraper_id={{ $json["scraperId"] }}` & `limit={{ $json["pageSize"] }}`. |
| **Code** (Transform) | Chuyển đổi dữ liệu trả về thành mảng các object `{name, email, company, title, linkedin}`. | Thêm đoạn JavaScript mẫu (được cung cấp trong file JSON). |
| **Split In Batches** | Chia danh sách lead thành các batch nhỏ (để tránh limit Google Sheets). | `Batch Size` = 50 (hoặc tùy nhu cầu). |
| **Remove Duplicates** | Loại bỏ lead đã tồn tại trong Sheet. | Chọn **Field** = `email`. |
| **If** (Check Errors) | Kiểm tra `response.statusCode` của ScraperCity. | Nếu != 200 → gửi thông báo Slack/Telegram (node **Slack** hoặc **Telegram** tùy chọn). |
| **Wait** | Thêm delay 1‑2 giây giữa các batch để tránh rate‑limit Google. | `Delay` = 1500 ms. |
| **Google Sheets** (Append) | Ghi lead vào Sheet đã chuẩn bị. | - **Credential**: Chọn Google OAuth2 Service Account.<br>- **Spreadsheet ID**: ID của file Google Sheet.<br>- **Sheet Name**: Tên sheet (ví dụ: `Leads`). |
| **Sticky Note** | Ghi chú hướng dẫn nhanh cho các node. | Không cần thay đổi, chỉ để tham khảo. |

> **Lưu ý:** Mỗi node **Credentials** phải được tạo trước trong n8n → **Credentials**. Đặc biệt, Google Sheets yêu cầu quyền `https://www.googleapis.com/auth/spreadsheets`.

#### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn **Execute Workflow** → Kiểm tra log ở mỗi node, chắc chắn dữ liệu được đưa vào Google Sheet.  
2. Nếu mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc phải).  
3. Đặt **Cron** (nếu dùng Manual Trigger → Schedule) để workflow tự chạy định kỳ.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo lỗi qua Slack**: Thêm node Slack ngay sau node **If** để nhận tin tức khi ScraperCity trả về lỗi.  
- **Lưu log chi tiết**: Dùng node **Write Binary File** để ghi JSON raw vào một bucket S3 hoặc Google Drive, phục vụ audit.  
- **Báo cáo định kỳ**: Kết hợp **Google Slides** hoặc **Email** để gửi báo cáo tổng hợp lead mỗi tuần.  
- **Kết hợp với HubSpot/CRM**: Thêm node **HubSpot** hoặc **Pipedrive** để tự động tạo contact ngay sau khi lưu vào Sheet.

### 📌 Kết luận
Với workflow này, các sếp có thể **tự động lấy hàng nghìn lead Apollo.io**, loại bỏ trùng lặp và **đồng bộ ngay vào Google Sheets** chỉ trong vài phút, không cần viết code. Hãy triển khai ngay để tối ưu hoá quy trình prospecting và tập trung vào việc **chốt deal**!

---  

**File JSON để import** (đính kèm trong phần tải xuống của bài viết): `scrape-apollo-leads-google-sheets.json`  

Nếu gặp bất kỳ khó khăn nào, đừng ngần ngại để lại comment hoặc hỏi trong cộng đồng n8n. Chúc các sếp thành công!