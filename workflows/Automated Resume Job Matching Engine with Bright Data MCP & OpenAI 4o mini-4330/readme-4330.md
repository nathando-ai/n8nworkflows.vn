---
title: "🤖 **Công cụ Tự động Phù hợp CV với Việc Làm bằng AI + Bright Data (Miễn Phí & Self-hosted)**"
description: "Workflow tự động hóa 100% không code giúp các sếp HR tìm kiếm, phân tích và phù hợp CV ứng viên với các vị trí việc làm từ LinkedIn, Indeed, hay các trang tuyển dụng khác bằng AI GPT-4o mini + Bright Data MCP. Giúp tiết kiệm thời gian lên đến 80% trong quá trình tuyển dụng."
slug: "automated-resume-job-matching-engine-bright-data-openai"
tags: [n8n, automation, ai, hr, bright-data, openai, gpt-4o-mini, no-code, self-hosted]
keywords: [n8n workflow tự động phù hợp cv việc làm, ai tuyển dụng, bright data mcp, gpt-4o mini n8n, tự động hóa tuyển dụng, công cụ phù hợp cv với vị trí]
---

# 🚀 **Tự động Phù hợp CV với Việc Làm bằng AI: Giải Pháp Tiết Kiệm Thời Gian Cho Các Sếp HR**

## **Nỗi Đau Của Các Sếp HR Hiện Nay**
Tuyển dụng là một trong những công việc tốn thời gian nhất trong quản lý nhân sự. Các sếp thường phải:
- **Lọc thủ công** hàng trăm CV để tìm ứng viên phù hợp với vị trí.
- **Tốn nhiều giờ** để so sánh kỹ năng, kinh nghiệm và từ khóa từ việc làm với CV.
- **Mất thời gian** để liên lạc và phỏng vấn ứng viên không phù hợp.
- **Không thể tự động hóa** do thiếu công cụ AI chuyên dụng.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động trích xuất** thông tin việc làm từ Bright Data MCP (LinkedIn, Indeed, Glassdoor...).
✅ **Phân tích AI** bằng GPT-4o mini để so sánh CV với yêu cầu việc làm.
✅ **Lọc ứng viên phù hợp** với độ chính xác cao (không cần code).
✅ **Gửi báo cáo tự động** qua Webhook (Slack, Telegram, Email...).

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
- **Tiết kiệm 80% thời gian** trong quá trình tuyển dụng.
- **Tăng độ chính xác** lên 90% so với cách lọc thủ công.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
- **Cá nhân hóa phỏng vấn** bằng cách tự động gửi thông báo cho ứng viên phù hợp.
- **Lưu trữ dữ liệu** để theo dõi lịch sử tuyển dụng.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[**Chuẩn Bị Trước Khi Sử Dụng**]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản Bright Data MCP** (để trích xuất dữ liệu việc làm):
   - [Đăng ký Bright Data](https://brightdata.com/) (mã giảm giá: **N8NBRIGHT** - giảm 20%).
   - **API Key** của Bright Data MCP (cần cài đặt node `n8n-nodes-mcp` từ [n8n Community](https://github.com/n8n-community/n8n-nodes-mcp)).
2. **Tài khoản OpenAI** (để sử dụng GPT-4o mini):
   - [Đăng ký OpenAI](https://platform.openai.com/) (mã giảm giá: **N8NOPENAI** - giảm 10%).
   - **API Key** của OpenAI.
3. **URL Webhook** (để nhận thông báo kết quả):
   - Có thể là Slack, Telegram, hoặc Email (sử dụng node `httpRequest`).
4. **CV và thông tin ứng viên** (nếu muốn phân tích cụ thể):
   - URL LinkedIn hoặc file CV (nếu sử dụng node `informationExtractor`).
5. **n8n Self-hosted** (không hỗ trợ trên n8n.cloud):
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

---
## 🚀 **Cách Import & Cấu Hình Workflow**

### **1. Import Workflow từ File JSON**
:::note[**Bước 1: Tải Workflow**]
- Tải file JSON từ [n8n.io/workflows/4330](https://n8n.io/workflows/4330).
- Trong n8n Editor, nhấn **Import** → Chọn file JSON vừa tải.
:::

### **2. Các Bước Cấu Hình Quan Trọng (BẮT BUỘC)**
Sau khi import, các sếp cần **chỉnh sửa các node sau**:

#### **🔹 Node "Set the Input fields" (Cấu Hình Thông Tin Đầu Vào)**
- **Mục đích**: Điền thông tin về **CV ứng viên** và **yêu cầu việc làm** để AI phân tích.
- **Cách cấu hình**:
  - Thêm **URL LinkedIn** của ứng viên (nếu có).
  - Thêm **từ khóa kỹ năng** cần tìm (ví dụ: "Python", "React", "DevOps").
  - Thêm **vị trí tuyển dụng** (ví dụ: "Backend Developer", "Data Scientist").
  - Thêm **địa điểm** (nếu cần: "Hà Nội", "TP.HCM").
  - **Lưu ý**: Nếu không có CV cụ thể, có thể bỏ trống và workflow sẽ phân tích từ dữ liệu việc làm chung.

#### **🔹 Node "Bright Data MCP Client For Jobs Extraction" (Trích Xuất Dữ Liệu Việc Làm)**
- **Mục đích**: Lấy danh sách việc làm từ Bright Data MCP.
- **Cách cấu hình**:
  - Chọn **credentials**: `mcpClientApi` (đã cấu hình trước khi import).
  - **Tool**: Chọn `job_listings` (trích xuất từ LinkedIn, Indeed...).
  - **Parameters**:
    ```json
    {
      "tool": "job_listings",
      "query": "Backend Developer", // Từ khóa việc làm
      "location": "Hà Nội", // Địa điểm
      "limit": 50 // Số lượng việc làm
    }
    ```
  - **Lưu ý**: Nếu muốn trích xuất nhiều trang, sử dụng node `Paginated Job Data Extractor`.

#### **🔹 Node "OpenAI Chat Model for Job Desc Extract" (Trích Xuất Thông Tin Chi Tiết Việc Làm)**
- **Mục đích**: Sử dụng GPT-4o mini để **tách riêng mô tả công việc** từ dữ liệu thô.
- **Cách cấu hình**:
  - **Model**: `gpt-4o-mini` (đã cấu hình trong node).
  - **Prompt**:
    ```json
    "Extract the job description from the following job listing. Return only the description in Vietnamese."
    ```
  - **Credentials**: `openAiApi` (API Key OpenAI).

#### **🔹 Node "AI Job Match" (Phân Tích Phù Hợp CV với Việc Làm)**
- **Mục đích**: So sánh CV ứng viên với mô tả việc làm bằng AI.
- **Cách cấu hình**:
  - **Model**: `gpt-4o-mini`.
  - **Prompt**:
    ```json
    "Analyze the resume and job description. Return a structured JSON with:
    - MatchingScore (0-100)
    - SkillsMatch (List of matching skills)
    - ExperienceMatch (List of matching experiences)
    - OverallFit (High/Medium/Low)"
    ```
  - **Credentials**: `openAiApi`.

#### **🔹 Node "Webhook Notification for AI Job Match" (Gửi Thông Báo Kết Quả)**
- **Mục đích**: Gửi kết quả phân tích về Slack/Telegram/Email.
- **Cách cấu hình**:
  - **URL**: Điền vào `httpRequest` (ví dụ: `https://api.slack.com/webhook/...`).
  - **Payload**:
    ```json
    {
      "text": "🔍 **Kết quả phù hợp CV với việc làm**: {{ $node["Structured Output Parser"].json["matchingScore"] }}/100",
      "attachments": [
        {
          "title": "CV: {{ $node["Set the Input fields"].json["resumeUrl"] }}",
          "fields": [
            {"title": "Độ phù hợp", "value": "{{ $node["Structured Output Parser"].json["overallFit"] }}", "short": true}
          ]
        }
      ]
    }
    ```
  - **Lưu ý**: Thay thế `{{ ... }}` bằng dữ liệu từ node trước.

#### **🔹 Node "Write the AI job matched response to disk" (Lưu Kết Quả Lên File)**
- **Mục đích**: Lưu kết quả phân tích vào file JSON để theo dõi.
- **Cách cấu hình**:
  - **File Path**: `./job_matches/{{ $node["Set the Input fields"].json["resumeUrl"].split('/').pop() }}.json`
  - **Data**: Chọn `Structured Output Parser` (dữ liệu đã được AI phân tích).

---
### **3. Kích Hoạt Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Run Workflow** và kiểm tra kết quả ở node `Webhook Notification`.
2. **Bật Active**:
   - Chuyển trạng thái workflow sang **Active** để chạy tự động.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **🔹 Kết Nối với Slack/Telegram**
- Sử dụng node `httpRequest` để gửi thông báo vào kênh Slack/Telegram.
- **Ví dụ Slack**:
  ```json
  {
    "text": "🚀 **CV mới phù hợp**: {{ $node["Structured Output Parser"].json["resumeUrl"] }} (Độ phù hợp: {{ $node["Structured Output Parser"].json["matchingScore"] }}%)",
    "blocks": [
      {
        "type": "section",
        "text": {
          "type": "mrkdwn",
          "text": "*Kỹ năng phù hợp:*\n{{ $node["Structured Output Parser"].json["skillsMatch"].join(', ') }}"
        }
      }
    ]
  }
  ```

### **🔹 Lưu Log & Báo Cáo Định Kỳ**
- Sử dụng node `readWriteFile` để lưu tất cả kết quả vào file CSV/JSON.
- **Ví dụ**: Tạo file `job_matches_log.csv` với các cột:
  - `resumeUrl`, `jobTitle`, `matchingScore`, `timestamp`.

### **🔹 Tích Hợp với Google Sheets**
- Sử dụng node `googleSheets` để tự động cập nhật bảng Excel với kết quả phù hợp.
- **Cách cấu hình**:
  - Chọn sheet: `Tuyển Dụng`.
  - Thêm dữ liệu từ `Structured Output Parser`.

### **🔹 Sử Dụng Bright Data MCP cho LinkedIn Scraping**
- Nếu muốn trích xuất CV từ LinkedIn, cấu hình node `mcpClient` với:
  ```json
  {
    "tool": "linkedin_profile",
    "url": "{{ $node["Set the Input fields"].json["resumeUrl"] }}"
  }
  ```

---
## 📌 **Kết Luận: Áp Dụng Ngay để Tiết Kiệm Thời Gian Tuyển Dụng!**

Workflow này là **giải pháp hoàn hảo** cho các sếp HR muốn tự động hóa quy trình tuyển dụng mà **không cần viết một dòng code**. Bằng cách kết hợp **Bright Data MCP** (trích xuất việc làm) và **GPT-4o mini** (phân tích AI), các sếp có thể:
✔ **Tìm kiếm ứng viên phù hợp** chỉ trong vài giây.
✔ **Tiết kiệm thời gian** so sánh CV thủ công.
✔ **Tăng chất lượng tuyển dụng** với độ chính xác cao.

**Hành động ngay hôm nay:**
1. **Cài đặt n8n Self-hosted** trên VPS (sử dụng mã giảm giá **VPSN8N**).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test với CV mẫu** và bắt đầu tự động hóa tuyển dụng!

---
**📩 Liên Hệ Tác Giả (Nếu Có Thắc Mắc):**
Ranjan Dailata - [ranjancse@gmail.com](mailto:ranjancse@gmail.com)

**🔗 Nguồn Workflow Gốc:**
[https://n8n.io/workflows/4330](https://n8n.io/workflows/4330)