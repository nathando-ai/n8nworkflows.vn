---
title: "🚀 Tự Động Hoàn Thành Báo Cáo Tài Liệu Média Hàng Ngày Với GPT-4.1-mini, NewsAPI & Gmail (Không Cần Code)"
description: "Workflow tự động hóa lấy tin tức mới nhất từ NewsAPI, tổng hợp và phân tích bằng GPT-4.1-mini, sau đó gửi báo cáo định kỳ qua email. Giúp tiết kiệm **1 giờ/ngày** cho công việc nghiên cứu và viết tóm tắt, đồng thời tự động lưu trữ dữ liệu để phân tích dài hạn."
slug: "tieu-dong-hoan-thanh-bao-cao-tai-lieu-media-hang-ngay"
tags: [n8n, automation, ai-summarization, news-api, gmail, google-sheets, gpt-4.1-mini]
keywords: [n8n workflow media briefing, tự động hóa báo cáo hàng ngày, gpt-4.1-mini tổng hợp tin tức, newsapi + gmail tự động, lưu trữ dữ liệu media]
---

# 🚀 **Tự Động Hoàn Thành Báo Cáo Tài Liệu Média Hàng Ngày Với AI (Không Cần Code)**

### **Nỗi Đau Của Các Sếp**
Hàng ngày, các sếp phải mất **từ 30 phút đến 1 giờ** để:
- Tìm kiếm tin tức liên quan đến **một chủ đề cụ thể** (ví dụ: tên công ty, từ khóa "Sustainability", "Tech Startup").
- Đọc và **tóm tắt** những tin tức quan trọng nhất.
- **Phân tích sâu** một số chủ đề nếu cần thiết.
- Gửi báo cáo định kỳ cho đội ngũ hoặc khách hàng.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động lấy tin tức** từ NewsAPI trong **2 ngày gần nhất**.
✅ **Tổng hợp và phân tích** bằng **GPT-4.1-mini** (rẻ hơn GPT-4 nhưng hiệu quả).
✅ **Gửi báo cáo email tự động** với **cấu trúc chuyên nghiệp**.
✅ **Lưu trữ dữ liệu** trên Google Sheets để **phân tích dài hạn**.
✅ **Tiết kiệm 1 giờ/ngày** cho công việc nghiên cứu và viết tóm tắt.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản miễn phí.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tìm kiếm, đọc và viết tóm tắt thủ công.
- **Dữ liệu chính xác**: AI phân tích và tổng hợp tin tức **một cách khách quan**.
- **Cá nhân hóa**: Chỉ cần **điền chủ đề** (ví dụ: tên công ty, từ khóa) và email nhận.
- **Lưu trữ dài hạn**: Dữ liệu được **ghi lại trên Google Sheets** để phân tích sau.
- **Phân tích sâu**: Workflow tự động **chọn ra những tin tức quan trọng nhất** và gửi báo cáo chi tiết.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản NewsAPI** (miễn phí có giới hạn, trả phí để mở rộng).
✔ **API Key của OpenAI** (để sử dụng GPT-4.1-mini).
✔ **Tài khoản Gmail** (hoặc Google Workspace) để gửi email tự động.
✔ **Google Sheets** (để lưu trữ dữ liệu lịch sử).
✔ **Thời gian đầu tư**: ~30 phút để cấu hình lần đầu.

---
:::note[LƯU Ý QUAN TRỌNG]
- Workflow **không cần code**, nhưng yêu cầu **cấu hình chính xác** các API Key và credentials.
- Nếu sử dụng **Gmail**, các sếp cần **bật "Dùng ứng dụng ít an toàn"** trong cài đặt Gmail.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/13181](https://n8n.io/workflows/13181) và import vào **n8n Editor**.
- **Copy/Paste** JSON từ file vào **n8n Editor** (đường dẫn: `https://n8n.io/editor`).

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này gồm **17 node**, nhưng các sếp chỉ cần chú ý đến **5 node quan trọng nhất**:

##### **A. Cấu Hình "Set user config" (Node "Set user config")**
- **Điền chủ đề** (ví dụ: `"Sustainability"`, `"Tech Startup"`).
- **Chọn email nhận** (ví dụ: `team@company.com`).
- **Thiết lập ngày bắt đầu** (ví dụ: `2024-01-01`).

##### **B. Cấu Hình NewsAPI (Node "Fetch news articles")**
- **API Key**: Điền vào **Credentials** của node `httpRequest`.
- **Query Parameters**:
  - `q`: Chủ đề (ví dụ: `"Sustainability"`).
  - `from`: Ngày bắt đầu (ví dụ: `2024-01-01`).
  - `to`: Ngày kết thúc (ví dụ: `2024-01-03`).
  - `sortBy`: `publishedAt` (để lấy tin tức mới nhất).

##### **C. Cấu Hình GPT-4.1-mini (Node "OpenAI Chat Model")**
- **API Key**: Điền vào **Credentials** của node `lmChatOpenAi`.
- **Prompt mẫu** (có thể chỉnh sửa):
  ```plaintext
  Tóm tắt tin tức về {topic} trong 2 ngày qua. Chỉ lấy những tin tức quan trọng nhất, không có chi tiết không cần thiết.
  ```

##### **D. Cấu Hình Gmail (Node "Send the email (Gmail)")**
- **Credentials**: Chọn tài khoản Gmail đã cấu hình.
- **Email nhận**: Điền vào `to` (ví dụ: `team@company.com`).
- **Tiêu đề email**: `"Báo cáo Tài Liệu Média Hàng Ngày - {topic}"`.
- **Nội dung email**: Sử dụng **dữ liệu từ node "Merge"** (tóm tắt AI + tin tức).

##### **E. Cấu Hình Google Sheets (Node "Get Google Sheets data" & "Save to Google Sheets")**
- **Credentials**: Chọn tài khoản Google đã kết nối.
- **Sheet Name**: Điền tên sheet (ví dụ: `"Media_Briefing"`).
- **Range**: `A1:D1000` (để lưu trữ dữ liệu dài hạn).

#### **3. Kích Hoạt ⚡️**
- **Test Run**: Chạy thử với **dữ liệu mẫu** để kiểm tra kết quả.
- **Bật Active**: Sau khi kiểm tra thành công, **bật workflow**.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Slack/Telegram Notifications**
   - Sử dụng node **Slack** hoặc **Telegram Bot** để gửi báo cáo ngay khi có tin tức mới.
   - Cấu hình trong node **"Send the email"** bằng cách **merge** với node **Slack**.

2. **Lưu Log Dữ Liệu**
   - Sử dụng node **Google Drive** hoặc **AWS S3** để lưu trữ **tin tức nguyên bản** (không chỉ tóm tắt).

3. **Phân Tích Dữ Liệu Dài Hạn**
   - Sử dụng **Google Data Studio** hoặc **Power BI** để **vẽ biểu đồ** từ dữ liệu trên Google Sheets.

4. **Tự Động Chọn Chủ Đề Theo Ngày**
   - Sử dụng node **DateTime** để **đổi chủ đề** theo ngày (ví dụ: Chủ nhật là "Sustainability", Thứ Hai là "Tech").

---
### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **strategy** thay vì công việc thủ công. **Chỉ cần 30 phút cấu hình**, workflow sẽ **tự động hoạt động hàng ngày**, gửi báo cáo email và lưu trữ dữ liệu.

**Hãy áp dụng ngay và tiết kiệm 1 giờ/ngày!** 🚀

---
:::tip[Gợi Ý Cuối Cùng]
- Nếu gặp vấn đề, **xem log** trong node **"StickyNote"** để debug.
- Muốn **tăng hiệu suất**, sử dụng **GPT-4.1-mini** thay vì GPT-4 để tiết kiệm chi phí.
- Để **cập nhật chủ đề**, chỉ cần chỉnh node **"Set user config"**.
:::

---
**Bạn đã sẵn sàng tự động hóa báo cáo media hàng ngày chưa?** 😊