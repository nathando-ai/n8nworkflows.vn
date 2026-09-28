---
title: "🚀 Tự động hóa quản lý danh bạ khách hàng trong Automizy với n8n"
description: "Hướng dẫn chi tiết cách kết nối và quản lý danh bạ, danh sách liên hệ, cập nhật thông tin tự động trên nền tảng Automizy sử dụng n8n workflow."
slug: "quan-ly-danh-ba-automizy-voi-n8n"
tags: [n8n, automation, no-code, automizy, crm, marketing]
keywords: [n8n workflow, tự động hóa automizy, quản lý danh bạ crm, n8n automizy integration]
---

# 🚀 Tự động hóa quản lý danh bạ khách hàng trong Automizy với n8n

Việc quản lý thủ công danh sách khách hàng (contacts) và danh bạ (lists) trên các nền tảng Email Marketing và CRM như Automizy thường tiêu tốn rất nhiều thời gian, dễ dẫn đến sai sót dữ liệu hoặc cập nhật chậm trễ các chiến dịch tiếp thị. 

Để giải quyết triệt để vấn đề này, workflow n8n **"Manage contacts in Automizy"** ra đời như một giải pháp tự động hóa 100% không cần code, giúp các sếp dễ dàng lấy danh sách, thêm mới, cập nhật thông tin liên hệ và quản lý tài nguyên trên Automizy một cách mượt mà và chuyên nghiệp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Quản lý danh sách liên hệ (lists) và contacts trên Automizy mà không cần thao tác thủ công trên giao diện web.
- **Đồng bộ chính xác:** Dễ dàng lấy toàn bộ dữ liệu (`getAll`), cập nhật thông tin khách hàng (`update`) nhanh chóng.
- **Tiết kiệm thời gian:** Giảm thiểu tối đa thao tác lặp đi lặp lại cho đội ngũ Marketing và Sales.
- **Linh hoạt mở rộng:** Dễ dàng tích hợp thêm các trigger thời gian (Schedule Trigger) hoặc kết nối với Google Sheets, Webhook tùy theo nhu cầu thực tế.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản Automizy:** Cần chuẩn bị tài khoản Automizy hoạt động.
- **Automizy API Key:** Lấy API Token từ tài khoản Automizy để cấu hình Credentials `automizyApi` trong n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Các sếp tải file JSON của workflow hoặc copy đoạn mã JSON từ n8n.
- Tại giao diện n8n Editor, chọn **Add workflow** -> **Import from File** hoặc dán trực tiếp vào màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 5 nodes chính, trong đó sử dụng các thao tác quan trọng với Automizy API:
- **Node `On clicking 'execute'` (manualTrigger):** Node kích hoạt thủ công để các sếp test workflow. Có thể thay thế bằng *Schedule Trigger* hoặc *Webhook* nếu muốn chạy tự động theo lịch.
- **Nodes `Automizy`, `Automizy1`, `Automizy2`, `Automizy3`:** 
  - **Credentials:** Cần tạo kết nối mới (`Create New Credential`) và điền **Automizy API Token** vào.
  - **Key Parameters:** Kiểm tra lại các thông số tài nguyên (`resource`) và thao tác (`operation`) như lấy danh sách (`getAll`), cập nhật thông tin liên hệ (`update`) cho phù hợp với kịch bản thực tế của doanh nghiệp.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm với dữ liệu mẫu và kiểm tra kết quả trả về từ Automizy.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để workflow sẵn sàng vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Schedule Trigger:** Thay thế nút bấm thủ công bằng trigger chạy định kỳ hàng ngày để quét và cập nhật danh bạ tự động.
- **Đồng bộ Google Sheets:** Kết nối thêm node Google Sheets để vừa quản lý trên file Excel/Sheets vừa tự động đẩy dữ liệu sang Automizy.
- **Nhận thông báo qua Slack/Telegram:** Thêm node gửi thông báo về nhóm chat mỗi khi cập nhật danh bạ thành công hoặc gặp lỗi API.

### 📌 Kết luận
Workflow **Manage contacts in Automizy** là công cụ đắc lực giúp tối ưu hóa quy trình quản trị dữ liệu khách hàng. Hãy "lên đồ" ngay hôm nay để tự động hóa hoàn toàn các thao tác Marketing của các sếp!