---
title: "🚀 Tự Động Hóa Nuôi Dưỡng Lead WhatsApp Cá Nhân Hóa Với Postgres & Gallabox"
description: "Workflow n8n tự động gửi tin nhắn WhatsApp cá nhân hóa cho lead dựa trên lịch trình, lưu trữ dữ liệu vào Postgres và cập nhật trạng thái lead một cách chính xác."
slug: "tu-dong-hoa-nuoi-duong-lead-whatsapp-postgres-gallabox"
tags: [n8n, automation, whatsapp, postgres, lead-nurturing, gallabox]
keywords: [n8n workflow, tự động hóa whatsapp, nuôi dưỡng lead, postgres n8n, gallabox api]
---

# 🚀 Tự Động Hóa Nuôi Dưỡng Lead WhatsApp Cá Nhân Hóa Với Postgres & Gallabox

Trong thế giới marketing hiện đại, việc "nuôi dưỡng" (nurturing) lead là yếu tố sống còn để chuyển đổi khách hàng tiềm năng thành doanh thu thực tế. Tuy nhiên, việc quản lý hàng trăm hoặc hàng nghìn lead với các giai đoạn tương tác khác nhau (lead mới, lead chưa phản hồi, lead đang cân nhắc...) bằng cách thủ công là một cơn ác mộng. Các sếp thường phải đối mặt với tình trạng: quên gửi tin nhắc, gửi sai nội dung cho từng nhóm lead, hoặc mất hàng giờ mỗi ngày chỉ để cập nhật trạng thái lead trong bảng tính.

Workflow **Automated WhatsApp Lead Nurturing** được thiết kế để giải quyết triệt để vấn đề này. Nó hoạt động như một "nhân viên chăm sóc khách hàng" không ngủ, tự động quét cơ sở dữ liệu Postgres, xác định lead cần được liên hệ dựa trên số lần tương tác trước đó (0, 1, 2, 3 lần), tạo ra nội dung tin nhắn cá nhân hóa và gửi đi qua nền tảng Gallabox (WhatsApp Business API). Toàn bộ quy trình diễn ra hoàn toàn tự động, không cần code phức tạp, đảm bảo mọi lead đều nhận được thông điệp đúng lúc, đúng người.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian thủ công:** Hệ thống tự động chạy theo lịch (Schedule Trigger), không cần con người can thiệp để gửi tin nhắn.
- **Cá nhân hóa thông điệp:** Sử dụng node Code để tạo ra các mẫu tin nhắn khác nhau dựa trên "độ chín" của lead (số lần đã liên hệ trước đó), tăng tỷ lệ phản hồi.
- **Quản lý dữ liệu tập trung & chính xác:** Lưu trữ và cập nhật trạng thái lead trực tiếp trong cơ sở dữ liệu Postgres, tránh sai sót do nhập liệu thủ công.
- **Tích hợp liền mạch với WhatsApp:** Gửi tin nhắn qua Gallabox API, đảm bảo tin nhắn đến hộp thoại WhatsApp của khách hàng một cách chuyên nghiệp và đáng tin cậy.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n:** Chạy local hoặc trên VPS.
2. **Cơ sở dữ liệu PostgreSQL:** Một instance Postgres đang hoạt động.
   - Tạo bảng dữ liệu chứa danh sách lead (các trường cần có: `id`, `phone_number`, `name`, `message_count` hoặc trường tương tự để đếm số lần liên hệ, `status`).
   - Tạo Credentials Postgres trong n8n (Host, Port, Database, User, Password).
3. **Tài khoản Gallabox:**
   - Đăng ký và kích hoạt tài khoản Gallabox.
   - Lấy **API Key** hoặc **Access Token** từ dashboard Gallabox.
   - Đảm bảo số điện thoại WhatsApp Business đã được liên kết và có quyền gửi tin nhắn.
4. **Dữ liệu Lead:** Đảm bảo bảng Postgres đã có dữ liệu lead mẫu để test.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from URL** và dán link: `https://n8n.io/workflows/7712` HOẶC copy toàn bộ JSON của workflow và dán vào editor.
3. Sau khi import, các sếp sẽ thấy 7 nodes chính được kết nối với nhau.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Dưới đây là các node quan trọng cần cấu hình chi tiết:

**1. Node `Schedule Trigger`**
- Đây là "trái tim" khởi động quy trình.
- **Cấu hình:** Chọn tần suất chạy (ví dụ: mỗi 15 phút, mỗi 1 giờ, hoặc hàng ngày vào khung giờ vàng).
- *Gợi ý:* Chạy vào giờ hành chính (9:00 - 17:00) để tránh làm phiền khách hàng ngoài giờ làm việc.

**2. Node `Execute a SQL query` (Postgres)**
- **Mục đích:** Lấy danh sách các lead cần được gửi tin nhắn.
- **Cấu hình:**
  - Chọn **Credentials** Postgres đã tạo ở bước chuẩn bị.
  - Trong phần **Query**, các sếp cần viết câu lệnh SQL để lọc lead.
  - *Logic tham khảo từ workflow gốc:* Lấy các lead có `message_count` là 0, 1, 2, hoặc 3. Ví dụ:
    ```sql
    SELECT * FROM leads WHERE message_count IN (0, 1, 2, 3) AND status = 'active';
    ```
  - Đảm bảo kết quả trả về các trường: `id`, `phone_number`, `name`, `message_count`.

**3. Node `Code1`**
- **Mục đích:** Xử lý dữ liệu và tạo nội dung tin nhắn cá nhân hóa.
- **Cấu hình:**
  - Node này chứa đoạn mã JavaScript để "ma trận hóa" (matrix) nội dung.
  - Các sếp cần kiểm tra lại logic trong code:
    - Nếu `message_count` = 0: Gửi tin nhắn chào mừng/lead mới.
    - Nếu `message_count` = 1: Gửi tin nhắn nhắc nhở lần 1.
    - Nếu `message_count` = 2: Gửi tin nhắn ưu đãi/nhắc nhở lần 2.
    - Nếu `message_count` = 3: Gửi tin nhắn chốt đơn/last call.
  - **Quan trọng:** Thay thế các biến trong tin nhắn (ví dụ: `{{ $json.name }}`) để đảm bảo tin nhắn được cá nhân hóa đúng tên khách hàng.

**4. Node `Loop Over Items4` (Split In Batches)**
- **Mục đích:** Xử lý từng lead một để tránh lỗi khi gửi hàng loạt và dễ kiểm soát lỗi.
- **Cấu hình:**
  - **Batch Size:** Đặt là `1` (xử lý từng item một).
  - Đảm bảo node này được kết nối đúng với node `new_lead_4` (gửi tin) và node `Update rows in a table4` (cập nhật DB).

**5. Node `new_lead_4` (HTTP Request)**
- **Mục đích:** Gọi API Gallabox để gửi tin nhắn WhatsApp.
- **Cấu hình:**
  - **Method:** POST.
  - **URL:** API endpoint của Gallabox (thường là `https://api.gallabox.com/v1/whatsapp/send` hoặc tương tự, kiểm tra tài liệu Gallabox).
  - **Headers:** Thêm Header `Authorization: Bearer [YOUR_GALLABOX_API_KEY]`.
  - **Body:** Cấu hình JSON body theo yêu cầu của Gallabox. Ví dụ:
    ```json
    {
      "to": "{{ $json.phone_number }}",
      "message": "{{ $json.personalized_message }}",
      "type": "text"
    }
    ```
  - *Lưu ý:* Đảm bảo số điện thoại có mã quốc gia (ví dụ: `84912345678` cho Việt Nam).

**6. Node `Update rows in a table4` (Postgres)**
- **Mục đích:** Cập nhật trạng thái lead sau khi gửi tin nhắn thành công.
- **Cấu hình:**
  - Chọn **Credentials** Postgres.
  - **Table:** Chọn bảng lead.
  - **Where Clause:** `id = {{ $json.id }}`.
  - **Update Fields:**
    - Tăng `message_count` lên 1 (ví dụ: `message_count = message_count + 1`).
    - Cập nhật `last_contact_date` là ngày hiện tại.
    - Có thể đổi `status` nếu cần (ví dụ: sang 'nurturing').

**7. Node `Insert rows in a table4` (Postgres)**
- **Mục đích:** (Tùy chọn) Lưu log lịch sử gửi tin nhắn vào một bảng log riêng để truy vết.
- **Cấu hình:**
  - Chọn bảng log (ví dụ: `whatsapp_logs`).
  - Điền các trường: `lead_id`, `message_content`, `sent_at`, `status`.

#### 3. Kích hoạt ⚡️
1. **Test Run:**
   - Chạy thử workflow với 1-2 lead mẫu.
   - Kiểm tra xem tin nhắn có đến đúng số điện thoại WhatsApp không.
   - Kiểm tra xem dữ liệu trong Postgres có được cập nhật `message_count` không.
2. **Bật Active:**
   - Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải n8n.
   - Workflow sẽ tự động chạy theo lịch đã thiết lập trong `Schedule Trigger`.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram Alert:** Thêm node `Slack` hoặc `Telegram` sau node `new_lead_4` để gửi thông báo cho đội sales khi một lead phản hồi hoặc khi có lỗi xảy ra trong quá trình gửi tin.
- **A/B Testing Nội Dung:** Sử dụng node `Code` để ngẫu nhiên chọn 2-3 mẫu tin nhắn khác nhau cho cùng một nhóm lead, sau đó đo lường tỷ lệ phản hồi để tối ưu nội dung.
- **Tự động Dừng Gửi:** Thêm điều kiện trong node `Code` hoặc `IF` để dừng gửi tin cho các lead đã phản hồi hoặc đã mua hàng (cập nhật `status` trong Postgres).
- **Lưu trữ Log Chi Tiết:** Đảm bảo node `Insert rows in a table4` hoạt động tốt để các sếp có thể truy xuất lịch sử giao tiếp, phục vụ cho việc phân tích hiệu quả chiến dịch.

### 📌 Kết luận
Workflow **Automated WhatsApp Lead Nurturing** là công cụ mạnh mẽ giúp các sếp tự động hóa hoàn toàn quy trình chăm sóc khách hàng qua WhatsApp. Với sự kết hợp giữa Postgres (dữ liệu), Code (cá nhân hóa), và Gallabox (gửi tin), các sếp có thể tập trung vào việc xây dựng chiến lược marketing thay vì mất thời gian cho các tác vụ lặp đi lặp lại. Hãy import, cấu hình và bắt đầu tự động hóa ngay hôm nay để tăng tỷ lệ chuyển đổi và tối ưu hóa chi phí marketing!