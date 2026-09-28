---
title: "🚀 Tự động hóa kiến trúc phần mềm từ mã nguồn GitHub với Claude AI"
description: "Hướng dẫn chi tiết cách tự động tạo tài liệu kiến trúc phần mềm từ mã nguồn GitHub bằng công cụ n8n và mô hình ngôn ngữ lớn Claude 3.5 Sonnet"
slug: "tu-dong-hoa-kien-truc-phan-mem-tu-github-voi-claude-ai"
tags: [n8n, automation, no-code, github, ai, architecture]
keywords: [n8n workflow, tự động hóa kiến trúc phần mềm, github automation, claude ai, kiến trúc phần mềm]
---

# 🚀 Tự động hóa kiến trúc phần mềm từ mã nguồn GitHub với Claude AI

[Các sếp] có bao giờ gặp tình trạng phải phân tích mã nguồn phức tạp để hiểu kiến trúc hệ thống không? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này chỉ trong vài phút, không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ việc phân tích thủ công sang tự động hóa hoàn toàn
- **Chính xác cao**: Dựa trên dữ liệu thực tế từ mã nguồn, không có dữ liệu giả
- **Tài liệu chuyên nghiệp**: Tạo ra tài liệu kiến trúc với biểu đồ Mermaid.js
- **Tích hợp Slack**: Nhận thông báo khi có cập nhật mới
- **Không cần code**: Hoàn toàn không cần viết code, chỉ cần cấu hình
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản GitHub với quyền tạo Personal Access Token
- API Key từ Anthropic (console.anthropic.com)
- (Tùy chọn) Tài khoản Slack với quyền tạo Bot Token
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/13362](https://n8n.io/workflows/13362)
2. Chọn "Import" và sao chép JSON workflow
3. Trong n8n Editor, chọn "Import from JSON" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Receive GitHub URL"**:
   - Đảm bảo đường dẫn webhook là duy nhất (không trùng với các workflow khác)
   - Có thể thay đổi đường dẫn nếu cần (ví dụ: "repo-blueprint" → "my-repo-blueprint")

2. **Node "Fetch Repo Metadata" và "Fetch Repo Tree"**:
   - Cần cấu hình credentials "GitHub API"
   - Tạo Personal Access Token với scope "repo" trong GitHub
   - Thêm token này vào n8n với tên "GitHub API"

3. **Node "Claude 3.5 Sonnet"**:
   - Cần cấu hình credentials "Anthropic API"
   - Đăng ký tài khoản tại console.anthropic.com và lấy API Key
   - Thêm API Key vào n8n với tên "Anthropic API"

4. **Node "Notify on Update" (tùy chọn)**:
   - Cần cấu hình credentials "Slack API"
   - Tạo Slack Bot Token với scope "chat:write"
   - Thêm token vào n8n với tên "Slack API"
   - Cập nhật ID kênh Slack trong node này

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node quan trọng, chọn "Activate" để bật workflow
2. Sử dụng một trong hai cách:
   - Truy cập URL form: `http://your-n8n-instance.com/webhook/repo-blueprint-form`
   - Gửi POST request đến webhook: `http://your-n8n-instance.com/webhook/repo-blueprint` với body JSON:
     ```json
     {
       "github_url": "https://github.com/owner/repo"
     }
     ```

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp với CI/CD**: Kết nối workflow này với pipeline CI/CD để tự động tạo tài liệu kiến trúc khi có thay đổi mã nguồn
2. **Lưu trữ lịch sử**: Thêm node để lưu trữ các phiên bản tài liệu kiến trúc trước đó
3. **Tùy chỉnh template**: Sửa đổi prompt trong node "Analyze Architecture" để phù hợp với phong cách tài liệu của công ty
4. **Báo cáo định kỳ**: Thiết lập lịch chạy định kỳ để phân tích các repository quan trọng

### 📌 Kết luận
Workflow này mang lại giải pháp toàn diện cho việc tự động hóa tạo tài liệu kiến trúc phần mềm từ mã nguồn GitHub. Với sự kết hợp của n8n và Claude AI, các sếp có thể tiết kiệm thời gian đáng kể trong quá trình phân tích và tài liệu hóa kiến trúc hệ thống. Hãy thử ngay và trải nghiệm sự khác biệt trong quy trình làm việc của mình!