---
title: "🚀 Tự động lấy danh sách video Douyin và chi tiết video đầu tiên với JustOneAPI trên n8n"
description: "Hướng dẫn chi tiết cách sử dụng n8n workflow để kết nối JustOneAPI, trích xuất danh sách video đã đăng của người dùng Douyin và lấy thông tin chi tiết video đầu tiên hoàn toàn tự động."
slug: "tu-dong-lay-video-douyin-va-chi-tiet-voi-justoneapi"
tags: [n8n, automation, douyin, justoneapi, market-research, api-integration]
keywords: [n8n workflow, douyin api, justoneapi, lay video douyin, tu dong hoa n8n, market research]
---

# 🚀 Tự động lấy danh sách video Douyin và chi tiết video đầu tiên với JustOneAPI

Các sếp đang làm nghiên cứu thị trường (Market Research), phân tích đối thủ hoặc xây dựng nội dung trên Douyin (TikTok Trung Quốc) chắc chắn đã từng đau đầu khi phải thủ công lướt tìm từng video, copy link và bóc tách số liệu. Việc này không chỉ tốn hàng giờ đồng hồ mà còn dễ bỏ sót các số liệu quan trọng.

Giải pháp là gì? Hãy để n8n lo! Workflow tự động hóa này sẽ giúp các sếp kết nối trực tiếp với **JustOneAPI**, tự động cào toàn bộ danh sách video đã xuất bản của một tài khoản Douyin bất kỳ và bóc tách sâu thông tin chi tiết của video đầu tiên chỉ trong vài giây. 100% không cần code phức tạp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần thủ công tìm kiếm và copy dữ liệu từ Douyin.
- **Tự động hóa dữ liệu chính xác:** Lấy danh sách video và phân tích chi tiết video mới nhất/đầu tiên một cách mượt mà.
- **Dễ dàng mở rộng:** Dữ liệu trả về dưới dạng JSON sạch, sẵn sàng đẩy vào Google Sheets, Notion hoặc cơ sở dữ liệu bất kỳ.
- **Vận hành liên tục:** Có thể kích hoạt thủ công khi cần hoặc kết hợp webhook để chạy tự động theo lịch trình.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống **n8n** đã sẵn sàng hoạt động.
- Tài khoản và API Key hợp lệ từ **JustOneAPI** (dùng để gọi dữ liệu Douyin).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này và dán trực tiếp vào n8n Editor của mình, hoặc import file JSON tải từ trang quản lý workflow.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp cần chú ý cấu hình các node sau:
- **Node `Prepare API and User Data` (kiểu Set):** Điền các tham số cấu hình API của JustOneAPI, bao gồm API Base URL và thông tin tài khoản/user ID Douyin cần quét.
- **Node `Fetch User Published Videos` & `Fetch First Video Details` (kiểu HTTP Request):** Kiểm tra lại các endpoint API, đảm bảo đã truyền đúng Header chứa API Key của JustOneAPI để không bị lỗi xác thực (401/403).
- **Node `Extract Video IDs from Data` (kiểu Code):** Node này chứa đoạn mã JavaScript ngắn để lọc ra danh sách ID video từ cục dữ liệu thô. Các sếp có thể tinh chỉnh đoạn code này nếu muốn lấy nhiều hơn 1 video đầu tiên.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** tại node `Start Workflow Execution` (manualTrigger) để chạy thử nghiệm (Test run) với dữ liệu mẫu.
- Kiểm tra kết quả ở các node `Output Final Video Data`. Nếu dữ liệu trả về chính xác, các sếp có thể bật công tắc **Active** để lưu lại cấu hình.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ tự động:** Nối thêm node **Google Sheets** hoặc **Notion** ở cuối workflow để tự động lưu danh sách video và thông tin chi tiết vào bảng tính phục vụ việc báo cáo.
- **Cảnh báo qua Telegram/Slack:** Thêm một node chatwork/Telegram để nhận thông báo ngay khi có video mới xuất bản từ kênh đối thủ.
- **Chạy định lịch:** Thay thế node `Manual Trigger` bằng `Schedule Trigger` để tự động quét kênh Douyin vào mỗi khung giờ cố định trong ngày.

### 📌 Kết luận
Workflow tích hợp JustOneAPI và Douyin này là một "vũ khí" cực kỳ lợi hại cho các nhà sáng tạo nội dung và Marketer muốn nghiên cứu thị trường Trung Quốc một cách bài bản. Hãy setup ngay hôm nay để tối ưu hóa hiệu suất công việc của các sếp nhé!