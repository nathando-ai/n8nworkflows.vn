---
title: "📰 **Tự Động Hoàn Chỉnh Tạp Chí Kinh Tế Hàng Ngày Israel Với RSS + GPT-4o (Không Cần Code!)**"
description: "Workflow tự động hóa thu thập, lọc và tổng hợp tin tức kinh tế hàng ngày từ Israel từ 2 nguồn RSS chính (Calcalist & Mako), sau đó sử dụng GPT-4o để chọn lọc 5 tin tức quan trọng nhất và gửi email định kỳ cho các sếp. Giúp tiết kiệm 10+ giờ/tháng và đảm bảo thông tin chính xác, cá nhân hóa."
slug: "tieu-dong-hoan-chinh-tap-chi-kinh-te-israel-rss-gpt-4o"
tags: [n8n, automation, finance, ai, gpt-4o, email-marketing, rss-feed, no-code]
keywords: [n8n workflow kinh tế, tự động hóa tin tức hàng ngày, GPT-4o chọn tin tức, email báo cáo định kỳ, RSS Israel, Calcalist Mako]
---

# 🚀 **Tự Động Hoàn Chỉnh Tạp Chí Kinh Tế Hàng Ngày Israel Với RSS + GPT-4o**

### **🔍 Nỗi Đau Của Các Sếp Và Giải Pháp Tự Động Hóa**
Các sếp trong ngành tài chính, đầu tư hoặc kinh doanh quốc tế thường phải mất **10+ giờ/tuần** để:
- **Thu thập tin tức** từ nhiều nguồn RSS khác nhau (Calcalist, Mako, Bloomberg...).
- **Lọc tin tức không liên quan** và bỏ qua nội dung trùng lặp.
- **Chọn lọc tin tức quan trọng** dựa trên tiêu chí cá nhân (ví dụ: mức độ ảnh hưởng, thời gian xuất bản, chủ đề).
- **Tổng hợp và gửi email định kỳ** cho đội ngũ hoặc bản thân.

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✅ **Tự động thu thập** tin tức mới nhất từ 2 nguồn RSS uy tín nhất của Israel.
✅ **Sử dụng GPT-4o** để **lọc và chọn 5 tin tức quan trọng nhất** hàng ngày.
✅ **Tạo email định dạng HTML** với design chuyên nghiệp, dễ đọc trên mobile.
✅ **Gửi tự động** vào email cá nhân hoặc nhóm của các sếp **mỗi ngày** (hoặc theo lịch bạn thiết lập).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7**, các sếp nên cài đặt **n8n trên VPS riêng** (Self-hosted) để tránh giới hạn của phiên bản Cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ nhanh, không lag khi xử lý GPT-4o)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** cho việc thu thập và lọc tin tức.
- **Tin tức được chọn lọc chính xác** bởi GPT-4o, phù hợp với nhu cầu của từng sếp.
- **Email định dạng chuyên nghiệp**, dễ đọc trên mọi thiết bị.
- **Hoạt động tự động 24/7**, không phụ thuộc vào thời gian làm việc.
- **Cá nhân hóa hoàn toàn** (có thể thay đổi tiêu chí lọc tin tức theo yêu cầu).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản API OpenAI** (để sử dụng GPT-4o):
   - [Đăng ký API Key OpenAI](https://platform.openai.com/account/api-keys) (Mã giảm giá **n8n** để mua credit: [Link](https://openai.com/pricing)).
   - **Lưu ý**: GPT-4o có giới hạn token, các sếp nên **monitor chi phí** (mỗi tin tức ~0.005$/1000 token).

2. **Thiết lập SMTP cho email gửi**:
   - Các sếp cần **credentials SMTP** của nhà cung cấp email (Gmail, Outlook, hoặc SMTP riêng).
   - **Không sử dụng email miễn phí** (Gmail, Yahoo) vì có thể bị block.

3. **Không cần thiết lập gì thêm** về RSS, vì workflow đã tích hợp sẵn URL của **Calcalist** và **Mako**.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
**Cách 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/3564](https://n8n.io/workflows/3564) (chọn **Export as JSON**).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Create new workflow** và nhấn **Import**.

**Cách 2: Copy/Paste JSON**
1. Copy toàn bộ mã JSON từ [n8n.io/workflows/3564](https://n8n.io/workflows/3564).
2. Trên **n8n Editor**, nhấn **Import** → Chọn **Paste JSON** và dán mã.

---

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **3 node quan trọng** cần cấu hình cẩn thận:

##### **A. Node "Schedule Trigger" (Lịch chạy hàng ngày)**
- **Thiết lập thời gian chạy**:
  - Mặc định là **lúc 8h sáng** (thời gian Israel).
  - Các sếp có thể thay đổi bằng cách nhấn **Edit** → **Schedule** → Chọn **Cron expression** hoặc **Time-based**.
  - **Gợi ý**: Chọn **8h sáng** (UTC+2) để tin tức mới nhất được thu thập trước khi bắt đầu ngày làm việc.

##### **B. Node "ChatGPT 4o" (Lọc tin tức)**
- **Cấu hình API Key**:
  - Trong **Credentials**, chọn **openAiApi** (đã thiết lập trước khi import).
  - **Prompt mặc định**:
    ```plaintext
    You are an expert in Israeli economy. Select the top 5 most relevant news articles from the following list. Prioritize articles that:
    1. Have significant economic impact (e.g., policy changes, market movements, M&A deals).
    2. Are published within the last 24 hours.
    3. Are from trusted sources (Calcalist, Mako, Globes).
    Return the selected articles in JSON format with "title", "link", and "summary" fields.
    ```
  - **Lưu ý**:
    - Nếu muốn **cá nhân hóa tiêu chí**, các sếp có thể chỉnh sửa prompt bằng **Node "Set"** (trước khi đưa vào GPT-4o).
    - **Limit token**: Đảm bảo không vượt quá **4096 token** (mỗi tin tức ~500 token).

##### **C. Node "Send Daily News" (Gửi email)**
- **Thiết lập SMTP**:
  - Trong **Credentials**, chọn **smtp** (đã cấu hình trước).
  - **Cấu hình email**:
    - **From**: Địa chỉ email của các sếp (ví dụ: `sếp@example.com`).
    - **To**: Địa chỉ email nhận (có thể là cá nhân hoặc nhóm).
    - **Subject**: Mặc định là **"Daily Israeli Economic Digest - [Date]"**.
    - **HTML Content**: Sử dụng **Node "Create HTML"** để tạo email có design chuyên nghiệp.

---
#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Run Workflow** và kiểm tra:
     - **RSS - Calcalist** và **RSS - Mako** có thu thập được tin tức không?
     - **GPT-4o** có chọn được 5 tin tức tốt không?
     - **Email** có được gửi đúng định dạng không?
2. **Bật Active**:
   - Sau khi kiểm tra thành công, nhấn **Active** để workflow chạy tự động theo lịch.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm nguồn RSS khác**:
   - Các sếp có thể **thêm node "rssFeedRead"** để thu thập từ **Globes** hoặc **Calcalist Tech**.
   - **Cách làm**:
     - Copy node **RSS - Calcalist** → **Duplicate**.
     - Thay đổi **URL** thành RSS của Globes: `https://www.globes.co.il/rss/`.

2. **Lưu log tin tức**:
   - Thêm **Node "Set"** sau **ChatGPT 4o** để lưu kết quả vào **Google Sheets** hoặc **Notion**.
   - **Cách làm**:
     - Sử dụng **Node "Google Sheets"** (n8n-nodes-base.googleSheets) để ghi dữ liệu vào sheet mới.

3. **Gửi báo cáo định kỳ**:
   - Thay vì gửi hàng ngày, các sếp có thể **thiết lập lịch tuần** (ví dụ: **Thứ 2 hàng tuần**).
   - **Cách làm**:
     - Trong **Schedule Trigger**, thay đổi **Cron expression** thành:
       ```plaintext
       0 0 * * 1  # Chạy vào ngày thứ 2 hàng tuần lúc 0h (UTC+2)
       ```

4. **Cá nhân hóa tin tức**:
   - Sử dụng **Node "Function"** để thêm logic lọc tin tức theo **ngành nghề** (ví dụ: chỉ tin tức về **tech** hoặc **ngân hàng**).
   - **Ví dụ**:
     ```javascript
     // Node "Function" trước GPT-4o
     return {
       json: {
         filter: "tech" // Chỉ lọc tin tức về tech
       }
     };
     ```

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa hoàn toàn** việc thu thập và tổng hợp tin tức kinh tế hàng ngày từ Israel. Bằng cách kết hợp **RSS + GPT-4o**, các sếp không chỉ **tiết kiệm thời gian** mà còn **nhận được tin tức được lọc chính xác** và **gửi định kỳ** một cách chuyên nghiệp.

**Hành động ngay hôm nay**:
1. **Cài đặt n8n trên VPS** (nếu chưa có).
2. **Import workflow** và **cấu hình SMTP + API Key**.
3. **Test và bật chạy** để nhận tin tức hàng ngày!

**Có thắc mắc?** Để lại comment bên dưới hoặc liên hệ với **Elay Guez** (tác giả) qua [n8n Community](https://community.n8n.io/). 🚀