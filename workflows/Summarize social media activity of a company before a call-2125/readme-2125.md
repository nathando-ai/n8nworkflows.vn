---
title: "🚀 Tự động tổng hợp hoạt động mạng xã hội của công ty trước cuộc gọi - Workflow n8n"
description: "Tiết kiệm thời gian chuẩn bị cuộc gọi quan trọng bằng cách tự động tổng hợp thông tin từ LinkedIn, Twitter và email của khách hàng tiềm năng."
slug: "tu-dong-tong-hop-hoat-dong-mang-xa-hoi-truoc-cuoc-goi"
tags: [n8n, automation, no-code, sales, marketing]
keywords: [n8n workflow, tự động hóa, sales, marketing, CRM]
---

# 🚀 Tự động tổng hợp hoạt động mạng xã hội của công ty trước cuộc gọi

[Các sếp bán hàng và marketing thường phải tốn nhiều thời gian để chuẩn bị cho cuộc gọi quan trọng. Thay vì phải tra cứu thông tin từ nhiều nguồn khác nhau, workflow này sẽ tự động tổng hợp thông tin từ LinkedIn, Twitter và email của khách hàng tiềm năng, giúp các sếp có cái nhìn tổng quan nhanh chóng và chính xác.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian lên tới 80% khi chuẩn bị cuộc gọi quan trọng.
- Có cái nhìn tổng quan về hoạt động mạng xã hội của khách hàng tiềm năng.
- Tăng độ chính xác thông tin khi chuẩn bị cuộc gọi.
- Tự động hóa hoàn toàn quá trình tổng hợp thông tin.
- Nhận báo cáo tóm tắt qua email trước mỗi cuộc gọi.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Calendar (để lấy danh sách cuộc họp).
- Tài khoản Gmail (để gửi email tóm tắt).
- API keys từ RapidAPI cho:
  - [Fresh LinkedIn Profile Data](https://rapidapi.com/freshdata-freshdata-default/api/fresh-linkedin-profile-data)
  - [Twitter API](https://rapidapi.com/omarmhaimdat/api/twitter154)
- API key từ OpenAI (để sử dụng tính năng tóm tắt bằng AI).
- API key từ Clearbit (để lấy thông tin công ty).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/2125](https://n8n.io/workflows/2125)
2. Click vào nút "Import" để tải file JSON về máy.
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Setup"**:
   - Điền danh sách email nhận báo cáo vào trường `emails`.

2. **Node "Get recent LinkedIn posts"**:
   - Điền API key từ RapidAPI vào trường `linkedInAPIKey`.

3. **Node "Get latest tweets"**:
   - Điền API key từ RapidAPI vào trường `twitterAPIKey`.

4. **Node "Get meetings for today"**:
   - Chọn credentials Google Calendar.
   - Đảm bảo tài khoản Google Calendar đã được chia sẻ với các sếp cần nhận báo cáo.

5. **Node "Gmail"**:
   - Chọn credentials Gmail.
   - Đảm bảo tài khoản Gmail đã được cấu hình để gửi email.

6. **Node "Ask AI to summerize"**:
   - Chọn credentials OpenAI.
   - Có thể điều chỉnh prompt trong trường `prompt` nếu cần.

7. **Node "Enrich attendee company"**:
   - Chọn credentials Clearbit.

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute Workflow" để test chạy dữ liệu mẫu.
2. Sau khi test thành công, click vào nút "Activate" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Để nhận báo cáo hàng ngày, các sếp có thể điều chỉnh lịch trình trong node "Every morning @ 7".
- Nếu cần thêm nguồn thông tin từ mạng xã hội khác, các sếp có thể thêm node tương ứng và xử lý trong node "Switch".
- Để gửi báo cáo qua Slack hoặc Telegram, các sếp có thể thêm node tương ứng sau node "Prepare email template".
- Để lưu log hoạt động, các sếp có thể thêm node "Sticky Note" sau node "Wrap everything together".

### 📌 Kết luận
Workflow này giúp các sếp bán hàng và marketing tiết kiệm thời gian đáng kể khi chuẩn bị cho cuộc gọi quan trọng. Bằng cách tự động tổng hợp thông tin từ nhiều nguồn khác nhau, các sếp có thể có cái nhìn tổng quan nhanh chóng và chính xác về khách hàng tiềm năng. Hãy áp dụng ngay để nâng cao hiệu suất làm việc!