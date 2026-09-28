---
title: "🚀 Tự Động Hóa Báo Cáo Tin AI Hàng Ngày Với Perplexity Pro + GPT-4.1-mini & Gmail (Không Code)"
description: "Workflow tự động hóa gửi báo cáo tin tức AI mới nhất trong 24h qua (đầu bài, tóm tắt 1 câu, nguồn + link) vào email cá nhân hoặc nhóm hàng ngày, với định dạng chuyên nghiệp do AI xử lý. Giúp các sếp tiết kiệm 3-5 tiếng/tháng theo dõi xu hướng AI."
slug: "tieu-dong-hoa-bao-cao-tin-ai-hang-ngay"
tags: [n8n, automation, ai-summarization, market-research, no-code]
keywords: [n8n workflow tự động hóa, báo cáo tin tức AI hàng ngày, Perplexity Pro + GPT-4.1-mini, tự động hóa email, market research AI]
---

# 🚀 **Tự Động Hóa Báo Cáo Tin AI Hàng Ngày: Từ Perplexity Pro → GPT-4.1-mini → Email (Không Code)**

### **Nỗi Đau Của Các Sếp**
Hàng ngày, các sếp phải mất **30-60 phút** để:
- Tìm kiếm tin tức AI mới nhất trên Google, Twitter, hoặc các nguồn tin chuyên ngành.
- Lọc bỏ tin cũ, tin không liên quan, và tổng hợp thông tin rải rác.
- Viết tóm tắt, định dạng email, và gửi cho team.
- Lo lắng bỏ sót tin quan trọng vì không theo dõi liên tục.

**Workflow này giải quyết tất cả!** Dùng AI tự động:
✅ **Tìm kiếm** tin tức AI mới nhất trong 24h qua (đầu bài, tóm tắt 1 câu, nguồn + link).
✅ **Tổng hợp** và định dạng thành email chuyên nghiệp.
✅ **Gửi tự động** vào email cá nhân hoặc nhóm **mỗi ngày lúc 9h sáng**.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng** (Self-hosted) để tránh giới hạn của phiên bản Cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 3-5 tiếng/tháng** theo dõi tin tức AI.
- **Định dạng chuyên nghiệp** với AI (không cần viết email thủ công).
- **Tin tức mới nhất** trong 24h qua, được lọc và tóm tắt bởi AI.
- **Gửi tự động** vào email cá nhân hoặc nhóm (không quên, không bỏ sót).
- **Cập nhật liên tục** (không phụ thuộc vào người dùng).
- **Dễ dàng mở rộng** (thêm Slack, Notion, hoặc thay đổi chủ đề tin tức).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Perplexity Pro** (để sử dụng API `sonar-pro`).
   - [Đăng ký Perplexity Pro](https://www.perplexity.ai/) (miễn phí 7 ngày, sau đó ~$20/tháng).
2. **API Key OpenAI** (để sử dụng GPT-4.1-mini trong định dạng email).
   - [Tạo API Key OpenAI](https://platform.openai.com/account/api-keys).
3. **Tài khoản Gmail** (để gửi email tự động).
   - Cần **OAuth2 credentials** trong n8n (hướng dẫn sau).
4. **n8n Self-hosted** (không dùng phiên bản Cloud để tránh giới hạn).

---
:::note[LƯU Ý QUAN TRỌNG]
- **Perplexity Pro** là **bắt buộc** vì workflow dùng model `sonar-pro` để tìm kiếm tin tức AI chính xác.
- **GPT-4.1-mini** được sử dụng để định dạng email (rẻ hơn GPT-4 nhưng hiệu quả).
- **Gmail OAuth2** phải được cấu hình trong n8n để gửi email tự động.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:

**Cách 1: Từ file JSON**
1. Tải workflow từ [n8n.io/workflows/5469](https://n8n.io/workflows/5469) (chọn "Export").
2. Mở **n8n Editor** (trang chủ của n8n).
3. Nhấn **"Import"** và chọn file JSON vừa tải.

**Cách 2: Copy/Paste JSON**
1. Copy toàn bộ JSON từ [n8n.io/workflows/5469](https://n8n.io/workflows/5469) (chọn "Export").
2. Trong n8n Editor, nhấn **"Import"** → **"Paste JSON"**.

---
#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Sau khi import, các sếp **phải cấu hình** các node sau:

##### **🔹 Node 1: Schedule Trigger (Đặt lịch chạy)**
- **Thời gian chạy**: Đặt **9h sáng** (hoặc thời gian phù hợp).
- **Zone giờ**: Chọn **Việt Nam (UTC+7)** hoặc khu vực phù hợp.

##### **🔹 Node 2: Perplexity Research Agent (Tìm kiếm tin tức AI)**
- **API Key**: Điền **Perplexity API Key** (từ tài khoản Perplexity Pro).
- **Model**: Đã mặc định là `sonar-pro` (không cần thay đổi).
- **Query**: Workflow tự động tìm kiếm tin tức AI mới nhất trong 24h qua (không cần chỉnh).

##### **🔹 Node 3: Simple Memory (Bộ nhớ AI - Tùy Chọn)**
- **Cài đặt mặc định**: Để nguyên (nếu muốn lưu lịch sử định dạng email).
- **Nếu không cần**: Có thể **xóa node này** để tiết kiệm tài nguyên.

##### **🔹 Node 4: OpenAI Chat Model (Định dạng email với GPT-4.1-mini)**
- **API Key**: Điền **OpenAI API Key** (từ tài khoản OpenAI).
- **Model**: Đã mặc định là `gpt-4.1-mini` (rẻ hơn GPT-4).
- **Prompt**: Workflow tự động sử dụng template định dạng email (không cần chỉnh).

##### **🔹 Node 5: Gmail (Gửi email tự động)**
- **Credentials**: Chọn **gmailOAuth2** (phải cấu hình trước).
  - **Cách cấu hình OAuth2**:
    1. Trong n8n, nhấn **"Add"** → **"Gmail"** → **"Add"** (OAuth2).
    2. Đăng nhập tài khoản Gmail và **cho phép quyền**.
    3. Chọn **email nhận** (cá nhân hoặc nhóm).
- **Tiêu đề email**: Đã mặc định là **"AI News Digest - [Ngày]"**.
- **Nội dung email**: Workflow tự động lấy từ AI (không cần chỉnh).

---
#### **3. Kích Hoạt ⚡️**
1. **Test Run** (kiểm tra trước khi chạy thực):
   - Nhấn **"Run Workflow"** và kiểm tra email có nhận được không.
   - Nếu có lỗi, kiểm tra lại **API Key** và **credentials Gmail**.
2. **Bật Active**:
   - Sau khi test thành công, nhấn **"Active"** để workflow chạy tự động hàng ngày.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁCH MỞ RỘNG THÊM]
1. **Thay đổi chủ đề tin tức**:
   - Thay `Perplexity Query` từ `"AI news"` thành `"Climate Tech news"` hoặc `"Crypto News"`.
2. **Gửi đến Slack/Telegram**:
   - Thay node **Gmail** bằng **Slack Webhook** hoặc **Telegram Bot**.
3. **Lưu log vào Google Sheets/Notion**:
   - Thêm node **Google Sheets** hoặc **Notion** để lưu lịch sử tin tức.
4. **Thêm AI Commentary**:
   - Sử dụng **LangChain Agent** để AI viết bình luận ngắn về tin tức.
5. **Báo cáo định kỳ**:
   - Thay đổi **Schedule Trigger** để gửi **tối hôm trước** thay vì sáng.
:::

---
### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **strategy** và **quản lý team** thay vì theo dõi tin tức AI thủ công. Với **AI tự động hóa**, các sếp sẽ:
✔ **Nhận tin tức mới nhất** trong 24h qua (đầu bài, tóm tắt, nguồn + link).
✔ **Email được định dạng chuyên nghiệp** bởi GPT-4.1-mini.
✔ **Không quên gửi** vì workflow chạy tự động hàng ngày.

**Hành động ngay!**
1. **Cài n8n Self-hosted** (nếu chưa có).
2. **Import workflow** và cấu hình API Key.
3. **Test Run** và **bật Active** để nhận báo cáo AI hàng ngày!

🔗 **Xem video hướng dẫn chi tiết**: [Tutorial của Automate With Marc](https://youtu.be/O-DLvaMVLso)

---
**Chia sẻ workflow này với team để cùng tự động hóa công việc!** 🚀