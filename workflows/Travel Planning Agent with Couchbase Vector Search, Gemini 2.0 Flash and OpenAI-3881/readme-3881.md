---
title: "🌍 [Tự động hóa Lập kế hoạch du lịch với Couchbase Vector Search, Gemini 2.0 Flash và OpenAI]"
description: "Hướng dẫn tự động hóa hoàn toàn quy trình lập kế hoạch du lịch bằng n8n, kết hợp công nghệ tìm kiếm vector của Couchbase, mô hình ngôn ngữ Gemini 2.0 Flash và OpenAI Embeddings."
slug: "tu-dong-hoa-lap-ke-hoach-du-lich-voi-couchbase-gemini-openai"
tags: [n8n, automation, no-code, AI, travel planning, vector search]
keywords: [n8n workflow, tự động hóa du lịch, Couchbase Vector Search, Gemini 2.0 Flash, OpenAI Embeddings]
---

# 🌍 Tự động hóa Lập kế hoạch du lịch với Couchbase Vector Search, Gemini 2.0 Flash và OpenAI

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn quy trình lập kế hoạch du lịch
- Tiết kiệm thời gian lên đến 80% so với phương pháp thủ công
- Cung cấp gợi ý du lịch cá nhân hóa dựa trên sở thích và lịch sử
- Hệ thống hoạt động liên tục 24/7 với dữ liệu cập nhật liên tục
- Tích hợp nhiều nguồn thông tin du lịch từ khắp nơi trên thế giới
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google API cho Gemini LLM
- Tài khoản OpenAI API
- Couchbase cluster (có thể sử dụng Couchbase Capella trên cloud)
- Database credentials với quyền truy cập phù hợp
- Bucket, scope và collection trong Couchbase (recommend: Bucket: `travel-agent`, Scope: `vectors`, Collection: `points-of-interest`)
- File JSON cho search index (có sẵn [tại đây](https://gist.github.com/ejscribner/6f16343d4b44b1af31e8f344557814b0))
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import from URL" và dán link sau: `https://n8n.io/workflows/3881`
3. Hoặc tải file JSON về và import từ local

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Webhook"**:
   - Đảm bảo đã cấu hình đúng path và HTTP method (POST)
   - Lưu ý URL webhook sẽ được sử dụng trong các bước tiếp theo

2. **Node "Google Gemini Chat Model"**:
   - Tạo và cấu hình Google API Credentials
   - Chọn mô hình Gemini 2.0 Flash

3. **Node "Generate OpenAI Embeddings"**:
   - Tạo và cấu hình OpenAI API Credentials
   - Chọn mô hình `text-embedding-3-small`

4. **Couchbase Configuration**:
   - Tạo Couchbase cluster (có thể sử dụng Couchbase Capella)
   - Thêm database credentials với quyền truy cập phù hợp
   - Cấu hình Allowed IP addresses (sử dụng `0.0.0.0/0` cho dễ dàng test)
   - Tạo bucket, scope và collection như hướng dẫn
   - Import search index từ file JSON đã cung cấp

5. **Node "Insert docs with Couchbase Search Vector"**:
   - Cấu hình kết nối đến Couchbase cluster của bạn
   - Đảm bảo bucket, scope và collection đã được tạo đúng

#### 3. Kích hoạt ⚡️
1. Kích hoạt workflow bằng cách nhấn nút "Activate" trên thanh công cụ
2. Test với dữ liệu mẫu bằng cách sử dụng CURL command đã cung cấp
3. Sau khi xác nhận hoạt động, bạn có thể sử dụng shell script để bulk insert dữ liệu

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp với các nền tảng khác**: Kết nối workflow với Slack, Telegram hoặc email để nhận thông báo về các gợi ý du lịch mới
2. **Lưu log hoạt động**: Thêm node để lưu log các truy vấn và phản hồi của hệ thống
3. **Tạo báo cáo định kỳ**: Sử dụng node "Schedule Trigger" để gửi báo cáo hàng tuần về các điểm du lịch mới được thêm vào hệ thống
4. **Mở rộng dữ liệu**: Kết nối với các API du lịch khác để tự động cập nhật thông tin điểm du lịch mới nhất

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động hóa lập kế hoạch du lịch, giúp các sếp tiết kiệm thời gian và cung cấp trải nghiệm du lịch cá nhân hóa. Bằng cách tích hợp công nghệ tìm kiếm vector của Couchbase, mô hình ngôn ngữ Gemini 2.0 Flash và OpenAI Embeddings, hệ thống có thể cung cấp các gợi ý du lịch chính xác và liên quan đến nhu cầu của từng người dùng. Hãy áp dụng ngay để nâng cao trải nghiệm du lịch của khách hàng và tối ưu hóa quy trình kinh doanh của bạn!