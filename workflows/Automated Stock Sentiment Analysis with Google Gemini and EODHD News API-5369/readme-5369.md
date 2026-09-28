---
title: "📈 **Tự Động Hóa Phân Tích Sentiment Tin Tức Sàn Giao Dịch với Google Gemini & EODHD API**"
description: "Workflow tự động hóa phân tích tình cảm (sentiment) của tin tức liên quan đến cổ phiếu, giúp các nhà đầu tư và quản lý đầu tư đánh giá xu hướng thị trường một cách chính xác và tiết kiệm thời gian. Kết quả được tự động ghi vào Google Sheets với điểm số và lý do phân tích chi tiết."
slug: "tieu-dong-hoa-phan-tich-sentiment-tin-tuc-co-phieu"
tags: [n8n, automation, crypto-trading, ai-summarization, google-gemini, google-sheets, api-integration]
keywords: [tự động hóa phân tích sentiment cổ phiếu, n8n workflow google gemini, phân tích tin tức sàn giao dịch, tự động hóa đầu tư chứng khoán, sentiment analysis api]
---

# 🚀 **Tự Động Hóa Phân Tích Sentiment Tin Tức Cổ Phiếu với Google Gemini & EODHD API**

### **Giải pháp cho những ai muốn đầu tư thông minh mà không cần phân tích thủ công**
Hàng ngày, các nhà đầu tư phải mất nhiều thời gian để đọc và phân tích hàng trăm bài tin tức liên quan đến cổ phiếu, tìm kiếm những thông tin quan trọng để đưa ra quyết định mua/bán. **Workflow này tự động hóa toàn bộ quá trình:**
- **Lấy danh sách cổ phiếu** từ Google Sheets.
- **Tải tin tức mới nhất** từ API EODHD.
- **Phân tích tình cảm (sentiment)** của tin tức bằng Google Gemini (AI mạnh nhất hiện nay).
- **Ghi kết quả** vào Google Sheets với điểm số và lý do phân tích chi tiết.

Kết quả? **Tiết kiệm 10+ giờ/tháng**, giảm thiểu sai sót, và có được báo cáo sentiment chính xác mỗi ngày.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo dữ liệu an toàn và không bị giới hạn.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian:** Không cần đọc hàng trăm bài tin tức mỗi ngày.
✅ **Đánh giá chính xác:** AI phân tích sentiment với độ chính xác cao (điểm số từ -1 đến 1).
✅ **Báo cáo tự động:** Kết quả được ghi vào Google Sheets với lý do phân tích chi tiết.
✅ **Hoạt động liên tục:** Workflow chạy tự động hàng ngày (4:00 PM theo giờ Jerusalem).
✅ **Dễ dàng mở rộng:** Thêm/loại cổ phiếu chỉ cần chỉnh sửa Google Sheets.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** (để lưu danh sách cổ phiếu và kết quả phân tích).
2. **API Key EODHD** (để lấy tin tức từ [EODHD](https://eodhistoricaldata.com/)).
3. **API Key Google Gemini** (để sử dụng mô hình AI phân tích sentiment).
4. **Thời gian zone** (workflow mặc định chạy ở **Asia/Jerusalem**, các sếp có thể điều chỉnh).

---
:::info[CHUẨN BỊ]
- **Google Sheets:**
  - Tạo 1 file Google Sheets tên **"Stock Sentiment"** với 2 sheet:
    - **"stocks"** (để lưu danh sách cổ phiếu cần theo dõi).
    - **"Sheet1"** (để lưu kết quả sentiment).
  - Cấu trúc sheet **"stocks"** (cột A: `Ticker`).
  - Cấu trúc sheet **"Sheet1"** (cột A: `Date`, B: `Ticker`, C: `Sentiment Score`, D: `Rationale`).
- **EODHD API:**
  - Đăng ký tài khoản tại [EODHD](https://eodhistoricaldata.com/) và lấy **API Key**.
- **Google Gemini API:**
  - Đăng ký tại [Google AI Studio](https://makersuite.google.com/) và lấy **API Key**.
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/5369](https://n8n.io/workflows/5369) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/5369) và dán vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Sau khi import, các sếp cần cấu hình các node quan trọng như sau:

##### **A. Cấu hình Credentials**
1. **Google Sheets OAuth2:**
   - Tạo **credentials mới** trong n8n với loại `googleSheetsOAuth2Api`.
   - Chọn **Google Sheets API** và đăng nhập với tài khoản Google đã tạo file **"Stock Sentiment"**.
   - Lưu credentials với tên: `googleSheetsOAuth2Api`.

2. **HTTP Query Auth (EODHD API):**
   - Tạo **credentials mới** với loại `httpQueryAuth`.
   - Điền **API Key** từ EODHD vào trường `auth`.
   - Lưu credentials với tên: `httpQueryAuth`.

3. **Google Gemini API:**
   - Tạo **credentials mới** với loại `googlePalmApi`.
   - Điền **API Key** từ Google AI Studio vào trường `apiKey`.
   - Lưu credentials với tên: `googlePalmApi`.

##### **B. Cấu hình Node "Read_tickers_from_Sheet"**
- **Sheet Name:** `Stock Sentiment`
- **Sheet Tab:** `stocks`
- **Range:** `A:A` (đọc toàn bộ cột Ticker).

##### **C. Cấu hình Node "Get articles from EODHD"**
- **URL:** `https://eodhistoricaldata.com/api/news/{ticker}`
- **Headers:**
  - `Authorization: Bearer {httpQueryAuth.auth}`
- **Query Parameters:**
  - `api_token`: `{httpQueryAuth.auth}`
  - `symbol`: `{json["ticker"]}` (lấy từ input).

##### **D. Cấu hình Node "AI Agent" (Prompt Google Gemini)**
Workflows đã cấu hình sẵn **prompt** cho Google Gemini để phân tích sentiment. Các sếp chỉ cần đảm bảo:
- **Model:** `gemini-pro` (hoặc mô hình khác nếu có).
- **Credentials:** `googlePalmApi`.

##### **E. Cấu hình Node "write_sentiment_to_sheets"**
- **Sheet Name:** `Stock Sentiment`
- **Sheet Tab:** `Sheet1`
- **Range:** `A1` (ghi từ dòng 1).
- **Data:** Đảm bảo cột `Date`, `Ticker`, `Sentiment Score`, `Rationale` được định dạng đúng.

##### **F. Cấu hình Schedule Trigger**
- **Time Zone:** Đổi từ `Asia/Jerusalem` sang `Asia/Ho_Chi_Minh` (hoặc thời gian zone phù hợp).
- **Cron:** `0 16 * * *` (chạy lúc 4:00 PM hàng ngày).

#### **3. Kích hoạt ⚡️**
1. **Test Run:**
   - Chạy workflow với **1-2 cổ phiếu mẫu** (ví dụ: `AAPL`, `MSFT`) để kiểm tra kết quả.
   - Kiểm tra Google Sheets xem có ghi dữ liệu không.
2. **Bật Active:**
   - Sau khi test thành công, bật **Active** cho workflow.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm cảnh báo Slack/Telegram:**
   - Sử dụng node **Slack** hoặc **Telegram Bot** để gửi thông báo khi có cổ phiếu có sentiment **rất cao (1.0)** hoặc **rất thấp (-1.0)**.
   - Ví dụ: *"Cổ phiếu AAPL có sentiment -0.95 - Cần xem xét!"*

2. **Lưu log lỗi:**
   - Thêm node **Google Sheets** hoặc **Email** để ghi log lỗi nếu workflow gặp vấn đề (ví dụ: API EODHD trả về lỗi).

3. **Tự động gửi báo cáo định kỳ:**
   - Sử dụng **Schedule Trigger** khác để gửi báo cáo sentiment hàng tuần qua **Email** hoặc **Google Drive**.

4. **Mở rộng cho nhiều loại tài sản:**
   - Thay vì chỉ cổ phiếu, workflow có thể được điều chỉnh để phân tích **tin tức crypto** (Bitcoin, Ethereum) bằng cách thay đổi API và danh sách tickers.

5. **Tối ưu hóa prompt AI:**
   - Nếu muốn kết quả phân tích **chính xác hơn**, các sếp có thể chỉnh sửa **prompt** trong node `Google Gemini Chat Model` để yêu cầu AI phân tích chi tiết hơn về:
     - **Từ khóa quan trọng** (ví dụ: "giảm giá", "tăng trưởng", "sự kiện").
     - **Nguồn tin tức** (chỉ phân tích tin từ nguồn uy tín).

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các nhà đầu tư, quỹ đầu tư hoặc doanh nghiệp muốn tự động hóa phân tích sentiment tin tức cổ phiếu. **Không cần code, không cần chuyên gia AI**, chỉ cần import và cấu hình vài bước là có được báo cáo sentiment chính xác hàng ngày.

**Hành động ngay:**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Thêm cổ phiếu** vào Google Sheets.
3. **Chạy thử** và theo dõi kết quả!

**Cần hỗ trợ?** Đăng ký tại [n8n Community](https://community.n8n.io/) hoặc liên hệ với tác giả Raz Hadas trên LinkedIn: [@raz-hadas](https://www.linkedin.com/in/raz-hadas/).

---
**🚀 Chúc các sếp thành công với chiến lược đầu tư thông minh!**