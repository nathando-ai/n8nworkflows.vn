---
title: "🤖 **Tự Động Hóa Tìm Việc Làm Xa Xôi Của Các Sếp Với AI + Slack (Không Cần Code!)**"
description: "Workflow này tự động tìm kiếm, phân tích và gửi danh sách việc làm xa xôi phù hợp với hồ sơ của các sếp hàng tuần qua Slack. Giúp tiết kiệm thời gian lên tới 15h/tháng và tăng cơ hội nhận được offer phù hợp."
slug: "tieu-dong-hoa-tim-viec-lam-xa-xoi-voi-ai-slack"
tags: [n8n, automation, no-code, ai-summarization, remote-jobs, browseract, openrouter, slack-integration]
keywords: [n8n workflow tìm việc xa xôi, tự động hóa tuyển dụng AI, scrap job board, gửi tin nhắn Slack tự động, OpenRouter GPT-4, BrowserAct n8n]
---

# 🚀 **Tự Động Hóa Tìm Việc Làm Xa Xôi Của Các Sếp Với AI + Slack (Không Cần Code!)**

## 🔍 **Nỗi Đau Của Các Sếp Khi Tìm Việc Làm Xa Xôi**
Các sếp thường phải:
- **Tốn thời gian** tra cứu hàng chục trang web tuyển dụng (Indeed, Dice, LinkedIn...) hàng tuần.
- **Khó lọc được việc phù hợp** với kỹ năng, mức lương mong muốn và vị trí xa xôi.
- **Bị bỏ qua** vì hồ sơ không được tối ưu hóa cho AI của các công ty tuyển dụng.
- **Không nhận được thông báo kịp thời** khi có offer mới phù hợp.

Workflow này **giải quyết tất cả** bằng cách tự động:
✅ **Scrape** tất cả việc làm xa xôi từ các trang web uy tín.
✅ **Phân tích AI** so sánh với hồ sơ của các sếp và đánh giá mức độ phù hợp.
✅ **Gửi tin nhắn Slack** hàng tuần với danh sách việc làm được lọc sàng kỹ lưỡng.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
- **Tiết kiệm 15h/tháng** so với cách tìm kiếm thủ công.
- **Nhận việc phù hợp 100%** với kỹ năng, mức lương và mong muốn xa xôi.
- **Cập nhật liên tục** hàng tuần mà không cần can thiệp.
- **Tối ưu hóa hồ sơ** thông qua phân tích AI từ OpenRouter (GPT-4).
- **Giao tiếp hiệu quả** với Slack (hoặc Telegram) để không bỏ lỡ offer.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**Chuẩn Bị Trước Khi Bắt Đầu**]
Các sếp cần chuẩn bị:
1. **Tài khoản BrowserAct** (để scrape job board):
   - [Đăng ký miễn phí BrowserAct](https://www.browseract.com/) (sử dụng template **"Job Board Aggregator"**).
   - **API Key** và **Workflow ID** từ BrowserAct (hướng dẫn [tại đây](https://docs.browseract.com)).
2. **Tài khoản OpenRouter** (để sử dụng mô hình AI GPT-4):
   - [Đăng ký OpenRouter](https://openrouter.ai/) và lấy **API Key**.
3. **Tài khoản Slack** (để nhận tin nhắn tự động):
   - [Tạo Bot Slack](https://api.slack.com/apps) và lấy **Token OAuth**.
4. **Hồ sơ cá nhân** (để AI so sánh):
   - Kỹ năng, kinh nghiệm, mức lương mong muốn, và vị trí xa xôi ưa thích.
5. **Danh sách trang web tuyển dụng** (ví dụ: Indeed, Dice, LinkedIn, RemoteOK).
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
#### **Cách 1: Từ File JSON**
1. **Tải workflow** từ [n8n.io](https://n8n.io/workflows/13382) (ấn nút **"Export"**).
2. **Mở n8n Editor** (trên máy hoặc VPS).
3. **Nhấn "Import"** và chọn file JSON vừa tải.
4. **Chọn "Create new workflow"** và đặt tên (ví dụ: **"AI Job Hunter"**).

#### **Cách 2: Copy/Paste JSON**
1. **Mở n8n Editor** và tạo workflow mới.
2. **Nhấn "Import"** → **"From JSON"** → **Dán mã JSON** từ [n8n.io/workflows/13382](https://n8n.io/workflows/13382).
3. **Lưu workflow** với tên phù hợp.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **10 node chính**, nhưng **3 node quan trọng nhất** cần cấu hình kỹ lưỡng:

#### **🔹 Node 1: "Add a Resume" (n8n-nodes-base.set)**
- **Mục đích**: Định nghĩa hồ sơ của các sếp (kỹ năng, mức lương, vị trí ưa thích).
- **Cách cấu hình**:
  - Nhấn **double-click** vào node này.
  - **Thêm các key-value** như:
    ```json
    {
      "location": "Remote (Asia-Pacific)",
      "skills": ["Python", "n8n", "AI", "Automation"],
      "salary_min": 1000,
      "salary_max": 2000,
      "job_types": ["Full-time", "Contract"]
    }
    ```
  - **Lưu ý**: Các giá trị này sẽ được AI so sánh với việc làm scrape được.

#### **🔹 Node 2: "Scrape Suitable Jobs" (browserAct)**
- **Mục đích**: Scrape việc làm từ các trang web tuyển dụng theo danh sách URL đã định nghĩa.
- **Cách cấu hình**:
  1. **Điền API Key** của BrowserAct (từ tài khoản đã đăng ký).
  2. **Chọn Template**: **"Job Board Aggregator"** (đã được tác giả chuẩn bị).
  3. **Cấu hình `Target_Sites`** (danh sách URL scrape):
     ```json
     {
       "Target_Sites": [
         "https://www.dice.com/jobs?q=remote&radius=100",
         "https://www.indeed.com/l/remote-jobs.html",
         "https://remoteok.com/remote-jobs"
       ]
     }
     ```
  4. **Kiểm tra "Test Run"** để đảm bảo scrape thành công.

#### **🔹 Node 3: "Analyze the jobs and generate a Slack message" (agent)**
- **Mục đích**: AI phân tích việc làm và tạo tin nhắn Slack với danh sách phù hợp.
- **Cách cấu hình**:
  - **Không cần chỉnh sửa** (AI đã được cấu hình sẵn để so sánh với hồ sơ từ Node 1).
  - **Lưu ý**:
    - Nếu muốn **tùy chỉnh prompt**, các sếp có thể mở node này và chỉnh sửa trong **`agentParameters`**.
    - Ví dụ: Thêm yêu cầu về **"mức độ ưu tiên"** (High/Medium/Low) cho mỗi việc làm.

#### **🔹 Node 4: "Send a message to the Slack channel" (slack)**
- **Mục đích**: Gửi tin nhắn Slack hàng tuần với kết quả phân tích.
- **Cách cấu hình**:
  1. **Chọn credentials**: Chọn **`slackApi`** (đã cấu hình trước khi import).
  2. **Chọn channel**: Nhập tên channel Slack (ví dụ: `#remote-jobs`).
  3. **Kiểm tra "Test Run"** để đảm bảo tin nhắn được gửi đúng.

---
### **3. Kích Hoạt ⚡️ Workflow**
1. **Bật "Active"** trên workflow.
2. **Chọn "Run"** để test với dữ liệu mẫu (nếu cần).
3. **Cấu hình "Weekly Trigger"** (Node 4):
   - Nhấn **double-click** vào node này.
   - Chọn **"Every Sunday at 8 AM"** (hoặc thời gian phù hợp).
   - **Lưu** và **bật Active**.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[**Cách Tối Ưu Hóa Workflow**]
1. **Thêm Logs cho Dễ Theo Dõi**:
   - Sử dụng node **`stickyNote`** để ghi lại lỗi hoặc kết quả scrape.
   - Ví dụ: Ghi ngày scrape và số lượng việc làm được tìm thấy.

2. **Kết Nối Với Telegram**:
   - Thay vì Slack, các sếp có thể sử dụng node **`telegram`** để nhận tin nhắn.
   - Hướng dẫn: [n8n Telegram Node](https://docs.n8n.io/integrations/n8n-nodes-base/telegram/).

3. **Lưu Kết Quả Vào Google Sheets/Notion**:
   - Sử dụng node **`googleSheets`** hoặc **`notion`** để lưu danh sách việc làm lâu dài.
   - Cách cấu hình: [n8n Google Sheets](https://docs.n8n.io/integrations/n8n-nodes-base/googleSheets/).

4. **Tăng Cường AI với Prompt Tùy Chỉnh**:
   - Nếu muốn AI **phân tích chi tiết hơn**, các sếp có thể chỉnh sửa **prompt** trong node **`lmChatOpenRouter`**.
   - Ví dụ: Yêu cầu AI **so sánh mức lương** giữa các việc làm và đề xuất mức lương phù hợp.

5. **Báo Cáo Định Kỳ**:
   - Sử dụng node **`email`** để gửi báo cáo hàng tháng cho bản thân hoặc team.
   - Hướng dẫn: [n8n Email Node](https://docs.n8n.io/integrations/n8n-nodes-base/email/).
:::

---

## 📌 **Kết Luận: Bắt Đầu Tự Động Hóa Hôm Nay!**
Workflow này **giải phóng thời gian** của các sếp để tập trung vào công việc quan trọng hơn, trong khi AI và tự động hóa làm việc 24/7 để tìm kiếm việc làm xa xôi phù hợp.

:::success[**Hành Động Ngay Bây Giờ**]
1. **Đăng ký VPS** để chạy n8n 24/7 (không bị giới hạn free tier):
   - 👉 [VPS TinoHost (Mã giảm: **VPSN8N**)](https://tino.vn/vps-n8n?affid=388) (giảm tới 39%).
   - 👉 [VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
2. **Import workflow** và cấu hình theo hướng dẫn trên.
3. **Bật Active** và chờ AI làm việc cho các sếp!
:::

**Các sếp đã sẵn sàng để AI tìm việc cho mình chưa?** 🚀