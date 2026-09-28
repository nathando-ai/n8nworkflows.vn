---
title: "🚀 Tự động hóa JotForm: Xác thực email và bổ sung thông tin từ Reoon và Apollo vào Google Sheets"
description: "Hướng dẫn tự động hóa quy trình xác thực email và bổ sung thông tin từ Reoon và Apollo vào Google Sheets khi nhận form JotForm"
slug: "tu-dong-hoa-jotform-xac-thuc-email-va-bo-sung-thong-tin-tu-reoon-va-apollo-vao-google-sheets"
tags: [n8n, automation, no-code, JotForm, Google Sheets, Reoon, Apollo]
keywords: [n8n workflow, tự động hóa, JotForm, Google Sheets, Reoon, Apollo]
---

# 🚀 Tự động hóa JotForm: Xác thực email và bổ sung thông tin từ Reoon và Apollo vào Google Sheets

[Các sếp đang gặp khó khăn khi phải xử lý thủ công hàng nghìn form liên hệ từ JotForm mỗi ngày. Bạn phải kiểm tra từng email, bổ sung thông tin và lưu vào Google Sheets - một quá trình tốn thời gian và dễ sai sót. Workflow này sẽ giúp các sếp tự động hóa hoàn toàn quy trình này với n8n.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động xử lý hàng nghìn form mỗi ngày mà không cần can thiệp
- Tăng độ chính xác: Xác thực email và bổ sung thông tin tự động
- Dữ liệu chất lượng cao: Chỉ lưu những email an toàn và thông tin bổ sung đầy đủ
- Hoạt động liên tục: Không ngừng nghỉ, xử lý ngay khi có form mới
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản JotForm (đã tạo form liên hệ)
- Tài khoản Google (đã tạo Google Sheet từ template)
- API Key từ Reoon Email Verification
- API Key từ Apollo.io
- Tài khoản n8n (đã cài đặt trên VPS hoặc n8n.cloud)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor
2. Nhấn vào "Import from URL" và dán link: https://n8n.io/workflows/9391
3. Hoặc copy nội dung JSON từ link trên và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Google Sheets**:
   - Copy [Google Sheet template](https://docs.google.com/spreadsheets/d/1RBZ_VcxxkNqU6weYv5OxX7OWj1Y46WLHM1sbLw-iCVc/copy)
   - Chia sẻ sheet với tài khoản service của n8n (n8n@project-type.iam.gserviceaccount.com)
   - Thay thế Google Sheet ID trong tất cả các node Google Sheets (tìm kiếm "1RBZ_VcxxkNqU6weYv5OxX7OWj1Y46WLHM1sbLw-iCVc" và thay bằng ID của sheet mới)

2. **JotForm Trigger**:
   - Cập nhật JotForm ID trong node "Trigger: JotForm Submission"
   - Đảm bảo form JotForm có các trường dữ liệu tương ứng với những gì bạn muốn lưu

3. **API Credentials**:
   - Cấu hình credentials cho Reoon Email Verification trong node "API: Email Verification (Reoon)"
   - Cấu hình credentials cho Apollo.io trong node "API: Contact Enrichment (Apollo)"

4. **Form Fields**:
   - Đảm bảo form JotForm có các trường dữ liệu phù hợp với những gì bạn muốn lưu vào Google Sheets

#### 3. Kích hoạt ⚡️
1. Nhấn "Execute Workflow" để kiểm tra với dữ liệu mẫu
2. Kiểm tra Google Sheet để đảm bảo dữ liệu được lưu đúng cách
3. Bật "Active" cho workflow để nó bắt đầu hoạt động tự động

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node gửi email thông báo khi có form mới được xử lý
- Tích hợp với Slack để nhận thông báo khi có email không an toàn
- Thêm node lưu log hoạt động vào Google Sheets
- Tự động gửi email cảm ơn cho những liên hệ an toàn
- Thiết lập báo cáo hàng tuần về số lượng form đã xử lý

### 📌 Kết luận
Workflow này sẽ giúp các sếp tiết kiệm hàng giờ mỗi ngày trong việc xử lý form liên hệ từ JotForm. Bằng cách tự động xác thực email và bổ sung thông tin từ Reoon và Apollo, các sếp có thể tập trung vào những công việc quan trọng hơn. Hãy áp dụng ngay để nâng cao hiệu quả làm việc của đội ngũ!