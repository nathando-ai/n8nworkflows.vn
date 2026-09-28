---
title: "🚀 Tự Động Hóa Sáng Tạo Danh Sách 100 Tiềm Năng (Prospects) Với AI Perplexity & Google Sheets - Không Cần Code"
description: "Workflow tự động hóa hoàn toàn giúp các sếp doanh nghiệp tự động sinh ra danh sách 100 tiềm năng (prospects) chất lượng cao thông qua AI nghiên cứu sâu (Perplexity) và lưu trữ tự động vào Google Sheets. Giúp tiết kiệm thời gian lên đến 80% so với cách làm thủ công."
slug: "tieu-dong-hoa-sang-tao-danh-sach-100-tiem-nang-ai-perplexity"
tags: [n8n, automation, ai-chatbot, google-sheets, perplexity-ai, no-code, sales-automation]
keywords: [n8n workflow prospecting, tự động hóa sinh danh sách tiềm năng, ai nghiên cứu sâu, google sheets tự động, perplexity ai n8n, tự động hóa bán hàng]
---

# 🚀 **Tự Động Hóa Sáng Tạo Danh Sách 100 Tiềm Năng (Prospects) Với AI Perplexity & Google Sheets**

### **Nỗi Đau Của Các Sếp: Tìm Tiềm Năng (Prospecting) Làm Thủ Công Làm Giảm Hiệu Quả**
Các sếp bán hàng, marketing hay team sales thường phải mất **giờ đồng hồ** để:
- Tìm kiếm thông tin chi tiết về khách hàng tiềm năng (tên, công ty, ngành nghề, liên lạc...).
- Lọc và cập nhật danh sách prospect thủ công vào Google Sheets.
- Đảm bảo dữ liệu chính xác và cập nhật liên tục.

**Kết quả?** Thời gian và năng suất bị "chôn vùi" trong công việc lặp đi lặp lại, trong khi AI có thể làm tất cả trong **vài phút**.

---
## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên đến 80%** so với cách làm thủ công.
- **Danh sách prospect chất lượng cao**: AI Perplexity nghiên cứu sâu để cung cấp thông tin chính xác, chi tiết và cá nhân hóa.
- **Cập nhật tự động**: Dữ liệu được lưu vào Google Sheets ngay lập tức, không cần can thiệp.
- **Hoạt động 24/7**: Workflow chạy liên tục, không phụ thuộc vào giờ làm việc của team.
- **Tích hợp Slack**: Nhận thông báo và tương tác với AI qua Slack, không cần mở n8n Editor.
:::

---
## 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản n8n Self-hosted** (để workflow hoạt động 24/7).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

2. **Tài khoản Google Sheets** và một **bảng tính trống** (không chứa tên nào).
   - **Template tham khảo**: [Google Sheets Template](https://docs.google.com/spreadsheets/d/1WWRwi3bseuZd1ebaAdGQYzDhwW_zBEOYib20l2Z_coY/edit?usp=sharing) (sao chép và sử dụng).

3. **API Keys và Credentials**:
   - **Perplexity API Key**: [Đăng ký tại Perplexity Developer Portal](https://www.perplexity.ai/api).
   - **Google Sheets OAuth 2.0**: Cấu hình trong n8n dưới `Credentials > Google Sheets OAuth2 API`.
   - **Slack API Token** (nếu muốn tích hợp Slack Trigger).

4. **Node LangChain** (n8n-nodes-langchain) để sử dụng AI Agent và OpenRouter.
   - Cài đặt từ [n8n Community Nodes](https://community.n8n.io/node/n8n-nodes-langchain).

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/8466](https://n8n.io/workflows/8466) (chọn "Download JSON").
2. Trên n8n Editor, nhấn **Import** và chọn file JSON vừa tải.
3. Chọn **Create new workflow** và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở n8n Editor và tạo workflow mới.
2. Nhấn **Import** > **Paste JSON** và dán nội dung JSON từ [n8n.io/workflows/8466](https://n8n.io/workflows/8466) (chọn "Copy JSON").
3. Chọn **Create new workflow** và nhấn **Import**.

---
### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
#### **A. Cấu Hình Credentials**
| **Node**               | **Credentials Cần Thiết**               | **Hướng Dẫn Cấu Hình**                                                                 |
|------------------------|----------------------------------------|-----------------------------------------------------------------------------------------|
| **Perplexity**         | `perplexityApi`                        | Điền `API Key` từ Perplexity vào `Credentials > Perplexity API`.                         |
| **Google Sheets**      | `googleSheetsOAuth2Api`               | Cấu hình OAuth 2.0 trong `Credentials > Google Sheets OAuth2 API`.                      |
| **OpenRouter Chat**    | `openRouterApi`                        | Điền `API Key` từ OpenRouter vào `Credentials > OpenRouter API`.                        |
| **Slack Trigger**      | Slack Workspace & Token                | Cấu hình trong `Credentials > Slack` (nếu muốn sử dụng Slack Trigger).                  |

#### **B. Cấu Hình Node Quan Trọng**
1. **Node "User Chat Message"**:
   - Đổi biến `n8n.chat.message` thành **Slack message** (theo hướng dẫn trong canvas: *"Change the variable in 'User Chat Message' from the n8n chat -> slack message"*).
   - Ví dụ: Nếu Slack message là `{{ $json.slack.message }}`, hãy cập nhật trong node `User Chat Message`.

2. **Node "Collect More Info" và "All Done!"**:
   - Đảm bảo **content** của message được kết nối từ output của **AI Agent** (`@n8n/n8n-nodes-langchain.agent`).

3. **Node "Check First Row" và "Check Last Row"**:
   - Chọn **Sheet Name** và **Range** trong Google Sheets (ví dụ: `Sheet1!A1:Z1000`).
   - Node này sẽ kiểm tra xem bảng có dữ liệu chưa để quyết định tiếp tục nghiên cứu hay dừng.

4. **Node "Research via Perplexity"**:
   - Đặt `model` thành `sonar-deep-research` (đã cấu hình sẵn trong workflow).
   - Nếu muốn thay đổi model, cập nhật trong `keyParameters`.

5. **Node "Insert Data Into Sheet"**:
   - Chọn **Sheet Name** và **Range** để dữ liệu được append/update.
   - Đảm bảo `operation` là `appendOrUpdate`.

---
### **3. Kích Hoạt ⚡️**
1. **Test Run với Dữ liệu Mẫu**:
   - Nhấn **Run Workflow** và gửi một **Slack message** hoặc chat với AI Agent (ví dụ: *"Tìm 5 tiềm năng trong ngành công nghệ AI ở Việt Nam"*).
   - Kiểm tra kết quả trong Google Sheets và Slack.

2. **Bật Active Workflow**:
   - Sau khi test thành công, chuyển trạng thái workflow từ **Inactive** sang **Active**.
   - Để workflow hoạt động liên tục, **không cần restart** (n8n self-hosted sẽ tự động chạy).

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Tích Hợp Slack Cho Trải Nghiệm Tốt Hơn**
- Sử dụng **Slack Trigger** để nhận tin nhắn từ team và tự động xử lý.
- Cấu hình **Slack Bot** để gửi thông báo kết quả nghiên cứu qua Slack.

### **2. Lưu Log & Báo Cáo Định Kỳ**
- Sử dụng **n8n-nodes-base.stickyNote** để lưu lịch sử chat và kết quả nghiên cứu.
- Tích hợp **Google Sheets** để tạo báo cáo định kỳ (ví dụ: hàng tuần).

### **3. Tối Ưu Hóa AI Agent**
- Cập nhật **prompt** trong node `Collect More Info` để AI trả về thông tin chi tiết hơn.
- Ví dụ:
  ```json
  {
    "prompt": "Tìm kiếm và tổng hợp thông tin chi tiết về {{ $json.userInput }} bao gồm: tên, công ty, vị trí, email, số điện thoại, và mô tả công việc. Đảm bảo dữ liệu chính xác và cập nhật."
  }
  ```

### **4. Sử Dụng Perplexity Tier Cao**
- Nếu muốn **tốc độ nhanh hơn**, nâng cấp lên **Perplexity Pro** (tốc độ nghiên cứu ~3-4 phút cho 10 tiềm năng → ~1-2 phút).

---
## 📌 **Kết Luận: Áp Dụng Ngay Để Tiết Kiệm Thời Gian & Tăng Doanh Thu!**
Workflow này **giải phóng thời gian** của các sếp để tập trung vào **strategy và closing deal**, trong khi AI và tự động hóa làm tất cả công việc lặp đi lặp lại.

**Bắt đầu ngay:**
1. **Cài đặt n8n trên VPS** (để workflow hoạt động 24/7).
2. **Import workflow** và cấu hình credentials.
3. **Test với một danh sách nhỏ** (ví dụ: 5 tiềm năng) và xem kết quả.
4. **Bật Active** và để AI làm việc cho bạn!

👉 **Xem video hướng dẫn chi tiết**: [SETUP TUTORIAL LOOM](https://www.loom.com/share/2a71542149054456b993826f56e5503f?sid=41a106b3-a16d-4686-8280-b7e56af8ce42)

---
**Chia sẻ ý kiến hoặc gặp vấn đề?** Đăng câu hỏi trên [Community n8n](https://community.n8n.io/) hoặc comment bên dưới! 🚀