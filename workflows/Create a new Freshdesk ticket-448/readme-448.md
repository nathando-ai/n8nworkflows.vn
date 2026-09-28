---
title: "🚀 Tự động tạo ticket Freshdesk chỉ bằng một click"
description: "Giải pháp không code giúp các sếp tạo ticket Freshdesk nhanh chóng, giảm lỗi nhập liệu và tiết kiệm thời gian hỗ trợ."
slug: "tu-dong-tao-ticket-freshdesk"
tags: [n8n, automation, no-code, freshdesk, support]
keywords: [n8n workflow, Freshdesk, tự động hóa, ticket support, no-code automation]
---

# 🚀 Tự động tạo ticket Freshdesk chỉ bằng một click

Trong môi trường hỗ trợ khách hàng, việc tạo ticket thủ công trên Freshdesk thường tốn thời gian, dễ gây sai sót và làm giảm hiệu suất của đội ngũ support. Các sếp thường phải sao chép thông tin từ email, chat hoặc form, rồi mới nhập vào Freshdesk – một quy trình lặp đi lặp lại, mất công và dễ gây lỗi.

Workflow **“Create a new Freshdesk ticket”** của n8n giải quyết hoàn toàn vấn đề này: chỉ cần một cú click, ticket sẽ được tạo tự động trên Freshdesk, dữ liệu được chuẩn hoá, đồng thời giảm thiểu tối đa thời gian và sai sót. Không cần viết một dòng code nào – chỉ cần cấu hình nhanh chóng và chạy 24/7.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tạo ticket chỉ trong vài giây, không còn thao tác nhập liệu lặp lại.  
- **Độ chính xác cao**: Dữ liệu được truyền trực tiếp từ nguồn (form, email…) sang Freshdesk, giảm lỗi nhập tay.  
- **Tự động ghi nhận**: Mọi ticket đều được lưu lại, hỗ trợ báo cáo và phân tích hiệu suất.  
- **Hoạt động liên tục**: Workflow chạy 24/7, không phụ thuộc vào giờ làm việc của nhân viên.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Freshdesk** với quyền tạo ticket.  
- **API Key** của Freshdesk (lấy tại *Admin Settings → API → Your API Key*).  
- **Domain Freshdesk** (ví dụ: `yourcompany.freshdesk.com`).  
- **n8n** đã được cài đặt và chạy (Self‑hosted hoặc n8n.cloud).  
- Kết nối internet ổn định để n8n có thể gọi API Freshdesk.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập **n8n → Workflows → Import**.  
2. Tải file JSON của workflow (hoặc copy toàn bộ JSON vào ô **Paste JSON**).  
3. Nhấn **Import** → Workflow sẽ xuất hiện trong danh sách.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Hành động cần cấu hình | Hướng dẫn chi tiết |
|------|------------------------|--------------------|
| **On clicking 'execute'** (Manual Trigger) | Không cần cấu hình thêm, chỉ dùng để kích hoạt workflow bằng một click trong UI n8n. | Khi workflow đã được import, mở node này và nhấn **Execute Workflow** để kiểm tra. |
| **Freshdesk** | **Credentials**, **Domain**, **Operation**, **Ticket fields** | 1. **Credentials** → Chọn **freshdeskApi** → Nhập **API Key** và **Domain**.<br>2. **Operation** → Chọn **Create** (tạo ticket mới).<br>3. **Ticket fields** → Điền các trường cần thiết: <br>   - **Subject**: tiêu đề ticket (có thể dùng expression `{{$json["subject"]}}`).<br>   - **Description**: nội dung chi tiết.<br>   - **Email**: email người gửi.<br>   - **Priority**, **Status**, **Tags** (tùy chọn).<br>4. Nếu muốn lấy dữ liệu từ một nguồn khác (ví dụ Google Sheet, webhook), dùng **Expression** để truyền giá trị vào các trường trên. |
| **Lưu ý quan trọng** | Kiểm tra **API Rate Limits** của Freshdesk để tránh bị chặn khi tạo quá nhiều ticket trong thời gian ngắn. | Đặt **Delay** node nếu cần giới hạn tốc độ. |

#### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn **Execute Workflow** → Kiểm tra kết quả trong Freshdesk (một ticket mới sẽ xuất hiện).  
2. Nếu mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc phải) để workflow luôn sẵn sàng nhận lệnh.  

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Slack/Telegram**: Thêm node Slack hoặc Telegram để gửi thông báo ngay khi ticket được tạo.  
- **Ghi log vào Google Sheets**: Dùng node Google Sheets để lưu lại mọi ticket đã tạo, hỗ trợ báo cáo định kỳ.  
- **Tự động phân loại**: Sử dụng node **IF** hoặc **Switch** để dựa trên từ khóa trong tiêu đề, tự động gán **Priority** hoặc **Group** cho ticket.  
- **Đính kèm file**: Nếu nguồn dữ liệu có file đính kèm, dùng node **HTTP Request** để tải file và truyền vào trường **Attachments** của Freshdesk.  

### 📌 Kết luận
Với workflow **Create a new Freshdesk ticket** trên n8n, các sếp có thể loại bỏ hoàn toàn công đoạn tạo ticket thủ công, giảm thiểu lỗi và nâng cao năng suất đội ngũ support. Hãy import ngay, cấu hình API Freshdesk và bắt đầu tự động hoá quy trình hỗ trợ khách hàng của mình – tiết kiệm thời gian, tăng độ chính xác và luôn sẵn sàng phục vụ 24/7!