---
title: "📁 Tự động Tải và Tổng hợp File từ Google Drive thành Dạng Key-Value Dictionary trong n8n"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n để quét toàn bộ thư mục Google Drive, tải nội dung file Google Docs và gom chúng thành một từ điển Key-Value gọn gàng."
slug: "tai-va-tong-hop-file-google-drive-thanh-dictionary-trong-n8n"
tags: [n8n, automation, no-code, google-drive, google-docs, data-transformation]
keywords: [n8n workflow, google drive n8n, tong hop file google drive, code node n8n, dictionary key value]
---

# 📁 Tự động Tải và Tổng hợp File từ Google Drive thành Dạng Key-Value Dictionary

Các sếp có bao giờ gặp cảnh phải mò mẫm mở từng file tài liệu trên Google Drive, copy nội dung rồi gom lại để xử lý cho các bước tự động hóa tiếp theo chưa? Công việc thủ công này cực kỳ tốn thời gian, dễ nhầm lẫn và làm gián đoạn chuỗi quy trình làm việc. 

Giải pháp ở đây là gì? Một workflow n8n tự động hoàn toàn giúp quét sạch thư mục, bốc toàn bộ nội dung tài liệu và nhào nặn chúng thành một cấu trúc **Key-Value Dictionary** (với Key là tên file, Value là nội dung file) cực kỳ gọn gàng, sẵn sàng để cung cấp cho các AI Agent hoặc các bước xử lý dữ liệu tiếp theo!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Không cần thao tác thủ công mở từng file trên Google Drive nữa.
- **Cấu trúc dữ liệu tối ưu:** Gom toàn bộ file thành định dạng `Key: Value` (Tên file: Nội dung) giúp dễ dàng tra cứu và truyền dữ liệu cho các node phía sau (như OpenAI, Claude...).
- **Modular hóa:** Được thiết kế dạng Sub-workflow (`Execute Workflow Trigger`), có thể dễ dàng gọi từ bất kỳ quy trình chính nào khi cần nạp dữ liệu tài liệu.
- **Linh hoạt mở rộng:** Dễ dàng tinh chỉnh để xử lý các định dạng file khác ngoài Google Docs nếu cần.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance **n8n** đang hoạt động.
- Tài khoản **Google Account** đã kết nối với n8n (Google Drive OAuth2 API và Google Docs OAuth2 API).
- Một thư mục trên Google Drive chứa các tài liệu cần tổng hợp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ mã JSON của workflow (hoặc tải từ nguồn cung cấp) và dán trực tiếp vào n8n Editor.

Danh sách các node trong workflow này bao gồm:
- **When Executed by Another Workflow** (`executeWorkflowTrigger`): Điểm khởi đầu, nhận tín hiệu gọi từ workflow chính.
- **Get files from folder** (`googleDrive`): Quét và lấy danh sách các file nằm trong thư mục chỉ định.
- **Download Google Docs** (`googleDocs`): Tải nội dung chi tiết của từng file Google Docs.
- **Code** (`code`): Xử lý lập trình Javascript để gom nhóm dữ liệu.
- **Mapping** (`set`): Chuẩn hóa dữ liệu đầu ra thành dạng từ điển hoàn chỉnh.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà không lỗi, các sếp cần chú ý cấu hình các điểm sau:

- **Node `Get files from folder` (Google Drive):**
  - Kết nối tài khoản Google Drive Credentials của các sếp.
  - Chọn đúng **Folder ID** của thư mục trên Google Drive mà các sếp muốn quét tài liệu. *(Xem hướng dẫn Step 1 trên canvas)*.
- **Node `Download Google Docs` (Google Docs):**
  - Kết nối Google Docs Credentials.
  - Node này mặc định xử lý file Google Docs. Nếu các sếp muốn mở rộng sang các định dạng khác (như PDF, Word...), hãy đổi node này thành node tương ứng phù hợp *(Xem hướng dẫn Step 2 trên canvas)*.
- **Node `Code` & `Mapping`:**
  - Phần này đã được tác giả cấu hình sẵn logic Javascript để ánh xạ dữ liệu. Node **Mapping** sẽ xuất ra một dictionary chuẩn xác với `Key` là tên file và `Value` là nội dung file bên trong.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** với một dữ liệu test từ workflow gọi để kiểm tra xem danh sách file đã được load và map thành công chưa.
- Sau khi test ngon lành, hãy bật nút **Active** ở góc trên bên phải để đưa workflow vào trạng thái sẵn sàng chiến đấu 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp AI (OpenAI / LangChain):** Đưa toàn bộ Key-Value Dictionary này vào các LLM để phân tích tổng hợp, tóm tắt toàn bộ tài liệu trong thư mục chỉ với 1 cú click.
- **Gửi thông báo qua Telegram/Slack:** Thêm bước gửi thông báo về Slack/Telegram mỗi khi sub-workflow này hoàn tất việc quét và nạp dữ liệu.
- **Lưu log vào Google Sheets:** Ghi lại lịch sử mỗi lần workflow được kích hoạt và số lượng file đã tổng hợp thành công.

### 📌 Kết luận
Workflow này là một "building block" cực kỳ mạnh mẽ và gọn gàng giúp giải quyết bài toán gom tài liệu hàng loạt từ Google Drive. Hãy áp dụng ngay vào hệ thống n8n của các sếp để tối ưu hóa quy trình xử lý tài liệu ngay hôm nay!