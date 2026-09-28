---
title: "🚀 Tự động lưu dữ liệu form website vào Notion CRM"
description: "Giải pháp không code giúp chuyển mọi submission từ form website ngay lập tức vào database Notion CRM, tiết kiệm thời gian và giảm lỗi nhập liệu."
slug: "tu-dong-luu-du-lieu-form-website-vao-notion-crm"
tags: [n8n, automation, no-code, lead-generation, crm, notion]
keywords: [n8n workflow, tự động hóa, Notion CRM, capture form, lead generation]
---

# 🚀 Tự động lưu dữ liệu form website vào Notion CRM

Khi các sếp phải thu thập thông tin khách hàng qua form trên website, thường gặp phải **độ trễ**, **sai sót khi copy‑paste**, và **không thể theo dõi thời gian thực**. Việc nhập liệu thủ công vào CRM tiêu tốn hàng giờ mỗi tuần và dễ gây mất mát dữ liệu quan trọng.  

Workflow này sẽ **bắt mọi submission** từ form, **làm sạch & chuẩn hoá** dữ liệu bằng một node Code, rồi **tự động tạo trang** trong database Notion của bạn – hoàn toàn không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: dữ liệu được chuyển ngay khi người dùng submit, không cần nhập tay.  
- **Độ chính xác 100 %**: không còn lỗi đánh máy hay dữ liệu bị thiếu.  
- **Tự động hoá quy trình lead**: mỗi lead xuất hiện ngay trong Notion, sẵn sàng phân công và theo dõi.  
- **Hoạt động liên tục 24/7**: workflow chạy trên server riêng, không phụ thuộc vào máy cá nhân.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản Notion** với quyền **Integration** và **Access** vào database CRM muốn ghi.  
- **API Key (Notion Integration Token)** để cấu hình node Notion.  
- **URL webhook** sẽ được tạo tự động trong node Webhook; cần đưa URL này vào thuộc tính “action” của form trên website (method POST).  
- (Tuỳ chọn) Nếu muốn mở rộng, chuẩn bị **Slack/Telegram webhook** để nhận thông báo khi có lead mới.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Đăng nhập vào n8n Dashboard.  
2. Click **“Import” → “From File”** và tải file JSON của workflow (hoặc **Copy/Paste** JSON vào ô nhập).  
3. Sau khi import, workflow sẽ xuất hiện với 3 node: **Form Submission Hook**, **Parse + Clean Lead Data**, **Notion**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Cấu hình quan trọng | Hướng dẫn chi tiết |
|------|--------------------|--------------------|
| **Form Submission Hook** (Webhook) | **Path**: `34e9fb3f-f6bd-4a44-bb58-6fe58ffe4a78` <br> **Method**: `POST` | - Sao chép URL webhook được n8n tạo (ví dụ: `https://your-n8n-domain/webhook/34e9fb3f-f6bd-4a44-bb58-6fe58ffe4a78`). <br> - Dán URL này vào thuộc tính `action` của form trên website và đặt method là POST. |
| **Parse + Clean Lead Data** (Code) | **Code**: (đã có sẵn, chỉ cần kiểm tra các trường) | - Mở node Code, kiểm tra phần `return items.map(item => ({ json: { name: item.json.name, email: item.json.email, businessName: item.json.businessName, "project intent/need": item.json.message, timeline: item.json.timeline, budget: item.json.budget } }))`. <br> - Nếu form của bạn có trường bổ sung (ví dụ: `preferredContactTime`), thêm vào đối tượng JSON và cập nhật phần **Mapping** ở node Notion. |
| **Notion** (Create Page) | **Database ID**: ID của database CRM trong Notion. <br> **Credentials**: Chọn Integration Token đã tạo. | - Trong tab **“Database”**, dán **Database ID** (lấy từ URL của database trong Notion). <br> - Trong **“Properties”**, map từng thuộc tính: <br>   - **Name** → `{{$json["name"]}}` <br>   - **Email** → `{{$json["email"]}}` <br>   - **Business Name** → `{{$json["businessName"]}}` <br>   - **Project Intent/Need** → `{{$json["project intent/need"]}}` <br>   - **Timeline** → `{{$json["timeline"]}}` <br>   - **Budget** → `{{$json["budget"]}}` <br> - Nếu đã thêm trường mới ở node Code, tạo thuộc tính mới trong Notion và map tương ứng. |

#### 3. Kích hoạt ⚡️
1. **Test run**: Mở form trên website, điền dữ liệu mẫu và submit. Kiểm tra tab **Execution** của node Webhook để chắc chắn dữ liệu đã tới.  
2. Kiểm tra node **Code** để xác nhận dữ liệu được chuyển thành JSON đúng định dạng.  
3. Kiểm tra node **Notion** – một trang mới phải xuất hiện trong database.  
4. Khi mọi thứ ổn, bật **“Active”** cho workflow (nút toggle ở góc trên bên phải).  

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram**: Thêm một node **Slack** hoặc **Telegram** sau node Notion để gửi tin nhắn “New lead from website” kèm link trang Notion.  
- **Ghi log vào Google Sheet**: Dùng node **Google Sheets** để lưu bản sao dữ liệu, giúp tạo báo cáo thống kê nhanh.  
- **Tự động phân công**: Kết hợp với node **Email** hoặc **Microsoft Teams** để gửi email cho người phụ trách dựa trên trường “budget” hoặc “timeline”.  
- **Xử lý duplicate**: Thêm một node **IF** kiểm tra xem email đã tồn tại trong Notion chưa; nếu có, cập nhật thay vì tạo mới.  

### 📌 Kết luận
Với chỉ **3 node** đơn giản, các sếp có thể biến mọi form website thành một nguồn lead **đầy đủ, sạch sẽ và luôn sẵn sàng** trong Notion CRM. Hãy triển khai ngay, giảm thiểu công việc nhập liệu thủ công và tập trung vào việc **chốt deal**! 🚀