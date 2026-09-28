---
title: "📊 Tự Động Hóa Báo Cáo Lượng Truy Cập Từ AI (LLM) Tuần Tế - Google Analytics + GPT-5 + Gmail"
description: "Tiết kiệm 10 giờ/tháng cho các sếp marketing bằng cách tự động hóa báo cáo tuần về lượng truy cập từ các công cụ AI như ChatGPT, Gemini, Perplexity... bằng Google Analytics, GPT-5 và Gmail. Kết quả: Dữ liệu chính xác, báo cáo cá nhân hóa, và quyết định marketing thông minh."
slug: "tieu-dong-hoa-bao-cao-llm-tuan-te"
tags: [n8n, automation, google-analytics, ai-llm, gpt-5, content-marketing, seo]
keywords: [n8n workflow tự động hóa báo cáo AI, tự động hóa Google Analytics, báo cáo lượng truy cập từ ChatGPT, tự động hóa marketing với GPT-5, tự động hóa báo cáo tuần]
---

# 🚀 **Tự Động Hóa Báo Cáo Lượng Truy Cập Từ AI (LLM) Tuần Tế - Google Analytics + GPT-5 + Gmail**

### **Nỗi Đau Của Các Sếp Marketing**
Các sếp marketing thường phải mất **10-15 giờ/tháng** để:
- **Truy xuất dữ liệu** từ Google Analytics về lượng truy cập từ các công cụ AI (ChatGPT, Gemini, Perplexity, Bard...).
- **Lọc và phân tích** dữ liệu thủ công để tìm ra xu hướng.
- **Viết báo cáo** bằng tay, mất thời gian và dễ sai sót.
- **Gửi báo cáo** qua email, không thể tự động hóa theo lịch.

**Kết quả?** Dữ liệu không kịp thời, báo cáo không cá nhân hóa, và quyết định marketing không dựa trên số liệu chính xác.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** bằng việc tự động hóa toàn bộ quy trình.
- **Dữ liệu chính xác 100%** từ Google Analytics, không sai sót như thủ công.
- **Báo cáo cá nhân hóa** với nội dung HTML đẹp mắt, được sinh ra bởi GPT-5.
- **Hoạt động liên tục** 24/7, không phụ thuộc vào thời gian làm việc.
- **Quản lý marketing thông minh** với dữ liệu về lượng truy cập từ AI, giúp tối ưu hóa nội dung và chiến dịch.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Analytics** (đã cài đặt và có **Property ID**).
2. **API Key OpenAI** (để sử dụng GPT-5).
3. **Tài khoản Gmail** (đã kích hoạt OAuth 2.0 cho Gmail).
4. **Thời gian** để cấu hình các node (khoảng 30 phút).
:::

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ [link gốc](https://n8n.io/workflows/9081) hoặc tải file JSON và import vào **n8n Editor**:
```bash
# Cách import từ file JSON:
1. Mở n8n Editor (trên máy chủ self-hosted hoặc n8n.cloud).
2. Nhấn **Import** ở góc trên bên phải.
3. Chọn file JSON đã tải xuống và nhấn **Import**.
```

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
##### **🔹 Node 1: Schedule Trigger (Khởi động tuần)**
- **Cấu hình:** Chọn **"Every week"** và thiết lập ngày/thời gian chạy (ví dụ: **Thứ 2 hàng tuần, 8h sáng**).
- **Lưu ý:** Đảm bảo **Active** để workflow chạy tự động.

##### **🔹 Node 2: Get Sessions by Source & Medium (Google Analytics)**
- **Cấu hình:**
  - Nhập **Google Analytics Property ID** (tìm ở `Admin Panel -> Property -> Property Details`).
  - Chọn **Views** (nếu có nhiều view, chọn view chính).
  - Thiết lập **Date Range** để lấy dữ liệu của **tuần trước** (sử dụng hàm `{{ $now.subtract(1, 'week').toISOString() }}`).
- **Lưu ý:**
  - Đảm bảo **credentials** `googleAnalyticsOAuth2` được cấu hình đúng.
  - Nếu không có dữ liệu, kiểm tra lại **Property ID** và quyền truy cập.

##### **🔹 Node 3: Filter Known Referral Domains from AI (Code Node)**
- **Cấu hình:**
  - Mở **Code Node** và chỉnh sửa danh sách **LLM domains** để phù hợp với các công cụ AI đang theo dõi (ví dụ: `chat.openai.com`, `perplexity.ai`, `gemini.google.com`).
  - **Mẫu code tham khảo:**
    ```javascript
    // Filter traffic from known LLM domains
    return $input.all().map(item => {
      const isLLM = item.referralDomain.includes('chat.openai.com') ||
                    item.referralDomain.includes('perplexity.ai') ||
                    item.referralDomain.includes('gemini.google.com');
      return isLLM ? item : null;
    }).filter(item => item !== null);
    ```
- **Lưu ý:**
  - Nếu muốn thêm/loại bỏ domain, chỉnh sửa phần `item.referralDomain.includes()`.

##### **🔹 Node 4: Combine Items (Aggregate)**
- **Cấu hình:**
  - Chọn **Aggregate by** là `referralDomain` để nhóm dữ liệu theo nguồn truy cập.
  - **Lưu ý:** Không cần chỉnh sửa gì nếu muốn giữ mặc định.

##### **🔹 Node 5: Create Traffic Report (OpenAI)**
- **Cấu hình:**
  - Nhập **OpenAI API Key** vào `openAiApi` (credentials).
  - **Prompt mẫu** (có thể chỉnh sửa để phù hợp):
    ```plaintext
    Tóm tắt báo cáo lượng truy cập từ các công cụ AI (LLM) trong tuần qua:
    - Dữ liệu: {{ $json["items"].map(item => `- ${item.referralDomain}: ${item.sessions} phiên`).join("\n") }}
    - Yêu cầu:
      1. Tóm tắt số liệu một cách ngắn gọn (dưới 200 từ).
      2. Đưa ra 2-3 nhận xét về xu hướng.
      3. Sử dụng HTML để định dạng báo cáo (đầu tiêu đề, danh sách, màu sắc).
      4. Thêm một khuyến nghị marketing cho tuần tới.
    ```
- **Lưu ý:**
  - Đảm bảo **model** chọn là `gpt-4` hoặc `gpt-5` (nếu có).
  - Nếu báo cáo không đẹp, thử chỉnh sửa **prompt** để rõ ràng hơn.

##### **🔹 Node 6: Send Report (Gmail)**
- **Cấu hình:**
  - Nhập **email nhận** (của chính mình hoặc team).
  - **Tiêu đề email** có thể là: **"Báo Cáo Lượng Truy Cập Từ AI (Tuần {{ $now.subtract(1, 'week').format('YYYY-MM-DD') })"**.
  - **Nội dung email** sẽ tự động lấy từ **OpenAI response**.
- **Lưu ý:**
  - Đảm bảo **credentials** `gmailOAuth2` được cấu hình (cài đặt OAuth 2.0 trong Google Cloud Console).
  - Kiểm tra **quyền gửi email** trong Gmail (có thể cần kích hoạt **Less Secure Apps** nếu dùng Gmail cá nhân).

---
#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Run Workflow** để kiểm tra từng node.
   - Kiểm tra **Gmail** xem báo cáo có được gửi không.
2. **Bật Active Workflow**:
   - Sau khi test thành công, chuyển **Active** sang **ON**.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[TIẾP CẬN HƠN]
1. **Thêm Slack/Telegram Notification**:
   - Sử dụng **Slack Node** hoặc **Telegram Bot Node** để thông báo khi báo cáo được gửi.
   - **Cách làm:**
     ```javascript
     // Thêm vào node Gmail sau khi gửi email
     const message = `Báo cáo LLM tuần ${$now.subtract(1, 'week').format('YYYY-MM-DD')} đã được gửi!`;
     return { text: message };
     ```
2. **Lưu Log vào Google Sheets**:
   - Sử dụng **Google Sheets Node** để ghi dữ liệu vào bảng tính để theo dõi dài hạn.
3. **Tự Động Gửi Báo Cáo cho Nhóm**:
   - Thay vì chỉ gửi cho 1 email, sử dụng **Code Node** để chia sẻ với nhiều người:
     ```javascript
     const emails = ["team1@example.com", "team2@example.com"];
     return emails.map(email => ({ email }));
     ```
4. **Cập Nhật Danh Sách LLM Động**:
   - Sử dụng **Webhook** để cập nhật danh sách domain LLM mới mà không cần chỉnh sửa code.
:::

---
### **📌 Kết Luận**
Workflow này giúp các sếp **tự động hóa hoàn toàn** quá trình báo cáo lượng truy cập từ AI, tiết kiệm thời gian và cải thiện chất lượng quyết định marketing. **Chỉ cần 30 phút cấu hình**, các sếp sẽ nhận được báo cáo tuần tự động, chính xác và cá nhân hóa mỗi thứ Hai sáng.

**🚀 Hãy áp dụng ngay và bắt đầu tối ưu hóa marketing của mình!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::