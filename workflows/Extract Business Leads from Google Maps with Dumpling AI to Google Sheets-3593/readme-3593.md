---
title: "🚀 Tự Động Trích Xuất Khách Hàng Tiềm Năng Từ Google Maps với Dumpling AI và Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động tìm kiếm địa điểm trên Google Maps qua Dumpling AI và lưu trữ danh sách leads chuyên nghiệp vào Google Sheets."
slug: "trich-xuat-leads-google-maps-dumpling-ai-google-sheets"
tags: [n8n, automation, sales, marketing, ai, google-sheets]
keywords: [n8n workflow, trích xuất leads google maps, dumpling ai, tự động hóa marketing, google sheets n8n]
---

# 🚀 Tự Động Trích Xuất Khách Hàng Tiềm Năng Từ Google Maps với Dumpling AI và Google Sheets

Việc tìm kiếm và thu thập thông tin khách hàng tiềm năng (B2B Leads) từ Google Maps thủ công là một cơn ác mộng thực sự đối với các đội ngũ sales và marketing. Các sếp thường phải mất hàng giờ đồng hồ gõ từ khóa, copy từng tên quán, địa chỉ, số điện thoại, website rồi paste vào Excel. Quá tẻ nhạt, mất thời gian và dễ xảy ra sai sót!

Giải pháp ư? Workflow n8n này sẽ tự động hóa toàn bộ quy trình: gọi API tìm kiếm thông minh từ Dumpling AI, xử lý dữ liệu và lưu thẳng vào Google Sheets chỉ trong vòng một nốt nhạc.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Thu thập hàng trăm data địa điểm, nhà hàng, cửa hàng chỉ với một cú click hoặc lịch chạy tự động.
- **Dữ liệu chuẩn chỉnh, có cấu trúc:** Tự động lọc ra tên, địa chỉ, số điện thoại, website, đánh giá (rating) và đưa ngay vào Google Sheets.
- **Cá nhân hóa chiến dịch:** Nhanh chóng có trong tay danh sách leads chất lượng để chạy quảng cáo hoặc cold calling.
- **Hoạt động không mệt mỏi:** Dễ dàng tích hợp Schedule Trigger để quét data tự động hàng ngày/hàng tuần.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- Tài khoản Dumpling AI và API Key (hoặc Http Header Auth tương ứng).
- Tài khoản Google Workspace / Google Sheets có sẵn một trang tính (Google Sheet) để lưu dữ liệu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã nguồn JSON của workflow (hoặc tải file JSON từ n8n template #3593) và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 4 nodes chính, các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Trigger: Manual Test Run (`manualTrigger`)**: Dùng để test thủ công. Khi chạy thật, các sếp có thể thay thế node này bằng *Schedule Trigger* để tự động hóa định kỳ.
- **Search Google Maps via Dumpling AI (`httpRequest`)**:
  - Chọn hoặc tạo mới **Credentials** loại `httpHeaderAuth` với API Key của Dumpling AI.
  - Kiểm tra phần Body của HTTP Request để thay đổi từ khóa tìm kiếm (`search query`) theo ý muốn (mặc định đang để `"best+restaurants+in+New+York"`). Các sếp có thể đổi thành bất kỳ dịch vụ hoặc khu vực nào khác (ví dụ: `"spa+quan+1+hcm"`).
- **Split Places List for Processing (`splitOut`)**: Node này có nhiệm vụ tách mảng dữ liệu `places[]` khổng lồ thành từng dòng đơn lẻ để hệ thống xử lý mượt mà. Không cần chỉnh sửa gì nhiều ở node này.
- **Save Results to Google Sheet (Place Info) (`googleSheets`)**:
  - Chọn **Credentials** loại `googleSheetsOAuth2Api` và kết nối với tài khoản Google của các sếp.
  - Chọn đúng File (Spreadsheet) và Tab (Sheet Name) đã chuẩn bị sẵn để lưu data các trường như: tên, địa chỉ, số điện thoại, website, rating, v.v.
  - Đảm bảo các cột trong Google Sheet khớp với các trường dữ liệu mà Dumpling AI trả về.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để test chạy thử với dữ liệu mẫu.
- Kiểm tra lại Google Sheet xem data đã được đổ về đầy đủ chưa.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để bật chế độ tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động hóa theo lịch:** Thay thế node Manual Trigger bằng *Schedule Trigger* để hệ thống tự động quét leads mỗi sáng thứ Hai hàng tuần.
- **Nhận thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối workflow để bắn thông báo ngay về máy mỗi khi quét xong một danh sách leads mới.
- **Lọc trùng lặp:** Thêm một bước kiểm tra dữ liệu cũ trong Google Sheets trước khi ghi dòng mới để tránh bị trùng lặp leads.

### 📌 Kết luận
Việc khai thác khách hàng tiềm năng trên Google Maps chưa bao giờ dễ dàng và tự động đến thế. Hãy "lên đồ" ngay với workflow này để tối ưu hóa đội ngũ sales và bứt phá doanh số cho doanh nghiệp của các sếp nhé!