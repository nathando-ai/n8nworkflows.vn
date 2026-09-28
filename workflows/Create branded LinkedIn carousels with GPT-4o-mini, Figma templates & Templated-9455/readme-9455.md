---
title: "🚀 Tự Động Hóa Tạo Bài Post LinkedIn Branding Sáng Tạo Với GPT-4o-mini, Figma & Templated - Không Cần Code!"
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp tạo bài post LinkedIn chuyên nghiệp, đa hình ảnh (carousel) với nội dung AI viết, thiết kế tự động từ template Figma, và đăng lên LinkedIn 24/7 - tiết kiệm 10+ giờ/tháng!"
slug: "tu-dong-hoa-tao-post-linkedin-branding-gpt-4o-mini"
tags: [n8n, automation, linkedin, ai-content, no-code, ai-marketing, gpt-4o-mini, figma, templated]
keywords: [tự động hóa linkedin, tạo post linkedin tự động, gpt-4o-mini linkedin, carousel linkedin ai, tự động hóa marketing ai, n8n workflow linkedin]
---

# 🚀 **Tự Động Hóa Tạo Bài Post LinkedIn Branding Sáng Tạo Với AI - Không Cần Code!**

### **Giải Pháp Cho Nỗi Đau Của Các Sếp Marketing**
Các sếp thường phải mất **giờ đồng hồ** để:
✅ Tìm kiếm ý tưởng post từ xu hướng thị trường (thời gian quý giá!)
✅ Viết nội dung chuyên nghiệp, cá nhân hóa cho brand
✅ Thiết kế carousel hấp dẫn với Figma (nếu không có designer)
✅ Đăng bài lên LinkedIn và theo dõi kết quả

**Workflow này tự động hóa toàn bộ quy trình trên - chỉ cần cung cấp input cơ bản!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng**: AI tự viết nội dung + thiết kế carousel
- **Nội dung chuyên nghiệp**: Sử dụng GPT-4o-mini + Perplexity để nghiên cứu xu hướng
- **Carousel hấp dẫn**: Tích hợp với [Templated](https://templated.cometai.eu/) để tạo thiết kế Figma tự động
- **Đăng bài tự động**: Hoạt động 24/7 với trigger hàng ngày
- **Theo dõi kết quả**: Nhận thông báo thành công/thất bại qua Telegram
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Các sếp cần chuẩn bị:
1. **API Keys**:
   - OpenAI API Key (để sử dụng GPT-4o-mini)
   - Perplexity API Key (nếu muốn nghiên cứu xu hướng)
   - LinkedIn OAuth2 API (để đăng bài)
   - Telegram Bot Token (để nhận thông báo)

2. **Tài Khoản**:
   - Tài khoản LinkedIn (để đăng bài)
   - Tài khoản Templated (để sử dụng template Figma)

3. **Cấu Hình N8n**:
   - Cài đặt các **credentials** trong n8n:
     - `openAiApi` (cho node `lmChatOpenAi`)
     - `perplexityApi` (cho node `perplexityTool`)
     - `linkedInOAuth2Api` (cho các node liên quan đến LinkedIn)
     - `telegramApi` (cho node `telegram`)
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/9455](https://n8n.io/workflows/9455) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ link trên và paste vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **24 node** với các bước chính sau:

##### **A. Khởi Động & Triggers**
- **Schedule Trigger**: Cài đặt để chạy hàng ngày (ví dụ: 8h sáng).
- **Switch**: Chọn logic xử lý dựa trên input (ví dụ: nếu có input từ Telegram).

##### **B. Tìm Kiếm Xu Hướng (Optional)**
- **Perplexity Tool**: Nếu cần, AI sẽ nghiên cứu xu hướng bằng Perplexity trước khi viết bài.

##### **C. Viết Nội Dung Post**
- **OpenAI Chat Model (GPT-4o-mini)**: Viết bài post chuyên nghiệp với prompt tự động.
- **Structured Output Parser**: Chuyển kết quả thành định dạng chuẩn.

##### **D. Tạo Carousel Tự Động**
- **MCP Client (Templated)**: Kết nối với [Templated](https://templated.cometai.eu/) để lấy template Figma.
- **Carousel Ideator (Agent)**: Tạo logic carousel từ template và nội dung AI viết.

##### **E. Chuyển Đổi & Đăng Bài**
- **Convert to Binary**: Chuyển nội dung thành file binary để upload.
- **LinkedIn HTTP Requests**: Upload carousel và đăng bài lên LinkedIn.

##### **F. Thông Báo Kết Quả**
- **Telegram**: Gửi thông báo thành công/thất bại qua Telegram.

---
#### **Cấu Hình Cần Thay Đổi**
1. **Node `Schedule Trigger`**:
   - Đặt thời gian chạy hàng ngày (ví dụ: `0 8 * * *` để chạy lúc 8h sáng).

2. **Node `OpenAI Chat Model`**:
   - Điền `openAiApi` vào credentials.
   - Cấu hình model: `gpt-4o-mini` (đã mặc định).

3. **Node `LinkedIn HTTP Requests`**:
   - Điền `linkedInOAuth2Api` vào credentials.
   - Cấu hình OAuth2 với scope: `r_liteprofile`, `r_emailaddress`, `w_member_social`.

4. **Node `Telegram`**:
   - Điền `telegramApi` vào credentials.
   - Cấu hình chat ID của Telegram Bot.

5. **Node `MCP Client` (Templated)**:
   - Điền `httpBearerAuth` (API Key của Templated).

---
#### **3. Kích Hoạt ⚡️**
- **Test Run**: Chạy thử với dữ liệu mẫu (ví dụ: input là "Tin tức mới về AI năm 2024").
- **Active Workflow**: Bật chế độ **Active** để workflow chạy tự động hàng ngày.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Slack/Email**:
   - Thay thế node Telegram bằng **Slack** hoặc **Email** để nhận thông báo.

2. **Lưu Log**:
   - Sử dụng node **Sticky Note** để ghi lại lịch sử post và kết quả.

3. **Báo Cáo Định Kỳ**:
   - Tạo workflow phụ để tổng hợp thống kê post thành công/thất bại.

4. **Cập Nhật Template**:
   - Kết nối với [Templated](https://templated.cometai.eu/) để cập nhật template mới.

5. **Tối Ưu Prompt**:
   - Cập nhật prompt cho GPT-4o-mini để phù hợp với brand của các sếp.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào chiến lược marketing cao cấp hơn. Với **AI viết nội dung + thiết kế tự động**, các sếp có thể:
✔ **Tăng tần suất post** (từ 1-2 bài/tuần lên hàng ngày)
✔ **Nâng cao chất lượng nội dung** (nhờ GPT-4o-mini)
✔ **Tiết kiệm chi phí** (không cần designer hoặc copywriter)

**Hãy import workflow này ngay và bắt đầu tự động hóa LinkedIn của mình!** 🚀

---
**Ghi chú cuối cùng**:
- Nếu gặp lỗi OAuth2 LinkedIn, hãy kiểm tra lại **scope** và **redirect URI**.
- Để tối ưu hiệu suất, các sếp nên chạy workflow trên **VPS** (không dùng phiên bản cloud n8n.io).