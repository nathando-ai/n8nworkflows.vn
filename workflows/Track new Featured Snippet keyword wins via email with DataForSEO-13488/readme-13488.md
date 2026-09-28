---
title: "🚀 Theo dõi từ khóa Featured Snippet mới qua email với DataForSEO"
description: "Tự động hóa việc theo dõi từ khóa Featured Snippet mới của bạn hàng tuần, lưu vào Google Sheets và nhận báo cáo qua email - hoàn toàn không cần code."
slug: "theo-doi-tu-khoa-featured-snippet-moi-qua-email"
tags: [n8n, automation, no-code, seo, dataforseo]
keywords: [n8n workflow, tự động hóa seo, featured snippet, dataforseo, google sheets]
---

# 🚀 Theo dõi từ khóa Featured Snippet mới qua email với DataForSEO

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi phải theo dõi thủ công từ khóa Featured Snippet hàng tuần. Giới thiệu workflow như giải pháp tự động hóa hoàn chỉnh, tiết kiệm thời gian và nâng cao hiệu quả SEO.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 2-3 giờ mỗi tuần cho việc theo dõi thủ công
- Nhận báo cáo tự động hàng tuần về từ khóa Featured Snippet mới
- Dữ liệu được lưu trữ an toàn trong Google Sheets
- Thông báo tức thì qua email khi có từ khóa mới
- Hệ thống hoạt động liên tục 24/7 không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Workspace (cho Google Sheets và Gmail)
- Tài khoản DataForSEO (API Key và mật khẩu)
- Danh sách từ khóa hiện tại trong Google Sheets (theo định dạng mẫu)
- Danh sách domain mục tiêu trong Google Sheets (theo định dạng mẫu)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/13488](https://n8n.io/workflows/13488)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link trên vào ô nhập liệu
4. Click "Import" để hoàn tất quá trình

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Get previous keywords" và "Get targets"**:
   - Tạo kết nối Google Sheets OAuth2
   - Chọn spreadsheet chứa từ khóa hiện tại (theo [định dạng mẫu](https://docs.google.com/spreadsheets/d/1pRNkz1us8N_w_Sw-8axiMxUDu7to2tIVFXyY5W7gH3U/edit?gid=1392477424#gid=1392477424))
   - Chọn spreadsheet chứa danh sách domain mục tiêu (theo [định dạng mẫu](https://docs.google.com/spreadsheets/d/1pRNkz1us8N_w_Sw-8axiMxUDu7to2tIVFXyY5W7gH3U/edit?gid=0#gid=0))

2. **Node "Get ranked keywords"**:
   - Tạo kết nối DataForSEO API
   - Nhập API Key và mật khẩu từ tài khoản DataForSEO của bạn
   - Có thể điều chỉnh các tham số bổ sung nếu cần

3. **Node "Append keyword in sheet"**:
   - Sử dụng cùng kết nối Google Sheets như node "Get previous keywords"
   - Đảm bảo spreadsheet được chọn có cùng định dạng

4. **Node "Send a message"**:
   - Tạo kết nối Gmail OAuth2
   - Nhập địa chỉ email nhận báo cáo
   - Có thể chỉnh sửa nội dung email theo nhu cầu

5. **Node "Run every Monday"**:
   - Có thể điều chỉnh lịch chạy theo nhu cầu (mặc định chạy mỗi thứ Hai)

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute Node" trên node "Run every Monday" để test chạy dữ liệu mẫu
2. Kiểm tra kết quả trên Google Sheets và email
3. Sau khi xác nhận hoạt động bình thường, click vào nút "Activate" ở góc trên bên phải để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Slack để nhận thông báo tức thì khi có từ khóa mới
- Kết hợp với workflow khác để tự động tạo nội dung cho các từ khóa mới
- Thiết lập báo cáo định kỳ hàng tháng về hiệu suất Featured Snippet
- Tích hợp với các công cụ SEO khác để phân tích sâu hơn
- Thêm node để lưu log hoạt động của workflow

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian quý giá, tự động hóa quy trình theo dõi từ khóa Featured Snippet hàng tuần và nhận báo cáo tự động qua email. Hãy triển khai ngay để nâng cao hiệu quả SEO của bạn!