---
title: "🤖 **Pre-Meeting Lead Research Agent: Tự Động Hoàn Thành Nghiên Cứu Khách Hàng Trước Cuộc Hẹn (Calendly + Perplexity + AI)**"
description: "Workflow tự động hóa nghiên cứu chi tiết về công ty, cá nhân và tín hiệu thị trường cho các cuộc họp sắp tới, tiết kiệm 30-45 phút/lần, giúp sales team chuẩn bị chuyên nghiệp hơn. Sử dụng Calendly, Perplexity AI, OpenAI và LinkedIn API để tự động thu thập thông tin từ LinkedIn, tin tức và hoạt động kinh doanh."
slug: "pre-meeting-lead-research-agent"
tags: [n8n, automation, ai-agent, recruiting, sales-automation, calendly, perplexity, openai, linkedin-api]
keywords: [n8n workflow tự động hóa nghiên cứu khách hàng, tự động hóa sales, AI agent cho cuộc họp, nghiên cứu công ty và cá nhân, Calendly + Perplexity + AI, tiết kiệm thời gian cho sales]
---

# 🚀 **Tự Động Hoàn Thành Nghiên Cứu Khách Hàng Trước Cuộc Hẹn Với AI Agent**

### **Giải Pháp Cho Nỗi Đau Của Sales Team**
Các sếp trong lĩnh vực **sales, BDR, hoặc account management** thường phải mất **30-45 phút** để nghiên cứu khách hàng trước mỗi cuộc họp. Thông tin từ LinkedIn, tin tức công ty, và hoạt động kinh doanh thường phân tán trên nhiều nền tảng, khiến quá trình này trở nên **tốn thời gian, thiếu chính xác và khó cập nhật**. Workflow này **tự động hóa toàn bộ quá trình** bằng cách kết hợp **Calendly, Perplexity AI, OpenAI, và LinkedIn API** để cung cấp **báo cáo nghiên cứu chi tiết** ngay trước khi cuộc họp diễn ra.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên cài đặt n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất tối ưu.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (Hỗ trợ 24/7)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động nghiên cứu khách hàng trong **vài giây** thay vì mất **30-45 phút** thủ công.
- **Thông tin chính xác và cập nhật**: Dữ liệu từ **LinkedIn, tin tức, và hoạt động kinh doanh** được tổng hợp tự động.
- **Cá nhân hóa cuộc họp**: Báo cáo nghiên cứu chi tiết về **công ty, cá nhân, và tín hiệu thị trường** giúp sales team chuẩn bị **chuyên nghiệp và hiệu quả**.
- **Hoạt động liên tục**: Workflow chạy **24/7** và tự động gửi kết quả đến Slack khi có cuộc họp mới.
- **Tự động phát hiện tín hiệu quan trọng**: Nhận biết **tín hiệu tuyển dụng, tăng trưởng, hoặc rủi ro** từ hoạt động của khách hàng.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
#### **1. API Keys & Credentials**
| **Dịch vụ**       | **API Key/Credential**       | **Mô tả**                                                                 |
|-------------------|-----------------------------|-----------------------------------------------------------------------------|
| **Calendly**      | API Key                     | Để nhận thông báo khi có cuộc họp mới được đặt lịch.                   |
| **OpenAI**        | API Key (`openAiApi`)        | Dùng cho **orchestration** và **nghiên cứu bằng AI** (gpt-4o, gpt-4o-mini). |
| **Perplexity**    | API Key (`perplexityApi`)    | Dùng để **tìm kiếm thông tin công ty và cá nhân** trên web.               |
| **RapidAPI**      | API Key (`httpHeaderAuth`)   | Dùng để **truy cập LinkedIn API** (profile, posts, comments, reactions).   |
| **Slack**         | Webhook URL (`slackApi`)     | Để gửi báo cáo nghiên cứu tự động vào kênh Slack.                       |

#### **2. Thông Tin Khách Hàng**
- **LinkedIn URL** của khách hàng (nên **cập nhật trong form Calendly** để workflow tự động lấy dữ liệu).
- **Tên công ty** (nếu không có, workflow sẽ tự động tìm kiếm thông tin từ LinkedIn).

#### **3. Cấu Hình Slack**
- **Kênh/Người dùng Slack** để nhận báo cáo (cần **cập nhật trong node cuối cùng**).
---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/8957](https://n8n.io/workflows/8957) hoặc **copy/paste JSON** vào **n8n Editor**.
- **Cách import**:
  1. Mở **n8n Editor** trên trang web hoặc máy chủ self-hosted.
  2. Nhấn **Import** và chọn file JSON.
  3. Hoặc **paste JSON** vào ô **Import Workflow** và nhấn **Import**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **19 node** và được chia thành **4 AI Agent** riêng biệt. Dưới đây là **các bước cấu hình quan trọng**:

##### **A. Cấu Hình Calendly Trigger**
- **Node**: `Calendly Trigger`
- **Cần thiết**:
  - **Kết nối Calendly API** với `calendlyApi` (đã cấu hình trong credentials).
  - **Chọn form Calendly** phù hợp (nên có trường **LinkedIn URL** để workflow tự động lấy dữ liệu).
  - **Test trigger** bằng cách đặt một cuộc họp mẫu và kiểm tra liệu workflow có nhận được dữ liệu không.

##### **B. Cấu Hình AI Agents**
Workflow sử dụng **4 AI Agent** để nghiên cứu:
1. **Company Research Agent** (nghiên cứu công ty)
2. **Person Research Agent** (nghiên cứu cá nhân)
3. **Signal Research Agent** (phát hiện tín hiệu thị trường)
4. **Main Agent** (orchestrate tất cả và tạo báo cáo cuối cùng)

- **Cần thiết**:
  - **Cập nhật `openAiApi`** trong tất cả các node `lmChatOpenAi` (đã có sẵn trong credentials).
  - **Chọn model OpenAI** phù hợp (workflow sử dụng `gpt-4o-mini` và `gpt-4o`).
  - **Không cần chỉnh sửa prompt** (nếu muốn tùy chỉnh, có thể cập nhật trong node `Structured Output Parser`).

##### **C. Cấu Hình Perplexity & LinkedIn API**
- **Node**: `Perplexity Research`, `Research a person`, `Enrich LinkedIn Profile`, `Get LinkedIn Posts`, `Get LinkedIn comments`, `Get LinkedIn Reactions`
- **Cần thiết**:
  - **Kết nối `perplexityApi`** và `httpHeaderAuth` (API Key RapidAPI cho LinkedIn).
  - **Kiểm tra quyền truy cập LinkedIn API**:
    - Nếu sử dụng **RapidAPI**, đảm bảo API key có quyền truy cập đầy đủ.
    - Nếu gặp lỗi, có thể **cập nhật header** trong node `httpRequestTool` (ví dụ: `Authorization: Bearer <API_KEY>`).

##### **D. Cấu Hình Slack Output**
- **Node**: `Send a message`
- **Cần thiết**:
  - **Chọn kênh/người dùng Slack** trong `slackApi`.
  - **Cập nhật message format** (nếu muốn thay đổi định dạng báo cáo).
  - **Test gửi tin nhắn** bằng cách chạy workflow với dữ liệu mẫu.

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Đặt một cuộc họp mẫu trên Calendly.
   - Chạy workflow và kiểm tra **Slack** để xem báo cáo có được tạo không.
2. **Bật Active**:
   - Sau khi test thành công, **bật workflow** để nó hoạt động tự động khi có cuộc họp mới.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tùy Chỉnh Prompt cho AI Agent**
   - Nếu muốn **cập nhật cách nghiên cứu**, có thể chỉnh sửa **prompt** trong node `Structured Output Parser` hoặc trong các node `agentTool`.
   - Ví dụ: Thêm yêu cầu **phân tích cạnh tranh** hoặc **tín hiệu tuyển dụng chi tiết**.

2. **Kết Nối Với Dịch Vụ Khác**
   - **Gửi báo cáo qua Email**: Thêm node `n8n-nodes-base.email` để gửi báo cáo tự động qua email.
   - **Lưu log vào Google Sheets/Notion**: Sử dụng node `n8n-nodes-base.googleSheets` để lưu lịch sử nghiên cứu.
   - **Tích hợp với CRM (HubSpot, Salesforce)**: Sử dụng node `n8n-nodes-base.hubspot` để cập nhật thông tin khách hàng vào CRM.

3. **Optimize Performance**
   - **Sử dụng cache** cho OpenAI API (workflow đã sử dụng `cachedResultName` để tối ưu).
   - **Limiter request** cho LinkedIn API để tránh bị chặn (nếu sử dụng RapidAPI, kiểm tra hạn mức request).

4. **Phân Tích Tín Hiệu Thị Trường**
   - **Cập nhật node `Signal Research Agent`** để phát hiện **tín hiệu mới** như:
     - **Tuyển dụng mới** (công ty tuyển dụng nhiều nhân viên).
     - **Tăng trưởng doanh thu** (quảng cáo mới, sản phẩm mới).
     - **Rủi ro** (tin tức tiêu cực, thay đổi lãnh đạo).

---

### 📌 **Kết Luận**
Workflow **Pre-Meeting Lead Research Agent** là **giải pháp hoàn hảo** cho các sales team muốn **tiết kiệm thời gian, nghiên cứu khách hàng chi tiết và chuẩn bị cuộc họp chuyên nghiệp**. Với **tự động hóa hoàn toàn** từ **Calendly đến Slack**, các sếp không cần lo lắng về việc **quá trình nghiên cứu thủ công** nữa.

**Hành động ngay hôm nay**:
1. **Cài đặt n8n trên VPS** (nếu chưa có).
2. **Import workflow** và **cấu hình API keys**.
3. **Test với cuộc họp mẫu** và **bật workflow** để tự động hóa nghiên cứu khách hàng!

👉 **[Tải workflow ngay từ n8n.io](https://n8n.io/workflows/8957)** và bắt đầu **tự động hóa sales team** của mình! 🚀