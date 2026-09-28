---
title: "🚀 Tự động tạo CV chuẩn ATS bằng Perplexity AI và xuất file PDF với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình tối ưu CV theo Job Description (JD) sử dụng Perplexity AI, chuyển đổi HTML sang PDF và lưu trữ trực tiếp lên Google Drive."
slug: "tao-cv-chuan-ats-perplexity-ai-n8n"
tags: [n8n, automation, no-code, ai, perplexity, google-drive, pdf-generator]
keywords: [n8n workflow, tạo CV chuẩn ATS, Perplexity AI, tự động hóa n8n, html to pdf, google drive automation]
keywords: [n8n workflow, tạo CV chuẩn ATS, Perplexity AI, tự động hóa n8n, html to pdf, google drive automation]
---

# 🚀 Tự động tạo CV chuẩn ATS bằng Perplexity AI và xuất file PDF với n8n

Việc thủ công chỉnh sửa CV cho từng vị trí ứng tuyển (Job Description - JD) thường tốn rất nhiều thời gian và công sức của các sếp. Thêm vào đó, nếu CV không được tối ưu theo các hệ thống lọc tự động (ATS), cơ hội lọt vào vòng phỏng vấn sẽ giảm đi đáng kể. 

Workflow n8n này sẽ giải quyết triệt để bài toán đó bằng cách tự động hóa 100%: nhận thông tin ứng viên và JD từ biểu mẫu web, phân tích nội dung, sử dụng sức mạnh của **Perplexity AI** để viết lại CV chuẩn ATS, chuyển đổi thành định dạng HTML/PDF sạch sẽ, và lưu trữ trực tiếp lên Google Drive. Các sếp không cần phải code dòng nào cả!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian**: Không còn mất hàng giờ đồng hồ để căn chỉnh hay viết lại CV cho từng job mới.
- **Tối ưu ATS tuyệt đối**: AI tự động đưa các từ khóa quan trọng từ JD vào CV một cách tự nhiên, chân thực.
- **Định dạng chuẩn chuyên nghiệp**: Chuyển đổi mượt mà từ văn bản sang HTML và xuất ra file PDF sạch sẽ, một cột, dễ đọc cho nhà tuyển dụng.
- **Lưu trữ tự động**: File CV hoàn chỉnh được đẩy thẳng vào thư mục Google Drive đã chỉ định, sẵn sàng tải xuống bất cứ lúc nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản sau:
1. **Hệ thống n8n** (Self-hosted hoặc n8n Cloud).
2. **Perplexity AI API Key**: Để sử dụng mô hình `sonar-reasoning` viết lại CV.
3. **Google Drive Account**: Kết nối OAuth2 để lưu file PDF tự động.
4. **CustomJS API / Toolkit credentials** (nếu sử dụng node HTML to PDF tùy chỉnh).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn cung cấp (hoặc copy toàn bộ JSON).
- Vào giao diện n8n Editor, chọn **Add workflow** -> Nhấn vào dấu `...` ở góc trên bên phải -> **Import from File** hoặc **Paste Workflow**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow vận hành trơn tru, các sếp nhớ cấu hình kỹ các node trọng điểm sau:

- **Form Trigger**: Node này tạo một Web Form tại đường dẫn `resume-builder`. Sau khi kích hoạt, các sếp có thể truy cập link form để upload file PDF CV gốc và file PDF JD cần ứng tuyển.
- **Process one binary file1 & Extracting resume1**: Xử lý và trích xuất toàn bộ văn bản từ file PDF đầu vào của ứng viên và JD một cách tự động thông qua mã lệnh JavaScript.
- **Merge Resume + JD1**: Gom nhóm nội dung CV và JD thành một chuỗi dữ liệu duy nhất làm đầu vào cho AI.
- **Customize resume1 (Perplexity AI Node)**: 
  - Chọn model: `sonar-reasoning`.
  - Kết nối **Perplexity API Credential**. 
  - Node này sẽ ép AI tuân thủ cấu trúc HTML chuẩn (không màu mè, một cột, font Arial/sans-serif) để vượt qua các bộ lọc ATS khó tính.
- **HTML format1**: Node Code JavaScript có nhiệm vụ lọc bỏ các ký tự thừa (`\n`), lấy đoạn mã HTML tinh gọn nhất từ phản hồi của AI.
- **HTML to PDF**: Chuyển đổi mã HTML đã làm sạch thành file PDF bằng toolkit chuyên dụng (yêu cầu cấu hình credentials tương ứng).
- **Upload file (Google Drive Node)**: 
  - Kết nối tài khoản Google Drive OAuth2.
  - Chọn thư mục lưu trữ trên Google Drive (Mặc định trong workflow là folder `Resume` với ID: `1vzNpRjBe1ylcLmJ2TKl4TN40BAeri-HD`). Các sếp nhớ thay đổi ID này thành thư mục của riêng mình!

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách điền form qua đường dẫn `resume-builder`.
- Kiểm tra kết quả trên Google Drive xem file PDF đã xuất hiện chưa.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để hệ thống chính thức chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
Để workflow này trở thành "vũ khí tối thượng" tìm việc, các sếp có thể mở rộng thêm:
- **Tích hợp Telegram/Slack**: Gửi thông báo kèm file PDF trực tiếp về chat cá nhân ngay khi CV được tạo xong.
- **Lưu log vào Google Sheets**: Ghi lại tên công ty, vị trí ứng tuyển và thời gian tạo CV để tiện theo dõi quá trình rải đơn.
- **Tự động gửi Email**: Kết nối thêm node Gmail để tự động gửi CV vừa tạo đính kèm email ứng tuyển cho nhà tuyển dụng (cần cân nhắc kỹ nội dung trước khi gửi).

### 📌 Kết luận
Với workflow n8n tự động hóa tạo CV chuẩn ATS này, việc tối ưu hồ sơ cho hàng chục vị trí công việc khác nhau không còn là nỗi ác mộng. Hãy cài đặt ngay lên hệ thống n8n của các sếp và trải nghiệm sức mạnh của AI trong tuyển dụng!