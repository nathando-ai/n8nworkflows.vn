---
title: "🚀 Tự động gửi email cảm ơn sau mua hàng cho Gumroad với Notion CRM & Gemini AI"
description: "Workflow n8n tự động nhận email mua hàng từ Gumroad, lưu khách hàng vào Notion và gửi email cảm ơn cá nhân hoá bằng Google Gemini AI."
slug: "tu-dong-gui-email-gumroad-notion-gemini"
tags: [n8n, automation, no-code, email, notion, gemini]
keywords: [n8n workflow, tự động hóa email, Gumroad, Notion CRM, Google Gemini AI]
---

# 🚀 Tự động gửi email cảm ơn sau mua hàng cho Gumroad với Notion CRM & Gemini AI

Bạn đã từng phải **đánh rơi hàng chục email mua hàng** trong hộp Gmail, sao chép thông tin khách hàng vào Notion, rồi viết tay email cảm ơn?  
Công việc này không chỉ tốn thời gian mà còn dễ gây lỗi, làm mất cơ hội tạo ấn tượng tốt với người mua.

**Workflow này** sẽ **lắng nghe email mua hàng của Gumroad**, **trích xuất thông tin khách hàng & sản phẩm**, **kiểm tra trùng lặp trong Notion**, **tạo bản ghi mới** và **gửi email cảm ơn cá nhân hoá** ngay lập tức bằng **Google Gemini AI** – **không cần viết một dòng code nào**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hoá toàn bộ quy trình từ nhận email → lưu CRM → gửi email.  
- **Độ chính xác 100 %**: Không còn nhập liệu thủ công, giảm lỗi sai.  
- **Cá nhân hoá**: AI Gemini tạo nội dung email dựa trên dữ liệu mua hàng, tăng mức độ gắn kết.  
- **Hoạt động liên tục**: Workflow chạy 24/7, không cần can thiệp sau khi thiết lập.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Gmail** (OAuth2) – để nhận và gửi email.  
- **Tài khoản Notion** + **API token** – để truy cập database khách hàng.  
- **Google Gemini (Palm) API key** – để sử dụng mô hình ngôn ngữ tạo nội dung.  
- **Gumroad**: Đảm bảo email mua hàng được chuyển tới hộp Gmail đã kết nối.  
- **n8n** (cloud hoặc self‑hosted) với ít nhất **9 nodes** (xem danh sách dưới).  
:::

## 📦 Danh sách các node trong workflow
| # | Tên node | Loại | Vai trò |
|---|----------|------|----------|
| 1 | **Gmail Trigger** | gmailTrigger | Lắng nghe email mua hàng từ Gmail. |
| 2 | **Get many database pages** | notion (getAll) | Lấy danh sách khách hàng hiện có để kiểm tra trùng lặp. |
| 3 | **If** | if | Kiểm tra xem khách hàng đã tồn tại chưa. |
| 4 | **Stop and Error** | stopAndError | Dừng workflow nếu khách đã có trong Notion. |
| 5 | **Create a database page** | notion (databasePage) | Tạo bản ghi khách hàng mới trong Notion. |
| 6 | **Code in JavaScript** | code | Xử lý dữ liệu email, trích xuất buyer & product info. |
| 7 | **AI Agent** | agent (LangChain) | Điều phối lời gọi tới mô hình Gemini. |
| 8 | **Google Gemini Chat Model** | lmChatGoogleGemini | Sinh nội dung email cảm ơn dựa trên prompt. |
| 9 | **Send a message** | gmail | Gửi email cảm ơn tới người mua. |

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. **Tải file JSON** của workflow (từ trang gốc https://n8n.io/workflows/11758).  
2. Mở **n8n Editor**, click **Import** → **Upload JSON** → Chọn file → **Import**.  
   *Hoặc* copy toàn bộ JSON, vào **n8n → New Workflow → Paste JSON**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
##### a. Gmail Trigger
- **Credentials**: Chọn `gmailOAuth2` đã kết nối.  
- **Mailbox**: Đặt `Inbox` (hoặc label riêng cho email Gumroad).  
- **Search Query**: `from:receipt@gumroad.com subject:"Your purchase"` (hoặc tùy chỉnh).

##### b. Get many database pages (Notion)
- **Credentials**: `notionApi`.  
- **Database ID**: Dán ID của database “Khách hàng” trong Notion.  
- **Operation**: `Get All`.  

##### c. If
- **Condition**: `{{$json["exists"]}}` (kết quả từ node “Get many database pages”).  
- **True** → **Stop and Error** (đánh dấu “Duplicate”).  
- **False** → tiếp tục tạo bản ghi.

##### d. Create a database page
- **Credentials**: `notionApi`.  
- **Database ID**: Same as ở bước b.  
- **Properties**: Map các trường:
  - `Name` → `{{$json["buyerName"]}}`
  - `Email` → `{{$json["buyerEmail"]}}`
  - `Product` → `{{$json["productName"]}}`
  - `Price` → `{{$json["price"]}}`
  - `Purchase Date` → `{{$json["purchaseDate"]}}`

##### e. Code in JavaScript
- **Input**: Email raw body từ Gmail Trigger.  
- **Script** (đã có sẵn) thực hiện:
  ```js
  const body = $json["body"];
  // Regex để lấy buyer, email, product, price, date
  // Trả về object {buyerName, buyerEmail, productName, price, purchaseDate}
  return [{ json: extracted }];
  ```
- Nếu muốn tùy chỉnh, chỉnh regex trong `code` node.

##### f. AI Agent + Google Gemini Chat Model
- **Agent**: Đặt `Prompt` như:
  ```
  Bạn là trợ lý AI, viết email cảm ơn ngắn gọn, thân thiện cho khách hàng {{buyerName}} đã mua {{productName}} với giá {{price}}. Đảm bảo nội dung:
  - Cảm ơn
  - Nhắc lại sản phẩm
  - Đề nghị hỗ trợ nếu có câu hỏi
  - Chữ ký của thương hiệu
  ```
- **Credentials**: `googlePalmApi` → dán API key từ Google Cloud (Gemini).  
- **Model**: `gemini-pro` (hoặc phiên bản mới nhất).  

##### g. Send a message (Gmail)
- **Credentials**: `gmailOAuth2`.  
- **To**: `{{$json["buyerEmail"]}}`.  
- **Subject**: `Cảm ơn bạn đã mua {{productName}}!`.  
- **Body**: Dùng output của node “Google Gemini Chat Model” (`{{$json["content"]}}`).  

##### h. Stop and Error
- Để lại mặc định, chỉ hiển thị thông báo “Khách hàng đã tồn tại – không gửi email”.

#### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn **Execute Workflow** → Kiểm tra log từng node, đặc biệt node “Code” và “Gemini”.  
2. Nếu mọi thứ ổn, bật **Active** (toggle ở góc phải).  
3. Kiểm tra thực tế bằng cách mua thử một sản phẩm trên Gumroad và xem email cảm ơn có tới hộp thư không.

### ✍️ Mẹo & gợi ý nâng cao
- **Gửi báo cáo hàng ngày**: Thêm node Google Sheets để ghi lại số lượng email đã gửi.  
- **Thông báo Slack/Telegram**: Khi có khách hàng mới, dùng node Slack/Telegram để gửi tin nhắn cho team bán hàng.  
- **Lưu log chi tiết**: Dùng node **Write Binary File** để lưu toàn bộ payload vào Google Drive hoặc S3 cho mục đích audit.  
- **A/B testing nội dung**: Tạo 2 prompt khác nhau trong AI Agent, dùng node **If** dựa trên `productCategory` để chọn nội dung phù hợp.

### 📌 Kết luận
Với workflow này, các sếp có thể **tự động hoá hoàn toàn quy trình sau mua hàng**: từ nhận email, lưu CRM, tới gửi email cảm ơn cá nhân hoá bằng AI.  
Cài đặt nhanh trong **5‑10 phút**, chạy 24/7, giúp tăng trải nghiệm khách hàng và giảm tải công việc thủ công.  
Hãy **import ngay**, cấu hình các credentials và để n8n làm việc thay bạn! 🚀