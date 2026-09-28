---
title: "🚀 Tự động cào và xuất hàng loạt Review sản phẩm Amazon ra Google Sheets qua RapidAPI"
description: "Hướng dẫn xây dựng workflow n8n tự động cào hàng loạt đánh giá (reviews) từ Amazon theo ASIN, xử lý phân trang thông minh và lưu trữ trực tiếp vào Google Sheets."
slug: "tu-dong-cao-va-xuat-review-amazon-ra-google-sheets"
tags: [n8n, automation, amazon, rapidapi, google-sheets, market-research]
keywords: [n8n workflow, cào review amazon, amazon scraper api, rapidapi amazon data, tu dong hoa google sheets]
---

# 🚀 Tự động cào và xuất hàng loạt Review sản phẩm Amazon ra Google Sheets qua RapidAPI

Các sếp làm trong ngành E-commerce (Thương mại điện tử) hoặc nghiên cứu thị trường (Market Research) chắc chắn hiểu được nỗi khổ khi phải thủ công đi copy hàng trăm, hàng nghìn đánh giá sản phẩm trên Amazon để phân tíchInsight khách hàng, đối thủ. Việc này vừa mất thời gian, dễ bỏ sót dữ liệu lại cực kỳ nhàm chán.

Đừng lo, workflow n8n này sinh ra là để giải quyết triệt để bài toán đó! Được thiết kế bởi chuyên gia Hunyao, hệ thống này tự động hóa 100% quy trình thu thập dữ liệu review từ Amazon thông qua RapidAPI và đẩy thẳng vào Google Sheets một cách mượt mà, không cần một dòng code phức tạp nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Thu thập dữ liệu toàn diện:** Tự động lấy 100 review mới nhất cho mỗi mức đánh giá (từ 1⭐ đến 5⭐) và 100 review hàng đầu cho 1⭐ và 5⭐.
- **Tiết kiệm 99% thời gian:** Thay vì mất hàng ngày copy-paste thủ công, hệ thống tự động hóa hoàn toàn với tổng cộng ~70 API call được quản lý thông minh qua vòng lặp (`Loop Over Items`, `Wait`).
- **Đồng bộ hóa tức thì:** Dữ liệu được phân loại rõ ràng và tự động cập nhật (`appendOrUpdate`) vào đúng bảng Google Sheets mà các sếp chỉ định thông qua Form đầu vào.
- **Vận hành không gián đoạn:** Tích hợp các bộ lọc thông minh (`If status "OK"`) để xử lý các phản hồi từ API một cách an toàn.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã hoạt động (Self-hosted hoặc n8n Cloud).
- **Tài khoản RapidAPI:** Để sử dụng API `Real-Time Amazon Data`.
- **Tài khoản Google:** Để kết nối Google Sheets (sử dụng OAuth2).
- **Google Sheet mẫu:** Chuẩn bị sẵn một file Google Sheet để lưu trữ dữ liệu review.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow (hoặc file JSON được cung cấp) và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà không gặp lỗi, các sếp cần lưu ý cấu hình kỹ các node sau:

- **`On form submission` (Form Trigger):** 
  - Khi điền form, hãy đảm bảo rằng **Tab URL** nhập vào khớp **chính xác** với URL của tab tương ứng trong Google Sheet mà các sếp muốn lưu dữ liệu. Nếu sai lệch, dữ liệu sẽ không được ghi đúng chỗ.
- **`HTTP Request`:** 
  - Cần cấu hình **Credentials** loại `httpHeaderAuth` bằng `X-RapidAPI-Key` lấy từ tài khoản RapidAPI của các sếp.
- **`Store reviews` (Google Sheets):** 
  - Kết nối tài khoản Google Sheets của các sếp bằng `googleSheetsOAuth2Api`.
  - Chọn đúng file Spreadsheet và cấu hình thao tác `appendOrUpdate`.
- **Logic xử lý `If status "OK" and contains reviews` & Vòng lặp (`Loop Over Items`, `Wait1`, `Wait2`):**
  - Workflow thực hiện khoảng 70 API call cho mỗi sản phẩm (50 cuộc gọi cho Most Recent và 20 cuộc gọi cho Top Reviews). Các node `Wait` giúp tránh việc bị giới hạn tốc độ (rate limit) từ phía API.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test run) bằng một ASIN mẫu thông qua Form để kiểm tra dòng dữ liệu.
- Sau khi dữ liệu đổ về Google Sheet chuẩn chỉnh, gạt công tắc sang **Active** để hệ thống chính thức tự động vận hành.

---

### ⚠️ Các trường hợp lỗi thường gặp (Known Failure Cases)

1. **Lỗi dừng tại node `If status "OK" and contains reviews`:**
   - *Nguyên nhân 1:* Không đủ số lượng review thực tế trên Amazon (workflow mặc định giả định có 10 trang review cho mỗi mức sao, nếu sản phẩm mới có ít review hơn, bước kiểm tra điều kiện sẽ bỏ qua một cách âm thầm).
   - *Nguyên nhân 2:* Vượt hạn mức RapidAPI (đã chạm quota của gói BASIC). Các sếp sẽ nhận được lỗi `Error 429` (The service is receiving too many requests from you). Hãy kiểm tra lại quota trên [RapidAPI Dashboard](https://rapidapi.com/developer/dashboard).

---

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo Telegram/Slack:** Thêm một node Telegram sau khi workflow hoàn tất để báo cáo số lượng review đã cào thành công cho từng sản phẩm.
- **Tự động hóa lịch trình (Schedule): thay thế Form Trigger bằng Schedule Trigger** nếu các sếp muốn tự động quét danh sách ASIN từ một Google Sheet có sẵn hàng tuần/hàng tháng.
- **Kết hợp AI (OpenAI/Claude):** Thêm một bước xử lý bằng LLM để phân tích cảm xúc (Sentiment Analysis) các review vừa cào trước khi lưu vào Sheets.

### 📌 Kết luận
Workflow "Export Amazon Product Reviews in Bulk to Google Sheets via RapidAPI" là một "vũ khí" cực kỳ lợi hại cho anh em làm E-commerce để nghiên cứu đối thủ và lắng nghe khách hàng. Hãy triển khai ngay lên VPS của các sếp để tối ưu hóa, tiết kiệm thời gian và bứt phá doanh thu thôi nào!