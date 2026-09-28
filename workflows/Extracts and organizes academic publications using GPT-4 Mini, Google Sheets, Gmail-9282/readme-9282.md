---
title: "🚀 Tự động trích xuất và phân loại công trình nghiên cứu khoa học với AI, Google Sheets và Gmail"
description: "Hướng dẫn xây dựng workflow n8n tự động cào dữ liệu công trình nghiên cứu từ website giảng viên, phân loại thông minh bằng GPT-4 Mini, lưu trữ vào Google Sheets và gửi báo cáo qua Gmail."
slug: "tu-dong-trich-xuat-va-phan-loai-cong-trinh-nghien-cuu-n8n"
tags: [n8n, automation, no-code, openai, google-sheets, gmail, ai-extraction]
keywords: [n8n workflow, tự động hóa nghiên cứu khoa học, gpt-4 mini, cào dữ liệu website, google sheets automation]
---

# 🚀 Tự động trích xuất và phân loại công trình nghiên cứu khoa học với AI

Các nhà nghiên cứu, giảng viên đại học hay quản lý thư viện thường xuyên đối mặt với việc thủ công cập nhật hàng trăm bài báo, ấn phẩm, hội thảo khoa học từ trang cá nhân vào cơ sở dữ liệu. Việc này cực kỳ tốn thời gian và dễ sai sót. 

Được sáng tạo bởi Giáo sư Cheng Siong Chin (Newcastle University), workflow n8n này chính là giải pháp tự động hóa 100% không cần code giúp cào, cấu trúc hóa dữ liệu công trình nghiên cứu bằng AI (GPT-4 Mini), phân loại tự động, lưu trữ khoa học vào Google Sheets và gửi email thông báo kèm file CSV hoàn chỉnh cho các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Chỉ cần nhập URL trang profile, hệ thống tự lo phần còn lại từ cào web đến lưu trữ.
- **Phân loại thông minh bằng AI:** Sử dụng `OpenAI Chat Model` và `Generate Summary Report` để phân loại chính xác các ấn phẩm thành Tạp chí, Hội thảo, Sách, Bằng sáng chế,...
- **Đồng bộ đa tầng Google Sheets:** Tự động lưu vào Master Sheet tổng hợp và các Sheet chuyên biệt theo từng loại hình ấn phẩm.
- **Báo cáo tức thì:** Tổng hợp thống kê số lượng và gửi file CSV qua `Send Notification Email` (Gmail) ngay khi hoàn tất.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã chạy ổn định (Self-hosted hoặc Cloud).
- **Tài khoản OpenAI:** Cần có API Key và quyền sử dụng model `gpt-4.1-mini` hoặc tương đương.
- **Google Sheets:** Tài khoản Google kết nối OAuth2 để tạo và ghi dữ liệu vào các bảng tính.
- **Gmail:** Tài khoản Gmail cấu hình OAuth2 để gửi email báo cáo kết quả.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ thư viện n8n (hoặc copy toàn bộ JSON) và import trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần chú ý cấu hình các node cốt lõi sau:
- **On form submission:** Node kích hoạt chạy workflow thông qua giao diện form nhập URL trang web chứa danh sách công trình nghiên cứu.
- **Fetch website content (`httpRequest`):** Nhận URL từ form và tải mã nguồn HTML của trang profile học thuật.
- **Extract all publications from the page (`html`):** Thiết lập `operation: extractHtmlContent` để trích xuất vùng chứa danh sách công trình.
- **OpenAI Chat Model & Generate Summary Report:** Chọn credentials OpenAI, cấu hình model `gpt-4.1-mini`, thiết lập prompt yêu cầu AI bóc tách rõ ràng: Tiêu đề, Tác giả, Năm, Loại ấn phẩm, Nơi xuất bản, DOI, URL.
- **Switch:** Thiết lập quy tắc định tuyến (`Route by publication type`) để tách các bài báo thành các nhánh riêng biệt.
- **Save All to Master Sheet & Các node Append to... Sheet (`googleSheets`):** Chọn credentials Google Sheets OAuth2, trỏ tới file Google Sheet đích và chọn đúng Sheet Name cho từng loại (Journal, Conference, Book, Magazine, Patent, Other) với thao tác `append` hoặc `appendOrUpdate`.
- **Format as CSV Export & Send Notification Email (`gmail`):** Chuyển đổi dữ liệu thành file CSV qua node `convertToFile` và cấu hình tài khoản Gmail để gửi báo cáo tổng hợp.

#### 3. Kích hoạt ⚡️
- Chạy thử (`Test workflow`) với một URL mẫu để kiểm tra dữ liệu trả về từ AI và Google Sheets.
- Bật công tắc `Active` để đưa workflow vào trạng thái vận hành tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng thông báo:** Kết hợp thêm node Telegram hoặc Slack để bắn tin nhắn thông báo ngay vào nhóm nghiên cứu khi hoàn tất cào dữ liệu.
- **Tự động hóa theo lịch:** Thay thế hoặc bổ sung `formTrigger` bằng `Schedule Trigger` để tự động quét website của giảng viên hàng tháng/hàng quý nhằm cập nhật công trình mới nhất.
- **Lưu trữ Log lỗi:** Thêm node `Error Trigger` để bắt sự cố nếu website nguồn thay đổi cấu trúc HTML, giúp dễ dàng debug.

### 📌 Kết luận
Workflow này là trợ thủ đắc lực giúp các nhà khoa học, trường đại học và viện nghiên cứu tối ưu hóa việc quản lý và tổng hợp thành tựu học thuật mà không tốn một phút nhập liệu thủ công nào. Hãy import ngay vào n8n của các sếp và trải nghiệm sức mạnh của AI trong tự động hóa!