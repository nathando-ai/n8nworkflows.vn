---
title: "🚀 Tự động hóa tổng kết cuộc gọi bán hàng và cập nhật CRM với WayinVideo và GPT-4o-mini"
description: "Hướng dẫn chi tiết cách tự động hóa quá trình tổng kết cuộc gọi bán hàng, trích xuất thông tin quan trọng và cập nhật CRM bằng n8n, WayinVideo và GPT-4o-mini"
slug: "tu-dong-hoa-tong-ket-cuoc-goi-ban-hang-va-cap-nhat-crm"
tags: [n8n, automation, no-code, CRM, AI]
keywords: [n8n workflow, tự động hóa, tổng kết cuộc gọi, CRM, GPT-4o-mini]
---

# 🚀 Tự động hóa tổng kết cuộc gọi bán hàng và cập nhật CRM với WayinVideo và GPT-4o-mini

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi phải tổng kết thủ công các cuộc gọi bán hàng dài, mất thời gian và dễ bỏ sót thông tin quan trọng. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 30-50% thời gian tổng kết cuộc gọi
- Tự động trích xuất thông tin quan trọng từ cuộc gọi
- Cập nhật CRM tự động với dữ liệu chính xác
- Hoạt động liên tục 24/7 mà không cần can thiệp
- Tạo báo cáo chi tiết cho mỗi cuộc gọi
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản WayinVideo với API key
- Tài khoản OpenAI để sử dụng GPT-4o-mini
- Tài khoản Google để lưu báo cáo
- URL của các cuộc gọi Zoom/Google Meet cần tổng kết
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/14588)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node 2 và 4 (WayinVideo)**:
   - Thay thế **YOUR_WAYIN_API_KEY** bằng API key của bạn
   - Đảm bảo tài khoản WayinVideo có quyền truy cập vào các cuộc gọi cần tổng kết

2. **Node 6 (OpenAI Chat Model)**:
   - Kết nối tài khoản OpenAI của bạn
   - Đảm bảo model được chọn là "gpt-4o-mini"

3. **Node 7 (Google Docs)**:
   - Thay thế **YOUR_GOOGLE_DOC_URL_OR_ID** bằng URL hoặc ID của Google Doc bạn muốn lưu báo cáo
   - Kết nối tài khoản Google OAuth2 của bạn

#### 3. Kích hoạt ⚡️
1. Test run với dữ liệu mẫu để đảm bảo workflow hoạt động đúng
2. Bật Active workflow
3. Chia sẻ URL của form với team bán hàng của bạn

### ✍️ Mẹo & gợi ý nâng cao
1. **Nâng cấp model AI**: Thay thế GPT-4o-mini bằng GPT-4o để có độ chính xác cao hơn với các cuộc gọi phức tạp
2. **Thông báo tự động**: Thêm node Slack hoặc Email sau node 7 để thông báo khi có báo cáo mới được lưu
3. **Giới hạn vòng lặp**: Thêm biến đếm để giới hạn số lần thử lại khi transcript chưa sẵn sàng (giúp tránh vòng lặp vô hạn)
4. **Lưu trữ dữ liệu**: Thêm node để lưu trữ các báo cáo trong Google Drive hoặc cơ sở dữ liệu của bạn

### 📌 Kết luận
Workflow này giúp các sếp bán hàng tiết kiệm thời gian quý giá, tự động hóa quy trình tổng kết cuộc gọi và cập nhật CRM một cách chính xác. Bằng cách áp dụng workflow này, các sếp có thể tập trung vào các hoạt động quan trọng hơn trong quá trình bán hàng. Hãy thử ngay và trải nghiệm sự khác biệt!