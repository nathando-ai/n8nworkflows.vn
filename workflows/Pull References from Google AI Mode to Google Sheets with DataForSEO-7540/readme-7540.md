---
title: "🤖 Tự Động Lấy Dữ Liệu AI Mode Google vào Google Sheets - Theo Dõi Xếp Hạng AI Miễn Phí"
description: "Workflow tự động hóa 100% không code để lấy tất cả nguồn tham khảo từ Google AI Mode cho từ khóa của bạn, lưu vào Google Sheets để theo dõi hiệu suất website trong kết quả AI. Chỉ cần chạy 1 lần/7 ngày!"
slug: "tieu-ly-ai-mode-google-vao-google-sheets"
tags: [n8n, automation, ai-summarization, dataforseo, google-sheets, seo-tracking]
keywords: [tự động hóa n8n, lấy dữ liệu google ai mode, theo dõi xếp hạng ai, google sheets api, dataforseo api, seo tự động]
---

# 🚀 **Tự Động Lấy Dữ Liệu AI Mode Google vào Google Sheets - Theo Dõi Xếp Hạng AI Miễn Phí**

### **Giải quyết vấn đề gì?**
Các sếp SEO đang phải **thủ công** tra cứu kết quả AI Mode của Google cho từng từ khóa, sao chép nguồn tham khảo (title, URL, domain) vào Google Sheets để theo dõi. **Công việc này tốn thời gian, dễ sai sót và không thể thực hiện liên tục**. Workflow này **tự động hóa toàn bộ quá trình** chỉ trong **5 node**, giúp các sếp:
- **Lấy tất cả nguồn tham khảo** từ AI Mode Google cho từ khóa của mình.
- **Lưu dữ liệu tự động** vào Google Sheets với định dạng chuẩn (Source, Domain, URL, Title, Text).
- **Theo dõi xếp hạng AI** của website một cách chính xác và liên tục (chỉ cần chạy 1 lần/7 ngày).

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không phải tra cứu thủ công hàng tuần.
✅ **Dữ liệu chính xác**: Tránh sai sót khi sao chép từ kết quả AI Mode.
✅ **Theo dõi liên tục**: Cập nhật tự động mỗi 7 ngày (hoặc thời gian bạn thiết lập).
✅ **Dễ dàng phân tích**: Dữ liệu sẵn sàng trong Google Sheets để export, visualize hoặc phân tích SEO.
✅ **Miễn phí (nếu tự host)**: Không phụ thuộc vào API trả phí.
:::

---
### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản DataForSEO**:
   - API Key từ [DataForSEO](https://dataforseo.com/) (đăng ký miễn phí để lấy API Key).
   - **Tham số bắt buộc**:
     - `Keyword` (ví dụ: "tự động hóa n8n").
     - `Location` (ví dụ: "Việt Nam").
     - `Language` (ví dụ: "vi-VN").

2. **Google Sheets**:
   - Một bảng Google Sheets **có sẵn các cột**: `Source`, `Domain`, `URL`, `Title`, `Text`.
   - **Quản lý quyền**:
     - Chia sẻ bảng với email OAuth2 của n8n (nếu self-hosted).
     - Nếu dùng n8n Cloud, chọn `googleSheetsOAuth2Api` trong credentials.

3. **N8n Setup**:
   - **Self-hosted** (khuyến nghị) để lưu trữ dữ liệu an toàn và không giới hạn chạy.
   - Nếu dùng **n8n Cloud**, lưu ý hạn chế số lần chạy/ngày.
:::

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/7540](https://n8n.io/workflows/7540) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ link trên và paste vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **5 node chính**, các sếp cần chú ý cấu hình sau:

##### **Node 1: ScheduleTrigger (Run every 7 days)**
- **Thời gian chạy**: Mặc định là **7 ngày/lần** (có thể điều chỉnh trong `cron`).
- **Lưu ý**:
  - Nếu dùng **n8n Cloud**, hạn chế số lần chạy/ngày để tránh vượt ngưỡng miễn phí.
  - Đối với **self-hosted**, có thể chạy liên tục (ví dụ: `0 0 * * *` để chạy hàng ngày).

##### **Node 2: Get Google AI Mode SERP Data (DataForSEO)**
- **Credentials**: Chọn `dataForSeoApi` (đã cấu hình API Key từ DataForSEO).
- **Key Parameters**:
  - `operation`: `get-google-ai-mode-serp` (không thay đổi).
  - `resource`: `serp` (không thay đổi).
- **Tham số bắt buộc**:
  - **Keyword**: Điền từ khóa bạn muốn theo dõi (ví dụ: "tự động hóa n8n").
  - **Location**: Địa điểm (ví dụ: "Vietnam").
  - **Language**: Ngôn ngữ (ví dụ: "vi-VN").
  - **Max Results**: Giới hạn số kết quả (mặc định là 10, có thể tăng lên 50).

##### **Node 3 & 4: SplitOut (items & references)**
- **Chức năng**: Tách dữ liệu thành các phần tử riêng lẻ để xử lý.
- **Lưu ý**:
  - Node này **không cần chỉnh sửa** (n8n tự động phân tách).
  - Nếu dữ liệu không phân tách đúng, kiểm tra **Node 2** có trả về format JSON chuẩn không.

##### **Node 5: Record references to Google Sheets (GoogleSheets)**
- **Credentials**: Chọn `googleSheetsOAuth2Api` (đã cấu hình OAuth2 từ Google).
- **Key Parameters**:
  - `operation`: `append` (thêm dữ liệu mới vào cuối bảng).
  - **Sheet Name**: Chọn tên bảng Google Sheets đã chuẩn bị.
  - **Range**: Điền tên cột (ví dụ: `Sheet1!A1:E1000`).
- **Lưu ý**:
  - **Cột trong Google Sheets phải trùng khớp** với dữ liệu trả về từ DataForSEO:
    - `Source` → Nguồn tham khảo (title).
    - `Domain` → Domain của URL.
    - `URL` → Link nguồn.
    - `Title` → Tiêu đề AI Mode.
    - `Text` → Nội dung tóm tắt (nếu có).
  - Nếu cột không trùng, dữ liệu sẽ không lưu được.

---
#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Chạy **manual test** để kiểm tra dữ liệu trả về từ DataForSEO và lưu vào Google Sheets.
   - Kiểm tra **Google Sheets** có xuất hiện dữ liệu mới không.
2. **Active Workflow**:
   - Sau khi test thành công, **bật Active** để workflow chạy tự động theo lịch.

---
### ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁCH LÀM NÂNG CAO]
1. **Lưu log dữ liệu**:
   - Thêm **Node `Set`** sau `GoogleSheets` để lưu dữ liệu vào biến hoặc file JSON cho phân tích sau này.
   - Ví dụ: Lưu vào `{{ $json("data") }}` để export sau.

2. **Gửi báo cáo định kỳ**:
   - Kết hợp với **Slack/Email** để thông báo khi có dữ liệu mới.
   - Sử dụng **Node `Slack`** hoặc **Node `Email`** sau `GoogleSheets` để gửi thông báo tự động.

3. **Tự động cập nhật nhiều từ khóa**:
   - Sử dụng **Node `Set`** trước `DataForSEO` để truyền danh sách từ khóa từ Google Sheets.
   - Ví dụ: Một cột `Keywords` trong Google Sheets chứa danh sách từ khóa, workflow sẽ lấy tất cả và xử lý.

4. **Lọc dữ liệu theo domain**:
   - Thêm **Node `Function`** để lọc chỉ các nguồn thuộc domain của bạn (ví dụ: chỉ lấy `.com.vn`).
   - Cú pháp:
     ```javascript
     $input.all().map(item => {
       if (item.domain.includes("com.vn")) {
         return item;
       }
     }).filter(item => item !== undefined);
     ```

5. **Tích hợp với Google Data Studio**:
   - Sau khi dữ liệu lưu vào Google Sheets, **tạo báo cáo** trong Google Data Studio để visualize xếp hạng AI.
   - Cài đặt **Data Source** từ Google Sheets và tạo dashboard theo dõi.
:::

---
### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp SEO khỏi công việc thủ công tra cứu AI Mode, đồng thời **cung cấp dữ liệu chính xác** để theo dõi hiệu suất website trong kết quả AI. **Chỉ cần import, cấu hình 5 phút và chạy tự động mỗi 7 ngày**, các sếp sẽ có **báo cáo xếp hạng AI hoàn chỉnh** sẵn sàng phân tích.

👉 **Hành động ngay**:
1. **Đăng ký DataForSEO** (miễn phí) để lấy API Key: [https://dataforseo.com/](https://dataforseo.com/).
2. **Chuẩn bị Google Sheets** với cột `Source`, `Domain`, `URL`, `Title`, `Text`.
3. **Import workflow** và chạy **test** để kiểm tra.
4. **Bật Active** và theo dõi xếp hạng AI của mình mỗi tuần!

---
:::note[CHÚ Ý]
- Nếu dùng **n8n Cloud**, lưu ý hạn chế số lần chạy/ngày để tránh vượt ngưỡng miễn phí.
- Đối với **self-hosted**, các sếp có thể **cài n8n trên VPS** để lưu trữ dữ liệu an toàn và không giới hạn chạy.
:::

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::