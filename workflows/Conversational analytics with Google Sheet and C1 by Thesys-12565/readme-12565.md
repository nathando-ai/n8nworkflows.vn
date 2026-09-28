---
title: "🤖 **Tự Động Hóa Phân Tích Dữ Liệu Chat Powered by Google Sheet & AI C1 (Thesys) – Không Cần Code!**"
description: "Chuyển Google Sheet của bạn thành **dashboard tương tác AI**, trả lời câu hỏi bằng tiếng Việt thông thường và nhận **báo cáo, biểu đồ, bảng thống kê** tự động. Giảm thời gian phân tích từ giờ xuống phút, không cần pivot table hay thủ công."
slug: "tieu-dong-hoa-phan-tich-du-lieu-google-sheet-ai-c1"
tags: [n8n, automation, no-code, ai-chatbot, google-sheets, thesys, market-research]
keywords: [tự động hóa n8n, phân tích dữ liệu google sheet, ai chatbot, dashboard tương tác, c1 by thesys, market research tự động]
---

# **🚀 Tự Động Hóa Phân Tích Dữ Liệu Google Sheet Bằng AI Chat – Không Cần Code!**

### **🔥 Nỗi Đau Của Các Sếp Hiện Nay**
Hàng ngày, các sếp phải:
- **Lọc, sắp xếp dữ liệu** trên Google Sheet thủ công để tìm ra thông tin quan trọng.
- **Tạo pivot table** để so sánh chiến dịch marketing, theo dõi leads, hoặc phân tích doanh số.
- **Mất thời gian** để vẽ biểu đồ, so sánh dữ liệu giữa các thời điểm.
- **Không thể tương tác** với dữ liệu như người dùng chatbot – chỉ có thể nhìn thẳng vào bảng số liệu khô khan.

**Giải pháp?** **Workflow này** giúp bạn:
✅ **Nhập câu hỏi bằng tiếng Việt thông thường** (ví dụ: *"Cho tôi biết doanh số bán hàng tháng 12 của khu vực Bắc Bộ là bao nhiêu?"*).
✅ **Nhận kết quả dưới dạng:**
   - **Bảng thống kê tự động** (không cần pivot table).
   - **Biểu đồ tương tác** (so sánh, phân tích xu hướng).
   - **Báo cáo văn bản chi tiết** (AI tổng hợp và phân tích).
✅ **Hoạt động 24/7** – Không cần can thiệp thủ công.

---
## **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[**3 Lợi Ích Cốt Lõi**]
- **Tiết kiệm thời gian lên đến 80%** so với phân tích thủ công.
- **Chính xác 100%** – AI không mắc lỗi tính toán như con người.
- **Tương tác linh hoạt** – Đặt câu hỏi theo cách tự nhiên, nhận kết quả dưới nhiều định dạng.
- **Hoạt động liên tục** – Dữ liệu Google Sheet tự cập nhật, AI phân tích ngay khi có thay đổi.
:::

---
## **🔧 Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
### **1. Tài Khoản & API Keys**
| **Dịch Vụ**          | **Thao Tác Cần Thực Hiện**                                                                 | **Liên Kết**                                                                 |
|----------------------|--------------------------------------------------------------------------------------------|------------------------------------------------------------------------------|
| **Thesys API Key**   | - Đăng ký tài khoản trên [Thesys Console](https://console.thesys.dev/keys).               | [Tạo API Key](https://console.thesys.dev/keys)                             |
|                      | - Copy API Key và lưu an toàn (sẽ dùng trong n8n).                                         |                                                                              |
| **Google Sheets**    | - Chuẩn bị 1 Google Sheet chứa dữ liệu (ví dụ: leads, doanh số, chiến dịch marketing).     | [Tạo Google Sheet mới](https://sheets.google.com)                          |
|                      | - **Cấu trúc dữ liệu:** Cột đầu tiên là tiêu đề (ví dụ: `date`, `campaign_name`, `leads`). |                                                                              |
| **n8n Self-Hosted**  | - Cài đặt n8n trên VPS để workflow hoạt động 24/7.                                         | 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm **VPSN8N**) |

---
## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow từ File JSON**
:::info[**Bước 1: Tải Workflow**]
- Tải file JSON của workflow từ [n8n.io/workflows/12565](https://n8n.io/workflows/12565).
- **Cách import:**
  1. Mở **n8n Editor**.
  2. Nhấn **Import Workflow** (icon `📥`).
  3. Chọn file JSON vừa tải và nhấn **Import**.
:::

### **2. Cấu Hình Cần Thực Hiện (BẮT BUỘC)**
Workflow gồm **5 node chính**, các sếp phải cấu hình như sau:

#### **🔹 Node 1: "When chat message received" (chatTrigger)**
- **Chức năng:** Nhận câu hỏi từ người dùng qua UI tương tác.
- **Lưu ý:**
  - **Không cần cấu hình thêm** – node này tự động kết nối với UI của Thesys.

#### **🔹 Node 2: "C1 Chat Model" (lmChatOpenAi)**
- **Chức năng:** Sử dụng mô hình AI **C1 by Thesys** (giống GPT-5) để phân tích dữ liệu.
- **Cấu hình:**
  1. **Thêm Credential:**
     - Nhấn **Create New** trong phần **Credentials**.
     - Nhập **API Key** từ Thesys (đã copy ở trên).
     - **Base URL:** `https://api.thesys.dev/v1/embed`.
     - **Tên Credential:** `openAiApi` (giữ nguyên).
  2. **Chọn Model:**
     - Trong **keyParameters > model**, chọn:
       ```json
       "c1/openai/gpt-5/v-20250930"
       ```
     - **Lưu ý:** Nếu model không có, liên hệ [support@thesys.dev](mailto:support@thesys.dev).

#### **🔹 Node 3: "Fetch data from Google Sheet" (googleSheetsTool)**
- **Chức năng:** Lấy dữ liệu từ Google Sheet để AI phân tích.
- **Cấu hình:**
  1. **Thêm Credential OAuth2:**
     - Nhấn **Create New** trong phần **Credentials**.
     - Chọn **Google Sheets OAuth2 API**.
     - Đăng nhập Google và cấp quyền truy cập.
     - **Tên Credential:** `googleSheetsOAuth2Api` (giữ nguyên).
  2. **Cấu hình Node:**
     - **Sheet Name:** Nhập tên tệp Google Sheet của bạn (ví dụ: `DoanhSoBanHang`).
     - **Range:** Nhập `Sheet1!A1:Z1000` (hoặc điều chỉnh theo số dòng dữ liệu).
     - **Lưu ý:** Đảm bảo dữ liệu trong Sheet **không có ô trống** và **không hợp nhất ô**.

#### **🔹 Node 4: "Simple Memory" (memoryBufferWindow)**
- **Chức năng:** Lưu trữ lịch sử đối thoại để AI hiểu ngữ cảnh.
- **Không cần cấu hình** – node này tự động hoạt động.

#### **🔹 Node 5: "UI Agent" (agent)**
- **Chức năng:** Tạo UI tương tác từ kết quả phân tích.
- **Không cần cấu hình** – node này kết nối với **Thesys GenUI SDK** để hiển thị kết quả.

---
### **3. Kích Hoạt Workflow**
1. **Test Run (Kiểm Tra Trước Khi Bật):**
   - Nhấn **Run Workflow** và nhập câu hỏi mẫu:
     - *"Cho tôi biết doanh số bán hàng tháng 12 của khu vực Bắc Bộ là bao nhiêu?"*
   - Kiểm tra kết quả có hợp lý không.
2. **Bật Workflow:**
   - Nhấn **Active** ở góc trên bên phải.
   - **Xác nhận** workflow đã hoạt động.

---
## **🌟 Mẹo & Gợi Ý Nâng Cao**
### **1. Kết Nối với Slack/Telegram**
- Sử dụng **node Slack Webhook** hoặc **Telegram Bot** để nhận kết quả phân tích qua chat.
- **Cách làm:**
  1. Thêm **node Slack Webhook** sau node `UI Agent`.
  2. Cấu hình **Webhook URL** từ Slack (Settings > Custom Integrations).
  3. AI sẽ gửi kết quả phân tích trực tiếp vào Slack.

### **2. Lưu Log Phân Tích**
- Thêm **node StickyNote** để ghi lại lịch sử câu hỏi và kết quả.
- **Cách làm:**
  1. Thêm node `n8n-nodes-base.stickyNote`.
  2. Chọn **Create New** và lưu vào **Google Drive** hoặc **Notion**.

### **3. Gửi Báo Cáo Định Kỳ**
- Sử dụng **node Email** (Gmail/SMTP) để gửi báo cáo tự động hàng tuần.
- **Cách làm:**
  1. Thêm **node Email** sau node `UI Agent`.
  2. Cấu hình **SMTP** (ví dụ: Gmail) và địa chỉ email nhận.
  3. Đặt **cron job** (n8n Pro) để chạy hàng tuần.

### **4. Tối Ưu Hóa Dữ Liệu**
- **Lọc dữ liệu trước khi phân tích:**
  - Thêm **node Set** để lọc chỉ dữ liệu mới nhất (ví dụ: `date > "2024-01-01"`).
- **Tăng tốc độ:**
  - Nếu Google Sheet lớn, sử dụng **node Google Sheets API** thay vì `googleSheetsTool`.

---
## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc phân tích dữ liệu thủ công, đồng thời **tăng cường hiệu quả** với AI C1 by Thesys. **Không cần code**, chỉ cần:
1. Chuẩn bị **Google Sheet** và **API Key Thesys**.
2. **Import workflow** và cấu hình 3 node quan trọng.
3. **Bật workflow** và bắt đầu tương tác với dữ liệu bằng tiếng Việt!

**🚀 Hành động ngay:**
- [Tải workflow](https://n8n.io/workflows/12565) và bắt đầu tự động hóa phân tích dữ liệu!
- **Cần hỗ trợ?** Giới thiệu với [Thesys Community](https://discord.com/invite/Pbv5PsqUSv) hoặc email `support@thesys.dev`.

---
**💡 Lưu ý cuối cùng:**
- Nếu gặp lỗi **API Key không hợp lệ**, kiểm tra lại trên [Thesys Console](https://console.thesys.dev/keys).
- Đối với **dữ liệu nhạy cảm**, đảm bảo Google Sheet được **đặt quyền riêng tư** và không chia sẻ với người ngoài.