---
title: "🚀 Tự động theo dõi đối thủ cạnh tranh 24/7 với Gemini, Olostep và n8n"
description: "Xây dựng hệ thống tự động quét trang web đối thủ, phát hiện thay đổi về tính năng, giá cả và gửi báo cáo chiến lược qua Gmail với n8n."
slug: "tu-dong-theo-doi-doi-thu-canh-tranh-voi-gemini-va-olostep"
tags: [n8n, automation, ai, google-sheets, gmail, market-research]
keywords: [n8n workflow, theo dõi đối thủ, olostep scrape, google gemini ai, tự động hóa marketing]
---

# 🚀 Tự động theo dõi đối thủ cạnh tranh 24/7 với Gemini, Olostep và n8n

Các sếp có bao giờ rơi vào cảnh bị đối thủ "đánh úp" bằng một tính năng mới tinh hoặc một chiến lược giá thay đổi chóng mặt mà bản thân chỉ biết trễ sau vài ngày? Việc kiểm tra thủ công các trang web đối thủ vừa tốn thời gian, dễ bỏ sót lại cực kỳ nhàm chán.

Giải pháp ở đây là gì? Hãy để công nghệ lo! Workflow n8n này hoạt động như một hệ thống tình báo thị trường tự động 24/7. Nó sẽ thay các sếp cào dữ liệu (scrape) trang web đối thủ, dùng AI (Google Gemini) để phân tích xem có thay đổi gì đột phá hay không, lọc bỏ những "nhiễu" không quan trọng và gửi thẳng một bản ghi nhớ chiến lược (actionable memo) qua **Gmail**. Tất cả hoàn toàn tự động và không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Bắt trọn tin tức chiến lược:** Nhận cảnh báo ngay lập tức khi đối thủ thay đổi giá, ra mắt tính năng mới (`MAJOR_FEATURE_LAUNCH`, `PRICE_CHANGE`, v.v.).
- **Tiết kiệm 90% thời gian:** Không cần phải mất công lướt web thủ công từng trang của đối thủ mỗi ngày.
- **Loại bỏ nhiễu thông tin:** AI tự động phân biệt đâu là thay đổi nhỏ (đổi chữ, cập nhật giao diện phụ) đâu là chiến lược cốt lõi.
- **Báo cáo tinh gọn, dễ hành động:** Nhận bản tóm tắt chiến lược dưới 100 từ kèm theo đề xuất hành động qua email cá nhân.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **Google Gemini API Credentials:** Dùng cho các node AI phân tích sự thay đổi và viết memo.
- **Olostep API Credentials:** Dịch vụ chuyên dụng để scrape dữ liệu web, vượt qua các hàng rào chống bot của đối thủ.
- **Google Sheets (OAuth2):** Nơi lưu trữ danh sách URL cần theo dõi và nội dung lịch sử (baseline).
- **Gmail (OAuth2):** Tài khoản gửi/nhận email cảnh báo chiến lược.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn cung cấp, sau đó tại giao diện n8n Editor, chọn **Add workflow** -> Dán nội dung JSON hoặc chọn **Import from File** để đưa toàn bộ 12 nodes lên màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống mượt mà trơn tru, các sếp cần cấu hình chính xác các điểm sau:
- **Node `Get row(s) in sheet` & `Google Sheets`:** Kết nối tài khoản Google Sheets của các sếp. Tạo một file Google Sheet có tên là `competitor monitoring` với các cột cơ bản: `url`, `previousContent`, và `newcontent`. Thêm sẵn danh sách các URL đối thủ cần theo dõi vào đây.
- **Node `scrape URL` & `scrape URL1` (Olostep):** Kết nối Olostep API để trích xuất nội dung văn bản từ các trang web mục tiêu.
- **Node `Changes identifier`, `Diff analyst`, `Memo editor` (Google Gemini):** Cấu hình credentials Google Gemini. Các node này sẽ chịu trách nhiệm so sánh nội dung cũ và mới, gán nhãn loại thay đổi và soạn thảo nội dung báo cáo nội bộ.
- **Node `Send a message` (Gmail):** Kết nối tài khoản Gmail cá nhân hoặc của công ty, sau đó điền địa chỉ email nhận thông báo chiến lược ở phần cấu hình người gửi/nhận.

#### 3. Kích hoạt ⚡️
- Bấm **`When clicking ‘Execute workflow’`** hoặc dùng nút **Test workflow** để chạy thử với dữ liệu mẫu trong Google Sheet.
- Kiểm tra kết quả trả về trong Gmail. Nếu mọi thứ hoạt động hoàn hảo, hãy gạt công tắc sang **Active** để workflow tự động chạy ngầm.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh nhận tin:** Kết nối thêm node **Slack** hoặc **Telegram** để bắn thẳng cảnh báo vào nhóm chat `#competitive-intel` thay vì chỉ nhận qua email.
- **Tự động hóa lịch chạy:** Thay vì dùng nút bấm thủ công (`manualTrigger`), hãy gắn thêm một **Schedule Trigger** để hệ thống tự quét đối thủ mỗi sáng thứ Hai hàng tuần.
- **Lưu lịch sử chi tiết:** Tận dụng các node **Append or update row in sheet** để lưu lại toàn bộ lịch sử biến động thị trường phục vụ cho các buổi họp chiến lược quý/năm.

### 📌 Kết luận
Việc nắm bắt thông tin đối thủ cạnh tranh chưa bao giờ dễ dàng đến thế với sức mạnh kết hợp từ n8n, Olostep và Gemini AI. Hãy thiết lập ngay workflow này để đội ngũ sản phẩm và marketing của các sếp luôn đi trước một bước trên thị trường!