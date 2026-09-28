---
title: "📰 Tự Động Hóa Theo Dõi & Phân Phối Tin Tức từ RSS Feed - Giúp Các Sếp Tiết Kiệm 10h/Tuần"
description: "Workflow tự động hóa theo dõi, lọc và phân phối tin tức từ nhiều nguồn RSS (đến Trello + Email), giúp các sếp tiết kiệm thời gian, duy trì thông tin cập nhật và chia sẻ nội dung chất lượng cho team. Kết quả: Tinh thần làm việc chuyên nghiệp cao hơn, quyết định dựa trên dữ liệu mới nhất."
slug: "tieu-dong-hoa-rss-feed-trello-email"
tags: [n8n, automation, marketing, rss-feed, trello, gmail, no-code]
keywords: [tự động hóa rss feed, theo dõi tin tức tự động, chia sẻ tin tức trello, workflow n8n marketing, tự động hóa nội dung]
---

# 🚀 **Tự Động Hóa Theo Dõi & Phân Phối Tin Tức từ RSS Feed - Giải Pháp Cho Các Sếp Marketing**

### **Nỗi Đau Của Các Sếp Hiện Nay**
Các sếp marketing hay content manager thường phải:
- **Tốn thời gian** theo dõi hàng chục nguồn tin tức (blog, báo, website chuyên ngành) thủ công.
- **Mất tập trung** vì phải lọc tin cũ, tin không liên quan hoặc tin trùng lặp.
- **Không đồng bộ** thông tin giữa team, dẫn đến quyết định sai lầm do thiếu dữ liệu mới nhất.
- **Khó chia sẻ** tin tức một cách hệ thống với team hoặc khách hàng.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Lấy tin tức** từ nhiều nguồn RSS (đến 9 nguồn).
✅ **Lọc tin mới nhất** (cấu hình được thời gian lọc, ví dụ: 7 ngày trở lại).
✅ **Sắp xếp theo thứ tự thời gian** để dễ đọc.
✅ **Chuyển đổi sang định dạng Markdown** (tiện cho chia sẻ).
✅ **Gửi tin tức lên Trello** (dạng comment) và **Email** (để team review).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy 24/7 mà không gián đoạn, các sếp nên **self-host n8n** trên VPS chuyên dụng.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10-15h/tuần** (không phải theo dõi RSS thủ công).
- **Tin tức luôn mới nhất** (cấu hình lọc theo ngày).
- **Chia sẻ dễ dàng** với team qua Trello + Email.
- **Dữ liệu sạch** (không tin trùng lặp, không tin cũ).
- **Hoạt động tự động** (không cần can thiệp người).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Trello** (để đăng tin tức dưới dạng comment).
2. **Tài khoản Gmail** (để gửi Email review cho team).
3. **API Key Trello** (để kết nối với Trello).
4. **Danh sách URL RSS** (các nguồn tin tức muốn theo dõi, ví dụ: TechCrunch, Forbes, BlogTechVietnam).
5. **Thời gian chạy định kỳ** (ví dụ: hàng ngày lúc 8h sáng).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/2785](https://n8n.io/workflows/2785) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ link trên và paste vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **2 phần chính**:
- **Phần 1:** Theo dõi **1 nguồn RSS** (ví dụ: MarkTechPost).
- **Phần 2:** Theo dõi **nhiều nguồn RSS** (tối đa 9 nguồn, cần merge).

##### **A. Cấu Hình Nguồn RSS**
1. **Thay đổi số lượng nguồn RSS**:
   - Mặc định có **2 node RSS Read** (1 nguồn + 1 nguồn merge).
   - **Nếu muốn thêm nguồn**, các sếp phải:
     - **Duplicate node RSS Read** (nhấp chuột phải > Duplicate).
     - **Kết nối node mới** vào **Merge node** (để hợp nhất dữ liệu).
     - **Cập nhật URL RSS** trong node mới (ví dụ: `https://feeds.feedburner.com/TechCrunch`).

2. **Cấu hình URL RSS**:
   - Mở node **RSS Read Testing Catalog** và **RSS Read MarkTechPost**.
   - Thay thế URL bằng nguồn tin tức của các sếp (ví dụ: `https://marktechpost.com/feed/`).

##### **B. Cấu Hình Lọc Tin Tức**
1. **Thay đổi thời gian lọc (7 ngày)**:
   - Mở node **Filter by date (more than 7 days)**.
   - Thay đổi công thức từ:
     ```javascript
     Date.now() - 7 * 24 * 60 * 60 * 1000
     ```
     thành:
     ```javascript
     Date.now() - 3 * 24 * 60 * 60 * 1000  // Lọc tin trong 3 ngày
     ```

2. **Thay đổi số lượng tin tức lấy**:
   - Mở node **Limit news to x** và thay đổi giá trị từ `10` thành số tin tức muốn lấy (ví dụ: `5`).

##### **C. Cấu Hình Trello & Gmail**
1. **Kết nối Trello**:
   - Vào **Credentials** > **Add Trello** và điền:
     - **API Key** (tạo từ [Trello Developer](https://trello.com/app-key)).
     - **Token** (tạo từ [Trello OAuth](https://trello.com/app-key)).
   - Trong node **Publish comment**, chọn:
     - **Board ID** (ID của Board Trello).
     - **List ID** (ID của List muốn đăng tin).
     - **Card ID** (ID của Card cụ thể, hoặc để trống để đăng comment chung).

2. **Kết nối Gmail**:
   - Vào **Credentials** > **Add Gmail OAuth2**.
   - Đăng nhập tài khoản Gmail và cấp quyền.
   - Trong node **Send revision email**, điền:
     - **Email recipient** (địa chỉ Email của người review).
     - **Subject** (tiêu đề Email, ví dụ: "Tin tức mới từ RSS - Review").

##### **D. Cấu Hình Schedule Trigger**
- Mở node **Schedule Trigger** và chọn:
  - **Frequency**: `Daily` (hàng ngày).
  - **Time**: `08:00:00` (lúc 8h sáng).
  - **Timezone**: `Asia/Ho_Chi_Minh` (hoặc timezone phù hợp).

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấp **Run Workflow** và kiểm tra:
     - Có tin tức được lấy không?
     - Có tin tức được lọc đúng không?
     - Trello và Email có nhận được không?
2. **Bật Active**:
   - Sau khi test thành công, chuyển **Status** từ `Inactive` sang `Active`.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Slack/Telegram Notifications**:
   - Thêm node **Slack** hoặc **Telegram Bot** sau **Merge node** để gửi tin tức ngay khi có.
   - Cài đặt **Slack Webhook** hoặc **Telegram Bot Token** trong Credentials.

2. **Lưu Log Tin Tức**:
   - Thêm node **Google Sheets** hoặc **Notion** sau **Merge node** để lưu tin tức vào bảng tính/đồ họa.
   - Cấu hình **Sheet Name** và **Range** trong node.

3. **Gửi Báo Cáo Định Kỳ**:
   - Thêm node **Google Drive** hoặc **Email Template** để gửi báo cáo tổng hợp hàng tuần.
   - Sử dụng **Code node** để định dạng báo cáo.

4. **Tự Động Xóa Tin Trùng Lặp**:
   - Thêm node **Filter** sau **Merge** với điều kiện:
     ```json
     {{$item.title}} !== undefined && !previousItems.includes($item.title)
     ```
     (Lọc bỏ tin trùng title).

---
### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp marketing muốn:
✔ **Tự động hóa theo dõi tin tức** từ nhiều nguồn.
✔ **Lọc tin tức mới nhất** và chia sẻ với team một cách hệ thống.
✔ **Tiết kiệm thời gian** để tập trung vào chiến lược nội dung.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test và bật Active** để bắt đầu tự động hóa.
3. **Mở rộng** bằng cách thêm Slack, Google Sheets hoặc báo cáo định kỳ.

**🚀 Các sếp sẵn sàng tự động hóa công việc của mình chưa?** 😉