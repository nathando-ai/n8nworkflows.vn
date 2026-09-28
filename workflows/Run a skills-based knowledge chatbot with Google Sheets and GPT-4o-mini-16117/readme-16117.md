---
title: "🤖 Chatbot Trí Tuệ Nhân Tạo Căn Bản Học Vấn - Google Sheets + GPT-4o-mini (Không Cần Code)"
description: "Tạo chatbot AI cá nhân hóa hoàn toàn dựa trên Google Sheets, cho phép các sếp tự định nghĩa các 'kỹ năng' cụ thể mà AI sẽ thực hiện theo yêu cầu - không cần thay đổi code nào. Hỗ trợ nhớ lịch sử hội thoại và phản hồi chính xác theo các quy tắc đã thiết lập."
slug: "chatbot-trie-tuong-nhan-tao-can-ban-hoc-van-google-sheets-gpt-4o-mini"
tags: [n8n, automation, ai-chatbot, google-sheets, no-code, openai, gpt-4o-mini, session-memory]
keywords: [n8n workflow chatbot, tự động hóa chatbot AI, google sheets skills, gpt-4o-mini n8n, chatbot không cần code, lưu trữ kỹ năng AI, nhớ lịch sử hội thoại]
---

# 🚀 Chatbot Trí Tuệ Nhân Tạo Căn Bản Học Vấn - Google Sheets + GPT-4o-mini

## 🔍 Giải quyết vấn đề gì?
Các sếp đang gặp khó khăn khi muốn tạo một chatbot AI cá nhân hóa để hỗ trợ công việc hàng ngày, nhưng lại phải đối mặt với những hạn chế sau:
- **Không thể tự định nghĩa hành vi AI** một cách dễ dàng (phải code hoặc sử dụng các template cứng nhắc).
- **AI phản hồi không chính xác** vì dựa vào kiến thức chung thay vì các quy tắc cụ thể của doanh nghiệp.
- **Không nhớ lịch sử hội thoại** giữa các lần tương tác.
- **Cần kiến thức kỹ thuật** để cập nhật hoặc thay đổi hành vi của AI.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tạo chatbot AI hoàn toàn dựa trên Google Sheets** - mọi người trong team đều có thể chỉnh sửa.
✅ **Định nghĩa các "kỹ năng" cụ thể** cho AI thực hiện (ví dụ: viết bài SEO, tổng kết văn bản, viết email lạnh).
✅ **AI phản hồi chính xác theo các quy tắc đã thiết lập** thay vì dựa vào kiến thức chung.
✅ **Giữ nhớ lịch sử hội thoại** trong mỗi phiên chat.
✅ **Không cần code** - chỉ cần chỉnh sửa Google Sheets là AI đã hoạt động mới.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động 24/7 với hiệu suất tối ưu, các sếp nên cài đặt n8n trên một VPS riêng (Self-hosted). Điều này đảm bảo:
- **Tính bảo mật cao** (không phụ thuộc vào nền tảng cloud công cộng).
- **Tốc độ phản hồi nhanh** (không bị giới hạn bởi API rate limit của n8n.cloud).
- **Dễ dàng mở rộng** (thêm các node hoặc dịch vụ khác).

👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) với mã giảm giá **VPSN8N** (giảm tới 39%).
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo ổn định cho AI).
:::

---

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần viết code hoặc quản lý các hệ thống phức tạp.
- **Chính xác 100%**: AI phản hồi theo các quy tắc đã định nghĩa trong Google Sheets, không bị lệch lạc.
- **Cá nhân hóa cao**: Mỗi kỹ năng (skill) đều có thể điều chỉnh riêng biệt (ví dụ: viết email lạnh, tổng kết báo cáo, viết bài SEO).
- **Hoạt động liên tục**: Workflow chạy 24/7 trên VPS, không phụ thuộc vào thời gian làm việc của team.
- **Dễ dàng cập nhật**: Chỉ cần chỉnh sửa Google Sheets là AI đã tự động áp dụng thay đổi mới.
- **Nhớ lịch sử**: AI nhớ được các thông tin trong phiên chat trước (ví dụ: tên khách hàng, yêu cầu cụ thể).
:::

---

### 🔧 Yêu cầu cần thiết
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để kết nối với Google Sheets).
2. **API Key OpenAI** (để sử dụng GPT-4o-mini).
3. **Google Sheet** với cấu trúc cụ thể (chi tiết ở phần sau).
4. **VPS** (để self-host n8n, khuyến nghị sử dụng TinoHost hoặc BNIX).

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Workflow này có **7 nodes** và được thiết kế để hoạt động trên **n8n Self-hosted**. Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/16117](https://n8n.io/workflows/16117) và import vào n8n Editor.
- **Copy/paste JSON** từ file vào n8n Editor (đảm bảo đã chọn tab "Import/Export" trong Editor).

:::note[Lưu ý quan trọng]
Workflow này **không hoạt động trên n8n.cloud** vì cần các node LangChain và OpenAI API Key. Các sếp phải **self-host** để sử dụng đầy đủ tính năng.
:::

---

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

##### **A. Cấu hình Google Sheets**
1. **Tạo Google Sheet mới** với **1 tab** có tên **"Skills"**.
2. **Cấu trúc cột** phải chính xác như sau (đảm bảo không có khoảng trắng hoặc ký tự đặc biệt):
   | **Skill Name**       | **Trigger Phrases**               | **Instructions**                          | **Example Output**                     | **Active** |
   |----------------------|------------------------------------|-------------------------------------------|----------------------------------------|------------|
   | Ví dụ: Write SEO Blog | write blog, SEO article, blog post | Write an 800-word SEO blog post...       | (Nếu có)                               | Yes/No     |

3. **Dữ liệu mẫu**:
   - **Skill Name**: *Tổng kết báo cáo*
     **Trigger Phrases**: *summarize report, tldr report, short report*
     **Instructions**: *Tóm tắt báo cáo trong 3-5 điểm chính, mỗi điểm dưới 15 từ.*
     **Active**: *Yes*

   - **Skill Name**: *Viết email lạnh*
     **Trigger Phrases**: *cold email, outreach email, sales email*
     **Instructions**: *Viết email 3 đoạn: đoạn mở đầu cá nhân hóa, đoạn giới thiệu giá trị, đoạn gọi hành động rõ ràng.*
     **Active**: *Yes*

4. **Trong node "2. Google Sheets — Load Active Skills"**:
   - Kết nối **Google Sheets OAuth2 credential** (tạo mới trong n8n).
   - Điền **ID của Sheet** vào trường `YOUR_SKILLS_SHEET_ID` (tìm ID trong URL của Sheet: `https://docs.google.com/spreadsheets/d/[ID]/edit`).

##### **B. Cấu hình OpenAI API Key**
1. Trong node **"OpenAI — GPT-4o-mini Model"**:
   - Kết nối **OpenAI API credential** (tạo mới trong n8n).
   - Đảm bảo **API Key** đã được cấp quyền sử dụng **gpt-4o-mini**.

##### **C. Cấu hình các node quan trọng**
1. **Node "3. Code — Format Skills for Agent"**:
   - **Không cần chỉnh sửa** (n8n tự động format dữ liệu từ Google Sheets thành định dạng phù hợp cho AI Agent).
   - Nếu cần thay đổi logic, các sếp có thể mở node này và chỉnh sửa mã JavaScript (nhưng **không khuyến nghị** vì có thể làm workflow bị lỗi).

2. **Node "4. AI Agent — Skills Executor"**:
   - **Không cần cấu hình thêm** (n8n tự động xử lý việc match trigger phrases với kỹ năng phù hợp).
   - AI sẽ **không sử dụng kiến thức chung** nếu không tìm thấy kỹ năng phù hợp.

3. **Node "Session Memory"**:
   - **Không cần cấu hình** (n8n tự động lưu trữ lịch sử hội thoại trong mỗi phiên chat).
   - Thời gian lưu trữ mặc định là **15 phút** (có thể điều chỉnh trong mã của node "memoryBufferWindow").

4. **Node "5. Respond to Chat"**:
   - **Không cần chỉnh sửa** (n8n tự động trả lời lại chat interface).

---

#### 3. Kích hoạt ⚡️
1. **Test run dữ liệu mẫu**:
   - Mở tab **"Chat Trigger"** trong workflow.
   - Gửi một **yêu cầu test** (ví dụ: *"summarize report"*).
   - Kiểm tra AI có phản hồi chính xác theo kỹ năng đã định nghĩa không.

2. **Bật Active workflow**:
   - Chuyển trạng thái workflow từ **"Inactive"** sang **"Active"**.
   - Lưu workflow.

3. **Mở chat interface**:
   - URL của **Chat Trigger** sẽ được hiển thị trong node "Chat Trigger".
   - Mở URL này trong trình duyệt để bắt đầu chat với AI.

---

### ✍️ Mẹo & gợi ý nâng cao
1. **Thêm nhiều kỹ năng hơn**:
   - Các sếp có thể thêm các kỹ năng mới vào Google Sheets (ví dụ: *tạo slide PowerPoint*, *tổng kết cuộc họp*, *viết bài LinkedIn*).
   - **Lưu ý**: Chỉ các kỹ năng với **Active = Yes** mới được AI sử dụng.

2. **Kết nối với Slack/Telegram**:
   - Thay vì sử dụng chat interface mặc định của n8n, các sếp có thể **kết nối với Slack/Telegram** bằng node **Slack** hoặc **Telegram Bot**.
   - Cách làm:
     - Thêm node **Slack** hoặc **Telegram Bot** vào workflow.
     - Kết nối với credential Slack/Telegram.
     - Thay thế node **"Chat Trigger"** bằng node **Webhook** (để nhận tin nhắn từ Slack/Telegram).

3. **Lưu log hoạt động**:
   - Thêm node **Google Sheets** hoặc **Database** để lưu lịch sử các câu hỏi và phản hồi của AI.
   - Cách làm:
     - Thêm node **Google Sheets** mới sau node **"Respond to Chat"**.
     - Lưu các thông tin như: *Thời gian, Câu hỏi, Phản hồi AI, Kỹ năng sử dụng*.

4. **Gửi báo cáo định kỳ**:
   - Thêm node **Email** hoặc **Slack Notification** để gửi báo cáo tổng hợp về các kỹ năng được sử dụng nhiều nhất.
   - Cách làm:
     - Thêm node **Code** để tính toán thống kê (ví dụ: kỹ năng nào được sử dụng nhiều nhất trong tuần).
     - Kết nối với node **Email** hoặc **Slack** để gửi báo cáo tự động hàng tuần.

5. **Tối ưu hóa AI**:
   - Nếu muốn AI phản hồi **nhanh hơn**, các sếp có thể:
     - **Giảm kích thước kỹ năng**: Tránh viết các kỹ năng quá dài trong cột **Instructions**.
     - **Sử dụng GPT-4o-mini** thay vì mô hình khác (nếu budget cho phép).

---

### 📌 Kết luận
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tạo một **chatbot AI cá nhân hóa, không cần code**, và có thể điều khiển hoàn toàn bằng Google Sheets. Với **GPT-4o-mini**, AI sẽ phản hồi **chính xác, nhanh chóng và nhớ lịch sử hội thoại**, giúp tiết kiệm thời gian và tăng hiệu suất công việc.

**Bắt đầu ngay hôm nay!**
1. **Tạo Google Sheet** với cấu trúc kỹ năng.
2. **Import workflow** vào n8n Self-hosted.
3. **Cấu hình Google Sheets và OpenAI API Key**.
4. **Bật workflow** và thử nghiệm với chat interface.

👉 [Tải workflow từ n8n.io](https://n8n.io/workflows/16117) và **cài đặt VPS** để bắt đầu tự động hóa công việc của mình!

---
**Chia sẻ và phản hồi**: Nếu các sếp có bất kỳ câu hỏi hoặc gặp khó khăn, hãy để lại comment bên dưới. Chúng tôi sẽ hỗ trợ miễn phí! 🚀