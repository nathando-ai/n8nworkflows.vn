---
title: "📸 **Tự Động Hóa Xếp Loại Ảnh Sự Kiện từ Khách Tham Dự bằng AI Gemma, Google Drive & Sheets – Giảm Thời Gian Làm Việc 90%!**"
description: "Workflow tự động hóa nhận ảnh từ khách tham dự sự kiện, phân loại tự động bằng AI Gemma (Google), lưu trữ trên Google Drive và ghi chép kết quả vào Google Sheets. Giúp các sếp tiết kiệm thời gian, tối ưu hóa quản lý nội dung và chia sẻ ảnh dễ dàng cho cộng đồng."
slug: "tieu-dong-hoa-xep-loai-anh-sukien-bang-ai-gemma"
tags: [n8n, automation, ai-automation, google-drive, google-sheets, featherless-ai, no-code]
keywords: [tự động hóa xếp loại ảnh sự kiện, ai phân loại ảnh, gemma ai n8n, lưu ảnh google drive, google sheets tự động, tự động hóa sự kiện]
---

# 🚀 **Tự Động Hóa Xếp Loại Ảnh Sự Kiện với AI Gemma, Google Drive & Sheets**

### **Giải pháp hoàn hảo cho các sếp quản lý sự kiện, marketing hoặc cộng đồng muốn:**
- **Tiết kiệm 90% thời gian** trong việc thu thập, phân loại và chia sẻ ảnh từ khách tham dự.
- **Tự động hóa hoàn toàn** quá trình nhận ảnh, phân loại bằng AI và lưu trữ kết quả.
- **Cung cấp bảng dữ liệu sẵn sàng** để chia sẻ trên mạng xã hội hoặc nội bộ, giúp cộng đồng dễ dàng tìm kiếm và chia sẻ kỷ niệm.
- **Không cần viết code** – chỉ cần cấu hình và chạy ngay!

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải thủ công thu thập, xếp loại và ghi chép ảnh từ hàng trăm khách tham dự.
- **Chính xác cao**: AI Gemma (Google) phân loại ảnh với độ chính xác cao, giảm sai sót của con người.
- **Dữ liệu sẵn sàng chia sẻ**: Tất cả ảnh và thông tin được lưu vào Google Sheets, dễ dàng chia sẻ với cộng đồng hoặc đội ngũ marketing.
- **Hoạt động liên tục 24/7**: Workflow tự động chạy ngay khi khách tham dự upload ảnh, không cần can thiệp thủ công.
- **Tối ưu chi phí**: Sử dụng **Featherless.ai** với mô hình **unlimited token**, tránh chi phí bất ngờ từ API.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Featherless.ai** (dùng để gọi API AI Gemma):
   - Đăng ký tại: [Featherless.ai](https://featherless.ai/register?referrer=HJUUTA6M) (mã giới thiệu: **HJUUTA6M**).
   - Chọn **Gemma 2B** (mô hình multimodal) và mua gói **unlimited token** (từ $10/tháng).
   - **Lưu ý**: Sau khi đăng ký, tạo **API Key** trong tài khoản và lưu lại.

2. **Tài khoản Google Drive & Google Sheets**:
   - Tạo một **Google Drive** để lưu ảnh (hoặc sử dụng Drive đã có).
   - Tạo một **Google Sheet** để ghi chép kết quả phân loại (mẫu tham khảo: [Google Sheet mẫu](https://docs.google.com/spreadsheets/d/1TpXQyhUq6tB8MLJ3maeWwswjut9wERZ8pSk_3kKhc58/edit?usp=sharing)).

3. **Cài đặt n8n Self-hosted** (không dùng phiên bản miễn phí trên cloud):
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

4. **Thiết bị chia sẻ form upload ảnh**:
   - Link form sẽ được tạo tự động khi cấu hình **Form Trigger** trong n8n.
   - Khách tham dự có thể upload ảnh từ **máy tính hoặc điện thoại** (hoạt động tốt trên mobile).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [link gốc](https://n8n.io/workflows/6575) hoặc [file JSON](https://cdn.subworkflow.ai/n8n-templates/workflows/6575.json).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. Workflow sẽ xuất hiện trên canvas.

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở **n8n Editor** → Nhấn **Import** → Chọn **Paste JSON**.
2. Copy toàn bộ nội dung JSON từ [file này](https://cdn.subworkflow.ai/n8n-templates/workflows/6575.json) và dán vào.
3. Nhấn **Import**.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này gồm **13 node**, nhưng các bước quan trọng cần chú ý như sau:

#### **🔹 Node 1: On form submission (formTrigger)**
- **Mục đích**: Tạo form cho khách tham dự upload ảnh.
- **Cấu hình**:
  - Nhấn **Edit** → Thay đổi tiêu đề form (ví dụ: **"Upload Ảnh Sự Kiện [Tên Sự Kiện]"**).
  - Thêm trường **Name** (tên khách tham dự) và **Files** (chọn ảnh).
  - **Lưu ý**: Form hoạt động tốt trên mobile, nên kiểm tra trên điện thoại để đảm bảo UI thân thiện.

#### **🔹 Node 5: Classify Photo and Suggest Tags (httpRequest)**
- **Mục đích**: Gọi API Featherless.ai để phân loại ảnh bằng AI Gemma.
- **Cấu hình**:
  1. Nhấn **Edit** → Chọn **Credentials**:
     - Chọn **featherlessApi** (nếu chưa có, tạo mới trong **Credentials** → **Add Credential** → **HTTP Header Auth**).
     - Điền **API Key** từ Featherless.ai vào **Header Auth**.
  2. Thay đổi **Payload** (nội dung gửi cho API):
     ```json
     {
       "prompt": "Classify this image into one of these categories: [Event, Food, Group, Portrait, Landscape, Funny, Product, Nature]. Return only the category name in JSON format.",
       "image": "{{ $json.base64 }}",
       "model": "gemma-2b-it"
     }
     ```
     - Thay `{{ $json.base64 }}` bằng biến từ node **Convert Image to Base64** (node 12).
  3. **Lưu ý**:
     - Đảm bảo **model** là `gemma-2b-it` (mô hình multimodal của Google).
     - Nếu API trả về lỗi, kiểm tra **API Key** và **URL endpoint** của Featherless.

#### **🔹 Node 7: Upload file (googleDrive)**
- **Mục đích**: Lưu ảnh gốc vào Google Drive.
- **Cấu hình**:
  1. Nhấn **Edit** → Chọn **Credentials**:
     - Chọn **googleDriveOAuth2Api** (nếu chưa có, tạo mới trong **Credentials** → **Google Drive OAuth2**).
     - Đăng nhập Google và cấp quyền cho n8n.
  2. Thay đổi **Folder Path**:
     - Đặt vào thư mục cụ thể (ví dụ: `/Sự Kiện/[Tên Sự Kiện]/Ảnh Gốc`).

#### **🔹 Node 13: Append to Sheet (googleSheets)**
- **Mục đích**: Ghi kết quả phân loại vào Google Sheets.
- **Cấu hình**:
  1. Nhấn **Edit** → Chọn **Credentials**:
     - Chọn **googleSheetsOAuth2Api** (nếu chưa có, tạo mới trong **Credentials** → **Google Sheets OAuth2**).
     - Đăng nhập Google và cấp quyền cho n8n.
  2. Thay đổi **Sheet Name**:
     - Đặt tên sheet theo ý muốn (ví dụ: **"Danh sách ảnh sự kiện"**).
  3. **Cấu trúc dữ liệu**:
     - Workflow sẽ tự động ghi các cột: **Tên khách**, **Link ảnh Drive**, **Danh mục phân loại**, **Ảnh Base64** (nếu cần).
     - **Lưu ý**: Nếu sheet đã có dữ liệu, node này sẽ **append** (thêm mới) vào cuối.

#### **🔹 Node 9 & 10: Resize Image & Get Image Info (editImage)**
- **Mục đích**: Optimize ảnh để giảm thời gian xử lý AI.
- **Cấu hình**:
  - Node **Resize Image**:
    - Thay đổi **Width** và **Height** (ví dụ: `800x800`) để ảnh không quá lớn.
  - Node **Get Image Info**:
    - Kiểm tra kích thước ảnh sau khi resize (đảm bảo dưới 5MB để Featherless xử lý nhanh).

---
### **3. Kích hoạt ⚡️**
1. **Test run dữ liệu mẫu**:
   - Nhấn **Run Workflow** và upload một ảnh mẫu (ví dụ: ảnh từ điện thoại).
   - Kiểm tra:
     - Ảnh có được resize không?
     - AI có phân loại đúng không?
     - Ảnh có được lưu vào Google Drive và Google Sheets không?

2. **Bật Active workflow**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động khi khách upload ảnh.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Chia sẻ form với cộng đồng**:
   - Sau khi cấu hình xong, chia sẻ **link form** với khách tham dự qua email, Facebook Event, hoặc QR code.
   - Ví dụ: Tạo QR code từ link form và in trên poster sự kiện.

2. **Tự động chia sẻ kết quả trên Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** sau node **Append to Sheet** để thông báo khi có ảnh mới được phân loại.
   - Cấu hình:
     ```json
     {
       "text": "📸 Ảnh mới được phân loại: {{ $node["Append to Sheet"].json["category"] }} - {{ $node["Append to Sheet"].json["name"] }}"
     }
     ```

3. **Tạo báo cáo định kỳ**:
   - Sử dụng **Google Apps Script** hoặc **n8n + Google Sheets** để tự động tạo báo cáo thống kê (ví dụ: số ảnh theo danh mục).
   - Ví dụ: Báo cáo hàng tuần về số ảnh được upload và phân loại.

4. **Tối ưu hình ảnh cho mạng xã hội**:
   - Thêm node **Edit Image** để cắt ảnh theo kích thước chuẩn (ví dụ: 1080x1080px cho Instagram).
   - Sau đó, upload vào **Google Drive** với folder riêng cho "Ảnh chuẩn".

5. **Sử dụng AI để tự động tạo caption**:
   - Thay vì chỉ phân loại, có thể yêu cầu AI **tạo mô tả** cho ảnh (ví dụ: "Ảnh này mô tả một khoảnh khắc vui vẻ tại sự kiện [Tên Sự Kiện]").
   - Cập nhật payload API:
     ```json
     {
       "prompt": "Describe this image in 3 sentences and suggest a hashtag for social media.",
       "image": "{{ $json.base64 }}",
       "model": "gemma-2b-it"
     }
     ```

6. **Lưu log hoạt động**:
   - Thêm node **Set** trước node **Append to Sheet** để ghi thêm thông tin như **thời gian upload**, **IP khách**, hoặc **thành viên đã upload**.
   - Ví dụ:
     ```json
     {
       "timestamp": "{{ $node["On form submission"].json["$dateTimeNow"] }}",
       "ip": "{{ $node["On form submission"].json["$ip"] }}"
     }
     ```
:::

---
## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** để các sếp quản lý sự kiện, marketing hoặc cộng đồng **tự động hóa hoàn toàn** quá trình thu thập, phân loại và chia sẻ ảnh từ khách tham dự. Bằng cách kết hợp **AI Gemma (Google)**, **Google Drive** và **Google Sheets**, các sếp sẽ:
✅ **Tiết kiệm thời gian** lên đến 90% so với cách làm thủ công.
✅ **Tối ưu hóa quản lý nội dung** với dữ liệu sẵn sàng chia sẻ.
✅ **Giảm chi phí** với mô hình **unlimited token** của Featherless.ai.
✅ **Hoạt động liên tục** 24/7, không cần can thiệp thủ công.

### **Bước tiếp theo**
1. **Cài đặt n8n Self-hosted** trên VPS (đăng ký mã giảm giá **VPSN8N**).
2. **Import workflow** và cấu hình các credentials (Featherless, Google Drive, Google Sheets).
3. **Test run** với ảnh mẫu và **bật Active** để chạy tự động.
4. **Chia sẻ form** với khách tham dự và theo dõi kết quả trên Google Sheets!

**🚀 Hãy tự động hóa ngay hôm nay và dành thời gian cho những việc quan trọng hơn!** 🚀

---
### **Cần hỗ trợ?**
- **Trang web chính thức**: [n8n.io](https://n8n.io/)
- **Community**: [Discord n8n](https://discord.com/invite/XPKeKXeB7d)
- **Forum**: [Community n8n](https://community.n8n.io/)
- **Đăng ký Featherless.ai**: [Featherless.ai](https://featherless.ai/register?referrer=HJUUTA6M) (mã giới thiệu: **HJUUTA6M**)