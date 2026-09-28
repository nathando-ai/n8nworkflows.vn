---
title: "🤖 **Tự Động Hóa Tạo & Thực Thi Claude Skills Với AI (GitHub + Anthropic + OpenAI) – Không Cần Code!**"
description: "Workflow n8n tiên tiến giúp các sếp tự động hóa việc **tạo các skill AI cá nhân hóa** từ Claude (Anthropic) và **thực thi chúng** thông qua GitHub, tiết kiệm thời gian lên đến 80% so với làm thủ công. Hỗ trợ cả OpenAI và Context7 cho tài liệu cập nhật."
slug: "tieu-dong-hoa-tao-thuc-thi-claude-skills-github-anthropic-openai"
tags: [n8n, automation, ai-chatbot, github-actions, anthropic, openai, langchain, no-code]
keywords: [tự động hóa claudie skills, n8n workflow ai, tạo skill ai với github, anthropic api n8n, openai chatbot tự động, langchain n8n, tự động hóa marketing ai]
---

# **🚀 Tự Động Hóa Tạo & Thực Thi Claude Skills Với AI – Giải Pháp AI Tối Tiến Cho Doanh Nghiệp**

## **💡 Giới Thiệu: Tại Sao Các Sếp Cần Workflow Này?**
Hiện nay, việc **tạo và quản lý các skill AI cá nhân hóa** (như Claude Skills) thường đòi hỏi sự tham gia của các chuyên gia kỹ thuật, tiêu tốn thời gian và chi phí cao. Với **workflow này**, các sếp có thể:
✅ **Tạo skill AI mới** một cách tự động hóa hoàn toàn, chỉ cần giao tiếp qua chatbot.
✅ **Thực thi skill đã có** từ GitHub một cách chính xác, dựa trên logic trong file `SKILL.md`.
✅ **Tích hợp Anthropic (Claude), OpenAI, và Context7** để đảm bảo tài liệu và logic luôn cập nhật.
✅ **Tiết kiệm thời gian lên đến 80%** so với cách làm thủ công, đồng thời giảm thiểu lỗi do con người gây ra.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
- **Tạo skill AI mới chỉ trong vài phút** thay vì nhiều giờ làm thủ công.
- **Thực thi logic AI một cách tự động** từ các file `SKILL.md` trên GitHub.
- **Cập nhật tài liệu tự động** bằng Context7 (không cần chỉnh sửa thủ công).
- **Hoạt động 24/7** mà không cần can thiệp của con người.
- **Cá nhân hóa skill** cho từng dự án hoặc khách hàng riêng biệt.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[**Chuẩn Bị Trước Khi Bắt Đầu**]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản GitHub** với một repository chứa thư mục `skills/` (để lưu trữ các file `SKILL.md`).
2. **API Key của Anthropic** (để sử dụng Claude Sonnet 4.x).
3. **API Key của OpenAI** (tùy chọn, nếu muốn sử dụng GPT-5 Mini).
4. **API Key của Context7** (để lấy tài liệu cập nhật cho skill).
5. **Webhook URL** để chatbot gửi tin nhắn vào workflow (có thể từ Slack, Discord, hoặc một trang web cá nhân).
6. **n8n Self-hosted** (không dùng phiên bản miễn phí để đảm bảo hoạt động 24/7).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/15225) hoặc copy toàn bộ mã JSON dưới đây.
- Mở **n8n Editor** → Nhấn **Import** → Chọn file JSON hoặc dán mã JSON vào ô **Import Workflow**.
- **Lưu ý:** Workflow này có **24 node**, nên đảm bảo kết nối mạng ổn định khi import.

```json
// (Mã JSON đầy đủ sẽ được cung cấp sau khi hoàn thành bài viết)
```

### **2. Các Bước Cấu Hình Bắt Buộc 📌**
Sau khi import, các sếp cần **cấu hình các node quan trọng** như sau:

#### **🔹 Node 1: "When chat message received" (chatTrigger)**
- **Cấu hình webhook** để nhận tin nhắn từ chatbot (Slack, Discord, hoặc trang web cá nhân).
- **Lưu ý:** Đảm bảo URL webhook được cấu hình đúng trong n8n và trong ứng dụng chatbot.

#### **🔹 Node 2-3: "Simple Memory" (memoryBufferWindow)**
- **Đặt `sessionId` duy nhất** cho mỗi phiên chat (ví dụ: `user_${dateTime}`).
- **Lưu ý:** Các node này giữ lịch sử chat để AI có thể tham chiếu trong các lần tương tác sau.

#### **🔹 Node 4: "Context7" (mcpClientTool)**
- **Thêm API Key của Context7** vào credentials.
- **Cấu hình URL API** của Context7 (thường là `https://api.context7.ai/v1/search`).
- **Lưu ý:** Context7 giúp lấy tài liệu cập nhật cho skill, đảm bảo logic AI không lỗi thời.

#### **🔹 Node 5-6: "OpenAI Chat Model" & "Anthropic Chat Model" (lmChatOpenAi / lmChatAnthropic)**
- **Thêm API Key của OpenAI/Anthropic** vào credentials tương ứng.
- **Chọn model**:
  - OpenAI: `gpt-5-mini` (hoặc model khác).
  - Anthropic: `claude-sonnet-4-6` hoặc `claude-sonnet-4-5-20250929`.
- **Lưu ý:** Đảm bảo model được chọn phù hợp với yêu cầu của skill.

#### **🔹 Node 7-8: "List Skills" & "List Files" (github)**
- **Thêm credentials GitHub** (tên tài khoản + token).
- **Cấu hình repository URL** (ví dụ: `https://github.com/ten-taikhoan/reponame`).
- **Lưu ý:** Thư mục `skills/` phải tồn tại trong repo để workflow có thể tìm kiếm và tạo skill mới.

#### **🔹 Node 9-10: "Skills Agent" & "AI Conversational Agent" (agent)**
- **Không cần cấu hình thêm**, nhưng có thể **cập nhật prompt** để điều chỉnh hành vi của AI.
- **Lưu ý:** Các agent này sẽ tự động quyết định xem người dùng muốn **tạo skill mới** hay **thực thi skill đã có**.

#### **🔹 Node 11-12: "Extract Skill MD" & "SKILL.md Parser" (informationExtractor / code)**
- **Node `informationExtractor`** sẽ phân tích nội dung chat để tạo file `SKILL.md`.
- **Node `code`** sẽ xử lý logic trong file Markdown (nếu cần).
- **Lưu ý:** Đảm bảo file `SKILL.md` được tạo với **cấu trúc YAML frontmatter** và **logic rõ ràng** (≤500 dòng).

#### **🔹 Node 13: "Create a Skill" (github)**
- **Chọn action**: `Create a file`.
- **Điền thông tin**:
  - **Path**: `skills/<ten-skill>/SKILL.md` (ví dụ: `skills/tim-kiem-thong-tin/SKILL.md`).
  - **Content**: Nội dung file `SKILL.md` từ node trước.
- **Lưu ý:** Workflow sẽ tự động upload file lên GitHub.

#### **🔹 Node 14: "Claude Skills Creator Agent" (agent)**
- **Agent này sẽ kiểm tra và hoàn thiện skill** trước khi upload.
- **Lưu ý:** Có thể **cập nhật prompt** để AI tạo skill phù hợp với yêu cầu cụ thể.

---
### **3. Kích Hoạt Workflow ⚡️**
1. **Test run** với một tin nhắn mẫu:
   - Gửi tin nhắn: **"Tạo một skill tìm kiếm thông tin về SEO"** → Workflow sẽ tự động tạo file `SKILL.md` và upload lên GitHub.
2. **Bật Active workflow** sau khi kiểm tra thành công.
3. **Kết nối với chatbot** (Slack/Discord) để sử dụng trong thực tế.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **1. Tích Hợp Với Slack/Telegram**
- Sử dụng **node `slack`** hoặc **`telegram`** để nhận tin nhắn từ các ứng dụng chat.
- **Cấu hình webhook** trong Slack/Telegram để gửi tin nhắn vào workflow.

### **2. Lưu Log Hoạt Động**
- Thêm **node `set`** để lưu lịch sử chat vào một file CSV hoặc database.
- **Lưu ý:** Có thể sử dụng **Google Sheets** hoặc **Airtable** để theo dõi.

### **3. Gửi Báo Cáo Định Kỳ**
- Sử dụng **node `schedule`** để chạy workflow hàng ngày/tuần và gửi báo cáo về các skill đã tạo/thực thi.
- **Ví dụ:** Gửi email báo cáo qua **Gmail API** hoặc **SendGrid**.

### **4. Cập Nhật Tài Liệu Tự Động**
- **Node `Context7`** sẽ tự động lấy tài liệu mới nhất, nhưng có thể **cập nhật API key** định kỳ để tránh lỗi.

### **5. Tạo Nhiều Skill Đồng Thời**
- Sử dụng **node `set`** để lưu trữ danh sách skill đang được tạo và **node `queue`** để quản lý thứ tự.

---
## **📌 Kết Luận: Áp Dụng Ngay Hôm Nay!**

Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa việc tạo và thực thi skill AI** một cách hiệu quả, **không cần viết một dòng code**. Bằng cách tích hợp **Anthropic, OpenAI, GitHub và Context7**, các sếp có thể:
✔ **Tiết kiệm thời gian** lên đến 80% so với cách làm thủ công.
✔ **Cập nhật logic AI tự động** khi có tài liệu mới.
✔ **Hoạt động 24/7** mà không cần can thiệp của con người.

**Hành động ngay hôm nay:**
1. **Import workflow** và cấu hình các node theo hướng dẫn.
2. **Test với một skill mẫu** và kiểm tra kết quả.
3. **Kết nối với chatbot** để sử dụng trong dự án thực tế.

**🚀 Cần hỗ trợ thêm?** Đăng ký **VPS n8n** từ [TinoHost](https://tino.vn/vps-n8n?affid=388) để workflow chạy ổn định 24/7!

---
**🎥 Xem video hướng dẫn chi tiết từ tác giả Davide Boizza:**
👉 [YouTube Channel của Davide](https://youtube.com/@n3witalia) – Đăng ký để nhận các template tự động hóa miễn phí!