---
title: "🚀 Theo dõi danh tiếng thương hiệu với Gemini AI & Phân tích cảm xúc Google News gửi email"
description: "Tự động thu thập tin tức, phân tích cảm xúc bằng Gemini AI và gửi báo cáo chi tiết qua Gmail ngay khi có từ khóa mới trong Google Sheets."
slug: "theo-doi-danh-tieng-thuong-hieu-gemini-ai-google-news-email"
tags: [n8n, automation, no-code, AI, sentiment-analysis, email]
keywords: [n8n workflow, tự động hóa, phân tích cảm xúc, Gemini AI, Google News, email báo cáo]
---

# 🚀 Theo dõi danh tiếng thương hiệu với Gemini AI & Phân tích cảm xúc Google News gửi email

Doanh nghiệp ngày càng phụ thuộc vào hình ảnh thương hiệu trên mạng. Việc **theo dõi tin tức** liên quan, **đánh giá cảm xúc** của người dùng và **gửi báo cáo kịp thời** thường phải làm thủ công: mở hàng chục trang web, sao chép nội dung, phân tích cảm xúc bằng mắt, rồi soạn email.  
Quá trình này tốn **nhiều giờ**, dễ **bị sai sót**, và **không thể phản hồi nhanh** khi có khủng hoảng.

**Workflow n8n** này giải quyết 100 % công việc trên mà không cần viết một dòng code nào. Khi bạn thêm một từ khóa và email vào Google Sheets, hệ thống sẽ:

1. **Lấy tin tức mới** từ Google News (RSS).  
2. **Phân tích cảm xúc** của từng bài viết bằng **Gemini AI (PaLM)**.  
3. **Tổng hợp** kết quả, tính điểm trung bình và tạo báo cáo chi tiết.  
4. **Gửi email** tự động tới người nhận trong vòng vài phút.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động thu thập và phân tích tin tức trong 1‑2 phút.  
- **Độ chính xác cao**: Gemini AI cung cấp phân tích cảm xúc dựa trên mô hình ngôn ngữ tiên tiến.  
- **Báo cáo cá nhân hoá**: Mỗi từ khóa có một email riêng, nội dung được tùy chỉnh theo nhu cầu.  
- **Hoạt động liên tục**: Không cần can thiệp thủ công, workflow chạy 24/7 trên server.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Google Sheets**: Tài liệu có sheet tên `page1`, ô A1 = `keyword`, ô B1 = `email`.  
- **Tài khoản Google** với **OAuth2** để cấp quyền **Google Sheets Trigger** và **Gmail**.  
- **API key** của **Google Gemini (PaLM)** (đăng ký tại Google AI Studio).  
- **RSS Feed** của Google News (không cần credential, chỉ URL).  
- **n8n** đã cài đặt và có quyền truy cập internet để gọi API.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Đăng nhập vào n8n Dashboard.  
2. Click **"Import"** → **"Upload JSON"** và chọn file `track-brand-reputation.json` (hoặc copy toàn bộ JSON vào ô **Paste JSON**).  
3. Nhấn **"Import"**, workflow sẽ xuất hiện trên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Cấu hình cần chỉnh |
|------|------|--------------------|
| **Google Sheets Trigger** | Đọc dữ liệu khi có hàng mới được thêm. | - Dán URL của Google Sheet đã tạo.<br>- Chọn **Trigger on** → `Row Added`.<br>- Chọn credential **googleSheetsTriggerOAuth2Api**. |
| **RSS Read** | Lấy tin tức Google News dựa trên từ khóa. | - URL mẫu: `https://news.google.com/rss/search?q={{$json["keyword"]}}` (sử dụng biểu thức n8n). |
| **Edit Fields** (Set) | Định dạng lại dữ liệu từ RSS để chuẩn bị cho AI. | - Thêm trường `content` (nội dung mô tả) và `link` (URL). |
| **Limit** | Giới hạn số bài báo sẽ gửi tới Gemini (để giảm chi phí). | - **Maximum Items**: 5 (hoặc tùy nhu cầu). |
| **Message a model** (Google Gemini) | Gửi prompt tới Gemini để phân tích cảm xúc. | - Chọn credential **googlePalmApi**.<br>- Prompt mẫu: <br>```Bạn là chuyên gia phân tích cảm xúc. Đánh giá cảm xúc của đoạn văn sau (positive, neutral, negative) và cho điểm từ -1 đến 1. Nội dung: {{ $json["content"] }}``` |
| **Aggregate** | Tổng hợp kết quả từ các lần gọi AI. | - **Operation**: `Merge` → `Add` các trường `sentimentScore`. |
| **Code in JavaScript** | Tính điểm trung bình, tạo nội dung email. | - Sử dụng `items.map` để lấy `sentimentScore`, tính `average`, xây dựng `emailBody`. |
| **Send a message** (Gmail) | Gửi báo cáo tới email được chỉ định. | - Chọn credential **gmailOAuth2**.<br>- **To**: `{{$json["email"]}}`.<br>- **Subject**: `Báo cáo cảm xúc thương hiệu: {{$json["keyword"]}}`.<br>- **Body**: Dùng output của node **Code**. |

> **Lưu ý:** Đảm bảo mọi node đều **kết nối đúng credential** và **định dạng dữ liệu** (JSON) khớp nhau, đặc biệt phần `{{ }}` trong biểu thức n8n.

#### 3. Kích hoạt ⚡️
1. Nhấn **"Execute Workflow"** lần đầu để kiểm tra với một **keyword** và **email** mẫu.  
2. Kiểm tra hộp thư Gmail nhận được báo cáo.  
3. Khi mọi thứ ổn, bật **"Active"** (nút chuyển đổi ở góc trên bên phải) để workflow tự động chạy khi có hàng mới.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram**: Thêm node **Slack** hoặc **Telegram** sau node **Aggregate** để nhận cảnh báo ngay trên kênh nội bộ.  
- **Lưu log vào Google Sheets**: Dùng node **Google Sheets** (Write) để ghi lại ngày giờ, từ khóa, điểm cảm xúc trung bình, số bài báo.  
- **Báo cáo định kỳ**: Kết hợp **Cron** node để tổng hợp hàng ngày/tuần và gửi bản tổng hợp cho quản lý.  
- **Đa ngôn ngữ**: Thêm bước **Translate** (Google Translate node) trước khi gửi tới Gemini nếu từ khóa là tiếng nước ngoài.  
- **Kiểm soát chi phí**: Điều chỉnh node **Limit** hoặc **Batch Size** để giảm số lần gọi API Gemini.

### 📌 Kết luận
Với workflow này, các sếp có thể **giám sát danh tiếng thương hiệu** một cách **tự động, nhanh chóng và chính xác** chỉ bằng một vài thao tác thiết lập. Không còn lo lắng về việc bỏ lỡ tin tức tiêu cực hay phải dành hàng giờ để tổng hợp báo cáo. Hãy triển khai ngay hôm nay, để thương hiệu của bạn luôn được bảo vệ và phản hồi kịp thời!