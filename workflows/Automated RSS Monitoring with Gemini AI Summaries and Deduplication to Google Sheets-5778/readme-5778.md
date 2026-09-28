---
title: "🤖 Tự Động Hóa Theo Dõi RSS + Tóm Tắt AI Gemini & Lọc Trùng Lặp Sang Google Sheets (N8N)"
description: "Workflow tự động hóa theo dõi RSS feeds từ nhiều nguồn, tóm tắt nội dung bằng AI Gemini, loại bỏ trùng lặp và ghi dữ liệu vào Google Sheets với định dạng chuyên nghiệp. Giúp các sếp tiết kiệm 10+ giờ/tháng theo dõi tin tức, phân tích thị trường và cập nhật thông tin nhanh chóng."
slug: "tieu-dong-hoa-theo-doi-rss-ai-gemini-google-sheets"
tags: [n8n, automation, ai-summarization, market-research, google-sheets, gemini-ai, no-code]
keywords: [tự động hóa theo dõi tin tức, gemini ai tóm tắt bài viết, loại bỏ trùng lặp rss, google sheets tự động hóa, workflow n8n market research]
---

# 🚀 **Tự Động Hóa Theo Dõi RSS Feeds + Tóm Tắt AI Gemini & Lọc Trùng Lặp Sang Google Sheets**

Bạn đã bao giờ phải mất **giờ đồng hồ** mỗi ngày để theo dõi tin tức từ nhiều nguồn RSS, đọc từng bài viết, tóm tắt và phân loại chúng? Hay phải lo lắng **trùng lặp dữ liệu** khi cùng một bài viết xuất hiện trên nhiều feed? **Workflow này giải quyết tất cả!**

Với **Automated RSS Monitoring with Gemini AI Summaries**, các sếp có thể:
✅ **Tự động theo dõi** tất cả RSS feeds từ Google Sheets
✅ **Lọc mới nhất** trong thời gian cấu hình (ví dụ: 7-30 ngày)
✅ **Loại bỏ trùng lặp** bằng cách kiểm tra URL đã tồn tại
✅ **Tải nội dung đầy đủ** từ bài viết (không chỉ tiêu đề)
✅ **Tóm tắt bằng AI Gemini** với **cấu trúc chuyên nghiệp** (điểm chính, takeaways, phân tích)
✅ **Ghi dữ liệu vào Google Sheets** với định dạng sẵn sàng phân tích

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng. Đây là giải pháp **an toàn, nhanh chóng và tiết kiệm chi phí** so với dùng phiên bản cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** theo dõi tin tức thủ công.
- **Dữ liệu chính xác 100%** (không bỏ sót, không trùng lặp).
- **Tóm tắt AI chuyên nghiệp** với Gemini, giúp **nhận ra điểm chính nhanh chóng**.
- **Cập nhật tự động** mỗi giờ (hoặc theo lịch bạn thiết lập).
- **Dữ liệu sẵn sàng phân tích** trên Google Sheets với định dạng chuẩn.
- **Cá nhân hóa** theo ngành nghề (thay đổi prompt AI theo nhu cầu).
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để sử dụng Google Sheets và OAuth2 API).
2. **API Key OpenRouter** (để kết nối với Gemini AI).
   - Đăng ký tại: [https://openrouter.ai/](https://openrouter.ai/)
   - **Model sử dụng**: `google/gemini-2.5-flash` (miễn phí trong giới hạn).
3. **Google Sheet mẫu** (sẽ copy từ link dưới đây).
4. **Danh sách RSS feeds** (các nguồn tin tức bạn muốn theo dõi).

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/5778](https://n8n.io/workflows/5778) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/5778) và paste vào **Create Workflow** → **Import JSON**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình Google Sheets**
1. **Copy Google Sheet mẫu**:
   - [📄 Link Sheet mẫu](https://docs.google.com/spreadsheets/d/1i1p_DPymm8QeZrCLxs-Skz8BMSutKpUW4khzpiNBcYc/copy)
   - Sau khi copy, **điền URL mới** vào **node "Settings"** (node `set` đầu tiên).

2. **Cấu trúc Sheet**:
   - **Tab "Articles"**: Ghi dữ liệu bài viết (pubDate, source, title, link, categories, ai summary).
   - **Tab "RSS FEEDS"**: Danh sách RSS feeds cần theo dõi (RSS NAME + RSS URL).

##### **B. Cấu hình API & Credentials**
1. **Google Sheets OAuth2**:
   - Tạo **credentials mới** trong n8n:
     - **Node**: `Get RSS Feed List`, `Get Row for URL is in Sheets`, `Append Summary to Google Sheets`.
     - **Thao tác**:
       - Vào **Credentials** → **Add** → **Google Sheets OAuth2 API**.
       - Đăng nhập Google và cấp quyền cho n8n.

2. **OpenRouter API (Gemini AI)**:
   - Tạo **credentials mới**:
     - **Node**: `LLM Chat Model` (model `lmChatOpenRouter`).
     - **Thao tác**:
       - Vào **Credentials** → **Add** → **OpenRouter API**.
       - Điền **API Key** từ OpenRouter (tạo tại [đây](https://openrouter.ai/)).
       - **Model mặc định**: `google/gemini-2.5-flash`.

##### **C. Cấu hình thời gian lọc & AI**
1. **Thiết lập thời gian lọc bài viết mới**:
   - Vào **node "Settings"** (node `set` đầu tiên).
   - Thay đổi giá trị `"lastXDays"` (ví dụ: `7` để lấy tin tức trong 7 ngày).

2. **Cấu hình AI Prompt (tóm tắt bài viết)**:
   - Vào **node "Summarize Content"** (node `chainLlm`).
   - **Prompt mặc định** đã tối ưu cho Gemini, nhưng các sếp có thể **tùy chỉnh** để phù hợp với ngành nghề:
     ```plaintext
     Tóm tắt bài viết này với cấu trúc sau:
     1. Điểm chính (3-5 điểm)
     2. Takeaways thực tế
     3. Phân tích ngắn về tác động
     ```

##### **D. Kích hoạt Workflow ⚡️**
1. **Test Run**:
   - Chạy **Manual Trigger** để kiểm tra workflow với 1-2 bài viết mẫu.
   - Kiểm tra **Google Sheets** xem dữ liệu có được ghi đúng không.

2. **Bật Schedule Trigger**:
   - Vào **node "Schedule Trigger"** (node `scheduleTrigger`).
   - Thiết lập **thời gian chạy tự động** (ví dụ: **mỗi giờ**).
   - **Bật Active** để workflow chạy liên tục.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm **node `webhook`** sau khi tóm tắt để gửi tin nhắn cảnh báo khi có bài viết mới quan trọng.

2. **Lưu log hoạt động**:
   - Thêm **node `stickyNote`** để ghi lại lỗi hoặc trạng thái của workflow.

3. **Báo cáo định kỳ**:
   - Sử dụng **node `googleSheets`** để tạo **báo cáo tổng hợp** (ví dụ: số bài viết mới mỗi tuần).

4. **Tùy chỉnh AI Prompt**:
   - Nếu theo dõi **tin tức thị trường**, thay đổi prompt để AI tập trung vào **dữ liệu số liệu, dự báo, và xu hướng**.
   - Ví dụ:
     ```plaintext
     Tóm tắt bài viết này với trọng tâm vào:
     - Dữ liệu thị trường (số liệu, con số)
     - Dự báo và xu hướng
     - Ảnh hưởng đến ngành [ngành của bạn]
     ```

5. **Lọc theo danh mục**:
   - Thêm **cột `categories`** vào Google Sheets và sử dụng **node `filter`** để chỉ lấy bài viết thuộc danh mục cụ thể.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **phân tích và ra quyết định** thay vì mất công theo dõi tin tức thủ công. Với **AI Gemini**, dữ liệu không chỉ được **tóm tắt nhanh chóng**, mà còn **cấu trúc chuyên nghiệp**, giúp **nhận ra điểm quan trọng chỉ trong vài giây**.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Thêm RSS feeds** của bạn vào Google Sheet.
3. **Bật Schedule Trigger** để tự động hóa hoàn toàn.

**🚀 Còn chờ gì nữa?** Hãy tự động hóa theo dõi tin tức của mình **hôm nay**! Nếu có vấn đề, các sếp có thể **comment bên dưới** hoặc liên hệ với cộng đồng n8n tại [n8n.io/community](https://n8n.io/community).