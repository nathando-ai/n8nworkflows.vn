---
title: "🚀 Tự động Scrape danh sách doanh nghiệp Google Maps vào Google Sheets – Không cần code"
description: "Giải pháp tự động thu thập danh sách doanh nghiệp từ Google Maps và lưu trữ ngay vào Google Sheets, giúp doanh nghiệp tiết kiệm thời gian và tránh sai sót khi nhập liệu thủ công."
slug: "tac-dong-scrape-google-maps-vao-google-sheets"
tags: [n8n, automation, no-code, google-sheets, apify, market-research]
keywords: [n8n workflow, tự động hóa, scrape Google Maps, Google Sheets, Apify]
---

# 🚀 Tự động Scrape danh sách doanh nghiệp Google Maps vào Google Sheets – Không cần code

Bạn đang phải nhập liệu thủ công danh sách doanh nghiệp từ Google Maps vào Google Sheets? Điều đó không chỉ tốn thời gian mà còn dễ dẫn đến lỗi dữ liệu. Workflow này sẽ **tự động** lấy dữ liệu từ Google Maps qua Apify, xử lý và lưu trữ ngay vào Google Sheets – hoàn toàn không cần viết code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không còn phải copy‑paste dữ liệu thủ công.
- **Độ chính xác cao**: Dữ liệu được lấy trực tiếp từ nguồn chính thức.
- **Tự động cập nhật**: Mỗi lần submit form, dữ liệu mới luôn được append hoặc update.
- **Linh hoạt**: Dễ dàng mở rộng thêm các trường dữ liệu hoặc kết nối tới Slack/Telegram.
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **Google Sheets**: Tạo một bảng tính mới, ghi lại `Spreadsheet ID` và tên sheet (ví dụ: `Sheet1`).
- **Google Sheets OAuth2**: Tạo credential `googleSheetsOAuth2Api` trong n8n.
- **Apify**: Đăng ký tài khoản Apify, lấy `API Key` và ID của actor “Google Maps Scraper”.
- **Form Trigger**: Thiết lập form với các trường `city`, `country`, `query`.
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
- Tải file JSON từ link gốc: <https://n8n.io/workflows/15367>
- Vào n8n Editor → **Import** → **Upload JSON** hoặc copy‑paste nội dung JSON.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên Node | Cấu hình cần chỉnh | Credential / Tham số |
|------|----------|---------------------|----------------------|
| 1 | When Search Form Submitted | Định nghĩa các trường `city`, `country`, `query` | - |
| 2 | Set City Country and Query | Định dạng dữ liệu đầu vào thành JSON chuẩn | - |
| 3 | Read Existing Listings from Sheets | `Spreadsheet ID`, `Sheet Name` | `googleSheetsOAuth2Api` |
| 4 | Upsert Listings in Sheets | `Spreadsheet ID`, `Sheet Name`, `Operation: appendOrUpdate` | `googleSheetsOAuth2Api` |
| 5 | Build Listing Fields | Xác định các trường cần lưu (title, price, category, address, …) | - |
| 6 | Scrape Google Maps via Apify | URL actor, `API Key` trong header hoặc body | `apifyApi` |

> **Lưu ý**: Đảm bảo `Actor ID` trong URL HTTP Request trùng với actor “Google Maps Scraper” mà bạn muốn sử dụng. Nếu muốn lấy thêm dữ liệu (địa chỉ, số điện thoại, website), mở rộng node **Build Listing Fields**.

### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow với dữ liệu mẫu (điền form thử nghiệm).
2. Kiểm tra Google Sheets xem dữ liệu đã được append/updated chưa.
3. Khi mọi thứ ổn, bật **Active** cho workflow.

## ✍️ Mẹo & gợi ý nâng cao
- **Slack/Telegram**: Thêm node Slack hoặc Telegram để gửi thông báo khi dữ liệu mới được lưu.
- **Lưu log**: Sử dụng node “Write Binary Data” để ghi log vào Google Drive hoặc Cloud Storage.
- **Báo cáo định kỳ**: Kết hợp với node “Cron” để tự động trigger workflow hàng ngày/tuần.
- **Tùy chỉnh query**: Đặt logic trong node “Set City Country and Query” để tự động sinh query dựa trên địa điểm và ngành nghề.

## 📌 Kết luận
Workflow này giúp các sếp **đưa công việc thu thập dữ liệu Google Maps lên một tầm cao mới** – nhanh, chính xác và không cần viết code. Hãy thử ngay và cảm nhận sự khác biệt!

---

## Need more advanced automation solutions? Contact us for custom enterprise workflows!

# Growth-AI.fr

- <https://www.linkedin.com/in/allanvaccarizi/>
- <https://www.linkedin.com/in/hugo-marinier-%F0%9F%A7%B2-6537b633/>

![Logo Growth AI](https://cdn.prod.website-files.com/6825df5b20329ba581df4914/68d413c43f8729fa336568a6_Logo_horizontal.png)

---