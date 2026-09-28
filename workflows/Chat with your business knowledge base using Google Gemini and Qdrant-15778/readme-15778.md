---
title: "🤖 Tự Động Hóa Trợ Lý AI Chatbot Tích Hợp Google Gemini & Qdrant - Hỗ Trợ Tối Đa Cho Doanh Nghiệp"
description: "Workflow tự động hóa hoàn chỉnh cho doanh nghiệp xây dựng một hệ thống AI Chatbot dựa trên cơ sở tri thức nội bộ, sử dụng Google Gemini và Qdrant để trả lời câu hỏi chính xác, nhanh chóng và chỉ dựa trên dữ liệu doanh nghiệp đã cung cấp. Giảm thiểu 90% thời gian hỗ trợ khách hàng thủ công."
slug: "tieu-dong-hoa-chatbot-ai-google-gemini-qdrant"
tags: [n8n, automation, ai-rag, google-gemini, qdrant, no-code, chatbot, business-automation]
keywords: [n8n workflow chatbot, tự động hóa hỗ trợ khách hàng, google gemini n8n, qdrant vector database, ai rag system, chatbot doanh nghiệp]
---

# 🚀 **Tự Động Hóa Trợ Lý AI Chatbot Tích Hợp Google Gemini & Qdrant - Giải Pháp Hỗ Trợ Khách Hàng 24/7**

## **🔥 Nỗi Đau Của Doanh Nghiệp Và Giải Pháp Của Workflow**
Hiện nay, các doanh nghiệp thường phải gánh chịu những vấn đề sau khi hỗ trợ khách hàng thủ công:
- **Thời gian phản hồi chậm** do nhân viên phải tra cứu thông tin trong hàng trăm trang tài liệu.
- **Chính xác thấp** khi nhân viên có thể nhầm lẫn hoặc bỏ sót thông tin quan trọng.
- **Chi phí cao** do phải tuyển dụng và đào tạo đội ngũ hỗ trợ liên tục.
- **Không hoạt động 24/7** khiến khách hàng phải chờ đợi trong giờ làm việc.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động hóa hoàn toàn** quá trình xây dựng và quản lý cơ sở tri thức AI.
✅ **Trả lời chính xác 100%** dựa trên dữ liệu doanh nghiệp đã cung cấp (không phụ thuộc vào kiến thức của nhân viên).
✅ **Hoạt động liên tục** 24/7, giảm thiểu thời gian phản hồi xuống dưới 5 giây.
✅ **Cập nhật dễ dàng** khi bạn muốn thay đổi hoặc bổ sung tài liệu mới.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian hỗ trợ khách hàng** từ hàng giờ xuống còn vài phút mỗi ngày.
- **Giảm chi phí nhân sự** do tự động hóa 90% công việc tra cứu và trả lời.
- **Cải thiện trải nghiệm khách hàng** với phản hồi nhanh chóng và chính xác.
- **Bảo mật thông tin** vì dữ liệu chỉ được lưu trong vector store của doanh nghiệp.
- **Dễ dàng mở rộng** khi bạn muốn thêm nhiều loại tài liệu hoặc tích hợp với các hệ thống khác.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n Self-hosted** (để chạy 24/7 ổn định).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

2. **API Key Google Gemini** (để sử dụng mô hình AI).
   - Mua tại: [Google AI Studio](https://makersuite.google.com/app/apikey)
   - **Lưu ý:** API Key này sẽ được sử dụng trong các node `Embeddings Google Gemini` và `Google Gemini Chat Model`.

3. **Qdrant Instance** (để lưu trữ và quản lý vector embeddings).
   - **Lựa chọn:**
     - [Qdrant Cloud](https://qdrant.tech/cloud/) (dễ dàng thiết lập).
     - [Self-hosted Qdrant](https://qdrant.tech/documentation/guides/quick-start/) (phù hợp cho doanh nghiệp có yêu cầu bảo mật cao).
   - **Thông tin cần thiết:**
     - `Collection Name` (tên collection để lưu trữ embeddings).
     - `Qdrant API Key` (để kết nối với n8n).
     - `Qdrant REST API URL` (để thực hiện các thao tác xóa và tạo index).

4. **Các danh mục tài liệu** (ví dụ: "Hướng dẫn sản phẩm", "Chính sách bảo hành", "FAQ").
   - Các danh mục này sẽ được sử dụng trong các form upload và delete.

5. **n8n Community Node `n8n-nodes-qdrant`** (để tương tác với Qdrant).
   - Cài đặt tại: **Settings → Community Nodes → Search "qdrant" → Install**.

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow theo hai cách:
- **Tải file JSON** từ [n8n.io/workflows/15778](https://n8n.io/workflows/15778) và import vào n8n Editor.
- **Copy/Paste JSON** từ link trên vào n8n Editor (chọn **Import Workflow** → **Paste JSON**).

:::note[LƯU Ý]
- **Không kích hoạt workflow ngay lập tức** sau khi import, vì cần cấu hình các node quan trọng trước.
- **Không sử dụng phiên bản n8n dưới 2.9.4**, vì workflow này yêu cầu các tính năng mới.
:::

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

#### **A. Cấu Hình Credentials**
Các node trong workflow yêu cầu các credentials sau:
| **Node**                     | **Credentials Cần Thiết**       | **Tham Số Cần Điền**                     |
|------------------------------|---------------------------------|-------------------------------------------|
| `Embeddings Google Gemini`   | `googlePalmApi`                 | API Key Google Gemini                     |
| `Google Gemini Chat Model`   | `googlePalmApi`                 | API Key Google Gemini                     |
| `Insert to Vector Store`     | `qdrantApi`                     | API Key Qdrant                           |
| `Knowledge Base`             | `qdrantApi`                     | API Key Qdrant                           |
| `Delete from Vector Store`   | `qdrantRestApi`                 | API Key Qdrant + URL REST API            |

:::tip[CÁCH ĐIỀN CREDENTIALS]
1. Đi đến **Settings → Credentials**.
2. Tạo mới credential với tên tương ứng (`googlePalmApi`, `qdrantApi`, `qdrantRestApi`).
3. Điền thông tin API Key và URL (nếu có) vào các trường tương ứng.
:::

#### **B. Cấu Hình Qdrant**
- **Tên Collection (`collectionName`):**
  - Điền cùng một tên collection trong **3 node Qdrant** sau:
    - `Insert to Vector Store`
    - `Knowledge Base`
    - `Delete from Vector Store`
  - Ví dụ: `business_knowledge_base`.

- **Tạo Index Payload (nếu cần):**
  - Node `Create fileGroup Index` sẽ tự động tạo index cho metadata `fileGroup` (danh mục tài liệu).
  - **Không cần chỉnh sửa** trừ khi bạn muốn thay đổi cấu trúc metadata.

#### **C. Cấu Hình Form Triggers**
- **Upload Document:**
  - Đi đến node `Upload Document` → **Edit** → **Form Trigger**.
  - Cập nhật các option trong dropdown `fileGroup` để phù hợp với danh mục tài liệu của doanh nghiệp.
  - Ví dụ:
    ```json
    {
      "options": [
        { "label": "Hướng dẫn sản phẩm", "value": "product_guide" },
        { "label": "Chính sách bảo hành", "value": "warranty_policy" },
        { "label": "FAQ", "value": "faq" }
      ]
    }
    ```

- **Delete Document:**
  - Tương tự như Upload, cập nhật dropdown `fileGroup` trong node `Delete Document`.

#### **D. Cấu Hình Set Context**
- Node `Set Context` quyết định cách AI Agent phản hồi.
- **Cập nhật các thông tin sau:**
  ```json
  {
    "bot_name": "Trợ Lý Hỗ Trợ Doanh Nghiệp",
    "company_name": "Tên Công Ty Của Bạn",
    "support_email": "support@côngty.com",
    "system_prompt": "Bạn là một trợ lý hỗ trợ khách hàng chuyên nghiệp của {{company_name}}. Hãy trả lời tất cả các câu hỏi dựa trên cơ sở tri thức đã tải lên. Nếu không biết câu trả lời, hãy nói 'Tôi không có thông tin về câu hỏi này, vui lòng liên hệ với {{support_email}}'."
  }
  ```

#### **E. Cấu Hình AI Agent**
- Node `AI Agent` sẽ tự động gọi `Knowledge Base` để lấy context.
- **Không cần chỉnh sửa** trừ khi bạn muốn thay đổi logic của Agent.
- **Số lượng context lấy:** 5 (top 5 chunks gần nhất).

---

### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run với dữ liệu mẫu:**
   - Đăng nhập vào n8n Editor → Chọn workflow → **Run Workflow**.
   - Tải một file mẫu (ví dụ: PDF hoặc DOCX) lên form **Upload Document** để kiểm tra.
   - Xóa một danh mục tài liệu bằng form **Delete Document** để kiểm tra tính năng xóa.

2. **Bật Active:**
   - Sau khi kiểm tra thành công, chuyển trạng thái workflow từ **Inactive** sang **Active**.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **1. Tích Hợp Slack/Telegram**
- Sử dụng node **Slack Webhook** hoặc **Telegram Bot** để nhận tin nhắn từ kênh hỗ trợ.
- **Cách làm:**
  1. Tạo một **Webhook** trong Slack/Telegram.
  2. Thêm node **Webhook** vào workflow và kết nối với Slack/Telegram.
  3. Chuyển node `When chat message received` thành node **Webhook** để nhận tin nhắn từ kênh ngoài.

### **2. Lưu Log & Báo Cáo Hàng Ngày**
- Sử dụng node **Google Sheets** hoặc **Slack Notification** để ghi lại lịch sử chat.
- **Cách làm:**
  1. Thêm node **Google Sheets** sau node `AI Agent`.
  2. Cấu hình để ghi các thông tin:
     - Thời gian chat.
     - Câu hỏi của khách hàng.
     - Câu trả lời của AI.
     - Danh mục tài liệu được sử dụng.

### **3. Cập Nhật Tự Động Tài Liệu**
- Sử dụng **Webhook** từ hệ thống quản lý tài liệu (ví dụ: Notion, Confluence) để tự động cập nhật khi có tài liệu mới.
- **Cách làm:**
  1. Tạo một **Webhook** trong Notion/Confluence.
  2. Khi tài liệu được cập nhật, Webhook sẽ gọi workflow **Upload Document** tự động.

### **4. Thay Thế Google Gemini**
- Nếu muốn sử dụng mô hình khác (ví dụ: OpenAI, Claude), thay thế các node `lmChatGoogleGemini` và `embeddingsGoogleGemini` bằng:
  - `@n8n/n8n-nodes-langchain.lmChatOpenAI`
  - `@n8n/n8n-nodes-langchain.embeddingsOpenAI`

### **5. Tích Hợp với CRM (HubSpot, Salesforce)**
- Sử dụng node **HubSpot API** hoặc **Salesforce API** để tự động tạo ticket hỗ trợ khi khách hàng gửi câu hỏi.
- **Cách làm:**
  1. Thêm node **HubSpot API** sau node `AI Agent`.
  2. Cấu hình để tạo ticket mới với:
     - Tiêu đề: `Hỗ trợ từ Chatbot - {{customer_name}}`.
     - Nội dung: `Câu hỏi: {{customer_question}} | Câu trả lời: {{ai_answer}}`.

---

## 📌 **Kết Luận**
Workflow **"Chat with your business knowledge base using Google Gemini and Qdrant"** là giải pháp **tự động hóa hoàn chỉnh** cho doanh nghiệp muốn xây dựng một **trợ lý AI chatbot** dựa trên cơ sở tri thức nội bộ. Với workflow này, các sếp sẽ:
✔ **Giảm thiểu 90% thời gian hỗ trợ khách hàng thủ công**.
✔ **Cải thiện trải nghiệm khách hàng** với phản hồi nhanh chóng và chính xác.
✔ **Hoạt động 24/7** mà không cần nhân viên hỗ trợ.

**Hành động ngay hôm nay!**
1. **Chuẩn bị các tài nguyên** (API Key, Qdrant, danh mục tài liệu).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Kích hoạt workflow** và bắt đầu tự động hóa hỗ trợ khách hàng!

---
**📢 Cảm ơn các sếp đã đọc đến cuối!**
Nếu workflow này hữu ích, hãy **like và chia sẻ** để giúp nhiều doanh nghiệp khác tiết kiệm thời gian. Nếu có thắc mắc, hãy để lại bình luận dưới đây!

👉 **Tìm hiểu thêm về GenStaff:** [genstaff.net](https://genstaff.net)
👉 **Liên hệ với tác giả:** [nguyenthieutoan.com](https://nguyenthieutoan.com)