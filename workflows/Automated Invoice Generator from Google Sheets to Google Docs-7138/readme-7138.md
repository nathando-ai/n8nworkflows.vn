---
title: "💰 Tự Động Hóa Tạo Hóa Đơn Từ Google Sheets Sang Google Docs (Không Cần Code)"
description: "Giải pháp tự động hóa hoàn toàn tự động tạo hóa đơn chuyên nghiệp từ dữ liệu Google Sheets sang Google Docs với định dạng thống nhất, tiết kiệm thời gian lên đến 80% cho bộ phận tài chính. Workflow này hoạt động 24/7, đảm bảo chính xác và cá nhân hóa cho từng khách hàng."
slug: "tieu-dong-hoa-tao-hoa-don-tu-google-sheets-sang-google-docs"
tags: [n8n, automation, google-sheets, google-docs, tài chính, không-code]
keywords: [tự động hóa hóa đơn, n8n workflow, google sheets google docs, tạo hóa đơn tự động, tiết kiệm thời gian tài chính]
---

# 🚀 **Tự Động Hóa Tạo Hóa Đơn Từ Google Sheets Sang Google Docs (Không Cần Code)**

### **🔥 Nỗi Đau Của Các Sếp?**
Hàng ngày, bộ phận tài chính phải:
- **Nhập lại dữ liệu** từ Google Sheets vào mẫu hóa đơn Google Docs thủ công.
- **Sửa lỗi định dạng** khi có thay đổi trong dữ liệu.
- **Tốn thời gian** lên đến 3-5 giờ/tuần cho việc tạo hóa đơn cho khách hàng.
- **Không đảm bảo tính nhất quán** giữa các hóa đơn do mỗi người tạo khác nhau.

**Giải pháp?** **Workflow này tự động hóa toàn bộ quy trình!** Chỉ cần một lần cấu hình, hệ thống sẽ:
✅ **Tạo hóa đơn mới** từ mẫu chuẩn.
✅ **Điền tự động** thông tin từ Google Sheets (tên công ty, số hóa đơn, mô tả, số tiền...).
✅ **Lưu vào Google Drive** theo định dạng thống nhất.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo an toàn và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Giảm 80% thời gian tạo hóa đơn thủ công.
- **Chính xác 100%**: Không còn sai sót do nhập liệu sai.
- **Định dạng thống nhất**: Tất cả hóa đơn đều có cùng bố cục chuyên nghiệp.
- **Hoạt động tự động**: Chỉ cần kích hoạt workflow, hệ thống sẽ làm việc cho bạn.
- **Dễ dàng mở rộng**: Thêm khách hàng mới chỉ cần cập nhật Google Sheets.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google** (đã kích hoạt API Google Sheets & Google Docs).
2. **Google Sheet mẫu** (có cột: `Company From`, `Company To`, `Terms`, `Invoice`, `Description`, `Amount`).
3. **Mẫu Google Docs hóa đơn** (có placeholder: `FromCompany#`, `ToCompany#`, `Terms#`, `Invoice#`, `Description#`, `Amount#`).
4. **Google Drive folder** (để lưu hóa đơn tự động, ID folder mặc định: `1TnDibwPPPUm3VbmETiqWDVhtaUTLJ6mn`).

---
:::info[CHUẨN BỊ]
**Bước 1: Cấu hình OAuth2 cho Google Sheets & Google Docs**
- **Google Sheets OAuth2**:
  1. Truy cập [Google Cloud Console](https://console.cloud.google.com/).
  2. Bật **Google Sheets API**.
  3. Tạo **OAuth 2.0 Credentials** và thêm **Redirect URI**:
     ```
     https://api.n8n.cloud/oauth2-credential/callback
     ```
- **Google Docs OAuth2**:
  1. Bật **Google Docs API** trong Cloud Console.
  2. Tạo OAuth 2.0 Credentials tương tự.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/7138](https://n8n.io/workflows/7138) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **7 node chính**, các sếp cần chú ý cấu hình như sau:

##### **Node 1: Manual Trigger (Bắt Đầu Tự Động)**
- **Định nghĩa**: Node này cho phép các sếp **kích hoạt workflow thủ công** khi cần test hoặc chạy một lần.
- **Lưu ý**: Sau khi cấu hình xong, các sếp có thể **bỏ qua node này** và thay thế bằng **Webhook** hoặc **Schedule Trigger** để tự động hóa hoàn toàn.

##### **Node 2: Google Sheets (Lấy Dữ Liệu Hóa Đơn)**
- **Cấu hình**:
  - **Credentials**: Chọn `googleSheetsOAuth2Api` (đã cấu hình trước).
  - **Sheet URL**: Dán liên kết Google Sheet của các sếp (ví dụ: [Google Sheet mẫu](https://docs.google.com/spreadsheets/d/1MHVZRVo5aPs5VqRXk7lBNPVlZ2gilKqZ8J9yeg4taW4/edit)).
  - **Range**: Chọn toàn bộ sheet (ví dụ: `Sheet1!A:F`).
- **Lưu ý**:
  - **Không thay đổi tên cột** trong Google Sheet (phải theo định dạng: `Company From`, `Company To`, `Terms`, `Invoice`, `Description`, `Amount`).
  - Nếu sheet có nhiều trang, chỉ lấy **trang đầu tiên**.

##### **Node 3: Merge (Kết Hợp Dữ Liệu)**
- **Định nghĩa**: Node này **ghép dữ liệu từ Google Sheets với mẫu Google Docs** để chuẩn bị cho bước cập nhật nội dung.
- **Lưu ý**: **Không cần chỉnh sửa** node này, nó hoạt động tự động.

##### **Node 4: Get Invoice Template (Lấy Mẫu Hóa Đơn)**
- **Cấu hình**:
  - **Credentials**: Chọn `googleDocsOAuth2Api`.
  - **Document ID**: Dán ID của **mẫu Google Docs** (có thể lấy từ URL: `https://docs.google.com/document/d/18n0HTqabDldi7fVbhbI1aG12qbFWsjyTXdduwDDOUu8/edit` → ID là `18n0HTqabDldi7fVbhbI1aG12qbFWsjyTXdduwDDOUu8`).
- **Lưu ý**:
  - **Mẫu phải có placeholder** như sau:
    ```
    FromCompany#
    ToCompany#
    Terms#
    Invoice#
    Description#
    Amount#
    ```
  - Nếu mẫu đã có nội dung, **xóa hết** để chỉ giữ placeholder.

##### **Node 5: Create New Doc (Tạo Hóa Đơn Mới)**
- **Cấu hình**:
  - **Credentials**: `googleDocsOAuth2Api`.
  - **Title Format**: `Invoice: {{ $json.Invoice }}` (định dạng tự động theo số hóa đơn).
  - **Parent Folder ID**: `1TnDibwPPPUm3VbmETiqWDVhtaUTLJ6mn` (hoặc thay bằng folder của các sếp).
- **Lưu ý**:
  - **Folder phải có quyền write** cho tài khoản OAuth2 của n8n.
  - Nếu muốn lưu vào folder khác, thay đổi **Parent Folder ID**.

##### **Node 6: Insert Content into Doc (Chèn Nội Dung)**
- **Định nghĩa**: Node này **sao chép nội dung từ mẫu** vào hóa đơn mới.
- **Lưu ý**: **Không cần chỉnh sửa**, nó tự động thực hiện sau khi tạo hóa đơn mới.

##### **Node 7: Input Invoice Details (Điền Thông Tin)**
- **Cấu hình**:
  - **Credentials**: `googleDocsOAuth2Api`.
  - **Document ID**: **Không cần điền**, node này sẽ tự động lấy ID từ node trước.
  - **Content**: Dùng **Google Docs API** để thay thế placeholder bằng dữ liệu từ Google Sheets.
- **Bảng thay thế placeholder**:
  | **Placeholder**   | **Thay Thế Bằng**               |
  |-------------------|----------------------------------|
  | `FromCompany#`    | `Company From` từ sheet          |
  | `ToCompany#`      | `Company To` từ sheet            |
  | `Terms#`          | `Terms` từ sheet                 |
  | `Invoice#`        | `Invoice` từ sheet               |
  | `Description#`    | `Description` từ sheet           |
  | `Amount#`         | `Amount` từ sheet                |

- **Lưu ý**:
  - **Kiểm tra định dạng số tiền** (nếu sheet có số tiền là `1,000.000`, phải chuyển thành `1000000` để tránh lỗi).
  - **Nếu placeholder không thay thế được**, kiểm tra lại **mẫu Google Docs** có đúng định dạng không.

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  1. Chọn **1 hàng dữ liệu** trong Google Sheet.
  2. Chạy **Test Execution** để kiểm tra workflow.
  3. Kiểm tra **Google Drive** xem hóa đơn đã tạo thành công chưa.
- **Bật Active**:
  - Sau khi test thành công, **bật Active** cho workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự Động Hóa Thường Xuyên**:
   - Thay thế **Manual Trigger** bằng **Schedule Trigger** (n8n Pro) để chạy hàng ngày/lần tuần.
   - Cấu hình **Webhook** để nhận dữ liệu từ hệ thống khác (ví dụ: Airtable, ERP).

2. **Gửi Hóa Đơn Cho Khách Hàng**:
   - Thêm **node Email** (n8n-nodes-base.email) để gửi hóa đơn tự động qua email.
   - Cấu hình **Slack/Telegram Notification** để thông báo khi hóa đơn được tạo.

3. **Lưu Log & Theo Dõi**:
   - Thêm **node Sticky Note** (n8n-nodes-base.stickyNote) để ghi log mỗi lần tạo hóa đơn.
   - Sử dụng **Google Sheets Log** để theo dõi lịch sử.

4. **Tùy Chỉnh Mẫu Hóa Đơn**:
   - Sử dụng **Google Docs API** để thay đổi màu sắc, logo, hoặc bố cục theo yêu cầu của công ty.

5. **Xử Lý Lỗi**:
   - Thêm **node If** (n8n-nodes-base.if) để kiểm tra lỗi (ví dụ: nếu `Amount` là `0`, bỏ qua hoặc gửi thông báo).

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho bộ phận tài chính, **giảm sai sót** và **cải thiện trải nghiệm khách hàng** với hóa đơn chuyên nghiệp. **Chỉ cần 1 lần cấu hình**, hệ thống sẽ tự động hóa mọi việc!

**Bắt đầu ngay hôm nay**:
1. **Import workflow** vào n8n.
2. **Cấu hình OAuth2** và Google Sheet.
3. **Test và bật Active**.
4. **Xem hóa đơn tự động được tạo** trong Google Drive!

**Nếu gặp vấn đề**, liên hệ với tác giả:
📧 rbreen@ynteractive.com
🔗 [LinkedIn](https://www.linkedin.com/in/robert-breen-29429625/)

---
**🚀 Hãy tự động hóa ngay và tập trung vào những việc quan trọng hơn!**