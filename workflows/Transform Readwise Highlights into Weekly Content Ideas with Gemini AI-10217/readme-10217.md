---
title: "🚀 Tự động hóa nội dung từ Readwise với Gemini AI - Workflow n8n hoàn chỉnh"
description: "Hướng dẫn chi tiết cách tự động hóa việc tổng hợp nội dung từ Readwise thành ý tưởng bài viết hàng tuần bằng Gemini AI, tiết kiệm 80% thời gian biên tập nội dung"
slug: "tu-dong-hoa-noi-dung-readwise-gemini-ai"
tags: [n8n, automation, no-code, content-creation, ai-summarization]
keywords: [n8n workflow, tự động hóa nội dung, Gemini AI, Readwise, biên tập nội dung]
---

# 🚀 Tự động hóa nội dung từ Readwise với Gemini AI - Workflow n8n hoàn chỉnh

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp biên tập nội dung khi phải thủ công tổng hợp hàng trăm highlight từ Readwise mỗi tuần. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm **80% thời gian** biên tập nội dung hàng tuần
- Tự động tổng hợp **hàng trăm highlight** từ Readwise thành nội dung chất lượng
- Cá nhân hóa nội dung theo phong cách riêng của mỗi sếp
- Hoạt động liên tục **mỗi tuần một lần** mà không cần can thiệp
- Tiết kiệm chi phí **không cần thuê biên tập viên** cho công việc này
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Readwise và API Key (để truy cập dữ liệu highlight)
- Tài khoản OpenRouter và API Key (để sử dụng Gemini AI)
- Kiến thức cơ bản về cấu hình n8n workflow
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/10217)
2. Click "Use workflow" > "Copy JSON"
3. Trong n8n Editor, click "Import from Clipboard" và dán JSON đã copy

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

**Node quan trọng nhất cần cấu hình:**
- **Fetch Articles** và **Fetch Highlights**: Cần cấu hình credentials với Readwise API Key
- **AI Model**: Cần cấu hình credentials với OpenRouter API Key
- **Prepare Prompt**: Có thể chỉnh sửa prompt để phù hợp với phong cách nội dung của các sếp

**Các bước cấu hình chi tiết:**
1. Tạo credentials cho Readwise API:
   - Trong n8n Editor, vào "Credentials" > "Create new"
   - Chọn "HTTP Header Auth" > "Create"
   - Đặt tên: "Readwise API"
   - Thêm header: `Authorization` với giá trị `Token YOUR_READWISE_API_KEY`

2. Tạo credentials cho OpenRouter API:
   - Tương tự như trên, tạo credentials "HTTP Header Auth"
   - Đặt tên: "OpenRouter API"
   - Thêm header: `Authorization` với giá trị `Bearer YOUR_OPENROUTER_API_KEY`

3. Cấu hình các node HTTP Request:
   - Đối với các node **Fetch Articles** và **Fetch Highlights**:
     - URL: `https://readwise.io/api/v2/export/`
     - Method: POST
     - Body: `{"updatedAfter": "7 days ago"}`
     - Headers: Sử dụng credentials "Readwise API"

4. Cấu hình node **AI Model**:
   - Model: `google/gemini-2.5-pro`
   - Credentials: "OpenRouter API"

5. Tùy chỉnh prompt (tùy chọn):
   - Vào node **Prepare Prompt** > "Edit code"
   - Chỉnh sửa phần prompt để phù hợp với phong cách nội dung của các sếp

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu:
   - Click vào node **When clicking ‘Execute workflow’**
   - Click "Execute Node" để kiểm tra kết quả
2. Bật Active workflow:
   - Click vào node **Monday - 09:00**
   - Click "Activate" để kích hoạt workflow chạy tự động mỗi thứ Hai lúc 9h sáng

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Telegram**: Thêm node gửi thông báo khi workflow hoàn thành
2. **Lưu log hoạt động**: Thêm node lưu kết quả vào Google Sheets để theo dõi lịch sử
3. **Tùy chỉnh định dạng đầu ra**: Chỉnh sửa node **Convert Insights to HTML** để phù hợp với hệ thống CMS của các sếp
4. **Thêm bộ lọc nội dung**: Mở rộng node **Filter Articles >10% Read** để lọc theo chủ đề hoặc tác giả

### 📌 Kết luận
Workflow này giúp các sếp biên tập nội dung **tự động hóa hoàn toàn** quá trình tổng hợp highlight từ Readwise thành nội dung hàng tuần. Với chỉ 15 nodes đơn giản, các sếp có thể tiết kiệm hàng giờ làm việc mỗi tuần mà không cần phải viết code hay thuê biên tập viên. Hãy thử ngay và thấy sự khác biệt trong hiệu suất biên tập nội dung của mình!