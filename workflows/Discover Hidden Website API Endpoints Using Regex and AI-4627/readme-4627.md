---
title: "🚀 Khám phá API Endpoint ẩn trên Website bằng Regex và AI với n8n"
description: "Tự động hóa việc phân tích mã nguồn JavaScript để tìm kiếm các API endpoint ẩn trên website không có tài liệu công khai bằng AI và Regex."
slug: "kham-pha-api-endpoint-an-tren-website-regex-ai"
tags: [n8n, automation, ai, web-scraping, api-discovery, openrouter]
keywords: [n8n workflow, tìm api ẩn, trích xuất api endpoint, javascript analysis, ai agent, openrouter, regex automation]
---

# 🚀 Khám phá API Endpoint ẩn trên Website bằng Regex và AI

Các ứng dụng web hiện đại thường sử dụng các API nội bộ để giao tiếp giữa frontend và backend nhưng lại không cung cấp tài liệu công khai. Việc tìm kiếm các endpoint này thủ công bằng Network Tab của trình duyệt cực kỳ mất thời gian. Bài toán này giải quyết triệt để bằng cách tự động cào mã nguồn JavaScript, sử dụng Regex kết hợp AI (Claude, Gemini qua OpenRouter) để phân tích, tự sinh và kiểm thử Regex tối ưu nhằm bóc tách toàn bộ API endpoint ẩn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 (đặc biệt khi xử lý các file JS lớn hoặc chạy LLM agent nhiều vòng lặp), các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Quét toàn bộ file JavaScript của trang web mục tiêu chỉ với 1 cú click.
- **Kết hợp đa phương pháp:** Sử dụng Regex định nghĩa trước kết hợp cùng AI Agent (tự sửa lỗi, tự cải tiến) để trích xuất triệt để endpoint.
- **Hiểu sâu cấu trúc web:** Nắm bắt nhanh các route nội bộ, cấu trúc query parameter và phương thức HTTP (GET/POST...) mà không cần đọc code thủ công.
- **Xuất báo cáo trực quan:** Tự động tổng hợp, loại bỏ trùng lặp và xuất kết quả ra file Excel (.xlsx) để tiện phân tích.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (phiên bản hỗ trợ LangChain và các AI Agent nodes).
- **OpenRouter API Key:** Tài khoản OpenRouter để kết nối với các mô hình LLM mạnh như Claude 3.7 Sonnet và Gemini 2.5 Pro.
- **Mục tiêu phù hợp:** Website cần phân tích phải chứa các API endpoint dạng chuỗi ký tự (string literal) trong mã nguồn JavaScript (phù hợp với các nền tảng SPA, Next.js, Nuxt.js, Knockout.js...).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n.io (Link: `https://n8n.io/workflows/4627`) và import trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node `Configuration`:** Điền URL của trang web mục tiêu vào trường `URL`.
- **Node `AI Endpoints Analysis` & `Regex Generation LLM`:** Cấu hình credentials cho `OpenRouter API`. Các sếp có thể tùy chỉnh model LLM (mặc định sử dụng Claude 3.7 Sonnet cho Agent và Gemini cho phân tích ban đầu).
- **Kiểm tra vòng lặp validation:** Workflow sử dụng cơ chế AI Agent tự đánh giá và cải tiến Regex thông qua sub-workflow (`Validate LLM Regex`), có thể lặp lại tối đa 4 lần để tìm ra biểu thức chính quy tối ưu nhất.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** tại node `Start API Discovery` để chạy thử nghiệm với URL mặc định.
- Sau khi kiểm tra dữ liệu đầu ra chính xác trong file Excel kết quả, các sếp có thể bật **Active** để sử dụng lâu dài.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Kết nối node cuối cùng với Slack hoặc Telegram để nhận ngay file Excel chứa danh sách API endpoint vừa quét được mỗi khi phân tích xong một website mới.
- **Lưu trữ lịch sử:** Lưu các file endpoint thô vào Google Drive hoặc Notion để xây dựng thư viện API nội bộ cho team phát triển.
- **Tùy chỉnh bộ lọc JS:** Tại node `Keep Relevant JS Files`, các sếp có thể bổ sung hoặc loại bỏ các điều kiện lọc URL để tập trung vào các file bundle chính của ứng dụng.

### 📌 Kết luận
Workflow này là "vũ khí bí mật" giúp các lập trình viên, chuyên gia bảo mật và kỹ sư tự động hóa tiết kiệm hàng giờ đồng hồ phân tích mã nguồn thủ công. Hãy import ngay vào n8n và bắt đầu khám phá hệ thống API ẩn của các nền tảng web phức tạp!