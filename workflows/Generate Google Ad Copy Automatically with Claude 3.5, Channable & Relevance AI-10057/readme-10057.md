---
title: "🚀 Tự Động Tạo Nội Dung Quảng Cáo Google Ads Với Claude 3.5, Channable & Relevance AI"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa 100% việc lấy dữ liệu sản phẩm, tạo quảng cáo chuẩn ký tự và kiểm duyệt chính sách Google Ads."
slug: "tu-dong-tao-quang-cao-google-ads-claude-35-relevance-ai"
tags: [n8n, automation, google-ads, relevance-ai, claude-35, content-creation]
keywords: [n8n workflow, tạo quảng cáo google tự động, relevance ai, channable, claude 3.5, kiểm duyệt quảng cáo]
---

# 🚀 Tự Động Tạo Nội Dung Quảng Cáo Google Ads Với Claude 3.5, Channable & Relevance AI

Các sếp chạy quảng cáo Google Ads chắc chắn đã từng đau đầu với việc phải viết hàng trăm, hàng ngàn tiêu đề (Headline) và mô tả (Description) cho các sản phẩm khác nhau. Việc viết thủ công không chỉ tốn thời gian, dễ sai sót ký tự (dẫn đến bị Google từ chối phê duyệt) mà còn cực kỳ mệt mỏi mỗi khi danh mục sản phẩm thay đổi.

Đừng lo, bài viết này sẽ hướng dẫn các sếp cách thiết lập một workflow n8n cực kỳ mạnh mẽ do **Nikan Noorafkan** xây dựng. Workflow này sẽ tự động hóa toàn bộ quy trình: lấy feed sản phẩm từ Channable, sử dụng sức mạnh của **Claude 3.5 (thông qua Relevance AI)** để viết ad copy, kiểm tra giới hạn ký tự bằng JavaScript, kiểm duyệt chính sách Google Ads, và cuối cùng lưu kết quả vào Google Sheets hoặc gửi thông báo qua Slack.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần viết content thủ công cho từng sản phẩm trong feed.
- **Chuẩn chính sách 100%:** Tự động kiểm tra độ dài ký tự (Tiêu đề $\le$ 30, Mô tả $\le$ 90) và quét lỗi chính sách Google Ads trước khi xuất bản.
- **Vận hành tự động 24/7:** Chạy ngầm mỗi nửa đêm để làm mới nội dung quảng cáo nhờ `Schedule Trigger - Daily1`.
- **Quản lý tập trung:** Toàn bộ dữ liệu được tổng hợp gọn gàng vào Google Sheets và thông báo trạng thái qua Slack.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản Channable (hoặc nguồn Product Feed khác):** Để lấy dữ liệu sản phẩm (tên, giá, thương hiệu, mô tả...).
- **Tài khoản Relevance AI:** Nơi cấu hình công cụ tạo text quảng cáo (Tool ID) và Agent kiểm duyệt (Agent ID) tích hợp mô hình Claude 3.5 / GPT-4.
- **Google Sheets & Slack Workspace:** Để lưu trữ dữ liệu đầu ra và nhận thông báo trạng thái (thành công/cảnh báo vi phạm).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ nguồn gốc hoặc copy đoạn JSON và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 13 nodes hoạt động nhịp nhàng với nhau. Các sếp cần cấu hình kỹ các điểm sau:

- **Node `Schedule Trigger - Daily1`:** Mặc định chạy vào lúc nửa đêm (`0 0 * * *`). Các sếp có thể đổi lịch hoặc bấm nút "Execute Workflow" để test thủ công bất cứ lúc nào.
- **Node `Get Product Feed` (HTTP Request):** 
  - Kết nối Authentication (`httpHeaderAuth`).
  - Trỏ tới API endpoint của Channable: `{{$env.CHANNABLE_API_URL}}/v1/projects/{{$env.PROJECT_ID}}/items` (hoặc thay thế bằng API nguồn sản phẩm của website các sếp).
- **Node `Split Into Batches1`:** Chia nhỏ dữ liệu thành các gói (mặc định 50 sản phẩm/batch) để tránh chạm ngưỡng giới hạn (Rate Limits) của API Relevance AI.
- **Node `Generate Ad Copy - Relevance AI1` (HTTP Request):**
  - Gọi API Tool của Relevance AI (`/tools/google_text_ad_copy_generator/run`).
  - Truyền các thông tin sản phẩm (title, description, price, brand, category) để Claude 3.5 viết nội dung quảng cáo.
- **Node `Validate Character Limits1` (Code):** Chạy đoạn code JavaScript tự động đếm ký tự, cắt gọt phần thừa để đảm bảo Tiêu đề $\le$ 30 ký tự và Mô tả $\le$ 90 ký tự, tránh việc quảng cáo bị Google từ chối.
- **Node `Compliance Check Agent1` (HTTP Request):** Gửi nội dung ad copy tới Relevance AI Agent (`/agents/google_ads_compliance_checker/run`) để quét lỗi từ ngữ nhạy cảm, viết hoa quá đà, thiếu minh bạch và trả về trạng thái `APPROVED` hoặc `REJECTED`.
- **Node `IF Compliant1` & Các nhánh xử lý:**
  - Nếu **Đạt chuẩn (APPROVED)**: Tiến hành lưu vào Google Sheets thông qua node `Save to Google Sheets` và gửi tin nhắn thành công qua Slack (`Success Notification1`).
  - Nếu **Không đạt (REJECTED)**: Gửi cảnh báo ngay lập tức qua Slack (`Alert - Non-Compliant`) để đội ngũ content kiểm tra lại.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm với 1 batch nhỏ để kiểm tra kết quả trả về ở Google Sheets.
- Sau khi mọi thứ mượt mà, gạt công tắc sang **Active** để hệ thống tự động chạy ngầm mỗi ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Thay vì chỉ dùng Slack, các sếp có thể tích hợp thêm node Telegram để nhận thông báo cảnh báo lỗi (`Alert - Non-Compliant`) trực tiếp vào điện thoại cá nhân.
- **Tùy biến Prompt:** Tinh chỉnh prompt bên trong Relevance AI Tool để Claude 3.5 viết ad copy theo đúng văn phong (Tone of Voice) riêng của thương hiệu các sếp.
- **Lưu lịch sử chạy:** Thêm node Google Sheets phụ để ghi log mỗi lần chạy (số lượng sản phẩm thành công, số lượng lỗi) nhằm dễ dàng theo dõi hiệu suất hệ thống.

### 📌 Kết luận
Tự động hóa việc tạo nội dung quảng cáo với AI không chỉ giúp giải phóng sức lao động mà còn tối ưu hóa hiệu suất chạy Ads nhờ tính chính xác cao và tốc độ thần tốc. Hãy cài đặt ngay workflow này để nâng cấp quy trình Marketing của doanh nghiệp các sếp lên một tầm cao mới!