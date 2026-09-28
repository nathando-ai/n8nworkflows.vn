---
title: "🚀 Cảnh Báo Giá Vàng Tự Động qua LINE – Web Scraping 100% Không Code"
description: "Giải pháp tự động kiểm tra giá vàng mỗi 6 giờ và gửi cảnh báo qua LINE khi giá vượt ngưỡng đã định, giúp bạn không bỏ lỡ cơ hội giao dịch."
slug: "goc-gia-vang-canh-bao-line"
tags: [n8n, automation, no-code, crypto trading, gold price, line notification]
keywords: [n8n workflow, tự động hóa, giá vàng, cảnh báo, LINE, web scraping, crypto trading]
---

# 🚀 Cảnh Báo Giá Vàng Tự Động qua LINE – Web Scraping 100% Không Code

Bạn đang theo dõi giá vàng để quyết định thời điểm mua bán nhưng lại phải lướt web liên tục? Mỗi lần giá thay đổi, bạn phải tự kiểm tra và gửi thông báo cho mình hoặc đồng nghiệp. Điều này tốn thời gian, dễ bỏ sót và không chính xác.  
Workflow n8n dưới đây sẽ **đánh giá giá vàng tự động mỗi 6 giờ**, **so sánh với ngưỡng bạn đặt** và **gửi cảnh báo qua LINE ngay khi giá vượt ngưỡng** – hoàn toàn không cần viết code, chỉ cần cấu hình một vài tham số.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần lướt web, tự động kiểm tra 24/7.  
- **Chính xác & kịp thời**: Cảnh báo ngay khi giá vượt ngưỡng, tránh lỡ cơ hội.  
- **Cá nhân hóa**: Đặt ngưỡng riêng cho từng người dùng hoặc chiến lược.  
- **Hoạt động liên tục**: Chạy trên VPS, không bị gián đoạn.  
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **Tài khoản LINE Notify**: Tạo token để gửi thông báo.  
- **URL trang web giá vàng**: Ví dụ `https://www.example.com/gold-price`.  
- **Ngưỡng giá vàng**: Số tiền (đơn vị VND) mà bạn muốn cảnh báo.  
- **VPS hoặc môi trường n8n**: Đảm bảo n8n đang chạy và có thể truy cập internet.  
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON workflow từ link gốc:  
   <https://n8n.io/workflows/6265> (hoặc lưu file `gold-price-alert.n8n.json`).  
2. Mở n8n Editor → **Import** → **Upload File** → chọn file JSON.  
3. Workflow sẽ xuất hiện với tên **Automated Gold Price Threshold Alerts via LINE**.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Tham số cần cấu hình |
|------|-------|----------------------|
| **Schedule Trigger** | Đặt lịch chạy. | `Interval: 6 hours` (hoặc `Cron: 0 */6 * * *`). |
| **Get Webpage** (`httpRequest`) | Lấy HTML trang. | `URL: https://www.example.com/gold-price` <br> `Method: GET` <br> `Authentication: None`. |
| **Extract Price** (`html`) | Trích xuất giá. | `Operation: extractHtmlContent` <br> `Selector: CSS selector của giá (ví dụ: `.price-value`)` <br> `Output: priceText`. |
| **If** | So sánh giá với ngưỡng. | `Conditions: priceText > THRESHOLD` <br> *THRESHOLD* là biến bạn đặt trong node (ví dụ: `5000000`). |
| **Send Line Message** (`httpRequest`) | Gửi thông báo. | `URL: https://notify-api.line.me/api/notify` <br> `Method: POST` <br> `Headers: Authorization: Bearer <YOUR_LINE_TOKEN>` <br> `Body: message=Giá vàng hiện tại là {{priceText}} VND, vượt ngưỡng {{THRESHOLD}} VND!` <br> **Credentials**: `httpHeaderAuth` – nhập token LINE Notify. |
| **Sticky Note** | Ghi chú nội dung (không ảnh hưởng workflow). | Không cần cấu hình. |

> **Lưu ý**: Node **Extract Price** cần chuyển giá từ chuỗi sang số. Bạn có thể dùng `{{ parseInt(priceText.replace(/[^0-9]/g, '')) }}` trong node **If** hoặc thêm một node **Function** để làm việc này.

### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow thủ công với dữ liệu mẫu để kiểm tra.  
2. Kiểm tra log: Đảm bảo giá được trích xuất đúng và điều kiện `If` hoạt động.  
3. **Bật Active**: Đánh dấu workflow là *Active* để nó tự động chạy theo lịch.

## ✍️ Mẹo & gợi ý nâng cao
- **Thêm Slack hoặc Telegram**: Thêm node `httpRequest` gửi thông báo tới Slack/Telegram cùng lúc.  
- **Lưu lịch sử**: Gửi dữ liệu vào Google Sheets hoặc Airtable để lưu lịch sử giá.  
- **Cảnh báo định kỳ**: Thêm node `Schedule Trigger` khác gửi báo cáo giá hàng ngày.  
- **Sử dụng biến môi trường**: Lưu token LINE và URL trang web trong biến môi trường để bảo mật.  
- **Tối ưu scraping**: Nếu trang thay đổi, cập nhật CSS selector hoặc dùng XPath trong node `html`.

## 📌 Kết luận
Workflow này giúp bạn **đừng bỏ lỡ bất kỳ biến động giá vàng nào** mà không cần phải lướt web liên tục. Chỉ cần một vài lần cấu hình, bạn đã có hệ thống cảnh báo tự động, chính xác và kịp thời.  
Hãy **cài đặt ngay** trên VPS của mình và bắt đầu nhận thông báo qua LINE ngay khi giá vàng vượt ngưỡng đã đặt. Happy trading!