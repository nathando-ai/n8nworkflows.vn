---
title: "🐾 **Tự Động Hóa Nghiên Cứu Tin Tức & Báo Cáo Tuần Kỷ Cho Sự Cứu Động Động Vật Với Claude AI & Serper**"
description: "Workflow tự động hóa tìm kiếm tin tức mới nhất về quyền lợi động vật, tổng hợp và gửi báo cáo tuần kỳ dưới dạng email HTML bằng Claude AI và Serper. Giúp các tổ chức phi lợi nhuận tiết kiệm thời gian lên tới 20 giờ/tuần, đồng thời cung cấp nội dung chính xác và chuyên nghiệp cho chiến dịch vận động."
slug: "tu-dong-hoa-nghien-cuu-tin-tuc-su-cuu-dong-vat"
tags: [n8n, automation, ai-summarization, animal-advocacy, serper, claude-ai]
keywords: [tự động hóa nghiên cứu tin tức động vật, workflow n8n Claude AI, báo cáo tuần kỳ quyền lợi động vật, Serper API tự động, email tự động hóa cho tổ chức phi lợi nhuận]
---

# 🚀 **Tự Động Hóa Nghiên Cứu Tin Tức & Báo Cáo Tuần Kỷ Cho Sự Cứu Động Động Vật**

Hiện nay, các tổ chức phi lợi nhuận (NPO) và vận động viên quyền lợi động vật phải mất **từ 15-20 giờ/tuần** để thủ công tìm kiếm, lọc và tổng hợp tin tức mới nhất về **công nghiệp nuôi trồng động vật, luật bảo vệ động vật, hoặc các vụ bê bối liên quan**. Kết quả là:
- **Thông tin không đầy đủ hoặc lỗi thời** khi gửi đến cộng đồng.
- **Tốn kém nhân lực** khi phải duy trì theo dõi liên tục.
- **Không cá nhân hóa** được nội dung cho từng nhóm đối tượng.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động tìm kiếm tin tức** từ Serper (Google-like search) trong vòng 7 ngày qua.
✅ **Tổng hợp và viết báo cáo HTML** bằng **Claude AI (OpenRouter)**, đảm bảo nội dung **chuyên nghiệp, ngắn gọn và tập trung vào hành động vận động**.
✅ **Gửi email tự động** mỗi tuần đến nhóm vận động viên, với **định dạng email responsive** (hoạt động trên mobile/desktop).
✅ **Không cần code** – chỉ cần cấu hình và chạy 24/7.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo **tính riêng tư và ổn định**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 20 giờ/tuần** cho đội ngũ nghiên cứu.
- **Nội dung chính xác và cập nhật** từ Serper + Claude AI.
- **Báo cáo định dạng email HTML** dễ đọc trên mọi thiết bị.
- **Tự động hóa hoàn toàn** – không cần can thiệp thủ công.
- **Cá nhân hóa** được chủ đề nghiên cứu (ví dụ: tập trung vào **lập pháp bảo vệ động vật** hoặc **vụ bê bối nuôi gà công nghiệp**).
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản OpenRouter API** (để sử dụng Claude AI):
   - [Đăng ký miễn phí tại OpenRouter](https://openrouter.ai/) và lấy **API Key**.
   - **Model khuyến nghị**: `anthropic/claude-sonnet-4` (đã cấu hình sẵn trong workflow).
2. **Tài khoản SMTP** (để gửi email tự động):
   - Có thể dùng **Gmail (SMTP), SendGrid, hoặc Mailgun**.
   - Cấu hình **SMTP Credentials** trong n8n (Host, Port, Username, Password).
3. **Workflow con "Multi-tool Research Agent"** (bắt buộc):
   - [Tải workflow này](https://n8n.io/workflows/5588-multi-tool-research-agent-for-animal-advocacy-with-openrouter-serper-and-open-paws-db/) và **import trước** vào n8n.
   - Workflow này sẽ **tìm kiếm tin tức** từ Serper và các nguồn khác.
4. **Email nhận báo cáo** (cần điền vào node **Set Preferences**).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/6482](https://n8n.io/workflows/6482) và **import vào n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ trang trên và **paste vào n8n Editor** (tab "Import").
- **Lưu ý**: Nếu import từ file, **không cần chỉnh sửa** phần **Call Research Agent** (nó sẽ tự động gọi workflow con đã import trước).

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình Schedule Trigger (Điều khiển thời gian chạy)**
- **Mode**: Chọn **Cron**.
- **Day of Week**: **Thứ 2** (hoặc ngày bạn muốn).
- **Hour**: **09:00** (thời gian bạn ưa thích).
- **Lưu ý**:
  - Nếu muốn **chạy hàng ngày** thay vì hàng tuần, **duplicate workflow** và thay đổi:
    ```json
    "tbs": "qdr:d"  // Thay vì "qdr:w" (tuần) thành "qdr:d" (ngày)
    ```
    (Điền vào node **Call Research Agent** và **Write HTML Report**).

##### **B. Cấu hình Set Preferences (Chủ đề & Email nhận)**
- **Update Topics**: Danh sách **chủ đề nghiên cứu** (ví dụ):
  ```json
  ["factory farming exposés", "animal rights laws", "wildlife trafficking", "vegan advocacy"]
  ```
- **Update Instructions**: Hướng dẫn tổng hợp (ví dụ):
  ```json
  "Focus on advocacy actions and credible sources. Use bullet points for key takeaways."
  ```
- **Recipient Email**: Điền **email của nhóm vận động viên** (ví dụ: `team@openpaws.org`).

##### **C. Cấu hình OpenRouter Chat Model (Claude AI)**
- **Credentials**: Chọn **openRouterApi** (đã cấu hình sẵn API Key).
- **Model**: Đã mặc định là `anthropic/claude-sonnet-4` (không cần thay đổi).

##### **D. Cấu hình Send Email (Gửi báo cáo)**
- **Credentials**: Chọn **smtp** (đã cấu hình SMTP trước).
- **Subject**: Đã mặc định là `Animal Advocacy Weekly Brief – {{ $now }}` (hiển thị ngày tháng).
- **Body**: Sử dụng **HTML output** từ node **Write HTML Report**.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chọn **Test Tab** trong n8n Editor.
   - Nhấn **Run Workflow** để kiểm tra email có gửi đúng không.
2. **Bật Active**:
   - Sau khi test thành công, **bật Active** để workflow chạy tự động hàng tuần.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm Slack/Telegram Notification**:
   - Sử dụng **node Slack Send Message** hoặc **Telegram Bot** để thông báo khi báo cáo được gửi.
   - **Cách làm**:
     ```json
     {
       "name": "Notify Slack",
       "type": "slackSendMessage",
       "credentials": ["slack"],
       "parameters": {
         "channel": "#animal-advocacy",
         "text": "📩 Weekly brief sent! Check email for details."
       }
     }
     ```
2. **Lưu log vào Google Sheets**:
   - Sử dụng **node Google Sheets** để ghi lại **liên kết tin tức** và **ngày gửi**.
   - **Ưu điểm**: Theo dõi được lịch sử báo cáo.
3. **Tùy chỉnh độ dài báo cáo**:
   - Trong node **Write HTML Report**, thêm tham số:
     ```json
     "max_length": 1500  // Giảm số lượng từ trong báo cáo
     ```
4. **Kết hợp với Notion/Confluence**:
   - Thay vì gửi email, **ghi báo cáo vào Notion** bằng node **Notion Create Page**.

---

### 📌 **Kết luận**
Workflow này **giải phóng đội ngũ nghiên cứu** khỏi công việc thủ công, đồng thời **cung cấp báo cáo chuyên nghiệp** mỗi tuần với **tính tự động hóa hoàn toàn**. Đặc biệt phù hợp cho:
- **Tổ chức phi lợi nhuận** vận động quyền lợi động vật.
- **Nhà hoạt động** cần cập nhật tin tức mới nhất.
- **Nhà báo/nhà nghiên cứu** theo dõi xu hướng công nghiệp động vật.

**Hành động ngay**:
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test Run** trước khi bật Active.
3. **Chia sẻ với đồng nghiệp** để tối ưu hóa chiến dịch!

---
**🔗 [Tải workflow gốc tại n8n.io](https://n8n.io/workflows/6482)**
**📌 [Hướng dẫn chi tiết về workflow con Research Agent](https://n8n.io/workflows/5588-multi-tool-research-agent-for-animal-advocacy-with-openrouter-serper-and-open-paws-db/)**