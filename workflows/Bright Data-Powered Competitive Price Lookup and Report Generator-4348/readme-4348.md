---
title: "🚀 Tự Động Hóa So Sánh Giá Thương Mại & Tạo Báo Cáo Giá Cập Nhật Mới Nhất Với Bright Data + AI Gemini"
description: "Workflow tự động hóa so sánh giá sản phẩm từ Bright Data, phân tích cạnh tranh và gửi báo cáo định kỳ qua email với AI Gemini - tiết kiệm thời gian lên đến 80% cho các sếp marketing."
slug: "tieu-dong-hoa-so-sanh-gia-thuong-mai-voi-bright-data"
tags: [n8n, automation, marketing, ai, bright-data, google-gemini, email-automation]
keywords: [n8n workflow bright data, tự động hóa so sánh giá cạnh tranh, báo cáo giá hàng hóa tự động, ai gemini n8n, marketing automation]
---

# 🚀 **Tự Động Hóa So Sánh Giá Thương Mại & Tạo Báo Cáo Giá Cập Nhật Mới Nhất**

### **Giải pháp cho các sếp marketing:**
Bạn đã bao giờ phải mất **giờ đồng hồ** để tra cứu giá sản phẩm từ nhiều nguồn thương mại, so sánh với đối thủ, và sau đó tổng hợp thành báo cáo? Hay phải lo lắng rằng dữ liệu không được cập nhật kịp thời? **Workflow này sẽ thay bạn làm tất cả!**

Với **Bright Data** (dữ liệu thương mại lớn nhất thế giới) kết hợp **AI Gemini** của Google, workflow này sẽ:
✅ **Tự động tra cứu** giá sản phẩm từ hàng ngàn nguồn thương mại (Amazon, Shopee, Lazada, Tiki...)
✅ **So sánh giá cạnh tranh** theo danh sách sản phẩm của bạn
✅ **Tạo báo cáo chi tiết** với phân tích giá, xu hướng và gợi ý chiến lược
✅ **Gửi báo cáo tự động** qua email hàng ngày/tuần/tháng (không cần can thiệp)

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **ổn định 24/7**, các sếp nên **self-host n8n** trên VPS riêng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ **8+ giờ/tuần** xuống **5 phút/ngày** với báo cáo tự động.
- **Dữ liệu chính xác**: Tra cứu từ **Bright Data** (dữ liệu sạch, cập nhật liên tục).
- **Phân tích sâu**: AI Gemini **tự động tổng hợp** báo cáo với gợi ý chiến lược giá.
- **Hoạt động liên tục**: Không cần can thiệp, chạy **24/7** trên VPS.
- **Cá nhân hóa**: Chỉ cần **cập nhật danh sách sản phẩm** trong Google Sheets, workflow sẽ tự động xử lý.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Bright Data** (API Key) → [Đăng ký miễn phí](https://brightdata.com/)
✔ **Tài khoản Google Sheets** (để lưu danh sách sản phẩm cần theo dõi)
✔ **Tài khoản Gmail/SMTP** (để gửi báo cáo qua email)
✔ **API Key Google Gemini** (để sử dụng AI phân tích)
✔ **Danh sách sản phẩm** (được nhập vào Google Sheets, **chú ý viết hoa chính xác** như "Iphone" thay vì "iphone")

---
:::note[Lưu ý quan trọng]
**Dữ liệu tra cứu là case-sensitive!**
Ví dụ:
- **Đúng**: "Iphone", "GeForce", "Samsung Galaxy"
- **Sai**: "iphone", "geforce", "samsung galaxy"
Nếu nhập sai, workflow sẽ **không tìm thấy sản phẩm** và báo lỗi.
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/4348](https://n8n.io/workflows/4348) và import vào **n8n Editor**.
- **Copy JSON** từ trang trên và **paste** vào **Import Workflow** trong n8n.

#### **2. Các bước cấu hình BẮT BUỘC**
Sau khi import, các sếp cần **cấu hình các node quan trọng** như sau:

##### **A. Cấu hình Google Sheets**
1. **Node "Google Sheets"** (đọc danh sách sản phẩm):
   - Chọn **credentials**: `googleSheetsOAuth2Api`
   - **Sheet Name**: Đặt tên sheet chứa danh sách sản phẩm (ví dụ: `DanhSachSanPham`).
   - **Range**: `Sheet1!A2:B` (giả sử cột A là tên sản phẩm, cột B là link tham khảo).

##### **B. Cấu hình Bright Data API**
1. **Node "Snapshot Request"**, **"Snapshot Progress"**, **"Snapshot Content"**:
   - Chọn **credentials**: `brightdataApi`
   - **API Key**: Điền từ tài khoản Bright Data của bạn.
   - **Dataset ID**: Thay thế bằng **ID của dataset** bạn muốn tra cứu (ví dụ: `marketplace_dataset_amazon_us`).

##### **C. Cấu hình AI Gemini (Google Palm API)**
1. **Node "Google Gemini Chat Model"**:
   - Chọn **credentials**: `googlePalmApi`
   - **API Key**: Điền từ tài khoản Google Cloud (đăng ký tại [Google AI Studio](https://makersuite.google.com/)).
   - **Model**: Chọn `gemini-pro`.

2. **Node "Compare Prices and Generate Report"**:
   - **Prompt**: AI sẽ tự động sử dụng **template mặc định** để phân tích giá. Các sếp có thể **cập nhật prompt** trong node `chainLlm` nếu muốn thay đổi logic.

##### **D. Cấu hình Email (Gửi báo cáo)**
1. **Node "Email Report"**:
   - Chọn **credentials**: `smtp` (nếu dùng Gmail, cấu hình SMTP như sau):
     - **Host**: `smtp.gmail.com`
     - **Port**: `465`
     - **Username**: Email Gmail của bạn
     - **Password**: **App Password** (tạo tại [My Google Account > Security](https://myaccount.google.com/security))
   - **To**: Email nhận báo cáo (ví dụ: `marketing@doanhnghiep.com`).
   - **Subject**: `Báo cáo giá cạnh tranh [Ngày tháng]` (có thể tùy chỉnh).

##### **E. Cấu hình Node "If - Checking status of Snapshot"**
- **Tham số điều kiện**:
  - Kiểm tra `status` từ Bright Data.
  - Nếu `status === "ready"`, workflow tiếp tục; nếu `status === "error"`, chuyển sang node **Error message**.

##### **F. Cấu hình Node "Loop Over Items" (splitInBatches)**
- **Batch Size**: Đặt **10-20** (tùy thuộc vào tốc độ Bright Data trả về).
- **Parallel**: Bật **ON** để tăng tốc độ xử lý.

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **"Test Workflow"** và **chọn "Manual Trigger"** để chạy thử.
   - Kiểm tra **Google Sheets** để đảm bảo danh sách sản phẩm được đọc đúng.
   - Kiểm tra **email** để xem báo cáo có được gửi không.

2. **Bật Active**:
   - Sau khi test thành công, **bật Active** để workflow chạy tự động.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tự động chạy hàng ngày**:
   - Sử dụng **n8n Cron Trigger** để chạy workflow **mỗi ngày 8h sáng** (thay thế node `manualTrigger`).

2. **Lưu log và theo dõi lỗi**:
   - Thêm **node `stickyNote`** để ghi lại lỗi nếu Bright Data trả về `status === "error"`.
   - Kết hợp với **Slack/Telegram** để thông báo lỗi ngay khi xảy ra.

3. **Tùy chỉnh báo cáo**:
   - Sửa **node `markdown`** và **`code - Build HTML`** để thay đổi định dạng báo cáo (ví dụ: thêm biểu đồ giá, so sánh xu hướng).

4. **So sánh nhiều đối thủ**:
   - Nếu muốn so sánh **nhiều đối thủ** (ví dụ: Amazon, Shopee, Lazada), **tạo nhiều dataset** trong Bright Data và **cập nhật trong Google Sheets**.

5. **Gửi báo cáo đến nhiều người**:
   - Thay đổi **node `emailSend`** để gửi **CC/BCC** cho nhiều người trong team.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp marketing để tập trung vào **strategy** thay vì **data entry**. Với **Bright Data** và **AI Gemini**, bạn sẽ luôn có **dữ liệu chính xác, báo cáo chuyên nghiệp** và **gợi ý chiến lược giá** chỉ trong **5 phút/ngày**.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test run** và **bật Active**.
3. **Nhận báo cáo tự động** hàng ngày!

👉 **Nếu có vấn đề**, hãy để lại **comment** dưới bài viết hoặc liên hệ **Gleb D** (tác giả) qua [n8n Community](https://community.n8n.io/).

---
**Chúc các sếp thành công với tự động hóa marketing!** 🚀