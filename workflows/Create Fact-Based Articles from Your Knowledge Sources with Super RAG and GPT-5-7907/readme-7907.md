---
title: "🚀 Tự Động Hóa Viết Bài Văn Bản Chuyên Nghiệp Đơn Giản Với Super RAG + GPT-5 (Không Cần Code)"
description: "Workflow tự động hóa viết bài báo, bài viết chuyên nghiệp dựa trên cơ sở tri thức riêng của doanh nghiệp, kết hợp công nghệ RAG và GPT-5 để đảm bảo độ chính xác cao và nội dung độc quyền. Giúp tiết kiệm thời gian nghiên cứu lên đến 90% so với cách viết thủ công."
slug: "tieu-dong-hoa-viet-bai-van-ban-chuyen-nghiep-su-per-rag-gpt-5"
tags: [n8n, automation, ai-rag, gpt-5, content-creation, no-code]
keywords: [n8n workflow viết bài, tự động hóa viết báo, RAG AI, GPT-5 tự động, viết bài chuyên nghiệp không code]
---

# 🚀 **Tự Động Hóa Viết Bài Văn Bản Chuyên Nghiệp Với Super RAG + GPT-5 (Không Cần Code)**

### **Giải pháp cho những người sợ viết bài dài, mất nhiều thời gian nghiên cứu, hoặc không chắc chắn về độ chính xác của thông tin?**
Hãy tưởng tượng một hệ thống AI tự động **tách nhỏ chủ đề**, **tìm kiếm và tổng hợp thông tin từ cơ sở tri thức riêng của doanh nghiệp**, và **viết bài hoàn chỉnh** với nguồn gốc dữ liệu minh bạch. Đó chính là **Workflow "AI Article Writer Based on Your Knowledge Base"** của n8n, kết hợp công nghệ **Super RAG** và **GPT-5** để tạo ra nội dung chuyên nghiệp, độc quyền, và **100% dựa trên dữ liệu của bạn**.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng. Với chi phí thấp nhưng hiệu suất cao, các sếp có thể lựa chọn:
👉 **[VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 **[VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ xử lý nhanh cho AI)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian nghiên cứu lên đến 90%** so với cách viết thủ công.
- **Nội dung 100% độc quyền** vì dựa trên cơ sở tri thức riêng của doanh nghiệp (không sao chép từ nguồn mở).
- **Độ chính xác cao** nhờ công nghệ **RAG (Retrieval-Augmented Generation)**, tránh sai sót thông tin.
- **Cá nhân hóa hoàn toàn** theo yêu cầu của từng bài viết (định dạng, độ dài, phong cách).
- **Hoạt động liên tục** 24/7, không cần can thiệp của con người.
- **Nguồn gốc dữ liệu minh bạch** với liên kết trực tiếp đến tài liệu gốc (Notion, Google Drive,...).
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Super.com** (để sử dụng công nghệ RAG và Super Assistant):
   - [Đăng ký tài khoản Super](https://super.com/) (miễn phí cho phiên bản cơ bản).
   - **API Token** và **Assistant ID** của Super Assistant (cần thiết để kết nối với workflow).
2. **Tài khoản OpenAI** (để sử dụng GPT-5):
   - [Đăng ký OpenAI](https://platform.openai.com/) và lấy **API Key**.
3. **Cơ sở tri thức riêng** (đã được upload vào Super Assistant):
   - Tài liệu từ **Notion**, **Google Drive**, **PDF**, hoặc bất kỳ nguồn nào được hỗ trợ bởi Super.
4. **Workflow n8n** (self-hosted hoặc dùng phiên bản cloud miễn phí).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải workflow gốc** từ [đây](https://n8n.io/workflows/7907) (nếu muốn).
- **Nhấn "Import"** trong n8n Editor và dán JSON vào.

:::note[Lưu ý]
Nếu sử dụng phiên bản **cloud miễn phí**, các sếp nên **self-host** để tránh giới hạn node và API call.
:::

---

### **2. Các bước cấu hình BẮT BUỘC phải chỉnh 📌**

#### **A. Kết nối Super.com và OpenAI**
1. **Tạo Super Assistant**:
   - Đăng nhập vào [Super.com](https://super.com/).
   - Tạo một **Assistant mới** và upload cơ sở tri thức (tài liệu Notion, Google Drive,...).
   - Lấy **API Token** và **Assistant ID** từ trang quản lý Assistant.

2. **Cấu hình node "Query Super Assistant"**:
   - Mở node **"Query Super Assistant"** (type: `httpRequest`).
   - Điền vào:
     - **URL**: `https://api.super.com/v1/assistant/{ASSISTANT_ID}/run`
     - **Headers**:
       - `Authorization`: `Bearer {SUPER_API_TOKEN}`
       - `Content-Type`: `application/json`
     - **Body (JSON)**:
       ```json
       {
         "input": "$$.json["question"]"
       }
       ```

#### **B. Cấu hình LLM (GPT-5)**
1. **Node "GPT 5 mini" và "GPT 5 chat"**:
   - Mở node **"GPT 5 mini"** (type: `lmChatOpenAi`).
   - Điền **API Key OpenAI** vào phần **Credentials**.
   - Chọn model: `gpt-5-mini` (hoặc `gpt-5-chat-latest` nếu muốn sử dụng phiên bản mới nhất).
   - **Prompt mặc định** đã được tối ưu hóa, các sếp chỉ cần đảm bảo **API Key** đúng.

2. **Node "New content - generate research questions"**:
   - Đây là node **ChainLLM** để phân tích chủ đề và tạo ra các câu hỏi nghiên cứu.
   - **Prompt mặc định** đã được thiết kế để tự động hóa quá trình này.
   - Các sếp có thể **cập nhật prompt** nếu muốn thay đổi cách phân tích chủ đề.

#### **C. Cấu hình Form Trigger**
1. **Node "New article form"**:
   - Đây là **form nhập liệu** để người dùng (hoặc các sếp) nhập:
     - **Tiêu đề bài viết**.
     - **Yêu cầu cụ thể** (ví dụ: "Viết bài về SEO năm 2025, định dạng 2000 từ").
   - Các sếp có thể **cập nhật trường nhập liệu** theo nhu cầu.

2. **Node "Prepare form values"**:
   - Node này **tạo ra cấu trúc dữ liệu** cho các node tiếp theo.
   - **Không cần chỉnh sửa** trừ khi muốn thay đổi cách xử lý dữ liệu.

#### **D. Node "Structured Output Parser"**
- Node này **định dạng kết quả** từ GPT-5 thành cấu trúc dễ đọc.
- **Không cần chỉnh sửa** trừ khi muốn thay đổi định dạng output.

---

### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **"Run"** trên node **"New article form"** và nhập một **tiêu đề mẫu** (ví dụ: "Tự động hóa nội dung marketing").
   - Kiểm tra kết quả ở node **"Article result"** để đảm bảo workflow hoạt động.

2. **Bật Active**:
   - Sau khi test thành công, **bật Active** cho workflow.

---

## ✍️ **Mẹo & gợi ý nâng cao**

### **1. Kết hợp với Slack/Telegram để thông báo kết quả**
- Thêm node **Slack** hoặc **Telegram** vào cuối workflow để **gửi kết quả bài viết** ngay khi hoàn thành.
- Ví dụ:
  ```json
  {
    "operation": "sendMessage",
    "text": "📝 Bài viết mới đã hoàn thành: {{ $node["Article result"].json["title"] }}"
  }
  ```

### **2. Lưu log và báo cáo định kỳ**
- Thêm node **Google Sheets** hoặc **Notion** để **lưu lịch sử bài viết**.
- Ví dụ:
  - Node **Google Sheets**: Thêm dữ liệu vào sheet với cột: `Tiêu đề`, `Ngày tạo`, `Độ dài`, `Link tài liệu gốc`.

### **3. Tối ưu prompt cho từng ngành nghề**
- Nếu viết bài về **y tế**, **kinh doanh**, hoặc **công nghệ**, các sếp có thể **cập nhật prompt** trong node **ChainLLM** để phù hợp với lĩnh vực.
- Ví dụ:
  ```plaintext
  "Viết bài về [chủ đề] với phong cách chuyên nghiệp, sử dụng dữ liệu từ cơ sở tri thức của chúng tôi, và đảm bảo có liên kết trực tiếp đến nguồn gốc."
  ```

### **4. Sử dụng cache để tiết kiệm API call**
- Node **GPT 5 mini** và **GPT 5 chat** đã được cấu hình **cache**, nhưng các sếp có thể **tăng thời gian cache** (ví dụ: 1 ngày) để giảm chi phí.

---

## 📌 **Kết luận**
Workflow **"AI Article Writer Based on Your Knowledge Base"** là **giải pháp hoàn hảo** cho các sếp muốn:
✅ **Tiết kiệm thời gian** viết bài và nghiên cứu.
✅ **Đảm bảo độ chính xác** với dữ liệu từ cơ sở tri thức riêng.
✅ **Tự động hóa hoàn toàn** quá trình viết nội dung chuyên nghiệp.

**Hành động ngay hôm nay!**
1. **Self-host n8n** trên VPS để tránh giới hạn.
2. **Import workflow** và cấu hình Super + OpenAI.
3. **Test với một bài viết mẫu** và bắt đầu tự động hóa nội dung của doanh nghiệp!

---
**🚀 Cần hỗ trợ thêm?** Các sếp có thể tham khảo [hướng dẫn chi tiết của Guillaume Duvernay](https://n8n.io/workflows/7907) hoặc liên hệ với cộng đồng n8n trên [Discord](https://n8n.io/discord).