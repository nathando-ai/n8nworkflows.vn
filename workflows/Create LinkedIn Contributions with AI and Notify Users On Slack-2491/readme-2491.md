---
title: "🚀 Tự Động Hóa Bài Đăng LinkedIn Chuyên Nghiệp Với AI + Thông Báo Trên Slack (Không Cần Code)"
description: "Workflow tự động hóa tìm kiếm, phân tích bài viết LinkedIn chuyên sâu, tạo nội dung AI cá nhân hóa hàng tuần và thông báo ngay trên Slack. Giúp các chuyên gia marketing, tư vấn viên và doanh nhân tiết kiệm 10+ giờ/tháng viết bài thủ công."
slug: "tu-dong-hoa-bai-dang-linkedin-voi-ai"
tags: [n8n, automation, ai-marketing, linkedin-automation, slack-integration]
keywords: [n8n workflow linkedin, tự động hóa bài viết linkedin, ai viết bài linkedin, tự động hóa marketing, n8n ai]
---

# 🚀 **Tự Động Hóa Bài Đăng LinkedIn Chuyên Nghiệp Với AI + Thông Báo Trên Slack**

### **Giải pháp hoàn hảo cho những người muốn trở thành "Top Voice" trên LinkedIn mà không tốn thời gian viết bài thủ công**

---

### **🎯 Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng**: Workflow tự động tìm kiếm, phân tích và tạo nội dung bài viết LinkedIn hàng tuần.
- **Nội dung chuyên nghiệp, cá nhân hóa**: AI phân tích bài viết LinkedIn và tạo phản hồi/đóng góp độc đáo, phù hợp với lĩnh vực của bạn.
- **Hoạt động liên tục 24/7**: Bật workflow vào thứ Hai lúc 8h sáng, nội dung sẽ được tự động gửi lên Slack và lưu trữ trong cơ sở dữ liệu.
- **Dễ dàng theo dõi và quản lý**: Tất cả bài viết được lưu trong **NocoDB** (hoặc Airtable/Google Sheets) để bạn có thể quản lý và cập nhật dễ dàng.
- **Tăng cường sự hiện diện trên LinkedIn**: Bài viết được đăng định kỳ giúp bạn trở thành "Top Voice" trong lĩnh vực chuyên môn.
:::

---

### **🔧 Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản và API Keys**:
   - **OpenAI API Key** (để sử dụng AI tạo nội dung).
   - **Slack OAuth2 API** (để gửi thông báo bài viết).
   - **NocoDB API Token** (hoặc **Airtable API** hoặc **Google Sheets OAuth2 API**) để lưu trữ bài viết.
   - **Google Search URL** (để tìm kiếm bài viết LinkedIn chuyên sâu).

2. **Dữ liệu đầu vào**:
   - **Chủ đề chuyên môn** (ví dụ: "marketing automation", "kinh doanh B2B", "AI trong marketing").
   - **Slack Channel** để nhận thông báo bài viết mới.
   - **NocoDB/Google Sheets/Airtable** để lưu trữ bài viết.

3. **Hệ thống tự động hóa**:
   - **n8n Self-hosted** (để workflow chạy 24/7). 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - **NocoDB** (hoặc Airtable/Google Sheets) để lưu trữ bài viết.
:::

---

### **🚀 Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [n8n.io/workflows/2491](https://n8n.io/workflows/2491).
2. Trong **n8n Editor**, nhấn **Import** và chọn file JSON.
3. Hoặc copy toàn bộ JSON và paste vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Sau khi import, các sếp cần cấu hình các node quan trọng sau:

##### **🔹 Node 1: "Set Topic for Google search" (n8n-nodes-base.set)**
- **Cấu hình**:
  - Thêm **chủ đề chuyên môn** vào trường `topic` (ví dụ: `"marketing automation"`).
  - Ví dụ: `{"topic": "marketing automation"}`.

##### **🔹 Node 2: "HTTP Request to get LinkedIn advice articles" (n8n-nodes-base.httpRequest)**
- **Cấu hình**:
  - Thay đổi URL Google Search để phù hợp với chủ đề của bạn.
  - Ví dụ:
    ```plaintext
    https://www.google.com/search?q=site%3Alinkedin.com+advice+"marketing+automation"
    ```
  - Thêm **headers** để mô phỏng trình duyệt:
    ```json
    {
      "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36"
    }
    ```

##### **🔹 Node 3: "LinkedIn Contribution Writer" (n8n-nodes-langchain.openAi)**
- **Cấu hình**:
  - Chọn **OpenAI API Key** trong **Credentials**.
  - Cấu hình **Prompt** để AI tạo nội dung phù hợp với phong cách của bạn.
  - Ví dụ:
    ```plaintext
    "Tôi là chuyên gia marketing. Hãy viết một bài phản hồi chuyên sâu về bài viết LinkedIn này. Bài viết phải:
    1. Phân tích điểm mạnh/điểm yếu của bài viết.
    2. Đưa ra 3-5 ý tưởng thực tế để áp dụng.
    3. Kết thúc bằng một câu hỏi thảo luận để kích thích tương tác."
    ```

##### **🔹 Node 4: "Post new LinkedIn contributions to Slack channel" (n8n-nodes-base.slack)**
- **Cấu hình**:
  - Chọn **Slack OAuth2 API** trong **Credentials**.
  - Chọn **channel** muốn gửi thông báo (ví dụ: `#linkedin-posts`).
  - **Message Format**:
    ```json
    {
      "text": "📢 Bài viết LinkedIn mới được tạo tự động:\n\n🔹 **Tiêu đề**: {{ $node["HTML extract LinkedIn article"].json["title"] }}\n🔹 **Đường link**: {{ $node["HTTP Request to get LinkedIn advice articles"].json["url"] }}\n🔹 **Nội dung**: {{ $node["LinkedIn Contribution Writer"].json["response"] }}"
    }
    ```

##### **🔹 Node 5: "Post new LinkedIn contributions to NocoDB" (n8n-nodes-base.nocoDb)**
- **Cấu hình**:
  - Chọn **NocoDB API Token** trong **Credentials**.
  - Chọn **table** muốn lưu trữ bài viết (ví dụ: `linkedin_posts`).
  - **Data to Create**:
    ```json
    {
      "title": "{{ $node["HTML extract LinkedIn article"].json["title"] }}",
      "url": "{{ $node["HTTP Request to get LinkedIn advice articles"].json["url"] }}",
      "content": "{{ $node["LinkedIn Contribution Writer"].json["response"] }}",
      "created_at": "{{ $node["Schedule Trigger"].json["$dateTimeString"] }}"
    }
    ```

##### **🔹 Node 6: "Schedule Trigger Every Monday, @ 08:00am" (n8n-nodes-base.scheduleTrigger)**
- **Lưu ý**: Workflow đã được cấu hình chạy tự động hàng tuần vào **thứ Hai lúc 8h sáng**. Các sếp không cần chỉnh sửa nếu muốn giữ nguyên lịch trình.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Run Workflow** để kiểm tra workflow với dữ liệu mẫu.
   - Kiểm tra kết quả trên **Slack** và **NocoDB** để đảm bảo mọi thứ hoạt động đúng.

2. **Bật Active**:
   - Sau khi test thành công, chuyển **Status** từ **Inactive** sang **Active**.

---

### **✍️ Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết hợp với Telegram**:
   - Thêm node **Telegram Bot** để gửi thông báo bài viết mới qua Telegram cùng với Slack.

2. **Lưu log hoạt động**:
   - Sử dụng **Google Sheets** hoặc **Airtable** để lưu trữ log của workflow (ví dụ: thời gian chạy, bài viết đã xử lý).

3. **Tự động đăng bài lên LinkedIn**:
   - Sử dụng **n8n-nodes-base.httpRequest** kết hợp với API của **LinkedIn** (nếu có quyền API) để đăng bài tự động.

4. **Tối ưu hóa AI**:
   - Cập nhật **Prompt** trong node **OpenAI** để AI tạo nội dung phù hợp với phong cách cá nhân của bạn.

5. **Báo cáo định kỳ**:
   - Sử dụng **n8n-nodes-base.email** để gửi báo cáo tuần/month về số lượng bài viết đã tạo và thống kê tương tác.
:::

---

### **📌 Kết luận**
Workflow này là **giải pháp hoàn hảo** cho những người muốn trở thành **Top Voice trên LinkedIn** mà không tốn thời gian viết bài thủ công. Với sự hỗ trợ của **AI**, **n8n** và **Slack**, các sếp có thể tự động hóa toàn bộ quy trình từ tìm kiếm bài viết đến tạo nội dung và thông báo, giúp tiết kiệm thời gian và tăng cường sự hiện diện chuyên môn trên LinkedIn.

**🚀 Hãy áp dụng ngay và trở thành chuyên gia hàng đầu trong lĩnh vực của bạn!**

---
:::note[CHÚ Ý]
- Nếu muốn thay thế **NocoDB** bằng **Airtable** hoặc **Google Sheets**, chỉ cần thay đổi **Credentials** và cấu hình **table/worksheet** tương ứng.
- Để workflow chạy ổn định 24/7, các sếp nên **self-host n8n** trên VPS. 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) với mã giảm giá **VPSN8N**.
:::

---
**🔗 [Xem workflow gốc tại n8n.io](https://n8n.io/workflows/2491)** | **📌 [Tải file JSON](https://n8n.io/workflows/2491/download)**