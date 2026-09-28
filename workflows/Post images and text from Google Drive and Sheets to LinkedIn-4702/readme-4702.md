---
title: "🚀 Tự Động Hóa Đăng Bài LinkedIn Từ Google Drive & Sheets - Khai Thác 100% Miễn Phí (N8n)"
description: "Workflow tự động hóa đăng bài LinkedIn từ nội dung và hình ảnh trong Google Drive và Sheets, với hệ thống phê duyệt thông qua Telegram - tiết kiệm thời gian và nâng cao hiệu quả marketing cho doanh nghiệp."
slug: "tu-dong-hoa-dang-bai-linkedin-tu-google-drive-sheets"
tags: [n8n, automation, marketing, linkedin, google-sheets, telegram, no-code]
keywords: [n8n workflow linkedin, tự động hóa đăng bài linkedin, google sheets linkedin, tự động hóa marketing, n8n marketing automation]
---

# 🚀 **Tự Động Hóa Đăng Bài LinkedIn Từ Google Drive & Sheets - Giải Pháp Marketing Không Cần Code**

### **🔥 Nỗi Đau Của Các Sếp Trong Marketing LinkedIn**
Hàng ngày, các sếp phải:
- **Tìm kiếm và chuẩn bị nội dung** từ nhiều nguồn khác nhau (Google Drive, Sheets, hoặc thậm chí email).
- **Chỉnh sửa và tối ưu hình ảnh** trước khi đăng.
- **Phê duyệt nội dung** từ nhiều thành viên trong team, gây chậm trễ và mất thời gian.
- **Đăng bài thủ công** trên LinkedIn, dễ quên hoặc không theo lịch trình.

**Kết quả?** Nội dung không được đăng kịp thời, hiệu quả marketing giảm sút, và công việc trở nên rườm rà.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
Với workflow này, các sếp sẽ:
✅ **Tự động hóa toàn bộ quy trình** từ lấy nội dung đến đăng bài LinkedIn.
✅ **Phê duyệt nội dung thông qua Telegram** (nhanh chóng, không phụ thuộc vào email).
✅ **Lưu lịch sử** tất cả bài đăng trong Google Sheets, dễ theo dõi và phân tích.
✅ **Tiết kiệm thời gian lên đến 80%** so với cách làm thủ công.
✅ **Đăng bài liên tục** theo lịch trình, không bỏ lỡ cơ hội nào.

---
### **🎯 Yêu Cầu Cần Thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
📌 **Tài khoản LinkedIn** (đã cấp quyền API).
📌 **Tài khoản Google Drive & Sheets** (đã chia sẻ quyền đọc/ghi cho n8n).
📌 **Tài khoản Telegram** (để phê duyệt bài đăng).
📌 **File Google Sheets** với cấu trúc như sau:
| **Column**       | **Mô Tả**                          |
|------------------|-------------------------------------|
| `Post ID`        | ID duy nhất cho bài đăng.           |
| `Status`         | `Pending`, `Approved`, `Declined`.   |
| `Text`           | Nội dung bài đăng.                  |
| `Image URL`      | Đường dẫn hình ảnh trong Google Drive. |
| `LinkedIn Post`  | Bài đăng đã được đăng (nếu có).    |

📌 **File Google Drive** chứa hình ảnh (đã chia sẻ quyền đọc cho n8n).

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/4702](https://n8n.io/workflows/4702) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ link trên và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này được thiết kế với **2 cách kích hoạt**:
- **Lịch trình tự động** (Schedule Trigger) hoặc
- **Phê duyệt qua Telegram** (Telegram Trigger).

##### **A. Cấu Hình Google Sheets**
- **Node "Google Sheets"** (lấy dữ liệu bài đăng):
  - **Credentials:** Chọn tài khoản Google đã kết nối.
  - **Sheet Name:** Đặt tên file Sheets của bạn.
  - **Range:** `Sheet1!A:E` (đảm bảo cột phù hợp với bảng trên).
  - **Query:** `SELECT * WHERE Status = 'Pending'`.

- **Node "Update Sheet - Posted" & "Update Sheet - Declined"**:
  - **Credentials:** Cùng tài khoản Google.
  - **Range:** `Sheet1!A:E` (cập nhật trạng thái bài đăng).

##### **B. Cấu Hình LinkedIn**
- **Node "LinkedIn"**:
  - **Credentials:** Thêm tài khoản LinkedIn vào n8n (đã cấp quyền API).
  - **Action:** `createPost` (đăng bài).
  - **Tham số cần điền:**
    - `content`: `$node["Google Sheets"].json[0].Text`.
    - `imageUrl`: `$node["Google Sheets"].json[0].Image URL`.
    - `caption`: (Nếu có).

##### **C. Cấu Hình Telegram (Phê Duyệt)**
- **Node "Telegram Trigger"**:
  - **Credentials:** Thêm bot Telegram vào n8n (tạo bot tại [@BotFather](https://t.me/BotFather)).
  - **Chat ID:** ID của chat cá nhân hoặc nhóm (lấy từ [@userinfobot](https://t.me/userinfobot)).

- **Node "Telegram Approval"**:
  - **Message:** `"Xác nhận đăng bài ID: ${{ $node["Find Next Post3"].json[0].Post ID }}"`.
  - **Reply Markup:** Cung cấp 2 tùy chọn: **✅ Approve** hoặc **❌ Decline**.

##### **D. Cấu Hình Lịch Trình (Schedule Trigger)**
- **Node "Schedule Trigger"**:
  - **Frequency:** Chọn thời gian đăng (ví dụ: **Mỗi ngày lúc 9h sáng**).
  - **Time Zone:** Đặt theo giờ của bạn.

##### **E. Cấu Hình Node "Find Next Post3" (Function)**
- **Code cần chỉnh sửa** (nếu cần):
  ```javascript
  return {
    json: [
      {
        PostID: $node["Google Sheets"].json[0].PostID,
        Text: $node["Google Sheets"].json[0].Text,
        ImageURL: $node["Google Sheets"].json[0].ImageURL
      }
    ]
  };
  ```

##### **F. Cấu Hình Node "Code" & "Code1"**
- **Node "Code"**: Chỉnh sửa nếu cần xử lý logic đặc biệt (ví dụ: thay đổi định dạng text).
- **Node "Code1"**: Xử lý lỗi hoặc kiểm tra lại dữ liệu trước khi đăng.

##### **G. Cấu Hình Telegram Thông Báo Kết Quả**
- **Node "Telegram Success" & "Telegram Decline"**:
  - **Message:** Thông báo kết quả phê duyệt (ví dụ: `"Bài đăng ID: ${{ $node["Find Next Post3"].json[0].Post ID }} đã được đăng!"`).

---
#### **3. Kích Hoạt ⚡️**
1. **Test Run** với 1 bài đăng mẫu:
   - Chạy workflow và kiểm tra:
     - Dữ liệu từ Sheets có được lấy đúng không?
     - Telegram có gửi yêu cầu phê duyệt không?
     - LinkedIn có đăng bài thành công không?
2. **Bật Active** khi đã kiểm tra xong.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
🔹 **Kết hợp với Slack**: Thay vì Telegram, sử dụng **Slack** để phê duyệt bài đăng (cài node `n8n-nodes-base.slack`).
🔹 **Lưu Log Bài Đăng**: Sử dụng **Sticky Note** để ghi lại lịch sử bài đăng (node `n8n-nodes-base.stickyNote`).
🔹 **Gửi Báo Cáo Định Kỳ**: Tạo workflow riêng để gửi **tổng hợp thống kê** bài đăng hàng tháng qua email.
🔹 **Tối Ưu Hình Ảnh**: Sử dụng **node `n8n-nodes-base.imageProcessing`** để resize hoặc tối ưu hình ảnh trước khi đăng.
🔹 **Phân Loại Nội Dung**: Sử dụng **AI (LLM)** để phân loại bài đăng (ví dụ: bài chia sẻ, bài review) và tự động gán thẻ.

---
### **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào chiến lược marketing hơn, thay vì mắc kẹt trong công việc thủ công. **Tự động hóa 100% không cần code**, chỉ cần cấu hình đúng như hướng dẫn.

**🚀 Hãy áp dụng ngay và xem kết quả trong vòng 1 giờ!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💡 Cần hỗ trợ?** Đăng câu hỏi tại [n8n Community](https://community.n8n.io/) hoặc liên hệ với tác giả papcy qua Telegram.