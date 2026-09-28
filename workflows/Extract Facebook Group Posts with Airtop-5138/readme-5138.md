---
title: "🚀 Tự động trích xuất bài viết nhóm Facebook bằng n8n và Airtop AI"
description: "Hướng dẫn tự động hóa quy trình cào dữ liệu bài viết từ nhóm Facebook (Facebook Group Posts) sử dụng n8n và trình duyệt thông minh Airtop AI mà không cần code."
slug: "tu-dong-trich-xuat-bai-viet-facebook-group-voi-airtop"
tags: [n8n, automation, no-code, airtop, facebook-scraper, ai-agents]
keywords: [n8n workflow, trích xuất bài viết facebook, cào dữ liệu facebook group, airtop ai, tự động hóa marketing]
---

# 🚀 Tự động trích xuất bài viết nhóm Facebook bằng n8n và Airtop AI

Các sếp có đang tốn quá nhiều thời gian để lướt thủ công các nhóm Facebook (Facebook Groups) nhằm nghiên cứu thị trường, theo dõi đối thủ hay thu thập nội dung không? Việc copy-paste từng bài viết, thống kê số lượng like, share, comment bằng cơm vừa mất thời gian vừa dễ bỏ lỡ thông tin quan trọng.

Giải pháp ở đây là workflow n8n kết hợp với **Airtop AI** – công cụ tự động hóa trình duyệt thông minh dựa trên AI. Giờ đây, các sếp chỉ cần nhập URL nhóm Facebook vào một biểu mẫu (Form), hệ thống sẽ tự động đăng nhập, duyệt qua bảng tin và trích xuất dữ liệu bài viết một cách gọn gàng dưới dạng cấu trúc JSON sẵn sàng sử dụng!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Tự động hóa hoàn toàn việc thu thập dữ liệu từ Facebook Group mà không cần thao tác tay.
- **Dữ liệu cấu trúc sạch sẽ:** Lấy tối đa 5 bài viết không tài trợ (non-sponsored) kèm theo đầy đủ chi tiết: nội dung, URL, thời gian, số lượng like/share/comment và ảnh thumbnail.
- **Ứng dụng AI thông minh:** Sử dụng Airtop AI hiểu ngôn ngữ tự nhiên để trúng đích dữ liệu cần lấy dù giao diện Facebook có thay đổi.
- **Linh hoạt mở rộng:** Dễ dàng kết nối tiếp dữ liệu này vào Google Sheets, Notion, Database hoặc gửi cảnh báo qua Telegram/Slack.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã cài đặt phiên bản n8n (Cloud hoặc Self-hosted).
- **Tài khoản Airtop:** 
  - [Airtop API Key](https://portal.airtop.ai/api-keys) (Miễn phí khởi tạo).
  - Một [Airtop Profile](https://portal.airtop.ai/browser-profiles) đã được đăng nhập sẵn tài khoản Facebook cá nhân để trình duyệt có quyền truy cập nhóm.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này hoặc copy toàn bộ mã nguồn JSON.
- Trong giao diện n8n Editor, nhấn vào dấu **`+`** (Add workflow) hoặc menu ở góc trên bên phải, chọn **Import from File / Clipboard** và dán đoạn JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này rất gọn nhẹ với chỉ 2 nodes chính, các sếp cần cấu hình chuẩn xác các điểm sau:

- **Node `On form submission` (Form Trigger):**
  - Node này tạo ra một biểu mẫu giao diện web đơn giản. 
  - Các sếp cần cấu hình để thu thập 2 trường dữ liệu đầu vào: **Facebook Group URL** (Đường dẫn nhóm Facebook muốn cào) và **Airtop Profile** (Tên cấu hình trình duyệt đã đăng nhập Facebook trên Airtop).
- **Node `Airtop`:**
  - **Credentials:** Tạo kết nối mới (`airtopApi`) bằng cách điền **Airtop API Key** lấy từ cổng quản lý của Airtop.
  - **Prompt AI:** Node được cấu hình sẵn câu lệnh (Prompt) thông minh bằng tiếng Anh để chỉ đạo AI điều hướng trình duyệt, lọc bài viết không phải quảng cáo và bóc tách các trường dữ liệu:
    - *Post text* (Nội dung bài viết)
    - *Post URL* (Đường dẫn bài viết)
    - *Page/profile URL* (Link tác giả)
    - *Timestamp* (Thời gian đăng)
    - *Number of likes / shares / comments* (Các chỉ số tương tác)
    - *Page or profile details* (Thông tin chi tiết trang/người đăng)
    - *Post thumbnail* (Ảnh thu nhỏ của bài viết)
  - Hãy đảm bảo truyền đúng biến URL nhóm Facebook và tên Airtop Profile từ form điền vào node này.

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** hoặc **Execute Workflow** để thử nghiệm nhập liệu vào form mẫu và kiểm tra kết quả trả về ở dạng JSON.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để đưa workflow vào trạng thái vận hành tự động thực tế.

### ✍️ Mẹo & gợi ý nâng cao
Để khai thác tối đa sức mạnh của workflow này, các sếp có thể mở rộng thêm:
1. **Lưu trữ tự động:** Thêm node **Google Sheets** hoặc **Notion** ngay sau node Airtop để tự động lưu toàn bộ danh sách bài viết vừa cào vào bảng tính.
2. **Cảnh báo thông minh:** Kết hợp với node **Slack** hoặc **Telegram** để bắn tin nhắn thông báo ngay lập tức khi có bài viết đạt lượng tương tác cao (viral post) trong nhóm.
3. **Tự động hóa phản hồi:** Kết hợp thêm các kịch bản Airtop khác để tự động tương tác hoặc phản hồi bình luận theo kịch bản có sẵn.

### 📌 Kết luận
Việc nghiên cứu thị trường và thu thập dữ liệu mạng xã hội chưa bao giờ dễ dàng đến thế khi kết hợp sức mạnh của n8n và Airtop AI. Hãy cài đặt ngay workflow này để tối ưu hóa hiệu suất làm việc cho đội ngũ marketing và R&D của doanh nghiệp các sếp nhé!