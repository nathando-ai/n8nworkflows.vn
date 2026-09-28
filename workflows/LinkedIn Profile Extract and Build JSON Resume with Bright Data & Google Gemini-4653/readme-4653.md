---
title: "🚀 Trích xuất thông tin LinkedIn và tạo CV JSON chuẩn cấu trúc tự động với Bright Data và Google Gemini"
description: "Tự động hóa hoàn toàn quy trình trích xuất dữ liệu hồ sơ LinkedIn, xử lý thông qua Bright Data và sử dụng AI Google Gemini để chuyển đổi thành CV dạng JSON chuyên nghiệp."
slug: "trich-xuat-linkedin-tao-cv-json-bright-data-gemini"
tags: [n8n, automation, hr, ai, google-gemini, bright-data, resume-extractor]
keywords: [n8n workflow, trích xuất linkedin, bright data, google gemini, tạo cv tự động, json resume, hr automation]
---

# 🚀 Tự động hóa trích xuất LinkedIn và tạo CV JSON với Bright Data & Google Gemini

Việc thủ công thu thập thông tin ứng viên từ LinkedIn, sao chép từng phần kinh nghiệm, kỹ năng và biên tập lại thành một bản CV chuẩn chỉnh ngốn rất nhiều thời gian của các HR, Headhunter hoặc nhà tuyển dụng. Quá trình này không chỉ chậm mà còn dễ bỏ sót thông tin quan trọng.

Workflow n8n này sẽ giải quyết triệt để vấn đề đó bằng cách kết hợp sức mạnh của **Bright Data** (công cụ thu thập dữ liệu web mạnh mẽ) và **Google Gemini AI** (mô hình ngôn ngữ lớn thông minh) để tự động hóa 100% quy trình: cào dữ liệu hồ sơ LinkedIn, trích xuất thông tin chi tiết, phân tích kỹ năng và xuất ra định dạng JSON Resume chuẩn hóa.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Biến một URL LinkedIn thô thành bộ dữ liệu JSON Resume có cấu trúc rõ ràng chỉ trong vài giây.
- **AI thông minh:** Sử dụng Google Gemini để làm sạch dữ liệu Markdown, trích xuất kỹ năng chuyên môn và chuẩn hóa kinh nghiệm làm việc.
- **Lưu trữ linh hoạt:** Tự động ghi file cấu trúc (JSON) xuống ổ cứng và hỗ trợ gửi thông báo qua Webhook tích hợp.
- **Tối ưu hóa quy trình HR:** Giúp đội ngũ tuyển dụng tiết kiệm hàng giờ đồng hồ sàng lọc và nhập liệu thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã sẵn sàng hoạt động (Cloud hoặc Self-hosted).
- **Tài khoản Bright Data:** Cần có API Key/Auth và cấu hình Zone name để thực hiện Web Request.
- **Google Gemini API Key:** Sử dụng cho các node LangChain LLM trong n8n (`googlePalmApi` credentials).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n hoặc copy trực tiếp và dán (Paste) vào màn hình n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node quan trọng sau đây để workflow chạy mượt mà:

- **Node `Set URL and Bright Data Zone`**: 
  - Điền URL của profile LinkedIn cần trích xuất vào biến cấu hình.
  - Cấu hình đúng tên Zone đã đăng ký trên Bright Data.
  - Điền Webhook notification URL (nếu muốn nhận thông báo kết quả).
- **Node `Perform Bright Data Web Request`**: 
  - Kiểm tra lại phần `httpHeaderAuth` credentials để đảm bảo kết nối thành công với API của Bright Data.
- **Các node Google Gemini (`Google Gemini Chat Model for Markdown to Textual`, `Google Gemini Chat Model for Skill Extractor`, `Google Gemini Chat Model`)**: 
  - Thêm API Key của Google Gemini vào `googlePalmApi` credentials.
- **Node `Write the structured content to disk` & `Write the structured skills content to disk`**: 
  - Kiểm tra đường dẫn thư mục lưu trữ file trên ổ cứng (disk) của hệ thống n8n để đảm bảo quyền ghi file (`readWriteFile`).

#### 3. Kích hoạt ⚡️
- Nhấn nút **‘Test workflow’** tại node kích hoạt thủ công (`When clicking ‘Test workflow’`) để chạy thử nghiệm với một profile LinkedIn mẫu.
- Kiểm tra kết quả trả về ở các node trung gian và file được ghi trên disk.
- Sau khi test thành công, bật nút **Active** để đưa workflow vào trạng thái vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thay vì chỉ ghi file lên disk, các sếp có thể kết nối thêm node Telegram hoặc Slack để gửi bản tóm tắt CV trực tiếp về nhóm tuyển dụng ngay khi xử lý xong.
- **Lưu vào Google Sheets / Airtable:** Thay thế hoặc bổ sung bước lưu file bằng việc đẩy dữ liệu JSON đã trích xuất vào Google Sheets để dễ dàng quản lý danh sách ứng viên.
- **Mở rộng hàng loạt (Batch Processing):** Kết hợp thêm node đọc danh sách URL từ file CSV hoặc Google Sheets để tự động cào hàng loạt hồ sơ LinkedIn cùng lúc.

### 📌 Kết luận
Workflow tích hợp Bright Data và Google Gemini này là trợ thủ đắc lực giúp tự động hóa khâu thu thập và xử lý hồ sơ ứng viên. Hãy áp dụng ngay để tối ưu hóa thời gian và nâng cao hiệu suất cho đội ngũ tuyển dụng của doanh nghiệp các sếp nhé!