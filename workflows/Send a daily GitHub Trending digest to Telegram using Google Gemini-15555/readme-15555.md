---
title: "🚀 Tự Động Hóa Báo Cáo GitHub Trending Hàng Ngày Với AI Gemini - Gửi Trực Tiếp Telegram"
description: "Workflow tự động hóa 100% không code giúp các sếp nhận được báo cáo tổng hợp dự án GitHub trending hàng ngày, được AI Gemini tóm tắt và gửi trực tiếp qua Telegram. Tiết kiệm thời gian theo dõi thủ công, phát hiện dự án mới nổi bật chỉ trong vài giây."
slug: "tieu-dong-hoa-bao-cao-github-trending-ai-gemini-telegram"
tags: [n8n, automation, ai-summarization, github, telegram, no-code]
keywords: [tự động hóa github trending, ai gemini telegram, báo cáo dự án open source hàng ngày, tự động hóa market research, n8n workflow ai]
---

# 🚀 **Tự Động Hóa Báo Cáo GitHub Trending Hàng Ngày Với AI Gemini - Gửi Trực Tiếp Telegram**

### **Giải pháp cho các sếp:**
- **Thủ công?** Phải tốn 10-15 phút mỗi ngày để duyệt trang *GitHub Trending*, đọc README của từng dự án, và chọn những dự án thú vị?
- **AI Gemini** sẽ làm tất cả cho bạn: Tóm tắt, phân tích, và gửi báo cáo định kỳ qua Telegram chỉ trong **vài giây** mỗi ngày.
- **Không cần code**, chỉ cần cấu hình và chạy 24/7 trên VPS.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động liên tục và ổn định, các sếp nên **self-host n8n** trên VPS. Dưới đây là 2 lựa chọn VPS chất lượng với mã giảm giá dành riêng:
👉 **[TinoHost - VPS N8N](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 **[BNIX - Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Tốc độ cao, ổn định)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Không phải duyệt thủ công hàng trăm dự án mỗi ngày.
- **Tóm tắt AI chính xác:** Gemini phân tích README và đưa ra **tóm tắt, lý do đáng chú ý, đối tượng mục tiêu, và từ khóa kỹ thuật** cho từng dự án.
- **Cá nhân hóa:** Chỉ cần chọn số lượng dự án (ví dụ: 5 dự án hàng ngày) và AI sẽ tự động lọc ra những dự án **nổi bật nhất**.
- **Hoạt động liên tục:** Workflow chạy tự động hàng ngày (cấu hình được thời gian chạy).
- **Dễ dàng chia sẻ:** Báo cáo được gửi trực tiếp qua Telegram, có thể chia sẻ với team hoặc lưu lại để theo dõi.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Telegram** (để nhận báo cáo hàng ngày).
2. **API Key Google Gemini** (để sử dụng AI tóm tắt).
3. **Tài khoản GitHub** (để fetch dữ liệu trending - mặc định không cần API key, nhưng nếu bị block, cần cấu hình proxy).

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/15555](https://n8n.io/workflows/15555) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ link trên và dán vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này gồm **14 node**, các sếp cần chú ý cấu hình các node sau:

##### **A. Cấu hình Schedule Trigger (Định thời gian chạy)**
- Node: **Schedule Trigger**
- **Lưu ý:**
  - Mặc định chạy **hàng ngày lúc 8h sáng** (UTC).
  - Các sếp có thể thay đổi thời gian bằng cách chỉnh `cron` (ví dụ: `0 8 * * *` để chạy lúc 8h sáng hàng ngày).
  - **Gợi ý:** Chọn thời gian phù hợp với giờ làm việc của team.

##### **B. Cấu hình Digest Config (Số lượng dự án)**
- Node: **Set Digest Config**
- **Lưu ý:**
  - Tham số `n_repos` quyết định số lượng dự án trending được lấy (mặc định là **5**).
  - **Khuyến nghị:** Đặt `n_repos = 5` để tránh quá tải API và đảm bảo chất lượng tóm tắt.

##### **C. Cấu hình Google Gemini (AI Tóm Tắt)**
- Node: **Google Gemini Chat Model**
- **Lưu ý:**
  1. **Thêm Credentials:**
     - Vào **Credentials** trong n8n → **Add Credential** → Chọn **Google Palm API**.
     - Điền **API Key** từ tài khoản Google Cloud (cần cấp quyền cho API Gemini).
  2. **Cấu hình Prompt:**
     - Workflow đã tự động cấu hình prompt để AI tóm tắt dự án theo định dạng:
       ```json
       {
         "repository_url": "URL dự án",
         "summary": "Tóm tắt ngắn gọn",
         "why_it_matters": "Lý do dự án đáng chú ý",
         "best_fit_audience": "Đối tượng mục tiêu",
         "keywords": "Từ khóa kỹ thuật"
       }
       ```

##### **D. Cấu hình Telegram (Gửi Báo Cáo)**
- Node: **Send a text message**
- **Lưu ý:**
  1. **Thêm Credentials:**
     - Vào **Credentials** → **Add Credential** → Chọn **Telegram**.
     - Điền:
       - **API Token:** Lấy từ [@BotFather](https://t.me/BotFather) (gửi `/newbot` để tạo bot).
       - **Chat ID:** Lấy từ [@userinfobot](https://t.me/userinfobot) (gửi `/start` và copy Chat ID).
  2. **Chỉnh nội dung báo cáo:**
     - Workflow đã tự động format báo cáo thành **dạng Markdown** để dễ đọc trên Telegram.
     - Nếu muốn thay đổi định dạng, chỉnh node **Format Telegram Message** (Code).

##### **E. Các Node Khác (Không cần chỉnh)**
- **Fetch GitHub Trending Page:** Lấy dữ liệu từ trang trending của GitHub.
- **Extract Trending Repository Links:** Trích xuất liên kết dự án từ trang HTML.
- **Fetch Repository README:** Lấy nội dung README của từng dự án.
- **Generate AI Repository Digest:** Gửi payload đến Gemini và nhận kết quả tóm tắt.
- **Structured Output Parser:** Chuyển kết quả Gemini thành JSON để dễ format.

#### **3. Kích hoạt ⚡️**
1. **Test Run:**
   - Chọn **Run Workflow** để kiểm tra dữ liệu mẫu.
   - Kiểm tra Telegram có nhận được báo cáo không.
2. **Bật Active:**
   - Sau khi kiểm tra thành công, bật **Active** để workflow chạy tự động hàng ngày.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm Logs cho Debugging:**
   - Thêm node **Sticky Note** sau **Google Gemini Chat Model** để lưu kết quả tóm tắt vào database (ví dụ: Google Sheets) để theo dõi lịch sử.
   - **Cách làm:**
     - Thêm node **Google Sheets** và cấu hình để ghi dữ liệu vào sheet mới.

2. **Gửi Báo Cáo qua Slack:**
   - Thay vì Telegram, các sếp có thể gửi báo cáo qua Slack bằng node **Slack**.
   - **Cách làm:**
     - Thêm node **Slack** và cấu hình với API Token từ Slack App.

3. **Tùy Chỉnh Prompt AI:**
   - Nếu muốn AI tóm tắt theo phong cách riêng, chỉnh node **Google Gemini Chat Model** và thay đổi prompt trong **Parameters → Prompt**.

4. **Lọc Dự án Theo Ngôn Ngữ/Kỹ Thuật:**
   - Thêm node **Code** sau **Fetch Repository README** để lọc dự án theo ngôn ngữ (ví dụ: chỉ lấy Python, JavaScript).
   - **Ví dụ mã:**
     ```javascript
     // Lọc dự án có README bằng tiếng Anh
     return $input.all().filter(item => item.language === "JavaScript" || item.language === "Python");
     ```

5. **Gửi Báo Cáo qua Email:**
   - Thay vì Telegram, các sếp có thể gửi báo cáo qua email bằng node **Email**.
   - **Cách làm:**
     - Thêm node **Email** và cấu hình với tài khoản Gmail (cần cấp quyền cho OAuth).

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn:
✅ **Tiết kiệm thời gian** theo dõi dự án GitHub trending.
✅ **Nhận báo cáo AI tóm tắt** hàng ngày, không cần đọc README thủ công.
✅ **Chia sẻ với team** một cách dễ dàng qua Telegram/Slack/Email.

**Hành động ngay:**
1. **Import workflow** và cấu hình theo hướng dẫn trên.
2. **Bật Active** để nhận báo cáo hàng ngày.
3. **Tích hợp vào workflow hàng ngày** của team!

---
**Cần hỗ trợ?**
- **LinkedIn:** [Atha Ahsan Xavier Haris](https://www.linkedin.com/in/athaahsan/)
- **Hỏi đáp:** Đăng câu hỏi trên [n8n Community](https://community.n8n.io/) với tag `#github-trending`.