---
title: "🚀 Tự động xuất danh mục đầu tư Spot trên Binance vào Google Sheets mỗi ngày với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy dữ liệu danh mục đầu tư crypto từ sàn Binance Spot và đồng bộ trực tiếp vào Google Sheets hoàn toàn miễn phí."
slug: "xuat-danh-muc-binance-spot-vao-google-sheets"
tags: [n8n, automation, crypto, binance, google-sheets, trading, no-code]
keywords: [n8n workflow, export binance portfolio, google sheets automation, crypto trading n8n, tự động hóa crypto]
---

# 🚀 Tự động xuất danh mục đầu tư Spot trên Binance vào Google Sheets mỗi ngày

Các sếp là trader, nhà đầu tư crypto và đang quản lý danh mục tài sản trên Binance? Chắc hẳn các sếp đã quen thuộc với việc mở app liên tục, tính toán thủ công hoặc copy/paste dữ liệu số dư vào file Excel/Google Sheets để theo dõi lời lỗ (PnL) theo ngày. Việc này vừa mất thời gian, vừa dễ sai sót và thiếu tính trực quan để phân tích dài hạn.

Đừng lo, bài viết này sẽ hướng dẫn các sếp cách "lên đồ" một workflow n8n cực kỳ xịn sò, tự động hóa 100% quy trình lấy dữ liệu tài sản Binance Spot và đẩy thẳng vào Google Sheets theo lịch trình cố định. Không cần code phức tạp, chỉ cần vài phút cài đặt là hệ thống tự chạy 24/7!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Không cần thao tác thủ công, dữ liệu cập nhật đều đặn mỗi ngày.
- **Quản lý tài sản chuyên nghiệp:** Có ngay một bảng Google Sheets tổng hợp số dư ví Spot để vẽ biểu đồ tăng trưởng tài sản.
- **Tiết kiệm thời gian:** Dành thời gian nghiên cứu thị trường thay vì ngồi nhập liệu.
- **Hoạt động không nghỉ:** Chạy ngầm 24/7 trên server riêng cực kỳ ổn định và bảo mật.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị sẵn các "vũ khí" sau:
1. **Server n8n:** Đã cài đặt sẵn n8n (Self-hosted hoặc n8n Cloud).
2. **Tài khoản Binance:** Cần tạo sẵn **API Key** và **Secret Key** từ tài khoản Binance (nhớ phân quyền chỉ đọc - Read Only để đảm bảo an toàn tuyệt đối cho tài sản).
3. **Google Sheets:** Tạo sẵn một file Google Sheets với các tiêu đề cột phù hợp (Ví dụ: Ngày, Tên Token, Số lượng, Giá trị...).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ [n8n Workflow #13512](https://n8n.io/workflows/13512).
- Copy toàn bộ nội dung JSON và dán trực tiếp vào giao diện n8n Editor của các sếp (chọn Import từ clipboard).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này sử dụng sự kết hợp của các node chính sau đây, các sếp cần chú ý cấu hình kỹ:
- **Schedule Trigger (`n8n-nodes-base.scheduleTrigger`):** Cấu hình thời gian chạy định kỳ (ví dụ: Chạy mỗi ngày 1 lần vào lúc 00:00 UTC).
- **Crypto / HTTP Request (`n8n-nodes-base.crypto` / `n8n-nodes-base.httpRequest`):** Dùng để gọi API của Binance, ký (sign) request bằng API Key & Secret Key để lấy thông tin số dư tài khoản Spot. Các sếp nhớ tạo Credentials kiểu Header Auth hoặc Custom API cho phần này.
- **Set, Filter & SplitOut (`n8n-nodes-base.set`, `n8n-nodes-base.filter`, `n8n-nodes-base.splitOut`):** Các node xử lý dữ liệu trung gian, lọc ra các đồng coin có số dư lớn hơn 0 để tránh làm loãng bảng thống kê.
- **Google Sheets (`n8n-nodes-base.googleSheets`):** Kết nối tài khoản Google của các sếp, chọn đúng file Google Sheets và Sheet Name đã chuẩn bị để ghi dữ liệu mới vào hàng cuối cùng (Append row).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử nghiệm với dữ liệu thực tế từ Binance xem dữ liệu có đẩy vào Google Sheets chuẩn chỉnh chưa.
- Sau khi test thành công, bật nút **Active** ở góc trên bên phải để workflow chính thức tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống quản lý tài sản trở nên "bá đạo" hơn, các sếp có thể mở rộng workflow bằng cách:
- **Tích hợp Telegram/Slack:** Thêm một node Telegram để nhận tin nhắn báo cáo tổng tài sản ngay lập tức mỗi khi workflow chạy xong.
- **Tính toán PnL:** Kết hợp thêm các hàm trong Google Sheets để quy đổi toàn bộ tài sản sang USDT hoặc VND, tính phần trăm tăng trưởng theo tuần/tháng.
- **Lưu log lỗi:** Thêm nhánh xử lý lỗi (Error Trigger) để nếu API Binance có sự cố, hệ thống sẽ bắn tin nhắn cảnh báo cho các sếp ngay lập tức.

### 📌 Kết luận
Việc quản lý tài chính và danh mục đầu tư crypto chưa bao giờ dễ dàng đến thế khi kết hợp sức mạnh của n8n và Google Sheets. Hãy tự tay setup ngay workflow này để tối ưu hóa thời gian và làm chủ dòng vốn của mình các sếp nhé!