---
title: "🤖 Tự Động Hóa Tóm Tắt Tin Tức & Tài Liệu AI từ Email Newsletter với Gemini, Slack & Notion"
description: "Workflow này tự động phân tích và tóm tắt nội dung từ email newsletter hàng ngày, tạo ra bản tóm tắt thông minh với AI Gemini, gửi kết quả lên Slack và lưu ý tưởng sáng tạo vào Notion. Giúp các sếp tiết kiệm thời gian, tránh bị ngập tràn thông tin và phát hiện xu hướng nhanh chóng."
slug: "tieu-dong-hoa-tom-tat-tin-tuc-newsletter-ai-gemini-slack-notion"
tags: [n8n, automation, ai-summarization, gemini-ai, slack-integration, notion-api, email-automation]
keywords: [n8n workflow newsletter, tự động hóa email newsletter, gemini ai tóm tắt, gửi tin tức lên slack, lưu ý tưởng vào notion, tự động hóa thông tin doanh nghiệp]
---

# 🚀 **Tự Động Hóa Tóm Tắt Tin Tức & Tài Liệu AI từ Email Newsletter với Gemini, Slack & Notion**

### **Giải pháp cho các sếp bị "ngập" email newsletter hàng ngày**
Các sếp đã từng phải mất **30-60 phút mỗi ngày** để đọc và tóm tắt nội dung từ email newsletter? Hay thậm chí **quên đọc một số email quan trọng** vì số lượng quá lớn? Workflow này sẽ **tự động hóa toàn bộ quá trình**, sử dụng AI Gemini để phân tích, lọc ra những điểm quan trọng nhất, và gửi kết quả dưới dạng **bản tóm tắt thông minh** lên Slack. Ngoài ra, nó còn **lưu các câu hỏi sáng tạo** vào Notion để các sếp có thể tham khảo sau này.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 1-2 giờ/ngày** để đọc và tóm tắt email newsletter.
- **Lọc ra những tin tức quan trọng** dựa trên tiêu chí cá nhân hóa (do các sếp tự định nghĩa).
- **Nhận bản tóm tắt AI** được gửi trực tiếp lên Slack hàng ngày (không cần mở email).
- **Lưu ý tưởng sáng tạo** vào Notion để tham khảo sau (đặc biệt hữu ích cho content marketing).
- **Hoạt động liên tục 24/7** mà không cần can thiệp thủ công.
- **Cải thiện hiệu suất công việc** bằng cách tập trung vào những thông tin thực sự có giá trị.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
✅ **Tài khoản Gmail** với email newsletter được **nhãn định** (ví dụ: "AI-Newsletter", "Industry-Update").
✅ **API Key OpenRouter** (để sử dụng mô hình AI Gemini 2.5 Flash).
✅ **Bot Slack** (để gửi bản tóm tắt hàng ngày).
✅ **Tài khoản Notion** (tùy chọn, để lưu các câu hỏi sáng tạo).
✅ **API Key Perplexity** (tùy chọn, để nghiên cứu sâu hơn).
✅ **VPS n8n** (để chạy workflow 24/7).
:::

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể **import workflow từ file JSON** hoặc **copy/paste JSON** vào n8n Editor:
```json
// Dữ liệu JSON của workflow sẽ được cung cấp sau
```
**Hướng dẫn chi tiết:**
1. Mở **n8n Editor** trên VPS.
2. Nhấn **Import** và chọn file JSON.
3. Hoặc **copy toàn bộ JSON** và dán vào **Import from JSON** trong Editor.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Node "Get Labeled Newsletters" (Gmail)**
- **Chọn nhãn email** trong dropdown (ví dụ: "AI-Newsletter").
- **Không cần thay đổi** phần `operation: getAll` (lấy tất cả email có nhãn trong 24h).

#### **🔹 Node "Daily Morning Trigger" (ScheduleTrigger)**
- **Điều chỉnh thời gian** theo múi giờ của các sếp:
  - **Múi giờ Việt Nam (UTC+7)**: `"0 1 * * *"` (8h sáng).
  - **Múi giờ Mỹ (Pacific, UTC-7)**: `"0 15 * * *"`.
  - **Múi giờ Mỹ (Eastern, UTC-5)**: `"0 12 * * *"`.
- **Lưu ý**: Workflow sẽ chạy hàng ngày vào thời gian đã thiết lập.

#### **🔹 Node "Configuration" (Set)**
- **Cập nhật thông tin cá nhân hóa** để AI phân tích phù hợp:
  - **Industry**: Chọn ngành nghề (ví dụ: "Tech", "Marketing", "Finance").
  - **Audience**: Đối tượng mục tiêu (ví dụ: "Founders", "Investors").
  - **Relevance Criteria**: Tiêu chí lọc tin tức (ví dụ: "Chỉ lấy tin tức về AI mới").
  - **Output Format**: Định dạng kết quả (ví dụ: "Bản tóm tắt ngắn", "Câu hỏi sáng tạo").

#### **🔹 Node "OpenRouter Chat Model" & "Output Parser Model" (lmChatOpenRouter)**
- **Không cần thay đổi** phần `model: "google/gemini-2.5-flash"` (sử dụng mô hình Gemini 2.5 Flash).
- **Đảm bảo API Key OpenRouter** đã được thêm vào **Credentials** trong n8n.

#### **🔹 Node "Send to Slack" (Slack)**
- **Chọn channel Slack** trong dropdown (ví dụ: `#ai-updates`).
- **Không cần thay đổi** phần `messageFormat` (sẽ tự động format thành tin nhắn Slack).

#### **🔹 Node "Save Questions to Notion" (Notion - tùy chọn)**
- **Chọn database Notion** trong dropdown (nếu muốn lưu câu hỏi).
- **Không cần thay đổi** phần `resource: "databasePage"` (lưu vào trang database).

#### **🔹 Node "Perplexity Research Tool" (PerplexityTool - tùy chọn)**
- **Chọn mô hình** trong dropdown (ví dụ: `sonar-pro`).
- **Không cần thay đổi** nếu chỉ muốn sử dụng Gemini.

---

### **3. Kích hoạt ⚡️**
1. **Test run** với **1-2 email mẫu** để kiểm tra kết quả.
2. **Bật Active workflow** sau khi đã cấu hình xong.
3. **Kiểm tra Slack** vào sáng hôm sau để xem bản tóm tắt AI.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH LÀM NÂNG CAO]
- **Thêm nhiều nhãn email** để workflow phân tích nhiều nguồn tin tức khác nhau.
- **Kết hợp với Google Drive** để lưu bản tóm tắt dài hạn.
- **Sử dụng Notion API** để tự động tạo **báo cáo tuần/month** từ các câu hỏi AI.
- **Tích hợp với Microsoft Teams** thay vì Slack (thay đổi node `Send to Slack`).
- **Cập nhật mô hình AI** (ví dụ: sử dụng `gemini-pro` thay vì `gemini-2.5-flash`).
- **Lưu log hoạt động** vào **Google Sheets** để theo dõi hiệu suất.
:::

---
## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp bị **ngập tin tức** nhưng muốn **tập trung vào những thông tin quan trọng nhất**. Bằng cách **tự động hóa phân tích và tóm tắt**, các sếp sẽ **tiết kiệm thời gian, tăng hiệu suất và phát hiện xu hướng nhanh chóng**.

**Hãy áp dụng ngay và bắt đầu ngày làm việc hiệu quả hơn!** 🚀

---
### **🔗 Tài liệu tham khảo**
- [Tutorial Gmail Label](https://support.google.com/mail/thread/208327636)
- [OpenRouter API Docs](https://openrouter.ai/)
- [Slack API Integration](https://api.slack.com/)
- [Notion API Guide](https://developers.notion.com/)