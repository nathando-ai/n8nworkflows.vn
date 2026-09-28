---
title: "🤖 **Tự Động Hóa Chatbot AI Telegram Với Chức Năng Giao Đổi Sang Người - Sẵn Sàng Sản Xuất!**"
description: "Workflow này xây dựng một chatbot Telegram AI thông minh, tích hợp trí tuệ nhân tạo (GPT-4o-mini) và khả năng chuyển giao tự động sang nhân viên khi cần thiết. Giải pháp hoàn toàn không cần code, hoạt động 24/7, và đảm bảo không có lỗi giao tiếp giữa bot và người dùng."
slug: "chatbot-telegram-ai-human-takeover"
tags: [n8n, automation, no-code, chatbot-ai, telegram-bot, trilox, gpt-4o-mini]
keywords: [n8n workflow telegram chatbot, tự động hóa hỗ trợ khách hàng, chatbot AI với giao tiếp người, GPT-4o-mini, Trilox, tự động hóa hỗ trợ khách hàng 24/7]
---

# 🚀 **Chatbot Telegram AI Với Chức Năng Giao Đổi Sang Người - Giải Pháp Tự Động Hóa Hỗ Trợ Khách Hàng Mới**

Hiện nay, các doanh nghiệp thường phải đối mặt với những thách thức như:
- **Thời gian phản hồi chậm** khi khách hàng gửi tin nhắn vào ban đêm hoặc cuối tuần.
- **Rủi ro sai sót** của bot khi trả lời sai hoặc không hiểu được yêu cầu phức tạp của khách.
- **Không thể cá nhân hóa** trong các trường hợp đặc biệt như yêu cầu hoàn tiền, khiếu nại, hoặc vấn đề phức tạp.

Workflow này **giải quyết tất cả những vấn đề trên** bằng cách kết hợp **AI GPT-4o-mini** với **hệ thống quản lý hỗ trợ khách hàng Trilox**, cho phép:
✅ **Trả lời tự động** cho 90% các câu hỏi thông thường.
✅ **Chuyển giao tự động** sang nhân viên khi AI không chắc chắn hoặc yêu cầu đặc biệt.
✅ **Không có lỗi giao tiếp** giữa bot và người dùng (không double reply).
✅ **Hoạt động liên tục** 24/7 mà không cần can thiệp thủ công.

---
## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian** cho đội ngũ hỗ trợ: Bot xử lý 90% các câu hỏi đơn giản, chỉ chuyển giao những trường hợp phức tạp.
- **Trải nghiệm khách hàng tốt hơn**: Khách hàng luôn nhận được phản hồi nhanh chóng, ngay cả khi nhân viên đang offline.
- **Chính xác và chuyên nghiệp**: AI được huấn luyện với hệ thống quy tắc rõ ràng, giảm thiểu sai sót.
- **Dễ dàng mở rộng**: Hoạt động trên Telegram, có thể kết nối thêm WhatsApp, Messenger, Instagram, hoặc Widget trong tương lai.
- **Dữ liệu theo dõi toàn diện**: Tất cả cuộc trò chuyện được ghi lại trong **Trilox**, giúp phân tích và cải thiện dịch vụ.
:::

---
## 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Trilox** (miễn phí tại [trilox.io](https://trilox.io)):
   - Tạo **Project** → **App (Inbox)** → **API Key**.
2. **Bot Telegram** (tạo tại [@BotFather](https://t.me/botfather)):
   - Lấy **API Token** để kết nối với n8n.
3. **API Key OpenAI** (hoặc các provider khác như OpenRouter, Anthropic):
   - Để sử dụng mô hình **GPT-4o-mini** cho AI Agent.
4. **n8n Self-hosted** (khuyến nghị cài trên VPS để hoạt động 24/7):
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
5. **Node Trilox cho n8n** (cần cài đặt trước khi import workflow):
   - Tải tại [n8n-nodes-trilox](https://github.com/trilox/n8n-nodes-trilox).
:::

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/13394](https://n8n.io/workflows/13394) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON từ file và dán vào **Import Workflow** trong n8n.

:::note[LƯU Ý]
- **Không** có thể import trực tiếp từ link trên n8n.io (do yêu cầu node Trilox).
- Sau khi import, **không kích hoạt workflow ngay** mà phải cấu hình các node quan trọng trước.
:::

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

#### **A. Cấu Hình Credentials**
Tất cả các node sử dụng **Trilox** và **Telegram** đều yêu cầu **credentials** được thiết lập trước:
1. **Trilox Credentials**:
   - Trong **n8n Credentials**, thêm **Trilox API Key** (từ [trilox.io](https://trilox.io)).
   - Trong các node **Trilox**, chọn **App (Inbox)** tương ứng từ danh sách dropdown.
2. **Telegram Credentials**:
   - Thêm **Telegram Bot Token** (từ [@BotFather](https://t.me/botfather)).
3. **OpenAI Credentials**:
   - Thêm **OpenAI API Key** và chọn mô hình **gpt-4o-mini**.

#### **B. Cấu Hình AI Agent (Prompt)**
- Node **"AI Agent"** sử dụng **LangChain Agent** kết hợp với **Structured Output Parser**.
- **Cần chỉnh sửa system prompt** để phù hợp với nghiệp vụ của doanh nghiệp:
  - Ví dụ: Thêm **FAQ**, **quy tắc chuyển giao sang người**, hoặc **danh sách sản phẩm**.
  - **Cấu trúc output phải theo định dạng JSON**:
    ```json
    {
      "message": "Trả lời của bot",
      "is_human_required": true/false
    }
    ```
- **Lưu ý**: Nếu `is_human_required: true`, workflow sẽ tự động chuyển giao sang nhân viên.

#### **C. Cấu Hình Handler (Quản Lý Trạng Thái)**
- Node **"Check Handler (Pre-Bot)"** và **"Check Handler (Post-Bot)"** kiểm tra trạng thái cuộc trò chuyện:
  - `bot`: Bot tiếp tục trả lời.
  - `awaiting_human`: Bot gửi tin nhắn "Đang chuẩn bị trả lời".
  - `assigned_human`: Bot im lặng, chờ nhân viên phản hồi.
- **Nếu AI trả lời sai hoặc chậm**, hệ thống sẽ tự động chuyển giao sang người.

#### **D. Cấu Hình Voice Message (Nếu Có)**
- Nếu muốn hỗ trợ **tin nhắn giọng nói**:
  - Node **"Download Voice File"** và **"Transcribe Voice Message"** cần **OpenAI API Key**.
  - Nếu không cần, có thể **xóa nhánh voice** và kết nối trực tiếp từ **"Message Type Router"** → **"Merge Text Input"**.

#### **E. Cấu Hình Escalation (Chuyển Giao Sang Người)**
- Node **"Escalate to Human"** sẽ gửi yêu cầu chuyển giao sang **Trilox Inbox**.
- Nhân viên sẽ nhận được cuộc trò chuyện và có thể **gửi tin nhắn trực tiếp** cho khách hàng thông qua Telegram.

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Gửi tin nhắn **"Hi, what are your hours?"** đến bot Telegram.
   - Kiểm tra trong **Trilox Inbox** xem bot có trả lời đúng không.
2. **Kích hoạt workflow**:
   - Đảm bảo tất cả credentials đã cấu hình đúng.
   - Bật **Active** và theo dõi log trong n8n.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **1. Tối Ưu Hóa Prompt cho AI**
- **Thêm quy tắc chuyển giao**:
  - Ví dụ: `is_human_required: true` khi khách hàng yêu cầu **hoàn tiền**, **khiếu nại**, hoặc **câu hỏi phức tạp**.
- **Cập nhật FAQ**:
  - Thêm các câu hỏi thường gặp của khách hàng vào system prompt để AI trả lời chính xác hơn.

### **2. Kết Nối Với Các Channel Khác**
Workflow hiện chỉ hỗ trợ **Telegram**, nhưng có thể mở rộng sang:
- **WhatsApp**: Thay thế node **Telegram Trigger** bằng **WhatsApp Trigger**.
- **Messenger**: Sử dụng node **Facebook Messenger**.
- **Instagram**: Kết nối với API Instagram.
- **Widget**: Hỗ trợ trên website.

**Cách làm**:
- Thêm node **Channel Router** và cấu hình cho từng channel.
- Sử dụng **placeholder outputs** trong workflow để kết nối dễ dàng.

### **3. Ghi Log & Báo Cáo**
- **Ghi lại tất cả cuộc trò chuyện** trong **Trilox** để phân tích.
- **Tạo báo cáo tự động** hàng tuần/month bằng node **Google Sheets** hoặc **Notion**.
- **Gửi báo cáo định kỳ** cho quản lý qua **Email** hoặc **Slack**.

### **4. Cài Đặt Thông Báo Cho Nhân Viên**
- Khi có cuộc trò chuyện mới được chuyển giao, gửi **thông báo Slack/Telegram** cho nhân viên:
  ```json
  {
    "text": "Có cuộc trò chuyện mới cần hỗ trợ: {{customer_name}}",
    "channel": "#support"
  }
  ```

---
## 📌 **Kết Luận**
Workflow này không chỉ **giải phóng đội ngũ hỗ trợ** khỏi việc trả lời các câu hỏi đơn giản, mà còn **cải thiện trải nghiệm khách hàng** bằng cách đảm bảo phản hồi nhanh chóng và chuyên nghiệp. Với **chức năng chuyển giao tự động sang người**, doanh nghiệp có thể **giảm thiểu rủi ro sai sót** và **tăng cường sự tin tưởng** của khách hàng.

**Hành động ngay hôm nay**:
1. **Cài đặt n8n trên VPS** (để workflow hoạt động 24/7).
2. **Import workflow** và cấu hình credentials.
3. **Test với tin nhắn mẫu** và điều chỉnh prompt AI.
4. **Kích hoạt và theo dõi** kết quả!

👉 **Cần hỗ trợ kỹ thuật?** Hãy tham gia **Discord Trilox**: [discord.gg/g9e6YTqmUs](https://discord.gg/g9e6YTqmUs).

---
**Chúc các sếp thành công với chatbot AI hoàn hảo của mình!** 🎉