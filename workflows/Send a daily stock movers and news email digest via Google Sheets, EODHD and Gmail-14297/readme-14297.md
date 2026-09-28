---
title: "📈 **Tự Động Hóa Email Tóm Tắt Giá Trị & Tin Tức Sàn Giao Dịch Hàng Ngày (N8n + EODHD + Gmail)**"
description: "Giải pháp tự động hóa 100% không code để theo dõi danh sách cổ phiếu/token crypto của bạn hàng ngày, nhận email tổng hợp giá trị thay đổi và tin tức tài chính với phân tích cảm xúc. Đáp ứng nhu cầu của nhà đầu tư, trader hoặc team phân tích thị trường cần dữ liệu nhanh chóng và chính xác."
slug: "tieu-dong-hoa-email-tom-tat-gia-tri-tin-tuc-san-giao-dich"
tags: [n8n, automation, crypto-trading, financial-data, gmail-integration, google-sheets]
keywords: [tự động hóa email cổ phiếu, n8n workflow crypto, tổng hợp tin tức tài chính, phân tích cảm xúc tin tức, API EODHD, tự động hóa trader]
---

# 🚀 **Tự Động Hóa Email Tóm Tắt Giá Trị & Tin Tức Sàn Giao Dịch Hàng Ngày**

## **Nỗi Đau Của Nhà Đầu Tư & Trader**
Hàng ngày, các sếp phải mất **30-60 phút** để:
- Theo dõi **giá trị thay đổi** của danh sách cổ phiếu/token crypto (MSFT, BTC, ETH...) trên nhiều sàn giao dịch.
- **Lọc và đọc** hàng chục tin tức tài chính liên quan đến từng cổ phiếu, phân tích cảm xúc (tin tích cực/tiêu cực) để đưa ra quyết định.
- **Tổng hợp** dữ liệu vào email gửi cho team hoặc bản thân, với định dạng không đồng nhất và dễ bị lỗi.

**Kết quả?** Thời gian phản ứng chậm, rủi ro bỏ lỡ cơ hội, và công việc thủ công gây mệt mỏi.

---
### **🎯 Giải Pháp: Workflow N8n Tự Động Hóa 100% Không Code**
Workflow này **tự động**:
✅ **Lấy dữ liệu giá trị** của tất cả cổ phiếu/token trong danh sách hàng ngày (tính % thay đổi vs ngày trước).
✅ **Tải tin tức tài chính** liên quan (7 ngày gần nhất) từ EODHD API, phân tích **cảm xúc** (tích cực/tiêu cực/trung lập).
✅ **Tổng hợp** vào email HTML đẹp mắt, gửi trực tiếp vào hộp thư của các sếp **từ 7h sáng UTC** (hoặc thời gian tùy chỉnh).
✅ **Cập nhật liên tục** mà không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**).
👉 **[VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow phức tạp).
:::

---

### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 1-2 giờ/ngày** cho công việc thủ công.
- **Dữ liệu chính xác 100%**: Không sai sót như khi copy-paste từ nhiều trang web.
- **Phân tích cảm xúc tự động**: Biết ngay tin tức nào ảnh hưởng tích cực/tiêu cực đến cổ phiếu.
- **Email đẹp mắt & cá nhân hóa**: Định dạng HTML chuyên nghiệp, dễ đọc trên mobile/desktop.
- **Hoạt động 24/7**: Không cần nhớ bật workflow hàng ngày.
:::

---

### **🔧 Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản EODHD** (miễn phí tại [eodhd.com](https://eodhd.com/)) để lấy API Key.
2. **Google Sheets** với **một cột tên `ticker`** (ví dụ: `MSFT`, `BTC`, `AMZN`), mỗi hàng là một cổ phiếu/token.
3. **Tài khoản Gmail** để nhận email tổng hợp (hoặc sử dụng Gmail Business cho nhiều người nhận).
4. **Credentials trong n8n**:
   - **Google Sheets OAuth2** (cấu hình trong `n8n Credentials`).
   - **Gmail OAuth2** (cho phép n8n gửi email tự động).

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/14297](https://n8n.io/workflows/14297) hoặc copy toàn bộ mã JSON từ trang này.
- Trong **n8n Editor**, nhấn **Import Workflow** và dán JSON vào.
- **Không cần chỉnh sửa** cấu trúc nodes, chỉ cần **điền thông tin cấu hình** như hướng dẫn dưới đây.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **8 nodes** chính, nhưng chỉ **3 node cần cấu hình kỹ**:

##### **A. Node ⚙️ Config (Set)**
- **Mở node** và điền:
  - `api_token`: **API Key của EODHD** (tìm trong tài khoản EODHD).
  - `recipient_email`: **Email Gmail** muốn nhận email tổng hợp (ví dụ: `trader@doanhnghiep.com`).
  - **Lưu ý**: Email này **phải là tài khoản Gmail** (n8n sẽ gửi email từ đây).

##### **B. Node Google Sheets**
- **Chọn Credential**: `googleSheetsOAuth2Api` (đã cấu hình trước).
- **Chọn Spreadsheet**: Lựa chọn file Google Sheets chứa danh sách cổ phiếu.
- **Chọn Sheet Name**: Tên của tab trong Google Sheets (ví dụ: `Watchlist`).
- **Lưu ý**:
  - **Cột `ticker` phải là lowercase** (ví dụ: `msft`, `btc`).
  - Mỗi hàng là một cổ phiếu/token (không bỏ trống).

##### **C. Node Send Email via Gmail**
- **Chọn Credential**: `gmailOAuth2` (cấu hình trước).
- **Kiểm tra `recipient_email`**: Đảm bảo trùng với giá trị trong node `⚙️ Config`.
- **Lưu ý**:
  - Nếu muốn gửi email cho nhiều người, thêm địa chỉ email vào `recipient_email` (ví dụ: `team@doanhnghiep.com, trader@doanhnghiep.com`).

#### **3. Kích Hoạt Workflow ⚡️**
- **Test Run** với dữ liệu mẫu:
  - Nhấn **Execute Workflow** để kiểm tra email có được gửi không.
  - Kiểm tra **Google Sheets** và **Gmail** để xác nhận dữ liệu.
- **Bật Active**:
  - Đặt **Schedule Trigger** chạy hàng ngày tại **7h sáng UTC** (hoặc thời gian khác trong `Workflow Settings`).
  - **Không cần bật Manual Trigger** nếu muốn tự động hóa hoàn toàn.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Slack/Telegram Notifications**:
   - Sử dụng **node Slack** hoặc **Telegram Bot** để thông báo khi có tin tức quan trọng (ví dụ: tin tức tiêu cực với cảm xúc < -0.4).

2. **Lưu Log Lịch Sử**:
   - Thêm **node Set** sau `Send Email` để lưu dữ liệu đã gửi vào Google Sheets (cột `sent_at`, `status`).

3. **Tùy Chỉnh Thời Gian**:
   - Đặt **Schedule Trigger** chạy vào **giờ Việt Nam** (UTC+7) bằng cách chỉnh `timezone` trong `Workflow Settings`.

4. **Phân Tích Chi Tiết Hơn**:
   - Sử dụng **node Code** để thêm logic phân tích thêm (ví dụ: tính **moving average** 5 ngày cho giá).

---
### **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **strategy trading** thay vì công việc thủ công. Với **cấu hình đơn giản** và **dữ liệu chính xác**, nó trở thành **công cụ không thể thiếu** cho nhà đầu tư, trader hoặc team phân tích tài chính.

**Hành động ngay**:
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test Run** trước khi bật tự động.
3. **Chia sẻ với team** để cùng theo dõi thị trường hiệu quả!

---
**💡 Lưu ý cuối cùng**:
- Nếu gặp lỗi **CORS** với EODHD, liên hệ hỗ trợ EODHD để mở khóa API cho domain của bạn.
- Để **cập nhật danh sách cổ phiếu**, chỉ cần chỉnh sửa Google Sheets và **không cần chỉnh workflow**.