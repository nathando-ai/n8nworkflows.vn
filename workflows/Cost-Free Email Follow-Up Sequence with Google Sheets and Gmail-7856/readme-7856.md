---
title: "🚀 **Hệ Thống Tự Động Gửi Email Follow-Up Miễn Phí với Google Sheets & Gmail (Không Cần Code!)**"
description: "Tự động hóa chuỗi email follow-up cho doanh nghiệp, tiết kiệm thời gian lên đến 80% so với làm thủ công. Workflow này lấy dữ liệu từ Google Sheets, gửi email cá nhân hóa qua Gmail, và tự động cập nhật trạng thái - hoàn toàn miễn phí và không cần viết code."
slug: "tu-dong-hoa-email-follow-up-google-sheets-gmail"
tags: [n8n, automation, lead-nurturing, gmail, google-sheets, no-code, email-marketing]
keywords: [tự động hóa email, n8n workflow, follow-up tự động, google sheets gmail, tự động hóa bán hàng, email marketing no-code]
---

# 🚀 **Tự Động Hóa Chuỗi Email Follow-Up Miễn Phí: Từ Google Sheets → Gmail (Không Cần Code!)**

### **💡 Nỗi Đau Của Các Sếp: Làm Thế Nào Để Gửi Email Follow-Up Cho Khách Hàng Mà Không Mất Thời Gian?**
Hàng ngày, các sếp phải:
- **Tìm kiếm** danh sách khách hàng tiềm năng trong Google Sheets.
- **Tạo email** cá nhân hóa cho từng lead (hoặc copy/paste template).
- **Gửi email** qua Gmail một cách thủ công.
- **Cập nhật trạng thái** sau mỗi lần gửi (đã gửi, đã phản hồi, đã bỏ qua...).

Kết quả? **Thời gian bị "chôn vùi" trong công việc lặp lại**, hiệu quả thấp, và dễ quên gửi email cho khách hàng quan trọng.

**Giải pháp?** Workflow này **tự động hóa toàn bộ quy trình** chỉ với **Google Sheets + Gmail** – **không cần viết một dòng code nào!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Tự động gửi **hàng trăm email/ngày** mà không cần can thiệp.
✅ **Cá nhân hóa cao**: Email được động dựa trên dữ liệu trong Google Sheets.
✅ **Không quên gửi**: Workflow chạy **liên tục**, không phụ thuộc vào người dùng.
✅ **Cập nhật tự động**: Trạng thái của từng lead được **update ngay** sau khi gửi.
✅ **Miễn phí**: Sử dụng **Google Sheets + Gmail miễn phí** (không cần API trả phí).
✅ **Dễ dàng mở rộng**: Thêm **Slack/Telegram báo cáo**, **AI viết email tự động**, hoặc **gửi nhiều lần theo lịch**.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Google** (để sử dụng **Google Sheets** và **Gmail**).
✔ **File Google Sheets** chứa danh sách khách hàng với các cột:
   - `Email` (địa chỉ email của lead).
   - `Name` (tên lead, dùng để cá nhân hóa email).
   - `Status` (trạng thái hiện tại: `New`, `Sent`, `Completed`, `Bounced`).
   - `Last Follow-Up` (ngày tháng cuối cùng gửi email).
✔ **Template email** (có thể là **Google Doc** hoặc văn bản trong Sheets).
✔ **API Key của Gmail** (nếu sử dụng **Gmail API**, nhưng workflow này **không bắt buộc** vì có thể dùng **OAuth 2.0** thông thường).

---
:::note[LƯU Ý QUAN TRỌNG]
- Workflow **không sử dụng API trả phí**, chỉ cần **tài khoản Gmail miễn phí**.
- Nếu **Google Sheets** hoặc **Gmail** bị giới hạn, các sếp có thể **mở rộng quy mô** bằng cách **self-host n8n** trên VPS.
:::

---

## 🚀 **Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/7856](https://n8n.io/workflows/7856) (ấn **Export**).
2. **Mở n8n Editor** (trên web hoặc self-hosted).
3. Nhấn **Import** → Chọn file JSON vừa tải → **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ mã JSON** từ [n8n.io/workflows/7856](https://n8n.io/workflows/7856).
2. Trong **n8n Editor**, nhấn **Import** → Chọn **Paste JSON** → Dán và **Import**.

---
### **2. Các Bước Cấu Hình BẮT BUỘC**

#### **🔹 Node 1: Schedule Trigger (Khởi động tự động)**
- **Cấu hình**:
  - **Frequency**: Chọn **Daily** (gửi hàng ngày) hoặc **Custom** (ví dụ: 9h sáng).
  - **Timezone**: Đặt theo giờ của doanh nghiệp (ví dụ: `Asia/Ho_Chi_Minh`).
- **Lưu ý**: Workflow sẽ chạy **tự động** theo lịch đã đặt.

#### **🔹 Node 2: Get Contacts (Lấy dữ liệu từ Google Sheets)**
- **Cấu hình**:
  - **Credentials**: Chọn **Google Sheets OAuth 2.0**.
  - **Sheet Name**: Đặt tên file Google Sheets chứa danh sách lead.
  - **Range**: Chọn **Sheet1!A:Z** (hoặc chỉ các cột cần thiết như `Email`, `Name`, `Status`).
  - **Filter**: **Không cần thiết** (workflow sẽ lọc sau).
- **Lưu ý**:
  - Đảm bảo **Google Sheets** có **cột `Status`** để workflow biết **đã gửi email chưa**.
  - Nếu Sheets có **dữ liệu cũ**, workflow sẽ **bỏ qua** và chỉ xử lý **lead mới**.

#### **🔹 Node 3: Filter (Lọc chỉ lead chưa xử lý)**
- **Cấu hình**:
  - **Condition**: `{{ $json["Status"] }} === "New"` (chỉ lấy lead có `Status = New`).
  - **Pass if condition is met**: **True**.
- **Lưu ý**:
  - Workflow **bỏ qua** lead đã gửi email (`Status = Sent` hoặc `Completed`).
  - Nếu muốn **gửi lại email** cho lead đã bỏ qua, chỉnh sửa điều kiện thành `{{ $json["Status"] }} !== "Completed"`.

#### **🔹 Node 4: email template selector (Chọn template email)**
- **Cấu hình**:
  - **Credentials**: Chọn **Google Docs OAuth 2.0**.
  - **Document ID**: **Tìm ID của Google Doc** chứa template email (có thể là **HTML** hoặc **văn bản**).
    - **Cách lấy ID**:
      1. Mở Google Doc template.
      2. URL sẽ có dạng: `https://docs.google.com/document/d/[ID_DOCUMENT]/edit`.
      3. **Copy ID** (phần giữa `/d/` và `/edit`).
  - **Range**: Chọn **Body** (nếu là văn bản) hoặc **HTML** (nếu là HTML).
- **Lưu ý**:
  - Template có thể chứa **tham số động** như `{{ $json["Name"] }}` để cá nhân hóa.
  - Ví dụ template:
    ```html
    <p>Chào <strong>{{ $json["Name"] }}</strong>,</p>
    <p>Tôi là [Tên bạn], và tôi thấy bạn quan tâm đến [sản phẩm/dịch vụ].</p>
    <p>Đây là email thứ 1 trong chuỗi follow-up của chúng tôi.</p>
    ```

#### **🔹 Node 5: HTML (Định dạng email)**
- **Cấu hình**:
  - **Input**: Chọn **Output từ node `email template selector`**.
  - **Format**: Chọn **HTML** (nếu template là HTML) hoặc **Plain Text** (nếu là văn bản).
- **Lưu ý**:
  - Nếu template là **văn bản**, node này sẽ **định dạng** thành HTML cơ bản.
  - Nếu template đã là **HTML**, node này **không cần thiết** (có thể bỏ qua).

#### **🔹 Node 6: Send a message (Gửi email qua Gmail)**
- **Cấu hình**:
  - **Credentials**: Chọn **Gmail OAuth 2.0**.
  - **To**: `{{ $json["Email"] }}` (địa chỉ email của lead).
  - **Subject**: `Follow-Up #1: [Tên sản phẩm]` (có thể động như `Follow-Up #{{ $json["EmailSequence"] }}`).
  - **Body**: Chọn **HTML** (nếu đã định dạng) hoặc **Plain Text**.
  - **Reply-To**: Đặt là email của bạn (ví dụ: `tiengian@gmail.com`).
- **Lưu ý**:
  - **Không sử dụng Gmail API** (workflow này **không cần**).
  - Nếu **Gmail bị giới hạn**, các sếp có thể **mở rộng quy mô** bằng cách **self-host n8n** trên VPS.

#### **🔹 Node 7: updatecontacts (Cập nhật trạng thái trong Google Sheets)**
- **Cấu hình**:
  - **Credentials**: Chọn **Google Sheets OAuth 2.0**.
  - **Sheet Name**: Đặt tên file Google Sheets.
  - **Range**: Chọn **Sheet1!A:Z** (hoặc chỉ các cột cần update).
  - **Update Values**:
    - `Status`: `{{ $json["Status"] }}` → Đặt thành `"Sent"` (hoặc `"Completed"` nếu là email cuối cùng).
    - `Last Follow-Up`: `{{ $json["Date"] }}` (ngày tháng hiện tại).
- **Lưu ý**:
  - Workflow sẽ **update trạng thái** của lead sau khi gửi email thành công.
  - Nếu email **bị phản hồi**, các sếp có thể **thêm node Slack/Telegram** để báo cáo.

#### **🔹 Node 8: Limits the number of emails per run (Giới hạn số email/giờ)**
- **Cấu hình**:
  - **Limit**: Đặt số lượng email **mỗi lần chạy** (ví dụ: **50 email/ngày**).
  - **Reason**: `To avoid Gmail rate limits`.
- **Lưu ý**:
  - Gmail có **giới hạn gửi email** (~500 email/ngày với tài khoản miễn phí).
  - Nếu gửi quá nhiều, **Gmail có thể khóa tài khoản**.

#### **🔹 Node 9: Wait (Chờ giữa các lần gửi)**
- **Cấu hình**:
  - **Time**: Đặt **10 giây** (để tránh bị Gmail chặn).
  - **Between items**: **True** (chờ giữa mỗi email).
- **Lưu ý**:
  - **Không cần thiết** nếu số lượng email ít, nhưng **khuyên dùng** để tránh bị chặn.

---
### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run** (nếu chưa chạy):
   - Nhấn **Run Workflow** với **dữ liệu mẫu** (đảm bảo Sheets có lead).
   - Kiểm tra **Gmail** xem email đã gửi thành công chưa.
2. **Bật Active**:
   - Đặt **Schedule Trigger** theo lịch (ví dụ: **9h sáng hàng ngày**).
   - Nhấn **Active** để workflow **chạy tự động**.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **1. Thêm Báo Cáo Slack/Telegram**
- **Cách làm**:
  - Thêm **node `n8n-nodes-base.slack`** hoặc **`n8n-nodes-base.telegram`**.
  - Gửi thông báo khi **email gửi thành công/bị lỗi**.
- **Lợi ích**:
  - Các sếp **biết ngay** nếu có lead nào bị lỗi.

### **2. Sử Dụng AI Viết Email Tự Động**
- **Cách làm**:
  - Thêm **node `n8n-nodes-base.llm`** (nếu self-hosted) hoặc **OpenAI API**.
  - **Prompt**:
    ```plaintext
    Tôi là [Tên bạn], và tôi muốn viết email follow-up cho lead [Tên lead].
    Email phải ngắn gọn, thân thiện, và đề cập đến [sản phẩm/dịch vụ].
    Dữ liệu lead: {{ $json["Name"] }}, {{ $json["Email"] }}, {{ $json["Note"] }}.
    ```
- **Lợi ích**:
  - **Tự động hóa viết email** mà không cần template.

### **3. Gửi Email Theo Chuỗi (Multi-Step)**
- **Cách làm**:
  - Thêm **cột `EmailSequence`** trong Google Sheets (ví dụ: `1`, `2`, `3`).
  - Sử dụng **node `filter`** để chỉ gửi email **thứ 1, 2, 3** cho từng lead.
- **Lợi ích**:
  - **Chuỗi email tự động** (ví dụ: Email 1 ngày 1, Email 2 ngày 3, Email 3 ngày 7).

### **4. Lưu Log Email Bị Lỗi**
- **Cách làm**:
  - Thêm **node `n8n-nodes-base.googleSheets`** để **ghi log lỗi** vào một sheet riêng.
  - Ví dụ: Nếu email bị lỗi, update cột `Error` trong Sheets.
- **Lợi ích**:
  - **Dễ dàng theo dõi** và **sửa lỗi** sau này.

### **5. Kết Hợp với CRM (HubSpot, Salesforce)**
- **Cách làm**:
  - Thêm **node `n8n-nodes-base.hubspot`** hoặc **`n8n-nodes-base.salesforce`**.
  - **Sync dữ liệu** từ Google Sheets sang CRM.
- **Lợi ích**:
  - **Tích hợp hoàn chỉnh** với hệ thống bán hàng hiện có.

---
## 📌 **Kết Luận: Tự Động Hóa Email Follow-Up Ngay Hôm Nay!**

Workflow này **giải