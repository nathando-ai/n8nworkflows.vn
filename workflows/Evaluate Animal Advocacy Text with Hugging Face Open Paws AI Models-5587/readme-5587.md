---
title: "🐾 Đánh giá văn bản bảo vệ động vật tự động bằng Hugging Face AI Models trong n8n"
description: "Hướng dẫn sử dụng sub-workflow n8n kết hợp Hugging Face AI Models từ Open Paws để chấm điểm hiệu suất và sở thích cho nội dung bảo vệ quyền lợi động vật."
slug: "danh-gia-van-ban-bao-ve-dong-vat-hugging-face-n8n"
tags: [n8n, automation, ai, hugging-face, machine-learning, animal-advocacy]
keywords: [n8n workflow, hugging face api, open paws, ai summarization, market research, tự động hóa n8n]
---

# 🐾 Đánh giá văn bản bảo vệ động vật tự động bằng Hugging Face AI Models

Trong các chiến dịch truyền thông bảo vệ quyền lợi động vật, việc đo lường xem một đoạn văn bản (bài viết, bài đăng mạng xã hội, email) có thực sự chạm đến cảm xúc và thu hút người đọc hay không thường tốn rất nhiều thời gian thử nghiệm thủ công. Các sếp làm truyền thông hoặc nghiên cứu thị trường thường phải "đoán mò" hiệu quả của nội dung.

Giải pháp là gì? Workflow n8n này được phát triển bởi **Open Paws** (tổ chức phi lợi nhuận chuyên xây dựng các công cụ AI mã nguồn mở cho hoạt động bảo vệ động vật), giúp tự động hóa 100% quy trình đánh giá văn bản thông qua các mô hình AI chuyên biệt trên Hugging Face.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Chấm điểm tự động:** Đánh giá chính xác điểm hiệu suất văn bản (*Text Performance Prediction*) và mức độ yêu thích của cộng đồng bảo vệ động vật (*Animal Advocate Preference Prediction*).
- **Tiết kiệm thời gian:** Thay vì phỏng vấn hay thử nghiệm A/B thủ công tốn kém, AI sẽ cho kết quả phân tích trong tích tắc.
- **Tối ưu hóa chiến dịch:** Giúp lọc và chọn ra những thông điệp sắc bén nhất trước khi tung ra chiến dịch quy mô lớn.
- **Hoạt động linh hoạt:** Được thiết kế dưới dạng sub-workflow, dễ dàng tích hợp vào bất kỳ hệ thống tự động hóa marketing nào của các sếp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động.
- Tài khoản **Hugging Face** có quyền tạo Inference Endpoints và API Access Token.
- Hai mô hình AI đã được deploy làm Inference Endpoints trên Hugging Face:
  1. [Animal Advocate Preference Prediction (Longform)](https://huggingface.co/open-paws/animal_advocate_preference_prediction_longform)
  2. [Text Performance Prediction (Longform)](https://huggingface.co/open-paws/text_performance_prediction_longform)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một Sub-Workflow mới trong n8n, sau đó copy toàn bộ mã JSON của workflow này (ID: 5587 trên thư viện n8n) và dán trực tiếp vào trình soạn thảo của n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Vì đây là một sub-workflow nhận dữ liệu đầu vào và trả kết quả về workflow chính, các sếp cần chú ý cấu hình các node sau:

- **Node `When Executed by Another Workflow` (`executeWorkflowTrigger`):** Đảm bảo node này nhận đúng định dạng dữ liệu đầu vào (text cần đánh giá) từ workflow gọi nó.
- **Node `Get Performance Score` & `Get Preference Score` (`httpRequest`):** 
  - Tại đây các sếp cần điền **Inference Endpoint URL** tương ứng đã lấy sau khi deploy hai mô hình trên Hugging Face.
  - Thiết lập **Credentials**: Chọn hoặc tạo mới `huggingFaceApi` bằng cách nhập Hugging Face Access Token của các sếp để xác thực quyền gọi API.
- **Các node Set (`Set Performance Score`, `Get Preference Score2`, `Set Output`):** Dùng để tinh chỉnh, ánh xạ và đóng gói kết quả trả về thành một định dạng gọn gàng, dễ đọc cho bước tiếp theo.
- **Node `Merge Branches` & `Create Single Item` (`merge`, `aggregate`):** Gom dữ liệu từ hai nhánh gọi API song song lại với nhau thành một đối tượng duy nhất trước khi trả kết quả về workflow cha.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test run) với một đoạn văn bản mẫu để kiểm tra xem Hugging Face Endpoint có trả về điểm số chính xác không.
- Sau khi test thành công, lưu lại và sẵn sàng để kết nối với các workflow chính.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Slack/Telegram Bot:** Các sếp có thể mở rộng workflow chính bằng cách nhận văn bản qua tin nhắn chat, gọi sub-workflow này và gửi lại báo cáo điểm số ngay lập tức lên nhóm làm việc.
- **Lưu trữ dữ liệu vào Google Sheets / Airtable:** Tự động ghi lại lịch sử các bài viết đã đánh giá cùng điểm số AI để đội ngũ content dễ dàng theo dõi và rút kinh nghiệm.
- **Chấm điểm hàng loạt:** Kết hợp thêm node lặp (Loop) hoặc xử lý mảng để đánh giá hàng chục bài viết PR/Marketing cùng một lúc trước khi lên lịch đăng bài.

### 📌 Kết luận
Việc tích hợp AI chuyên ngành vào quy trình tự động hóa chưa bao giờ dễ dàng đến thế với các công cụ mã nguồn mở từ Open Paws. Hãy áp dụng ngay workflow này để nâng cao chất lượng nội dung truyền thông, giúp tối ưu hóa nguồn lực và mang lại tác động lớn hơn cho các chiến dịch ý nghĩa của các sếp!