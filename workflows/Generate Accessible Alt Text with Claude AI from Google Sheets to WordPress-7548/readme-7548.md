---
title: "🚀 Tự động tạo Alt Text chuẩn SEO cho WordPress bằng Claude AI và Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình phân tích hình ảnh bằng Claude AI, tạo Alt Text chuẩn SEO/Accessibility và cập nhật trực tiếp vào WordPress thông qua Google Sheets."
slug: "tu-dong-tao-alt-text-wordpress-claude-ai-google-sheets"
tags: [n8n, automation, wordpress, claude-ai, google-sheets, seo]
keywords: [n8n workflow, alt text wordpress, claude ai multimodal, tu dong hoa seo, google sheets to wordpress]
---

# 🚀 Tự động tạo Alt Text chuẩn SEO cho WordPress bằng Claude AI và Google Sheets

Các sếp sở hữu website WordPress chắc chắn hiểu rõ tầm quan trọng của Alt Text (văn bản thay thế) đối với SEO hình ảnh và tiêu chuẩn tiếp cận người khuyết tật (Accessibility). Tuy nhiên, việc ngồi viết tay Alt Text cho hàng trăm, hàng nghìn hình ảnh trong thư viện Media là một cơn ác mộng tốn cực kỳ nhiều thời gian.

Giải pháp là gì? Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ mạnh mẽ giúp tự động hóa 100% quy trình này: Đọc danh sách ảnh từ **Google Sheets**, sử dụng **Claude AI (Anthropic)** để phân tích và viết mô tả ảnh chuẩn xác, sau đó tự động cập nhật ngược lại vào **Google Sheets** và thư viện **WordPress** thông qua REST API.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh nhập thủ công alt text cho từng ảnh trên WordPress.
- **Tối ưu SEO & Accessibility:** AI tự động phân tích chi tiết hình ảnh và tạo mô tả ngắn gọn (dưới 125 ký tự) chuẩn quy chuẩn web quốc tế.
- **Xử lý hàng loạt mượt mà:** Cơ chế lặp qua từng batch giúp xử lý thư viện ảnh lớn mà không sợ tràn bộ nhớ hay lỗi timeout.
- **Tự động hóa toàn diện:** Đồng bộ trực tiếp từ Google Sheets lên WordPress Media Library và lưu vết kết quả ngay trong bảng tính.
:::

### 📦 Các Nodes chính trong Workflow
Workflow này sử dụng 10 nodes phối hợp nhịp nhàng:
1. **Chat Trigger / Send Sheets URL**: Điểm khởi đầu để kích hoạt quy trình.
2. **Get URLs** & **Get WP Key + website URL WITHOUT https://**: Lấy dữ liệu danh sách ảnh và thông tin xác thực từ Google Sheets.
3. **Get Base64 key**: Node code chuẩn bị chuỗi mã hóa xác thực cho WordPress REST API.
4. **Loop Over Items** (`splitInBatches`): Chia nhỏ danh sách hình ảnh để xử lý lần lượt.
5. **Analyze image** (`anthropic`): Trí tuệ nhân tạo Claude AI phân tích hình ảnh đa phương thức (Multimodal).
6. **If**: Kiểm tra điều kiện và xử lý lỗi (bỏ qua các định dạng media không được hỗ trợ).
7. **Update row in sheet**: Ghi kết quả Alt Text trả về vào Google Sheets.
8. **Update WP image alt** (`httpRequest`): Đẩy Alt Text mới cập nhật thẳng lên WordPress Media qua API.
9. **Fin**: Kết thúc quy trình.

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Anthropic (Claude AI)** kèm API Key.
- **Google Account** để sử dụng Google Sheets.
- **Website WordPress** có bật tính năng Application Passwords và cài đặt sẵn plugin **Export Media URLs**.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy mã JSON của workflow này.
- Mở n8n Editor, chọn **New Workflow** -> Bấm tổ hợp `Ctrl + V` (hoặc `Cmd + V`) để dán toàn bộ workflow vào màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình kỹ các thành phần sau để workflow chạy trơn tru:
- **Node `Analyze image` (Anthropic):** 
  - Chọn `anthropicApi` credentials và điền API Key của các sếp.
  - *Mẹo:* Prompt mặc định trong node đang là tiếng Pháp, các sếp có thể sửa lại thành tiếng Việt hoặc ngôn ngữ mong muốn và giới hạn độ dài (ví dụ: dưới 125 ký tự).
- **Các node Google Sheets (`Get URLs`, `Get WP Key...`, `Update row in sheet`):**
  - Kết nối tài khoản Google thông qua `googleSheetsOAuth2Api`.
  - Trỏ đúng tới file Google Sheets quản lý dữ liệu của các sếp (xem cấu trúc template bên dưới).
- **Node `Update WP image alt` (HTTP Request):**
  - Cấu hình phương thức gọi API tới endpoint của WordPress (`/wp-json/wp/v2/media/{ID}`).
  - Sử dụng thông tin xác thực (Base64 key) được tạo tự động từ node Code phía trước.

#### 3. Chuẩn bị Google Sheets Template 📊
Các sếp cần chuẩn bị 1 file Google Sheets gồm 2 Sheet chính:
- **Sheet 1 (`Export media`):** Chứa danh sách ảnh xuất từ WordPress với các cột:
  - `ID`: WordPress media ID.
  - `URL`: Đường dẫn trực tiếp tới hình ảnh.
  - `Alt text`: Cột trống để workflow tự điền kết quả AI.
- **Sheet 2 (`Infos client`):** Chứa thông tin đăng nhập WordPress:
  - `Admin Name`: Tên đăng nhập tài khoản WordPress quản trị.
  - `KEY`: Application Password được tạo từ WordPress.
  - `Domaine`: URL website của các sếp dạng `example.com` (tuyệt đối không có `https://` hay dấu `/` ở cuối).

*Cách tạo Application Password trên WordPress:*
1. Vào trang quản trị WordPress Admin -> **Users** (Người dùng) -> **Your Profile** (Hồ sơ của bạn).
2. Cuộn xuống mục **Application Passwords**.
3. Nhập tên định danh (Ví dụ: `n8n Automation`) rồi bấm **Add New Application Password**.
4. Copy ngay đoạn mã được sinh ra vì WordPress sẽ không hiển thị lại lần thứ hai.

#### 4. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (Test workflow) với 1-2 dòng dữ liệu đầu tiên để kiểm tra lỗi kết nối AI và WordPress.
- Sau khi thấy Alt Text được cập nhật thành công trên WordPress Media, các sếp bật công tắc **Active** để workflow chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node Telegram hoặc Slack vào cuối workflow để nhận báo cáo tổng kết số lượng hình ảnh đã được tối ưu Alt Text thành công mỗi ngày.
- **Tùy biến ngôn ngữ Prompt:** Nếu website của các sếp hướng tới độc giả toàn cầu, có thể yêu cầu Claude AI sinh Alt Text bằng tiếng Anh hoặc đa ngôn ngữ.
- **Mở rộng lưu log:** Lưu thêm thời gian (timestamp) cập nhật vào Google Sheets để dễ dàng kiểm tra lịch sử tối ưu SEO.

### 📌 Kết luận
Tự động hóa quy trình tạo Alt Text hình ảnh cho WordPress bằng Claude AI không chỉ giúp website của các sếp đạt điểm cao về SEO, tuân thủ tiêu chuẩn Accessibility mà còn giải phóng hàng chục giờ làm việc thủ công. Hãy triển khai ngay hôm nay để tối ưu hóa hiệu suất vận hành website nhé các sếp!