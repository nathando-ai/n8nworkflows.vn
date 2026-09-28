---
title: "🤖 Tự Động Hóa Trả Lời AI Khi Được Nhắc Đến Trong Liveblocks (Không Cần Code)"
description: "Workflow tự động hóa trả lời AI khi người dùng nhắc đến '@AI Assistant' trong Liveblocks Comments, giúp hỗ trợ khách hàng 24/7 với phản hồi thông minh và cá nhân hóa. Giảm thiểu thời gian phản hồi từ giờ đến giây!"
slug: "tieu-dong-hoa-tra-loi-ai-liveblocks"
tags: [n8n, automation, no-code, liveblocks, ai-chatbot, support-chatbot]
keywords: [n8n workflow liveblocks, tự động hóa trả lời AI, chatbot hỗ trợ khách hàng, liveblocks comments, AI agent n8n]
---

# 🚀 **Tự Động Hóa Trả Lời AI Khi Được Nhắc Đến Trong Liveblocks (Không Cần Code)**

### **Giải Pháp Cho Nỗi Đau:**
Các sếp đang phải **phản hồi hàng trăm tin nhắn trong Liveblocks Comments** mỗi ngày? Hoặc **khách hàng phải chờ lâu** để được hỗ trợ? Với workflow này, **AI sẽ tự động trả lời** khi được nhắc đến (`@AI Assistant`), giúp tiết kiệm **tối thiểu 80% thời gian phản hồi** và nâng cao **trải nghiệm khách hàng** với phản hồi **cá nhân hóa và thông minh**!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian:** AI tự động trả lời thay vì các sếp phải làm thủ công.
✅ **Phản hồi tức thời:** Khách hàng nhận được trợ giúp **trong vòng vài giây** khi nhắc đến `@AI Assistant`.
✅ **Cá nhân hóa:** AI hiểu **bối cảnh toàn bộ cuộc trò chuyện** trước khi trả lời.
✅ **Hoạt động 24/7:** Không cần người hỗ trợ trực tiếp, hệ thống hoạt động **mọi lúc mọi nơi**.
✅ **Tăng trải nghiệm khách hàng:** Phản hồi **chuyên nghiệp và thông minh** làm tăng độ tin tưởng.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Liveblocks** (đăng ký tại [liveblocks.io](https://liveblocks.io/)).
2. **API Key Liveblocks** (tạo trong **Liveblocks Dashboard** → **Settings** → **API Keys**).
3. **Webhook Signing Secret** (tạo trong **Liveblocks Dashboard** → **Webhooks**).
4. **API Key Anthropic** (đăng ký tại [anthropic.com](https://www.anthropic.com/) để sử dụng mô hình **Claude Sonnet 4.6**).
5. **Ứng dụng Liveblocks Comments** (cài đặt từ [Next.js Comments Example](https://liveblocks.io/examples/comments/nextjs-comments)).
6. **Cổng webhook** (sử dụng `localtunnel` hoặc `ngrok` để expose URL).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Bước 1:** Tải workflow từ [n8n.io/workflows/14299](https://n8n.io/workflows/14299) hoặc copy JSON từ trang này.
- **Bước 2:** Mở **n8n Editor**, nhấn **Import Workflow** và dán JSON vào.
- **Bước 3:** Chọn **Active** để kích hoạt workflow.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này gồm **7 node chính**, các sếp cần cấu hình **cẩn thận** các node sau:

##### **🔹 Node 1: Liveblocks Trigger (CUSTOM.liveblocksTrigger)**
- **Credentials:** Điền `liveblocksWebhookSigningSecretApi` (từ Liveblocks Dashboard).
- **Lưu ý:**
  - Webhook phải **lắng nghe sự kiện `commentCreated`**.
  - **Expose URL** bằng `localtunnel` hoặc `ngrok` (ví dụ: `https://your-subdomain.loca.lt/webhook/...`).
  - **Cập nhật URL** trong Liveblocks Dashboard.

##### **🔹 Node 2 & 3: Get a Comment & Get a Thread (CUSTOM.liveblocks)**
- **Credentials:** Điền `liveblocksApi` (từ Liveblocks Dashboard).
- **Key Parameters:**
  - `operation`: `getComment` (node 2) và `getThread` (node 3).
  - **Lưu ý:** Đảm bảo **secret key** trong ứng dụng Liveblocks **khớp** với API Key trong n8n.

##### **🔹 Node 4: If (n8n-nodes-base.if)**
- **Điều kiện:** Kiểm tra xem comment có nhắc đến `@AI Assistant` (ID: `"__AI_AGENT"`) không.
- **Lưu ý:** Nếu không nhắc đến, workflow **dừng lại** (không tạo phản hồi).

##### **🔹 Node 5: AI Agent (@n8n/n8n-nodes-langchain.agent)**
- **Lưu ý:**
  - AI sẽ **hiểu toàn bộ bối cảnh** của thread trước khi trả lời.
  - **Prompt mặc định** đã được tối ưu, nhưng các sếp có thể **cập nhật** để phù hợp với brand.

##### **🔹 Node 6: Anthropic Chat Model (lmChatAnthropic)**
- **Credentials:** Điền `anthropicApi` (từ Anthropic).
- **Model:** Chọn `claude-sonnet-4-6` (mô hình mạnh nhất hiện tại).
- **Lưu ý:**
  - Nếu không đủ credit, **cập nhật API Key** mới.
  - **Giám sát chi phí** vì mô hình này có thể tốn kém.

##### **🔹 Node 7: Create a Comment (CUSTOM.liveblocks)**
- **Credentials:** Điền `liveblocksApi` (giống node 2 & 3).
- **Lưu ý:**
  - **User ID** của AI phải là `"__AI_AGENT"` (đã được cấu hình trong ứng dụng Liveblocks).
  - **Kiểm tra** phản hồi AI có xuất hiện trong ứng dụng không.

#### **3. Kích Hoạt ⚡️**
- **Test Run:** Nhấn **Run Workflow** với một comment mẫu nhắc đến `@AI Assistant`.
- **Kiểm tra:** Phản hồi AI có xuất hiện trong ứng dụng không?
- **Active:** Nếu test thành công, **bật Active** để workflow hoạt động tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết nối với Slack/Telegram:**
   - Sử dụng **node `n8n-nodes-base.slack`** để thông báo khi AI trả lời.
   - Ví dụ: `Gửi tin nhắn Slack: "AI đã trả lời comment #<ID> trong Liveblocks!"`

2. **Lưu Log & Báo Cáo:**
   - Sử dụng **node `n8n-nodes-base.googleSheets`** để ghi lại tất cả các cuộc trò chuyện AI.
   - **Tích hợp với Google Analytics** để theo dõi hiệu suất.

3. **Cập Nhật Prompt AI:**
   - Nếu AI trả lời không phù hợp, **cập nhật prompt** trong node `AI Agent` để phù hợp với brand.
   - Ví dụ: `"Trả lời ngắn gọn, chuyên nghiệp, và luôn nhắc đến sản phẩm của chúng tôi."`

4. **Bật Tích Lộp Cho AI:**
   - Sử dụng **node `n8n-nodes-base.if`** để **lọc ra các câu hỏi phức tạp** và chuyển cho nhân viên hỗ trợ.

5. **Dùng AI để Tự Cập Nhật Bối Cảnh:**
   - Thêm **node `n8n-nodes-base.httpRequest`** để AI **tải thêm thông tin** từ API sản phẩm trước khi trả lời.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc phản hồi tin nhắn Liveblocks thủ công, đồng thời **nâng cao chất lượng hỗ trợ khách hàng** với phản hồi **tức thời và thông minh**. **Chỉ cần 10 phút setup**, các sếp đã có một **AI trợ lý 24/7** hoạt động trong ứng dụng!

**🚀 Hãy áp dụng ngay và trải nghiệm sự khác biệt!**
Nếu có vấn đề, **hãy comment bên dưới** hoặc liên hệ với Liveblocks/n8n Community để hỗ trợ.

---
**#TựĐộngHóa #AIChatbot #Liveblocks #n8n #HỗTrợKháchHàng**