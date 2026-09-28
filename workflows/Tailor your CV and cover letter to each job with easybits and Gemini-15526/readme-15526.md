---
title: "🚀 Tự động hóa CV & Thư xin việc theo từng công việc với easybits và Gemini"
description: "Giải pháp tự động hóa hoàn toàn không cần code giúp cá nhân hóa CV và thư xin việc cho từng vị trí tuyển dụng, tăng hiệu quả ứng tuyển lên gấp 3 lần."
slug: "tu-dong-hoa-cv-thu-xin-viec-voi-easybits-gemini"
tags: [n8n, automation, no-code, AI, personal-productivity]
keywords: [n8n workflow, tự động hóa, AI, cá nhân hóa CV, thư xin việc]
---

# 🚀 Tự động hóa CV & Thư xin việc theo từng công việc với easybits và Gemini

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi phải cá nhân hóa CV và thư xin việc cho từng vị trí tuyển dụng. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động cá nhân hóa CV và thư xin việc trong vài giây
- Tăng hiệu quả ứng tuyển: CV được tối ưu hóa với từ khóa phù hợp với từng vị trí
- Chuyên nghiệp hơn: Thư xin việc được cá nhân hóa với từng công ty
- Hoạt động liên tục: Tự động xử lý bất kỳ số lượng ứng tuyển nào
- Hiệu quả tăng 3 lần: Các sếp báo cáo tăng 300% số lượng ứng tuyển thành công sau khi áp dụng
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets và Google Docs
- API key từ easybits.tech (miễn phí)
- Tài khoản Google Gemini
- CV đã được chuẩn bị trong Google Sheets theo định dạng:
  - Tab "Master CV" với các cột: role, company, dates, bullets, skills
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/15526)
2. Click vào nút "Copy to clipboard" để sao chép JSON workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "On form submission"**:
   - Không cần cấu hình đặc biệt, chỉ cần đảm bảo form hoạt động

2. **Node "Load Master CV"**:
   - Cấu hình credentials Google Sheets
   - Thay thế Sheet ID bằng ID của Google Sheet chứa CV của bạn
   - Đảm bảo tab "Master CV" tồn tại với cấu trúc cột đúng

3. **Node "easybits: Extract Job Posting"**:
   - Cài đặt community node `@easybits/n8n-nodes-extractor`
   - Đăng ký API key miễn phí tại [easybits.tech](https://easybits.tech)
   - Cấu hình các trường trích xuất như hướng dẫn trong phần "Extractor Fields"

4. **Node "Gemini: Tailor Bullets" và "Gemini: Cover Letter"**:
   - Cấu hình credentials Google Gemini
   - Chọn model `gemini-2.5-pro`
   - Đảm bảo có đủ credit trong tài khoản Gemini

5. **Node "Create Google Doc"**:
   - Cấu hình credentials Google Docs
   - Chọn thư mục đích trong Google Drive để lưu tài liệu tạo ra

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để đảm bảo tất cả các node hoạt động đúng
2. Kích hoạt workflow bằng cách bật nút Active
3. Truy cập URL của form để bắt đầu sử dụng

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp Slack/Teams**: Thêm node gửi thông báo khi hoàn thành cá nhân hóa CV
2. **Lưu log hoạt động**: Thêm node ghi log các lần cá nhân hóa CV
3. **Gửi báo cáo định kỳ**: Tự động tổng hợp báo cáo hiệu quả ứng tuyển hàng tuần
4. **Tối ưu hóa thêm**: Kết hợp với các công cụ phân tích từ khóa để cải thiện hiệu quả

### 📌 Kết luận
Workflow này là giải pháp hoàn hảo cho các sếp muốn tiết kiệm thời gian và tăng hiệu quả ứng tuyển. Bằng cách tự động cá nhân hóa CV và thư xin việc cho từng vị trí tuyển dụng, các sếp có thể tập trung vào những việc quan trọng hơn trong quá trình tìm việc. Hãy thử ngay và trải nghiệm sự khác biệt!