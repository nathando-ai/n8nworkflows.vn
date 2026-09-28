---
title: "🚀 Tự Động Hóa Báo Cáo ASO (App Store Optimization) Cho Ứng Dụng Google Play Với AI Gemini & Google Docs"
description: "Giải pháp tự động hóa hoàn toàn không cần code để phân tích ứng dụng Google Play, tạo báo cáo ASO chuyên nghiệp với AI Gemini, lưu trữ trên Google Docs và thông báo ngay lập tức qua Telegram. Tiết kiệm thời gian nghiên cứu và tối ưu hóa hiệu suất ứng dụng chỉ trong vài giây."
slug: "tieu-dong-hoa-bao-cao-aso-google-play-ai-gemini"
tags: [n8n, automation, no-code, app-store-optimization, ai-gemini, google-docs, telegram-notification, market-research]
keywords: [tự động hóa n8n, báo cáo ASO, AI Gemini, Google Play, Google Docs, Telegram alert, phân tích ứng dụng di động]
---

# 🚀 **Tự Động Hóa Báo Cáo ASO Cho Ứng Dụng Google Play Với AI Gemini & Google Docs**

### **Giải pháp nào giúp các sếp:**
- **Tiết kiệm 10-15 giờ/năm** nghiên cứu thủ công về ASO (App Store Optimization) cho ứng dụng Google Play?
- **Nhận báo cáo chuyên nghiệp** với phân tích AI, so sánh đối thủ và đề xuất tối ưu hóa chỉ trong vài giây?
- **Không cần viết một dòng code** nhưng vẫn tự động hóa toàn bộ quy trình từ lấy dữ liệu đến báo cáo?

Nếu câu trả lời là **Có**, thì **workflow này** chính là giải pháp hoàn hảo cho bạn!

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Xóa bỏ công việc thủ công phân tích ứng dụng và tạo báo cáo.
- **Báo cáo chuyên nghiệp**: AI Gemini tự động tổng hợp dữ liệu thành báo cáo có cấu trúc với các phần:
  - **Tổng quan ứng dụng** (tên, nhà phát triển, danh mục, xếp hạng).
  - **Đánh giá & phản hồi người dùng** (phân tích cảm xúc, điểm mạnh/điểm yếu).
  - **Phân tích đối thủ** (so sánh với ứng dụng tương tự trên thị trường).
  - **Thông tin thị trường** (tải xuống, doanh thu, xu hướng).
  - **Đề xuất tối ưu hóa** (cách cải thiện xếp hạng, nội dung mô tả, hình ảnh).
- **Lưu trữ trung tâm**: Tất cả báo cáo được tự động lưu trên **Google Docs** với tên ứng dụng, dễ chia sẻ và theo dõi.
- **Thông báo tức thời**: Nhận tin nhắn Telegram ngay khi báo cáo mới được tạo, **không bỏ lỡ bất kỳ cập nhật nào**.
- **Cập nhật liên tục**: Chỉ cần nhập URL ứng dụng vào form, workflow sẽ tự động chạy và trả về kết quả.
:::

---

## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **API Key SensorTower (hoặc API tương tự)**:
   - Dịch vụ lấy dữ liệu về ứng dụng (tên, xếp hạng, đối thủ, thống kê tải xuống).
   - *Lưu ý*: Nếu không có SensorTower, có thể thay thế bằng API khác như **App Annie** hoặc **AppFollow**.
   - **Cách lấy API Key**:
     - Đăng ký tại [SensorTower](https://www.sensortower.com/) (hoặc dịch vụ tương tự).
     - Tạo một **API Key** trong tài khoản và lưu trữ an toàn.

2. **API Key OpenRouter**:
   - Dịch vụ truy cập mô hình AI **Gemini 2.0 Flash** (miễn phí).
   - **Cách lấy API Key**:
     - Đăng ký tại [OpenRouter](https://openrouter.ai/).
     - Tạo một **API Key** và lưu trong n8n (Node `OpenRouter Chat Model`).

3. **Google Docs OAuth2**:
   - Tài khoản Google và **OAuth2 Credentials** để tạo/sửa báo cáo trên Google Docs.
   - **Cách thiết lập**:
     - Tạo một **Google Cloud Project** tại [Google Cloud Console](https://console.cloud.google.com/).
     - Bật **Google Docs API** và tạo **OAuth Client ID**.
     - Cấu hình trong n8n (Node `Create a document` và `Update a document`).

4. **Telegram Bot Token**:
   - Bot Telegram để gửi thông báo báo cáo mới.
   - **Cách lấy Token**:
     - Trên Telegram, tìm bot `@BotFather` và gửi lệnh `/newbot`.
     - Nhận **API Token** và cấu hình trong n8n (Node `Send a text message`).

5. **Form Trigger (n8n)**:
   - Cấu hình một **form** trong n8n để nhận URL ứng dụng từ Google Play.
   - *Lưu ý*: Form này sẽ tự động tạo khi import workflow.
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow theo hai cách:
#### **Cách 1: Import từ file JSON**
1. Tải file JSON của workflow từ [đây](https://n8n.io/workflows/7460) (hoặc sao chép JSON từ trang gốc).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Self-hosted** (nếu tự host) hoặc **n8n Cloud** (nếu dùng dịch vụ cloud).
4. Nhấn **Import** để hoàn tất.

#### **Cách 2: Sao chép JSON và dán vào Editor**
1. Mở **n8n Editor** và chọn **Create Workflow**.
2. Nhấn **Import** → Chọn **Paste JSON**.
3. Dán toàn bộ JSON từ [trang gốc](https://n8n.io/workflows/7460) vào ô nhập liệu.
4. Nhấn **Import** để tạo workflow.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Sau khi import, các sếp cần **cấu hình chi tiết** các node quan trọng dưới đây:

#### **🔹 Node 1: "On form submission" (formTrigger)**
- **Không cần chỉnh sửa** (n8n tự tạo form khi import).
- **Lưu ý**:
  - Form này sẽ hiển thị một ô nhập **URL ứng dụng Google Play** (ví dụ: `https://play.google.com/store/apps/details?id=com.example.app`).
  - Khi người dùng nhập URL và nhấn **Submit**, workflow sẽ tự động chạy.

#### **🔹 Node 2: "HTTP Request" (httpRequest)**
- **Mục đích**: Lấy dữ liệu ứng dụng từ API SensorTower (hoặc dịch vụ tương tự).
- **Cấu hình cần chỉnh**:
  - **URL**: `https://api.sensortower.com/v0.2/apps/{packageName}` (thay `{packageName}` bằng giá trị trích xuất từ URL).
    - *Lưu ý*: Các sếp cần **trích xuất `packageName`** từ URL (ví dụ: từ `id=com.example.app`).
    - **Cách trích xuất**:
      - Sử dụng **Node Code** (Node 4) để lấy `packageName` từ URL.
      - Ví dụ mã JavaScript trong Node Code:
        ```javascript
        const url = $input.all().url;
        const packageName = url.split('id=')[1];
        return { json: { packageName } };
        ```
  - **Headers**:
    - `Authorization: Bearer {API_KEY_SENSORTOWER}` (điền API Key từ bước chuẩn bị).
    - `Content-Type: application/json`.
  - **Method**: `GET`.

#### **🔹 Node 3: "Basic LLM Chain" (chainLlm) + "OpenRouter Chat Model" (lmChatOpenRouter)**
- **Mục đích**: Sử dụng AI Gemini để phân tích dữ liệu và tạo báo cáo ASO.
- **Cấu hình cần chỉnh**:
  - **Node `OpenRouter Chat Model`**:
    - **API Key**: Điền **API Key OpenRouter** từ bước chuẩn bị.
    - **Model**: Đã mặc định là `google/gemini-2.0-flash-exp:free`.
    - **Prompt**: Sử dụng template dưới đây (có thể chỉnh sửa để phù hợp):
      ```plaintext
      Analyze the following app data and generate a professional ASO report with these sections:
      1. App Overview (name, publisher, category, rating, downloads)
      2. User Ratings & Reviews (top reviews, sentiment analysis)
      3. Competitor Analysis (top 3 competitors, their ratings, keywords)
      4. Market Insights (trends, revenue estimates)
      5. Actionable Recommendations (how to improve rankings, descriptions, screenshots)

      Data:
      {{ $json.appData }}

      Format the report in Markdown with clear headings and bullet points.
      ```
    - **Input**: Điền từ **Node Code** (Node 4) hoặc **Node HTTP Request** (Node 2).
  - **Node `Basic LLM Chain`**:
    - **Model**: Chọn `OpenRouter Chat Model` (đã kết nối).
    - **Prompt**: Sử dụng template trên.

#### **🔹 Node 4: "Code" (Node Code)**
- **Mục đích**: Trích xuất `packageName` từ URL và chuẩn bị dữ liệu cho AI.
- **Mã cần chỉnh**:
  ```javascript
  // Trích xuất packageName từ URL
  const url = $input.all().url;
  const packageName = url.split('id=')[1];

  // Gọi API SensorTower để lấy dữ liệu ứng dụng
  const response = await $nodeHelper.request({
    method: 'GET',
    url: `https://api.sensortower.com/v0.2/apps/${packageName}`,
    headers: {
      'Authorization': 'Bearer YOUR_SENSORTOWER_API_KEY',
      'Content-Type': 'application/json'
    }
  });

  // Trả về dữ liệu để AI phân tích
  return {
    json: {
      appData: response.json
    }
  };
  ```
  - Thay `YOUR_SENSORTOWER_API_KEY` bằng API Key thực tế.

#### **🔹 Node 5: "Create a document" (googleDocs)**
- **Mục đích**: Tạo một Google Doc mới với tên ứng dụng.
- **Cấu hình cần chỉnh**:
  - **Folder ID**: Điền **ID thư mục Google Drive** nơi lưu báo cáo.
    - *Làm thế nào để lấy Folder ID?*
      1. Mở Google Drive và chọn thư mục cần lưu.
      2. Nhấn **Chia sẻ** → Sao chép **liên kết chia sẻ**.
      3. Trích xuất **ID** từ liên kết (ví dụ: `https://drive.google.com/drive/folders/1AbCdEfGhIjKlMnOp` → `1AbCdEfGhIjKlMnOp`).
  - **Title**: `ASO Report - {{ $json.appName }}` (điền từ dữ liệu ứng dụng).
  - **Content**: Trống (sẽ được cập nhật bởi Node sau).

#### **🔹 Node 6: "Update a document" (googleDocs)**
- **Mục đích**: Thêm nội dung báo cáo vào Google Doc.
- **Cấu hình cần chỉnh**:
  - **Document ID**: Lấy từ **Node "Create a document"** (n8n tự động trả về ID).
  - **Content**: Điền từ **Node LLM Chain** (đã phân tích bởi AI).

#### **🔹 Node 7: "Send a text message" (telegram)**
- **Mục đích**: Gửi thông báo Telegram khi báo cáo mới được tạo.
- **Cấu hình cần chỉnh**:
  - **Bot Token**: Điền **API Token Telegram** từ bước chuẩn bị.
  - **Chat ID**: Lấy **Chat ID** của bot (có thể lấy bằng cách gửi tin nhắn cho bot và sử dụng công cụ như [@userinfobot](https://t.me/userinfobot)).
  - **Message**: `📊 Báo cáo ASO mới được tạo cho ứng dụng: {{ $json.appName }}. Link: {{ $json.docUrl }}`.

#### **🔹 Node 8 & 9: "Code1" (Node Code)**
- **Mục đích**: Chuẩn bị dữ liệu cho Telegram và Google Docs.
- **Mã mẫu**:
  ```javascript
  // Trả về dữ liệu cần thiết cho Telegram và Google Docs
  return {
    json: {
      appName: $input.all().appName,
      docUrl: $input.all().documentUrl
    }
  };
  ```

---
### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhập một **URL ứng dụng Google Play** vào form.
   - Nhấn **Submit** và kiểm tra:
     - AI có phân tích dữ liệu không?
     - Google Doc có tạo thành công không?
     - Telegram có gửi thông báo không?
2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** trên workflow.

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::info[CẢI TIẾN & MỞ RỘNG]
1. **Thêm nhiều ứng dụng cùng lúc**:
   - Sử dụng **Node Code** để xử lý danh sách URL (ví dụ: từ Google Sheets).
   - Ví dụ:
     ```javascript
     const urls = $input.all().urls; // Danh sách URL từ Google Sheets
     const results = [];
     for (const url of urls) {
       const packageName = url.split('id=')[1];
       const response = await $nodeHelper.request({ /* ... */ });
       results.push(response.json);
     }
     return { json: results };
     ```

2. **Lưu log hoạt động**:
   - Thêm **Node StickyNote** để ghi lại lịch sử chạy workflow.
   - Cấu hình trong **Node StickyNote** để lưu:
     - Thời gian chạy.
     - URL ứng dụng.
     - Trạng thái thành công/thất bại.

3. **Gửi báo cáo định kỳ**:
   - Sử dụng **Node Schedule** (n8n Pro) để chạy workflow hàng tuần/month cho các ứng dụng quan trọng.
   - Ví dụ: Tạo một lịch trình chạy vào thứ 2 hàng tuần và gửi báo cáo cho tất cả ứng dụng theo dõi.

4. **Tích hợp với Slack**:
   - Thay vì Telegram, các sếp có thể gửi thông báo báo cáo lên **Slack** bằng Node `slack`.
   - Cấu hình:
     - **Webhook URL**: Lấy từ **Slack App** (tạo tại [Slack API](https://api.slack.com/)).
     - **Message**: `📊 Báo cáo ASO mới: {{ $json.appName }}. Link: {{ $json.docUrl }}`.

5. **Tối ưu hóa AI Prompt**:
   - Chỉnh sửa **prompt** cho AI để phù hợp với ngành nghề cụ thể (ví dụ: game, e-commerce, giáo dục).
   - Ví dụ:
     ```plaintext
     For a game app, focus on:
     - Player retention metrics.
     - In-app purchase strategies.