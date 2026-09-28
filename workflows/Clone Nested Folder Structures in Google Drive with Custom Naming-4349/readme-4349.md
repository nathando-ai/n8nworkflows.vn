---
title: "🚀 Tự Động Clone Cấu Trúc Thư Mục Google Drive Với Tên Tùy Biến"
description: "Giải pháp n8n giúp nhân bản hàng loạt cấu trúc thư mục lồng nhau trên Google Drive, tự động đổi tên theo quy tắc và báo cáo chi tiết, không cần code."
slug: "clone-cuu-truc-thu-muc-google-drive-n8n"
tags: [n8n, google-drive, automation, it-ops, no-code]
keywords: [n8n workflow, google drive api, tự động hóa thư mục, clone folder structure, n8n code node]
---

# 🚀 Tự Động Clone Cấu Trúc Thư Mục Google Drive Với Tên Tùy Biến

Các sếp làm IT Ops hay quản lý dữ liệu chắc hẳn đã từng gặp tình huống "đau đầu" khi cần sao chép một cây thư mục phức tạp (nested folders) từ dự án cũ sang dự án mới, hoặc từ template sang môi trường production. Làm thủ công trên giao diện Google Drive không chỉ tốn thời gian mà còn dễ sai sót khi phải đổi tên hàng chục, hàng trăm thư mục theo quy tắc mới.

Workflow **Clone Nested Folder Structures in Google Drive with Custom Naming** chính là "cứu tinh" cho vấn đề này. Với 7 nodes tối giản nhưng mạnh mẽ, workflow này sẽ quét toàn bộ cấu trúc thư mục gốc, xử lý logic đổi tên, và tự động tạo lại cây thư mục đích hoàn chỉnh trên Google Drive trong vài giây.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, đặc biệt khi cần chạy định kỳ hoặc xử lý lượng dữ liệu lớn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Thay vì click chuột hàng trăm lần, chỉ cần 1 lần bấm "Execute".
- **Chính xác tuyệt đối:** Logic xử lý tên và cấu trúc được mã hóa trong Code Node, tránh lỗi người dùng (human error).
- **Tùy biến linh hoạt:** Dễ dàng thay đổi quy tắc đặt tên (prefix, suffix, replace string) ngay trong cấu hình.
- **Báo cáo minh bạch:** Kết thúc quá trình, workflow sẽ xuất ra báo cáo chi tiết các thư mục đã tạo thành công và các lỗi (nếu có).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Google:** Có quyền truy cập vào thư mục nguồn (Source) và thư mục đích (Destination).
- **Google Drive API Credentials:** Các sếp cần tạo OAuth2 credentials trong n8n hoặc sử dụng API Key (tùy thuộc vào cách cấu hình HTTP Request, nhưng thường với Google Drive API v3, OAuth2 là chuẩn nhất).
- **ID Thư mục:**
  - `SOURCE_FOLDER_ID`: ID của thư mục gốc cần clone.
  - `DESTINATION_FOLDER_ID`: ID của thư mục đích nơi sẽ tạo cấu trúc mới.
- **Quy tắc đặt tên:** Xác định rõ logic đổi tên (ví dụ: thêm prefix `[PROJECT_NAME]_` vào đầu tên mọi thư mục).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from URL** và dán link: `https://n8n.io/workflows/4349` HOẶC copy toàn bộ JSON của workflow và paste vào n8n.
3. Sau khi import, các sếp sẽ thấy 7 nodes được kết nối sẵn.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Đây là phần quan trọng nhất. Workflow sử dụng `HTTP Request` để gọi Google Drive API trực tiếp, do đó các sếp cần cấu hình kỹ các node sau:

**1. Node: `⚙️ CONFIG - Edit the 3 variables above` (Code Node)**
Đây là "trái tim" của cấu hình. Các sếp cần mở node này và chỉnh sửa 3 biến chính trong code:
- `sourceFolderId`: Dán ID của thư mục nguồn.
- `destinationFolderId`: Dán ID của thư mục đích.
- `namingConvention`: Chỉnh sửa hàm hoặc chuỗi để áp dụng quy tắc đổi tên. Ví dụ:
  ```javascript
  // Ví dụ: Thêm prefix "ARCHIVE_" vào đầu tên thư mục
  const newName = "ARCHIVE_" + originalName;
  ```
  *Lưu ý: Các sếp có thể viết logic phức tạp hơn ở đây, như thay thế ký tự đặc biệt, chuyển chữ hoa/thường, v.v.*

**2. Node: `📁 Get All Folders` (HTTP Request)**
- **Authentication:** Chọn credentials Google Drive OAuth2 đã tạo.
- **URL:** Kiểm tra đảm bảo URL trỏ đến endpoint `files` của Google Drive API với tham số `q` lọc đúng `sourceFolderId`.
- **Headers:** Đảm bảo có header `Authorization` (nếu dùng API Key) hoặc để n8n tự xử lý nếu dùng OAuth2.

**3. Node: `🔄 Process Folders` (Code Node)**
- Node này nhận dữ liệu từ bước Get All Folders và xử lý logic đệ quy (recursion) hoặc phẳng (flat) để xác định thứ tự tạo thư mục (phải tạo thư mục cha trước khi tạo con).
- Kiểm tra lại logic xử lý tên ở đây nếu có thay đổi phức tạp so với node CONFIG.

**4. Node: `✨ Create Folder` (HTTP Request)**
- **Authentication:** Cũng dùng credentials Google Drive OAuth2.
- **Body:** Kiểm tra JSON body gửi lên API. Nó cần chứa:
  ```json
  {
    "name": "{{ $json.newName }}",
    "mimeType": "application/vnd.google-apps.folder",
    "parents": ["{{ $json.parentId }}"]
  }
  ```
- **Method:** POST.
- **URL:** `https://www.googleapis.com/drive/v3/files`

**5. Node: `🔀 Should Create?` (IF Node)**
- Kiểm tra điều kiện để đảm bảo chỉ tạo thư mục khi cần thiết (ví dụ: nếu thư mục đích đã tồn tại thì bỏ qua hoặc ghi đè, tùy logic các sếp muốn).

**6. Node: `📊 Final Report` (Code Node)**
- Node này tổng hợp kết quả. Các sếp có thể chỉnh sửa để thêm thông tin vào báo cáo, ví dụ: tổng số thư mục đã tạo, danh sách lỗi, hoặc gửi email thông báo.

#### 3. Kích hoạt ⚡️
1. **Test Run:** Bấm nút **"Test workflow"** (Manual Trigger).
2. Quan sát từng node:
   - `Get All Folders` phải trả về danh sách thư mục con của nguồn.
   - `Process Folders` phải xử lý đúng thứ tự.
   - `Create Folder` phải trả về ID của thư mục mới được tạo.
3. Kiểm tra trực tiếp trên Google Drive xem cấu trúc có đúng không.
4. Nếu ổn, bật **Active** workflow. Các sếp có thể thay Manual Trigger bằng Cron Trigger nếu muốn chạy định kỳ (ví dụ: sao lưu cấu trúc hàng ngày).

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram:** Thêm node `Slack` hoặc `Telegram` sau `Final Report` để gửi thông báo "Đã clone xong X thư mục" vào kênh làm việc.
- **Xử lý Lỗi Chi Tiết:** Trong node `Final Report`, các sếp có thể lọc ra các item có lỗi (status 400/403) và gửi riêng một email cảnh báo cho admin.
- **Clone File kèm theo:** Hiện tại workflow chỉ clone *thư mục*. Nếu cần clone cả file, các sếp có thể thêm logic vào `Process Folders` để gọi API copy file sau khi tạo xong thư mục cha.
- **Log vào Google Sheets:** Thêm node `Google Sheets` để ghi lại lịch sử các lần clone (Thời gian, Người chạy, Số lượng thư mục) vào một sheet riêng để audit.

### 📌 Kết luận
Workflow **Clone Nested Folder Structures in Google Drive** là một công cụ "nhỏ mà có võ" cho các sếp IT Ops. Nó biến một tác vụ lặp đi lặp lại, dễ sai sót thành một quy trình tự động, chính xác và nhanh chóng. Chỉ với vài phút cấu hình ban đầu, các sếp sẽ tiết kiệm được hàng giờ làm việc thủ công mỗi khi cần sao chép cấu trúc dữ liệu. Hãy import ngay và thử nghiệm với một thư mục nhỏ trước khi áp dụng cho dự án lớn nhé!