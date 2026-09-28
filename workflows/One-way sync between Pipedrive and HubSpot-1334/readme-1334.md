---
title: "🔄 Đồng bộ Pipedrive sang HubSpot tự động 100% với n8n"
description: "Giải pháp tự động hóa đồng bộ danh sách khách hàng (Contacts) từ Pipedrive sang HubSpot theo lịch trình định kỳ, giúp đội Sales không bao giờ phải nhập liệu thủ công."
slug: "dong-bo-pipedrive-sang-hubspot-tu-dong"
tags: [n8n, crm, sales-automation, pipedrive, hubspot, no-code]
keywords: [n8n workflow, đồng bộ CRM, Pipedrive HubSpot, tự động hóa sales, n8n integration]
---

# 🔄 Đồng bộ Pipedrive sang HubSpot tự động 100% với n8n

Trong môi trường kinh doanh hiện đại, việc quản lý khách hàng thường bị phân tán trên nhiều nền tảng khác nhau. Rất nhiều doanh nghiệp sử dụng **Pipedrive** để quản lý quy trình bán hàng (Sales Pipeline) nhưng lại dùng **HubSpot** cho các chiến dịch Marketing hoặc quản lý quan hệ khách hàng tổng thể.

Nỗi đau lớn nhất ở đây là: **Nhập liệu thủ công.**
Mỗi khi có một khách hàng mới được thêm vào Pipedrive, nhân viên Sales phải mở HubSpot, tìm kiếm và sao chép thông tin sang đó. Việc này không chỉ tốn thời gian, dễ gây sai sót (sai email, sai số điện thoại) mà còn làm chậm tốc độ phản hồi của đội Marketing.

Workflow này được thiết kế để giải quyết triệt để vấn đề đó. Nó sẽ tự động quét dữ liệu từ Pipedrive và đẩy sang HubSpot theo lịch trình cố định (ví dụ: mỗi 15 phút, mỗi giờ hoặc mỗi ngày). Các sếp không cần viết một dòng code nào, chỉ cần cấu hình credentials là xong.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, đặc biệt là các tác vụ cron (định kỳ), các sếp nên cài n8n trên VPS riêng (Self-hosted) để tránh giới hạn về số lần chạy (execution limit) của bản miễn phí hoặc cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian nhập liệu:** Không còn cảnh copy-paste dữ liệu khách hàng giữa hai hệ thống.
- **Dữ liệu luôn nhất quán:** Đảm bảo thông tin khách hàng trong HubSpot luôn cập nhật theo thời gian thực (hoặc gần thời gian thực) từ nguồn gốc Pipedrive.
- **Tăng tốc độ Marketing:** Đội Marketing có thể tiếp cận khách hàng mới ngay lập tức sau khi họ được thêm vào Pipedrive.
- **Giảm thiểu sai sót con người:** Loại bỏ hoàn toàn lỗi do gõ sai email hoặc thiếu sót thông tin liên hệ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n:** Bản miễn phí hoặc Self-hosted.
2. **Tài khoản Pipedrive:** Có quyền truy cập vào danh sách Persons/Contacts.
3. **Tài khoản HubSpot:** Có quyền tạo/sửa Contact.
4. **API Keys/Credentials:**
   - Pipedrive API Token.
   - HubSpot Private App Token (khuyến nghị) hoặc OAuth2.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from File** hoặc **Import from URL**.
3. Dán link workflow gốc: `https://n8n.io/workflows/1334` hoặc tải file JSON về và import.
4. Workflow sẽ hiển thị với 5 nodes chính: `Cron`, `Pipedrive`, `Merge`, `Hubspot` (lấy dữ liệu), và `HubSpot2` (đẩy dữ liệu).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Đây là phần quan trọng nhất. Các sếp cần click vào từng node và cấu hình như sau:

**1. Node `Cron` (Định kỳ chạy)**
- Mặc định workflow có thể được thiết lập chạy theo chu kỳ nhất định.
- Các sếp nên chỉnh **Interval** (ví dụ: `15 minutes`, `1 hour`) tùy thuộc vào tần suất cập nhật khách hàng mới của doanh nghiệp.
- *Lưu ý:* Nếu chạy quá thường xuyên (ví dụ mỗi 1 phút), có thể gây áp lực lên API của HubSpot/Pipedrive.

**2. Node `Pipedrive` (Nguồn dữ liệu)**
- **Operation:** Chọn `Get All`.
- **Resource:** Chọn `Person` (hoặc `Contact` tùy phiên bản API, nhưng trong workflow này là `Person`).
- **Credentials:** Chọn hoặc tạo mới credential Pipedrive.
- **Filter (Quan trọng):** Để tránh việc đẩy toàn bộ lịch sử khách hàng cũ mỗi lần chạy, các sếp nên thêm bộ lọc (Filter) trong node này.
  - *Gợi ý:* Lọc theo `created_at` lớn hơn thời gian chạy lần trước, hoặc sử dụng logic "Only new items" nếu n8n hỗ trợ trong cấu hình node cụ thể. Tuy nhiên, với cấu trúc `Merge` bên dưới, workflow này có vẻ đang so sánh dữ liệu. Hãy đảm bảo bạn hiểu rõ logic so sánh.

**3. Node `Hubspot` (Kiểm tra dữ liệu hiện có)**
- **Operation:** Chọn `Get All`.
- **Resource:** Chọn `Contact`.
- **Credentials:** Chọn credential HubSpot.
- *Mục đích:* Node này lấy danh sách contact hiện có trong HubSpot để so sánh với dữ liệu từ Pipedrive (thông qua node Merge).

**4. Node `Merge` (Ghép dữ liệu)**
- Node này kết nối dữ liệu từ `Pipedrive` và `Hubspot`.
- Các sếp cần kiểm tra **Mode** của Merge (thường là `Append` hoặc `Combine by position`).
- *Lưu ý kỹ thuật:* Workflow này có vẻ đang thực hiện việc so sánh (diff) dữ liệu. Nếu các sếp muốn đơn giản hóa, có thể thay thế logic Merge + Hubspot (get all) bằng một node **IF** hoặc **Code** để chỉ đẩy những contact nào có email/số điện thoại chưa tồn tại trong HubSpot. Tuy nhiên, hãy giữ nguyên cấu trúc gốc và test kỹ trước khi thay đổi.

**5. Node `HubSpot2` (Đẩy dữ liệu)**
- **Operation:** Chọn `Create` (hoặc `Upsert` nếu có sẵn).
- **Resource:** Chọn `Contact`.
- **Mapping Fields:** Đây là bước quan trọng nhất. Các sếp phải ánh xạ (map) các trường dữ liệu từ Pipedrive sang HubSpot:
  - `first_name` (Pipedrive) -> `firstname` (HubSpot)
  - `last_name` (Pipedrive) -> `lastname` (HubSpot)
  - `email` (Pipedrive) -> `email` (HubSpot)
  - `phone` (Pipedrive) -> `phone` (HubSpot)
- **Credentials:** Chọn credential HubSpot.
- *Lưu ý:* Nếu HubSpot yêu cầu `email` là trường bắt buộc, hãy đảm bảo dữ liệu từ Pipedrive luôn có email. Nếu không, workflow có thể lỗi.

#### 3. Kích hoạt ⚡️
1. **Test Run:**
   - Click vào nút **Test Workflow** ở góc trên bên phải.
   - Quan sát dữ liệu đi qua từng node.
   - Kiểm tra xem node `HubSpot2` có báo lỗi không (ví dụ: lỗi duplicate contact nếu không xử lý tốt bước so sánh).
2. **Bật Active:**
   - Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải.
   - Workflow sẽ bắt đầu chạy tự động theo lịch trình Cron đã thiết lập.

### ✍️ Mẹo & gợi ý nâng cao

1. **Thêm thông báo khi có lỗi:**
   - Thêm một node **Slack** hoặc **Telegram** sau node `HubSpot2` (kết nối qua nhánh Error).
   - Khi có lỗi xảy ra (ví dụ: API HubSpot bị rate limit, hoặc dữ liệu thiếu email), các sếp sẽ nhận được thông báo ngay lập tức để xử lý.

2. **Log dữ liệu đã đồng bộ:**
   - Thêm một node **Google Sheets** hoặc **Airtable** để ghi lại lịch sử đồng bộ (Email khách hàng, Thời gian đồng bộ, Trạng thái).
   - Điều này giúp các sếp dễ dàng kiểm tra lại và đối soát khi có vấn đề.

3. **Tối ưu hóa API Calls:**
   - Thay vì lấy `Get All` contacts từ HubSpot mỗi lần chạy (rất tốn tài nguyên), các sếp có thể sử dụng node **HubSpot** với operation `Get` và lọc theo `lastmodified` hoặc sử dụng **Webhook** từ HubSpot (nếu có) để chỉ xử lý khi có thay đổi. Tuy nhiên, với quy mô nhỏ, cách Cron + Get All vẫn chấp nhận được.

4. **Cá nhân hóa dữ liệu:**
   - Trong node `HubSpot2`, các sếp có thể thêm các trường tùy chỉnh (Custom Properties) của HubSpot và ánh xạ từ các trường tương ứng trong Pipedrive (ví dụ: `company_name`, `job_title`).

### 📌 Kết luận

Việc đồng bộ dữ liệu giữa các CRM là một trong những nhu cầu cơ bản nhưng lại gây ra nhiều phiền toái nhất nếu làm thủ công. Với workflow n8n này, các sếp có thể tự động hóa toàn bộ quy trình, đảm bảo dữ liệu khách hàng luôn nhất quán và sẵn sàng cho các chiến dịch Marketing tiếp theo.

Hãy import workflow, cấu hình credentials, và để n8n làm việc thay cho các sếp. Nếu gặp khó khăn trong việc ánh xạ dữ liệu, đừng ngần ngại thử nghiệm với một vài contact mẫu trước khi bật chạy toàn bộ. Chúc các sếp triển khai thành công! 🚀