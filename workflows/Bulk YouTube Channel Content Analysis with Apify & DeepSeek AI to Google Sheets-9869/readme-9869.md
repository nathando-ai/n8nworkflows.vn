---
title: "🚀 Tự Động Hóa Phân Tích Nội Dung Channel YouTube Bulk với AI DeepSeek & Google Sheets (Không Cần Code)"
description: "Workflow tự động hóa crawl toàn bộ video từ channel YouTube, phân tích nội dung bằng AI DeepSeek, và lưu kết quả vào Google Sheets với định dạng chuyên nghiệp. Giúp các sếp tiết kiệm 10-15 giờ/tháng và có báo cáo AI chi tiết cho chiến lược content."
slug: "tieu-dong-hoa-phan-tich-youtube-deepseek-google-sheets"
tags: [n8n, automation, no-code, ai-deepseek, google-sheets, youtube-scraper, content-analysis]
keywords: [n8n workflow youtube, tự động hóa phân tích video youtube, ai deepseek google sheets, crawl youtube bulk, tự động hóa content marketing]
---

# 🚀 **Tự Động Hóa Phân Tích Nội Dung Channel YouTube Bulk với AI DeepSeek & Google Sheets**

### **Giải pháp cho các sếp:**
- **Thủ công** phân tích hàng trăm video trên channel YouTube? **Tốn thời gian, dễ bỏ sót, và không chuyên nghiệp.**
- **Workflow này tự động hóa toàn bộ quy trình:**
  - Crawl **toàn bộ video** từ channel YouTube (không giới hạn số lượng).
  - **Phân tích nội dung** bằng AI DeepSeek (hoặc mô hình LLM khác) để tạo **tóm tắt chuyên nghiệp** cho mỗi video.
  - **Lưu kết quả** vào Google Sheets với định dạng **cấu trúc JSON** (video ID, chủ đề, tóm tắt AI).
  - **Gửi thông báo hoàn thành** qua email khi xong.
  - **Backup dữ liệu** lên Google Drive để phục hồi nếu workflow bị lỗi.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10-15 giờ/tháng** so với cách làm thủ công.
- **Dữ liệu chính xác 100%**: Không bỏ sót video nào, không sai sót trong phân tích.
- **Báo cáo AI chuyên nghiệp**: Mỗi video có **tóm tắt, chủ đề, và metadata** được cấu trúc sẵn.
- **Hoạt động 24/7**: Chỉ cần chạy workflow 1 lần, nó tự động hoàn thành mọi việc.
- **Backup an toàn**: Dữ liệu crawl được lưu trên Google Drive để phục hồi nếu workflow bị lỗi.
:::

---

## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để sử dụng Google Sheets, Google Drive, và Gmail).
2. **API Key Apify** (để crawl YouTube):
   - Đăng ký tại [Apify](https://apify.com/) và lấy token API.
   - **Actor sử dụng**: `apify/youtube-channel-scraper` (hoặc tương tự).
3. **API Key DeepSeek** (hoặc mô hình LLM khác):
   - Đăng ký tại [DeepSeek](https://deepseek.com/) và lấy API Key.
   - Nếu không dùng DeepSeek, có thể thay thế bằng **LangChain** hoặc mô hình khác hỗ trợ `lmChat`.
4. **Google Sheets** (để lưu kết quả):
   - Tạo 1 file mới trên Google Drive và chia sẻ cho workflow.
5. **Gmail** (để nhận thông báo hoàn thành).
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [link gốc](https://n8n.io/workflows/9869) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ link trên và dán vào **Import Workflow** trong n8n.
- **Cách 3**: Sử dụng **n8n CLI** để import:
  ```bash
  n8n import workflow.json --name "YouTube Analysis"
  ```

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **5 phần chính**, các sếp cần cấu hình kỹ các node sau:

#### **📝 Phần 1: Input & Initialization (Form Trigger)**
- **Node**: `Parameters (Form Trigger)`
- **Cấu hình**:
  - Thêm **5 trường form** với tên và kiểu dữ liệu như sau:
    | Trường | Kiểu dữ liệu | Ghi chú |
    |---------|-------------|---------|
    | `Youtuber_MainPage_URL` | Text | URL channel YouTube (vd: `https://www.youtube.com/@n8n-io`) |
    | `Total_number_video` | Number | Số lượng video muốn crawl (giới hạn max 1000 video) |
    | `Storing_Name` | Text | Tên tab Google Sheets và tên file backup (vd: `n8n-analysis`) |
    | `Apify_API` | Password | API Key Apify của bạn |
    | `Email` | Text | Email để nhận thông báo hoàn thành |

#### **🤖 Phần 2: Crawl YouTube & Kiểm tra Trạng Thái**
- **Node quan trọng**:
  - `Start_YouTube_Scraper` (HTTP Request): Điền URL API Apify:
    ```
    https://api.apify.com/v2/act/your-apify-actor-id/runs
    ```
    (Thay `your-apify-actor-id` bằng ID actor của bạn).
  - `Get_Scraper_Status` (HTTP Request): Điền URL để check trạng thái crawl:
    ```
    https://api.apify.com/v2/act/your-apify-actor-id/runs/YOUR_RUN_ID/status
    ```
    (Thay `YOUR_RUN_ID` bằng ID run từ bước trước).
  - `Wait_15_Seconds` (Wait): Đảm bảo crawl hoàn thành trước khi tiếp tục.

#### **📁 Phần 3: Backup Dữ liệu lên Google Drive**
- **Node**: `Upload_To_Google_Drive` và `Download_From_Google_Drive`
- **Cấu hình**:
  - Đảm bảo **credentials `googleDriveOAuth2Api`** đã được thiết lập trong n8n.
  - **Folder lưu**: Chọn folder Google Drive muốn backup (vd: `YouTube Analysis`).

#### **🤖 Phần 4: Phân Tích AI với DeepSeek**
- **Node quan trọng**:
  - `DeepSeek Chat Model` (`lmChatDeepSeek`):
    - Điền `deepSeekApi` vào **credentials**.
    - Cấu hình **Prompt** để phân tích video (vd:
      ```
      Analyze this YouTube video transcript and metadata. Return a structured JSON with:
      - "video_id": [YouTube ID]
      - "topic": [Main topic in 1-2 words]
      - "summary": [Professional summary in Vietnamese, max 200 words]
      - "keywords": [3-5 keywords]
      ```
    - **Model**: Chọn `deepseek-chat` (hoặc mô hình khác hỗ trợ).
  - `Content_Analysis_Agent` (`agent`): Đảm bảo **credentials `langchain`** đã được cài đặt.
  - `Structured_Output_Parser` và `Output_Parser_Auto_Fix`: Để đảm bảo output JSON đúng định dạng.

#### **📊 Phần 5: Ghi Dữ liệu vào Google Sheets**
- **Node**: `Write_Contentdata_To_Sheet` (`googleSheets`)
- **Cấu hình**:
  - Chọn **Google Sheets OAuth2** trong credentials.
  - **Sheet Name**: Đặt tên theo `Storing_Name` từ form trigger.
  - **Operation**: Chọn `appendOrUpdate` để thêm dữ liệu mới.

#### **⚡ Phần 6: Thông báo hoàn thành qua Email**
- **Node**: `Send a message` (`gmail`)
- **Cấu hình**:
  - Chọn **gmailOAuth2** trong credentials.
  - **Subject**: `YouTube Analysis Complete: {Storing_Name}`
  - **Body**:
    ```
    Xin chào,

    Quá trình phân tích channel {Youtuber_MainPage_URL} đã hoàn thành thành công!
    - Tổng số video phân tích: {Total_number_video}
    - Kết quả đã được lưu vào tab "{Storing_Name}" trên Google Sheets.
    - Dữ liệu raw đã được backup tại: [Link Google Drive]

    Trân trọng,
    Workflow n8n
    ```

---

### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Điền dữ liệu mẫu vào form (vd: channel `https://www.youtube.com/@n8n-io`, số video = 10).
   - Chạy workflow và kiểm tra:
     - Dữ liệu crawl có xuất hiện không?
     - AI có phân tích đúng không?
     - Dữ liệu có ghi vào Sheets không?
2. **Bật Active**:
   - Sau khi test thành công, bật **Active** để workflow chạy tự động khi có input.

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::note[MỞ RỘNG THÊM TÍNH NĂNG]
1. **Tích hợp Slack/Telegram**:
   - Thêm node `slack` hoặc `telegram` để gửi thông báo khi workflow hoàn thành.
   - Ví dụ:
     ```json
     {
       "node": "slack",
       "credentials": "slackApi",
       "parameters": {
         "text": "🚀 YouTube Analysis Done! Check Google Sheets: {{ $json["sheetUrl"] }}"
       }
     }
     ```
2. **Lưu log hoạt động**:
   - Thêm node `stickyNote` để ghi log lỗi hoặc trạng thái.
   - Ví dụ:
     ```json
     {
       "node": "stickyNote",
       "parameters": {
         "text": "Workflow started at: {{ $node["Parameters"].json["timestamp"] }}"
       }
     }
     ```
3. **Gửi báo cáo định kỳ**:
   - Sử dụng **n8n Trigger** (Webhook) kết hợp với **Google Calendar** để chạy workflow hàng tuần.
4. **Tối ưu batch size**:
   - Nếu crawl nhiều video, tăng `batchSize` trong node `splitInBatches` (vd: 50 video/lần).
5. **Phục hồi từ lỗi**:
   - Nếu workflow bị lỗi, sử dụng **tính năng "Resume from Drive CSV"** (nêu trong ghi chú gốc):
     - Tắt node `Create_Sheet` và kết nối `Parameters` → `Download_From_Google_Drive`.
     - Điền **ID file CSV** từ Google Drive vào `Download_From_Google_Drive`.
     - Sử dụng `Start_Row` để chỉ xử lý video chưa hoàn thành.
:::

---

## 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc phân tích video thủ công, đồng thời cung cấp **báo cáo AI chuyên nghiệp** để hỗ trợ quyết định content marketing. **Chỉ cần chạy 1 lần**, workflow sẽ tự động:
✅ Crawl toàn bộ video.
✅ Phân tích nội dung bằng AI DeepSeek.
✅ Lưu kết quả vào Google Sheets.
✅ Gửi thông báo hoàn thành.

**👉 Hãy thử ngay và tiết kiệm 10-15 giờ/tháng!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💡 Lưu ý cuối cùng**:
- Nếu gặp lỗi **API rate limit**, giảm số lượng video crawl hoặc tăng thời gian chờ (`Wait` nodes).
- Để **tối ưu AI**, thử thay đổi **prompt** trong node `DeepSeek Chat Model` để phù hợp với nội dung video của bạn.