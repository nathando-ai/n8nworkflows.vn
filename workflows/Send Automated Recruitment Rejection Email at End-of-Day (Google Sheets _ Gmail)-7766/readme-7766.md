---
title: "🤖 **Tự Động Gửi Email Từ Chối Tuyển Dụng Tối Hôm Nay (Google Sheets + Gmail) – Không Cần Code!**"
description: "Workflow tự động hóa gửi email từ chối ứng viên vào cuối ngày từ Google Sheets, tiết kiệm thời gian cho bộ phận HR và tránh bỏ sót ứng viên. Hoạt động 24/7, cá nhân hóa nội dung, và tích hợp AI để tối ưu hóa."
slug: "tu-dong-gui-email-tu-choi-tuyen-dung-google-sheets-gmail"
tags: [n8n, automation, hr-automation, google-sheets, gmail-api, no-code-workflow]
keywords: [tự động hóa tuyển dụng, gửi email từ chối ứng viên, n8n workflow hr, google sheets gmail automation, tự động hóa bộ phận nhân sự]
---

# 🚀 **Tự Động Gửi Email Từ Chối Tuyển Dụng Tối Hôm Nay – Giải Pháp HR Không Cần Code**

### **Nỗi Đau Của Các Sếp HR**
Gửi email từ chối ứng viên là một trong những công việc **nhàn nhạt, tốn thời gian nhất** trong tuyển dụng. Các sếp thường phải:
- **Lặp đi lặp lại** cùng một nội dung từ chối cho hàng chục ứng viên.
- **Lo lắng bỏ sót** ứng viên nào đó vì quá tải công việc.
- **Chậm trễ** trong phản hồi, làm mất uy tín của công ty.
- **Khó theo dõi** trạng thái đã gửi hay chưa.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Lọc ứng viên cần từ chối** từ Google Sheets.
✅ **Tối ưu hóa nội dung email** với AI (nếu cần).
✅ **Gửi email cá nhân hóa** vào cuối ngày.
✅ **Cập nhật trạng thái** trong Google Sheets.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản miễn phí.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ cao)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải gửi email thủ công hàng ngày (tối đa **5 phút/ngày**).
- **Tránh bỏ sót ứng viên**: Workflow tự động lọc và xử lý tất cả ứng viên chưa được phản hồi.
- **Cá nhân hóa email**: Sử dụng tên và thông tin ứng viên từ Google Sheets.
- **Hoạt động liên tục**: Gửi email vào **cuối ngày** (ví dụ 18h) mà không cần can thiệp.
- **Tối ưu hóa AI (nâng cao)**: Có thể kết hợp với **LLM** để tự động viết email từ chối (nếu cần).
- **Theo dõi dễ dàng**: Cập nhật trạng thái **"Đã gửi"** trong Google Sheets.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Google Sheets**:
   - Một **bảng dữ liệu ứng viên** với các cột như:
     - `Email` (địa chỉ email ứng viên)
     - `Name` (tên ứng viên)
     - `Status` (trạng thái: "Pending", "Rejected", "Interviewed")
     - `Notes` (nếu có)
   - **Chia sẻ bảng với n8n** (quyền **Chỉ đọc** hoặc **Chỉ sửa**).

✔ **Tài khoản Gmail**:
   - Một **tài khoản Gmail chính thức** của công ty (không là Gmail cá nhân).
   - **API Gmail được kích hoạt** (trong [Google Cloud Console](https://console.cloud.google.com/)).
   - **OAuth 2.0 Credentials** đã cấu hình trong n8n (hướng dẫn [tại đây](https://docs.n8n.io/integrations/builtins/nodes/Gmail/)).

✔ **N8n Self-hosted** (không dùng phiên bản miễn phí để tránh giới hạn).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
**Bước 1:** Tải file JSON từ [n8n.io/workflows/7766](https://n8n.io/workflows/7766) hoặc copy toàn bộ JSON dưới đây.

**Bước 2:** Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON hoặc tải file JSON.

**Bước 3:** Chọn **"Create Workflow"** để tạo mới.

---
#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

##### **A. Cấu Hình Google Sheets**
- **Node: `Fetch Candidate Data`**
  - **Sheet Name**: Điền tên **trong Google Sheets** (không phải đường dẫn).
  - **Range**: Điền **tất cả dữ liệu** (ví dụ: `"Sheet1!A:Z"`).
  - **Credentials**: Chọn `googleSheetsOAuth2Api` (đã cấu hình trước).

- **Node: `Mark as Sent in Sheet`**
  - **Sheet Name**: Giống như trên.
  - **Range**: Điền **cột trạng thái** (ví dụ: `"Sheet1!D:D"`).
  - **Update Value**: Sử dụng **`{{ $json["status"] }}`** (cần chỉnh sửa trong **Code Node** sau).

##### **B. Cấu Hình Gmail**
- **Node: `Send Rejection Email1`**
  - **Credentials**: Chọn `gmailOAuth2`.
  - **From Email**: Điền **tài khoản Gmail chính thức** của công ty.
  - **Subject**: Có thể chỉnh sửa trong **Code Node** (`Process Email Template`).

##### **C. Chỉnh Sửa Code Node (Quá Trình Tối ưu)**
Workflow có **3 Code Node** quan trọng cần chỉnh sửa:

1. **`Filter Candidates for Rejection`**
   - **Mục tiêu**: Lọc ứng viên có `Status = "Pending"` và chưa được gửi email.
   - **Code mẫu**:
     ```javascript
     return {
       json: {
         candidates: $input.all().filter(item =>
           item.Status === "Pending" && !item.EmailSent
         )
       }
     };
     ```

2. **`Process Email Template`**
   - **Mục tiêu**: Tạo email cá nhân hóa với tên ứng viên.
   - **Code mẫu**:
     ```javascript
     return {
       json: {
         email: {
           to: item.Email,
           subject: "Cảm ơn vì đã ứng tuyển - Kết quả tuyển dụng",
           html: `
             <p>Chào <strong>${item.Name}</strong>,</p>
             <p>Cảm ơn bạn đã gửi hồ sơ ứng tuyển cho vị trí <strong>${item.Position}</strong> tại [Tên Công Ty].</p>
             <p>Sau khi xem xét kỹ lưỡng, chúng tôi quyết định không tiếp tục quá trình tuyển dụng cho vị trí này.</p>
             <p>Chúng tôi rất trân trọng thời gian và năng lực của bạn.</p>
             <p>Trân trọng,</p>
             <p>[Tên Công Ty]</p>
           `
         }
       }
     };
     ```

3. **`Mark as Sent in Sheet` (nếu cần cập nhật trạng thái)**
   - **Mục tiêu**: Cập nhật cột `EmailSent` thành `true` sau khi gửi.
   - **Code mẫu**:
     ```javascript
     return {
       json: {
         values: [
           ["true"] // Điền vào hàng ứng viên tương ứng
         ]
       }
     };
     ```

##### **D. Thiết Lập Lịch Triggers**
- **Node: `Schedule Trigger`**
  - **Cron Expression**: Đặt thời gian gửi email (ví dụ: `0 18 * * *` → **18h hàng ngày**).
  - **Time Zone**: Chọn **múi giờ của công ty**.

##### **E. Thiết Lập Dry Run (Test)**
- **Node: `Is Dry Run?`**
  - **Mục tiêu**: Test workflow trước khi gửi thật.
  - **Cách hoạt động**:
    - Nếu `{{ $json["dryRun"] }} = true`, workflow sẽ **không gửi email** mà chỉ hiển thị preview.
    - **Chỉnh sửa trong `Set: Config`**:
      ```json
      {
        "dryRun": false // Đặt `false` khi đã test xong
      }
      ```

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với **dryRun = true** để kiểm tra logic.
2. **Chạy workflow** và kiểm tra:
   - Email có được gửi không?
   - Trạng thái trong Google Sheets có được cập nhật không?
3. **Bật Active** khi đã kiểm tra xong.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với AI (LLM) để tự động viết email**
   - Thêm **node `n8n-nodes-ai.llm`** để tự động viết email từ chối dựa trên hồ sơ ứng viên.
   - Ví dụ: Sử dụng **Prompt**:
     ```
     Tôi là một ứng viên đã gửi hồ sơ cho công ty [Tên Công Ty]. Hãy viết một email từ chối lịch sự và cá nhân hóa với tên tôi là [Tên Ứng Viên], vị trí là [Vị Trí].
     ```

2. **Gửi báo cáo định kỳ**
   - Thêm **node `n8n-nodes-base.slack`** hoặc **`n8n-nodes-base.email`** để báo cáo số lượng email đã gửi mỗi ngày.

3. **Lưu log hoạt động**
   - Thêm **node `n8n-nodes-base.set`** để lưu log vào Google Sheets hoặc **Google Drive**.

4. **Tối ưu hóa rate limit**
   - Nếu gửi nhiều email, thêm **node `wait`** giữa các lần gửi để tránh bị Gmail chặn.

5. **Tích hợp với Slack/Telegram**
   - Thêm **node `n8n-nodes-base.slack`** để thông báo khi workflow hoàn thành.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho bộ phận HR, **tránh bỏ sót ứng viên**, và **cải thiện trải nghiệm ứng viên** với email cá nhân hóa. **Chỉ cần import, cấu hình và bật chạy** – không cần code!

**Hành động ngay:**
1. **Import workflow** vào n8n của mình.
2. **Chỉnh sửa Google Sheets và Gmail credentials**.
3. **Test dry run** trước khi kích hoạt.
4. **Bật workflow** và **nghỉ ngơi** – công việc từ chối ứng viên đã được tự động hóa!

---
**💡 Cần hỗ trợ?** Để lại comment hoặc liên hệ [WeblineIndia](https://www.weblineindia.com/) – đội ngũ đã phát triển workflow này!