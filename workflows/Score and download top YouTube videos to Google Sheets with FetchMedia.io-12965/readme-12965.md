---
title: "🎥 **Tự Động Hóa Tải Xuống & Đánh Giá Top Video YouTube Sang Google Sheets (Không Cần Code!)**"
description: "Workflow tự động hóa tìm kiếm, lọc, đánh giá và tải xuống video YouTube chất lượng cao sang Google Sheets với FetchMedia.io. Giúp các sếp tiết kiệm thời gian nghiên cứu thị trường và tự động hóa quá trình phân tích nội dung video."
slug: "tieu-dong-hoa-tai-xuong-video-youtube-sang-google-sheets"
tags: [n8n, automation, youtube, google-sheets, fetchmedia, market-research]
keywords: [n8n workflow youtube, tự động hóa tải video youtube, phân tích video youtube, fetchmedia api, google sheets automation]
---

# 🚀 **Tự Động Hóa Tải Xuống & Đánh Giá Top Video YouTube Sang Google Sheets**

### **Giải pháp hoàn hảo cho các sếp cần:**
- **Tìm kiếm và lọc video YouTube chất lượng cao** (theo tiêu đề, lượt xem, tương tác, thời lượng).
- **Tự động tải xuống video** (nếu kết nối FetchMedia.io).
- **Lưu kết quả vào Google Sheets** với metadata chi tiết (đánh giá, trạng thái tải, URL).
- **Không cần viết code** – chỉ cần cấu hình và chạy!

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Tự động hóa quá trình tìm kiếm và lọc video thay vì làm thủ công.
✅ **Chất lượng cao**: Lọc video theo tiêu chí **tương tác, thời lượng, ngày đăng** để tránh spam.
✅ **Tải xuống tự động**: Sử dụng FetchMedia.io để tải video một cách hiệu quả.
✅ **Báo cáo tự động**: Kết quả được ghi vào Google Sheets với **đánh giá, trạng thái tải, và URL**.
✅ **Hoạt động 24/7**: Workflow chạy liên tục, không cần can thiệp thủ công.
:::

---

## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Cloud** (để kích hoạt **YouTube Data API v3**).
2. **Tài khoản Google Sheets** (để lưu kết quả).
3. *(Tùy chọn)* **API Key FetchMedia.io** (nếu muốn tải video).
4. **Tham số cấu hình**:
   - Danh sách **query tìm kiếm YouTube** (ví dụ: "cách học tiếng Anh", "marketing digital").
   - **Ngưỡng lọc video** (lượt xem, lượt thích, thời lượng, ngày đăng).
   - **Tên Sheet Google** và **tab** để lưu kết quả.
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/12965](https://n8n.io/workflows/12965) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ link trên và dán vào **Import Workflow** trong n8n.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **3 phần chính**:
1. **Tìm kiếm & Lọc Video YouTube**
2. **Đánh giá & Sắp xếp**
3. **Tải xuống & Cập nhật Google Sheets**

#### **🔹 Bước 1: Cấu hình YouTube API**
- **Node "Search YouTube"**:
  - Chọn **credentials**: `youTubeOAuth2Api` (cần thiết lập trước).
  - Điền **query** (ví dụ: `"cách học tiếng Anh"`).
  - Cấu hình **lọc theo tiêu chí**:
    - **Title keywords** (lọc video có từ khóa trong tiêu đề).
    - **Publish date** (chỉ lấy video trong khoảng thời gian nhất định).
    - **Engagement signals** (lượt xem, lượt thích tối thiểu).

#### **🔹 Bước 2: Chuyển đổi & Đánh giá Video**
- **Node "Add Duration Seconds" (Code)**:
  - Chuyển đổi thời lượng video từ **ISO-8601** (ví dụ: `PT5M30S`) thành **giây** để dễ dàng lọc.
  - Ví dụ: `5 minutes 30 seconds` → `330 seconds`.
- **Node "Generate Relevance Score" (Set)**:
  - Đánh giá video theo **công thức tự định义** (ví dụ: `(likes / (views / 1000)) * duration`).
  - Cập nhật điểm số vào metadata.

#### **🔹 Bước 3: Tải xuống & Cập nhật Google Sheets**
- **Node "Start Fetch (FetchMedia)"**:
  - Nếu có **FetchMedia API Key**, workflow sẽ gửi yêu cầu tải video.
  - Nếu không, workflow sẽ **bỏ qua bước tải** và chỉ ghi metadata vào Sheets.
- **Node "Poll loop (Wait → GET status → check → loop)"**:
  - **Polling** (kiểm tra trạng thái tải) mỗi **30 giây** cho đến khi video tải xong.
  - Sau **30 lần retry**, nếu tải thất bại, workflow sẽ ghi **"Failed"** vào Sheets.

#### **🔹 Cấu hình Google Sheets**
- **Node "Send to Google Sheets"**:
  - Chọn **credentials**: `googleSheetsOAuth2Api`.
  - Chọn **Sheet và tab** để lưu kết quả.
  - **Operation**: `append` (thêm mới) hoặc `update` (cập nhật nếu video đã tồn tại).
- **Node "Update the status of the download"**:
  - Cập nhật **trạng thái tải** (Pending → Success/Failed).

---

### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Chọn **Execute workflow** và kiểm tra kết quả trong Google Sheets.
   - Nếu có FetchMedia.io, kiểm tra **trạng thái tải** trong Sheets.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, **bật Active** để workflow chạy tự động.

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
🔹 **Kết hợp với Slack/Telegram**:
   - Gửi thông báo khi **tải video thành công/thất bại** qua Slack/Telegram.
   - Sử dụng **node `n8n-nodes-base.slack`** hoặc **`n8n-nodes-base.telegram`**.

🔹 **Lưu log chi tiết**:
   - Thêm **node `n8n-nodes-base.set`** để ghi **log lỗi** vào Google Sheets hoặc một file JSON.

🔹 **Báo cáo định kỳ**:
   - Sử dụng **node `n8n-nodes-base.schedule`** để chạy workflow hàng ngày/tuần.

🔹 **Tối ưu FetchMedia.io**:
   - Nếu API có giới hạn, **lọc video dài hơn 5 phút** để giảm số lượng tải.
   - Sử dụng **node `n8n-nodes-base.filter`** để loại bỏ video quá ngắn.
:::

---

## 📌 **Kết luận**
Workflow này giúp các sếp **tự động hóa quá trình nghiên cứu thị trường video YouTube** một cách hiệu quả, **không cần viết code**. Bằng cách lọc, đánh giá và tải xuống video chất lượng cao, các sếp có thể **tiết kiệm thời gian** và **nâng cao hiệu quả phân tích**.

**🚀 Hãy áp dụng ngay và tự động hóa công việc của mình!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**📌 Lưu ý cuối cùng**:
- Nếu gặp lỗi **CORS** khi kết nối YouTube API, kiểm tra lại **credentials OAuth2**.
- Để **tăng tốc độ**, giảm số lượng query tìm kiếm hoặc tăng **ngưỡng lọc video**.