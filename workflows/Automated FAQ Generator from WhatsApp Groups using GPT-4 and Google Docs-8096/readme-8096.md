---
title: "🤖 Tự Động Hóa Tạo FAQ Từ Nhóm WhatsApp Sử Dụng GPT-4 & Google Docs (Không Cần Code)"
description: "Workflow tự động hóa chuyển đổi tin nhắn thường gặp từ nhóm WhatsApp thành FAQ chuẩn mực, được tổng hợp và cập nhật tự động vào Google Docs hàng tuần. Giúp các sếp tiết kiệm 10+ giờ/tháng và cải thiện trải nghiệm khách hàng."
slug: "tay-dong-hoa-tao-faq-tu-nhom-whatsapp-su-dung-gpt-4-google-docs"
tags: [n8n, automation, AI Summarization, Multimodal AI, Google Workspace, GPT-4, no-code]
keywords: [tự động hóa FAQ WhatsApp, GPT-4 tự động hóa, tạo FAQ từ tin nhắn, n8n workflow AI, tự động hóa hỗ trợ khách hàng]
---

# 🚀 **Tự Động Hóa Tạo FAQ Từ Nhóm WhatsApp Sử Dụng GPT-4 & Google Docs**

### **Giải pháp cho các sếp đang mệt mỏi vì phải thủ công tổng hợp FAQ từ hàng trăm tin nhắn WhatsApp mỗi tuần**
Hàng ngày, các nhóm hỗ trợ khách hàng hoặc marketing phải mất **giờ đồng hồ** để:
- Lọc tin nhắn thường gặp từ WhatsApp.
- Phân loại và tổng hợp thành FAQ.
- Cập nhật vào Google Docs/Sheets để chia sẻ với team.
- **Kết quả?** FAQ không đồng bộ, thiếu cập nhật, và khách hàng vẫn phải chờ đợi.

**Workflow này tự động hóa toàn bộ quy trình trong 5 phút mỗi tuần**, sử dụng **GPT-4.1-mini** để phân tích tin nhắn và **Google Docs** để cập nhật FAQ tự động. **Không cần viết code, chỉ cần cài đặt và chạy!**

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** cho team hỗ trợ khách hàng.
- **FAQ chính xác và cập nhật tự động** hàng tuần (thứ 2, 6h sáng).
- **Tối ưu hóa trải nghiệm khách hàng** với câu trả lời chuẩn mực từ AI.
- **Dữ liệu tập trung** trên Google Docs, dễ chia sẻ và theo dõi.
- **Không phụ thuộc vào con người**, hoạt động 24/7.
:::

---
### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Workspace** (Google Sheets, Google Docs, Google Drive) với quyền **Editor**.
2. **API Key OpenAI** (đăng ký tại [OpenAI](https://platform.openai.com/)) để sử dụng GPT-4.1-mini.
3. **Danh sách tin nhắn WhatsApp** được lưu trên **Google Sheets** với cấu trúc:
   - Cột `Message` (tin nhắn gốc).
   - Cột `Date` (ngày gửi, định dạng `YYYY-MM-DD`).
   - Cột `Group` (tên nhóm WhatsApp, ví dụ: "Dịch vụ Khách Hàng").
4. **File mẫu FAQ** trên Google Docs (sẽ được sao chép và cập nhật tự động).
:::

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/8096](https://n8n.io/workflows/8096) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON từ link trên và dán vào **Import Workflow** trong n8n.
- **Cách 3:** Sử dụng **n8n CLI** (nếu tự host):
  ```bash
  n8n import /path/to/workflow.json
  ```

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **7 node** chính, các sếp cần cấu hình kỹ lưỡng như sau:

##### **A. Node "Schedule Trigger" (Khởi động hàng tuần)**
- **Thiết lập lịch:** Chọn **Every Monday at 6:00 AM** (UTC hoặc timezone của bạn).
- **Lưu ý:** Đảm bảo n8n **self-hosted** để workflow chạy 24/7.

##### **B. Node "Get row(s) in sheet" (Lấy tin nhắn từ Google Sheets)**
- **Credentials:** Chọn `googleSheetsOAuth2Api` (đã cấu hình trước).
- **Parameters:**
  - **Sheet Name:** Đặt tên sheet chứa tin nhắn (ví dụ: "WhatsApp_FAQ_Data").
  - **Range:** `A1:B1000` (hoặc điều chỉnh theo số lượng tin nhắn).
  - **Filter:** Thêm điều kiện lọc tin nhắn **thuộc tuần trước** (ví dụ: `Date >= "2024-05-20"` và `Date <= "2024-05-26"`).

##### **C. Node "Code" (Xử lý dữ liệu trước khi AI phân tích)**
- **Mã JavaScript mẫu** (sẽ được tự động thêm trong workflow):
  ```javascript
  // Chuyển đổi tin nhắn thành format phù hợp cho AI
  return {
    messages: $input.all().map(item => ({
      content: item.json.Message,
      role: "user"
    })),
    metadata: {
      group: $input.all()[0].json.Group,
      week: $input.all()[0].json.Date.split('-')[0] // Lấy năm/tuần
    }
  };
  ```
- **Lưu ý:** Nếu tin nhắn có định dạng khác, cần chỉnh sửa mã này.

##### **D. Node "AI Agent" (Phân tích tin nhắn với GPT-4)**
- **Credentials:** Chọn `openAiApi` (đã cấu hình API Key).
- **Key Parameters:**
  - **Model:** `gpt-4.1-mini` (đã được thiết lập mặc định).
  - **Prompt mẫu** (cần chỉnh sửa theo yêu cầu):
    ```
    Tôi là một AI hỗ trợ tạo FAQ. Hãy phân tích tin nhắn dưới đây từ nhóm {group} và trả về:
    1. Danh sách câu hỏi thường gặp (FAQ).
    2. Câu trả lời chi tiết và chuẩn mực.
    3. Nếu tin nhắn là phản hồi của khách hàng, hãy tổng hợp ý kiến chung.
    Format trả về:
    {
      "questions": ["Câu hỏi 1", "Câu hỏi 2"],
      "answers": ["Trả lời 1", "Trả lời 2"]
    }
    ```
- **Lưu ý:** **Không bỏ qua bước này!** Prompt yếu sẽ dẫn đến FAQ không chất lượng.

##### **E. Node "Update a document" (Cập nhật FAQ vào Google Docs)**
- **Credentials:** Chọn `googleDocsOAuth2Api`.
- **Parameters:**
  - **Document ID:** ID của file mẫu FAQ (tìm trong URL Google Docs: `https://docs.google.com/document/d/[ID]/edit`).
  - **Operation:** `update` (đã mặc định).
  - **Content:** Chọn **JSON từ node AI Agent** (cấu trúc `{ "questions": [...], "answers": [...] }`).
- **Lưu ý:**
  - File mẫu phải có **cấu trúc chuẩn** (ví dụ: danh sách `## Câu hỏi 1`, `## Câu trả lời 1`).
  - Nếu muốn **thêm ngày tháng**, chỉnh sửa mã trong node **Code** để thêm metadata.

##### **F. Node "Copy file" (Sao chép file mẫu trước khi cập nhật)**
- **Credentials:** Chọn `googleDriveOAuth2Api`.
- **Parameters:**
  - **Source ID:** ID của file mẫu FAQ (tìm trong Google Drive).
  - **Destination:** Chọn **Create new copy** và đặt tên tự động (ví dụ: `FAQ_Week_{week}`).
- **Lưu ý:** Node này đảm bảo **không ghi đè** vào file gốc.

---
#### **3. Kích hoạt ⚡️**
1. **Test Run:**
   - Chọn **Run Workflow** và nhập **dữ liệu mẫu** từ Google Sheets.
   - Kiểm tra kết quả trên Google Docs.
2. **Bật Active:**
   - Chuyển trạng thái workflow sang **Active**.
   - **Kiểm tra log** để đảm bảo không có lỗi.

---
### ✍️ **Mẹo & gợi ý nâng cao**
:::info[CẢI TIẾN TRONG QUÁ TRÌNH]
1. **Kết hợp với Slack/Telegram:**
   - Thêm node **Slack Webhook** để thông báo khi FAQ được cập nhật.
   - Ví dụ: `📢 FAQ đã được tự động cập nhật cho tuần {week}!`.

2. **Lưu log hoạt động:**
   - Sử dụng node **Sticky Note** để ghi lại lịch sử cập nhật.
   - Cấu hình trong node `n8n-nodes-base.stickyNote` với credentials `stickyNote`.

3. **Tự động gửi báo cáo:**
   - Thêm node **Email** (n8n-nodes-base.email) để gửi báo cáo tuần cho team.
   - Nội dung email: `Danh sách FAQ mới nhất từ {group} - Tuần {week}`.

4. **Phân loại tin nhắn theo nhóm:**
   - Nếu có nhiều nhóm WhatsApp, chỉnh sửa node **Code** để lọc tin nhắn theo `Group`.
   - Ví dụ: `if (item.json.Group === "Dịch vụ Khách Hàng") { ... }`.

5. **Sử dụng GPT-4 Turbo (nếu có budget):**
   - Thay `gpt-4.1-mini` bằng `gpt-4-1106-preview` trong node `lmChatOpenAi` để tăng độ chính xác.
:::

---
### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc thủ công, đồng thời **cải thiện chất lượng hỗ trợ khách hàng** với FAQ được tổng hợp tự động hàng tuần. **Không cần kỹ thuật, chỉ cần cài đặt và chạy!**

**Bắt đầu ngay:**
1. **Cài đặt n8n self-hosted** trên VPS (để workflow hoạt động 24/7).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Active** và để AI làm việc cho bạn!

**Chia sẻ kết quả sau khi sử dụng** để giúp cộng đồng n8n Việt Nam cải thiện workflow này! 🚀