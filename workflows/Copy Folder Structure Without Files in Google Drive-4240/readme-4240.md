---
title: "📂 Tự Động Sao Chép Cấu Trúc Thư Mục Google Drive (Không File) với n8n"
description: "Giải pháp tự động hóa 100% để nhân bản cây thư mục phức tạp từ Google Drive nguồn sang đích, loại bỏ hoàn toàn thao tác copy-paste thủ công và lỗi sai."
slug: "tu-dong-sao-kep-cau-truc-thu-muc-google-drive"
tags: [n8n, google-drive, automation, it-ops, no-code]
keywords: [n8n workflow, sao chép thư mục google drive, tự động hóa google drive, n8n google drive, copy folder structure]
---

# 📂 Tự Động Sao Chép Cấu Trúc Thư Mục Google Drive (Không File) với n8n

Các sếp có bao giờ phải đối mặt với tình huống cần thiết lập lại một hệ thống thư mục phức tạp trên Google Drive cho một dự án mới, một khách hàng mới, hoặc đơn giản là backup cấu trúc dữ liệu? Việc copy-paste thủ công từng thư mục con, thư mục cha không chỉ tốn thời gian mà còn dễ dẫn đến sai sót (quên thư mục, đặt sai tên, hoặc nhầm lẫn đường dẫn).

Workflow **"Copy Folder Structure Without Files in Google Drive"** do *Builds.Cool* phát triển chính là giải pháp "chữa cháy" hoàn hảo. Nó cho phép các sếp quét toàn bộ cây thư mục từ một Drive nguồn và tự động tái tạo y hệt cấu trúc đó trên một Drive đích, **chỉ bao gồm các thư mục (folders)**, không sao chép bất kỳ file nào. Quy trình này diễn ra hoàn toàn tự động, chính xác và nhanh chóng, giúp tiết kiệm hàng giờ làm việc thủ công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, đặc biệt khi cần chạy định kỳ hoặc xử lý lượng lớn thư mục, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối:** Thay vì mất hàng giờ click chuột, cấu trúc hàng trăm thư mục được nhân bản trong vài phút.
- **Độ chính xác 100%:** Loại bỏ hoàn toàn lỗi con người như quên thư mục, đặt sai tên hoặc nhầm lẫn đường dẫn.
- **Tinh gọn dữ liệu:** Chỉ sao chép "xương sống" (cấu trúc thư mục), không tải file, giúp quá trình chạy nhanh và không tốn dung lượng lưu trữ tạm thời.
- **Tái sử dụng linh hoạt:** Dễ dàng áp dụng cho nhiều dự án khác nhau chỉ bằng cách thay đổi ID thư mục nguồn và đích.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Google Drive:** Đã kết nối với n8n (Credentials).
- **ID Thư mục Nguồn (Source Folder ID):** ID của thư mục gốc trên Drive mà các sếp muốn sao chép cấu trúc.
- **ID Thư mục Đích (Destination Folder ID):** ID của thư mục gốc trên Drive nơi các sếp muốn tạo lại cấu trúc.
- **Quyền truy cập:** Tài khoản Google kết nối với n8n phải có quyền **Read** trên thư mục nguồn và quyền **Create/Write** trên thư mục đích.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from URL** hoặc **Import from File**.
3. Dán link workflow gốc: `https://n8n.io/workflows/4240` hoặc tải file JSON về và import.
4. Workflow sẽ hiển thị với các node đã được nối sẵn.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Đây là phần quan trọng nhất. Các sếp cần cấu hình kỹ các node sau để workflow hoạt động đúng ý đồ:

*   **Node: `EDIT_THIS_NODE` (Loại: Set)**
    *   Đây là node "chìa khóa". Các sếp cần vào node này và thay đổi giá trị trong trường `value`.
    *   **Source Folder ID:** Dán ID của thư mục nguồn (các sếp có thể lấy ID từ URL của Google Drive, phần sau `/folders/`).
    *   **Destination Folder ID:** Dán ID của thư mục đích.
    *   *Lưu ý:* Nếu các sếp muốn thay đổi tên thư mục đích (ví dụ: thêm prefix "Backup_"), hãy kiểm tra logic trong node này hoặc node `Set Destination Names`.

*   **Node: `Get_Folders_SOURCE` (Loại: Google Drive)**
    *   Đảm bảo **Credentials** đã được chọn đúng tài khoản Google có quyền đọc thư mục nguồn.
    *   Kiểm tra tham số `Folder ID` (nếu có) hoặc đảm bảo nó nhận dữ liệu từ node `EDIT_THIS_NODE`.

*   **Node: `Get_Folders_DESTINATION` (Loại: Google Drive)**
    *   Chọn **Credentials** của tài khoản Google có quyền ghi vào thư mục đích.
    *   Node này thường dùng để kiểm tra xem thư mục con đã tồn tại chưa, tránh tạo trùng lặp.

*   **Node: `Create Folder` (Loại: Google Drive)**
    *   Kiểm tra tham số `Name` và `Parent ID`.
    *   `Parent ID` cần được ánh xạ đúng để đảm bảo thư mục con được tạo trong đúng thư mục cha tương ứng trên Drive đích.

*   **Node: `Check if folder exists` (Loại: Code)**
    *   Node này chứa logic JavaScript để so sánh danh sách thư mục nguồn và đích. Các sếp không cần sửa code nếu không muốn thay đổi logic kiểm tra trùng lặp, nhưng nên đọc qua để hiểu luồng xử lý.

*   **Node: `If exists` (Loại: If)**
    *   Node này quyết định luồng: Nếu thư mục đã tồn tại ở đích, nó sẽ bỏ qua; nếu chưa, nó sẽ tạo mới. Đảm bảo điều kiện (Condition) được cấu hình đúng theo output của node Code.

#### 3. Kích hoạt ⚡️
1. **Test Run:** Nhấn nút **Test workflow**.
   *   Quan sát luồng dữ liệu: Nó sẽ lấy danh sách thư mục nguồn, so sánh với đích, và chỉ tạo những thư mục còn thiếu.
   *   Kiểm tra kết quả trên Google Drive đích để đảm bảo cấu trúc đã được tạo đúng.
2. **Active Workflow:** Nếu các sếp muốn chạy định kỳ (ví dụ: mỗi ngày kiểm tra và đồng bộ cấu trúc), hãy bật công tắc **Active**. Nếu chỉ chạy một lần, có thể giữ ở chế độ Manual.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm thông báo qua Slack/Telegram:** Kết nối thêm node `Slack` hoặc `Telegram` sau node `Create Folder` (hoặc cuối workflow) để gửi thông báo "Đã hoàn tất sao chép X thư mục" cho các sếp.
- **Lưu log vào Google Sheets:** Thêm node `Google Sheets` để ghi lại lịch sử các thư mục đã được tạo, thời gian tạo, và trạng thái. Điều này hữu ích cho việc audit và kiểm soát.
- **Xử lý lỗi (Error Handling):** Thêm node `Error Trigger` hoặc cấu hình `On Error` cho các node Google Drive để xử lý trường hợp mất kết nối hoặc hết quota API, tránh workflow dừng đột ngột giữa chừng.
- **Tự động hóa theo sự kiện:** Thay vì chạy thủ công, các sếp có thể kết hợp với `Cron` (định kỳ) hoặc `Webhook` (khi có yêu cầu từ hệ thống khác) để tự động đồng bộ cấu trúc thư mục khi cần.

### 📌 Kết luận
Workflow **"Copy Folder Structure Without Files in Google Drive"** là một công cụ IT Ops cực kỳ hữu ích cho các đội ngũ vận hành, quản trị viên hệ thống, hoặc bất kỳ ai làm việc nhiều với Google Drive. Nó biến một tác vụ nhàm chán, dễ sai sót thành một quy trình tự động, chính xác và nhanh chóng. Các sếp hãy thử áp dụng ngay để trải nghiệm sự khác biệt mà tự động hóa mang lại!