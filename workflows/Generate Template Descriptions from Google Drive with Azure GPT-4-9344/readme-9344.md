---
title: "🚀 Tự động tạo mô tả template n8n từ Google Drive bằng Azure GPT-4"
description: "Hướng dẫn xây dựng workflow n8n tự động quét file JSON trên Google Drive, phân tích bằng AI Agent (Azure OpenAI GPT-4o) để sinh mô tả chuẩn SEO, lưu vào Google Sheets và gửi báo cáo qua Gmail."
slug: "tu-dong-tao-mo-ta-template-n8n-google-drive-azure-gpt-4"
tags: [n8n, automation, no-code, AI Agent, Google Drive, Azure OpenAI, Google Sheets]
keywords: [n8n workflow, tự động hóa n8n, Azure OpenAI GPT-4, Google Drive automation, AI content generation, LangChain n8n]
---

# 🚀 Tự động tạo mô tả template n8n từ Google Drive bằng Azure GPT-4

Các sếp làm nội dung, phát triển sản phẩm hoặc quản lý kho template n8n chắc chắn hiểu cảm giác mệt mỏi khi phải viết mô tả chi tiết, cấu trúc chuẩn Markdown, định dạng HTML cho từng workflow thủ công. Việc này vừa tốn thời gian, vừa dễ thiếu sót các thông tin cốt lõi như tính năng, lợi ích hay hướng dẫn cấu hình.

Workflow n8n tuyệt vời được thiết kế bởi chuyên gia **Rahul Joshi** này sẽ giúp các sếp giải quyết triệt để bài toán trên. Hệ thống sẽ tự động quét các file JSON workflow trong Google Drive, sử dụng sức mạnh của **AI Agent kết hợp Azure OpenAI (GPT-4o)** và **LangChain** để phân tích, tự động sinh tiêu đề cùng mô tả chuẩn chỉnh, sau đó lưu kết quả vào Google Sheets và gửi email thông báo qua Gmail. Tất cả diễn ra tự động 100% không cần đụng tay!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% quy trình viết content**: Biến các file code JSON khô khan thành bài mô tả template chuyên nghiệp, hấp dẫn.
- **AI thông minh chuẩn ngữ cảnh**: Sử dụng Azure OpenAI GPT-4o kết hợp bộ nhớ ngắn hạn (LangChain Memory) giúp hiểu sâu cấu trúc workflow.
- **Đồng bộ đa kênh liền mạch**: Tự động lưu trữ cơ sở dữ liệu trên Google Sheets để dễ quản lý và gửi email tổng hợp qua Gmail ngay lập tức.
- **Tiết kiệm 90% thời gian**: Thay vì mất hàng giờ viết documentation cho mỗi template, hệ thống hoàn thành chỉ trong vài giây.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt sẵn (Self-hosted hoặc n8n Cloud).
- **Google Drive Account**: Tài khoản chứa thư mục các file JSON workflow.
- **Azure OpenAI API**: Tài khoản và API Key truy cập mô hình GPT-4o.
- **Google Sheets**: File Google Sheets để lưu log kết quả.
- **Gmail Account**: Tài khoản gửi email báo cáo (hoặc Gmail OAuth2 credentials).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này hoặc tải file trực tiếp từ nguồn, sau đó dán vào giao diện n8n Editor (nhấn `Ctrl + V` hoặc `Cmd + V` trong vùng làm việc của n8n).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà không gặp lỗi "lực bất tòng tâm", các sếp cần cấu hình kỹ các node sau:

- **Search files and folders (Google Drive)**: Kết nối tài khoản thông qua `googleDriveOAuth2Api`. Thay thế ID thư mục mẫu bằng ID thư mục Google Drive thực tế của các sếp chứa các file JSON workflow.
- **Download file (Google Drive)**: Đảm bảo phân quyền tài khoản cho phép đọc/tải file từ thư mục đã chọn.
- **AI Agent & Connect to Azure OpenAI GPT Model**: 
  - Kết nối credential `azureOpenAiApi`.
  - Kiểm tra và đảm bảo tên model được cấu hình chính xác là `gpt-4o` (hoặc model tương đương trên Azure của các sếp).
  - Node `AI Agent` sử dụng System Prompt để định hình cách AI trích xuất thông tin, các sếp có thể tinh chỉnh prompt này nếu muốn thay đổi phong cách hành văn của bài mô tả.
- **Store AI Context (LangChain Memory)**: Giữ kích thước cửa sổ bộ nhớ (window size) ở mức nhỏ (khoảng 7–10) để tối ưu hiệu suất và tránh ngốn RAM.
- **Save To Google Sheets (Google Sheets)**: Kết nối `googleSheetsOAuth2Api`, trỏ tới file Google Sheet và Sheet Name nơi các sếp muốn lưu tiêu đề cùng mô tả template.
- **Send Email With Description (Gmail)**: Kết nối tài khoản Gmail thông qua `gmailOAuth2` để hệ thống tự động gửi email chứa nội dung HTML đã được định dạng đẹp mắt.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** tại node `When clicking ‘Execute workflow’` để test chạy thử với dữ liệu thực tế.
- Kiểm tra kết quả trên Google Sheets và hộp thư Gmail xem đã nhận được đúng định dạng chưa.
- Sau khi test thành công, gạt công tắc sang **Active** để bật chế độ chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo**: Thay vì chỉ gửi Gmail, các sếp có thể gắn thêm node Telegram hoặc Slack để nhận thông báo ngay lập tức vào nhóm chat khi có template mới được phân tích xong.
- **Tự động hóa kích hoạt**: Thay thế node `When clicking ‘Execute workflow’` bằng node `Schedule Trigger` (chạy định kỳ hàng ngày/hàng tuần) hoặc `Webhook` (kích hoạt ngay khi có file mới được tải lên Google Drive).
- **Lưu trữ backup**: Tận dụng dữ liệu trên Google Sheets để tự động đẩy lên hệ thống Notion hoặc CMS nội bộ làm thư viện template cho team.

### 📌 Kết luận
Workflow "Generate Template Descriptions from Google Drive with Azure GPT-4" là một mảnh ghép hoàn hảo cho các đội ngũ phát triển giải pháp n8n No-Code/Low-Code muốn chuyên nghiệp hóa quy trình quản lý và xuất bản tài liệu. Hãy cài đặt ngay lên hệ thống của các sếp để tối ưu hóa năng suất làm việc từ hôm nay!