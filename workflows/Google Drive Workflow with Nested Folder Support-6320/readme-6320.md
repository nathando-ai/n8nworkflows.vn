---
title: "🚀 Tự động hóa quản lý Google Drive với hỗ trợ thư mục lồng nhau trong n8n"
description: "Hướng dẫn xây dựng workflow n8n giúp xử lý và quản lý tệp tin, thư mục trên Google Drive tự động, hỗ trợ quét sâu các thư mục con lồng nhau một cách mượt mà."
slug: "google-drive-workflow-nested-folder-support-n8n"
tags: [n8n, automation, google-drive, file-management, no-code, workflow]
keywords: [n8n workflow, google drive automation, quản lý thư mục google drive, n8n google drive nested folder]
---

# 🚀 Tự động hóa quản lý Google Drive với hỗ trợ thư mục lồng nhau

Việc quản lý hàng ngàn tệp tin và cấu trúc thư mục lồng nhau (nested folders) thủ công trên Google Drive luôn là nỗi ác mộng đối với các doanh nghiệp, đội ngũ vận hành hay quản trị viên dữ liệu. Việc lục lọi từng thư mục con để tìm kiếm hoặc xử lý file vừa mất thời gian vừa dễ xảy ra sai sót. 

Được thiết kế bởi chuyên gia phần mềm Zain Ali, workflow n8n này sẽ giải quyết triệt để bài toán trên bằng cách tự động hóa hoàn toàn quy trình quét, duyệt và trích xuất thông tin tệp tin từ thư mục gốc cho đến tận các thư mục con sâu bên trong mà không cần viết một dòng code phức tạp nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Quét sạch toàn bộ cấu trúc cây thư mục (folder tree) và tệp tin trên Google Drive mà không cần thao tác thủ công.
- **Xử lý thư mục lồng nhau thông minh:** Sử dụng kỹ thuật Sub-workflow kết hợp vòng lặp để xử lý mượt mà các tầng thư mục con sâu vô tận.
- **Tiết kiệm thời gian tối đa:** Thay vì mất hàng giờ đồng hồ kiểm tra từng thư mục, hệ thống xử lý chỉ trong vài giây.
- **Hoạt động 24/7:** Chạy ngầm liên tục trên hạ tầng tự túc, sẵn sàng kết nối với bất kỳ hệ thống báo cáo nào khác.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một tài khoản n8n (Cloud hoặc Self-hosted).
- Tài khoản Google có quyền truy cập Google Drive API (đã tạo Credentials kết nối Google Drive trong n8n).
- Hiểu cơ bản về cấu trúc Sub-workflow trong n8n (vì workflow này sử dụng mô hình gọi workflow con để duyệt thư mục lồng nhau).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ nguồn cấp (ID: 6320) hoặc copy toàn bộ mã nguồn JSON dán trực tiếp vào n8n Editor của mình. Workflow này bao gồm tổng cộng 11 nodes phối hợp nhịp nhàng với nhau.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Khi đưa workflow vào vận hành thực tế, các sếp cần chú ý cấu hình kỹ các node trọng điểm sau:
- **Google Drive Nodes (`Get children folders from folder id` & `Get all files inside a folder`):** Bắt buộc phải kết nối với tài khoản Google Drive (Google Drive OAuth2 API credentials) của các sếp. Đảm bảo tài khoản này có quyền đọc thư mục mục tiêu.
- **Code Node (`Get all folder ids`):** Node này dùng để xử lý mảng dữ liệu trả về từ Google Drive, lọc và gom nhóm các ID thư mục con. Có thể tinh chỉnh đoạn code JS bên trong nếu muốn thay đổi logic lọc tên thư mục.
- **Sub-workflow Nodes (`Start sub-execution` & `Return parent folder id to sub-workflow`):** Đảm bảo cấu hình đúng đường dẫn gọi đến sub-workflow chuyên trách việc quét file bên trong từng thư mục con.
- **Logic Nodes (`If parent folder has no folder`, `If parent folder has nested folders or not`):** Kiểm tra xem thư mục hiện tại có còn thư mục con nào nữa không để quyết định tiếp tục vòng lặp (`Loop Over folder ids` - `splitInBatches`) hay dừng lại.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** với dữ liệu mẫu để kiểm tra xem hệ thống có bóc tách chính xác các ID thư mục và file hay không.
- Sau khi test thành công, chuyển công tắc sang **Active** để workflow chính thức tự động hóa 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối thông báo:** Mở rộng workflow bằng cách gắn thêm node Telegram hoặc Slack ở cuối luồng để nhận thông báo ngay lập tức khi hoàn tất việc quét thư mục.
- **Lưu trữ dữ liệu:** Đưa toàn bộ danh sách file và đường dẫn thư mục vào Google Sheets hoặc cơ sở dữ liệu (PostgreSQL/Supabase) để dễ dàng tra cứu về sau.
- **Chạy định kỳ:** Kết hợp thêm node Schedule Trigger để tự động quét Google Drive hàng ngày hoặc hàng tuần, giúp cập nhật trạng thái tài liệu mới liên tục.

### 📌 Kết luận
Workflow Google Drive với hỗ trợ thư mục lồng nhau là một "vũ khí" cực kỳ lợi hại giúp tối ưu hóa việc quản lý tài liệu số cho cá nhân và doanh nghiệp. Hãy áp dụng ngay hôm nay để giải phóng sức lao động khỏi những công việc lặp đi lặp lại nhàm chán!