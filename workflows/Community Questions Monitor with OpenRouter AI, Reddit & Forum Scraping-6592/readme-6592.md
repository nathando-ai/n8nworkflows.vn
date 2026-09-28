---
title: "🚀 **Tự Động Hóa Theo Dõi Câu Hỏi Cộng Đồng: AI Tóm Tắt Reddit & Forum n8n (Không Cần Code!)**"
description: "Workflow tự động hóa thu thập, phân loại và tóm tắt câu hỏi mới từ Reddit và diễn đàn n8n hàng ngày, gửi báo cáo định kỳ qua email. Giúp các sếp tiết kiệm thời gian theo dõi cộng đồng, hiểu rõ xu hướng và phản hồi nhanh chóng."
slug: "tieu-dong-hoi-community-reddit-forum-n8n"
tags: [n8n, automation, market-research, ai-summarization, reddit-scraping]
keywords: [n8n workflow tự động hóa, theo dõi cộng đồng Reddit, tóm tắt AI, tự động hóa forum, báo cáo hàng ngày]
---

# 🚀 **Tự Động Hóa Theo Dõi Câu Hỏi Cộng Đồng: AI Tóm Tắt Reddit & Forum n8n**

## **🔍 Nỗi Đau Của Các Sếp Khi Theo Dõi Cộng Đồng Thủ Công**
Hàng ngày, các sếp phải:
- **Quét thủ công** hàng trăm câu hỏi trên Reddit, diễn đàn hoặc nhóm Telegram để tìm kiếm ý kiến phản hồi về sản phẩm/dịch vụ.
- **Tóm tắt nội dung** dài dòng của từng bài viết, mất thời gian và dễ bỏ lỡ thông tin quan trọng.
- **Phân loại câu hỏi** (cần hỗ trợ, ý kiến phản hồi, đề xuất cải tiến) một cách rườm rà, không có hệ thống.
- **Bỏ lỡ xu hướng** vì không theo dõi liên tục, dẫn đến phản hồi chậm trễ.

**Workflow này giải quyết tất cả!** Với AI và tự động hóa, các sếp sẽ nhận được **báo cáo tóm tắt hàng ngày** về câu hỏi mới nhất từ Reddit và diễn đàn n8n, được phân loại và sắp xếp logic, giúp **tiết kiệm 10+ giờ/tuần** và **hiểu rõ hơn về cộng đồng**.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
✅ **Tiết kiệm thời gian**: Không cần quét thủ công hàng trăm bài viết mỗi ngày.
✅ **Tóm tắt thông minh**: AI tự động phân loại và tóm tắt câu hỏi, giữ lại nội dung quan trọng.
✅ **Báo cáo định kỳ**: Nhận email tổng hợp hàng ngày (sáng 9h và chiều 5h) với tất cả câu hỏi mới.
✅ **Phân tích xu hướng**: Dễ dàng theo dõi xu hướng, ý kiến phản hồi và đề xuất cải tiến từ cộng đồng.
✅ **Hoạt động 24/7**: Workflow chạy tự động, không cần can thiệp của con người.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ**]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản Reddit OAuth2**:
   - [Tạo OAuth2 App trên Reddit](https://www.reddit.com/prefs/apps) (đăng ký với mục đích "Scripting").
   - Lưu **Client ID** và **Client Secret** vào credentials `redditOAuth2Api` trong n8n.
2. **API Key OpenRouter**:
   - [Đăng ký tài khoản OpenRouter](https://openrouter.ai/) và lấy **API Key**.
   - Thêm vào credentials `openRouterApi` trong n8n.
3. **Thiết lập SMTP cho email**:
   - Cấu hình tài khoản email (Gmail, Outlook, hoặc SMTP riêng) để gửi báo cáo.
   - Thêm vào credentials `smtp` trong n8n.
4. **Subreddit mục tiêu**:
   - Chỉ định tên **subreddit** (ví dụ: `n8nio`) trong node **"Get Latest Reddit Posts"**.
5. **Keyword lọc forum**:
   - Đặt từ khóa lọc trong node **"Filter recent posts"** (ví dụ: `n8n`, `automation`, `workflow`).
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/6592](https://n8n.io/workflows/6592) (chọn **Export JSON**).
2. Trong n8n Editor, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Create new workflow** và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở n8n Editor → Tạo workflow mới.
2. Nhấn **Import** → Chọn **Paste JSON** và dán nội dung từ [file JSON này](https://n8n.io/workflows/6592) (hoặc tải từ link trên).
3. Chọn **Create new workflow** và nhấn **Import**.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này bao gồm **hai phần tự động hóa riêng biệt**:
- **Reddit Digest**: Thu thập và tóm tắt câu hỏi từ Reddit.
- **n8n Forum Digest**: Scrape và tóm tắt bài viết từ diễn đàn n8n.

#### **A. Cấu Hình Reddit Digest**
1. **Node "Get latest 50 reddit posts"**:
   - Điền **Subreddit name** (ví dụ: `n8nio`).
   - Chọn **credentials**: `redditOAuth2Api`.
   - Thiết lập **limit** (số lượng bài viết lấy, mặc định 50).

2. **Node "Filter for Questions"**:
   - Cấu hình **lọc câu hỏi** bằng cách chỉnh sửa **JSON Path** (ví dụ: `$["data"][?[contains($.body, "?" || $.title, "?")]]`).
   - **Mẹo**: Sử dụng **Text Classifier** (node `textClassifier`) để phân loại câu hỏi (ví dụ: "Cần hỗ trợ", "Đề xuất", "Phản hồi").

3. **Node "Summarize Reddit Questions"**:
   - Chỉnh sửa **prompt AI** trong node `chainLlm` để tóm tắt câu hỏi:
     ```json
     {
       "prompt": "Tóm tắt câu hỏi này trong 3 câu ngắn gọn. Nếu câu hỏi liên quan đến {sản phẩm/dịch vụ của bạn}, hãy nhấn mạnh điểm đó. Câu trả lời phải rõ ràng và không có thông tin không liên quan."
     }
     ```
   - **Mẹo**: Thử nghiệm với các **OpenRouter Models** khác (ví dụ: `openrouter/mistral-7b`, `openrouter/mixtral-8x7b`) trong node `lmChatOpenRouter`.

4. **Node "Prepare Reddit Email Body"**:
   - Chỉnh sửa mã **JavaScript** trong node `code` để định dạng email:
     ```javascript
     // Ví dụ: Thêm logo hoặc link vào email
     const emailBody = `
       <h2>Reddit Digest - ${new Date().toLocaleDateString()}</h2>
       <p>Dưới đây là tóm tắt các câu hỏi mới nhất từ subreddit <strong>${subredditName}</strong>:</p>
       ${posts.map(post => `<p><strong>${post.title}</strong></p><p>${post.summary}</p><hr>`).join('')}
       <p>Xem chi tiết: <a href="${post.url}">Link bài viết</a></p>
     `;
     return { emailBody };
     ```

5. **Node "Send Reddit Summary Email"**:
   - Chọn **credentials SMTP** đã cấu hình.
   - Điền **địa chỉ email nhận** (ví dụ: `team@doanhnghiep.com`).
   - **Lưu ý**: Nếu dùng Gmail, bật **Less Secure Apps** hoặc sử dụng **App Password**.

---

#### **B. Cấu Hình n8n Forum Digest**
1. **Node "Filter recent posts"**:
   - Chỉnh sửa **keyword lọc** (ví dụ: `n8n`, `automation`) để chỉ lấy bài viết liên quan.
   - **Mẹo**: Sử dụng **regex** để lọc chính xác:
     ```json
     { "data": { "title": { "$regex": "n8n" } } }
     ```

2. **Node "Summarize n8n Forum Posts"**:
   - Tương tự như Reddit, chỉnh sửa **prompt AI** trong node `chainLlm`:
     ```json
     {
       "prompt": "Tóm tắt bài viết này về {sản phẩm/dịch vụ của bạn} trong 4 câu. Nếu có đề xuất cải tiến, hãy nhấn mạnh điểm đó."
     }
     ```

3. **Node "Prepare Forum Email Body"**:
   - Chỉnh sửa mã **JavaScript** để định dạng email với logo hoặc link:
     ```javascript
     const emailBody = `
       <h2>n8n Forum Digest - ${new Date().toLocaleDateString()}</h2>
       <p>Dưới đây là tóm tắt các bài viết mới nhất từ diễn đàn:</p>
       ${posts.map(post => `<p><strong>${post.title}</strong></p><p>${post.summary}</p><hr>`).join('')}
       <p>Xem chi tiết: <a href="${post.url}">Link bài viết</a></p>
     `;
     return { emailBody };
     ```

---

### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Test workflow** để kiểm tra các node.
   - Kiểm tra **email mẫu** đã được gửi đúng không.
2. **Bật Active**:
   - Sau khi test thành công, chuyển trạng thái workflow sang **Active**.
3. **Cấu Hình Lịch Trình**:
   - Node **"Send every morning at 9am"** và **"Send every afternoon at 5pm"** sẽ tự động chạy hàng ngày.
   - **Lưu ý**: Đảm bảo n8n chạy trên **VPS 24/7** (không dùng phiên bản web n8n.io).

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[**TIẾP CẬN HƠN**]
1. **Thêm Slack/Telegram Notifications**:
   - Sử dụng node `slackSend` hoặc `telegramSend` để gửi báo cáo ngay khi có câu hỏi mới.
   - **Cách làm**:
     - Thêm node `slackSend` sau node `emailSend`.
     - Cấu hình **webhook Slack** và định dạng thông báo:
       ```json
       {
         "text": `🚨 Câu hỏi mới từ Reddit: <${post.url}|${post.title}>`,
         "blocks": [
           { "type": "section", "text": { "type": "mrkdwn", "text": `*Tóm tắt:* ${post.summary}` } }
         ]
       }
       ```

2. **Lưu Log vào Google Sheets/Notion**:
   - Sử dụng node `googleSheets` hoặc `notion` để ghi lại tất cả câu hỏi và tóm tắt.
   - **Cách làm**:
     - Thêm node `googleSheets` sau node `merge`.
     - Chọn **Sheet Name** và cấu hình **headers**:
       ```json
       {
         "sheetName": "Reddit_Questions",
         "headers": ["Title", "Summary", "URL", "Date"]
       }
       ```

3. **Phân Tích Xu Hướng với AI**:
   - Sử dụng node `chainLlm` để phân tích **tần suất xuất hiện** các từ khóa trong câu hỏi.
   - **Prompt AI**:
     ```json
     {
       "prompt": "Phân tích 10 câu hỏi gần đây nhất. Hãy liệt kê 3 từ khóa phổ biến nhất và cho biết chúng liên quan đến vấn đề gì trong sản phẩm/dịch vụ của chúng tôi."
     }
     ```

4. **Tự Động Trả Lời Câu Hỏi**:
   - Sử dụng node `redditReply` hoặc `emailSend` để tự động trả lời câu hỏi thường gặp.
   - **Cách làm**:
     - Thêm node `filter` để lọc câu hỏi có từ khóa cụ thể (ví dụ: "cách sử dụng").
     - Thêm node `redditReply` với nội dung trả lời tự động:
       ```json
       {
         "body": "Xin chào! Đây là câu trả lời tự động. Để hỗ trợ chi tiết, bạn có thể liên hệ qua email: support@doanhnghiep.com."
       }
       ```

---

## 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** để các sếp:
✔ **Tiết kiệm thời gian** theo dõi cộng đồng.
✔ **Hiểu rõ hơn** về ý kiến phản hồi và xu hướng.
✔ **Tự động hóa hoàn toàn** quá trình tóm tắt và báo cáo.

**Hành động ngay!**
1. **Cài đặt n8n trên VPS** (để workflow chạy 24/7).
2. **Import workflow** và cấu hình các credentials.
3. **Test và bật Active** để nhận báo cáo hàng ngày.

👉 **🎁 Mã giảm giá VPS TinoHost (39% off)** cho các sếp tự động hóa: **VPSN8N**
🔗 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

**Chia sẻ workflow này với đồng nghiệp để cùng tự động hóa công việc!** 🚀