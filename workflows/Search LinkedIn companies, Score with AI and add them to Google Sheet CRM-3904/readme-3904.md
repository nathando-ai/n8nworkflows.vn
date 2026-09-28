---
title: "🚀 Tự Động Hóa Tìm Kiếm & Đánh Giá Doanh Nghiệp LinkedIn + Lưu Trữ CRM Google Sheets (AI Lead Scoring)"
description: "Workflow tự động hóa tìm kiếm doanh nghiệp LinkedIn, đánh giá tiềm năng bằng AI, và lưu trữ vào Google Sheets CRM - tiết kiệm 10+ giờ/tháng cho bộ phận Sales/Marketing. Kết quả: Danh sách doanh nghiệp được sàng lọc và đánh giá chính xác, tối ưu hóa chiến dịch outreach."
slug: "tu-dong-hoa-tim-kiem-danh-gia-doanh-nghiep-linkedin-ai-lead-scoring"
tags: [n8n, automation, sales, marketing, ai-lead-scoring, google-sheets, linkedin-api]
keywords: [tự động hóa tìm kiếm LinkedIn, AI đánh giá doanh nghiệp, CRM Google Sheets, tự động hóa sales, Ghost Genius API, OpenAI lead scoring]
---

# 🚀 **Tự Động Hóa Tìm Kiếm Doanh Nghiệp LinkedIn, Đánh Giá AI + Lưu Trữ CRM Google Sheets**

## **🔥 Giới Thiệu: Giải Pháp Tự Động Hóa Cho Bộ Phận Sales/Marketing**
Bạn đã bao giờ phải **tìm kiếm thủ công** danh sách doanh nghiệp mục tiêu trên LinkedIn, sau đó **đánh giá tiềm năng** bằng cách phân tích thủ công, rồi **lưu trữ vào CRM** để theo dõi? Quá trình này không chỉ tốn **thời gian** mà còn dễ **bỏ sót** hoặc **lặp lại** dữ liệu.

**Workflow này giải quyết tất cả:**
✅ **Tìm kiếm tự động** doanh nghiệp trên LinkedIn (với Ghost Genius API)
✅ **Đánh giá tiềm năng** bằng AI (OpenAI) dựa trên nhiều tiêu chí (số lượng follower, website, ngành nghề,…)
✅ **Lọc bỏ trùng lặp** và **lưu trữ vào Google Sheets CRM** (cập nhật liên tục)
✅ **Tối ưu hóa outreach** bằng cách chỉ tiếp cận doanh nghiệp có **score cao**

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** so với cách làm thủ công.
- **Danh sách doanh nghiệp được sàng lọc chính xác** (không trùng lặp, có score AI).
- **Cập nhật liên tục** (không cần update thủ công).
- **Tối ưu hóa chiến dịch outreach** bằng cách chỉ tiếp cận doanh nghiệp có tiềm năng cao.
- **Hoạt động 24/7** (không phụ thuộc vào giờ làm việc).
:::

---
## **🔧 Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
### **📌 Tài Khoản & API Keys**
| **Dịch Vụ**          | **Liên Hệ** | **Ghi Chú** |
|----------------------|-------------|-------------|
| **Ghost Genius API** | [ghostgenius.fr](https://ghostgenius.fr) | API để tìm kiếm và lấy thông tin doanh nghiệp LinkedIn. |
| **Google Sheets**     | [Google Workspace](https://workspace.google.com) | CRM để lưu trữ danh sách doanh nghiệp. |
| **OpenAI API**       | [platform.openai.com](https://platform.openai.com) | Đánh giá tiềm năng doanh nghiệp bằng AI. |

### **📝 Tham Số Cần Điền**
1. **API Key Ghost Genius** (để cấu hình `Header Auth` trong node `Search Companies` và `Get Company Info`).
2. **Google Sheets OAuth 2.0** (để kết nối với node `Check If Company Exists` và `Add Company to CRM`).
3. **OpenAI API Key** (để cấu hình node `AI Company Scoring`).
4. **Thông tin biến (Variables)** trong node `Set Variables` (để tùy chỉnh AI scoring và điều kiện lọc).

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/3904](https://n8n.io/workflows/3904) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/3904) và dán vào **Create Workflow** trong n8n.

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
#### **🔹 Node `Search Companies` (httpRequest)**
- **Tham số quan trọng:**
  - **URL:** `https://api.ghostgenius.fr/v1/companies/search`
  - **Headers:**
    - `Authorization: Bearer <API_KEY_GHOST_GENIUS>`
    - `Content-Type: application/json`
  - **Body (JSON):**
    ```json
    {
      "query": "growth marketing agency",
      "location": "VN",
      "size": "11-50",
      "max_pages": 10  // Thay đổi để test (mỗi page ~100 kết quả)
    }
    ```
  - **Lưu ý:**
    - **Không vượt quá 1000 kết quả** (tương đương 100 trang LinkedIn).
    - **Tùy chỉnh `query`, `location`, `size`** theo nhu cầu (ví dụ: `query: "AI startup"`, `location: "SG"`).

#### **🔹 Node `Get Company Info` (httpRequest)**
- **Tham số quan trọng:**
  - **URL:** `https://api.ghostgenius.fr/v1/companies/{company_id}`
  - **Headers:** Cùng với `Search Companies`.
  - **Lưu ý:**
    - **Sử dụng `company_id` từ kết quả `Search Companies`**.
    - **Thêm delay 2s** giữa các request để tránh bị chặn API.

#### **🔹 Node `AI Company Scoring` (OpenAI)**
- **Tham số cần điền trong `Set Variables`:**
  ```json
  {
    "system_prompt": "You are an expert in evaluating company potential. Score companies from 1-10 based on:
    - Followers (200+ = 5 points)
    - Website presence (1 point)
    - Industry relevance (2 points)
    - Job postings (1 point)
    Return JSON: { 'score': X, 'reason': '...' }",
    "company_name": "{{ $node['Extract Company Data'].json['name'] }}",
    "followers": "{{ $node['Extract Company Data'].json['followers'] }}",
    "website": "{{ $node['Extract Company Data'].json['website'] }}"
  }
  ```
  - **Lưu ý:**
    - **Tùy chỉnh `system_prompt`** để phù hợp với ngành nghề của bạn.
    - **Đảm bảo `OpenAI API Key` được cấu hình đúng** trong credentials.

#### **🔹 Node `Check If Company Exists` (Google Sheets)**
- **Tham số cần thiết:**
  - **Sheet Name:** `Companies` (tên sheet trong Google Sheets mẫu).
  - **Query:** `SELECT * WHERE LinkedIn_ID = "{{ $json['linkedin_id'] }}"`
  - **Lưu ý:**
    - **Kiểm tra cột `LinkedIn_ID`** để tránh trùng lặp.

#### **🔹 Node `Add Company to CRM` (Google Sheets)**
- **Tham số cần thiết:**
  - **Range:** `Companies!A1` (để append dữ liệu mới).
  - **Headers:** `LinkedIn_ID, Name, Followers, Website, Score, Reason`
  - **Lưu ý:**
    - **Thêm delay 2s** trước khi append để tránh bị giới hạn API của Google Sheets.

---
### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chạy workflow với `Max Pages = 1` để kiểm tra kết quả.
   - Kiểm tra **Google Sheets** xem dữ liệu có được append đúng không.
2. **Bật Active** khi mọi thứ hoạt động ổn định.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
### **🔹 Tối Ưu Hóa AI Scoring**
- **Thử nghiệm với nhiều công ty** để điều chỉnh `system_prompt` phù hợp với ngành nghề.
- **Thêm tiêu chí mới** vào scoring (ví dụ: số lượng nhân viên, ngành nghề cụ thể).

### **🔹 Tích Hợp Slack/Telegram**
- **Sử dụng node `webhook`** để gửi thông báo khi có doanh nghiệp mới được thêm vào CRM.
- **Ví dụ:**
  ```json
  {
    "text": "🚀 New company added: {{ $json['name'] }} (Score: {{ $json['score'] }})",
    "url": "https://hooks.slack.com/services/..."
  }
  ```

### **🔹 Lưu Log & Báo Cáo Định Kỳ**
- **Sử dụng node `googleSheets`** để tạo sheet `Logs` lưu lịch sử hoạt động.
- **Tự động gửi báo cáo** hàng tuần bằng **node `email`** hoặc **Slack**.

### **🔹 Tăng Tốc Độ với Batch Processing**
- **Sử dụng `splitInBatches`** để xử lý nhiều công ty cùng lúc (nhưng vẫn giữ delay 2s để tránh bị chặn API).

---
## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho bộ phận Sales/Marketing bằng cách tự động hóa **tìm kiếm, đánh giá AI và lưu trữ CRM**. **Không cần code**, chỉ cần **cấu hình đúng các API key và biến**, bạn đã có một hệ thống **hoạt động 24/7**, **không sai sót**, và **tối ưu hóa outreach**.

**👉 Hãy thử ngay và tiết kiệm 10+ giờ/tháng!**
**👉 [Tải workflow từ n8n.io](https://n8n.io/workflows/3904) và import vào n8n của bạn.**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💬 Có thắc mắc? Hãy liên hệ với tác giả Matthieu qua [LinkedIn](https://www.linkedin.com/in/matthieu-belin83/)** để được hỗ trợ chi tiết!