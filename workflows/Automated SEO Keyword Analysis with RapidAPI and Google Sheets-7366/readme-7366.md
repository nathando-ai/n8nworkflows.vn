---
title: "🚀 Tự động phân tích từ khóa SEO với RapidAPI & Google Sheets"
description: "Workflow n8n giúp tự động thu thập dữ liệu từ RapidAPI, phân tích từ khóa và lưu kết quả vào Google Sheets, giảm thiểu công việc thủ công và tăng hiệu quả nghiên cứu thị trường."
slug: "tu-dong-phan-tich-tu-khoa-seo-rapidapi-google-sheets"
tags: [n8n, automation, no-code, seo, rapidapi, google-sheets]
keywords: [n8n workflow, tự động hóa, phân tích từ khóa, SEO, RapidAPI]
---

# 🚀 Tự động phân tích từ khóa SEO với RapidAPI & Google Sheets

Bạn đang phải nhập liệu thủ công, gửi yêu cầu API, trích xuất dữ liệu và dán vào bảng tính?  
Workflow này sẽ **đưa toàn bộ quy trình** từ **gửi từ khóa** → **gọi API** → **định dạng dữ liệu** → **lưu vào Google Sheets** thành một chuỗi tự động 100% không cần code.  

:::info[Hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài phút nhập liệu thành vài giây tự động.  
- **Độ chính xác cao**: Trích xuất dữ liệu trực tiếp từ API, giảm lỗi nhập liệu.  
- **Tự động cập nhật**: Mỗi lần người dùng gửi form, dữ liệu mới được ghi vào Google Sheets ngay lập tức.  
- **Dễ dàng mở rộng**: Thêm các sheet, API hoặc kênh thông báo (Slack, Telegram) chỉ vài cú click.  
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **Google Sheets**: Tạo một bảng tính mới và tạo ba sheet:  
  1. `Keyword Insights`  
  2. `KeyWord Difficulty`  
  3. `SERP Result`  
- **Google API Credentials**: Tạo OAuth2 client trong Google Cloud Console, tải file JSON và import vào n8n dưới tên `googleApi`.  
- **RapidAPI Key**: Đăng ký tại RapidAPI, lấy API key và lưu vào biến môi trường hoặc nhập trực tiếp vào node `httpRequest`.  
- **Form**: Tạo một form (HTML, Typeform, Google Forms…) có hai trường `keyword` và `country`.  
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON của workflow từ link gốc: <https://n8n.io/workflows/7366>.  
2. Trong n8n, vào **Workflows** → **Import** → **Upload JSON**.  
3. Hoặc copy toàn bộ JSON và paste vào **n8n Editor** → **File** → **New** → **Import JSON**.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Tên node | Cấu hình cần chỉnh | Ghi chú |
|------|----------|---------------------|---------|
| 1 | `On form submission` | Trường `keyword`, `country` phải khớp tên trường trong form | Đảm bảo form gửi dữ liệu đúng định dạng JSON |
| 2 | `Global Storage` | `keyword`, `country` → `{{ $json["keyword"] }}`, `{{ $json["country"] }}` | Lưu trữ vào context để dùng trong các node tiếp theo |
| 3 | `Keyword Insights Request` | **HTTP Method**: POST, **URL**: `https://rapidapi.com/.../keyword-tool.php`, **Headers**: `x-rapidapi-key`, `x-rapidapi-host`, **Body**: JSON chứa `keyword`, `country` | Đặt RapidAPI key vào header |
| 4 | `KeyWord Difficulty Request` | Tương tự như node 3 nhưng URL: `https://rapidapi.com/.../keywordDifficulty.php` | |
| 5 | `Re-Format` | **Code**: `return items.map(item => ({ json: { broadMatchKeywords: item.json.broadMatchKeywords } }));` | Trích xuất mảng `broadMatchKeywords` |
| 6 | `Keyword Insights` | **Google Sheets Credentials**: `googleApi`, **Operation**: `append`, **Sheet**: `Keyword Insights`, **Columns**: `keyword`, `broadMatchKeywords` | Đảm bảo tên sheet đúng |
| 7 | `Re-Format 2` | **Code**: `return items.map(item => ({ json: { keywordDifficultyIndex: item.json.keywordDifficultyIndex } }));` | |
| 8 | `KeyWord Difficulty` | **Google Sheets Credentials**: `googleApi`, **Operation**: `append`, **Sheet**: `KeyWord Difficulty`, **Columns**: `keyword`, `keywordDifficultyIndex` | |
| 9 | `Re -Format 5` | **Code**: `return items.map(item => ({ json: { serpResults: item.json.serpResults } }));` | |
| 10 | `SERP Result` | **Google Sheets Credentials**: `googleApi`, **Operation**: `append`, **Sheet**: `SERP Result`, **Columns**: `keyword`, `serpResults` | |

> **Lưu ý**: Nếu bạn muốn lưu dữ liệu chi tiết hơn, mở rộng các trường trong các node `googleSheets` (ví dụ: `searchVolume`, `competition`, `cpc`).

### 3. Kích hoạt ⚡️
1. **Test run**: Chọn một dữ liệu mẫu (ví dụ: `keyword: "seo optimization"`, `country: "US"`), chạy workflow và kiểm tra Google Sheets.  
2. **Bật Active**: Khi mọi thứ hoạt động đúng, bật toggle `Active` ở góc trên bên phải.  
3. **Giám sát**: Kiểm tra logs trong n8n để phát hiện lỗi (đặc biệt là lỗi API key hoặc sheet name).

## ✍️ Mẹo & gợi ý nâng cao

:::tip[Thêm Slack thông báo]
- Thêm node `Slack` sau node `SERP Result`.  
- Gửi tin nhắn: `Keyword "{{ $json.keyword }}" đã được phân tích và lưu vào Google Sheets.`

:::tip[Ghi log vào Google Sheets]
- Thêm node `Google Sheets` với sheet `Logs`.  
- Ghi timestamp, status, error message.

:::tip[Định kỳ gửi báo cáo]
- Sử dụng node `Cron` để chạy workflow hàng ngày, lấy dữ liệu từ Google Sheets và gửi email qua `SendGrid` hoặc `Gmail`.

:::note[Định dạng dữ liệu]
- Nếu API trả về dữ liệu phức tạp, hãy mở rộng các node `Code` để parse sâu hơn (ví dụ: `JSON.parse`, `Object.entries`).

## 📌 Kết luận

Workflow này giúp các sếp **đưa công việc phân tích từ khóa SEO** từ giai đoạn thủ công sang **tự động hoàn toàn**.  
Bạn chỉ cần **đưa form** lên website, **đăng ký RapidAPI** và **định cấu hình Google Sheets** – mọi thứ sẽ được n8n xử lý, lưu trữ và báo cáo cho bạn.  

Hãy thử ngay hôm nay và cảm nhận sự khác biệt!