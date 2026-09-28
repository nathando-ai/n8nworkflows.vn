---
title: "🚀 [New York Times] Tự động hóa tìm kiếm bài báo với MCP Server"
description: "Tự động hóa tìm kiếm bài báo từ New York Times thông qua MCP Server, giúp AI agent truy cập dữ liệu một cách nhanh chóng và hiệu quả."
slug: "tu-dong-hoa-tim-kiem-bai-bao-new-york-times-voi-mcp-server"
tags: [n8n, automation, no-code, AI, RAG]
keywords: [n8n workflow, tự động hóa, AI agent, New York Times, MCP Server]
---

# 🚀 [New York Times] Tự động hóa tìm kiếm bài báo với MCP Server

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian và công sức trong việc tìm kiếm và xử lý thông tin từ New York Times.
- Tự động hóa quá trình truy cập dữ liệu, giúp AI agent hoạt động hiệu quả hơn.
- Dữ liệu được trả về theo cấu trúc gốc của API, đảm bảo tính nhất quán và chính xác.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản New York Times API với API Key.
- Trình cài đặt n8n đã được cấu hình và chạy ổn định.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **Article Search MCP Server**: Node này sẽ làm server endpoint cho AI agent. Các sếp cần cấu hình path là `article-search-mcp`.
- **Search Articles**: Node này sẽ thực hiện các yêu cầu HTTP đến API của New York Times. Các sếp cần cấu hình API Key trong phần credentials.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Thêm các node xử lý dữ liệu nếu cần thiết.
- Triển khai xử lý lỗi tùy chỉnh.
- Thêm các node ghi log hoặc giám sát để theo dõi hoạt động của workflow.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quá trình tìm kiếm và xử lý thông tin từ New York Times một cách hiệu quả, giúp AI agent hoạt động nhanh chóng và chính xác hơn. Hãy áp dụng ngay để tiết kiệm thời gian và công sức!