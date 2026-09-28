---
title: "🚀 Tự động tạo hình ảnh chiến dịch mạng xã hội với Mistral AI & Pollinations.ai"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa hoàn toàn việc tạo nội dung và hình ảnh chiến dịch marketing bằng AI đa phương thức, tích hợp Google Drive và Pollinations.ai."
slug: "tu-dong-tao-hinh-anh-chien-dich-social-mistral-pollinations"
tags: [n8n, automation, no-code, ai-agent, mistral-ai, google-drive, content-creation]
keywords: [n8n workflow, tạo hình ảnh ai, mistral ai, pollinations ai, tự động hóa marketing, AI agent n8n]
---

# 🚀 Tự động tạo hình ảnh chiến dịch mạng xã hội với Mistral AI & Pollinations.ai

Các sếp làm marketing chắc chắn hiểu cảm giác "cạn kiệt ý tưởng" và mất hàng giờ liền để viết nội dung, sau đó lại lọ mọ tìm kiếm hoặc thiết kế hình ảnh cho từng bài đăng trên mạng xã hội. Việc này không chỉ tốn thời gian mà đôi khi còn thiếu sự đồng bộ về nhận diện thương hiệu.

Giải pháp là gì? Hãy để tự động hóa gánh vác! Workflow n8n này sẽ giúp các sếp kết hợp sức mạnh của **Mistral AI** và **Pollinations.ai** để tự động đọc thông tin thương hiệu từ Google Drive, lên ý tưởng chiến dịch, viết prompt chi tiết, tạo ra hàng loạt hình ảnh chất lượng cao và gom tất cả lại lưu trữ gọn gàng vào Google Drive chỉ với 1 cú click. Không cần tốn một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% quy trình sáng tạo:** Từ việc phân tích tài liệu thương hiệu đến sinh prompt và tạo hình ảnh.
- **Đồng bộ thương hiệu:** AI đọc trực tiếp file brand profile và brand goals từ Google Drive để đảm bảo hình ảnh sinh ra luôn bám sát tinh thần doanh nghiệp.
- **Tiết kiệm hàng giờ thiết kế:** Tạo đồng loạt nhiều hình ảnh cho chiến dịch chỉ trong vài giây thông qua API miễn phí/linh hoạt của Pollinations.ai.
- **Lưu trữ khoa học:** Tự động gom nhóm và lưu toàn bộ file hình ảnh vào thư mục Google Drive định sẵn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Mistral AI** kèm API Key (`mistralCloudApi`).
- **Tài khoản Google Drive** chứa file thông tin thương hiệu (`brand profile`) và mục tiêu thương hiệu (`brand goals`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ n8n template (ID: 8770), sau đó vào giao diện n8n Editor, chọn **Add workflow** -> **Import from File** hoặc dán trực tiếp mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 23 nodes được chia thành các cụm chức năng rõ ràng. Các sếp cần cấu hình các điểm sau:

- **Nodes Google Drive (`brand goals`, `brand profile`, `Upload file`):** 
  - Kết nối tài khoản Google Drive của các sếp qua `googleDriveOAuth2Api`.
  - Chọn đúng file ID hoặc đường dẫn đến file mục tiêu và hồ sơ thương hiệu của doanh nghiệp trong các node `brand goals` và `brand profile`.
- **Node AI & Agent (`Mistral Cloud Chat Model4`, `Campaign Goal generator`, `image prompt generator base on the goal`):**
  - Thêm Mistral API Key vào credentials `mistralCloudApi`.
  - Kiểm tra model mặc định `mistral-small-latest` (có thể đổi sang các model mạnh hơn tùy nhu cầu).
- **Nodes HTTP Request tạo ảnh (`pollinations.ai`, `pollinations.ai2`, v.v.):**
  - Các node này gọi API tới Pollinations.ai dựa trên prompt được AI sinh ra. Các sếp không cần chuẩn bị API key riêng cho Pollinations vì đây là dịch vụ mở, tuy nhiên hãy kiểm tra URL endpoint để đảm bảo việc truyền prompt diễn ra chính xác.
- **Nodes xử lý dữ liệu (`clean retrived data`, `separate each Prompts`, `Change name to photo...`):**
  - Các node Code và Set này giúp chuẩn hóa tên file, tách các prompt thành các luồng riêng biệt để gọi ảnh song song. Không cần sửa gì nhiều trừ khi muốn đổi định dạng tên file đầu ra.

#### 3. Kích hoạt ⚡️
- Nhấn **Test workflow** tại node `When clicking ‘Test workflow’` để chạy thử nghiệm và kiểm tra kết quả trả về ở Google Drive.
- Sau khi test thành công, bật nút **Active** để đưa workflow vào trạng thái hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Chatbot / Telegram:** Thay vì dùng `manualTrigger`, các sếp có thể đổi thành Webhook hoặc Telegram Trigger để kích hoạt chiến dịch ngay khi chat với bot.
- **Gửi thông báo:** Thêm node Slack hoặc Telegram ở cuối luồng để nhận thông báo kèm link Google Drive ngay khi bộ ảnh chiến dịch hoàn thành.
- **Mở rộng số lượng ảnh:** Có thể nhân bản thêm các node HTTP Request (`pollinations.ai`) và Code đổi tên nếu chiến dịch yêu cầu nhiều hơn 5 hình ảnh mỗi lần chạy.

### 📌 Kết luận
Việc ứng dụng AI vào sáng tạo nội dung chưa bao giờ dễ dàng đến thế. Với sự kết hợp giữa tư duy chiến lược của Mistral AI và khả năng tạo hình ảnh linh hoạt của Pollinations.ai, các sếp hoàn toàn có thể tối ưu hóa hiệu suất đội ngũ marketing ngay hôm nay. Chúc các sếp cài đặt thành công!