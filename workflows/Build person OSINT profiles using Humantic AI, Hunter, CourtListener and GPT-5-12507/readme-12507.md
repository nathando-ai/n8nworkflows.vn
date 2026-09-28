---
title: "🔍 Tự Động Hoàn Chỉnh Hồ Sơ Cá Nhân OSINT Bằng AI: Từ Dữ Liệu Công Khai Đến Báo Cáo Cấu Trúc (N8n + Humantic AI)"
description: "Workflow tự động hóa cao cấp giúp các sếp nghiên cứu, tổng hợp và phân tích thông tin công khai về cá nhân/doanh nghiệp từ hàng chục nguồn dữ liệu khác nhau, tạo ra báo cáo Markdown chính xác, không chứa sai lệch (hallucination). Giúp tiết kiệm thời gian lên đến 90% so với phương pháp thủ công."
slug: "tieu-dong-hoan-chinh-ho-so-canh-nhan-osint-bang-ai"
tags: [n8n, automation, osint, ai-rag, market-research, humantic-ai, open-router, self-hosted]
keywords: [n8n workflow osint, tự động hóa nghiên cứu thị trường, humantic ai n8n, báo cáo công khai cá nhân, ai r&g, tự động hóa dữ liệu công khai]
---

# **🚀 Tự Động Hoàn Chỉnh Hồ Sơ Cá Nhân OSINT Bằng AI: Giải Pháp Tối Tiến Cho Nghiên Cứu Thị Trường & Doanh Nghiệp**

### **📌 Nỗi Đau Của Các Sếp Hiện Nay**
Trong thế giới kinh doanh ngày nay, thông tin là **vàng**. Tuy nhiên, việc thu thập, phân tích và tổng hợp dữ liệu công khai về cá nhân, đối thủ cạnh tranh hoặc đối tác từ hàng chục nguồn khác nhau (LinkedIn, Twitter, cơ quan pháp lý, báo chí, tài liệu công khai...) là một **công việc cực kỳ tốn thời gian và dễ mắc sai sót**.

- **Thủ công quá chậm**: Một hồ sơ cá nhân đầy đủ thông tin thường mất **từ 5-10 tiếng** để nghiên cứu thủ công.
- **Sai lệch cao**: Con người dễ bị **hiểu sai, bỏ sót hoặc tạo ra thông tin giả (hallucination)** khi tổng hợp.
- **Không thể tự động hóa**: Các công cụ truyền thống chỉ cho phép tra cứu đơn lẻ, không kết nối được nhiều nguồn cùng lúc.
- **Không có báo cáo cấu trúc**: Kết quả thường là một tập tin rối ren, khó phân tích và chia sẻ.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động hóa 100% quá trình OSINT** (Open-Source Intelligence) từ tra cứu đến báo cáo.
✅ **Sử dụng AI tiên tiến** (Humantic AI, GPT-5, Gemini 2.5) để phân tích, sắp xếp và viết báo cáo **không sai lệch**.
✅ **Kết nối nhiều nguồn dữ liệu** (LinkedIn, Twitter, cơ quan pháp lý, tài liệu công khai, cơ sở dữ liệu công ty...) trong một workflow duy nhất.
✅ **Cung cấp báo cáo Markdown sạch sẽ**, dễ đọc và chia sẻ.

---

## **🎯 Kết Quả Các Sếp Nhận Được**
Sau khi triển khai workflow này, các sếp sẽ:
🔹 **Tiết kiệm thời gian lên đến 90%** so với phương pháp thủ công.
🔹 **Nhận báo cáo chính xác 100%**, không chứa thông tin sai lệch (hallucination).
🔹 **Tự động cập nhật thông tin mới** khi có thay đổi từ các nguồn dữ liệu.
🔹 **Dễ dàng chia sẻ và tích hợp** báo cáo vào các hệ thống khác (CRM, Slack, Notion...).
🔹 **Giảm rủi ro pháp lý** nhờ kiểm tra dữ liệu từ cơ quan chính phủ và tài liệu công khai.

---

## **🔧 Yêu Cầu Cần Thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
### **1. API Keys & Credentials**
| **Dịch Vụ**               | **API Key**               | **Mô Tả**                                                                 |
|---------------------------|---------------------------|-----------------------------------------------------------------------------|
| **OpenRouter API**        | `openRouterApi`           | Dùng cho các mô hình AI (GPT-5, Gemini, Auto Fallback).                     |
| **Humantic AI**           | `humanticAiApi`           | API chuyên dụng cho việc tạo và lấy hồ sơ cá nhân OSINT.                   |
| **Hunter.io**             | `hunterApi`               | Tra cứu email và thông tin liên lạc của cá nhân.                         |
| **CourtListener**         | `httpHeaderAuth`          | Lấy dữ liệu từ các tòa án liên bang (Mỹ).                                 |
| **LegiScan**              | `httpQueryAuth`           | Tra cứu luật pháp và hoạt động của cơ quan chính phủ.                     |
| **DocumentCloud**         | (Không cần API)           | Trích xuất nội dung từ tài liệu công khai.                                |
| **ScrapingDog**           | `httpQueryAuth`           | Trích xuất dữ liệu từ LinkedIn, Twitter, Instagram.                         |
| **Weaviate (Vector DB)**  | `weaviateApi`             | Lưu trữ và tra cứu dữ liệu OSINT đã xử lý.                                |
| **OpenAI Embeddings**     | `openAiApi`               | Tạo embedding cho dữ liệu để tra cứu hiệu quả.                            |

### **2. Hệ Thống N8n**
- **N8n Self-Hosted** (không dùng phiên bản cloud để đảm bảo bảo mật và ổn định).
- **VPS 4GB+ RAM** (để chạy workflow với nhiều node đồng thời).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Cách 1: Từ File JSON**
1. Tải workflow từ [n8n.io/workflows/12507](https://n8n.io/workflows/12507) (chọn **Download JSON**).
2. Trên giao diện n8n Editor, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Workflow 1** (tên: *Build person OSINT profiles using Humantic AI, Hunter, CourtListener and GPT-5*).

#### **Cách 2: Copy/Paste JSON**
1. Copy toàn bộ mã JSON từ file tải về.
2. Trên n8n Editor, nhấn **Import** → Chọn **Paste JSON**.
3. Dán mã và nhấn **Import**.

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này **không hoạt động được** nếu không cấu hình đúng các node quan trọng sau:

#### **🔹 Node "Trigger individual research (Webhook)"**
- **Cấu hình Webhook**:
  - **Path**: `osint-personal-profile` (không thay đổi).
  - **HTTP Method**: `POST`.
  - **Credentials**: Không cần (sử dụng mặc định).

#### **🔹 Node "Prepare research input fields" (Set)**
- **Cấu hình Input Schema** (JSON):
  ```json
  {
    "firstName": "string",       // Tên đầu tiên của cá nhân
    "lastName": "string",        // Họ của cá nhân
    "companyName": "string",     // Tên công ty liên quan (nếu có)
    "companyDomain": "string",  // Domain của công ty (ví dụ: google.com)
    "linkedinURL": "string",    // Link LinkedIn (nếu có)
    "reportGoal": "string"      // Mục tiêu báo cáo (ví dụ: "Tìm hiểu lịch sử công việc")
  }
  ```
  - **Lưu ý**: Các trường này **bắt buộc** để workflow hoạt động.

#### **🔹 Node "Auto Fallback" & "GPT-5" (lmChatOpenRouter)**
- **Chọn mô hình AI**:
  - **Auto Fallback**: Sử dụng `openrouter/auto` (mô hình tự động chọn).
  - **GPT-5**: Chọn `openai/gpt-5` (hoặc `google/gemini-2.5-flash`).
- **Cấu hình API Key**:
  - Điền vào `openRouterApi` (từ OpenRouter Dashboard).

#### **🔹 Node "Hunter" (emailFinder)**
- **Cấu hình API Key**:
  - Điền vào `hunterApi` (từ [Hunter.io](https://hunter.io/)).
- **Tham số thêm**:
  - Nếu muốn tra cứu email từ domain, thêm vào `keyParameters`:
    ```json
    {
      "domain": "example.com"
    }
    ```

#### **🔹 Node "CourtListener Discovery" & "LegiScan Discovery"**
- **Cấu hình API Key**:
  - Điền vào `httpHeaderAuth` (từ [CourtListener](https://www.courtlistener.com/) và [LegiScan](https://legiscan.com/)).
- **Tham số thêm**:
  - Thêm `Authorization: Bearer YOUR_API_KEY` vào **Headers** của node.

#### **🔹 Node "Jina URL Text Extraction"**
- **Cấu hình API Key**:
  - Điền vào `jinaAiApi` (từ [Jina AI](https://www.jina.ai/)).
- **Tham số thêm**:
  - Đảm bảo URL được truyền vào `url` trong `keyParameters`.

#### **🔹 Node "Search Open Paws Database" (vectorStoreWeaviate)**
- **Cấu hình Weaviate**:
  - Điền `weaviateApi` (từ [Weaviate](https://weaviate.io/)).
  - **URL**: `http://localhost:8080` (nếu self-hosted).
  - **Schema**: Sử dụng schema mặc định từ Open Paws (xem [đây](https://github.com/Open-Paws/documentation)).

#### **🔹 Node "If hallucinations present" (if)**
- **Cấu hình logic**:
  - Nếu `outputParserStructured` trả về `hallucination: true`, workflow sẽ **bỏ qua bước viết báo cáo** và chuyển sang **Fixing Hallucinations Agent**.

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Gửi request POST đến Webhook với payload:
     ```json
     {
       "firstName": "John",
       "lastName": "Doe",
       "companyName": "TechCorp",
       "companyDomain": "techcorp.com",
       "linkedinURL": "https://linkedin.com/in/johndoe",
       "reportGoal": "Tìm hiểu lịch sử công việc và liên lạc"
     }
     ```
   - Kiểm tra kết quả trong **Final Output**.

2. **Bật Active**:
   - Nhấn **Active** trên workflow.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**
### **1. Tích Hợp Slack/Telegram để Báo Cáo Kết Quả**
- Sử dụng node **Slack** hoặc **Telegram Bot** để gửi báo cáo tự động khi workflow hoàn thành.
- **Cách làm**:
  - Thêm node **Slack** (hoặc **Telegram**) sau **Final Output**.
  - Cấu hình `webhookUrl` từ Slack/Telegram Bot.
  - Chọn `json` trong `Format` để gửi toàn bộ báo cáo.

### **2. Lưu Log & Audit Trail**
- Sử dụng node **Set** để lưu dữ liệu vào **Google Sheets** hoặc **Notion**.
- **Cách làm**:
  - Thêm node **Google Sheets** sau **Final Output**.
  - Cấu hình `sheetName` và `credentials`.
  - Chọn `json` trong `Format` để lưu toàn bộ kết quả.

### **3. Chạy Định Kỳ (Cron Job)**
- Sử dụng **n8n Cron** để tự động chạy workflow hàng ngày/tuần.
- **Cách làm**:
  - Trên n8n Editor, nhấn **Schedule** trên workflow.
  - Chọn **Cron Expression** (ví dụ: `0 0 * * *` để chạy hàng ngày lúc 00:00).

### **4. Tích Hợp với CRM (Salesforce, HubSpot)**
- Sử dụng node **HTTP Request** để gửi báo cáo về CRM.
- **Cách làm**:
  - Thêm node **HTTP Request** sau **Final Output**.
  - Cấu hình `url` là API endpoint của CRM (ví dụ: `https://api.salesforce.com/services/data/v56.0/sobjects/Account/`).
  - Chọn `json` trong `Format`.

### **5. Sử Dụng Mô Hình AI Mới Nhất**
- Nếu OpenRouter không hỗ trợ mô hình mới, có thể **thay thế bằng API khác** (ví dụ: Mistral, Claude).
- **Cách làm**:
  - Thay đổi `model` trong node `lmChatOpenRouter`:
    ```json
    {
      "model": "mistralai/mistral-tiny"
    }
    ```

---

## **📌 Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần:
✔ **Tự động hóa nghiên cứu thị trường** một cách chính xác và hiệu quả.
✔ **Tạo báo cáo OSINT cấu trúc** từ hàng chục nguồn dữ liệu khác nhau.
✔ **Giảm thời gian nghiên cứu** từ nhiều giờ xuống chỉ vài phút.

**Hành động ngay hôm nay:**
1. **Cài đặt n8n Self-Hosted** trên VPS (sử dụng mã giảm giá **VPSN8N**).
2. **Import workflow** và cấu hình các API Key.
3. **Test với dữ liệu mẫu** và bắt đầu tự động hóa nghiên cứu của mình!

**🚀 Cùng n8n và AI biến dữ liệu công khai thành lợi thế cạnh tranh!**

---
**🔗 Tài liệu tham khảo:**
- [Open Paws Documentation](https://github.com/Open-Paws/documentation)
- [n8n Workflow OSINT](https://n8n.io/workflows/12507)
- [OpenRouter API](https://openrouter.ai/)
- [Humantic AI](https://humantic.ai/)