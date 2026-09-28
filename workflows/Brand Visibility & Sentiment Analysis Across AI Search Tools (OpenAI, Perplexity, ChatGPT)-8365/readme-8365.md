---
title: "🔍 **Tự Động Hóa Xem Xét Tầm Nhìn & Sentiment Brand Trên AI Search Tools (OpenAI, Perplexity, ChatGPT) – Không Cần Code**"
description: "Workflow tự động hóa phân tích tầm nhìn thương hiệu và cảm xúc khách hàng trên các công cụ AI như OpenAI, Perplexity và ChatGPT, giúp doanh nghiệp đánh giá hiệu quả marketing và tối ưu hóa nội dung một cách nhanh chóng và chính xác."
slug: "tieu-dong-hoa-brand-visibility-sentiment-analysis"
tags: [n8n, automation, ai-search, market-research, sentiment-analysis, openai, perplexity, chatgpt, google-sheets, no-code]
keywords: [n8n workflow brand visibility, tự động hóa phân tích sentiment, tối ưu hóa nội dung trên AI, phân tích tầm nhìn thương hiệu, tự động hóa market research, chatgpt scraper, openai api tự động hóa]
---

# 🚀 **Tự Động Hóa Phân Tích Tầm Nhìn & Sentiment Brand Trên AI Search Tools**

## **Giới Thiệu**
Bạn đã bao giờ lo lắng rằng thương hiệu của mình có thể bị "bỏ qua" khi khách hàng sử dụng các công cụ AI như **ChatGPT, Perplexity hoặc OpenAI** để tìm kiếm thông tin? Hay bạn muốn biết cách **đánh giá hiệu quả của chiến dịch marketing** một cách chính xác mà không cần phân tích thủ công?

**Workflow này giải quyết vấn đề đó!** Nó tự động hóa quá trình:
✅ **Kiểm tra tầm nhìn thương hiệu** trên các công cụ AI nổi tiếng.
✅ **Phân tích cảm xúc (sentiment)** của khách hàng khi tương tác với thương hiệu.
✅ **Tích hợp kết quả vào Google Sheets** để theo dõi và báo cáo định kỳ.
✅ **So sánh phản hồi từ OpenAI, Perplexity và ChatGPT** để tối ưu hóa nội dung.

Không cần viết một dòng code nào, bạn chỉ cần **cấu hình và chạy** – workflow sẽ tự động hóa toàn bộ quy trình!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phân tích thủ công trên hàng trăm câu hỏi từ khách hàng.
- **Đánh giá chính xác**: So sánh phản hồi từ **OpenAI, Perplexity và ChatGPT** để biết thương hiệu được nhắc đến như thế nào.
- **Sentiment Analysis tự động**: Nhận kết quả phân tích cảm xúc (tích cực, trung tính, tiêu cực) từ AI.
- **Báo cáo tự động**: Kết quả được lưu vào **Google Sheets**, dễ dàng theo dõi và chia sẻ.
- **Tối ưu hóa nội dung**: Nhận đề xuất cải thiện từ AI để tăng **tầm nhìn thương hiệu** trên các công cụ tìm kiếm AI.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản API**:
   - **OpenAI API Key** (để gọi các mô hình GPT-4, GPT-5).
   - **Perplexity API Key** (để phân tích trên Perplexity).
   - **APIfy Credential** (để gọi ChatGPT qua web interface – **sử dụng có rủi ro, chỉ dành cho testing**).

2. **Google Sheets**:
   - **Sheet 1**: Danh sách **câu hỏi/prompt** (cột "Prompt").
   - **Sheet 2**: Bảng kết quả (các cột: `LLM`, `Response`, `Brand mentioned`, `Basic Polarity`, `Emotion Category`, `Source 1`, `Source 2`, `Source 3`, `Source 4`).

3. **Credentials trong n8n**:
   - **Google Sheets OAuth 2.0** (để đọc/giới thiệu dữ liệu).
   - **HTTP Query Auth** (để gọi APIfy ChatGPT Scraper).
   - **Perplexity API** (nếu muốn sử dụng Perplexity).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/8365](https://n8n.io/workflows/8365) hoặc copy/paste JSON vào **n8n Editor**.
- **Nhấn "Import"** và chọn **Self-hosted** (nếu cài trên VPS).

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **2 chế độ chính**:
- **Chế độ đơn giản (Perplexity chỉ)**: Dùng để test với 1 prompt.
- **Chế độ đa mô hình (OpenAI + Perplexity + ChatGPT)**: Phân tích trên 3 công cụ khác nhau.

##### **Cấu hình cơ bản (cả 2 chế độ)**
| Node | Thao tác cần làm |
|------|------------------|
| **Manual Trigger** | Khởi động workflow thủ công. |
| **Read Prompts1 (Google Sheets)** | Chọn **Sheet 1** (câu hỏi) và **cột "Prompt"**. |
| **Loop Over prompts (Split in Batches)** | Chọn **batch size** (ví dụ: 10 câu hỏi/lần). |
| **LLM-Prompts (Set)** | Điền **template prompt** để AI phân tích (có sẵn trong workflow). |
| **Chat Model (OpenAI, Perplexity, ChatGPT)** | Chọn mô hình AI (gpt-4.1-mini, gpt-5, Perplexity "sonar"). |
| **Output Parser Structured** | Đảm bảo **cấu trúc JSON** của kết quả đúng (ví dụ: `{"brand_mentioned": true, "sentiment": "positive"}`). |
| **Append row in sheet (Google Sheets)** | Chọn **Sheet 2** (kết quả) và **các cột** cần ghi. |

##### **Cấu hình riêng cho mỗi công cụ**
| Công cụ | Node | Lưu ý |
|---------|------|-------|
| **OpenAI** | `lmChatOpenAi` | Chọn mô hình (`gpt-4.1-mini` hoặc `gpt-5`). Đảm bảo **API Key** đã cấu hình trong `openAiApi`. |
| **Perplexity** | `perplexity` | Chọn mô hình `sonar`. Đảm bảo **API Key** đã cấu hình trong `perplexityApi`. |
| **ChatGPT (APIfy)** | `httpRequest` | Sử dụng **Generic Credential Type > Query Auth** với tên `token`. **Chỉ dùng để test!** |

##### **Cấu hình Sentiment Analysis**
- Workflow sử dụng **Agent-based LLM** để phân tích cảm xúc.
- Kết quả sẽ được **ghi vào Google Sheets** với các cột:
  - `Basic Polarity` (tích cực/tiêu cực/trung tính).
  - `Emotion Category` (sự hài lòng, lo lắng, trung lập...).

#### **3. Kích hoạt ⚡️**
- **Test Run**: Chọn **1-2 câu hỏi mẫu** và chạy thử.
- **Bật Active**: Sau khi kiểm tra, **bật workflow** để chạy tự động.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tăng cường phân tích đa ngôn ngữ**:
   - Thêm **cột "Ngôn ngữ"** vào Google Sheets và sử dụng **prompt đa ngôn ngữ** trong LLM.

2. **Gửi báo cáo định kỳ qua Email/Slack**:
   - Kết hợp với **Node Email** hoặc **Slack Webhook** để tự động gửi báo cáo hàng tuần.

3. **Lưu log vào cơ sở dữ liệu**:
   - Thêm **Node Database** (PostgreSQL, MySQL) để lưu lịch sử phân tích.

4. **Tối ưu hóa prompt**:
   - Sử dụng **LangChain Agent** để tự động cải thiện prompt dựa trên kết quả trước đó.

5. **So sánh với đối thủ**:
   - Thêm **cột "Brand Competitor"** vào Google Sheets và so sánh phản hồi giữa thương hiệu và đối thủ.

---

### 📌 **Kết luận**
Workflow này là **công cụ mạnh mẽ** để doanh nghiệp:
✔ **Đánh giá tầm nhìn thương hiệu** trên các công cụ AI.
✔ **Phân tích sentiment** một cách tự động.
✔ **Tối ưu hóa nội dung** dựa trên phản hồi thực tế.

**Hành động ngay!**
- **Import workflow** và bắt đầu phân tích.
- **Cập nhật Google Sheets** với câu hỏi của khách hàng.
- **Theo dõi kết quả** và cải thiện chiến lược marketing!

👉 **Bạn có thể mở rộng workflow này** để phân tích trên **Bing AI, You.com, hoặc các công cụ tìm kiếm AI mới** trong tương lai.

---
**Chia sẻ và đóng góp ý kiến** để workflow này ngày càng hoàn thiện! 🚀