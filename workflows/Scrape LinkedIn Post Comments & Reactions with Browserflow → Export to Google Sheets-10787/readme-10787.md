---
title: "🚀 Tự Động Hóa Scrape Bình Luận & Phản Hồi LinkedIn → Xuất Dữ Liệu Sang Google Sheets (Không Code)"
description: "Giải pháp tự động hóa 100% không cần code để scrap bình luận, phản hồi từ bài viết LinkedIn và xuất dữ liệu vào Google Sheets. Tiết kiệm thời gian lên đến 80% cho công việc nghiên cứu thị trường, lead generation và phân tích xu hướng."
slug: "tự-dộng-hoa-scrape-linkedin-comments-reactions-google-sheets"
tags: [n8n, automation, no-code, lead-generation, browserflow, google-sheets]
keywords: [scrape linkedin comments, tự động hóa linkedin, n8n workflow, export data google sheets, lead generation tự động]
---

# 🚀 **Tự Động Hóa Scrape Bình Luận & Phản Hồi LinkedIn → Xuất Dữ Liệu Sang Google Sheets**

### **Giải pháp cho các sếp:**
- **Bị mệt mỏi** khi phải copy-paste bình luận LinkedIn vào Excel để phân tích?
- **Mất thời gian** theo dõi phản hồi từ bài viết để đánh giá hiệu quả marketing?
- **Cần dữ liệu sạch** để xây dựng chiến lược lead generation nhưng không muốn viết code?

**Workflow này giúp bạn:**
✅ **Scrape bình luận và phản hồi** từ bất kỳ bài viết LinkedIn nào chỉ bằng một cú nhấp chuột.
✅ **Xuất dữ liệu tự động** vào Google Sheets với định dạng sẵn sàng phân tích.
✅ **Cập nhật trạng thái** bài viết đã được scrape để tránh trùng lặp.
✅ **Hoạt động 24/7** nếu kết hợp với cron job (nếu self-hosted).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Scrape hàng trăm bình luận chỉ trong vài giây thay vì thủ công.
- **Dữ liệu chính xác:** Không lo bị lỗi copy-paste hoặc thiếu thông tin.
- **Tự động hóa hoàn toàn:** Chỉ cần nhấp nút "Execute" hoặc lập lịch chạy định kỳ.
- **Dễ dàng phân tích:** Dữ liệu được xuất vào Google Sheets với cột riêng cho bình luận, phản hồi và trạng thái.
- **Cập nhật liên tục:** Tránh trùng lặp bằng cách đánh dấu bài viết đã scrape.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản LinkedIn** (để scrape bình luận).
2. **API Key của Browserflow** (node cộng đồng cho n8n).
3. **Google Sheets** với **3 tab** sau (sẵn sàng từ template):
   - **Posts** (danh sách URL bài viết cần scrape).
   - **Comments** (lưu bình luận scraped).
   - **Reactions** (lưu phản hồi scraped).
4. **Thành viên Google Sheets** có quyền chỉnh sửa.

---
:::info[CHUẨN BỊ]
**Bước 1:** Cài đặt node **Browserflow** cho LinkedIn:
- Vào [n8n Community Nodes](https://community.n8n.io/) và tìm `n8n-nodes-browserflow`.
- Cài đặt và kích hoạt node này trong n8n Editor.

**Bước 2:** Tạo **Google Sheets OAuth2 API Key**:
- Mở n8n Editor → **Credentials** → Tạo mới với loại `Google Sheets OAuth2`.
- Theo hướng dẫn để kết nối Google Sheets với n8n.

**Bước 3:** Chuẩn bị **template Google Sheets**:
- Sử dụng [template này](https://docs.google.com/spreadsheets/d/1XYZ...) (sẽ được cập nhật sau).
- Hoặc sao chép cấu trúc từ [hướng dẫn của tác giả](https://n8n.io/workflows/10787).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [đây](https://n8n.io/workflows/10787) (link gốc).
- Trong n8n Editor, nhấn **Import Workflow** và chọn file JSON tải xuống.
- **Hoặc copy JSON** từ file và dán vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **8 node** chính, các sếp cần chú ý cấu hình sau:

##### **A. Node `Manual Trigger` (Bắt đầu workflow)**
- **Không cần chỉnh sửa**, chỉ cần nhấn **Execute** khi cần chạy.

##### **B. Node `Browserflow` (Scrape bình luận & phản hồi)**
- **Credentials:** Chọn `browserflowApi` (đã tạo trước).
- **Key Parameters:**
  - `operation`: Đặt là `scrapeProfilesFromPostComments` (không đổi).
  - **Cần thêm:**
    - `url`: **Không điền thủ công!** Dữ liệu URL sẽ được lấy từ **Google Sheets (tab Posts)**.
    - **API Key Browserflow:** Điền vào `browserflowApi` trong Credentials.

##### **C. Node `Split Out` (Tách dữ liệu)**
- **Không cần chỉnh**, node này tự động tách bình luận và phản hồi thành 2 stream riêng.

##### **D. Node `Google Sheets` (Xuất dữ liệu)**
- **Credentials:** Chọn `googleSheetsOAuth2Api` (đã tạo trước).
- **Tab `Comments`:**
  - **Sheet Name:** Đặt là `Comments` (phải trùng với tab trong Google Sheets).
  - **Range:** Đặt là `A1` (nơi dữ liệu sẽ được append).
- **Tab `Reactions`:**
  - **Sheet Name:** Đặt là `Reactions`.
  - **Range:** Đặt là `A1`.
- **Tab `Posts` (lấy URL):**
  - **Operation:** Chọn `update` (để cập nhật trạng thái bài viết đã scrape).
  - **Range:** Đặt là `A1` (cột chứa URL).
  - **Column:** Chọn cột `Status` (để ghi `Scraped` khi hoàn tất).

##### **E. Node `Sticky Note` (Ghi chú)**
- **Không cần chỉnh**, chỉ dùng để ghi chú trong workflow.

---
#### **3. Kích hoạt ⚡️**
1. **Test Run với dữ liệu mẫu:**
   - Điền **1 URL bài viết** vào tab `Posts` trong Google Sheets.
   - Chạy workflow và kiểm tra tab `Comments` và `Reactions` có xuất dữ liệu không.
2. **Bật Active:**
   - Sau khi test thành công, nhấn **Active** để workflow sẵn sàng chạy.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Lập lịch chạy tự động (Cron Job):**
   - Nếu self-hosted, sử dụng **Cron Job** để chạy workflow định kỳ (ví dụ: hàng ngày).
   - Ví dụ: `0 9 * * *` (chạy lúc 9h sáng hàng ngày).

2. **Lọc phản hồi theo loại:**
   - Sử dụng **Browserflow** để filter chỉ lấy phản hồi như "Like", "Celebrate", "Love" (nếu cần).

3. **Xuất dữ liệu sang Excel/CSV:**
   - Sau khi scrape xong, sử dụng **Google Apps Script** để xuất dữ liệu từ Sheets sang Excel.

4. **Kết hợp với Slack/Telegram:**
   - Thêm node **Slack** hoặc **Telegram Bot** để thông báo khi scrape hoàn tất.

5. **Phân tích dữ liệu tự động:**
   - Sử dụng **Google Apps Script** hoặc **n8n** để tự động tính toán:
     - Số bình luận trung bình.
     - Phản hồi tích cực/tiêu cực.
     - Từ khóa phổ biến.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần scrape dữ liệu LinkedIn mà không viết code. Bằng cách kết hợp **Browserflow** và **Google Sheets**, bạn có thể:
✔ **Tiết kiệm thời gian** so với phương pháp thủ công.
✔ **Dữ liệu sạch và dễ phân tích**.
✔ **Hoạt động 24/7** nếu tự động hóa.

**Hành động ngay:**
1. Chuẩn bị **Google Sheets** và **Browserflow API Key**.
2. Import workflow và **chỉnh sửa các node Google Sheets**.
3. **Test Run** và bắt đầu scrape!

**Cần hỗ trợ?** Để lại comment bên dưới hoặc liên hệ với tác giả [Kees Bosch](https://n8n.io/workflows/10787) để cập nhật template Sheets.

---
**🚀 Cùng tự động hóa công việc của mình ngay hôm nay!**