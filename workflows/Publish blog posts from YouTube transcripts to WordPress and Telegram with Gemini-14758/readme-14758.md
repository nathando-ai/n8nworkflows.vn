---
title: "🚀 Tự Động Hóa Tạo Bài Blog Từ Transcript YouTube → WordPress + Telegram Với Gemini AI (Không Cần Code)"
description: "Workflow tự động hóa hoàn chỉnh chuyển đổi transcript YouTube thành bài blog chuyên nghiệp, tự động đăng lên WordPress và chia sẻ trên Telegram với AI Gemini. Giúp tiết kiệm 10+ giờ công/tháng, tối ưu SEO và tăng engagement cho nội dung."
slug: "tu-dong-hoa-tao-bai-blog-tu-transcript-youtube-den-wordpress-telegram-gemini"
tags: [n8n, automation, content-creation, ai-gemini, wordpress, telegram-bot, google-sheets, no-code]
keywords: [n8n workflow tự động hóa blog, chuyển transcript YouTube thành bài viết, AI Gemini tạo nội dung, tự động đăng bài WordPress, chia sẻ bài blog Telegram, tự động hóa content marketing]
---

# 🚀 **Tự Động Hóa Tạo Bài Blog Từ Transcript YouTube → WordPress + Telegram Với Gemini AI**

## **🔥 Giải Pháp Cho Những Ai:**
- **Chủ blogger** muốn tự động hóa quá trình viết bài từ video YouTube mà không cần viết tay.
- **Marketing manager** cần tạo nội dung định kỳ từ video giáo dục, review sản phẩm, hoặc tutorial.
- **Doanh nghiệp** muốn tối ưu hóa content marketing bằng AI mà không cần đội ngũ viết bài chuyên nghiệp.

**Trước khi tự động hóa:**
- Tốn **5-10 giờ/ngày** để transcribe video, viết bài, tối ưu SEO, và đăng tải.
- Nội dung **không đồng bộ** giữa video và bài viết, mất thời gian chỉnh sửa.
- **Không theo dõi** tiến độ công việc, dẫn đến quên hoặc trễ hạn.

**Sau khi áp dụng workflow này:**
✅ **Tự động hóa 100%** từ transcript → bài blog → đăng tải.
✅ **Nội dung chuyên nghiệp** với AI Gemini tối ưu SEO và cấu trúc logic.
✅ **Tiết kiệm 80% thời gian** so với viết tay.
✅ **Đăng tải tự động** lên WordPress và chia sẻ trên Telegram.
✅ **Theo dõi trạng thái** toàn bộ quá trình trên Google Sheets.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ cao cho AI Gemini)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** so với viết bài thủ công.
- **Nội dung SEO-optimized** tự động từ AI Gemini.
- **Tự động đăng tải** lên WordPress và chia sẻ Telegram **không cần can thiệp**.
- **Theo dõi toàn bộ quá trình** trên Google Sheets (trạng thái video, bài viết, hình ảnh).
- **Tăng engagement** với hình ảnh tự động tạo từ AI.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản và API Key:**
   - **Google Sheets API** (để lưu video, bài viết, và trạng thái).
   - **Google Docs API** (để lưu transcript).
   - **WordPress API** (đăng bài tự động).
   - **Telegram Bot Token** (gửi thông báo).
   - **YouTube API Key** (fetch playlist và transcript).
   - **RapidAPI Key** (nếu sử dụng API transcript ngoài YouTube).
   - **AI Gemini API Key** (n8n-nodes-langchain).

2. **Dữ liệu chuẩn bị:**
   - **Google Sheet** với cấu trúc cột:
     - `Video ID`, `Title`, `Transcript Link`, `Blog Content`, `Status` (New/Processing/Completed).
   - **YouTube Playlist** cần tự động hóa (cần ID playlist).
   - **WordPress Site** đã cấu hình REST API.
   - **Telegram Channel** để chia sẻ bài viết.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/14758](https://n8n.io/workflows/14758) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON và paste vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **3 phần chính**, các sếp cần cấu hình kỹ lưỡng:

##### **📌 Phần 1: Fetch YouTube Playlist & Transcript**
| Node | Cấu hình cần chú ý |
|------|---------------------|
| **When Fetch Playlist Scheduled** | Thiết lập **lịch trình** (ví dụ: hàng ngày 6h sáng). |
| **Fetch Playlist Items** | Điền **URL Playlist YouTube** và **API Key YouTube**. |
| **Filter New Videos Only** | Cấu hình cột `Video ID` trong Google Sheets để so sánh. |
| **Fetch Transcript via RapidAPI** | Điền **API Key RapidAPI** (nếu dùng dịch vụ ngoài YouTube). |
| **Create Transcript Google Doc** | Chọn **Google Sheet** lưu link transcript và **mô tả file**. |

##### **📌 Phần 2: AI Tạo Nội dung Blog**
| Node | Cấu hình cần chú ý |
|------|---------------------|
| **Blog Post Generator Agent** | Điền **Prompt AI** (ví dụ: *"Tạo bài blog SEO-optimized từ transcript YouTube này, cấu trúc: Title, Introduction, 3 phần nội dung chính, kết luận, từ khóa: [danh sách từ khóa]."*). |
| **Google Gemini Model** | Chọn **Model Gemini Pro** và điền **API Key**. |
| **Fetch Internal Links Tool** | Cấu hình **Google Sheet** chứa danh sách liên kết nội bộ (nếu có). |
| **Parse AI Output** | Node **Code** này cần chỉnh sửa nếu AI trả về format không đúng. |

##### **📌 Phần 3: Publish WordPress & Telegram**
| Node | Cấu hình cần chú ý |
|------|---------------------|
| **Publish to WordPress** | Điền **URL WordPress**, **Username**, **Password API**, và **Slug Prefix** (ví dụ: `blog/`). |
| **Create AI Featured Image** | Chọn **Prompt AI** (ví dụ: *"Tạo hình ảnh đẹp cho bài blog về [chủ đề] với phong cách minimalist, background trắng, font bold."*). |
| **Transform Image to WebP** | Chọn **kích thước** (ví dụ: 1200x630px). |
| **Send to Telegram Channel** | Điền **Telegram Bot Token** và **ID Channel**. |

#### **3. Kích hoạt ⚡️**
- **Test Run:** Chạy **manual trigger** cho phần **Fetch Playlist** và kiểm tra:
  - Transcript có được lưu vào Google Docs không?
  - AI có tạo bài blog không?
  - Bài viết có đăng lên WordPress thành công không?
- **Bật Active:** Sau khi test thành công, bật **Active** cho tất cả **Schedule Trigger**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tối ưu AI Gemini:**
   - Thêm **các constraint** trong prompt để AI trả về format chuẩn (ví dụ: yêu cầu bài viết có **3 phần chính**, **từ khóa SEO**, và **câu hỏi thường gặp**).
   - Sử dụng **LangChain Agent** để AI tự động tham khảo **Google Sheets** nếu thiếu thông tin.

2. **Tự động hóa thêm:**
   - **Gửi báo cáo hàng tuần** về số bài viết được tạo trên Telegram.
   - **Tự động chia sẻ bài viết** trên Facebook/LinkedIn bằng **n8n-nodes-social**.
   - **Lưu log** tất cả quá trình vào **Google Sheets** để theo dõi lỗi.

3. **Cải thiện chất lượng hình ảnh:**
   - Thay thế **AI tạo hình ảnh** bằng **MidJourney API** nếu chất lượng không đáp ứng.
   - Sử dụng **n8n-nodes-image** để **cắt, đen trắng, hoặc thêm watermark**.

---

### 📌 **Kết luận**
Workflow này **giải phóng 80% thời gian** của các sếp trong việc tạo nội dung từ video YouTube, đồng thời **tự động hóa toàn bộ quy trình** từ transcribe → viết bài → đăng tải → chia sẻ. **Không cần code**, chỉ cần cấu hình API và Google Sheets là xong!

**🚀 Hành động ngay:**
1. **Import workflow** và cấu hình API theo hướng dẫn.
2. **Test với 1-2 video** để đảm bảo hoạt động ổn định.
3. **Bật tự động hóa** và **nhận bài blog tự động** hàng ngày!

**💡 Lưu ý:** Nếu gặp lỗi, hãy kiểm tra:
- **Google Sheets** có cấu trúc cột đúng không?
- **API Key** có hết hạn hay không?
- **Prompt AI** có rõ ràng không?

**Chia sẻ workflow này với đồng nghiệp để cùng tự động hóa content marketing!** 🚀