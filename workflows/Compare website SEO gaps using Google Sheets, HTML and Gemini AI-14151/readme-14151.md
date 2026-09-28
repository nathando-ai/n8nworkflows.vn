---
title: "🔍 **Tự Động Hóa So Sánh Hổng SEO Website Bằng AI Gemini, Google Sheets & Scraping HTML**"
description: "Workflow tự động so sánh website của các sếp với đối thủ cạnh tranh để phát hiện hổng SEO (keyword, nội dung, kỹ thuật) và tự động sinh báo cáo cải tiến bằng AI Gemini. Giúp tiết kiệm 10-15 giờ/tháng cho công việc nghiên cứu SEO thủ công."
slug: "tieu-dong-hoa-so-sanh-hong-seo-website-bang-ai-gemini"
tags: [n8n, automation, seo, ai, google-sheets, google-gemini, web-scraping, no-code]
keywords: [n8n workflow seo, tự động hóa so sánh seo website, gemini ai seo, google sheets seo, scrap html website, công cụ seo tự động]
---

# 🚀 **Tự Động Hóa So Sánh Hổng SEO Website: Từ Đối Thủ Sang Báo Cáo Cải Tiến Bằng AI**

### **Nỗi Đau Của Các Sếp Trong SEO**
Các sếp thường phải mất **từ 10-15 giờ/tháng** để:
✅ **So sánh thủ công** nội dung, tiêu đề, meta description giữa website của mình và đối thủ.
✅ **Scraping HTML** để tìm hiểu cấu trúc trang, nội dung blog, hoặc trang dịch vụ.
✅ **Phân tích keyword** và đề xuất chủ đề mới bằng trí tuệ nhân tạo.
✅ **Tạo báo cáo** để trình lên ban lãnh đạo với dữ liệu không đầy đủ hoặc lỗi thời.

**Workflow này giải quyết tất cả bằng một cú nhấp chuột!** Nó tự động:
✔ **So sánh SEO** giữa website của các sếp và đối thủ (từ URL đến nội dung chi tiết).
✔ **Sinh báo cáo cải tiến** bằng AI Gemini (Google’s latest LLM) với đề xuất keyword, chủ đề blog, và lỗi kỹ thuật.
✔ **Cập nhật dữ liệu** vào Google Sheets để theo dõi tiến độ cải tiến.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ scraping nhanh)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10-15 giờ/tháng** so sánh SEO thủ công.
- **Phát hiện hổng keyword** và đề xuất chủ đề blog mới bằng AI.
- **Báo cáo tự động** với phân tích kỹ thuật (speed, mobile-friendly) và nội dung.
- **Cập nhật liên tục** dữ liệu từ Google Sheets (không cần update thủ công).
- **Dễ dàng mở rộng** cho nhiều đối thủ hoặc trang web khác.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** (để lưu URL và báo cáo kết quả).
2. **API Key Google Gemini** (để phân tích AI).
3. **Tài khoản Google Cloud** (để kích hoạt API Gemini).
4. **URL của website và đối thủ** (các sếp muốn so sánh).
5. **Bảng Google Sheets cấu trúc** (mẫu sẽ được hướng dẫn sau).

---
:::info[CHUẨN BỊ]
**Cấu trúc bảng Google Sheets cần thiết:**
| **Sheet 1: Input URLs**       | **Sheet 2: Output SEO Report** | **Sheet 3: All Links (My Website)** |
|-------------------------------|--------------------------------|------------------------------------|
| URL (Website của các sếp)    | Keyword Gaps                  | URL + Title + Meta Description     |
| URL (Đối thủ)                | Missing Content               | Headings (H1, H2, H3)             |
|                               | Technical Issues             | Internal Links                    |
|                               | Improvement Plan             |                                    |

**Lưu ý:** Các sếp cần **chia sẻ quyền chỉnh sửa** cho n8n trên Google Sheets.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import:
- **Tải file JSON** từ [n8n.io/workflows/14151](https://n8n.io/workflows/14151) và upload lên **n8n Editor**.
- **Copy JSON** từ link trên và **paste** vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow có **4 phần chính** cần cấu hình kỹ:

##### **A. Cấu Hình Google Sheets**
1. **Node "Get row(s) in sheet"** (Sheet Input URLs):
   - Chọn **Sheet 1: Input URLs**.
   - **Filter:** `Status = "New"` (để chỉ xử lý URL mới).
   - **Credentials:** Chọn tài khoản Google Sheets đã chia sẻ quyền.

2. **Node "Append in Competitor Sheet"** (Sheet Output SEO Report):
   - Chọn **Sheet 2: Output SEO Report**.
   - **Credentials:** Cùng tài khoản trên.

##### **B. Cấu Hình Google Gemini AI**
1. **Node "Message a model" (GoogleGemini):**
   - **API Key:** Điền **API Key Google Cloud** (mua tại [Google Cloud Console](https://console.cloud.google.com/)).
   - **Prompt Template:** Sử dụng mẫu mặc định (hoặc tùy chỉnh để yêu cầu AI phân tích chi tiết hơn).
   - **Model:** Chọn `gemini-pro` (mô hình mạnh nhất hiện tại).

##### **C. Cấu Hình Scraping HTML**
1. **Node "HTML (for My website)" & "HTML (for Competitor Website)":**
   - **URL:** Được truyền tự động từ Google Sheets.
   - **Headers:** Thêm `User-Agent` để tránh bị chặn:
     ```json
     {
       "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36"
     }
     ```
   - **Timeout:** Đặt **30 giây** để tránh timeout với trang tải chậm.

2. **Node "All Links (My Website)" & "All Links (Competitor Website)" (Code):**
   - **JavaScript:** Sử dụng mã mặc định (đã tối ưu để trích xuất tất cả liên kết trong trang).
   - **Lưu ý:** Nếu website có **JavaScript render**, các sếp cần thêm **Puppeteer** hoặc **Playwright** (n8n có node hỗ trợ).

##### **D. Cấu Hình Merge & Update**
1. **Node "Merge":**
   - Kết hợp dữ liệu từ **website của các sếp** và **đối thủ** trước khi gửi AI phân tích.
2. **Node "Update row in sheet":**
   - Cập nhật **trạng thái** từ "New" → "Processed" trong Sheet Input.

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với **1 URL mẫu** để kiểm tra:
   - Dữ liệu scrap có đầy đủ không?
   - AI có trả về báo cáo hợp lý không?
2. **Bật Active** workflow sau khi kiểm tra thành công.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm nhiều đối thủ:**
   - Mở rộng **Sheet Input URLs** để so sánh với **3-5 đối thủ** cùng lúc.
2. **Tùy chỉnh AI Prompt:**
   - **Yêu cầu AI chi tiết hơn** về:
     ```json
     "Analyze the differences between the two websites and provide:
     1. Missing keywords in my site compared to competitor.
     2. Blog topics I should create based on competitor's content.
     3. Technical SEO issues (e.g., missing alt tags, slow loading pages).
     4. A 3-step improvement plan with actionable steps."
     ```
3. **Lưu log hoạt động:**
   - Thêm **node "Set"** sau "Message a model" để lưu **báo cáo AI** vào Sheet riêng.
4. **Gửi báo cáo qua Email/Slack:**
   - Kết hợp với **node "Email"** hoặc **Slack** để tự động thông báo khi có báo cáo mới.

---
### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **strategy SEO** thay vì công việc thủ công. Bằng cách **tự động hóa so sánh website, scraping HTML, và phân tích AI**, các sếp sẽ:
✅ **Phát hiện hổng SEO** nhanh chóng.
✅ **Sinh báo cáo cải tiến** với đề xuất cụ thể.
✅ **Theo dõi tiến độ** trên Google Sheets.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Thêm URL website** của các sếp vào Sheet Input.
3. **Chạy và xem AI làm việc!**

**🚀 Cần hỗ trợ?** Đăng ký **consulting tự động hóa** tại [iTechNotion](https://itechnotion.com/) để có workflow **được tùy chỉnh hoàn toàn** cho doanh nghiệp của các sếp!