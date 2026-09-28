---
title: "📁 **Tự Động Hóa Kiểm Tra & Xử Lý Tệp Hàng Ngày + Gửi Báo Cáo Email (GitHub Storage)**"
description: "Workflow tự động hóa kiểm tra, tải xuống, phân tích và lưu trữ dữ liệu từ các tệp mới (đặc biệt là CSV) vào GitHub, đồng thời gửi báo cáo kết quả qua email hàng ngày. Giúp các sếp tiết kiệm thời gian, giảm thiểu lỗi thủ công và đảm bảo dữ liệu luôn được cập nhật chính xác."
slug: "tu-dong-hoa-kiem-tra-xu-ly-tep-github-email"
tags: [n8n, automation, file-management, github, email-notification, csv-processing, no-code]
keywords: [n8n workflow tự động hóa tệp, xử lý CSV tự động, lưu trữ GitHub tự động, gửi báo cáo email hàng ngày, tự động hóa file management]
---

# 🚀 **Tự Động Hóa Kiểm Tra & Xử Lý Tệp Hàng Ngày Với GitHub Storage**

### **Giải quyết vấn đề gì?**
Các sếp thường phải **thủ công** kiểm tra, tải xuống và xử lý hàng loạt tệp mới (đặc biệt là CSV) từ các nguồn khác nhau như FTP, SharePoint hoặc API. Quá trình này **tốn thời gian, dễ sai sót**, và không thể hoạt động liên tục 24/7. Workflow này **tự động hóa toàn bộ quy trình** bằng cách:
✅ **Kiểm tra và tải xuống** tất cả tệp mới từ một **endpoint HTTP** (hoặc thay thế bằng S3/SharePoint).
✅ **Phân tích và validate** dữ liệu trong CSV theo **nguyên tắc kinh doanh** (kiểm tra trường bắt buộc, kiểu dữ liệu, logic tùy chỉnh).
✅ **Lưu trữ dữ liệu hợp lệ** vào **GitHub** dưới dạng commit mới.
✅ **Gửi báo cáo email tự động** cho các stakeholder, thông báo **thành công/thất bại** của mỗi run.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài **n8n trên VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ xử lý nhanh)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần kiểm tra tệp thủ công hàng ngày.
- **Chính xác 100%**: Kiểm tra và validate dữ liệu tự động, giảm thiểu lỗi.
- **Lưu trữ an toàn**: Dữ liệu hợp lệ được commit vào **GitHub** với lịch sử thay đổi.
- **Báo cáo tự động**: Email thông báo kết quả mỗi run (thành công/thất bại).
- **Dễ mở rộng**: Thay đổi nguồn tệp (S3, SharePoint) mà không cần sửa code.
- **Hoạt động liên tục**: Chạy theo lịch trình (daily/weekly) mà không cần can thiệp.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Endpoint HTTP** trả về danh sách tệp mới (dạng JSON với trường: `id`, `url`, `fileName`, `mimeType`).
   - Ví dụ: `https://api.example.com/files/pending`
2. **Credentials GitHub OAuth**:
   - Tạo **Personal Access Token** (PAT) với quyền `repo` (ở [GitHub Settings](https://github.com/settings/tokens)).
   - Thêm vào n8n dưới dạng **GitHub Credential** (trong **Credentials Management**).
3. **SMTP Credential** cho gửi email:
   - Cấu hình tài khoản email (Gmail, Outlook, hoặc SMTP riêng) trong **Email Send Node**.
4. **Tham số tùy chỉnh** (nếu cần):
   - **Validation rules** trong node **Validate Data** (cập nhật theo logic kinh doanh).
   - **Branch/GitHub repo** để lưu trữ dữ liệu.

---
---

### 🚀 **Cách Import & Lưu ý khi "Lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/13192](https://n8n.io/workflows/13192) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn **Import Workflow** → Dán JSON hoặc tải file `.json`.
- **Kích hoạt workflow** bằng cách bật **Active** ở góc trên bên phải.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **17 node**, các bước quan trọng cần cấu hình:

##### **A. Cấu hình Trigger & Lấy Dữ liệu**
1. **Daily File Check (Schedule Trigger)**
   - Thiết lập **interval** (ví dụ: `0 0 * * *` = chạy hàng ngày lúc 00:00).
   - **Lưu ý**: Nếu muốn chạy theo lịch trình khác, chỉnh sửa ở đây.

2. **Fetch File List (HTTP Request)**
   - **URL**: Điền vào **Request URL** (ví dụ: `https://api.example.com/files/pending`).
   - **Method**: `GET`.
   - **Headers**: Thêm `Authorization` nếu cần (nếu API yêu cầu token).
   - **Response Format**: Chọn `JSON`.

3. **Check File Count (Code Node)**
   - **Lưu ý**: Node này đếm số tệp để quyết định tiếp tục hoặc dừng workflow.
   - **Không cần chỉnh sửa** nếu endpoint trả về đúng định dạng.

4. **Any New Files? (If Node)**
   - **Condition**: `$json["files"].length > 0` (kiểm tra danh sách tệp có trống không).
   - **Nếu không có tệp**, workflow sẽ tự động chuyển sang **Send Error Email** (nếu cần).

##### **B. Xử Lý & Validate Tệp**
5. **Prepare File Items (Code Node)**
   - **Lưu ý**: Node này chuẩn bị dữ liệu cho **SplitInBatches**.
   - **Không cần chỉnh sửa** nếu endpoint trả về đúng cấu trúc.

6. **Iterate Files (SplitInBatches)**
   - **Batch Size**: Đặt số lượng tệp xử lý cùng một lúc (ví dụ: `1` để xử lý từng tệp riêng).
   - **Lưu ý**: Nếu tệp lớn, có thể tăng batch size nhưng cần kiểm tra tài nguyên VPS.

7. **Download File (HTTP Request)**
   - **URL**: `$node["Fetch File List"].json["files"][item].url` (tự động lấy từ danh sách).
   - **Method**: `GET`.
   - **Response Format**: `Binary` (để tải xuống tệp nguyên vẹn).

8. **Is CSV? (If Node)**
   - **Condition**: `$json["mimeType"].includes("csv")`.
   - **Nếu không phải CSV**, workflow sẽ **bỏ qua** tệp đó (không gửi email lỗi).

9. **Parse CSV (Code Node)**
   - **Lưu ý**: Node này sử dụng **Papaparse** để phân tích CSV.
   - **Không cần chỉnh sửa** nếu dữ liệu CSV chuẩn.

10. **Validate Data (Code Node)**
    - **Đây là node quan trọng nhất!** Các sếp cần **cập nhật logic validate** theo yêu cầu kinh doanh.
    - **Ví dụ code mẫu** (cập nhật trong **Code Editor**):
      ```javascript
      // Kiểm tra trường bắt buộc và kiểu dữ liệu
      const requiredFields = ["id", "name", "email", "status"];
      const errors = [];

      for (const field of requiredFields) {
        if (!data[field]) {
          errors.push(`Missing required field: ${field}`);
        }
      }

      // Kiểm tra kiểu dữ liệu (ví dụ: email phải là string)
      if (data.email && typeof data.email !== "string") {
        errors.push("Email must be a string");
      }

      return {
        json: {
          isValid: errors.length === 0,
          errors: errors
        }
      };
      ```
    - **Nếu validate thất bại**, workflow sẽ chuyển sang **Send Error Email**.

##### **C. Lưu Trữ & Gửi Báo Cáo**
11. **Prepare GitHub Commit (Set Node)**
    - **GitHub Credential**: Chọn credential đã tạo trước đó.
    - **Repository**: Điền tên repo (ví dụ: `my-data-repo`).
    - **Branch**: Đặt tên branch (ví dụ: `main`).
    - **Commit Message**: Tùy chỉnh (ví dụ: `Update data from ${new Date().toLocaleDateString()}`).

12. **Create/Update File (GitHub Node)**
    - **Path**: Đặt đường dẫn tệp trong repo (ví dụ: `data/processed/${fileName}`).
    - **Content**: `$node["Parse CSV"].json` (dữ liệu đã parse).
    - **Lưu ý**: Nếu tệp đã tồn tại, GitHub sẽ **update** nó.

13. **Success/Error Email Content (Set Node)**
    - **Email Subject**: Tùy chỉnh (ví dụ: `📊 Thành công: ${fileName} đã được xử lý`).
    - **Email Body**: Thêm thông tin chi tiết (ví dụ: số dòng, thời gian xử lý).
    - **Example**:
      ```html
      <p>🎉 File <strong>{{ $node["Download File"].json["fileName"] }}</strong> đã được xử lý thành công!</p>
      <p>Số dòng: {{ $node["Parse CSV"].json.data.length }}</p>
      <p>Thời gian: {{ $node["Schedule Trigger"].date }}</p>
      ```

14. **Send Success/Error Email (Email Send Node)**
    - **SMTP Credential**: Chọn credential email đã cấu hình.
    - **To**: Điền email của stakeholder (ví dụ: `team@example.com`).
    - **From**: Điền địa chỉ gửi (ví dụ: `noreply@example.com`).
    - **Lưu ý**: Nếu muốn gửi email lỗi cho người khác, chỉnh sửa ở đây.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Chạy **Manual Trigger** để kiểm tra workflow với dữ liệu mẫu.
   - Kiểm tra **GitHub repo** và **email** để xác nhận kết quả.
2. **Bật Active**:
   - Sau khi test thành công, bật **Active** để workflow chạy tự động theo lịch.

---

### ✍️ **Mẹo & Gợi ý Nâng Cao**
1. **Thay đổi nguồn tệp**:
   - Thay **HTTP Request** bằng **S3** hoặc **SharePoint** bằng cách sử dụng **n8n nodes** tương ứng (ví dụ: `n8n-nodes-base.awsS3`).
   - **Lưu ý**: Cần cập nhật **Prepare File Items** để phù hợp với định dạng mới.

2. **Lưu log xử lý**:
   - Thêm **Sticky Note** hoặc **Database Node** (ví dụ: **PostgreSQL**) để lưu lịch sử xử lý.
   - **Ví dụ**:
     ```json
     {
       "fileName": "{{ $node["Download File"].json["fileName"] }}",
       "status": "{{ $node["Validation Passed?"].json["isValid"] ? "Success" : "Error" }}",
       "timestamp": "{{ $node["Schedule Trigger"].date }}"
     }
     ```

3. **Gửi báo cáo định kỳ**:
   - Sử dụng **Schedule Trigger** khác để gửi **tổng hợp báo cáo hàng tuần/tháng**.
   - **Ví dụ**: Chạy workflow thứ 7 hàng tuần và gửi email tổng hợp.

4. **Tự động xử lý tệp mới trên SharePoint**:
   - Thay **HTTP Request** bằng **SharePoint Node** (`n8n-nodes-base.sharepoint`).
   - Cấu hình **List Name** và **Filter Query** để lấy tệp mới.

5. **Kết hợp với Slack/Telegram**:
   - Thêm **Slack Webhook** hoặc **Telegram Bot** để thông báo kết quả thực thời.
   - **Ví dụ**:
     ```json
     {
       "text": "📄 File *{{ $node["Download File"].json["fileName"] }}* đã được xử lý thành công!"
     }
     ```

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc kiểm tra tệp thủ công hàng ngày, đồng thời **đảm bảo dữ liệu luôn được validate và lưu trữ an toàn** trên GitHub. Bằng cách **tự động hóa toàn bộ quy trình**, các sếp có thể:
✔ **Tiết kiệm 5-10 giờ/tuần** cho công việc thủ công.
✔ **Giảm thiểu lỗi** do con người gây ra.
✔ **Cập nhật dữ liệu liên tục** mà không cần can thiệp.
✔ **Dễ dàng mở rộng** cho các nguồn tệp mới.

**🚀 Hãy import workflow ngay hôm nay và tự động hóa quy trình của mình!**
Nếu có bất kỳ câu hỏi hoặc cần hỗ trợ, các sếp có thể **comment bên dưới** hoặc liên hệ với cộng đồng n8n tại [n8n Community](https://community.n8n.io/).

---
**#TựĐộngHóa #n8n #GitHub #EmailAutomation #CSVProcessing**