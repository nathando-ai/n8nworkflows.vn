---
title: "📊 Tự Động Báo Cáo Chi Phí Dự Án Hàng Tuần: MySQL + Outlook HTML"
description: "Workflow n8n tự động truy vấn dữ liệu chi phí từ MySQL, xử lý logic và gửi email báo cáo HTML chuyên nghiệp qua Microsoft Outlook mỗi tuần. Giải pháp hoàn hảo cho đội ngũ Finance & IT Ops."
slug: "tu-dong-bao-cao-chi-phi-du-an-mysql-outlook"
tags: [n8n, automation, mysql, microsoft-outlook, finance-automation]
keywords: [n8n workflow, báo cáo chi phí, tự động hóa tài chính, mysql to email, outlook html email]
---

# 📊 Tự Động Báo Cáo Chi Phí Dự Án Hàng Tuần: MySQL + Outlook HTML

Trong môi trường doanh nghiệp, việc tổng hợp chi phí dự án thường là một gánh nặng nặng nề cho đội ngũ Finance hoặc IT Ops. Mỗi tuần, các sếp phải mất hàng giờ để chạy query trên database, copy dữ liệu vào Excel, định dạng lại và soạn email gửi cho ban giám đốc. Không chỉ tốn thời gian, quy trình thủ công này còn tiềm ẩn rủi ro sai sót con người (human error) và thiếu tính nhất quán trong cách trình bày.

Workflow **"Automated Weekly Project Cost Reports"** được thiết kế để giải quyết triệt để vấn đề này. Nó hoạt động như một "nhân viên tài chính ảo", tự động thức dậy vào khung giờ cố định, truy vấn dữ liệu chi tiết từ MySQL, xử lý logic phân loại dự án và gửi đi những email báo cáo HTML đẹp mắt, chuyên nghiệp qua Microsoft Outlook. Toàn bộ quy trình diễn ra 100% tự động, không cần một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 5-10 giờ/tuần**: Loại bỏ hoàn toàn công đoạn copy-paste và định dạng báo cáo thủ công.
- **Độ chính xác tuyệt đối**: Dữ liệu được lấy trực tiếp từ nguồn (MySQL), loại bỏ sai sót do nhập liệu tay.
- **Chuyên nghiệp hóa hình ảnh**: Email được gửi dưới dạng HTML có định dạng sẵn, thể hiện sự chỉn chu của doanh nghiệp.
- **Hoạt động liên tục**: Báo cáo được gửi đúng giờ, đúng ngày, bất kể cuối tuần hay ngày lễ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n**: Đã cài đặt và chạy n8n (Self-hosted hoặc Cloud).
- **CSDL MySQL**: Một database đang hoạt động chứa bảng dữ liệu chi phí dự án (Project Cost Table). Các sếp cần có thông tin Host, Port, User, Password và Database Name.
- **Tài khoản Microsoft Outlook**: Đã cấu hình OAuth2 hoặc App Password trong n8n để gửi email.
- **Dữ liệu mẫu**: Đảm bảo bảng MySQL có các trường dữ liệu cần thiết như: `Project Name`, `Cost`, `Date`, `Category` (hoặc các trường tương tự tùy cấu trúc DB của bạn).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from URL** hoặc **Import from File** (nếu bạn đã tải file JSON từ link gốc).
3. Hoặc copy toàn bộ code JSON của workflow và dán vào **Edit Mode**.
4. Lưu workflow với tên dễ nhớ, ví dụ: `Weekly Project Cost Report`.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 6 nodes chính, các sếp cần cấu hình kỹ từng phần sau:

**1. Node `Schedule Trigger`**
- Đây là "trái tim" khởi động workflow.
- **Cấu hình**: Chọn tần suất chạy (ví dụ: Hàng tuần vào Thứ Hai lúc 08:00 AM).
- **Lưu ý**: Đảm bảo múi giờ (Timezone) trong n8n khớp với múi giờ doanh nghiệp của bạn để báo cáo gửi đi đúng giờ.

**2. Node `MySQL`**
- **Operation**: Chọn `Execute Query`.
- **Query**: Đây là phần quan trọng nhất. Các sếp cần thay câu lệnh SQL mẫu bằng câu lệnh truy vấn thực tế của mình.
  - *Ví dụ*: `SELECT project_name, SUM(cost) as total_cost, date FROM project_costs WHERE date >= DATE_SUB(CURDATE(), INTERVAL 7 DAY) GROUP BY project_name;`
- **Credentials**: Chọn hoặc tạo mới credential MySQL. Điền đầy đủ Host, User, Password, Database.
- **Lưu ý**: Nếu bảng dữ liệu của bạn có tên khác, hãy cập nhật tên bảng trong câu lệnh SQL.

**3. Node `Switch`**
- Node này dùng để phân luồng dữ liệu dựa trên điều kiện (ví dụ: phân loại dự án theo trạng thái hoặc mức độ chi phí).
- **Cấu hình Rules**: Các sếp cần chỉnh sửa các rule để khớp với logic kinh doanh.
  - *Ví dụ*: Nếu `total_cost > 1000` thì đi nhánh A, nếu `total_cost <= 1000` đi nhánh B.
  - Hoặc phân loại theo `Project Status` (Active, Completed, On Hold).
- **Lưu ý**: Kiểm tra kỹ các giá trị so sánh (Value) để đảm bảo dữ liệu từ MySQL khớp với điều kiện ở đây.

**4. Nodes `Microsoft Outlook1`, `Microsoft Outlook6`, `Microsoft Outlook7`**
- Workflow có 3 nodes Outlook, thường dùng để gửi email cho các nhóm đối tượng khác nhau hoặc gửi các phần nội dung khác nhau (ví dụ: Email tổng quan, Email chi tiết, Email cảnh báo).
- **To (Email người nhận)**: Điền địa chỉ email của người nhận (Ban giám đốc, Trưởng phòng, v.v.).
- **Subject**: Chỉnh sửa tiêu đề email cho phù hợp, ví dụ: `📊 Báo cáo chi phí dự án tuần {{ $now.format('dd/MM/yyyy') }}`.
- **HTML Body**: Đây là phần hiển thị nội dung email.
  - Các sếp cần chỉnh sửa template HTML để hiển thị đúng các trường dữ liệu từ MySQL (dùng cú pháp `{{ $json.project_name }}`, `{{ $json.total_cost }}`).
  - Có thể chèn thêm CSS inline để làm đẹp bảng biểu, màu sắc, logo công ty.
- **Credentials**: Chọn credential Microsoft Outlook đã tạo sẵn.

:::note[LƯU Ý QUAN TRỌNG VỀ HTML EMAIL]
Email HTML trong Outlook có thể bị render khác nhau trên các client (Gmail, Outlook Web, Outlook Desktop). Các sếp nên test kỹ bằng cách gửi email cho chính mình trước khi bật Active. Nếu gặp lỗi hiển thị, hãy sử dụng các bảng HTML đơn giản (table-based layout) thay vì CSS phức tạp.
:::

#### 3. Kích hoạt ⚡️
1. **Test Run**: Nhấn nút **Execute Workflow** để chạy thử với dữ liệu hiện tại.
2. **Kiểm tra Email**: Mở hộp thư Outlook để xem email đã được gửi chưa, nội dung HTML có hiển thị đúng không.
3. **Kiểm tra Logic**: Đảm bảo dữ liệu từ MySQL được phân loại đúng qua node Switch.
4. **Bật Active**: Khi mọi thứ ổn, bật công tắc **Active** ở góc trên bên phải. Workflow sẽ tự động chạy theo lịch đã đặt.

### ✍️ Mẹo & gợi ý nâng cao
- **Gửi kèm File PDF**: Thay vì chỉ gửi HTML, các sếp có thể thêm node `Convert to PDF` (nếu có) hoặc dùng dịch vụ bên ngoài để render HTML thành PDF và đính kèm vào email.
- **Tích hợp Slack/Telegram**: Sau khi gửi email, thêm node `Slack` hoặc `Telegram` để gửi thông báo ngắn gọn "Báo cáo chi phí tuần đã được gửi" vào kênh làm việc chung.
- **Lưu Log Báo Cáo**: Thêm node `Google Sheets` hoặc `MySQL` (INSERT) để lưu lại lịch sử các báo cáo đã gửi, giúp truy vết khi cần.
- **Cảnh Báo Chi Phí Vượt Ngưỡng**: Thêm logic trong node Switch để nếu tổng chi phí vượt quá ngân sách dự kiến, gửi email riêng với tiêu đề "⚠️ CẢNH BÁO" và màu đỏ nổi bật.

### 📌 Kết luận
Việc tự động hóa báo cáo chi phí không chỉ giúp tiết kiệm thời gian mà còn nâng cao độ tin cậy của dữ liệu tài chính. Với workflow này, các sếp có thể tập trung vào việc phân tích và ra quyết định thay vì loay hoay với các thao tác thủ công lặp đi lặp lại. Hãy import, cấu hình và để n8n làm việc thay bạn ngay hôm nay!