---
title: "💰 **Tự Động Hóa Quản Lý Tài Chính Cá Nhân Với Telegram Bot + AI Gemini + Google Sheets**"
description: "Workflow tự động hóa hoàn toàn giúp các sếp theo dõi chi tiêu, phân tích hóa đơn, và trả lời câu hỏi tài chính bằng AI thông minh chỉ với Telegram. Tiết kiệm 10+ giờ/tháng và giảm 90% sai sót thủ công."
slug: "tieu-dong-hoa-quan-ly-tai-chinh-ca-nhan-telegram-gemini-sheets"
tags: [n8n, automation, no-code, ai-chatbot, google-sheets, google-gemini, telegram-bot]
keywords: [tự động hóa quản lý tài chính, bot telegram quản lý chi tiêu, google gemini n8n, lưu hóa đơn tự động, phân tích chi tiêu bằng ai]
---

# 🚀 **Tự Động Hóa Quản Lý Tài Chính Cá Nhân Với Telegram Bot + AI Gemini + Google Sheets**

### **🔥 Bạn đã bao giờ mệt mỏi vì:**
- **Nhập liệu hóa đơn thủ công** hàng ngày, dễ quên hoặc nhập sai?
- **Không biết chi tiêu ra sao** trong tháng, phải tra cứu hàng giờ trên Google Sheets?
- **Muốn phân tích chi tiêu** theo danh mục (ăn uống, giao thông, giải trí...) nhưng không có thời gian?
- **Sợ mất hóa đơn** vì quên lưu hoặc bị xóa trên điện thoại?

**Workflow này giải quyết tất cả!** Các sếp chỉ cần **gửi ảnh hóa đơn/PDF hoặc hỏi câu hỏi tài chính** qua Telegram, AI sẽ tự động:
✅ **Trích xuất thông tin** (ngày, số tiền, mô tả, danh mục) từ hóa đơn.
✅ **Lưu dữ liệu** vào Google Sheets và Google Drive (an toàn, không mất).
✅ **Trả lời câu hỏi tài chính** bằng tiếng Việt (ví dụ: *"Tôi đã chi bao nhiêu tiền ăn trong tháng?"*).
✅ **Tạo báo cáo tự động** theo tháng/quý với phân tích chi tiết.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS. Dưới đây là 2 lựa chọn ổn định và giá cả phải chăng:

👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
   - **Dung lượng:** 2GB RAM, 40GB SSD (đủ cho workflow này).
   - **Địa chỉ IP:** Đĩnh, không bị chặn (phù hợp cho Telegram API).
   - **Hỗ trợ 24/7** và cài đặt n8n 1 click.

👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)**
   - **Tốc độ cao**, phù hợp cho AI Gemini và Google Sheets.
   - **Không giới hạn băng thông**, đảm bảo workflow không bị treo.
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** không phải nhập liệu thủ công.
- **Giảm 90% sai sót** nhờ AI trích xuất tự động từ hóa đơn.
- **Phân tích chi tiêu chi tiết** theo danh mục, tháng, hoặc năm.
- **Báo cáo tự động** gửi qua Telegram hoặc email định kỳ.
- **An toàn dữ liệu** với lưu trữ trên Google Drive + Sheets.
- **Hỏi đáp tài chính bằng tiếng Việt** một cách tự nhiên (ví dụ: *"AI, tổng chi tiêu tháng này là bao nhiêu?"*).
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Telegram Bot**:
   - Tạo bot mới trên [@BotFather](https://t.me/BotFather) và lấy **API Token**.
   - Cài đặt bot vào nhóm hoặc chat cá nhân để test.

2. **Google Sheets**:
   - Tạo một **bảng Google Sheets mới** với cấu trúc 5 cột:
     - `Ngày` (Date)
     - `Số tiền (VND)` (Number)
     - `Mô tả` (Text)
     - `Danh mục` (Text, ví dụ: "Ăn uống", "Giao thông", "Giải trí")
     - `Hình ảnh` (Link Google Drive)
   - **Chia sẻ bảng** với quyền **"Sửa"** cho n8n (quyền OAuth2).

3. **Google Drive**:
   - Tạo một **thư mục mới** để lưu ảnh hóa đơn.
   - Lấy **ID thư mục** (có thể tìm bằng cách chia sẻ thư mục và sao chép link, sau đó lấy phần sau `/d/`).

4. **Google Gemini API**:
   - Đăng ký [Google AI Studio](https://makersuite.google.com/) và lấy **API Key**.
   - Chọn **Gemini Pro Vision** (phù hợp cho OCR và phân tích hình ảnh).

5. **N8n Self-hosted**:
   - Cài đặt n8n trên VPS (hướng dẫn [đây](https://docs.n8n.io/hosting/installation/)).
   - Cài đặt **n8n-nodes-langchain** (để sử dụng AI Gemini và Agent).

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có 2 cách import:
- **Tải file JSON** từ [n8n.io/workflows/10871](https://n8n.io/workflows/10871) và import vào n8n Editor.
- **Copy/paste JSON** từ link trên vào **Import Workflow** trong n8n.

:::note[Lưu ý]
- **Không xóa node nào** trong workflow, chỉ chỉnh sửa cấu hình.
- **Không cần cài thêm node** ngoài danh sách đã liệt kê (n8n sẽ tự động tải các node cần thiết).
:::

---

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Dưới đây là **danh sách node quan trọng** cần cấu hình:

| **Node**                     | **Cần chỉnh gì?**                                                                 | **Lưu ý**                                                                 |
|------------------------------|-----------------------------------------------------------------------------------|---------------------------------------------------------------------------|
| **Telegram Trigger**         | Điền **API Token** từ BotFather.                                                  | Chọn **Chat ID** là chat cá nhân hoặc nhóm bạn muốn bot hoạt động.       |
| **Google Sheets (Append row)** | Điền **ID Sheet** và **Tên Sheet** (ví dụ: "Quản lý chi tiêu").                  | Chọn **Sheet Name** chính xác trong bảng Google Sheets của bạn.          |
| **Google Drive (Upload file)** | Điền **ID Thư mục** để lưu ảnh hóa đơn.                                        | Lấy từ link chia sẻ thư mục (phần sau `/d/`).                           |
| **Google Gemini (lmChat)**    | Điền **API Key** từ Google AI Studio.                                            | Chọn **Model**: `gemini-pro` (hoặc `gemini-pro-vision` nếu cần OCR).       |
| **AI Agent**                 | Cấu hình **prompt** để AI phân loại chi tiêu (ví dụ: "Danh mục là gì?").         | Tham khảo [hướng dẫn cấu hình Agent](https://docs.n8n.io/nodes/n8n-nodes-base.agent/). |
| **Switch (Route)**           | Chọn **các trường hợp** (image, text, PDF) để AI xử lý.                          | Đảm bảo **tất cả trường hợp** (ảnh, văn bản, PDF) đều được định tuyến.   |
| **Calculator**               | Cấu hình **công thức** để tính tổng chi tiêu (ví dụ: `{{ $json["amount"] }}`).   | Sử dụng **JavaScript** trong node **Code** nếu cần tính toán phức tạp.   |

##### **Cách chỉnh node "Append row in sheet" (Google Sheets):**
1. Vào node **Append row in sheet**.
2. Điền:
   - **Spreadsheet ID**: Sao chép từ link Google Sheets (phần sau `/d/`).
   - **Sheet Name**: Tên sheet bạn muốn lưu dữ liệu (ví dụ: "Chi tiêu").
   - **Headers**: Đảm bảo trùng khớp với cột trong sheet (Ngày, Số tiền, Mô tả, Danh mục, Hình ảnh).
3. **Test run** với một dòng dữ liệu mẫu để kiểm tra.

##### **Cách chỉnh node "Google Gemini Chat Model":**
1. Vào node **Google Gemini Chat Model**.
2. Điền:
   - **API Key**: Từ Google AI Studio.
   - **Model**: `gemini-pro` (hoặc `gemini-pro-vision` nếu cần phân tích ảnh).
3. **Prompt mẫu** (có thể chỉnh sửa):
   ```
   Bạn là một trợ lý tài chính thông minh. Hãy phân tích hóa đơn và trả lời câu hỏi về chi tiêu.
   - Nếu là ảnh hóa đơn: Trích xuất ngày, số tiền (VND), mô tả, và danh mục (ăn uống, giao thông, giải trí...).
   - Nếu là câu hỏi tài chính: Trả lời bằng tiếng Việt và tham khảo dữ liệu trong Google Sheets.
   ```

##### **Cách chỉnh node "AI Agent":**
1. Vào node **AI Agent**.
2. Cấu hình **tools** (công cụ) cho AI:
   - **Google Sheets Tool**: Để AI truy cập dữ liệu.
   - **Calculator**: Để AI tính toán tổng chi tiêu.
   - **Memory Buffer**: Để AI nhớ các câu hỏi trước đó.
3. **Prompt mẫu**:
   ```
   Bạn là một trợ lý tài chính cá nhân. Hãy trả lời các câu hỏi về chi tiêu bằng tiếng Việt.
   - Nếu người dùng gửi ảnh hóa đơn: Trích xuất thông tin và lưu vào Google Sheets.
   - Nếu người dùng hỏi "Tôi đã chi bao nhiêu tiền ăn trong tháng?":
     + Truy cập Google Sheets để lấy dữ liệu.
     + Sử dụng công cụ Calculator để tính tổng.
     + Trả lời: "Tháng này bạn đã chi {{tổng}} VND cho ăn uống."
   ```

---

#### **3. Kích hoạt ⚡️**
1. **Test run** với dữ liệu mẫu:
   - Gửi **ảnh hóa đơn** hoặc **PDF** qua Telegram bot.
   - Gửi **câu hỏi tài chính** (ví dụ: *"AI, tổng chi tiêu tháng này là bao nhiêu?"*).
2. **Bật Active workflow** trong n8n Editor.

---
### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tự động gửi báo cáo tháng**:
   - Sử dụng **node Telegram (Send a text message)** để gửi báo cáo tổng hợp vào ngày cuối tháng.
   - **Prompt AI** để tạo báo cáo chi tiết:
     ```
     Hãy tạo một báo cáo tổng hợp chi tiêu tháng này với:
     - Tổng chi tiêu theo danh mục (ăn uống, giao thông, giải trí...).
     - Chi tiêu cao nhất trong tháng.
     - Dự báo chi tiêu tháng tiếp theo.
     ```

2. **Phân loại chi tiêu tự động**:
   - Chỉnh sửa **prompt của AI Agent** để phân loại chi tiêu theo **ngưỡng** (ví dụ: chi tiêu >500k là "Giải trí").
   - Sử dụng **node Switch** để chuyển hướng hóa đơn sang danh mục phù hợp.

3. **Lưu log hoạt động**:
   - Thêm **node StickyNote** để ghi lại các câu hỏi và phản hồi của AI.
   - Sử dụng **node Code (JavaScript)** để lưu log vào Google Sheets.

4. **Kết hợp với Slack/Email**:
   - Thay thế node Telegram bằng **Slack** hoặc **Email** để bot hoạt động trên nhiều nền tảng.
   - Cấu hình **webhook** cho Slack/Email trong node tương ứng.

5. **Cập nhật danh mục chi tiêu**:
   - Thêm **node Google Sheets (Get row)** để AI tham khảo danh sách danh mục trước khi phân loại.

---
### 📌 **Kết luận**
Workflow này **giải phóng thời gian** của các sếp khỏi công việc nhập liệu và phân tích tài chính thủ công. Với **AI Gemini + Telegram + Google Sheets**, bạn có một **trợ lý tài chính 24/7**, trả lời câu hỏi và quản lý chi tiêu một cách thông minh.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn trên.
2. **Test với 1-2 hóa đơn** để đảm bảo AI trích xuất chính xác.
3. **Bắt đầu sử dụng** và tiết kiệm **10+ giờ/tháng**!

---
**💡 Cần hỗ trợ?**
- **Hỏi đáp** trong [Community n8n](https://community.n8n.io/).
- **Tư vấn cài đặt VPS** tại [TinoHost](https://tino.vn/) hoặc [BNIX](https://my.bnix.one/).
- **Chia sẻ feedback** để tôi cập nhật hướng dẫn chi tiết hơn! 🚀