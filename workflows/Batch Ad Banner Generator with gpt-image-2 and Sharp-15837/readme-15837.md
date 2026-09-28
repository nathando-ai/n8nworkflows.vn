---
title: "🚀 Tự Động Sáng Tạo Banner Quảng Cáo Batch với AI OpenAI & Sharp - Không Cần Code"
description: "Workflow tự động hóa hoàn toàn bằng n8n để tạo hàng loạt banner quảng cáo đa kích thước từ hình ảnh gốc, sử dụng AI OpenAI để chỉnh sửa và công cụ Sharp để xử lý ảnh. Giúp các sếp tiết kiệm thời gian lên tới 80% so với làm thủ công."
slug: "tieu-dong-sang-tao-banner-quang-cao-batch-voi-gpt-image-2"
tags: [n8n, automation, content-creation, ai-multimodal, google-drive, google-sheets]
keywords: [n8n workflow banner quảng cáo, tự động hóa tạo banner, AI chỉnh sửa ảnh, Sharp resize ảnh, Google Drive API]
---

# 🚀 **Tự Động Sáng Tạo Banner Quảng Cáo Batch với AI OpenAI & Sharp**

### **Giải pháp hoàn toàn tự động hóa cho các sếp quảng cáo**
Làm thủ công việc tạo hàng loạt banner quảng cáo với nhiều kích thước khác nhau là một công việc **mệt mỏi, tốn thời gian và dễ sai sót**. Mỗi khi cần cập nhật hình ảnh cho chiến dịch mới, các sếp phải:
- Tải xuống hình ảnh gốc từ Google Drive
- Chỉnh sửa từng ảnh theo hướng dẫn khác nhau
- Resize và crop theo nhiều kích thước khác nhau (300x250, 728x90, 970x250...)
- Upload lại lên Google Drive và cập nhật Google Sheets

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động hóa hoàn toàn** – Chỉ cần nhập dữ liệu vào Google Sheets, workflow sẽ chạy 24/7.
✅ **Chỉnh sửa ảnh thông minh** – Sử dụng AI OpenAI để chỉnh sửa hình ảnh theo prompt tự động.
✅ **Tạo nhiều kích thước banner** – Sử dụng công cụ Sharp để resize và crop chính xác.
✅ **Cập nhật kết quả tự động** – Kết quả được lưu vào Google Sheets và Google Drive một cách tự động.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên tới 80%** so với làm thủ công.
- **Chính xác 100%** – Không còn sai sót khi resize hoặc crop ảnh.
- **Hoạt động liên tục** – Workflow chạy tự động khi có dữ liệu mới trong Google Sheets.
- **Tích hợp hoàn hảo** – Kết quả được tự động lưu vào Google Drive và cập nhật Google Sheets.
- **Cá nhân hóa** – Mỗi banner được tạo theo prompt và kích thước riêng biệt.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive** (để lưu hình ảnh gốc và kết quả).
2. **Tài khoản Google Sheets** (để quản lý danh sách công việc và kết quả).
3. **API Key OpenAI** (để sử dụng OpenAI Edit Image).
4. **Folder trong Google Drive** (để lưu kết quả banner cuối cùng).
5. **Dữ liệu mẫu trong Google Sheets** (theo cấu trúc dưới đây).

---

### 📊 **Cấu trúc Google Sheets (cột bắt buộc)**
| Cột               | Mô tả                                                                 | Ví dụ                                                                 |
|--------------------|------------------------------------------------------------------------|-----------------------------------------------------------------------|
| `id`               | ID duy nhất cho công việc                                            | `campaign_001`                                                       |
| `status`           | Trạng thái: `pending`, `todo`, hoặc `new`                             | `pending`                                                             |
| `source_file_id`   | ID file Google Drive của hình ảnh gốc                                | `1AbCdEfGhIjKlMnOpQrStUvWxYz`                                        |
| `prompt`           | Prompt chung cho chiến dịch                                         | `"Banner quảng cáo cho sản phẩm mới"`                                |
| `headline`         | Văn bản chính (nếu có)                                              | `"Giảm giá 50% chỉ trong tuần này!"`                                 |
| `subheadline`      | Văn bản phụ (nếu có)                                                | `"Mua trước ngày 30/12 để được ưu đãi đặc biệt"`                     |
| `cta`              | Call-to-action (nếu có)                                              | `"Xem chi tiết ngay!"`                                                |
| `target_sizes`     | Danh sách kích thước banner (cách nhau bởi dấu phẩy)                  | `300x250,728x90,970x250`                                             |
| `output_folder_id` | ID folder Google Drive để lưu kết quả                               | `1AbCdEfGhIjKlMnOpQrStUvWxYz`                                        |
| `edit_instruction` | Prompt cụ thể cho OpenAI chỉnh sửa hình ảnh                          | `"Chỉnh sửa hình ảnh để phù hợp với banner quảng cáo, giữ nguyên màu sắc và logo"` |

**Cột kết quả tự động thêm:**
- `generated_at` (thời gian tạo)
- `output_links` (đường dẫn tải banner)
- `output_files` (danh sách file banner)
- `status` (cập nhật trạng thái hoàn thành)

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n.io](https://n8n.io/) và tạo một workflow mới.
2. Nhấp vào **Import** và chọn file JSON (hoặc copy/paste JSON từ [link gốc](https://n8n.io/workflows/15837)).
3. Hoặc tải file JSON từ [đây](https://github.com/n8n-io/workflows/raw/main/workflows/15837.json).

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Sau khi import, các sếp cần cấu hình các node quan trọng như sau:

##### **A. Cấu hình Google Sheets**
1. **Node "Google Sheets - Read Jobs"**:
   - Chọn **Credentials**: Tạo một OAuth 2.0 credential cho Google Sheets.
   - Chọn **Sheet Name**: Tên của sheet chứa dữ liệu (ví dụ: `Banner_Jobs`).
   - Chọn **Range**: Phần dữ liệu cần đọc (ví dụ: `A1:Z1000`).
   - **Lưu ý**: Chỉ đọc các hàng có `status = "pending"` hoặc `status = "todo"`.

2. **Node "Google Sheets - Update Result"**:
   - Chọn **Credentials**: Cùng credential Google Sheets như trên.
   - Chọn **Sheet Name**: Cùng sheet như trên.
   - **Operation**: Chọn `appendOrUpdate` để cập nhật kết quả.

##### **B. Cấu hình Google Drive**
1. **Node "Google Drive - Download Source Image"**:
   - Chọn **Credentials**: Tạo một OAuth 2.0 credential cho Google Drive.
   - **File ID**: Sử dụng `$json.source_file_id` từ Google Sheets.

2. **Node "Google Drive - Upload Banner"**:
   - Chọn **Credentials**: Cùng credential Google Drive như trên.
   - **Folder ID**: Sử dụng `$json.output_folder_id` từ Google Sheets.
   - **File Name**: Tự động tạo tên file theo định dạng `banner_${id}_${size}.png`.

##### **C. Cấu hình OpenAI**
1. **Node "Edit image"**:
   - Chọn **Credentials**: Tạo một credential cho OpenAI với API Key.
   - **Prompt**: Sử dụng `$json.edit_instruction` từ Google Sheets.
   - **Lưu ý**: Đảm bảo `$json.edit_instruction` được định nghĩa rõ ràng trong Google Sheets.

##### **D. Cấu hình Code Node (Sharp)**
1. **Node "Code - Build Banner Sizes With Sharp"**:
   - **Lưu ý**: Nếu tự host n8n, cần cài đặt `sharp` theo hướng dẫn dưới đây:
     ```bash
     NODE_FUNCTION_ALLOW_EXTERNAL=sharp
     npm install sharp
     ```
   - **Nếu dùng n8n Cloud**: Thay thế node này bằng một API xử lý ảnh bên ngoài (ví dụ: Cloudinary API).

##### **E. Cấu hình Node "Split In Batches"**
- **Batch Size**: Đặt số lượng hàng cần xử lý cùng một lúc (ví dụ: `5`).
- **Lưu ý**: Nếu có nhiều công việc, workflow sẽ tự động chia thành batch.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấp vào **Run Workflow** và chọn một hàng mẫu trong Google Sheets để kiểm tra.
   - Kiểm tra kết quả trong Google Drive và Google Sheets.

2. **Bật Active**:
   - Sau khi kiểm tra thành công, chuyển workflow sang trạng thái **Active**.
   - **Lưu ý**: Đảm bảo Google Sheets có dữ liệu mới với `status = "pending"` để workflow tự động chạy.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tích hợp Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram** để thông báo khi workflow hoàn thành.
   - Ví dụ: Gửi tin nhắn `"Banner đã tạo thành công: [link]"` khi kết quả được upload.

2. **Lưu log hoạt động**:
   - Thêm node **Code** để log hoạt động vào Google Sheets hoặc một file CSV.
   - Ví dụ: Log thời gian chạy, kích thước banner, và trạng thái lỗi.

3. **Gửi báo cáo định kỳ**:
   - Sử dụng node **Google Sheets** hoặc **Email** để gửi báo cáo tổng hợp hàng tuần.
   - Ví dụ: Báo cáo số lượng banner tạo, thời gian trung bình xử lý, và kích thước phổ biến.

4. **Tối ưu hóa prompt**:
   - Nếu kết quả chỉnh sửa ảnh không như mong đợi, hãy thử:
     - Cập nhật `$json.edit_instruction` trong Google Sheets.
     - Thử prompt ngắn gọn và rõ ràng hơn.

5. **Xử lý lỗi tự động**:
   - Thêm node **Code** để kiểm tra lỗi và cập nhật `status` thành `failed` nếu có vấn đề.
   - Ví dụ: Nếu OpenAI trả về lỗi, workflow sẽ tự động chuyển trạng thái sang `failed`.

---

### 📌 **Kết luận**
Workflow **Batch Ad Banner Generator** là giải pháp **hoàn toàn tự động hóa** để các sếp tiết kiệm thời gian và nâng cao hiệu quả quảng cáo. Bằng cách kết hợp **Google Sheets, Google Drive, OpenAI AI, và Sharp**, workflow này tự động:
✔ Tải xuống hình ảnh gốc
✔ Chỉnh sửa ảnh theo prompt
✔ Resize và crop theo nhiều kích thước khác nhau
✔ Upload kết quả và cập nhật Google Sheets

**Hành động ngay hôm nay!**
- **Import workflow** và bắt đầu tự động hóa banner quảng cáo của bạn.
- **Tối ưu hóa prompt** để đạt kết quả chỉnh sửa ảnh tốt nhất.
- **Tích hợp thêm Slack/Telegram** để theo dõi hoạt động một cách dễ dàng.

**Nếu có bất kỳ câu hỏi hoặc gặp vấn đề, hãy để lại comment bên dưới!** 🚀