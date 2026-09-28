---
title: "🚀 Tự động hóa báo cáo OTIF chuỗi cung ứng hàng tuần với AI và Notion"
description: "Hướng dẫn xây dựng workflow n8n tự động tổng hợp dữ liệu giao hàng TMS/WMS, tính toán KPI OTIF, phân tích chuyên sâu bằng GPT-4o và lưu trữ trực tiếp lên Notion dashboard."
slug: "tu-dong-hoa-bao-cao-otif-chuoi-cung-ung-notion-gpt4o"
tags: [n8n, automation, supply-chain, ai-summary, notion, gpt-4o]
keywords: [n8n workflow, OTIF report, chuỗi cung ứng, tự động hóa Notion, GPT-4o supply chain, n8n AI agent]
---

# 🚀 Tự động hóa báo cáo OTIF chuỗi cung ứng hàng tuần với AI và Notion

Việc tổng hợp dữ liệu vận chuyển từ các hệ thống TMS (Transportation Management System) và WMS (Warehouse Management System), tính toán các chỉ số cốt lõi như **OTIF (On-Time In-Full)**, lead time và viết báo cáo phân tích hiệu suất hàng tuần thường ngốn rất nhiều thời gian của các nhà quản lý logistics. Nếu làm thủ công, đội ngũ không chỉ dễ mắc sai sót mà còn chậm trễ trong việc đưa ra quyết định tối ưu.

Workflow n8n này do chuyên gia **Samir Saci** thiết kế sẽ giải quyết triệt để bài toán trên bằng cách tự động hóa 100% quy trình: gom nhóm dữ liệu, tính toán KPI theo tuần, nhờ AI (GPT-4o) phân tích nguyên nhân gốc rễ và tự động đẩy toàn bộ báo cáo lên Notion dashboard một cách chuyên nghiệp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Chạy định kỳ hàng tuần nhờ lịch trình tự động, loại bỏ hoàn toàn các bảng tính Excel thủ công.
- **Phân tích thông minh bằng AI:** GPT-4o không chỉ tính toán mà còn viết nhận xét chi tiết về hiệu suất từng tuần và đưa ra đánh giá tổng quan (Global Summary) kèm xu hướng.
- **Quản lý tập trung trên Notion:** Lưu trữ toàn bộ dữ liệu chỉ số OTIF và các thẻ phân tích (Performance Cards) trực quan trong workspace của công ty.
- **Ra quyết định nhanh chóng:** Cung cấp bức tranh toàn cảnh về chuỗi cung ứng ngay khi bắt đầu tuần mới, giúp phát hiện sớm các nút thắt cổ chai trong logistics.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **OpenAI API Key:** Để sử dụng các model `gpt-4o-mini` trong AI Agent.
- **Notion Integration:** Tài khoản Notion và tích hợp (Integration Token) có quyền truy cập vào các database quản lý chuỗi cung ứng.
- **Dữ liệu nguồn:** Nguồn dữ liệu lô hàng từ TMS/WMS được kết nối qua DataTable hoặc Database tích hợp trong n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ nguồn cấp hoặc copy trực tiếp mã nguồn JSON, sau đó dán (Paste) vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:
- **Weekly Trigger:** Cấu hình thời gian chạy định kỳ (ví dụ: sáng thứ Hai hàng tuần).
- **Collect Shipments from TMS & WMS (`dataTable`):** Trỏ tới nguồn dữ liệu lô hàng thực tế của doanh nghiệp.
- **OpenAI Chat Model & OpenAI Chat Model Global (`lmChatOpenAi`):** Thêm credentials OpenAI API Key và chọn model mong muốn (`gpt-4o-mini` hoặc `gpt-4o`).
- **AI Agent Weekly Performance Summary & AI Agent Global Performance Summary (`agent`):** Kiểm tra lại các prompt mẫu để tinh chỉnh phong cách ngôn ngữ (tiếng Việt hoặc tiếng Anh) cho phù hợp với doanh nghiệp.
- **Fill the report, Create Weekly Performance Card, Update Global Performance Summary (`notion`):** Kết nối tài khoản Notion, sau đó map chính xác các **Database ID** tương ứng trong workspace của các sếp.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm với dữ liệu mẫu, kiểm tra xem Notion đã nhận được bản ghi mới chưa.
- Sau khi test thành công, bật nút **Active** ở góc trên bên phải để workflow tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo:** Bổ sung thêm node Telegram hoặc Slack ở cuối workflow để bắn thông báo ngay vào group chat của bộ phận Supply Chain khi báo cáo Notion mới được tạo xong.
- **Lưu lịch sử lỗi (Error Logging):** Thêm Error Trigger để ghi nhận lại nếu kết nối API với OpenAI hoặc Notion gặp sự cố gián đoạn.
- **Mở rộng KPI:** Tùy chỉnh code trong node `Aggregate by Week` để tính thêm các chỉ số đặc thù của doanh nghiệp như tỷ lệ hàng lỗi, chi phí vận chuyển trung bình trên mỗi đơn hàng.

### 📌 Kết luận
Workflow tự động hóa báo cáo OTIF kết hợp Notion và GPT-4o này là cỗ máy đắc lực giúp tối ưu hóa vận hành logistics cho các nhà quản lý. Hãy cài đặt ngay hôm nay để tiết kiệm hàng chục giờ làm việc thủ công mỗi tháng và nâng tầm chiến lược chuỗi cung ứng của doanh nghiệp!