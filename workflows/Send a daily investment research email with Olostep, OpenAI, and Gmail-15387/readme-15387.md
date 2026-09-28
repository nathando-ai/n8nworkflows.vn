---
title: "📈 Tự Động Hóa Báo Cáo Nghiên Cứu Đầu Tư Hàng Ngày Với Olostep, OpenAI & Gmail (Không Code)"
description: "Workflow tự động hóa gửi báo cáo nghiên cứu đầu tư hàng ngày cho các sếp đầu tư, tích hợp Olostep để tra cứu tin tức thị trường, OpenAI để tổng hợp và Gmail để gửi báo cáo định dạng HTML. Tiết kiệm 5+ giờ/tháng và giảm thiểu sai sót."
slug: "tieu-dong-hoa-bao-cao-nghien-cuu-dau-tu-hang-ngay"
tags: [n8n, automation, crypto-trading, ai-summarization, gmail-integration]
keywords: [n8n workflow đầu tư, tự động hóa báo cáo tài chính, Olostep + OpenAI, gửi email tự động hóa, nghiên cứu thị trường crypto]
---

# 🚀 **Tự Động Hóa Báo Cáo Nghiên Cứu Đầu Tư Hàng Ngày Với Olostep, OpenAI & Gmail**

### **Giải quyết vấn đề gì?**
Các sếp đầu tư thường phải mất **30-60 phút/ngày** để:
- Tra cứu tin tức thị trường từ nhiều nguồn (Bloomberg, Reuters, CoinDesk...).
- Tổng hợp thông tin về các cổ phiếu/crypto trong danh sách theo dõi.
- Viết báo cáo và gửi cho đội ngũ hoặc bản thân.

**Workflow này tự động hóa toàn bộ quy trình** bằng cách:
✅ **Tra cứu tin tức** từ Olostep (không cần viết code).
✅ **Tổng hợp báo cáo** bằng OpenAI (GPT-5.4-mini) với ngữ điệu chuyên nghiệp.
✅ **Gửi email định dạng HTML** qua Gmail, có thể mở trên mobile/desktop.

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 5+ giờ/tháng**: Không cần tra cứu thủ công mỗi ngày.
- **Báo cáo chính xác & cá nhân hóa**: Dữ liệu từ nhiều nguồn được tổng hợp logic.
- **Hoạt động 24/7**: Gửi báo cáo tự động vào giờ mở thị trường (thời gian tùy chỉnh).
- **Định dạng chuyên nghiệp**: Email HTML đẹp mắt, dễ đọc trên mọi thiết bị.
- **Cập nhật động**: Thêm/bỏ tickers trong danh sách theo dõi mà không cần sửa code.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản & API Keys**:
   - [Olostep](https://olostep.com/) (đăng ký miễn phí để lấy API Key).
   - [OpenAI](https://platform.openai.com/) (tạo API Key từ tài khoản Pro/Pay-as-you-go).
   - [Gmail](https://mail.google.com/) (tạo ứng dụng mật khẩu 2FA hoặc sử dụng OAuth 2.0).

2. **Danh sách tickers đầu tư**:
   - Danh sách các mã cổ phiếu/crypto cần theo dõi (ví dụ: `AAPL, BTC/USD, MSFT`).
   - Email nhận báo cáo (của chính sếp hoặc team).

3. **Hệ thống n8n**:
   - Cài đặt n8n trên **VPS riêng** (Self-hosted) để workflow hoạt động 24/7.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

---

## 🚀 **Cách Import & Lưu ý khi "Lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Từ file JSON**
1. Tải workflow từ [n8n.io/workflows/15387](https://n8n.io/workflows/15387) (chọn "Download JSON").
2. Mở n8n Editor → Nhấn **"Import"** → Chọn file JSON vừa tải.
3. Chọn **"Create new workflow"** và nhấn **"Import"**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Tải file JSON từ link trên và copy toàn bộ nội dung.
2. Trong n8n Editor, nhấn **"Import"** → Chọn **"Paste JSON"** và dán nội dung.
3. Nhấn **"Import"** để tạo workflow mới.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow có **9 node** quan trọng, các sếp cần cấu hình như sau:

#### **🔹 Node 1: "Weekday Market Open Trigger" (scheduleTrigger)**
- **Cấu hình**:
  - **Schedule**: Chọn ngày trong tuần (ví dụ: **Thứ 2 đến Thứ 6**) và giờ mở thị trường (ví dụ: **8:00 AM**).
  - **Timezone**: Chọn timezone phù hợp (ví dụ: `Asia/Ho_Chi_Minh`).
  - **Active**: Bật để workflow chạy tự động hàng ngày.

#### **🔹 Node 2: "Investment Watchlist" (set)**
- **Cấu hình**:
  - **Input Data**: Nhập danh sách tickers dưới dạng JSON:
    ```json
    [
      {"ticker": "AAPL", "email": "sếp@example.com"},
      {"ticker": "BTC/USD", "email": "sếp@example.com"},
      {"ticker": "MSFT", "email": "sếp@example.com"}
    ]
    ```
  - **Lưu ý**: Thay đổi `email` thành địa chỉ nhận báo cáo.

#### **🔹 Node 3: "Olostep Search - Investment Sources" (olostepScrape)**
- **Cấu hình**:
  - **API Key**: Điền API Key từ Olostep (tạo tại [dashboard Olostep](https://olostep.com/dashboard)).
  - **Query Parameters**:
    - `query`: Thay đổi thành từ khóa tra cứu (ví dụ: `"{{$node["Investment Watchlist"].json["ticker"]}} stock news"`).
    - `limit`: Số kết quả trả về (gợi ý: `5`).
  - **Lưu ý**: Olostep hỗ trợ tra cứu tin tức từ nhiều nguồn như Bloomberg, Reuters, CoinDesk...

#### **🔹 Node 4: "OpenAI - Create Full Watchlist Email Report" (openAi)**
- **Cấu hình**:
  - **API Key**: Điền API Key từ OpenAI.
  - **Model**: Chọn `gpt-5.4-mini` (hoặc `gpt-4` nếu có).
  - **Prompt**: Sử dụng template mặc định, nhưng các sếp có thể tùy chỉnh:
    ```plaintext
    You are an investment analyst. Summarize the latest news for {{$node["Investment Watchlist"].json["ticker"]}} in bullet points.
    Include:
    1. Key events from the past 24 hours.
    2. Price movement (if available).
    3. Analyst recommendations (if any).
    Keep it concise and professional.
    ```
  - **Temperature**: Giữ mặc định `0.7` (đảm bảo báo cáo logic).

#### **🔹 Node 5: "Send HTML Email via Gmail" (gmail)**
- **Cấu hình**:
  - **Credentials**: Chọn OAuth 2.0 (không sử dụng mật khẩu 2FA).
  - **From Email**: Điền email Gmail của sếp (ví dụ: `sếp@doanhnghiep.com`).
  - **To Email**: Sử dụng `$node["Investment Watchlist"].json["email"]` (đã cấu hình ở Node 2).
  - **Subject**: Thay đổi thành `"Báo cáo Nghiên cứu Đầu Tư - {{$node["Investment Watchlist"].json["ticker"]}}"`.
  - **HTML Body**: Sẽ được tự động xây dựng từ Node 6.

---

### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **"Manual Test Trigger"** để chạy workflow với dữ liệu mẫu.
   - Kiểm tra email nhận được có đúng nội dung không.
2. **Active Workflow**:
   - Sau khi kiểm tra thành công, bật **"Active"** ở góc trên bên phải.

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Thêm Slack/Telegram Notification**:
   - Sử dụng node `slack` hoặc `telegramBot` để thông báo khi workflow hoàn thành.
   - Cấu hình trong Node **"Send HTML Email via Gmail"** bằng cách thêm step `webhook` sau đó.

2. **Lưu Log vào Google Sheets**:
   - Thêm node `googleSheets` để ghi lại lịch sử báo cáo (ticker, ngày gửi, kết quả).
   - Cấu hình sheet với cột: `Ticker`, `Ngày`, `Tóm tắt tin tức`, `Giá trị`.

3. **Tùy chỉnh HTML Email**:
   - Sửa Node **"Build HTML Email Body"** (Code) để thay đổi style (màu sắc, logo, footer).
   - Ví dụ:
     ```javascript
     return {
       html: `<div style="font-family:Arial; color:#333;">
               <h1>Báo cáo Đầu Tư - {{$node["Investment Watchlist"].json["ticker"]}}</h1>
               <p>{{$json.body}}</p>
               <p>Trung tâm Đầu Tư - {{new Date().toLocaleDateString()}}</p>
             </div>`
     };
     ```

4. **Kết hợp với Notion/Notepad**:
   - Thay vì gửi email, lưu báo cáo vào Notion hoặc OneNote bằng node `notion` hoặc `onedrive`.
:::

---

## 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp đầu tư để tập trung vào chiến lược hơn là tra cứu tin tức thủ công. Với **Olostep + OpenAI + Gmail**, báo cáo được tự động hóa hoàn toàn, chính xác và chuyên nghiệp.

### **Bước tiếp theo**:
1. **Import workflow** và cấu hình theo hướng dẫn trên.
2. **Test Run** trước khi bật chế độ tự động.
3. **Tùy chỉnh** danh sách tickers, prompt OpenAI và style email theo nhu cầu.

👉 **Bắt đầu tự động hóa ngay hôm nay!** Nếu có vấn đề, các sếp có thể chia sẻ trên [community n8n](https://community.n8n.io/) hoặc liên hệ tác giả [Abid Ali Awan](https://n8n.io/workflows/15387).

---