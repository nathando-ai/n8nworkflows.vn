---
title: "🚀 Tự Động Lọc Trùng Lặp Lead với Google Sheets và GoHighLevel trên n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động kiểm tra trùng lặp lead, đồng bộ CRM GoHighLevel và ghi log chi tiết vào Google Sheets."
slug: "tu-dong-loc-trung-lap-lead-google-sheets-gohighlevel"
tags: [n8n, automation, crm, gohighlevel, google-sheets, lead-management]
keywords: [n8n workflow, lọc trùng lead, duplicate leads n8n, google sheets trigger, gohighlevel integration]
---

# 🚀 Tự Động Lọc Trùng Lặp Lead với Google Sheets và GoHighLevel trên n8n

Các sếp có đang gặp tình trạng khách hàng điền form nhiều lần, dẫn đến hệ thống CRM (như GoHighLevel) bị tràn ngập các contact trùng lặp, gây rối loạn trong việc chăm sóc và tốn kém chi phí không? Việc lọc và xử lý lead trùng lặp bằng tay cực kỳ mất thời gian và dễ xảy ra sai sót.

Workflow n8n này do chuyên gia **Rahul Joshi** thiết kế sẽ giải quyết triệt để bài toán trên. Hệ thống sẽ tự động theo dõi Google Sheets, kiểm tra xem lead đã tồn tại hay chưa, sau đó tự động **Tạo mới contact (nếu là khách mới)** hoặc **Cập nhật thông tin (nếu là khách cũ)** lên GoHighLevel, đồng thời ghi log đầy đủ vào Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Loại bỏ 100% bản ghi trùng lặp**: Tự động nhận diện email đã tồn tại trong hệ thống.
- **Đồng bộ CRM thông minh**: Tự động tạo contact mới hoặc cập nhật thông tin mới nhất vào GoHighLevel (GHL).
- **Quản lý Log chặt chẽ**: Ghi lại lịch sử lead mới và lịch sử lead trùng lặp vào Google Sheets riêng biệt để dễ dàng theo dõi, thống kê.
- **Hoạt động tự động 24/7**: Chạy ngầm liên tục, phản hồi tức thì ngay khi có lead mới điền form.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **Google Sheets** chứa bảng dữ liệu lead nguồn và file log.
- Tài khoản **GoHighLevel (GHL)** cùng với API Key / Credentials để kết nối.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ kho lưu trữ n8n (ID: `8281`) và tiến hành Import trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 9 nodes chính, các sếp cần cấu hình kỹ các điểm sau:

- **Google Sheets Trigger1**: Kết nối tài khoản Google Sheets của các sếp và chọn đúng file/sheet chứa dữ liệu form đăng ký lead đến. Node này sẽ quét dữ liệu mới mỗi phút.
- **Lookup Lead1**: Cấu hình trỏ tới cơ sở dữ liệu master để tìm kiếm email của lead mới gửi đến xem đã tồn tại trước đó hay chưa.
- **Check from the data base?1** & **Check the duplication**: Các node điều kiện và lọc dữ liệu giúp phân tách rõ ràng 2 nhánh: Khách hàng hoàn toàn mới (New Lead) và Khách hàng đã tồn tại (Duplicate Lead).
- **Create Contact (GHL)1** & **Update Contact (GHL)1**: Điền thông tin API Credentials của GoHighLevel để hệ thống thực hiện lệnh tạo contact mới hoặc cập nhật contact cũ.
- **Log New Lead1** & **Log Duplicate Lead1**: Trỏ đến các Google Sheets tương ứng để ghi nhận log, lưu thời gian (timestamp) và trạng thái xử lý lead.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) với một vài dòng dữ liệu mẫu để kiểm tra luồng chạy qua các nhánh có chính xác không.
- Sau khi test thành công, bật công tắc **Active** để workflow chính thức vận hành tự động.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo Real-time**: Thêm node Telegram hoặc Slack vào nhánh Log để nhận thông báo ngay lập tức về điện thoại mỗi khi có lead mới hoặc lead trùng lặp.
- **Mở rộng nguồn dữ liệu**: Thay vì chỉ dùng Google Sheets Trigger, các sếp có thể kết hợp thêm Webhook từ Landing Page, Facebook Lead Ads hoặc Typeform.
- **Lưu trữ lịch sử chi tiết**: Sử dụng thêm node tính toán để đếm số lần một khách hàng quay lại submit form, phục vụ cho việc đánh giá độ quan tâm của khách hàng (Lead Scoring).

### 📌 Kết luận
Workflow tự động hóa lọc trùng lặp lead này là một mảnh ghép không thể thiếu cho các đội ngũ Marketing và Sales. Giúp hệ thống CRM luôn sạch sẽ, dữ liệu chính xác và không bỏ lỡ bất kỳ tương tác nào từ khách hàng. Hãy áp dụng ngay vào hệ thống của các sếp!