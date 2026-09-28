---
title: "🚀 Tự động trích xuất kết quả tìm kiếm LinkedIn vào Google Sheet với SourceGeek"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy danh sách ứng viên/leads từ LinkedIn (Basic, Sales Navigator, Recruiter) và đồng bộ trực tiếp vào Google Sheet."
slug: "trich-xuat-linkedin-vao-google-sheet-sourcegeek"
tags: [n8n, automation, no-code, linkedin, lead-generation, sourcegeek, google-sheets]
keywords: [n8n workflow, tự động hóa linkedin, trích xuất leads linkedin, sourcegeek n8n, google sheets automation]
---

# 🚀 Tự động trích xuất kết quả tìm kiếm LinkedIn vào Google Sheet với SourceGeek

Việc thủ công copy từng profile ứng viên hoặc khách hàng tiềm năng từ các trang tìm kiếm của LinkedIn (Basic, Sales Navigator, Recruiter) rồi dán vào Google Sheet là một ác mộng tốn thời gian. Các nhà tuyển dụng và marketer thường xuyên phải đối mặt với hàng giờ đồng hồ làm việc lặp đi lặp lại chỉ để xây dựng danh sách outreach (tiếp cận).

Giải pháp là gì? Workflow n8n này sẽ tự động hóa 100% quy trình đó! Chỉ với một Form đầu vào chứa đường dẫn tìm kiếm LinkedIn, hệ thống sẽ tự động quét, xử lý ngầm, chuyển đổi dữ liệu và đồng bộ toàn bộ danh sách chất lượng cao thẳng vào Google Sheet của các sếp mà không cần một dòng code phức tạp nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh copy-paste thủ công hàng trăm profile từ LinkedIn.
- **Hỗ trợ đa nền tảng LinkedIn:** Tương thích hoàn hảo với tìm kiếm cơ bản (Basic), Sales Navigator và LinkedIn Recruiter.
- **Đồng bộ thời gian thực:** Dữ liệu tự động được định dạng chuẩn và đẩy thẳng vào Google Sheet ngay khi tiến trình hoàn tất.
- **Vận hành trơn tru 24/7:** Cơ chế chờ thông minh (`Wait` & `If`) giúp theo dõi tiến trình chạy ngầm mà không làm nghẽn hệ thống.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã thiết lập sẵn sàng (Cloud hoặc Self-hosted).
- **Tài khoản SourceGeek:** Dịch vụ SaaS tích hợp để trích xuất dữ liệu từ LinkedIn (`sourcegeekCredentialsApi`).
- **Google Sheets Credentials:** Tài khoản Google OAuth2 để kết nối và ghi dữ liệu vào bảng tính.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sao chép đoạn JSON của workflow (từ nguồn n8n.io/workflows/13647) và paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 12 nodes phối hợp nhịp nhàng. Các sếp cần chú ý cấu hình kỹ các điểm sau:
- **On form submission (`formTrigger`):** Tạo form giao diện để người dùng nhập URL tìm kiếm LinkedIn.
- **Switch:** Node này sẽ tự động phân loại URL đầu vào để quyết định dùng loại tìm kiếm nào:
  - *Basic Search:* Sử dụng node **Import contacts from basic search** (`sourcegeekCredentialsApi`).
  - *Sales Navigator:* Sử dụng node **Import contacts from sales navigator search** (`sourcegeekCredentialsApi`).
  - *Recruiter:* Sử dụng node **Import contacts from recruiter search** (`sourcegeekCredentialsApi`).
- **Get tool run ID & Wait nodes:** SourceGeek sẽ trả về một `Run ID` trong khi tiến trình tạo danh sách diễn ra ở chế độ nền. Node **Wait until job is completed** sẽ tạm dừng 5 giây và kiểm tra lại trạng thái qua node **If Job Run is Complete** cho đến khi xong.
- **Convert to array for insert (`code`):** Chuyển đổi dữ liệu thô thành mảng chuẩn trước khi đẩy đi.
- **Append row in sheet (`googleSheets`):** Chọn file Google Sheet đích và mapping các trường thông tin (Tên, Chức vụ, Công ty, Link Profile...) tương ứng với các cột trong bảng tính của các sếp.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng một URL tìm kiếm LinkedIn ngắn trên Form để kiểm tra luồng dữ liệu.
- Sau khi kiểm tra dữ liệu đã vào Google Sheet chính xác, gạt công tắc sang **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Kết nối thêm node Telegram hoặc Slack sau bước **Append row in sheet** để nhận thông báo ngay khi quét xong một danh sách leads/ứng viên khủng.
- **Lọc trùng lượp:** Thêm một bước xử lý JavaScript hoặc Google Sheets script để kiểm tra trùng lặp URL profile trước khi append, tránh việc lưu thừa dữ liệu.
- **Tự động hóa Outreach:** Kết hợp tiếp tục với các workflow gửi tin nhắn tự động nối tiếp (nếu nền tảng hỗ trợ) để tối ưu hóa phễu tuyển dụng/bán hàng.

### 📌 Kết luận
Việc khai thác dữ liệu từ LinkedIn chưa bao giờ dễ dàng và mượt mà đến thế khi kết hợp sức mạnh của n8n và SourceGeek. Hãy "lên đồ" ngay hôm nay để giải phóng đội ngũ khỏi những tác vụ thủ công nhàm chán!