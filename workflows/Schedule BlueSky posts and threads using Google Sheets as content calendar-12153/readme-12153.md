---
title: "🚀 Tự Động Hóa Đăng Bài & Thread Trên BlueSky Từ Google Sheets (Không Cần Code)"
description: "Workflow tự động hóa đăng bài, thread và hình ảnh lên BlueSky từ Google Sheets với lịch trình tự động, hỗ trợ đa hình ảnh và quản lý thread. Giúp tiết kiệm thời gian lên tới 80% cho các sếp marketing và content creator."
slug: "tu-dong-hoa-dang-bai-blue-sky-googlesheets"
tags: [n8n, automation, social-media, blue-sky, google-sheets, no-code, ai-multimodal]
keywords: [tự động hóa blue sky, đăng bài tự động, lịch trình content calendar, google sheets blue sky, workflow n8n social media]
---

# 🚀 **Tự Động Hóa Đăng Bài & Thread Trên BlueSky Từ Google Sheets (Không Cần Code)**

### **📌 Nỗi Đau Của Các Sếp Marketing & Content Creator**
Các sếp đang phải:
- **Đăng bài thủ công** trên BlueSky mỗi ngày, mất thời gian và dễ quên lịch trình.
- **Quản lý thread phức tạp**, phải nhớ thứ tự và liên kết giữa các bài viết.
- **Không có lịch trình tự động**, dẫn đến việc đăng bài không đồng bộ hoặc trễ hạn.
- **Không tích hợp hình ảnh**, phải tải lên từng bài một, tốn thời gian và dễ lỗi.

**Workflow này giải quyết tất cả!** Hãy tự động hóa toàn bộ quy trình đăng bài, thread và hình ảnh từ Google Sheets lên BlueSky, chỉ với một lần cấu hình.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và độ ổn định cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên tới 80%** so với đăng bài thủ công.
- **Quản lý thread tự động**, đảm bảo thứ tự và liên kết giữa các bài viết.
- **Đăng bài theo lịch trình chính xác**, không bao giờ quên hoặc trễ hạn.
- **Tích hợp hình ảnh tự động**, tải lên và gắn vào bài viết một cách nhanh chóng.
- **Lưu lịch sử đăng bài**, theo dõi tất cả bài viết đã đăng và liên kết BlueSky.
- **Hoạt động liên tục 24/7**, không cần can thiệp của con người.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản BlueSky** và **App Password** (không phải mật khẩu chính).
   - [Hướng dẫn tạo App Password trên BlueSky](https://support.bsky.app/hc/en-us/articles/360051767351-How-to-create-an-app-password)
2. **Google Sheet** với cấu trúc như mẫu dưới đây (sẽ được giải thích chi tiết).
3. **API Key của Google Sheets** (để kết nối với n8n).
4. **Thời gian múi** (ví dụ: `Asia/Ho_Chi_Minh` cho Việt Nam).
5. **Dung lượng lưu trữ** trên VPS để lưu log và dữ liệu.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/12153) hoặc copy/paste JSON từ trang này vào **n8n Editor**.
- **Cách import**:
  1. Mở **n8n Editor** trên trang web hoặc VPS của bạn.
  2. Nhấn **Import Workflow** (icon hình mũi tên vòng tròn).
  3. Chọn file JSON hoặc dán JSON từ trang này.
  4. Nhấn **Import**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **16 node** và cần cấu hình cẩn thận. Dưới đây là hướng dẫn chi tiết:

##### **🔹 Bước 1: Cấu Hình Credentials (Node "Configuration")**
- Mở node **"Configuration"** (node đầu tiên, màu xanh lá).
- Điền thông tin sau:
  - **BlueSky Handle**: Ví dụ `steve.bsky.social` (đây là tên tài khoản của bạn trên BlueSky).
  - **App Password**: App Password đã tạo trên BlueSky (không phải mật khẩu chính).
  - **Timezone**: Chọn múi giờ phù hợp với bạn (ví dụ: `Asia/Ho_Chi_Minh` cho Việt Nam).
    - [Tìm kiếm múi giờ](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones).

##### **🔹 Bước 2: Kết Nối Google Sheets**
- Mở node **"Get row(s) in sheet"** (node thứ 2).
- Chọn **credentials** là `googleSheetsOAuth2Api`.
- Nếu chưa kết nối tài khoản Google, nhấn **Add New** và đăng nhập tài khoản Google.
- Chọn **Sheet ID** và **Sheet Name** từ Google Sheet mẫu (sẽ được giải thích sau).

##### **🔹 Bước 3: Chuẩn Bị Google Sheet**
- **Tải mẫu Google Sheet** từ [đây](https://docs.google.com/spreadsheets/d/1Mg04gK1K5DBtJHrWw3ePRFc_JjkxwAp0deGjapVl2q0/edit?usp=sharing).
- **Cấu trúc cột bắt buộc**:
  | Cột          | Mô Tả                                                                 | Ví Dụ                          |
  |---------------|------------------------------------------------------------------------|--------------------------------|
  | **Content**   | Nội dung bài viết.                                                     | "Hôm nay là ngày tốt để học n8n!" |
  | **Thread ID** | ID nhóm cho thread (cần duy nhất, ngay cả bài viết đơn lẻ).           | "Thread-001"                    |
  | **Sequence**  | Thứ tự trong thread (bắt buộc nhập `1` cho bài viết đơn lẻ).          | `1`                             |
  | **Image URL** | Link hình ảnh (nếu có). Cần kết thúc bằng `.png` hoặc `.jpg`.         | `https://example.com/image.jpg` |
  | **Scheduled Time** | Thời gian đăng (định dạng `YYYY-MM-DD HH:mm`). Cột này **phải** là **Plain Text**. | `2024-12-25 14:30`          |
  | **Status**    | Trạng thái: `"Ready"` (để đăng) hoặc `"Posted"` (đã đăng).           | `Ready`                         |
  | **Posted At** | Thời gian đăng (sẽ tự động cập nhật sau khi đăng).                     | (Trống ban đầu)                |
  | **Post Link** | Link bài đăng (sẽ tự động cập nhật sau khi đăng).                     | (Trống ban đầu)                |

- **Lưu ý quan trọng**:
  - Cột **Scheduled Time** **phải** là **Plain Text** (không là DateTime) để workflow kiểm tra thời gian chính xác.
  - Để test, thêm một dòng mới với `Status = "Ready"` và `Scheduled Time` là thời gian trong tương lai gần (ví dụ: `2024-01-01 00:00`).

##### **🔹 Bước 4: Cấu Hình Node "If" (Lọc Bài Đăng)**
- Node **"If"** sẽ kiểm tra xem `Status = "Ready"` và thời gian đã đến (`Scheduled Time <= Current Time`).
- Nếu điều kiện này đúng, workflow sẽ tiếp tục xử lý bài viết.

##### **🔹 Bước 5: Xử Lý Hình Ảnh (Node "HTTP Download Image" và "Upload Blob")**
- Nếu có **Image URL**, workflow sẽ:
  1. **Tải hình ảnh** từ URL xuống (node `HTTP Download Image`).
  2. **Tải hình ảnh lên BlueSky** để lấy **Blob Link** (node `Upload Blob`).
  3. **Gắn Blob Link** vào bài viết (node `Attach Image Blob`).

##### **🔹 Bước 6: Xây Dựng Payload (Node "Construct Payload")**
- Node này là **"Não Logic"** của workflow, thực hiện:
  - **Kết hợp text và hình ảnh** (nếu có).
  - **Liên kết thread**: Nếu `Sequence > 1`, nó sẽ tìm bài viết trước đó trong thread và trả lời nó.
  - **Reset memory** cho thread mới.

##### **🔹 Bước 7: Đăng Bài (Node "Create Post")**
- Gọi API BlueSky để tạo bài viết hoặc trả lời bài viết (nếu là phần tiếp theo của thread).

##### **🔹 Bước 8: Cập Nhật Trạng Thái (Node "Update Thread State" và "Update row in sheet")**
- Sau khi đăng thành công, workflow sẽ:
  - Cập nhật **Post ID** vào memory (để bài viết tiếp theo trong thread biết liên kết).
  - Cập nhật **Status = "Posted"** và **Post Link** trong Google Sheet.

---

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  1. Chọn một dòng trong Google Sheet với `Status = "Ready"` và `Scheduled Time` là thời gian trong quá khứ (ví dụ: `2024-01-01 00:00`).
  2. Nhấn **Run Workflow** để kiểm tra.
  3. Kiểm tra BlueSky và Google Sheet để xác nhận bài viết đã đăng và trạng thái đã cập nhật.
- **Bật Active**:
  - Sau khi test thành công, chuyển workflow sang **Active**.
  - Workflow sẽ chạy **mỗi giờ** (hoặc thời gian bạn cấu hình trong node `Schedule Trigger`) để kiểm tra và đăng bài.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram** sau node **"Create Post"** để thông báo khi bài viết đăng thành công.
   - Cấu hình node **HTTP Request** để gửi tin nhắn thông báo.

2. **Lưu Log Dữ Liệu**:
   - Thêm node **Set** hoặc **Code** để lưu log các bài viết đã đăng vào một sheet khác hoặc cơ sở dữ liệu.
   - Ví dụ: Lưu `Post ID`, `Thread ID`, `Scheduled Time`, và `Status` vào một sheet mới.

3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng node **Schedule Trigger** để chạy một workflow khác mỗi tuần/month để tổng hợp thống kê số bài đăng, engagement, và gửi báo cáo qua email.
   - Cấu hình node **Email** (ví dụ: Gmail) để gửi báo cáo tự động.

4. **Quản Lý Nhiều Thread**:
   - Nếu bạn quản lý nhiều thread, bạn có thể chia sheet thành nhiều tab (ví dụ: `Thread-1`, `Thread-2`) và cấu hình node `Get row(s) in sheet` để lấy dữ liệu từ tab cụ thể.

5. **Sử Dụng AI Tạo Nội Dung**:
   - Kết hợp với node **LLM** (ví dụ: Mistral, Llama) để tự động tạo nội dung bài viết từ một prompt hoặc từ khóa.
   - Ví dụ: Nếu cột `Content` trống, node **Code** hoặc **LLM** sẽ tự động tạo nội dung dựa trên `Thread ID`.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp marketing và content creator muốn tự động hóa toàn bộ quy trình đăng bài trên BlueSky. Bằng cách kết hợp **Google Sheets** làm lịch trình và **n8n**, bạn có thể:
✅ **Tiết kiệm thời gian** lên tới 80%.
✅ **Quản lý thread một cách chuyên nghiệp**.
✅ **Đăng bài theo lịch trình chính xác**.
✅ **Tích hợp hình ảnh tự động**.
✅ **Hoạt động liên tục 24/7**.

**Hãy thử ngay!** Import workflow, cấu hình theo hướng dẫn, và bắt đầu tự động hóa content của bạn từ hôm nay.

---
**🚀 Cần hỗ trợ thêm?**
- Trả lời câu hỏi trên [Community n8n](https://community.n8n.io/).
- Liên hệ với tác giả Soumya Sahu qua [GitHub](https://github.com/soumyasahu).