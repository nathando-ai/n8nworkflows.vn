---
title: "🤖 Deep Research Agent: Tự Động Hoàn Thành Nghiên Cứu & Tạo Báo Cáo Notion Với AI (Không Cần Code)"
description: "Workflow tự động hóa nghiên cứu chuyên sâu bằng AI, từ việc thu thập thông tin từ nhiều nguồn đến tổng hợp và xuất báo cáo sẵn sàng trên Notion. Giúp các sếp tiết kiệm thời gian lên tới 80% trong công việc nghiên cứu thị trường, phân tích đối thủ hoặc lập báo cáo chuyên sâu."
slug: "deep-research-agent-tuo-dong-hoan-thanh-nghien-cuu-notion"
tags: [n8n, automation, no-code, market-research, ai-agent, notion-integration, openai, google-gemini, openrouter]
keywords: [n8n workflow nghiên cứu thị trường, tự động hóa báo cáo Notion, AI agent cho nghiên cứu, Tavily API n8n, OpenRouter Claude 3.5, Google Gemini Markdown to HTML]
---

# 🚀 **Deep Research Agent: AI Tự Động Hoàn Thành Nghiên Cứu & Tạo Báo Cáo Notion**

### **Giải pháp cho các sếp bị "ngập" trong công việc nghiên cứu thủ công**
Các sếp đã từng phải mất **giờ đồng hồ** để:
- **Thu thập** thông tin từ nhiều nguồn khác nhau (blog, báo cáo, trang web đối thủ).
- **Lọc** và **tóm tắt** nội dung quan trọng trong hàng trăm trang.
- **Tổng hợp** thành một báo cáo logic, chuyên nghiệp, và **sẵn sàng chia sẻ** với team.
- **Cập nhật** liên tục khi có thông tin mới xuất hiện.

**Deep Research Agent** là **AI Agent tự động hóa toàn bộ quy trình** này chỉ trong **vài phút**, với kết quả **chính xác, chuyên nghiệp và sẵn sàng xuất bản** trên Notion. Không cần viết code, không cần kiến thức kỹ thuật – chỉ cần **gửi yêu cầu** và **nhận báo cáo hoàn chỉnh**.

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian lên tới 80%** so với cách làm thủ công.
✅ **Báo cáo tự động cập nhật** khi có thông tin mới (không cần can thiệp).
✅ **Chất lượng cao** nhờ AI tổng hợp từ nhiều nguồn uy tín (Tavily Search + OpenRouter Claude 3.5).
✅ **Dữ liệu sẵn sàng chia sẻ** trên Notion với định dạng chuyên nghiệp (Markdown → HTML → Notion Blocks).
✅ **Hoạt động 24/7** khi tự động hóa trên VPS (self-hosted).
:::

---

## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần:
- **Tài khoản n8n** (đặc biệt là **self-hosted** để tự động hóa 24/7).
- **Tài khoản Notion** và **ID Database** để lưu trữ báo cáo.
- **API Keys** sau:
  - **Tavily API Key** (để tìm kiếm và trích xuất nội dung từ web).
  - **OpenRouter API Key** (để sử dụng mô hình Claude 3.5 cho AI Agent).
  - **Google Gemini API Key** (để chuyển đổi Markdown → HTML và tạo Notion Blocks).
- **Nguồn dữ liệu** (các sếp có thể kết nối thêm API khác như Google Search, Bing, hoặc API nội bộ).
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/7160](https://n8n.io/workflows/7160) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Chọn **"Import"** → Dán JSON và nhấn **"Import"**.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này **phức tạp** và có **36 node**, nhưng các sếp chỉ cần chú ý đến các phần sau:

#### **A. Cấu hình Webhook (đầu vào)**
- Node **"Webhook"** (path: `1c86c408-aeed-40c5-b4ba-aad5f4cdf0ad`) là **điểm bắt đầu**.
- **Không cần thay đổi** URL này, nhưng các sếp cần:
  - **Kết nối Webhook** với ứng dụng/đơn vị gửi yêu cầu (ví dụ: Slack, Telegram, hoặc form web).
  - **Gửi payload JSON** với trường `"topic"` (ví dụ: `"topic": "Tương lai của AI trong y tế"`).

#### **B. Cấu hình API Keys**
| **Node**               | **API Key cần thiết**          | **Lưu ý**                                                                 |
|------------------------|----------------------------------|---------------------------------------------------------------------------|
| **Tavily Search**      | Tavily API Key                  | Điền vào node **"HTTP Request"** (để tìm kiếm và trích xuất nội dung). |
| **OpenRouter Claude 3.5** | OpenRouter API Key             | Điền vào node **"OpenRouter Chat Model"** (để AI Agent hoạt động).       |
| **Google Gemini**       | Google Gemini API Key            | Điền vào node **"Google Gemini Chat Model"** (để chuyển đổi Markdown).   |
| **Notion**             | Notion Integration Token        | Cấu hình trong node **"Notion"** và **"Notion1"** (để tạo và cập nhật trang). |

#### **C. Cấu hình Notion Database**
- **Node "Notion"** (tạo trang mới) và **"Notion1"** (cập nhật) cần:
  - **Database ID** của Notion (tham khảo [Notion API Docs](https://developers.notion.com/docs/working-with-databases)).
  - **Properties** cần thiết (ví dụ: `Title`, `Description`, `Content`).

#### **D. Cấu hình AI Agents**
- **Strategy Agent** (node `"Strategy Agent"`) và **Report Agent** (node `"Report Agent"`) sử dụng **OpenRouter Claude 3.5**.
  - **Prompt** đã được tối ưu sẵn, nhưng các sếp có thể **cập nhật** trong node `"chainLlm"` nếu cần.
- **Notion Block Generator** (node `"Notion Block Generator"`) sử dụng **Google Gemini** để chuyển đổi nội dung thành định dạng Notion.

#### **E. Cấu hình Tavily API**
- Node **"HTTP Request"** (để gọi Tavily Search) và **"HTTP Request1"** (để trích xuất nội dung) cần:
  - **Base URL**: `https://api.tavily.com`
  - **Headers**:
    ```json
    {
      "X-API-Key": "TAVILY_API_KEY",
      "Content-Type": "application/json"
    }
    ```
  - **Payload mẫu**:
    ```json
    {
      "searchTerm": "{{$node["Loop Over Queries"].json["query"]}}",
      "maxAnswers": 3,
      "safeSearch": "strict"
    }
    ```

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi yêu cầu đến Webhook với payload:
     ```json
     {
       "topic": "Tương lai của blockchain trong ngân hàng"
     }
     ```
   - Kiểm tra **log** trong n8n để đảm bảo workflow chạy đúng.
2. **Bật Active** workflow sau khi kiểm tra thành công.

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁCH LÀM NÂNG CAO]
- **Kết hợp với Slack/Telegram**:
  - Sử dụng **n8n Slack Node** để gửi yêu cầu nghiên cứu qua Slack và nhận báo cáo tự động.
- **Lưu log hoạt động**:
  - Thêm node **"Set"** sau **"Report Agent"** để lưu **tất cả dữ liệu đầu vào/đầu ra** vào Google Sheets hoặc Firebase.
- **Tự động gửi báo cáo định kỳ**:
  - Sử dụng **n8n Cron Node** để chạy workflow hàng tuần/month cho các chủ đề cố định (ví dụ: "Tình hình thị trường AI Việt Nam").
- **Cải thiện chất lượng AI**:
  - Thay đổi mô hình AI trong node `"OpenRouter Chat Model"` sang **GPT-4** (nếu có API key) để tăng độ chính xác.
- **Tích hợp với Google Drive**:
  - Thay vì Notion, các sếp có thể xuất báo cáo dưới dạng **PDF/Word** bằng **Google Docs Node**.
:::

---

## 📌 **Kết luận**
**Deep Research Agent** là **công cụ tự động hóa mạnh mẽ** giúp các sếp:
✔ **Tiết kiệm thời gian** trong nghiên cứu thị trường, phân tích đối thủ, hoặc lập báo cáo chuyên sâu.
✔ **Nhận báo cáo chuyên nghiệp** sẵn sàng chia sẻ trên Notion.
✔ **Hoạt động 24/7** khi tự động hóa trên VPS (self-hosted).

**Hành động ngay!**
1. **Cài đặt n8n trên VPS** (để tự động hóa liên tục):
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
2. **Import workflow** và **cấu hình API Keys**.
3. **Gửi yêu cầu đầu tiên** và **nhận báo cáo tự động**!

**Không cần là Dev, không cần code – chỉ cần AI và n8n!** 🚀