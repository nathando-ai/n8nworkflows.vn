---
title: "🚀 Tự Động Hóa Trích Xuất Điểm Nhấn Cuộc Gọi Doanh Thu với GPT-4o-mini & WayinVideo - Giúp Analyst Tiết Kiệm 100% Thời Gian Scrub Video"
description: "Workflow tự động hóa trích xuất và tổng hợp điểm nhấn quan trọng từ cuộc gọi doanh thu (earnings call) của các công ty, tự động phân tích bằng GPT-4o-mini và lưu kết quả vào Notion. Giúp các nhà phân tích tài chính, quỹ đầu tư và nhóm IR tiết kiệm hàng giờ mỗi tuần, đồng thời đảm bảo độ chính xác cao và cá nhân hóa thông tin."
slug: "tieu-dong-hoa-trich-xuat-diem-nhan-earnings-call-gpt-4o-mini-wayinvideo"
tags: [n8n, automation, ai-summarization, market-research, financial-analysis, notion-integration, wayinvideo, openai-gpt-4o-mini]
keywords: [n8n workflow earnings call, tự động hóa phân tích tài chính, trích xuất điểm nhấn từ video, GPT-4o-mini tổng hợp thông tin, Notion tự động hóa, WayinVideo API, tự động hóa cho nhà đầu tư]
---

# 🚀 **Tự Động Hóa Trích Xuất Điểm Nhấn Cuộc Gọi Doanh Thu với GPT-4o-mini & WayinVideo: Giải Pháp Cho Nhà Phân Tích Tài Chính**

---

### **💥 Nỗi Đau Của Các Nhà Phân Tích Tài Chính**
Hàng tuần, các nhà phân tích tài chính, quỹ đầu tư và nhóm **Investor Relations (IR)** phải **ngồi trước hàng giờ video** của cuộc gọi doanh thu (earnings call) để:
- **Tìm kiếm thủ công** các điểm nhấn quan trọng (revenue growth, guidance, challenges, metrics).
- **Ghi chú lại** thông tin chi tiết như timestamp, nội dung, và ý nghĩa của từng điểm.
- **Tổng hợp** thông tin vào các công cụ như Notion, Excel hay Google Sheets để phân tích sau.

**Kết quả?** Thời gian và sự tập trung bị "đốt cháy" trong khi **mất đi độ chính xác** do con người không thể theo dõi toàn bộ cuộc gọi một cách hiệu quả.

**Workflow này giải quyết tất cả!** Với **AI + API tự động hóa**, bạn chỉ cần **nhập URL cuộc gọi và chủ đề tài chính**, hệ thống sẽ:
✅ **Tự động tìm kiếm** các điểm nhấn quan trọng trong video.
✅ **Phân tích bằng GPT-4o-mini** để tổng hợp thành **báo cáo 8 phần** (categorized, summary, metrics, sentiment, flags, và Notion-ready).
✅ **Lưu kết quả vào Notion** dưới dạng trang cá nhân hóa, sẵn sàng cho phân tích sâu hơn.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng. Đây là giải pháp tối ưu nhất cho các công việc tự động hóa phức tạp như này.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ cao cho AI)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 5-10 giờ/tuần** so với cách làm thủ công.
- **Độ chính xác cao** nhờ AI phân tích toàn bộ nội dung (không bỏ sót điểm nào).
- **Cá nhân hóa báo cáo** với 8 phần phân tích chi tiết (topic, metrics, sentiment, flags).
- **Hoạt động liên tục** (24/7) mà không cần can thiệp của con người.
- **Tích hợp Notion** để quản lý dữ liệu đầu tư một cách hệ thống.
- **Giảm thiểu sai sót** do con người mệt mỏi khi xem video dài.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản WayinVideo** (để sử dụng API **Find Moments**).
   - [Đăng ký WayinVideo](https://wayin.video/) (miễn phí cho thử nghiệm).
   - **API Key** (cần thay thế trong workflow).
2. **Tài khoản OpenAI** (để sử dụng mô hình **GPT-4o-mini**).
   - [Đăng ký OpenAI](https://platform.openai.com/) (cần **API Key**).
3. **Tài khoản Notion** (để lưu kết quả).
   - **OAuth2 Credential** (cấu hình trong n8n).
   - **Database Notion** có tên **"Investor Intelligence"** với các property sau:
     - **Title** (tiêu đề trang).
     - **Company** (tên công ty).
     - **Ticker Symbol** (mã chứng khoán).
     - **Quarter** (quý).
     - **Topic Category** (danh mục chủ đề).
     - **Sentiment** (tình cảm: tích cực/tiêu cực/trung lập).
     - **Timestamp** (thời gian điểm nhấn).
     - **Relevance Score** (điểm tương quan).
     - **Recording URL** (link video).
     - **Call Date** (ngày cuộc gọi).
     - **Status** (trạng thái: New/Processed).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/15434](https://n8n.io/workflows/15434) hoặc copy toàn bộ JSON từ **View Code** trên trang workflow.
- **Dán vào n8n Editor**:
  - Mở **n8n Workflow Editor** (trang chủ → **Create Workflow** → **Import from JSON**).
  - Dán JSON và nhấn **Import**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Dưới đây là **các node quan trọng** cần cấu hình kỹ lưỡng:

##### **🔹 Node 2 & 4: WayinVideo — Submit & Get Moments**
- **Thay thế `YOUR_WAYINVIDEO_API_KEY`** bằng API Key thực tế của bạn.
- **Headers** cần cấu hình:
  - `Authorization: Bearer YOUR_WAYINVIDEO_API_KEY`
  - `Content-Type: application/json`
- **URL API**:
  - **Submit**: `https://api.wayin.video/v1/find-moments`
  - **Get Results**: `https://api.wayin.video/v1/find-moments/{jobId}`

##### **🔹 Node 9: OpenAI — GPT-4o-mini Model**
- **Kết nối credential OpenAI**:
  - Vào **Credentials** → **Add New** → **OpenAI**.
  - Nhập **API Key** từ tài khoản OpenAI.
- **Model**: Đảm bảo chọn **gpt-4o-mini** (không cần thay đổi).

##### **🔹 Node 11: Notion — Create Highlight Page**
- **Kết nối OAuth2**:
  - Vào **Credentials** → **Add New** → **Notion**.
  - Chọn **OAuth2** và đăng nhập tài khoản Notion.
- **Database ID**:
  - Mở **Investor Intelligence** trong Notion → **Settings** → **Share** → **Copy Database ID**.
  - Dán vào trường **Database ID** trong node Notion.
- **Properties**:
  - Đảm bảo các property trong **Investor Intelligence** khớp với cấu trúc trong **Code Node 10** (sẽ giải thích sau).

##### **🔹 Node 7 & 10: Code — Extract Highlight Clips & Parse Investor Analysis**
- **Node 7 (Extract Highlight Clips)**:
  - Chức năng: Chuyển đổi timestamp từ **milliseconds** sang **HH:MM:SS**.
  - **Không cần chỉnh sửa** nếu dùng mã gốc.
- **Node 10 (Parse Investor Analysis)**:
  - **Regex** trong mã sẽ trích xuất **8 phần** từ output của GPT-4o-mini.
  - **Cấu trúc Notion Page Title**:
    ```
    {Company} {Ticker} — {Quarter} — {Topic Category} — Highlight {N}
    ```
  - **Nếu muốn thay đổi**, chỉnh sửa trong **Code Node 10**.

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Nhập **URL cuộc gọi** và **chủ đề tài chính** (ví dụ: "revenue growth", "guidance", "challenges").
  - Chạy **Test Execution** để kiểm tra:
    - WayinVideo có tìm được **8 điểm nhấn** không?
    - GPT-4o-mini có tạo được **8 phần báo cáo** không?
    - Notion có tạo trang mới không?
- **Bật Active**:
  - Sau khi test thành công, chuyển **Workflow Status** từ **Inactive** sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm **Node Slack/Telegram** sau **Node 11** để thông báo khi hoàn thành.
   - Ví dụ: `Tạo trang Notion mới cho {Company} {Ticker} — {Quarter} — {Topic}`

2. **Lưu Log cho Dữ Liệu Audit**:
   - Thêm **Node StickyNote** hoặc **Google Sheets** để ghi lại:
     - Thời gian chạy.
     - Số điểm nhấn tìm được.
     - Status (SUCCESS/FAILED).

3. **Tự Động Chạy Định Kỳ**:
   - Sử dụng **Node Cron** để chạy workflow hàng tuần cho các cuộc gọi mới.
   - Ví dụ: `0 0 * * 1` (chạy thứ 2 hàng tuần).

4. **Tối Ưu Hóa Prompt cho GPT-4o-mini**:
   - Nếu kết quả của GPT-4o-mini không phù hợp, chỉnh sửa **prompt** trong **Node 8 (AI Agent)**:
     ```json
     {
       "prompt": "Tóm tắt chi tiết về {topic} trong cuộc gọi {company} ({ticker}) quý {quarter}. Cấu trúc báo cáo phải bao gồm:",
       "instructions": [
         "1. Topic Category: Danh mục chủ đề (ví dụ: Revenue, Guidance, Challenges).",
         "2. Investor Summary: Tóm tắt ngắn gọn cho nhà đầu tư.",
         "3. Key Metrics: Các con số quan trọng (ví dụ: Revenue: $X billion).",
         "4. Why It Matters: Lý do tại sao điểm này quan trọng.",
         "5. Sentiment: Tình cảm (Positive/Negative/Neutral) + Lý do.",
         "6. Flags: Đánh dấu nếu có thông tin quan trọng (ví dụ: Warning, Surprise).",
         "7. Notion Page Content: Nội dung sẵn sàng để tạo trang Notion."
       ]
     }
     ```

5. **Xử Lý Trùng Lặp**:
   - Thêm **Node IF** trước **Node 11** để kiểm tra:
     - Nếu trang Notion **đã tồn tại**, thì **skip** hoặc **update**.
     - Cách kiểm tra: So sánh **Ticker + Quarter + Topic** trong database.

---

### 📌 **Kết Luận: Hãy Tự Động Hóa Ngay!**
Workflow này **giải phóng thời gian** cho các nhà phân tích tài chính, giúp họ tập trung vào **phân tích sâu hơn** thay vì **làm việc thủ công**. Với **AI + API**, bạn không chỉ **tiết kiệm thời gian**, mà còn **nâng cao độ chính xác** và **cá nhân hóa thông tin** một cách hiệu quả.

**Bước đầu tiên:**
1. **Import workflow** và cấu hình các **API Key**.
2. **Test với 1-2 cuộc gọi** để đảm bảo hoạt động.
3. **Bật Active** và **để nó chạy tự động** hàng tuần!

**🚀 Hãy bắt đầu ngay hôm nay!** Nếu có bất kỳ câu hỏi hoặc gặp khó khăn, hãy để lại **comment** dưới đây, chúng tôi sẽ hỗ trợ chi tiết.

---
**#TựĐộngHóaTàiChính #AIPhânTích #NotionAutomation #WayinVideo #GPT4o-mini**