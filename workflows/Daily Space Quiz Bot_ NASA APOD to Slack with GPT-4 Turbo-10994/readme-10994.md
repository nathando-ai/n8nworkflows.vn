---
title: "🚀 **Tự Động Hóa Bot Trắc Nghiệm Hàng Ngày Về Không Gian: Từ NASA APOD Đến Slack Với GPT-4 Turbo**"
description: "Workflow tự động hóa tạo ra trắc nghiệm hàng ngày về không gian dựa trên hình ảnh NASA APOD, gửi đến Slack với GPT-4 Turbo, và tính điểm tự động. Giúp các sếp tiết kiệm thời gian tổ chức hoạt động nội bộ, tăng sự tham gia và tương tác trong đội nhóm."
slug: "daily-space-quiz-bot-nasa-apod-slack-gpt-4-turbo"
tags: [n8n, automation, no-code, content-creation, ai-multimodal, slack, openai, nasa]
keywords: [n8n workflow tự động hóa, bot trắc nghiệm không gian, NASA APOD Slack, GPT-4 Turbo tự động, tự động hóa nội bộ doanh nghiệp, tự động hóa Slack]
---

# 🚀 **Bot Trắc Nghiệm Hàng Ngày Về Không Gian: Từ NASA APOD Đến Slack Với GPT-4 Turbo**

### **Tại sao các sếp cần một bot trắc nghiệm không gian tự động?**
Hàng ngày, các sếp và đội nhóm phải tổ chức các hoạt động nội bộ như trắc nghiệm, trò chơi hoặc hoạt động tăng cường tinh thần. Tuy nhiên, **làm thủ công** lại tốn thời gian, dễ bị lỗi và không thể cá nhân hóa. Với **Daily Space Quiz Bot**, các sếp có thể:
- **Tự động hóa** việc tạo ra trắc nghiệm hàng ngày về không gian dựa trên hình ảnh NASA APOD.
- **Gửi trắc nghiệm** đến Slack với GPT-4 Turbo, đảm bảo nội dung hấp dẫn và đa dạng.
- **Tính điểm tự động** và công bố kết quả, tiết kiệm thời gian và giảm thiểu sai sót.
- **Tăng sự tham gia** của đội nhóm thông qua hệ thống phản hồi và phản ứng trên Slack.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tạo ra trắc nghiệm thủ công hàng ngày.
- **Nội dung đa dạng**: Sử dụng hình ảnh và thông tin từ NASA để tạo ra trắc nghiệm mới mẻ.
- **Tính điểm chính xác**: Hệ thống tự động tính điểm và công bố kết quả.
- **Tăng tương tác**: Hệ thống phản ứng trên Slack giúp đội nhóm tham gia dễ dàng.
- **Hoạt động liên tục**: Workflow chạy tự động hàng ngày vào thời gian đã thiết lập.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
- **API Key NASA**: Để lấy hình ảnh và thông tin về NASA APOD.
- **API Key OpenAI (GPT-4 Turbo)**: Để tạo ra trắc nghiệm thông qua AI.
- **Credentials Slack**: Token Slack để gửi tin nhắn và quản lý phản ứng.
- **Slack Channel ID**: ID của kênh Slack nơi bot sẽ gửi trắc nghiệm.
- **Thời gian chạy**: Workflow được thiết lập chạy hàng ngày vào 21:00 (thời gian có thể điều chỉnh).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n Editor](https://n8n.io/editor).
2. Nhấp vào **Import Workflow** và chọn file JSON đã tải xuống từ [link gốc](https://n8n.io/workflows/10994).
   *Hoặc* copy toàn bộ JSON và dán vào **Import Workflow** trong Editor.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **a. Cấu hình Workflow Configuration**
- **Node: Workflow Configuration**
  - Thiết lập **Slack Channel ID** (để bot gửi trắc nghiệm vào kênh này).
  - Chỉnh **độ khó** của trắc nghiệm (ví dụ: "dễ", "trung bình", "khó").
  - Thiết lập các biến khác như **tên kênh**, **tên bot**, hoặc **thời gian chờ phản hồi**.

##### **b. Cấu hình NASA Node**
- **Node: Get APOD**
  - Đảm bảo đã thêm **API Key NASA** vào **Credentials** của node này.
  - Node sẽ tự động lấy hình ảnh và thông tin về NASA APOD hàng ngày.

##### **c. Cấu hình OpenAI Node**
- **Node: OpenAI: Create Quiz**
  - Thêm **API Key OpenAI** vào **Credentials** của node này.
  - Prompt mặc định đã được thiết kế để tạo ra trắc nghiệm đa lựa chọn từ dữ liệu NASA. Các sếp có thể tùy chỉnh prompt để thay đổi phong cách hoặc độ khó.

##### **d. Cấu hình Slack Node**
- **Node: Slack: Post Quiz**
  - Chọn **Credentials Slack** đã thiết lập trước đó.
  - Đảm bảo **Slack Channel ID** trong **Workflow Configuration** khớp với kênh thực tế.
- **Node: Slack: Get Reactions**
  - Sử dụng cùng **Credentials Slack** như trên.
- **Node: Slack: Add Reaction 1-4**
  - Các node này sẽ thêm **phản ứng (reactions)** 1️⃣, 2️⃣, 3️⃣, 4️⃣ vào tin nhắn trắc nghiệm để người dùng phản hồi.

##### **e. Cấu hình Code Node**
- **Node: Code: Tally Correct Answers**
  - Node này tính điểm dựa trên phản ứng của người dùng. Các sếp **không cần chỉnh sửa mã** nếu đã import workflow chính xác, nhưng có thể mở rộng logic nếu cần.

##### **f. Thiết lập Schedule Trigger**
- **Node: Schedule: Daily at 21:00**
  - Đảm bảo thời gian chạy đã được thiết lập đúng (ví dụ: 21:00 hàng ngày).
  - Các sếp có thể điều chỉnh thời gian này trong **Settings** của node.

#### **3. Kích hoạt ⚡️**
1. **Test Run**: Nhấp vào **Run Workflow** để kiểm tra nếu tất cả node hoạt động như mong đợi.
2. **Active Workflow**: Sau khi kiểm tra thành công, bật **Active** để workflow chạy tự động hàng ngày.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tùy chỉnh Prompt OpenAI**:
   - Mở rộng prompt để tạo ra các loại trắc nghiệm khác nhau (ví dụ: trắc nghiệm hình ảnh, trắc nghiệm lý thuyết, hoặc trắc nghiệm kết hợp).
   - Thay đổi ngôn ngữ hoặc phong cách để phù hợp với văn hóa doanh nghiệp.

2. **Lưu Log & Báo Cáo**:
   - Thêm node **Google Sheets** hoặc **Database** để lưu lịch sử trắc nghiệm và kết quả.
   - Sử dụng node **Email** để gửi báo cáo kết quả hàng tuần cho quản lý.

3. **Kết hợp với Telegram**:
   - Thêm node **Telegram** để gửi trắc nghiệm đến nhóm Telegram cùng lúc với Slack.

4. **Thêm Hình Ảnh & GIF**:
   - Sử dụng node **Image Processing** để thêm hình ảnh hoặc GIF từ NASA vào tin nhắn Slack để làm trắc nghiệm hấp dẫn hơn.

5. **Phân Tích Kết Quả**:
   - Sử dụng node **Analytics** để phân tích độ tham gia và hiệu suất của trắc nghiệm.

---

### 📌 **Kết luận**
**Daily Space Quiz Bot** là giải pháp hoàn hảo để tự động hóa việc tổ chức trắc nghiệm hàng ngày trong doanh nghiệp, giúp tiết kiệm thời gian, tăng tương tác và mang lại trải nghiệm thú vị cho đội nhóm. Với workflow này, các sếp có thể **chỉ cần import, cấu hình và kích hoạt** mà không cần viết một dòng code nào!

**Hãy áp dụng ngay và làm cho đội nhóm của mình hứng thú hơn với không gian vũ trụ mỗi ngày!** 🚀🌌