---
title: "🚀 Tự động ghi nhận quyết định phê duyệt hóa đơn từ Slack lên Google Sheets với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động bắt sự kiện bấm nút phê duyệt (Approve, Reject, Flag) trên Slack, ghi log vào Google Sheets và gửi tin nhắn xác nhận qua Slack DM."
slug: "tu-dong-ghi-nhan-phe-duyet-hoa-don-slack-google-sheets"
tags: [n8n, automation, slack, google-sheets, invoice-processing, no-code]
keywords: [n8n workflow, tự động hóa slack, phê duyệt hóa đơn, google sheets automation, webhook n8n]
---

# 🚀 Tự động ghi nhận quyết định phê duyệt hóa đơn từ Slack lên Google Sheets

Việc quản lý và phê duyệt hóa đơn thủ công thường tốn rất nhiều thời gian, dễ xảy ra sai sót và khó theo dõi trạng thái. Các sếp có bao giờ gặp tình trạng nhân viên gửi yêu cầu thanh toán, quản lý bấm duyệt trên Slack nhưng lại quên cập nhật vào file Excel/Google Sheets quản lý chung, dẫn đến việc thu chi lệch lạc cuối tháng?

Giải pháp tuyệt vời nhất là tự động hóa 100% quy trình này! Bài viết này sẽ hướng dẫn các sếp thiết lập một workflow **n8n** cực kỳ thông minh: Lắng nghe thao tác bấm nút của sếp trên Slack (Approve/Reject/Flag), tự động phân loại, ghi nhận dữ liệu vào đúng tab tương ứng trên **Google Sheets** và gửi tin nhắn xác nhận (DM) lại cho người phê duyệt ngay lập tức. Không còn thủ công, không còn sai sót!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn luồng duyệt hóa đơn:** Xóa bỏ khâu copy-paste thủ công từ Slack sang Google Sheets.
- **Phân loại thông minh:** Tự động chia nhỏ dòng dữ liệu vào các tab *Approved*, *Rejected*, hoặc *Flagged* tùy theo nút bấm.
- **Minh bạch và tức thời:** Gửi tin nhắn xác nhận (Slack DM) ngay lập tức cho người phê duyệt để làm bằng chứng lưu trữ.
- **Vận hành 24/7:** Hệ thống luôn sẵn sàng nhận tín hiệu từ Slack bất kể ngày đêm.
:::

### 📦 Các loại Node được sử dụng trong Workflow
- **Webhook (`n8n-nodes-base.webhook`):** Nhận tín hiệu POST từ Slack Interactivity khi bấm nút.
- **Set (`n8n-nodes-base.set`):** Xử lý, bóc tách và định dạng lại dữ liệu payload từ Slack.
- **Switch (`n8n-nodes-base.switch`):** Định tuyến luồng xử lý dựa trên quyết định (Approved / Rejected / Flagged).
- **Google Sheets (`n8n-nodes-base.googleSheets`):** Thêm dòng dữ liệu (append) vào các tab tương ứng.
- **Slack (`n8n-nodes-base.slack`):** Gửi tin nhắn thông báo xác nhận trực tiếp (DM) cho người thao tác.

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- Một Slack App đã được cấu hình tính năng **Interactivity**.
- Một Google Sheet với các quyền truy cập API (Google Sheets OAuth2).
:::

---

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ mã JSON của workflow (từ nguồn cấp) và dán trực tiếp vào giao diện làm việc của n8n Editor.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

#### Bước A: Chuẩn bị Google Sheet
1. Tạo một Google Sheet mới với **3 tab** có tên chính xác là: `Approved`, `Rejected`, `Flagged`.
2. Thêm các cột tiêu đề (Header) cho mỗi tab:
   - `Supplier Name`
   - `Invoice Number`
   - `Amount`
   - `Date`
3. Sao chép lại **Sheet ID** từ đường dẫn URL của Google Sheet đó.

#### Bước B: Cấu hình các Node trong n8n
- **Node `Receive Slack Button Click` (Webhook):** Lấy đường dẫn Webhook Production URL do n8n cung cấp để dán vào cấu hình Slack App (mục Interactivity & Shortcuts).
- **Node `Parse Slack Payload` & `Extract Decision & Invoice Data` (Set):** Các node này dùng để xử lý dữ liệu URL-encoded gửi từ Slack thành JSON sạch. Các sếp giữ nguyên cấu hình nếu sử dụng đúng mẫu chuẩn.
- **Node `Route: Approved / Rejected / Flagged` (Switch):** Thiết lập các điều kiện rẽ nhánh dựa trên giá trị hành động (action value) trả về từ nút bấm Slack.
- **Các node `Log to Sheets: Approved`, `Rejected`, `Flagged` (Google Sheets):** 
  - Chọn **Credentials**: Kết nối tài khoản Google Sheets OAuth2 của các sếp.
  - Điền **Document ID**: Dán Sheet ID đã lấy ở Bước A.
  - Chọn đúng tên Sheet Name (`Approved`, `Rejected`, `Flagged`) cho từng node tương ứng.
- **Các node `Slack DM: Approved ✅`, `Rejected ❌`, `Flagged 🚩` (Slack):**
  - Kết nối Slack Bot Credentials.
  - Cấu hình ID người nhận (User ID) hoặc kênh thông báo để hệ thống gửi tin nhắn xác nhận.

### 3. Kích hoạt ⚡️
1. Chạy thử nghiệm (**Test step / Execute node**) bằng cách gửi một request giả lập từ Slack hoặc dùng nút Test trong webhook.
2. Kiểm tra xem dữ liệu có được ghi đúng vào Google Sheets và Slack DM có nhận được tin nhắn hay không.
3. Bật công tắc **Active** ở góc trên bên phải màn hình để đưa workflow vào trạng thái hoạt động chính thức 24/7.

---

## ✍️ Mẹo & Gợi ý nâng cao
- **Tích hợp thêm thông báo chung:** Ngoài việc gửi tin nhắn riêng (DM) cho người duyệt, các sếp có thể bổ sung thêm một node Slack để bắn tin nhắn vào kênh chung của phòng kế toán (#finance) để đội ngũ chuẩn bị thanh toán tiền.
- **Lưu lịch sử lỗi (Error Handling):** Thêm node *Error Trigger* vào workflow để nếu Google Sheets gặp sự cố quá tải API, hệ thống sẽ tự động bắn cảnh báo về một kênh Telegram riêng cho quản lý kỹ thuật.
- **Mở rộng phê duyệt đa cấp:** Kết hợp thêm các bước kiểm tra hạn mức tiền (Ví dụ: Dưới 10 triệu duyệt tự động, trên 10 triệu cần sếp lớn bấm duyệt tiếp).

---

## 📌 Kết luận
Với workflow n8n này, quy trình duyệt hóa đơn từ Slack lên Google Sheets sẽ trở nên mượt mà, tự động và minh bạch tuyệt đối. Hãy triển khai ngay hôm nay để tiết kiệm hàng giờ thao tác thủ công mỗi tuần cho đội ngũ của các sếp nhé!