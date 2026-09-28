---
title: "🚀 Tự động hóa gia hạn hợp đồng thuê nhà với AI Ollama, Supabase và Gmail"
description: "Hướng dẫn xây dựng quy trình tự động hoàn toàn việc tạo thư gia hạn hợp đồng, cập nhật cơ sở dữ liệu Supabase và gửi email qua Gmail bằng mô hình AI nội bộ Ollama."
slug: "tu-dong-hoa-gia-han-hop-dong-thue-nha-ollama-supabase-gmail"
tags: [n8n, automation, ai, ollama, supabase, gmail, document-automation]
keywords: [n8n workflow, gia hạn hợp đồng, ollama llm, supabase automation, gmail n8n, tự động hóa tài liệu]
---

# 🚀 Tự động hóa gia hạn hợp đồng thuê nhà với AI Ollama, Supabase và Gmail

Việc xử lý thủ tục gia hạn hợp đồng thuê nhà cho khách hàng thường ngốn rất nhiều thời gian: từ việc tra cứu thông tin khách hàng trong cơ sở dữ liệu, soạn thảo thư đề nghị gia hạn, lưu trữ file trên Google Drive cho đến việc gửi email thông báo. Nếu làm thủ công, các sếp rất dễ gặp sai sót về thông tin hợp đồng hoặc gửi chậm trễ.

Workflow này sẽ giúp các sếp giải quyết triệt để bài toán trên bằng cách tự động hóa 100% quy trình: Nhận yêu cầu từ Form, truy vấn dữ liệu từ Supabase, sử dụng AI nội bộ (Ollama) để soạn thảo thư đề nghị, lưu trữ trên Google Drive và tự động gửi email cho khách hàng qua Gmail.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện**: Từ lúc khách hàng điền form đến khi nhận được thư đề nghị gia hạn qua email mà không cần can thiệp thủ công.
- **Cá nhân hóa bằng AI**: Sử dụng mô hình `llama3.1` qua Ollama để tạo nội dung thư đề nghị và email chuyên nghiệp, đúng trọng tâm.
- **Đồng bộ dữ liệu chuẩn xác**: Tự động tra cứu và cập nhật thông tin khách hàng trên Supabase, quản lý file gọn gàng trên Google Drive.
- **Hoạt động 24/7**: Tiết kiệm hàng chục giờ làm việc thủ công mỗi tháng cho đội ngũ quản lý bất động sản hoặc chăm sóc khách hàng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Ollama**: Đã cài đặt Ollama (chạy cục bộ hoặc trên server) với mô hình `llama3.1:latest`.
- **Supabase Account**: Dự án Supabase có bảng quản lý thông tin khách hàng (`customer`).
- **Google Drive & Gmail API**: Tài khoản Google tích hợp kết nối OAuth2 để quản lý file và gửi email.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và dán trực tiếp vào n8n Editor (hoặc sử dụng tính năng import từ file).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chuẩn các node sau:

- **On form submission**: Node khởi chạy quy trình. Các sếp cấu hình các trường thông tin đầu vào (như ID khách hàng, thời gian gia hạn mới...) để thu thập dữ liệu từ người dùng.
- **Supabase-search_cust & Supabase_cust_info**: Kết nối tài khoản Supabase qua `supabaseApi`. Node `Supabase-search_cust` dùng để truy vấn thông tin khách hàng hiện tại dựa trên dữ liệu từ Form, trong khi `Supabase_cust_info` cập nhật lại trạng thái hợp đồng mới.
- **Ollama Chat Model & Basic LLM Chain (offerLetter, email)**: 
  - Cấu hình credentials cho Ollama (`ollamaApi`).
  - Chọn model `llama3.1:latest`.
  - Thiết lập Prompt trong các chuỗi LLM để AI hiểu cách soạn thư đề nghị gia hạn hợp đồng và nội dung email gửi khách hàng.
- **Google Drive (search, upload, delete_dup, get_file)**: Kết nối tài khoản Google Drive (`googleDriveOAuth2Api`). Cấu hình thư mục lưu trữ (`folderId`) để lưu trữ các file thư đề nghị được chuyển đổi từ định dạng văn bản.
- **Convert to File**: Chuyển đổi nội dung văn bản thư đề nghị thành file định dạng text hoặc PDF trước khi đẩy lên Google Drive.
- **If-check_dup & Edit Fields**: Xử lý logic kiểm tra file trùng lặp trên Google Drive và chuẩn hóa các biến trước khi gửi email.
- **Gmail**: Kết nối tài khoản Gmail qua `gmailOAuth2`. Cấu hình người nhận (lấy từ dữ liệu khách hàng), tiêu đề và đính kèm file thư đề nghị vừa tạo.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử điền dữ liệu mẫu vào Form để kiểm tra toàn bộ luồng chạy.
- Sau khi test thành công, bật công tắc **Active** góc trên cùng bên phải để đưa workflow vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo nội bộ**: Thêm node Telegram hoặc Slack ở cuối workflow để thông báo cho đội ngũ Sales/Admin ngay khi có khách hàng hoàn tất yêu cầu gia hạn.
- **Lưu trữ Log**: Ghi lại lịch sử gửi email và trạng thái gia hạn vào một bảng riêng trên Supabase để dễ dàng theo dõi, thống kê.
- **Chuyển đổi định dạng PDF**: Thay vì chỉ convert sang text thuần túy, các sếp có thể sử dụng các dịch vụ tạo PDF chuyên nghiệp để file thư đề nghị gửi khách hàng trông đẹp mắt và trang trọng hơn.

### 📌 Kết luận
Workflow tích hợp AI Ollama, Supabase và Gmail này là giải pháp hoàn hảo giúp tự động hóa toàn bộ quy trình chăm sóc và gia hạn hợp đồng thuê nhà. Hãy triển khai ngay hôm nay để tối ưu hóa vận hành và mang lại trải nghiệm chuyên nghiệp nhất cho khách hàng của các sếp!