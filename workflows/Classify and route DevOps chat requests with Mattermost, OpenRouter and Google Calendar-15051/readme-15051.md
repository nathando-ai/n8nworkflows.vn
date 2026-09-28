---
title: "🤖 Tự Động Hóa & Phân Loại Yêu Cầu DevOps Trên Mattermost Với AI + Google Calendar (N8N)"
description: "Giải pháp tự động hóa hoàn toàn không cần code để phân loại và chuyển tiếp yêu cầu DevOps từ Mattermost sang người phụ trách hiện tại, giảm thiểu thời gian phản hồi và tối ưu hóa công việc 24/7."
slug: "tieu-dong-hoa-phan-loai-yeu-cau-devops-mattermost-ai-google-calendar"
tags: [n8n, automation, devops, ai-chatbot, mattermost, google-calendar, openrouter, no-code]
keywords: [tự động hóa devops, phân loại yêu cầu devops, mattermost webhook, ai chatbot n8n, google calendar on-call, openrouter n8n]
---

# 🚀 Tự Động Hóa Phân Loại & Chuyển Tiếp Yêu Cầu DevOps Trên Mattermost Với AI + Google Calendar

## 🔍 Nỗi Đau Của Các Sếp DevOps
Các sếp DevOps thường phải đối mặt với tình trạng:
- **Lượng yêu cầu từ team phát triển** tăng cao, nhưng việc phân loại và chuyển tiếp yêu cầu thủ công tốn thời gian và dễ gây nhầm lẫn.
- **Không biết ai là người phụ trách** hiện tại trong lịch on-call, dẫn đến phản hồi chậm trễ.
- **Phải theo dõi nhiều kênh** (Mattermost, email, Slack) để quản lý yêu cầu, làm giảm hiệu suất công việc.

Workflow này **giải quyết tất cả những vấn đề trên** bằng cách tự động:
✅ **Phân loại yêu cầu** thành 8 danh mục chính xác với AI (OpenRouter + Claude Sonnet).
✅ **Tìm người phụ trách** hiện tại từ Google Calendar (lịch on-call).
✅ **Chuyển tiếp tự động** yêu cầu đến người đúng, đồng thời **trả lời ngay** trong Mattermost với kết quả phân loại.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng** (Self-hosted) để tránh giới hạn của phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 Kết Quả Các Sếp Nhận Được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 5-10 giờ/tuần** cho team DevOps bằng việc loại bỏ công việc phân loại và chuyển tiếp thủ công.
- **Phản hồi nhanh chóng** (trong giây phút) với thông báo tự động trong Mattermost, giảm thiểu sự chậm trễ.
- **Tối ưu hóa công việc on-call** bằng cách tự động xác định người phụ trách hiện tại từ Google Calendar.
- **Giảm nhầm lẫn** trong việc phân loại yêu cầu, đảm bảo mỗi yêu cầu được chuyển đến người đúng.
- **Hoạt động liên tục** (24/7) mà không cần can thiệp của con người.
:::

---

### 🔧 Yêu Cầu Cần Thiết
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Mattermost**:
   - Một **outgoing webhook** được cấu hình để gửi yêu cầu đến workflow (khi nhắc `@devops-duty`).
   - **Token webhook** (sẽ được sử dụng để xác thực yêu cầu).
2. **Tài khoản OpenRouter**:
   - **API Key** của OpenRouter (để kết nối với model AI `anthropic/claude-sonnet-4.6`).
3. **Tài khoản Google Calendar**:
   - **OAuth2 API Key** để đọc lịch on-call.
   - **Calendar ID** của lịch on-call (định dạng: `Devops duty: @username`).
4. **Workflow n8n**:
   - Cài đặt **n8n Community Edition** (self-hosted) hoặc **n8n Cloud** (nếu không muốn tự cài).

---

### 🚀 Cách Import & Lưu Ý Khi "Lên Đồ"

#### 1. Import Workflow 📥
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [n8n.io/workflows/15051](https://n8n.io/workflows/15051).
- Mở **n8n Editor** → Nhấn **Import** → Chọn file JSON hoặc dán JSON vào ô `Paste JSON`.

#### 2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌
Sau khi import, các sếp cần **cấu hình chi tiết** các node quan trọng:

##### **A. Webhook (GetQuestions)**
- **Path**: Đã mặc định là `f25e385c-a923-4c60-8b6e-a1a7ed6c7227` (không cần thay đổi).
- **HTTP Method**: `POST` (không thay đổi).
- **Lưu ý**:
  - Đảm bảo **outgoing webhook** của Mattermost được cấu hình để gửi yêu cầu đến URL này.
  - **Token xác thực** (EXPECTED_TOKEN) sẽ được kiểm tra trong node `ValidateAndExtractMessage` (xem phần sau).

##### **B. ValidateAndExtractMessage (Code Node)**
- **Mã nguồn**:
  ```javascript
  // Kiểm tra token và trích xuất thông tin từ yêu cầu Mattermost
  const expectedToken = "YOUR_MATTERMOST_WEBHOOK_TOKEN"; // Thay thế bằng token của bạn
  const token = $input.all().token;

  if (token !== expectedToken) {
    throw new Error("Invalid token");
  }

  const message = $input.all().message;
  const user = $input.all().user;

  return {
    json: {
      message: message,
      user: user,
    },
  };
  ```
- **Cách làm**:
  - Mở node `ValidateAndExtractMessage` → Nhấn **Edit** → Thay thế `YOUR_MATTERMOST_WEBHOOK_TOKEN` bằng **token webhook** của Mattermost.
  - Lưu và kiểm tra lại.

##### **C. OpenRouter Chat Model (Basic LLM Chain)**
- **Model**: Đã mặc định là `anthropic/claude-sonnet-4.6` (có thể thay đổi nếu muốn).
- **Credentials**:
  - Đảm bảo đã thêm **OpenRouter API Key** trong `n8n Credentials` (tên: `openRouterApi`).
  - Cách thêm:
    - Mở **Credentials** → Nhấn **+ Add** → Chọn **OpenRouter API** → Điền API Key → Lưu.

##### **D. Switch Node**
- **Cấu trúc logic**:
  - Node này sẽ **chuyển tiếp yêu cầu** đến các node khác dựa trên kết quả phân loại từ AI.
  - Các trường hợp mặc định:
    - `urgent` → Chuyển đến node `Reply Investigating` (trả lời ngay).
    - `on-call` → Kết hợp với Google Calendar để tìm người phụ trách.
    - Các trường hợp khác (ví dụ: `documentation`, `infrastructure`) có thể được cấu hình thêm.

##### **E. Mattermost (Reply Investigating)**
- **Credentials**:
  - Thêm **Mattermost API Key** trong `n8n Credentials` (tên: `mattermostApi`).
  - Cách thêm:
    - Mở **Credentials** → Nhấn **+ Add** → Chọn **Mattermost API** → Điền token API → Lưu.
- **Lưu ý**:
  - Đảm bảo **outgoing webhook** của Mattermost được cấu hình để gửi yêu cầu đến workflow.

##### **F. Google Calendar (GetDutyEvent)**
- **Credentials**:
  - Thêm **Google Calendar OAuth2 API Key** trong `n8n Credentials` (tên: `googleCalendarOAuth2Api`).
  - Cách thêm:
    - Mở **Credentials** → Nhấn **+ Add** → Chọn **Google Calendar OAuth2** → Theo hướng dẫn để kết nối.
- **Key Parameters**:
  - `operation`: Đã mặc định là `getAll` (không cần thay đổi).
  - **Calendar ID**: Đảm bảo **lịch on-call** của bạn có định dạng `Devops duty: @username`.

##### **G. Inject duty name (Code Node)**
- **Mã nguồn**:
  ```javascript
  // Trích xuất tên người phụ trách từ Google Calendar và gắn vào yêu cầu
  const dutyEvent = $input.all().json;
  const dutyName = dutyEvent.name; // Giả sử format: "Devops duty: @username"

  return {
    json: {
      ...$input.all(),
      dutyName: dutyName,
    },
  };
  ```
- **Lưu ý**:
  - Node này sẽ **trích xuất tên người phụ trách** từ Google Calendar và gắn vào yêu cầu trước khi chuyển tiếp.

#### 3. Kích Hoạt ⚡️
- **Test Run**:
  - Gửi một yêu cầu mẫu từ Mattermost (nhắc `@devops-duty`).
  - Kiểm tra **log** trong n8n để đảm bảo workflow chạy đúng.
- **Bật Active**:
  - Sau khi kiểm tra thành công, chuyển trạng thái workflow từ `Inactive` sang `Active`.

---

### ✍️ Mẹo & Gợi Ý Nâng Cao
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để gửi thông báo về yêu cầu mới đến các sếp DevOps.

2. **Lưu Log Yêu Cầu**:
   - Thêm node **Google Sheets** hoặc **Airtable** để lưu lịch sử yêu cầu, giúp theo dõi và phân tích hiệu suất.

3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng node **n8n-nodes-base.email** hoặc **Slack Alert** để gửi báo cáo tổng hợp yêu cầu hàng tuần.

4. **Cải Thiện Model AI**:
   - Thay đổi model OpenRouter thành một model mạnh hơn (ví dụ: `mistral-large-2407`) nếu cần độ chính xác cao hơn.

5. **Tự Động Xóa Yêu Cầu Sau Xử Lý**:
   - Thêm node **Mattermost** để tự động xóa yêu cầu sau khi đã được xử lý (nếu không cần lưu lại).

---

### 📌 Kết Luận
Workflow này **giải phóng thời gian** cho team DevOps bằng cách tự động hóa việc phân loại và chuyển tiếp yêu cầu, đồng thời **tăng cường hiệu quả** trong quản lý on-call. Với chỉ **vài bước cấu hình**, các sếp có thể bắt đầu sử dụng ngay và **tận hưởng lợi ích ngay từ ngày đầu tiên**.

**Hành động ngay hôm nay**:
1. Cài đặt **n8n trên VPS** (nếu chưa có).
2. Import workflow và **cấu hình các credentials** theo hướng dẫn.
3. **Test với một yêu cầu mẫu** và bắt đầu tự động hóa!

---
**Chia sẻ và phản hồi**: Nếu các sếp có bất kỳ câu hỏi hoặc cần hỗ trợ, hãy để lại bình luận dưới đây hoặc liên hệ với tác giả [Sergei Byvshev](https://n8n.io/workflows/15051) để được hỗ trợ chi tiết!