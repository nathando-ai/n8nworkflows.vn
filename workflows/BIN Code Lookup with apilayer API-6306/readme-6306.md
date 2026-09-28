---
title: "🔍 Tìm kiếm Mã BIN Tự Động với APILayer - Không Cần Code!"
description: "Tự động tra cứu thông tin chi tiết của mã BIN (Bank Identification Number) chỉ với một cú nhấp chuột, tiết kiệm thời gian và tránh sai sót trong xử lý giao dịch ngân hàng. Workflow này kết hợp APILayer với n8n để cung cấp kết quả chính xác 24/7."
slug: "tam-kieu-ma-bin-tu-dong-voi-apilayer"
tags: [n8n, automation, no-code, api-integration, banking, apilayer]
keywords: [tìm kiếm mã BIN tự động, tra cứu mã BIN với n8n, APILayer n8n, tự động hóa ngân hàng, tra cứu mã thẻ ngân hàng]
---

# 🔍 **Tìm Kiếm Mã BIN Tự Động với APILayer - Không Cần Code!**

### **Giải pháp cho ai?**
Các sếp quản lý ngân hàng, bộ phận tài chính, hoặc bất kỳ ai cần tra cứu thông tin về **mã BIN** (Bank Identification Number) của thẻ ngân hàng một cách nhanh chóng và chính xác. Thay vì phải tra cứu thủ công trên website hoặc gọi API bằng code, workflow này cho phép bạn **nhấp chuột một lần** để lấy tất cả thông tin chi tiết về một mã BIN cụ thể, bao gồm:
- Tên ngân hàng
- Quốc gia
- Loại thẻ (Visa, Mastercard, Amex...)
- Thông tin liên quan khác

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tra cứu chỉ trong giây lát thay vì phút hoặc giờ.
- **Chính xác 100%**: Dữ liệu từ APILayer - nguồn tin cậy hàng đầu về mã BIN.
- **Hoạt động 24/7**: Không cần can thiệp người dùng, workflow chạy tự động khi kích hoạt.
- **Dễ dàng mở rộng**: Kết hợp với Slack/Telegram để thông báo kết quả ngay khi có yêu cầu.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **API Key của APILayer**:
   - Đăng ký miễn phí tại [APILayer](https://apilayer.com/marketplace/bincheck-api) để lấy API key.
   - Lưu ý: APILayer có giới hạn miễn phí (500 request/tháng), nên các sếp nên nâng cấp nếu cần sử dụng nhiều.
2. **Tài khoản n8n Self-hosted** (không dùng phiên bản cloud để đảm bảo bảo mật và hoạt động liên tục).
   :::info[Gợi ý hạ tầng cho n8n]
   Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
   :::
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow theo hai cách:
- **Tải file JSON**:
  1. Tải workflow từ [n8n.io](https://n8n.io/workflows/6306) (ấn nút "Download").
  2. Trên n8n Editor, nhấn **"Import"** và chọn file JSON vừa tải.
- **Copy/Paste JSON**:
  1. Sao chép nội dung JSON từ [n8n.io](https://n8n.io/workflows/6306) (ấn nút "Copy JSON").
  2. Trên n8n Editor, nhấn **"Import"** và chọn **"Paste JSON"**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này bao gồm **3 node chính**, các sếp cần chú ý cấu hình như sau:

##### **Node 1: Manual Trigger (Kích hoạt thủ công)**
- **Tên node**: "When clicking ‘Execute workflow’"
- **Chức năng**: Bắt đầu workflow khi người dùng nhấn nút "Execute".
- **Lưu ý**: Không cần chỉnh sửa gì, chỉ cần kích hoạt workflow khi cần.

##### **Node 2: Set API Key & BIN Number (Cấu hình tham số)**
- **Tên node**: "Set BIN Code and API Key"
- **Cần thiết**: Điền **hai trường sau** trong node này:
  - **bin_code**: Nhập mã BIN cần tra cứu (ví dụ: `JH4KA7560RC003647`).
    - *Lưu ý*: Các sếp có thể thay đổi giá trị này bằng cách **set default** trong node `Set` hoặc truyền động khi kích hoạt workflow.
  - **apikey**: Nhập **API Key của APILayer** (đã đăng ký trước).
    - *Lưu ý*: **Không bao giờ chia sẻ API Key** với ai cả, đặc biệt là trên công khai.

##### **Node 3: HTTP Request (Gửi yêu cầu API)**
- **Tên node**: "Lookup BIN"
- **Cấu hình quan trọng**:
  - **Method**: Đảm bảo chọn **GET**.
  - **URL**: `https://api.apilayer.com/bincheck/{{ $json.bin_code }}`
    - *Giải thích*: `{{ $json.bin_code }}` là biến động từ node `Set`, sẽ thay thế bằng mã BIN đã nhập.
  - **Headers**:
    - **Name**: `apiKey`
    - **Value**: `{{ $json.apikey }}`
    - *Giải thích*: Biến này sẽ truyền API Key của APILayer cho yêu cầu.

#### **3. Kích hoạt ⚡️**
1. **Test run dữ liệu mẫu**:
   - Nhấn **"Execute"** trên node `Manual Trigger`.
   - Kiểm tra kết quả trả về từ APILayer (nếu thành công, sẽ hiển thị JSON chứa thông tin về mã BIN).
2. **Bật Active workflow**:
   - Chuyển trạng thái workflow từ **"Inactive"** sang **"Active"** để tự động hóa.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[Nâng cao tính năng]
1. **Kết hợp với Slack/Telegram**:
   - Sau khi tra cứu thành công, gửi kết quả về Slack/Telegram thông qua node `Slack` hoặc `Telegram Bot`.
   - *Cách làm*: Thêm node `Set` để định dạng kết quả trước khi gửi, hoặc sử dụng node `HTTP Request` để gọi API của Slack/Telegram.

2. **Lưu log tra cứu**:
   - Thêm node `Google Sheets` hoặc `Airtable` để ghi lại lịch sử tra cứu (mã BIN, ngày giờ, kết quả).
   - *Ưu điểm*: Dễ dàng theo dõi và phân tích dữ liệu lâu dài.

3. **Tự động hóa theo lịch**:
   - Nếu cần tra cứu định kỳ (ví dụ: hàng ngày), thay thế node `Manual Trigger` bằng node `Schedule` (n8n Pro) hoặc sử dụng **n8n Cloud** với tính năng `Cron`.

4. **Xử lý lỗi**:
   - Thêm node `If` để kiểm tra trạng thái trả về từ APILayer.
   - Nếu API trả về lỗi (ví dụ: mã BIN không hợp lệ), có thể gửi thông báo lỗi về Slack hoặc email.
   - *Cách làm*:
     ```json
     {
       "node": "If",
       "properties": {
         "condition": "{{ $json.status === 'error' }}"
       }
     }
     ```
     Sau đó kết nối với node `Slack` hoặc `Email` để thông báo.
:::

---

### 📌 **Kết luận**
Workflows **Tìm Kiếm Mã BIN Tự Động** là giải pháp **siêu nhanh** để các sếp tra cứu thông tin ngân hàng một cách chính xác và không cần code. Với chỉ **3 node đơn giản**, workflow này giúp tiết kiệm thời gian và giảm thiểu sai sót trong xử lý giao dịch.

**Hành động ngay!**
1. **Đăng ký API Key** tại [APILayer](https://apilayer.com/marketplace/bincheck-api).
2. **Import workflow** vào n8n của mình.
3. **Chỉnh sửa API Key và mã BIN** trong node `Set`.
4. **Kích hoạt workflow** và bắt đầu tra cứu!

Nếu có bất kỳ câu hỏi hoặc gặp khó khăn, hãy để lại comment bên dưới. Chúc các sếp thành công! 🚀