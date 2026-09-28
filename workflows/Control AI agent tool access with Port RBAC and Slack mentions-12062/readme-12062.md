---
title: "🔒 **Quản lý quyền truy cập AI Agent thông qua RBAC Port + Slack Mention (Tự động hóa 100% không code)**"
description: "Workflow tự động kiểm tra và cấp quyền sử dụng các công cụ AI cho người dùng Slack thông qua hệ thống RBAC của Port.io, đảm bảo an toàn và tuân thủ chính sách doanh nghiệp. Giúp các sếp loại bỏ rủi ro sử dụng sai công cụ, tiết kiệm thời gian quản lý và tăng cường an ninh dữ liệu."
slug: "quan-ly-quyen-ai-agent-port-slack"
tags: [n8n, automation, ai-agent, rbac, slack, port-io, no-code, ai-chatbot, security]
keywords: [n8n workflow rbac, tự động hóa quản lý quyền ai agent, slack mention + port io, kiểm tra quyền truy cập công cụ ai, tự động hóa an ninh dữ liệu, workflow ai agent an toàn]
---

# 🚀 **Quản lý quyền truy cập AI Agent thông qua RBAC Port + Slack Mention**

## 💡 **Giải pháp cho vấn đề gì?**
Các sếp đang gặp khó khăn khi:
- **AI Agent tự do sử dụng các công cụ** như PagerDuty, AWS S3, Wikipedia, Calculator mà không kiểm soát quyền truy cập.
- **Rủi ro an ninh dữ liệu** khi người dùng không được cấp phép vẫn có thể gọi các API nhạy cảm.
- **Phải kiểm tra thủ công** mỗi khi có yêu cầu mới, tốn thời gian và dễ xảy ra lỗi.
- **Không có cơ chế tự động thông báo** khi người dùng cố gắng sử dụng công cụ không được phép.

**Workflow này giải quyết tất cả đó bằng cách:**
✅ **Kiểm tra quyền truy cập thực thời** khi người dùng @mention bot Slack.
✅ **Chỉ cho phép sử dụng các công cụ đã được cấp phép** thông qua hệ thống RBAC của Port.io.
✅ **Tự động gửi thông báo** nếu người dùng cố gắng sử dụng công cụ không được phép.
✅ **Ghi log và báo cáo** để quản lý dễ dàng.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **An toàn tuyệt đối**: Chỉ cho phép người dùng sử dụng các công cụ đã được cấp phép.
- **Tiết kiệm thời gian**: Không cần kiểm tra thủ công mỗi lần người dùng yêu cầu sử dụng công cụ.
- **Tự động hóa thông báo**: Ngăn chặn người dùng cố gắng sử dụng công cụ không được phép bằng cách gửi tin nhắn Slack rõ ràng.
- **Dễ dàng quản lý**: Sử dụng hệ thống RBAC của Port.io để cập nhật quyền truy cập một cách đơn giản.
- **Hoạt động liên tục**: Workflow chạy tự động 24/7, không cần can thiệp của con người.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Slack**:
   - Bot Slack đã được tạo và invite vào channel cần sử dụng.
   - **Credentials**: `slackApi` (API Token của bot Slack).
2. **Tài khoản OpenAI**:
   - API Key của OpenAI để sử dụng mô hình `gpt-4o`.
3. **Tài khoản Port.io**:
   - Tạo **rbacUser blueprint** với thuộc tính `allowed_tools` (mảng chuỗi).
   - Thêm các user entity với email và danh sách công cụ được phép.
   - **Credentials**: `httpBearerAuth` (Client ID và Secret của Port.io).
4. **Các dịch vụ công cụ (nếu cần)**:
   - **PagerDuty**: API Key (`pagerDutyApi`) để tạo incident.
   - **AWS S3**: Credentials (`aws`) để tạo bucket.
   - **Wikipedia/Calculator**: Không cần credentials, chỉ cần kết nối.
5. **Channel Slack**:
   - Đặt ID của channel Slack trong node `Slack Trigger`.
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### 1. **Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/12062](https://n8n.io/workflows/12062) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ link trên và paste vào **Import Workflow** trong n8n Editor.

#### 2. **Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình Credentials**
- **Slack**:
  - Node `Slack Trigger` và `Send a message`: Điền `slackApi` (API Token của bot Slack).
  - Node `Get user's slack profile`: Chọn `slackApi` và chọn operation `getProfile`.
- **OpenAI**:
  - Node `OpenAI Chat Model`: Điền `openAiApi` và chọn mô hình `gpt-4o`.
- **Port.io**:
  - Node `Get Port access token`: Điền `httpBearerAuth` (Client ID và Secret của Port.io).
  - Node `Get user permission from Port`: Chọn `httpBearerAuth` và cấu hình URL API của Port.io (ví dụ: `https://api.port.io/v1/rbacUser/{email}`).
- **PagerDuty (nếu sử dụng)**:
  - Node `Create an incident in PagerDuty`: Điền `pagerDutyApi`.
- **AWS S3 (nếu sử dụng)**:
  - Node `Create a bucket in AWS S3`: Điền `aws`.

##### **B. Cấu hình Node `Check permissions` (Code Node)**
- Mở node `Check permissions` và chỉnh sửa code để phù hợp với API của Port.io. Ví dụ:
  ```javascript
  // Kiểm tra user có tồn tại và lấy danh sách allowed_tools
  const userEmail = $input.all().user_email;
  const response = await $node["Get user permission from Port"].execute({});
  const allowedTools = response.json().allowed_tools || [];

  // So sánh với danh sách công cụ được phép
  const permittedTools = ["toolWikipedia", "toolCalculator", "pagerDutyTool", "awsS3Tool"];
  const filteredTools = permittedTools.filter(tool => allowedTools.includes(tool));

  // Trả về danh sách công cụ được phép
  return { json: { allowedTools: filteredTools } };
  ```

##### **C. Cấu hình Node `AI Agent`**
- Node này sẽ sử dụng danh sách `allowedTools` từ node `Check permissions` để chỉ cho phép sử dụng các công cụ đã được cấp phép.
- Đảm bảo node `AI Agent` có instruction rõ ràng:
  ```
  Always use the connected tools to respond to the user's request.
  If a tool is not authorized, return a message: "You are not authorized to use this tool."
  ```

##### **D. Cấu hình Node `Slack Trigger`**
- Đặt `Channel ID` của Slack channel bạn muốn bot lắng nghe.
- Đặt `Trigger Phrase` là `@botname` (ví dụ: `@ai-assistant`).

#### 3. **Kích hoạt ⚡️**
- **Test Run**: Chạy workflow với dữ liệu mẫu để kiểm tra:
  - Bot có lắng nghe được @mention không?
  - AI Agent có kiểm tra quyền truy cập không?
  - Bot có gửi tin nhắn Slack phản hồi không?
- **Bật Active**: Sau khi test thành công, bật workflow để hoạt động liên tục.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm Log & Monitoring**:
   - Sử dụng node `stickyNote` để ghi log mỗi lần kiểm tra quyền truy cập.
   - Kết nối với **Google Sheets** hoặc **AWS S3** để lưu lịch sử hoạt động.

2. **Tự động Báo cáo**:
   - Sử dụng node `pagerDutyTool` để báo cáo các sự cố (ví dụ: user cố gắng sử dụng công cụ không được phép).
   - Gửi báo cáo định kỳ qua Slack hoặc email.

3. **Cá nhân hóa Trải nghiệm**:
   - Thêm node `memoryBufferWindow` để lưu lịch sử chat của từng user, giúp AI Agent trả lời thông minh hơn.

4. **Kết hợp với Các Dịch Vụ Khác**:
   - Thêm **Google Drive** để lưu các file từ AWS S3.
   - Kết nối với **Notion** để cập nhật wiki nội bộ khi có yêu cầu mới.

5. **Cập Nhật Quyền Truy cập**:
   - Sử dụng **Port.io API** để tự động cập nhật quyền truy cập cho user khi có thay đổi trong blueprint.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** để các sếp quản lý quyền truy cập AI Agent một cách tự động, an toàn và hiệu quả. Bằng cách kết hợp **RBAC của Port.io** và **Slack Mention**, bạn không chỉ tiết kiệm thời gian mà còn **giảm thiểu rủi ro an ninh dữ liệu** đáng kể.

**Hành động ngay hôm nay:**
1. Import workflow và cấu hình theo hướng dẫn.
2. Test với một user test và kiểm tra phản hồi.
3. Bật workflow và bắt đầu tự động hóa quản lý quyền truy cập AI Agent!

👉 **Cần hỗ trợ thêm?** Đăng ký VPS n8n tại [TinoHost](https://tino.vn/vps-n8n?affid=388) để workflow chạy ổn định 24/7!