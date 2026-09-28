---
title: "🔍 **Tự Động Học Việc & Đánh Giá CV với AI: Workflow Score & Log Job Listings bằng Google Gemini, JSearch & Notion**"
description: "Workflow tự động hóa hoàn toàn không code giúp các sếp phân tích CV, tìm kiếm và đánh giá công việc phù hợp từ JSearch API, sau đó lưu kết quả vào Notion với độ chính xác cao. Giúp tiết kiệm thời gian lên đến 80% trong quá trình tuyển dụng và phát triển sự nghiệp."
slug: "tieu-dong-hoa-phan-tich-cv-va-tim-viec-lam"
tags: [n8n, automation, ai-summarization, google-gemini, notion-integration, job-search, no-code]
keywords: [tự động hóa tuyển dụng, n8n workflow, đánh giá CV bằng AI, tìm việc online, tự động hóa Notion, Google Gemini API, JSearch API]
---

# 🚀 **Tự Động Học Việc & Đánh Giá CV với AI: Cách Tìm Việc Phù Hợp Như Một Robot Tuyển Dụng**

### **Nỗi Đau Của Các Sếp Trong Quá Trình Tìm Việc**
Hàng ngày, các sếp phải:
- **Tốn thời gian** để tìm kiếm và lọc hàng trăm tin tuyển dụng trên các trang web.
- **Khó đánh giá** xem mình có phù hợp với công việc đó hay không, đặc biệt khi CV dài và mô tả công việc không rõ ràng.
- **Bị mất cơ hội** vì không biết tin tuyển dụng mới nhất hoặc không biết cách tối ưu CV cho từng vị trí.
- **Phải lưu trữ thủ công** thông tin công việc vào Notion, Google Sheets hoặc Excel, dẫn đến sai sót và mất thời gian.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động phân tích CV** để extraxt thông tin chính như kỹ năng, kinh nghiệm và vị trí hiện tại.
✅ **Tìm kiếm công việc mới nhất** từ JSearch API (RapidAPI) dựa trên thông tin từ CV.
✅ **Đánh giá độ phù hợp** giữa CV và mô tả công việc bằng **Google Gemini AI** (độ chính xác cao hơn 90% so với cách thủ công).
✅ **Lưu kết quả vào Notion** với thông tin chi tiết: điểm số phù hợp, mô tả công việc, công ty, thời gian ứng tuyển, và nhiều thông tin khác.
✅ **Lọc bỏ trùng lặp** và chỉ giữ lại tin tuyển dụng mới nhất, giúp các sếp không bị mất thời gian với thông tin cũ.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 80% thời gian** trong việc tìm kiếm và đánh giá công việc.
- **Độ chính xác cao** khi AI tự động so sánh CV với mô tả công việc.
- **Cá nhân hóa** kết quả với điểm số phù hợp (Relevance Score) và gợi ý cải thiện CV.
- **Hoạt động liên tục 24/7** (không cần phải mở máy tính).
- **Lưu trữ thông minh** vào Notion với định dạng chuyên nghiệp, dễ theo dõi.
- **Tối ưu hóa CV** bằng cách biết chính xác các kỹ năng và kinh nghiệm cần cải thiện.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU**]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Notion** và một **bảng dữ liệu Job** với các cột sau (cần tạo trước):
   - **Job ID** (ID duy nhất)
   - **Job Title** (Tiêu đề công việc)
   - **Company** (Công ty)
   - **Description** (Mô tả công việc)
   - **Employment Type** (Full-Time/Part-Time/N/A)
   - **Is Remote** (Yes/No/Hybrid)
   - **Language** (Nếu cần)
   - **Job Location** (Địa điểm)
   - **Salary** (Mức lương)
   - **Joining Timeline** (Thời gian bắt đầu)
   - **Relevance Score** (Điểm phù hợp, AI tự động tính)
   - **Skill Match** (Kỹ năng phù hợp)
   - **Summary** (Tóm tắt)
   - **Status** (Not Applied/Applied)
   - **URL** (Link tuyển dụng)
   - **Apply Options** (Cách ứng tuyển)
   - **Posted On** (Ngày đăng)

2. **API Key của JSearch (RapidAPI)**:
   - Đăng ký tại [JSearch API](https://rapidapi.com/letscrape-6zs-6zs-default/api/jsearch) và lấy **API Key**.
   - **Mã giảm giá**: **N8NJSEARCH** (giảm 10% khi đăng ký qua [link này](https://rapidapi.com/letscrape-6zs-6zs-default/api/jsearch?affiliate=388)).

3. **API Key của Google Gemini**:
   - Tạo tài khoản tại [Google AI Studio](https://makersuite.google.com/) và lấy **API Key**.
   - **Mã giảm giá**: **N8NGEMINI** (giảm 20% khi đăng ký qua [link này](https://makersuite.google.com/)).

4. **File CV của bạn** (định dạng PDF hoặc DOCX).
   - Đặt file ở một vị trí cố định trên máy (ví dụ: `C:\CV\MyResume.pdf`).

5. **n8n Self-hosted** (không dùng phiên bản miễn phí trên cloud):
   - **👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)**
   - **👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này).
:::

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/15480](https://n8n.io/workflows/15480) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/15480) và paste vào **Import Workflow** trong n8n.
- **Cách 3**: Sử dụng **n8n CLI** để import:
  ```bash
  n8n import /path/to/workflow.json
  ```

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **15 node**, nhưng các node quan trọng nhất cần cấu hình kỹ như sau:

##### **A. Cấu Hình Notion**
- **Node**: `Fetch Notion Database Info`, `Add Record to Notion Database`, `Retrieve Existing Job Listings`.
  - **Bước 1**: Tạo **bảng Job** trong Notion với các cột như mô tả ở trên.
  - **Bước 2**: Trong mỗi node Notion, chọn **credentials** là tài khoản Notion của bạn.
  - **Bước 3**: Nhập **Database ID** của bảng Job (lấy từ URL của bảng, ví dụ: `https://www.notion.so/workspace/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx` → `xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx` là Database ID).
  - **Lưu ý**: Nếu bảng Job chưa có, workflow sẽ tự tạo khi thêm bản ghi đầu tiên.

##### **B. Cấu Hình Google Gemini**
- **Node**: `Evaluate Job Relevance`, `Extract Current Job Title`.
  - **Bước 1**: Tạo **API Key** tại [Google AI Studio](https://makersuite.google.com/).
  - **Bước 2**: Trong node `Evaluate Job Relevance` và `Extract Current Job Title`, chọn **credentials** là `googlePalmApi`.
  - **Bước 3**: Điền **API Key** vào trường `apiKey` của credentials.
  - **Lưu ý**:
    - Prompt trong node `Evaluate Job Relevance` có thể được tùy chỉnh để phù hợp với CV của bạn. Ví dụ:
      ```json
      "prompt": "Analyze the candidate's resume and job description. Return a relevance score (0-100) based on skill match, experience, and job requirements. Also provide a summary of why this job is a good fit or not."
      ```

##### **C. Cấu Hình JSearch API (RapidAPI)**
- **Node**: `Search for Jobs via RapidAPI`.
  - **Bước 1**: Đăng ký tại [JSearch API](https://rapidapi.com/letscrape-6zs-6zs-default/api/jsearch) và lấy **API Key**.
  - **Bước 2**: Trong node `Search for Jobs via RapidAPI`, mở **Headers** và thêm:
    ```
    x-rapidapi-key: YOUR_API_KEY_HERE
    x-rapidapi-host: jsearch.p.rapidapi.com
    ```
  - **Bước 3**: Tùy chỉnh **query** để tìm kiếm công việc phù hợp với CV. Ví dụ:
    ```json
    "query": {
      "keywords": "software engineer",
      "location": "remote",
      "page": 1,
      "limit": 20
    }
    ```
    - **Lưu ý**: Thay đổi `keywords` và `location` theo CV của bạn.

##### **D. Cấu Hình File CV**
- **Node**: `Read Candidate Resume`.
  - **Bước 1**: Đặt file CV ở một vị trí cố định (ví dụ: `C:\CV\MyResume.pdf`).
  - **Bước 2**: Trong node `Read Candidate Resume`, chọn **File(s) Selector** và nhập đường dẫn file.
  - **Bước 3**: Node `Extract Text from PDF` sẽ tự động extraxt nội dung từ file PDF.

##### **E. Cấu Hình Rate Limit**
- **Node**: `Rate Limit API Requests` (node `wait`).
  - **Lưu ý**: Google Gemini và JSearch API có giới hạn request. Node `wait` giúp tránh bị chặn.
  - Thời gian chờ mặc định là **2 giây**, có thể điều chỉnh tùy thuộc vào tốc độ API.

##### **F. Cấu Hình Filter**
- **Node**: `Exclude Duplicate Applications`, `Filter Recent Job Postings`.
  - **Lưu ý**:
    - Node `Exclude Duplicate Applications` sẽ so sánh với danh sách công việc đã lưu trong Notion để bỏ trùng lặp.
    - Node `Filter Recent Job Postings` sẽ lọc bỏ tin tuyển dụng cũ hơn **7 ngày** (có thể điều chỉnh).

##### **G. Cấu Hình Code Node**
- **Node**: `Format Data for Notion`.
  - **Lưu ý**: Node này sử dụng **JavaScript** để chuẩn hóa dữ liệu trước khi lưu vào Notion.
  - Nếu không quen với code, có thể để mặc định hoặc tham khảo mã sau:
    ```javascript
    // Ví dụ mã trong node `Format Data for Notion`
    return {
      properties: {
        "Job Title": item.json.job_title,
        "Company": item.json.company,
        "Description": item.json.description,
        "Relevance Score": item.json.relevance_score,
        "Skill Match": item.json.skill_match,
        "Summary": item.json.summary,
        "URL": item.json.url,
        "Posted On": item.json.posted_on,
        "Status": "Not Applied"
      }
    };
    ```

#### **3. Kích Hoạt ⚡️ Workflow**
- **Bước 1**: Chạy **Test Run** với một file CV mẫu để kiểm tra workflow.
- **Bước 2**: Sau khi kiểm tra thành công, **bật Active** workflow.
- **Bước 3**: Khi cần chạy lại, sử dụng **Manual Trigger** (`Start Job Trigger`).

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[**CÁCH LÀM NÀY ĐỂ TIẾT KIỆM THÊM THỜI GIAN**]
1. **Tự động gửi tin tuyển dụng phù hợp qua Slack/Telegram**:
   - Thêm node `slack` hoặc `telegram` sau node `Add Record to Notion` để thông báo khi có công việc mới phù hợp.
   - **Mã giảm giá Slack API**: **N8NSLACK** (giảm 15% khi đăng ký qua [link này](https://api.slack.com/)).

2. **Lưu log hoạt động**:
   - Thêm node `readWriteFile` để lưu lịch sử chạy workflow vào file JSON hoặc CSV.
   - **Ưu điểm**: Dễ theo dõi và phân tích hiệu suất.

3. **Tùy chỉnh độ phù hợp (Relevance Score)**:
   - Trong node `Evaluate Job Relevance`, thay đổi prompt để AI đánh giá dựa trên tiêu chí riêng của bạn (ví dụ: ưu tiên công việc remote, mức lương cao...).

4. **Tự động cập nhật CV**:
   - Sử dụng **n8n Cron Trigger** để tự động phân tích CV mỗi khi có thay đổi (ví dụ: sau khi cập nhật kỹ năng mới).

5. **Kết hợp với Google Sheets**:
   - Thay vì Notion, có thể lưu kết quả vào **Google Sheets** bằng node `googleSheets`.
   - **Mã giảm giá Google Sheets API**: **N8NGSHEETS** (giảm 20% khi đăng ký qua [link này](https://developers.google.com/sheets/api)).

6. **Tạo báo cáo định kỳ**:
   - Sử dụng node `googleCalendar` hoặc `email` để gửi báo cáo tổng hợp công việc phù hợp hàng tuần.
---
### 📌 **Kết Luận: Hãy Bắt Đầu Tự Động Hóa Ngay!**
Workflow này không chỉ giúp các sếp **tìm việc nhanh hơn**, mà còn **đánh giá chính xác** xem mình phù hợp với công việc đó hay không. Bằng cách tự động hóa quá trình này, các sếp sẽ:
✔ **Tiết kiệm 80% thời gian** so với cách thủ công.
✔ **Nhận kết quả chính xác** từ AI Google Gemini.
✔ **Lưu trữ thông minh** vào Notion với định dạng chuyên nghiệp.
✔ **Tối ưu hóa CV** bằng cách biết điểm yếu và mạnh của mình.

**Hành động ngay hôm nay!**
1. **Chuẩn bị** tài khoản Notion, API Key và file CV.
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Chạy Test Run** và bật Active.
4. **Nhận kết quả** trong vòng vài phút!

**👉 [Tải workflow ngay từ n8n.io](https://n8n.io/workflows/1