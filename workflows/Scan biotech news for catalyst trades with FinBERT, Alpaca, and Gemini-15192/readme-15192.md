---
title: "🧬 **Tự Động Hóa Dò Tìm Tin Tức Biotech & Đánh Giá Giao Dịch Catalyst với AI (FinBERT + Gemini + Alpaca)** – Không Cần Code!"
description: "Workflow n8n tự động quét tin tức từ PRNewswire, GlobeNewswire và BusinessWire, lọc tin liên quan đến biotech, phân tích cảm xúc với FinBERT, và đánh giá khả năng giao dịch catalyst bằng AI Gemini. Giúp các sếp crypto/trading tự động hóa quy trình tìm kiếm cơ hội giao dịch 24/7 mà không cần viết một dòng code nào."
slug: "tieu-dong-hoa-do-tin-tuc-biotech-voi-ai"
tags: [n8n, automation, crypto-trading, ai-summarization, biotech, finbert, gemini, alpaca, no-code]
keywords: [tự động hóa tin tức biotech, finbert sentiment analysis, gemini ai trading, alpaca api, workflow n8n crypto, dò tìm tin tức catalyst, tự động hóa giao dịch biotech]
---

# 🚀 **Tự Động Hóa Dò Tìm Tin Tức Biotech & Đánh Giá Giao Dịch Catalyst với AI (FinBERT + Gemini + Alpaca)**

### **Giải pháp hoàn hảo cho các sếp trading biotech muốn:**
- **Tiết kiệm 10+ giờ/ngày** quét tin tức thủ công.
- **Lọc tin tức chính xác** với biotech keywords + FinBERT sentiment.
- **Đánh giá khả năng giao dịch** bằng AI Gemini và Alpaca.
- **Hoạt động liên tục 24/7** mà không cần can thiệp.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động quét tin tức** từ 3 nguồn tin chính (PRNewswire, GlobeNewswire, BusinessWire).
- **Lọc tin tức biotech** với keyword tự động và phân tích cảm xúc (FinBERT).
- **Đánh giá khả năng giao dịch** bằng AI Gemini và dữ liệu thị trường từ Alpaca.
- **Lưu trữ và theo dõi** tất cả tin tức, phân tích và dữ liệu giao dịch trong các bảng dữ liệu.
- **Nhận thông báo** về các cơ hội giao dịch mới qua webhook.
- **Tùy chỉnh dễ dàng** keyword, ngưỡng spread/volume và logic AI.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản API**:
   - [HuggingFace API](https://huggingface.co/docs/api-inference/index) (để sử dụng FinBERT).
   - [Google Gemini API](https://ai.google.dev/gemini-api) (để phân tích AI).
   - [Alpaca API](https://alpaca.markets/) (để lấy dữ liệu thị trường).
2. **Bảng dữ liệu (DataTables)** trong n8n:
   - `news_events` (lưu tin tức mới).
   - `processed_events` (lưu tin tức đã xử lý).
   - `trade_candidates` (lưu các cơ hội giao dịch).
   - `llm_analysis` (lưu phân tích AI).
   - `market_snapshots` (lưu dữ liệu thị trường).
3. **N8n Self-hosted** (để chạy 24/7).
   :::info[Gợi ý hạ tầng cho n8n]
   Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
   :::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/15192](https://n8n.io/workflows/15192).
- **Mở n8n Editor** và chọn **Import Workflow** → Chọn file JSON đã tải.
- **Hoặc copy/paste** JSON từ file vào n8n Editor.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **64 node** và được chia thành **3 Layer + 2 Stage**. Dưới đây là các bước **cấu hình bắt buộc**:

#### **🔹 Layer 0: News Ingestion (Quét tin tức)**
- **PRNewswire & GlobeNewswire**: Điền URL RSS của các nguồn tin (ví dụ: `https://feeds.prnewswire.com/prnewswire/biotech`).
- **Merge All Feeds**: Kết hợp tin tức từ cả 2 nguồn.

#### **🔹 Layer 1: FinBERT Sentiment Filter (Lọc tin tức biotech)**
- **Normalize & Extract Tickers**: Sử dụng **code node** để trích xuất tickers từ tin tức (cần chỉnh logic nếu cần).
- **FinBERT Sentiment API**: Điền **HuggingFace API Key** vào credentials `huggingFaceApi`.
- **Biotech Keyword Filter**: Cấu hình danh sách keyword biotech (ví dụ: `CRISPR, mRNA, gene therapy, biotech IPO`).

#### **🔹 Stage 1: Trade Eligibility (Đánh giá khả năng giao dịch)**
- **Alpaca API Key**: Điền vào node `Alpaca Historical Bars` và `Alpaca Quote`.
- **VWAP Bands & Spread Check**: Cấu hình ngưỡng spread (ví dụ: `<= 0.80%`) và relative volume (`>= 4`).
- **Store in trade_candidates**: Lưu các tin tức đáp ứng điều kiện vào bảng `trade_candidates`.

#### **🔹 Stage 2: VWAP Analysis & AI Inference (Phân tích AI)**
- **Gemini Model**: Điền **Google Palm API Key** vào credentials `googlePalmApi`.
- **Build LLM Prompt**: Chỉnh logic prompt để AI phân tích tin tức (ví dụ: *"Analyze this biotech news and suggest trading opportunities"*).
- **Store Snapshot**: Lưu kết quả phân tích AI vào bảng `llm_analysis`.

#### **🔹 Webhooks (Nhận thông báo)**
- **Webhook - Trade Candidates**: Cấu hình URL để nhận tin tức về các cơ hội giao dịch mới.
- **Webhook 2: Get Market Snapshots**: Nhận dữ liệu thị trường mới.
- **Webhook 3: Get LLM Analysis**: Nhận phân tích AI mới.

---
### **3. Kích hoạt ⚡️**
- **Bật Schedule Trigger**: Đặt lịch chạy hàng giờ/ngày (ví dụ: `0 * * * *` để chạy mỗi giờ).
- **Test Run**: Chạy thử với dữ liệu mẫu để kiểm tra logic.
- **Active Workflow**: Sau khi kiểm tra, bật **Active** để workflow chạy tự động.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH TỰ CẢNH BÁO TRÊN SLACK/TELEGRAM]
- Thêm node **Slack/Telegram** vào cuối workflow để nhận thông báo khi có tin tức mới hoặc cơ hội giao dịch.
- Ví dụ: Sau node `Store in trade_candidates`, thêm node **Slack Webhook** để gửi tin nhắn tự động.
:::

:::tip[LƯU LỜI LOG CHO DÒ THỊ TRƯỜNG]
- Thêm node **Google Sheets** hoặc **Notion** để lưu lịch sử tin tức và phân tích AI.
- Sử dụng node **Code** để format dữ liệu trước khi lưu.
:::

:::tip[TỰ ĐỘNG GỬI BÁO CÁO THỰC TẾ]
- Sử dụng **n8n Schedule Trigger** kết hợp với **Email Node** để gửi báo cáo hàng tuần về các tin tức và cơ hội giao dịch.
:::

---
## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp trading biotech muốn tự động hóa quy trình tìm kiếm tin tức và đánh giá cơ hội giao dịch **không cần viết code**. Với **FinBERT, Gemini và Alpaca**, workflow sẽ:
✅ **Lọc tin tức biotech chính xác**.
✅ **Phân tích cảm xúc và khả năng giao dịch**.
✅ **Lưu trữ và theo dõi tất cả dữ liệu**.
✅ **Hoạt động 24/7 mà không cần can thiệp**.

**🚀 Hãy áp dụng ngay và tiết kiệm thời gian cho mình!** 🚀

---
### **🔗 Tài liệu tham khảo**
- [Hướng dẫn cài n8n Self-hosted](https://docs.n8n.io/)
- [HuggingFace API Docs](https://huggingface.co/docs/api-inference/index)
- [Alpaca API Docs](https://docs.alpaca.markets/)
- [Google Gemini API Docs](https://ai.google.dev/gemini-api)