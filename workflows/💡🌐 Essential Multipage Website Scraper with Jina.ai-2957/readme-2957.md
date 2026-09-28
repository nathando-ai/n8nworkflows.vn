---
title: "💡🌐 Tự động hóa thu thập nội dung website đa trang với Jina.ai"
description: "Workflow n8n giúp tự động thu thập nội dung từ nhiều trang website, chuyển đổi sang định dạng Markdown và lưu vào Google Drive - giải pháp hoàn hảo cho SEO và quản lý nội dung"
slug: "tu-dong-hoa-thu-thap-noi-dung-website-da-trang-jina-ai"
tags: [n8n, automation, no-code, web-scraping, seo]
keywords: [n8n workflow, tự động hóa thu thập nội dung, web scraping, Jina.ai, Google Drive]
---

# 💡🌐 Tự động hóa thu thập nội dung website đa trang với Jina.ai

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động thu thập nội dung từ nhiều trang website một cách nhanh chóng và chính xác
- Chuyển đổi nội dung sang định dạng Markdown chuẩn SEO
- Lưu trữ nội dung đã thu thập vào Google Drive với cấu trúc tổ chức rõ ràng
- Tiết kiệm thời gian và công sức cho việc quản lý nội dung
- Tự động hóa quy trình thu thập dữ liệu liên tục mà không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Drive với quyền truy cập đầy đủ
- URL của sitemap website cần thu thập nội dung
- Kiến thức cơ bản về cách sử dụng n8n
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **Node "When clicking ‘Test workflow’"**: Đây là điểm khởi đầu của workflow. Khi các sếp nhấn "Test workflow" trong n8n Editor, quá trình thu thập nội dung sẽ bắt đầu.
- **Node "Loop Over Items"**: Cấu hình số lượng trang cần thu thập trong mỗi lần chạy workflow.
- **Node "Wait"**: Đặt thời gian chờ giữa các lần thu thập để tránh bị chặn bởi server.
- **Node "Limit"**: Giới hạn số lượng trang được xử lý trong mỗi lần chạy để tránh quá tải.
- **Node "Get List of Website URLs"**: Cấu hình URL của sitemap website cần thu thập nội dung.
- **Node "Convert to JSON"**: Chuyển đổi dữ liệu XML từ sitemap sang định dạng JSON.
- **Node "Create List of Website URLs"**: Tạo danh sách các URL từ dữ liệu JSON.
- **Node "Filter By Topics or Pages"**: Lọc các trang theo chủ đề hoặc tiêu chí cụ thể.
- **Node "Set Website URL"**: Thiết lập URL của trang cần thu thập nội dung.
- **Node "Jina.ai Web Scraper"**: Không cần cấu hình API key, sử dụng dịch vụ Jina.ai để thu thập nội dung trang web.
- **Node "Save Webpage Contents to Google Drive"**: Cấu hình tài khoản Google Drive và tên file để lưu nội dung thu thập được.
- **Node "Extract Title & Markdown Content"**: Sử dụng code để trích xuất tiêu đề và nội dung Markdown từ dữ liệu thu thập được.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi workflow hoàn thành.
- Lưu log các lần thu thập nội dung để theo dõi quá trình.
- Gửi báo cáo định kỳ về nội dung đã thu thập qua email.

### 📌 Kết luận
Workflow này cung cấp giải pháp tự động hóa hoàn hảo cho việc thu thập nội dung từ nhiều trang website, giúp tiết kiệm thời gian và công sức cho các sếp trong việc quản lý nội dung. Hãy áp dụng ngay để nâng cao hiệu quả làm việc!