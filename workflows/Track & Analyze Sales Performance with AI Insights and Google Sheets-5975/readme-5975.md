---
title: "🚀 Theo dõi & Phân tích hiệu suất bán hàng với AI và Google Sheets"
description: "Tự động hóa hoàn toàn quy trình theo dõi hiệu suất nhân viên bán hàng, phân tích dữ liệu bằng AI và lưu trữ kết quả vào Google Sheets - không cần viết code."
slug: "theo-doi-phan-tich-hieu-suat-ban-hang-ai-google-sheets"
tags: [n8n, automation, no-code, ai, google-sheets]
keywords: [n8n workflow, tự động hóa, phân tích bán hàng, ai, google sheets]
---

# 🚀 Theo dõi & Phân tích hiệu suất bán hàng với AI và Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động thu thập và phân tích dữ liệu hiệu suất bán hàng
- Chính xác: Sử dụng AI để trích xuất thông tin chính xác từ các nguồn dữ liệu phức tạp
- Cá nhân hóa: Phân tích hiệu suất từng nhân viên bán hàng một cách chi tiết
- Hoạt động liên tục: Theo dõi hiệu suất 24/7 mà không cần can thiệp thủ công
- Tích hợp dễ dàng: Lưu trữ dữ liệu vào Google Sheets để tạo báo cáo và dashboard
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI API (để sử dụng mô hình AI phân tích)
- Tài khoản Google Sheets API (để lưu trữ dữ liệu)
- Tài khoản Bright Data MCP (để thu thập dữ liệu từ các trang web)
- URL nguồn dữ liệu hiệu suất bán hàng của bạn
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang workflow gốc: [https://n8n.io/workflows/5975](https://n8n.io/workflows/5975)
2. Nhấn nút "Download" để tải file JSON workflow
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

**Node ⚡ Start Scraping (Manual Trigger):**
- Không cần cấu hình gì, chỉ cần nhấn "Execute Node" để bắt đầu workflow

**Node 🔗 Set MCP Source URL:**
- Thay đổi giá trị của biến `url` thành URL nguồn dữ liệu hiệu suất bán hàng của bạn
- Ví dụ: `https://your-sales-performance-dashboard.com`

**Node 🤖 Analyze Sales Rep Performance:**
- Không cần cấu hình gì, node này sử dụng AI để phân tích dữ liệu

**Node 🧠 AI Brain (OpenAI):**
- Cấu hình credentials OpenAI API
- Đảm bảo bạn đã chọn mô hình phù hợp (gpt-4.1-mini hoặc phiên bản mới nhất)

**Node 🌐 Bright Data MCP Tool:**
- Cấu hình credentials Bright Data MCP API
- Đảm bảo bạn đã chọn operation "executeTool"

**Node 🧩 Split JSON to Individual Records:**
- Không cần cấu hình gì, node này sẽ tự động chia dữ liệu thành các bản ghi riêng biệt

**Node 📊 Store Rep Performance (Google Sheets):**
- Cấu hình credentials Google Sheets API
- Chỉ định Spreadsheet ID và Sheet Name nơi bạn muốn lưu trữ dữ liệu
- Đảm bảo bạn đã chọn operation "append"

#### 3. Kích hoạt ⚡️
1. Nhấn "Execute Workflow" để chạy thử với dữ liệu mẫu
2. Kiểm tra kết quả trong Google Sheets của bạn
3. Nếu mọi thứ hoạt động tốt, nhấn "Activate" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
- Thiết lập lịch chạy tự động hàng ngày để cập nhật dữ liệu mới nhất
- Kết hợp với Slack/Teams để nhận thông báo khi có nhân viên bán hàng cần được đào tạo
- Thêm node để gửi email báo cáo hàng tuần cho quản lý
- Tích hợp với các công cụ dashboard như Google Data Studio để trực quan hóa dữ liệu
- Sử dụng workflow này như một phần của hệ thống báo cáo hiệu suất bán hàng toàn diện

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình theo dõi và phân tích hiệu suất bán hàng, từ việc thu thập dữ liệu đến lưu trữ và báo cáo. Với sự trợ giúp của AI và Bright Data, bạn có thể nhận được thông tin chính xác và chi tiết về hiệu suất của từng nhân viên bán hàng, giúp bạn đưa ra quyết định quản lý tốt hơn và cải thiện hiệu suất bán hàng của đội ngũ.