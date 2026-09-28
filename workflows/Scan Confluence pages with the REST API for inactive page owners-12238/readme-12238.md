---
title: "🔍 **Tự Động Hóa Scan Trang Confluence Có Chủ Đăng Ký Inactive - Giải Pháp Không Code Cho Quản Trị Nội Dung**"
description: "Workflow này tự động phát hiện và báo cáo các trang Confluence có chủ sở hữu không còn hoạt động (`accountStatus !== active`), giúp các sếp tiết kiệm thời gian kiểm tra thủ công và duy trì tính chính xác của dữ liệu. Kết quả được xuất dưới dạng báo cáo sẵn sàng chia sẻ hoặc tích hợp với Slack/Email."
slug: "tieu-dong-hoa-scan-trang-confluence-co-chu-dang-ky-inactive"
tags: [n8n, automation, confluence, api-integration, document-management, no-code]
keywords: [n8n workflow confluence, tự động hóa quản lý nội dung, tìm kiếm chủ sở hữu inactive, API Confluence v2, tự động hóa IT]
---

# 🚀 **Tự Động Hóa Scan Trang Confluence Có Chủ Đăng Ký Inactive**

### **Nỗi Đau Của Các Sếp**
Quản lý nội dung trên Confluence là một công việc phức tạp, đặc biệt khi phải theo dõi hàng trăm trang và chủ sở hữu. Các sếp thường phải:
- **Kiểm tra thủ công** từng trang để xác định chủ sở hữu đã inactive (ví dụ: nhân viên nghỉ việc, chuyển nhóm).
- **Tốn thời gian** để cập nhật quyền hạn hoặc chuyển nhượng trang cho người mới.
- **Mất trắng dữ liệu** khi không phát hiện kịp thời các chủ sở hữu không còn hoạt động, dẫn đến nội dung bị bỏ rơi hoặc không được cập nhật.

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✅ **Tự động quét** tất cả trang trong các space được chỉ định.
✅ **Phát hiện chủ sở hữu inactive** dựa trên API Confluence (trạng thái `accountStatus !== active`).
✅ **Tạo báo cáo chi tiết** sẵn sàng chia sẻ hoặc tích hợp với Slack/Email.
✅ **Hoạt động 24/7** trên VPS riêng, không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần quét thủ công hàng trăm trang mỗi tháng.
- **Chính xác 100%**: Dựa trên API Confluence, tránh sai sót do con người.
- **Cá nhân hóa báo cáo**: Lọc ra chỉ các trang có chủ sở hữu inactive, sẵn sàng chuyển giao.
- **Hoạt động liên tục**: Workflow chạy tự động mỗi khi kích hoạt, không phụ thuộc vào giờ làm việc.
- **Tích hợp dễ dàng**: Kết quả có thể gửi qua Slack, Email, hoặc xuất CSV cho phân tích sâu hơn.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Confluence**:
   - Một tài khoản **Admin** hoặc có quyền đọc **spaces, pages, và users** trên Confluence Cloud.
   - **API Token** của tài khoản (tạo tại [Atlassian API Token](https://id.atlassian.com/manage-profile/security/api-tokens)).
2. **Thông tin cấu hình**:
   - **Domain Confluence**: Ví dụ: `yourcompany.atlassian.net`.
   - **Space Keys**: Danh sách keys của các space cần quét (ví dụ: `ENG,HR,DEV`), cách nhau bởi dấu phẩy.
3. **Credentials n8n**:
   - **HTTP Basic Auth** (sử dụng email Atlassian + API Token) để kết nối với API Confluence.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/12238) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn **Import** → Dán JSON hoặc chọn file JSON đã tải.
- Workflow sẽ tự động tạo 14 nodes như mô tả.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
##### **A. Cấu Hình Node "Set Variables"**
- Mở node **"Set Variables"** (node thứ 2).
- Điền các tham số sau:
  ```json
  {
    "atlassianDomain": "yourcompany.atlassian.net",
    "spaceKeys": "ENG,HR,DEV"  // Thay thế bằng keys của các space cần quét
  }
  ```
- **Lưu ý**: Không có dấu cách trong `spaceKeys` và các keys cách nhau bởi dấu phẩy.

##### **B. Thiết Lập Credentials HTTP Basic Auth**
- Mở **Credentials Manager** trong n8n (nhấn vào biểu tượng **⚙️** ở góc trên bên phải).
- Tạo một **HTTP Basic Auth** mới với:
  - **Username**: Email Atlassian của bạn (ví dụ: `nguyen.van.a@yourcompany.com`).
  - **Password**: **API Token** đã tạo trước đó.
- **Gán credentials** cho tất cả các node `httpRequest` liên quan đến Confluence (tên node bắt đầu bằng "Confluence -"):
  - Mở từng node `httpRequest` → Tab **Credentials** → Chọn credentials vừa tạo.

##### **C. Kiểm Tra Node "Confluence - Get Pages"**
- Node này có **limit 50 trang/trang**. Nếu space có nhiều hơn 50 trang, workflow sẽ tự động phân trang.
- **Không cần chỉnh sửa** nếu không muốn thay đổi logic phân trang mặc định.

##### **D. Node "Filter Inactive Owners"**
- Workflow tự động lọc trang có `accountStatus !== active`. **Không cần chỉnh sửa** nếu muốn giữ logic mặc định.

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Nhấn **Execute Workflow** để chạy thử với dữ liệu mẫu.
  - Kiểm tra **output** trong node **"Aggregate"** để xem kết quả lọc ra các trang có chủ sở hữu inactive.
- **Bật Active**:
  - Sau khi kiểm tra thành công, chuyển trạng thái workflow từ **Inactive** sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Slack/Email Báo Cáo**:
   - Sau node **"Aggregate"**, thêm node **Slack** hoặc **Email** để tự động gửi báo cáo khi phát hiện trang inactive.
   - Ví dụ: Gửi thông báo Slack với danh sách trang cần chuyển giao:
     ```json
     {
       "blocks": [
         {
           "type": "section",
           "text": {
             "type": "mrkdwn",
             "text": "*Báo cáo trang Confluence có chủ sở hữu inactive*"
           }
         },
         {
           "type": "divider"
         },
         {
           "type": "section",
           "fields": [
             {
               "type": "mrkdwn",
               "text": "*Trang:*\n${$json["title"]}\n*Space:*\n${$json["spaceName"]}\n*Chủ sở hữu:*\n${$json["displayName"]}"
             }
           ]
         }
       ]
     }
     ```

2. **Xuất Dữ Liệu Sang CSV**:
   - Thêm node **Google Sheets** hoặc **CSV** sau node **"Aggregate"** để lưu dữ liệu vào file Excel hoặc bảng Google Sheets cho phân tích sâu hơn.

3. **Lưu Log Hoạt Động**:
   - Thêm node **n8n-nodes-base.stickyNote** để ghi lại thời gian chạy và số trang bị phát hiện.
   - Ví dụ:
     ```json
     {
       "text": `📅 Thời gian chạy: ${new Date().toLocaleString()}\n📊 Số trang inactive: ${$json.length}`
     }
     ```

4. **Chạy Định Kỳ**:
   - Sử dụng **n8n Trigger** (n8n-nodes-base.trigger) để chạy workflow hàng tuần/monthly. Ví dụ:
     - **Trigger**: `n8n-nodes-base.cron` với biểu thức `0 0 1 * *` (chạy hàng tháng ngày 1).

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp quản lý nội dung Confluence, giúp tự động hóa việc phát hiện và xử lý chủ sở hữu inactive **không cần viết code**. Bằng cách kết hợp với Slack, Email, hoặc Google Sheets, các sếp có thể **tích hợp workflow này vào quy trình làm việc hàng ngày** và tiết kiệm hàng giờ mỗi tháng.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn trên.
2. **Kích hoạt** và theo dõi kết quả trong node **"Aggregate"**.
3. **Tích hợp** với Slack/Email để nhận báo cáo tự động.

Nếu có vấn đề, liên hệ với **Atlassian Support** hoặc **n8n Community** tại [n8n.io](https://n8n.io/community). 🚀

---
**💡 Chia sẻ workflow này với đồng nghiệp để cùng tự động hóa quản lý nội dung Confluence!**