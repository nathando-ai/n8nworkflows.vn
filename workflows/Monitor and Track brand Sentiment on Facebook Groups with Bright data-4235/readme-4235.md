---
title: "🚀 Tự động giám sát và phân tích cảm xúc thương hiệu trên Facebook Groups với Bright Data và AI"
description: "Hướng dẫn xây dựng hệ thống tự động quét bài viết từ các hội nhóm Facebook bằng Bright Data, phân tích cảm xúc bằng AI OpenRouter và lưu trữ kết quả lên Google Sheets."
slug: "tu-dong-giam-sat-cam-xuc-thuong-hieu-facebook-groups-bright-data-ai"
tags: [n8n, automation, no-code, facebook, ai, bright-data]
keywords: [n8n workflow, giám sát thương hiệu, facebook groups, sentiment analysis, bright data, openrouter ai, google sheets]
---

# 🚀 Tự động giám sát và phân tích cảm xúc thương hiệu trên Facebook Groups với AI

Các sếp làm Marketing chắc chắn hiểu rõ nỗi đau: Việc thủ công lướt hàng chục hội nhóm Facebook mỗi ngày để tìm xem khách hàng đang khen hay chê sản phẩm của mình vừa tốn thời gian, vừa dễ bỏ lỡ thông tin quan trọng. Chưa kể việc tổng hợp và phân tích cảm xúc (Positive/Negative/Neutral) lại càng mất sức.

Đừng lo, workflow n8n cực kỳ mạnh mẽ này do chuyên gia Imperol thiết kế sẽ giúp các sếp tự động hóa 100% quy trình: Quét bài viết hội nhóm qua Bright Data API, lọc tên thương hiệu, phân tích cảm xúc bằng AI (OpenRouter), trích xuất insight và lưu toàn bộ kết quả gọn gàng vào Google Sheets. Tất cả diễn ra tự động mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 24/7:** Lên lịch chạy định kỳ (`Schedule Trigger`) để không bỏ lỡ bất kỳ bài thảo luận nào về thương hiệu.
- **Sức mạnh AI (OpenRouter):** Tự động phân tích cảm xúc (Tích cực, Tiêu cực, Trung tính), trích xuất tóm tắt nội dung, phân loại danh mục và insights chuyên sâu.
- **Dữ liệu trực quan:** Toàn bộ kết quả được đẩy thẳng về Google Sheets để các sếp dễ dàng báo cáo và đưa ra chiến lược xử lý khủng hoảng hoặc chăm sóc khách hàng kịp thời.
- **Tiết kiệm 90% thời gian:** Không còn cảnh nhân sự phải "cắm mặt" lướt Facebook tìm bài viết thủ công nữa.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **n8n Instance:** Đã cài đặt sẵn sàng (Self-hosted hoặc Cloud).
- **Bright Data Account:** Tài khoản Bright Data để sử dụng dịch vụ Web Scraping thu thập dữ liệu Facebook Groups.
- **OpenRouter API Key:** Để sử dụng các mô hình AI thông minh phục vụ việc phân tích cảm xúc và trích xuất thông tin.
- **Google Sheets:** Tài khoản Google để lưu trữ danh sách link nhóm, tên thương hiệu và nhận kết quả quét.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và dán trực tiếp vào n8n Editor của mình, hoặc import file JSON tải từ trang gốc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình chính xác các node trọng điểm sau:

- **Chuẩn bị Google Sheet:** Hãy copy mẫu Google Sheet chính thức tại đây: [Google Sheet Template](https://docs.google.com/spreadsheets/d/1TXF_xLPF7XJJakoWB5Ix-tTduvX3GRxocJcp6DA-U_A/edit?usp=sharing). Sheet này sẽ chứa danh sách link nhóm Facebook cần theo dõi và tên thương hiệu của các sếp.
- **Node `Set up KEYS`:** Điền các thông tin API Key của Bright Data và các biến cấu hình cần thiết vào đây.
- **Node `Get links` & `Get Brand names` (Google Sheets):** Kết nối với tài khoản Google Sheets của các sếp và trỏ đúng đến file mẫu vừa copy ở trên.
- **Node `OpenRouter Chat Model` & `OpenRouter Chat Model1`:** Chọn credentials `openRouterApi` và điền API Key từ OpenRouter của các sếp để kích hoạt AI.
- **Node `Receive results` (Webhook):** Đảm bảo webhook URL nhận kết quả trả về từ Bright Data được cấu hình đúng để hệ thống nhận dữ liệu bất đồng bộ.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (`Test workflow`) với một vài nhóm mẫu để kiểm tra luồng dữ liệu từ Bright Data qua AI rồi đổ về Google Sheets.
- Sau khi test thành công, bật nút **Active** để workflow tự động chạy theo lịch của `Schedule Trigger`.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo tức thời:** Thêm node Telegram hoặc Slack ngay sau bước phân tích cảm xúc. Nếu AI phát hiện bài viết có cảm xúc *Negative* (Tiêu cực), hệ thống sẽ bắn thông báo khẩn cấp ngay lập tức để đội ngũ CSKH vào xử lý khủng hoảng truyền thông.
- **Báo cáo định kỳ:** Kết hợp thêm node Schedule vào cuối tuần để tổng hợp số lượng bài viết tích cực/tiêu cực và gửi email báo cáo tự động cho quản lý.
- **Mở rộng từ khóa:** Ngoài tên thương hiệu chính, các sếp có thể cấu hình thêm các từ khóa viết tắt, tên sản phẩm cụ thể vào Google Sheets để AI quét sâu hơn.

### 📌 Kết luận
Việc giám sát thương hiệu trên mạng xã hội chưa bao giờ dễ dàng và tự động đến thế với sự kết hợp hoàn hảo giữa n8n, Bright Data và AI. Hãy cài đặt ngay workflow này để nắm thế chủ động trong mọi chiến dịch Marketing và bảo vệ uy tín thương hiệu của các sếp!