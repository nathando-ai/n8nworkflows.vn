---
title: "🌐 Tự Động Hóa Phân Tích Domain Chi Tiết Với WHOIS + GPT-5-Nano (Không Cần Code)"
description: "Workflow tự động hóa lấy thông tin WHOIS domain từ RapidAPI, phân tích bằng GPT-5-Nano và trả về kết quả dưới dạng card HTML đẹp mắt, tiết kiệm thời gian cho nghiên cứu thị trường và marketing. Chỉ cần 1 lần setup, hoạt động 24/7."
slug: "tieu-dong-hoa-phan-tich-domain-voi-whois-gpt-5-nano"
tags: [n8n, automation, market-research, ai-summarization, whois-lookup, rapidapi]
keywords: [n8n workflow domain analysis, tự động hóa phân tích domain, whois lookup tự động, gpt-5-nano n8n, nghiên cứu thị trường online]
---

# 🚀 **Tự Động Hóa Phân Tích Domain Chi Tiết Với WHOIS + GPT-5-Nano**

### **Giải quyết vấn đề gì?**
Các sếp thường phải **tìm kiếm thủ công thông tin WHOIS** của domain (ngày đăng ký, registrar, DNS, trạng thái) và **viết tóm tắt phân tích** bằng tay để đánh giá tiềm năng của một domain. Quá trình này **tốn thời gian, dễ sai sót**, và không thể thực hiện được **liên tục** cho nhiều domain.

**Workflow này tự động hóa toàn bộ quá trình:**
✅ **Lấy WHOIS domain** từ RapidAPI (API miễn phí hoặc trả phí).
✅ **Phân tích bằng GPT-5-Nano** (mô hình AI nhẹ của OpenAI) để tạo **tóm tắt ngắn gọn** về domain.
✅ **Trả về kết quả dưới dạng card HTML đẹp mắt**, hỗ trợ **dark mode**, với thông tin chi tiết như:
   - Ngày đăng ký, hết hạn
   - Registrar (công ty quản lý)
   - DNS và trạng thái domain
   - Phân tích AI về tiềm năng sử dụng

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** thay vì dùng phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tìm kiếm WHOIS thủ công, phân tích AI tự động hóa.
- **Chính xác & toàn diện**: Lấy dữ liệu từ API chính thống (RapidAPI) + phân tích AI.
- **Hiển thị chuyên nghiệp**: Kết quả trả về dưới dạng **card HTML đẹp mắt**, dễ chia sẻ và in ấn.
- **Hoạt động liên tục**: Chỉ cần **setup 1 lần**, workflow tự chạy khi có yêu cầu (Webhook).
- **Hỗ trợ nhiều ngôn ngữ**: Chỉ cần thay đổi biến `language` trong **OPTIONS node**.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản RapidAPI** (để lấy WHOIS domain):
   - [Đăng ký miễn phí tại RapidAPI](https://rapidapi.com/) (hoặc dùng API trả phí cho dữ liệu chính xác hơn).
   - **API Key** của RapidAPI (điền vào **HTTP Request1 node**).
   - **Endpoint WHOIS** (ví dụ: `https://whois.p.rapidapi.com/v1/domain/{domain}`).

2. **Tài khoản OpenAI** (để sử dụng GPT-5-Nano):
   - [Đăng ký OpenAI](https://platform.openai.com/) và lấy **API Key**.
   - Điền vào **credentials** của node `Message a model` (tên: `openAiApi`).

3. **Domain cần phân tích**:
   - Gửi request đến **Webhook URL** (sẽ được tạo khi import workflow) với tham số `domain` (ví dụ: `example.com`).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1: Import từ file JSON**
  1. Tải workflow từ [n8n.io](https://n8n.io/workflows/8672) (ấn **Export**).
  2. Trên n8n Editor, nhấn **Import** và chọn file JSON.
- **Cách 2: Copy/Paste JSON**
  1. Copy toàn bộ JSON từ [n8n.io](https://n8n.io/workflows/8672).
  2. Trên n8n Editor, nhấn **Import** > **Paste JSON**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Sau khi import, các sếp **phải cấu hình** các node sau:

| **Node**               | **Cấu hình cần thiết**                                                                 | **Lưu ý**                                                                 |
|------------------------|---------------------------------------------------------------------------------------|---------------------------------------------------------------------------|
| **Webhook**            | - Path đã được tự động tạo (`76654401-5166-4a5a-94df-fa3a2d986142`).                     | Không cần chỉnh, chỉ cần lưu ý URL Webhook để gọi request.             |
| **OPTIONS (Set)**      | Thêm các biến sau (điền giá trị):                                                 | Biến này **quan trọng nhất**, quyết định cách workflow hoạt động.         |
|                        | - `domain`: Domain cần phân tích (ví dụ: `example.com`).                           | **Không thể bỏ trống**, nếu không sẽ lỗi.                                |
|                        | - `language`: Ngôn ngữ phân tích (ví dụ: `vi` cho tiếng Việt).                      | Mặc định là `en` (Tiếng Anh).                                            |
|                        | - `apiKey`: API Key của RapidAPI (điền vào `HTTP Request1`).                        | Nếu không có, workflow sẽ lỗi khi gọi API WHOIS.                          |
|                        | - `search_web`: `true` (nếu muốn AI tra cứu thêm thông tin trên web).              | Mặc định `false` (không tra cứu).                                        |
| **HTTP Request1**      | - **URL**: `https://whois.p.rapidapi.com/v1/domain/{domain}` (thay `{domain}` bằng biến `{{$node["OPTIONS"].json["domain"]}}`). | Sử dụng **Expressions** để truyền domain từ `OPTIONS`.                     |
|                        | - **Headers**:                                                                       |                                                                           |
|                        |   - `x-rapidapi-key`: Điền **API Key** của RapidAPI.                              | **Bắt buộc**, nếu không API sẽ trả lỗi.                                  |
|                        |   - `x-rapidapi-host`: `whois.p.rapidapi.com`.                                     |                                                                           |
| **Message a model**    | - **Credentials**: Chọn `openAiApi` (đã cấu hình trước).                           | Nếu chưa có, tạo mới trong **Credentials** của n8n.                       |
|                        | - **Prompt**: Sử dụng **Expressions** để truyền WHOIS data + biến `language`.      | Ví dụ: `Analyze this WHOIS data in {{$node["OPTIONS"].json["language"]}} and summarize the key insights.` |                                                                           |
| **Respond to Webhook** | - **Response Type**: Chọn **HTML** để trả về card đẹp mắt.                         | Nếu chọn **JSON**, kết quả sẽ không đẹp.                                  |

#### **3. Kích hoạt ⚡️**
1. **Test run với dữ liệu mẫu**:
   - Gửi request đến **Webhook URL** (được tạo tự động) với payload:
     ```json
     {
       "domain": "example.com",
       "language": "vi",
       "search_web": false
     }
     ```
   - Kiểm tra kết quả trong **Respond to Webhook** để đảm bảo AI phân tích đúng.

2. **Bật Active workflow**:
   - Nhấn **Active** trên n8n Editor.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tự động phân tích nhiều domain**:
   - Sử dụng **n8n Cron Trigger** để gọi workflow định kỳ (ví dụ: mỗi ngày phân tích 10 domain).
   - **Cách làm**:
     - Tạo một **Cron Trigger** mới.
     - Kết nối với **Webhook** bằng cách truyền `domain` từ một **Google Sheet** hoặc **CSV**.

2. **Lưu log phân tích**:
   - Thêm node **n8n-nodes-base.manual** sau **Respond to Webhook** để lưu kết quả vào **Google Sheets** hoặc **Notion**.
   - **Cách làm**:
     - Sử dụng node **HTTP Request** để gửi data đến API của Google Sheets.
     - Ví dụ: `https://sheets.googleapis.com/v4/spreadsheets/{sheetId}/values/{range}?valueInputOption=RAW`.

3. **Gửi báo cáo định kỳ qua Email/Slack**:
   - Kết nối với **n8n-nodes-base.email** hoặc **n8n-nodes-base.slack** để gửi kết quả phân tích cho team.
   - **Cách làm**:
     - Sau khi **Respond to Webhook**, thêm node **Email** hoặc **Slack** với nội dung HTML từ kết quả AI.

4. **Cập nhật API Key tự động**:
   - Sử dụng **n8n-nodes-base.credentials** để lưu API Key của RapidAPI và OpenAI trong **Credentials**.
   - **Lợi ích**: Không cần chỉnh sửa workflow khi API Key hết hạn.

5. **Chuyển workflow sang mode "Batch Processing"**:
   - Nếu cần phân tích **nhiều domain cùng lúc**, thay vì Webhook, sử dụng **n8n-nodes-base.queue** để xử lý hàng đợi.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp trong việc nghiên cứu domain, giúp **tối ưu hóa quy trình marketing** và **cải thiện quyết định đầu tư**. Bằng cách tự động hóa **WHOIS lookup + phân tích AI**, các sếp có thể:
✔ **Nhận kết quả chuyên nghiệp** chỉ trong vài giây.
✔ **Chia sẻ dễ dàng** với team qua card HTML đẹp mắt.
✔ **Hoạt động 24/7** mà không cần can thiệp thủ công.

**Hành động ngay!**
1. **Setup VPS** (nếu chưa có) và cài n8n.
2. **Import workflow** và cấu hình API Keys.
3. **Test với domain** của mình và **bật Active** để tự động hóa!

---
**💡 Lưu ý cuối cùng**:
- Nếu muốn **mở rộng tính năng**, có thể kết hợp với **n8n-nodes-base.llm** (để sử dụng mô hình AI khác) hoặc **n8n-nodes-base.airtable** (để lưu kết quả vào Airtable).
- **Không bán workflow** (theo điều khoản của tác giả Oriol Seguí), nhưng hoàn toàn miễn phí sử dụng cho mục đích cá nhân hoặc thương mại **không thương mại**.

**Chúc các sếp thành công!** 🚀