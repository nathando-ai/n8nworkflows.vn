---
title: "🚀 Hướng dẫn tự động đồng bộ và di chuyển dữ liệu khách hàng từ Odoo v15 lên v18 bằng n8n"
description: "Tự động hóa hoàn toàn quy trình chuyển đổi và đồng bộ dữ liệu khách hàng từ Odoo v15 sang v18 an toàn, nhanh chóng và không mất mát dữ liệu với n8n."
slug: "migrate-customer-data-odoo-v15-to-v18-n8n"
tags: [n8n, automation, odoo, crm, data-migration, no-code]
keywords: [odoo migration, odoo v15 to v18, n8n odoo integration, đồng bộ dữ liệu odoo, tự động hóa n8n]
---

# 🚀 Tự động đồng bộ và di chuyển dữ liệu khách hàng từ Odoo v15 lên v18

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Khi doanh nghiệp phát triển và nâng cấp hệ thống ERP từ **Odoo v15 lên v18**, một trong những thách thức lớn nhất là việc di chuyển dữ liệu khách hàng cũ sang phiên bản mới. Nếu làm thủ công bằng cách xuất/nhập file Excel (CSV) thông thường, các sếp sẽ dễ gặp phải các vấn đề đau đầu như: trùng lặp dữ liệu, mất mát thông tin liên hệ, lỗi định dạng trường dữ liệu, và tốn hàng giờ kiểm tra thủ công. 

Hiểu được nỗi đau đó, workflow n8n này ra đời như một vị cứu tinh giúp các sếp tự động hóa 100% quy trình trích xuất, phân đoạn và đẩy dữ liệu khách hàng từ Odoo v15 sang Odoo v18 một cách mượt mà, chính xác và an toàn tuyệt đối mà không cần viết một dòng code phức tạp nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Thay vì thao tác thủ công từng bản ghi hoặc xử lý file Excel nặng nề, hệ thống tự động xử lý hàng ngàn khách hàng chỉ trong vài phút.
- **Tránh sai sót dữ liệu:** Dữ liệu được truyền tải trực tiếp qua API giữa Odoo v15 và v18, hạn chế tối đa lỗi nhập liệu thủ công.
- **Xử lý thông minh theo lô (Batching):** Chia nhỏ dữ liệu thành từng phần giúp hệ thống không bị quá tải (timeout) khi migration lượng lớn khách hàng.
- **Chủ động kiểm soát:** Dễ dàng kích hoạt thủ công để kiểm tra kết quả trước khi chạy hàng loạt cho toàn bộ hệ thống.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã cài đặt sẵn sàng (Self-hosted hoặc n8n Cloud).
- **Odoo v15 Credentials:** URL, Database Name, Username và API Key/Password để kết nối node lấy dữ liệu.
- **Odoo v18 Credentials:** URL, Database Name, Username và API Key/Password để kết nối node tạo dữ liệu mới.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Các sếp copy đoạn mã JSON của workflow này hoặc tải file JSON trực tiếp từ kho lưu trữ.
- Tại giao diện n8n Editor, chọn **Add workflow** -> Nhấp vào biểu tượng ba chấm ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow được cấu hình sẵn với 4 nodes cơ bản. Các sếp cần tập trung cấu hình kỹ các node sau:

- **Get Customers from v15 (`odoo`):** 
  - Tạo mới `Odoo API` credentials kết nối tới hệ thống Odoo v15 của các sếp.
  - Chọn đúng Resource là `Customer` (hoặc `Res Partner`) và Action là `Get Many` để lấy danh sách khách hàng cũ.
- **SplitInBatches (`splitInBatches`):**
  - Node này giúp chia nhỏ danh sách khách hàng thành các batch (mặc định thường là 10 hoặc 50 items/lần). Các sếp có thể điều chỉnh thông số `Batch Size` cho phù hợp với cấu hình server Odoo của mình để tránh bị nghẽn mạng.
- **Create Customers in v18 (`odoo`):**
  - Tạo mới một `Odoo API` credentials khác kết nối tới hệ thống Odoo v18 mới.
  - Chọn Resource là `Customer` và Action là `Create`. Ánh xạ (Map) các trường dữ liệu từ đầu ra của Odoo v15 sang các trường tương ứng của Odoo v18 (như Tên, Email, Số điện thoại, Địa chỉ...).
- **When clicking ‘Test workflow’ (`manualTrigger`):**
  - Node kích hoạt thủ công, dùng để test chạy thử trước khi đưa vào vận hành chính thức.

#### 3. Kích hoạt ⚡️
- Nhấp vào nút **Execute Workflow** để chạy thử với một lượng nhỏ dữ liệu mẫu.
- Kiểm tra lại trên giao diện Odoo v18 xem dữ liệu khách hàng đã được đổ về chính xác chưa.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để hoàn tất.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa quy trình migration này lên một tầm cao mới, các sếp có thể áp dụng thêm các ý tưởng sau:
- **Tích hợp Thông báo:** Thêm node Telegram hoặc Slack ở cuối luồng để nhận thông báo tự động (Ví dụ: *"Đã migrate thành công 500 khách hàng từ v15 sang v18!"*) khi hoàn tất.
- **Xử lý trùng lặp (Upsert):** Cấu hình thêm điều kiện kiểm tra xem email khách hàng đã tồn tại trên v18 hay chưa trước khi tạo mới để tránh bị lỗi trùng lặp bản ghi.
- **Lưu Log báo cáo:** Ghi lại danh sách các khách hàng migrate thành công hoặc gặp lỗi vào Google Sheets để tiện đối soát.

### 📌 Kết luận
Việc nâng cấp hệ thống ERP sẽ trở nên nhẹ nhàng và đơn giản hơn rất nhiều nếu các sếp biết tận dụng sức mạnh tự động hóa của n8n. Hãy áp dụng ngay workflow này để tiết kiệm thời gian và đảm bảo an toàn tuyệt đối cho cơ sở dữ liệu khách hàng của doanh nghiệp nhé!