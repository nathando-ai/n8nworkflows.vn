---
title: "🚀 Tự động tải hóa đơn điện tử KSeF (Ba Lan) vào file Excel bằng n8n"
description: "Hướng dẫn chi tiết cách sử dụng n8n workflow để kết nối hệ thống hóa đơn điện tử KSeF của Ba Lan, xác thực API v2 và xuất dữ liệu hóa đơn tự động ra file XLSX."
slug: "tu-dong-tai-hoa-don-ksef-ba-lan-excel-n8n"
tags: [n8n, automation, ksef, invoice-processing, excel, api-integration]
keywords: [n8n workflow, ksef ba lan, tai hoa don dien tu, xuat excel n8n, tu dong hoa hoa don]
---

# 🚀 Tự động tải hóa đơn điện tử KSeF (Ba Lan) vào file Excel bằng n8n

Các doanh nghiệp hoạt động tại Ba Lan hoặc có đối tác tại đây chắc chắn đều quen thuộc với hệ thống hóa đơn điện tử quốc gia **KSeF (Krajowy System e-Faktur)**. Việc phải thủ công đăng nhập, tra cứu và tải từng hóa đơn mua vào, bán ra xuống để làm báo cáo kế toán là một "cực hình" tốn rất nhiều thời gian và dễ xảy ra sai sót. 

Giải pháp ư? Workflow n8n này sẽ giúp các sếp tự động hóa 100% quy trình gọi API xác thực phức tạp (v2 API) của KSeF, truy vấn danh sách hóa đơn theo khoảng thời gian tùy chọn và xuất toàn bộ dữ liệu ra một file Excel (`.xlsx`) gọn gàng chỉ bằng một cú click chuột!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các tác vụ dài hạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Không cần thao tác thủ công trên cổng thông tin KSeF.
- **Xác thực bảo mật thông minh**: Tự động mã hóa RSA-OAEP token, xử lý quy trình multi-step auth (Get Public Key, Challenge, Init, Redeem Token).
- **Dữ liệu chuẩn xác**: Trích xuất đầy đủ metadata hóa đơn (Số KSeF, Số hóa đơn, Ngày phát hành, NIP người bán/mua, Tiền NET, VAT, Gross, Loại hóa đơn).
- **Linh hoạt đầu ra**: Xuất trực tiếp file Excel (`.xlsx`) sẵn sàng để gửi cho bộ phận kế toán hoặc lưu trữ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản KSeF Ba Lan**: Đã đăng ký tại cổng [ksef.mf.gov.pl](https://ksef.mf.gov.pl).
- **KSeF Authorization Token**: Token được tạo từ hệ thống KSeF (Định dạng mẫu: `YYYYMMDD-XX-XXXXXXXXXX-XXXXXXXXXX-XX|nip-XXXXXXXXXX|hash`).
- **Mã số thuế NIP**: Mã số thuế 10 chữ số của doanh nghiệp các sếp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã nguồn JSON từ [n8n Workflow #13925](https://n8n.io/workflows/13925).
- Mở n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc dùng tổ hợp phím `Ctrl+V` để dán trực tiếp vào giao diện).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 14 nodes hoạt động tuần tự. Các sếp cần chú ý cấu hình kỹ các node sau:

- **Node `⚙️ Config` (Set)**: 
  - Mở node này và điền thông tin doanh nghiệp:
    - `nip`: Mã số thuế 10 chữ số của các sếp.
    - `authToken`: KSeF authorization token đã lấy từ cổng thông tin KSeF.
    - `startDate` / `endDate`: Khoảng thời gian cần lấy hóa đơn (định dạng chuẩn ISO 8601, ví dụ: `2024-01-01T00:00:00Z`).
    - `subjectType`: 
      - `Subject2`: Hóa đơn **mua vào** (các sếp là người mua).
      - `Subject1`: Hóa đơn **bán ra** (các sếp là người bán).

- **Chuỗi Node Xác thực (Authentication Flow v2 API)**:
  - Các node `Get Public Key`, `Get Challenge`, `Encrypt Token`, `Init Auth`, `Wait 2s`, `Check Auth Status`, `Redeem Token`, `Close Session` hoạt động tự động dựa trên script và cấu hình HTTP Request sẵn có. 
  - *Lưu ý kỹ:* `authenticationToken` ở bước khởi tạo là token tạm thời, workflow sẽ tự động đổi lấy `accessToken` chính thức ở bước Redeem Token để gọi API lấy danh sách hóa đơn.

- **Node `Write XLSX` (Spreadsheet File)**:
  - Node này nhận dữ liệu đã được làm sạch và định dạng từ node `Format for Spreadsheet` để tạo file nhị phân `.xlsx`. Các sếp có thể để cấu hình mặc định (`toFile`).

#### 3. Kích hoạt ⚡️
- Click vào nút **Test workflow** (sử dụng trigger `When clicking 'Test workflow'`) để chạy thử nghiệm lần đầu.
- Kiểm tra kết quả trả về tại node **Write XLSX** để đảm bảo file Excel đã được tạo thành công kèm theo dữ liệu.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để workflow sẵn sàng hoạt động theo lịch trình (nếu các sếp cấu hình thêm Schedule Trigger).

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động gửi Email cho kế toán**: Kết nối thêm node **Send Email** ngay sau node `Write XLSX` để tự động gửi file Excel hóa đơn hàng tháng cho bộ phận kế toán.
- **Lưu trữ đám mây**: Thay vì chỉ lưu cục bộ, các sếp có thể nối tiếp node **Google Drive** hoặc **OneDrive** để tự động upload file Excel lên folder chung của công ty.
- **Đồng bộ Database**: Thay thế hoặc mở rộng node ghi file Excel bằng node **PostgreSQL** hoặc **MySQL** để lưu trữ toàn bộ lịch sử hóa đơn vào cơ sở dữ liệu nội bộ phục vụ BI (Business Intelligence).

### 📌 Kết luận
Việc tự động hóa tải hóa đơn từ KSeF không chỉ giúp tiết kiệm hàng giờ làm việc thủ công mỗi tháng mà còn loại bỏ hoàn toàn rủi ro sai sót dữ liệu. Hãy áp dụng ngay workflow này để tối ưu hóa quy trình kế toán - tài chính cho doanh nghiệp của các sếp!