---
title: "🚀 Tự Động Theo Dõi và Trích Xuất Dữ Liệu Startup Gọi Vốn Seed Bằng RSS, GPT-4o-mini & Bright Data"
description: "Hướng dẫn xây dựng workflow n8n tự động bắt tin tức RSS, cào dữ liệu bài báo ẩn paywall bằng Bright Data, dùng AI trích xuất thông tin startup gọi vốn vòng Seed và lưu vào Excel."
slug: "tu-dong-theo-doi-trich-xuat-du-lieu-startup-seed-funding-n8n"
tags: [n8n, automation, no-code, lead-generation, ai-summarization, bright-data]
keywords: [n8n workflow, trích xuất dữ liệu startup, gọi vốn seed, bright data n8n, openai n8n, tự động hóa lead generation]
---

# 🚀 Tự Động Theo Dõi và Trích Xuất Dữ Liệu Startup Gọi Vốn Seed Bằng RSS, GPT-4o-mini & Bright Data

Các sếp làm trong lĩnh vực đầu tư, nghiên cứu thị trường hay Sales/BD (Business Development) chắc chắn hiểu được nỗi khổ khi phải ngày đêm "canh me" các trang tin tức công nghệ để tìm kiếm thông tin các startup vừa gọi vốn vòng Seed (vòng hạt giống). Việc copy-paste thủ công vừa tốn thời gian, dễ sót tin, lại cực kỳ mệt mỏi.

Giải pháp ở đây là gì? Hãy để hệ thống tự động hóa n8n lo! Bài viết này sẽ hướng dẫn các sếp triển khai một workflow cực xịn sò giúp tự động hóa 100% quy trình: Bắt tin tức qua RSS 👉 Cào nội dung sạch bằng Bright Data 👉 Xử lý thông tin bằng OpenAI (GPT-4o-mini) 👉 Lọc dữ liệu trùng lặp và lưu thẳng vào Microsoft Excel.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không sợ sập nguồn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 24/7:** Không bỏ lỡ bất kỳ thương vụ gọi vốn Seed nào ngay khi báo chí vừa đăng tải.
- **Cào dữ liệu chuyên sâu:** Vượt qua cả các bài báo bị chặn paywall hoặc sử dụng nội dung động nhờ tích hợp Bright Data.
- **AI thông minh:** Trích xuất chính xác thông tin doanh nghiệp, số tiền gọi vốn, thông tin nhà sáng lập vào cấu trúc chuẩn.
- **Làm sạch dữ liệu:** Tự động lọc bỏ các bản ghi trùng lặp dựa trên tên công ty được chuẩn hóa trước khi đẩy vào Excel.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
1. **Server n8n:** Đã cài đặt và đang hoạt động.
2. **OpenAI API Key:** Để kết nối với node AI trích xuất dữ liệu (GPT-4o-mini).
3. **Bright Data Account:** API/Credentials để sử dụng dịch vụ cào dữ liệu web.
4. **Microsoft Graph API / Excel Credentials:** Để workflow có thể ghi dữ liệu tự động vào file Excel trên OneDrive/SharePoint.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ kho lưu trữ n8n (Link gốc: [n8n.io/workflows/6775](https://n8n.io/workflows/6775)) và thực hiện import trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 9 nodes chính được chia theo các tầng nhiệm vụ rõ ràng. Các sếp cần chú ý cấu hình kỹ các node sau:

- **`RSS Feed Trigger`**: 
  - Cấu hình URL của các trang tin tức công nghệ, khởi nghiệp uy tín (ví dụ: TechCrunch, VentureBeat,...) để bắt bài viết mới tự động.
- **`Refactor article link` & `Add article link` (Code Nodes)**: 
  - Các đoạn code JavaScript có sẵn giúp bóc tách và giải mã URL bài viết gốc từ các đường dẫn chuyển hướng (redirect links), đảm bảo không bị lỗi link hỏng.
- **`Get article Page` (Bright Data Node)**: 
  - Điền thông tin xác thực (Credentials) của Bright Data. Node này cực kỳ mạnh mẽ giúp cào trọn vẹn nội dung bài báo ngay cả khi trang web đó có bảo mật chống cào hoặc ẩn sau paywall.
- **`Markdown` (Markdown Node)**: 
  - Chuyển đổi dữ liệu thô vừa cào được thành định dạng Markdown gọn gàng, giúp AI dễ dàng đọc hiểu và xử lý thông tin ở bước tiếp theo.
- **`Message a model` (OpenAI Node)**: 
  - Kết nối OpenAI Credentials. Thiết lập prompt để yêu cầu AI đọc nội dung Markdown và trích xuất cấu trúc dữ liệu mong muốn: Tên công ty, số tiền gọi vốn, thông tin nhà sáng lập, lĩnh vực hoạt động,...
- **`Filter company data` (Code Node)**: 
  - Xử lý dữ liệu dạng lồng nhau (nested data), làm sạch tên công ty và loại bỏ các bản ghi bị trùng lặp (duplicates) trước khi lưu trữ.
- **`Add data into excel sheet` (HTTP Request Node)**: 
  - Sử dụng Microsoft Graph API để đẩy dữ liệu các startup đã được trích xuất vào bảng tính Excel một cách gọn gàng, chuyên nghiệp.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử với một bài báo mẫu để kiểm tra dữ liệu đầu ra ở từng node xem đã chính xác chưa.
- Sau khi mọi thứ mượt mà, gạt công tắc sang **Active** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa hơn nữa hệ thống này, các sếp có thể cân nhắc mở rộng:
1. **Tích hợp Thông báo:** Thêm node **Telegram** hoặc **Slack** ngay sau bước AI trích xuất để bắn thông tin nóng hổi về nhóm Sales/Founder ngay lập tức.
2. **Lưu trữ đa kênh:** Ngoài Excel, có thể đẩy dữ liệu song song vào **Google Sheets** hoặc CRM như **Notion** / **HubSpot** để tiện chăm sóc khách hàng.
3. **Báo cáo định kỳ:** Tạo thêm một nhánh chạy theo lịch trình (Schedule Trigger) vào cuối tuần để tổng hợp danh sách startup gọi vốn thành một báo cáo PDF gửi qua Email.

### 📌 Kết luận
Việc tự động hóa quy trình thu thập thông tin startup gọi vốn chưa bao giờ dễ dàng đến thế với n8n kết hợp AI và Bright Data. Hãy setup ngay hôm nay để tiết kiệm hàng chục giờ đồng hồ làm việc thủ công và nắm bắt cơ hội kinh doanh trước đối thủ! Chúc các sếp thao tác thành công!