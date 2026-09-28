---
title: "🚀 Tự Động Hóa Scraping Pinterest Bằng Từ Khóa + AI Agent & BrightData (Không Cần Code)"
description: "Workflow tự động hóa lấy dữ liệu Pinterest dựa trên từ khóa, xử lý bằng AI Claude Sonnet 4 và lưu kết quả vào Google Sheets. Giúp các sếp tiết kiệm thời gian nghiên cứu thị trường, phân tích xu hướng và tối ưu nội dung marketing chỉ trong vài giây."
slug: "tieu-dong-hoa-scraping-pinterest-ai-agent-brightdata"
tags: [n8n, automation, ai-agent, brightdata, google-sheets, content-marketing]
keywords: [scraping pinterest tự động, ai agent n8n, brightdata api, lấy dữ liệu pinterest bằng từ khóa, tối ưu nội dung marketing]
---

# 🚀 **Tự Động Hóa Scraping Pinterest Bằng Từ Khóa + AI Agent & BrightData**

### **Giải pháp cho các sếp muốn:**
- **Tìm kiếm dữ liệu Pinterest nhanh chóng** mà không cần viết code.
- **Phân tích xu hướng thị trường** từ hàng ngàn bài đăng Pinterest chỉ bằng một từ khóa.
- **Tự động hóa quá trình nghiên cứu nội dung** để tối ưu chiến dịch marketing.
- **Lưu kết quả vào Google Sheets** để phân tích định kỳ hoặc chia sẻ với team.

---
### **🎯 Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10-20 giờ/tháng** so với cách làm thủ công.
- **Dữ liệu chính xác và cập nhật** từ Pinterest (thông qua BrightData).
- **Tối ưu nội dung** nhờ AI Claude Sonnet 4 phân tích và enrich từ khóa.
- **Hoạt động 24/7** mà không cần can thiệp người dùng.
- **Lưu trữ dữ liệu sạch** vào Google Sheets với định dạng chuẩn (Tiêu đề, URL, Nội dung, Ảnh, Hashtags...).
:::

---
### **🔧 Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản BrightData** (để scraping Pinterest):
   - [Đăng ký BrightData](https://brightdata.com/) (sử dụng mã giới thiệu **N8NBRIGHT** để giảm 10% phí đầu tiên).
   - **API Key** và **Proxy List** từ BrightData (cần cấu hình trong node `BrightData Pinterest Scraping`).
   - **Snapshot ID** (nếu đã có dự án scraping trước đó).

2. **Tài khoản Google Sheets**:
   - **Google OAuth 2.0 API Key** (cấu hình trong `googleSheetsOAuth2Api`).
   - **File Google Sheets mẫu** (cần tạo trước để lưu kết quả):
     - [Mẫu Google Sheets](https://docs.google.com/spreadsheets/d/1XyZABC123/edit) (sao chép và thay thế `SAMPLE_SHEET_ID` trong workflow).

3. **Tài khoản Anthropic API** (để sử dụng AI Claude Sonnet 4):
   - [Đăng ký Anthropic](https://www.anthropic.com/) và lấy **API Key**.
   - **Model**: `claude-sonnet-4-20250514` (đã cấu hình sẵn trong workflow).

4. **n8n Self-hosted** (không dùng phiên bản miễn phí):
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

---
### **🚀 Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/5193](https://n8n.io/workflows/5193) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/5193) và paste vào **Create Workflow** → **Import JSON**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình BrightData**
- **Node**: `BrightData Pinterest Scraping` và `Check Scraping Status`.
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_BRIGHTDATA_API_KEY",
      "Content-Type": "application/json"
    }
    ```
  - **Body (POST request)**:
    ```json
    {
      "keyword": "{{$node["Pinterest Keyword Input"].json["keyword"]}}",
      "proxy": "residential:US:NY:port_80",
      "snapshot_type": "pinterest_search"
    }
    ```
  - **URL**:
    ```
    https://api.brightdata.com/v1/snapshots
    ```

##### **B. Cấu hình Google Sheets**
- **Node**: `Save Pinterest Data to Google Sheets`.
  - **Spreadsheet ID**: Thay thế `SAMPLE_SHEET_ID` bằng ID của file Sheets bạn tạo.
  - **Sheet Name**: Đặt tên sheet (ví dụ: `Pinterest_Data_${date}`).
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_GOOGLE_OAUTH2_API_KEY"
    }
    ```

##### **C. Cấu hình Anthropic (AI Claude Sonnet 4)**
- **Node**: `Anthropic Chat Model`.
  - **Credentials**: Chọn `anthropicApi` (đã cấu hình trước khi import).
  - **Model**: Đã mặc định là `claude-sonnet-4-20250514`.

##### **D. Cấu hình AI Agent**
- **Node**: `Keyword-based Scraping Agent`.
  - **Tools**: Đã liên kết tự động với các node khác (BrightData, Claude, Google Sheets).
  - **Prompt mặc định**:
    ```
    Analyze the keyword "{{$node["Pinterest Keyword Input"].json["keyword"]}}"
    and return structured data for scraping Pinterest.
    ```

##### **E. Node `Wait for 1 Minute`**
- **Lưu ý**: Node này **đang bị tắt** (disabled) trong workflow gốc. Nếu scraping mất thời gian, các sếp có thể bật lại và điều chỉnh thời gian chờ.

##### **F. Node `Format & Extract Pinterest Content`**
- **Code mẫu** (nếu cần chỉnh sửa):
  ```javascript
  // Example: Extract and format data from BrightData response
  const data = $input.all();
  return data.map(item => ({
    Title: item.title,
    URL: item.url,
    Content: item.description,
    ImageURL: item.image_url,
    Hashtags: item.hashtags,
    Likes: item.likes
  }));
  ```

#### **3. Kích hoạt ⚡️**
1. **Test run** với từ khóa mẫu (ví dụ: `"digital marketing"`).
2. **Bật Active workflow** và kiểm tra Google Sheets để xem kết quả.
3. **Xem log** trong n8n để debug nếu có lỗi (ví dụ: BrightData rate limit, Google Sheets permission).

---
### **✍️ Mẹo & gợi ý nâng cao**
:::info[TIẾP CẬN HƠN]
1. **Kết hợp với Slack/Telegram**:
   - Thêm node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram` để thông báo kết quả scraping.
   - **Ví dụ**:
     ```json
     {
       "text": "Scraping completed for keyword: {{$node["Pinterest Keyword Input"].json["keyword"]}}",
       "channel": "#pinterest-data"
     }
     ```

2. **Lưu log scraping**:
   - Thêm node `n8n-nodes-base.fileSystem` để lưu file JSON của kết quả scraping vào VPS.
   - **Cú pháp**:
     ```json
     {
       "path": "/data/pinterest_scrapes/{{$node["Pinterest Keyword Input"].json["keyword"]}}.json",
       "fileContent": "{{$json}}"
     }
     ```

3. **Tự động gửi báo cáo định kỳ**:
   - Sử dụng **n8n Cron Trigger** để chạy workflow hàng tuần/month và gửi báo cáo qua email (node `n8n-nodes-base.email`).

4. **Phân tích dữ liệu với AI**:
   - Sử dụng **LangChain Agent** để tổng hợp xu hướng từ dữ liệu Pinterest (ví dụ: từ khóa hot, hashtag phổ biến).

5. **Optimize BrightData Proxy**:
   - Thay đổi proxy trong `BrightData Pinterest Scraping` để tránh bị block (ví dụ: `residential:US:CA:port_80`).
:::

---
### **📌 Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa nghiên cứu thị trường trên Pinterest mà không cần viết code. Bằng cách kết hợp **BrightData** (scraping), **Anthropic Claude Sonnet 4** (AI phân tích), và **Google Sheets** (lưu trữ), các sếp có thể:
✅ **Tiết kiệm thời gian** so với cách làm thủ công.
✅ **Nắm bắt xu hướng thị trường** nhanh chóng.
✅ **Tối ưu nội dung marketing** dựa trên dữ liệu thực tế.

**Hành động ngay!**
1. **Chuẩn bị tài khoản** (BrightData, Google Sheets, Anthropic).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test run** với từ khóa mẫu và **bật hoạt động 24/7**!

---
**💡 Gợi ý thêm**: Nếu cần **scraping nhiều nền tảng** (Pinterest, Instagram, TikTok), các sếp có thể mở rộng workflow bằng cách thêm **BrightData cho các nền tảng khác** và kết hợp với **AI Agent** để phân tích tổng hợp.

---
**🚀 Cảm ơn các sếp đã đọc!** Nếu có vấn đề, hãy để lại comment dưới đây hoặc liên hệ qua [n8n Community](https://community.n8n.io/). 😊