---
title: "🤖 **Tự Động Hóa Phân Tích Quảng Cáo Meta (Facebook) với AI Gemini + ScrapingFlash – Không Cần Code!**"
description: "Workflow tự động hóa phân tích chi tiết quảng cáo Meta từ Facebook Ad Library, sử dụng AI Gemini để đánh giá creatives, text, và đề xuất cải tiến, sau đó lưu kết quả vào Google Sheets. Giúp các sếp tiết kiệm thời gian phân tích thủ công và đưa ra quyết định marketing thông minh."
slug: "tự-dộng-hoa-phân-tích-quảng-cáo-meta-ai-gemini"
tags: [n8n, automation, ai-gemini, meta-ads, google-sheets, scraping, no-code]
keywords: [tự động hóa quảng cáo facebook, phân tích quảng cáo meta với ai, gemini ai meta ads, scraping facebook ads, google sheets automation, n8n workflow]
---

# 🚀 **Tự Động Hóa Phân Tích Quảng Cáo Meta (Facebook) với AI Gemini – Giải Pháp Marketing 24/7**

### **Nỗi Đau Của Các Sếp Marketing**
Phân tích quảng cáo Meta thủ công là một công việc **mệt mỏi, tốn thời gian** và dễ bị bỏ qua. Các sếp phải:
- **Tìm kiếm và scrap** hàng chục quảng cáo từ Facebook Ad Library.
- **Đọc và đánh giá** từng creatives, text, và chiến lược của đối thủ.
- **So sánh và tổng hợp** kết quả vào bảng Excel hoặc Google Sheets.
- **Đề xuất cải tiến** dựa trên phân tích chủ quan, dễ bị sai sót.

**Kết quả?** Thời gian và nguồn lực bị "chôn vùi" trong công việc thủ công, trong khi đối thủ đã tối ưu hóa chiến dịch với AI.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10-15 giờ/tháng** phân tích thủ công.
- **Đánh giá khách quan** từng quảng cáo với AI Gemini (Google).
- **Lưu trữ dữ liệu** trong Google Sheets, dễ dàng theo dõi và báo cáo.
- **Cải tiến chiến dịch** dựa trên phân tích chi tiết về creatives, text, và hiệu quả.
- **Hoạt động 24/7** với trigger lịch trình (daily/weekly).
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản ScrapingFlash** (để scrap quảng cáo Meta):
   - [Đăng ký miễn phí](https://scrapingflash.com/) và lấy **API Key**.
2. **Google Gemini API Key**:
   - [Cài đặt API Key](https://makersuite.google.com/) (đăng ký tài khoản Google Cloud).
3. **Google Sheets**:
   - Một bảng Google Sheets với **2 sheet**:
     - **Sheet 1**: Danh sách URL của Facebook Ad Library (cột `URL`).
     - **Sheet 2**: Để lưu kết quả phân tích (cấu trúc sẽ được tự động tạo).
4. **Tài khoản n8n Self-hosted** (để workflow chạy 24/7):
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

---
## 🚀 **Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [đây](https://n8n.io/workflows/6276) (hoặc sử dụng link gốc).
- Trong n8n Editor, nhấn **Import Workflow** và chọn file JSON.

:::note[LƯU Ý]
- Nếu copy/paste JSON, **không quên chọn "Import from JSON"** trong menu dropdown.
- Đảm bảo **n8n phiên bản 1.x** (các node LangChain chỉ hỗ trợ từ phiên bản này).
:::

---

### **2. Các Bước Cấu Hình BẮT BUỘC 📌**

#### **🔹 Bước 1: Thiết Lập Credentials**
Các node quan trọng cần cấu hình credentials:

| **Node**               | **Yêu Cầu**                                                                 | **Hướng Dẫn Cấu Hình**                                                                 |
|------------------------|-----------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| **ScrapingFlash**      | API Key                                                                     | - Tạo **Header Auth** trong Credentials.                                            |
|                        |                                                                             | - **Name**: `x-api-key`                                                          |
|                        |                                                                             | - **Value**: API Key từ ScrapingFlash.                                             |
| **Google Gemini**      | API Key (Google Cloud)                                                       | - Tạo **API Key** trong Credentials.                                               |
|                        |                                                                             | - Đăng ký tại [Google Cloud](https://console.cloud.google.com/apis/credentials).     |
| **Google Sheets**      | Tài khoản Google đã kết nối                                               | - Chọn **Google Sheets** trong Credentials và đăng nhập.                          |

#### **🔹 Bước 2: Cấu Hình Node "Get URL to scrap"**
- Chọn **Google Sheets** và chọn **Sheet** chứa danh sách URL.
- Cột chứa URL phải được chọn (ví dụ: `A2:A100`).
- **Lưu ý**: Sheet này sẽ được **đọc tự động** khi workflow chạy.

#### **🔹 Bước 3: Cấu Hình Node "Add row in Sheet"**
- Chọn **Sheet** để lưu kết quả phân tích (tạo mới nếu cần).
- **Mapping columns**:
  - Các trường từ **Structured Output Parser** (ví dụ: `creative_analysis`, `text_analysis`, `suggestions`) sẽ tự động được map vào cột tương ứng.
  - **Lưu ý**: Đảm bảo cột trong Sheet **khớp với output từ AI**.

#### **🔹 Bước 4: Cấu Hình Schedule Trigger (Nếu Muốn Chạy Lịch Trình)**
- Trong node **Schedule Trigger**, chọn:
  - **Frequency**: `Daily` (hoặc `Weekly`).
  - **Time**: Thời gian thích hợp (ví dụ: 8h sáng).

#### **🔹 Bước 5: Test Run & Kích Hoạt**
1. **Test Run**:
   - Chọn **Execute Workflow** để chạy thử với **1-2 URL** đầu tiên.
   - Kiểm tra kết quả trong **Google Sheets** để đảm bảo cấu hình đúng.
2. **Active Workflow**:
   - Sau khi test thành công, **bật Active** để workflow chạy tự động.

---

### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Tăng Số Lượng Quảng Cáo**:
   - Xóa node **Limit to 10 ads** nếu muốn phân tích **tất cả quảng cáo** trong Sheet.
   - **Lưu ý**: AI Gemini có giới hạn token, nên phân tích quá nhiều quảng cáo có thể làm chậm workflow.

2. **Tích Hợp Slack/Telegram**:
   - Thêm node **Slack/Telegram** sau **Structured Output Parser** để thông báo kết quả phân tích.
   - Ví dụ: Gửi tin nhắn khi workflow hoàn thành.

3. **Lưu Log & Báo Cáo Định Kỳ**:
   - Sử dụng node **Google Sheets** để tạo **báo cáo tổng hợp** hàng tuần/month.
   - Ví dụ: Tính trung bình điểm đánh giá của các quảng cáo.

4. **Cải Tiến Prompt AI**:
   - Mở node **chainLlm** và chỉnh sửa **prompt** để AI tập trung vào:
     - **Creative**: Đánh giá hình ảnh, màu sắc, font chữ.
     - **Text**: Kiểm tra CTA, từ khóa, và logic marketing.
     - **Suggestions**: Đề xuất cải tiến dựa trên xu hướng hiện tại.

---

### **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp marketing để tập trung vào **strategy** thay vì phân tích thủ công. Với **AI Gemini**, các quảng cáo được đánh giá **khách quan và chi tiết**, trong khi **Google Sheets** lưu trữ dữ liệu một cách **đơn giản và dễ theo dõi**.

**Hành động ngay!**
1. **Cài đặt VPS** và import workflow.
2. **Cấu hình credentials** và test run.
3. **Bật lịch trình** để workflow chạy tự động hàng ngày.

**🚀 Cùng tự động hóa marketing của mình ngay hôm nay!** 🚀

---
:::note[CẦN GIÚP?]
- **Hỏi đáp**: [n8n Forum](https://community.n8n.io/) hoặc [Discord](https://discord.com/invite/XPKeKXeB7d).
- **Cần hỗ trợ cài đặt VPS**: Liên hệ [TinoHost](https://tino.vn/) hoặc [BNIX](https://my.bnix.one/) với mã **VPSN8N** để giảm giá.