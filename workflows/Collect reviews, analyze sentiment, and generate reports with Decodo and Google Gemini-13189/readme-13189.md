---
title: "🚀 Tự Động Hóa Thu Thập Đánh Giá, Phân Tích Sentiment & Tạo Báo Cáo AI Với Decodo + Google Gemini (N8N)"
description: "Workflow tự động hóa thu thập đánh giá từ Airtable, phân tích cảm xúc bằng AI (Google Gemini), và gửi báo cáo tổng hợp hàng ngày qua email - giúp doanh nghiệp tiết kiệm 10+ giờ/tháng và đưa ra quyết định dựa trên dữ liệu chính xác."
slug: "tự-dộng-hoa-thu-thap-danh-gia-phan-tich-sentiment"
tags: [n8n, automation, ai-summarization, market-research, google-gemini, decodo, airtable, google-sheets]
keywords: [n8n workflow tự động hóa đánh giá, phân tích sentiment AI, thu thập dữ liệu đánh giá, báo cáo tự động hóa doanh nghiệp, google gemini n8n, decodo n8n]
---

# 🚀 **Tự Động Hóa Thu Thập Đánh Giá, Phân Tích Sentiment & Tạo Báo Cáo AI Với Decodo + Google Gemini**

## **Nỗi Đau Của Các Sếp: "Tôi phải mất 5-10 giờ/tuần để thu thập, phân tích và tổng hợp đánh giá khách hàng từ nhiều nguồn!"**
Hàng ngày, các sếp phải:
- **Làm thủ công** tìm kiếm và thu thập đánh giá từ các trang web, email, hoặc Airtable.
- **Phân tích từng đánh giá** để tìm xu hướng tích cực/tiêu cực, mất nhiều thời gian và dễ bị bỏ sót.
- **Tạo báo cáo** để trình lên lãnh đạo, nhưng lại không có cách nào tự động hóa việc này.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Thu thập** đánh giá từ Airtable (hoặc nguồn khác) qua Decodo.
✅ **Phân tích cảm xúc** bằng Google Gemini (AI tiên tiến nhất hiện nay).
✅ **Tạo báo cáo tự động** với xu hướng sentiment, feedback tích cực/tiêu cực.
✅ **Gửi email báo cáo** hàng ngày/tuần cho bạn **không cần làm gì**.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**3 Lợi Ích Cốt Lõi**]
- **Tiết kiệm 10+ giờ/tháng** không phải thu thập và phân tích đánh giá thủ công.
- **Dữ liệu chính xác 100%** nhờ AI tự động trích xuất ngày, điểm số, và nội dung đánh giá.
- **Báo cáo tự động** với sentiment analysis, feedback nổi bật, và đề xuất cải tiến.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI LẮP ĐỘNG**]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản Airtable** (để lưu trữ danh sách link đánh giá).
2. **Google Sheets** (để lưu trữ dữ liệu thu thập được).
3. **Google Gemini API Key** (để phân tích sentiment).
4. **Tài khoản Gmail** (để gửi báo cáo tự động).
5. **API Key của Decodo** (để trích xuất nội dung đánh giá từ URL).

👉 **Nếu chưa có API Key:**
- [Đăng ký Decodo](https://decodo.ai/) (miễn phí cho 100 request/tháng).
- [Mua API Key Google Gemini](https://makersuite.google.com/) (từ 1.5$/1M token).
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/13189](https://n8n.io/workflows/13189) (chọn "Export").
2. **Mở n8n Editor** → Nhấn **"Import"** → Chọn file JSON vừa tải.
3. **Chọn "Import"** để workflow xuất hiện trên canvas.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ mã JSON** từ [n8n.io/workflows/13189](https://n8n.io/workflows/13189) (chọn "Export" → "Copy JSON").
2. **Mở n8n Editor** → Nhấn **"Import"** → Chọn **"Paste JSON"** → Dán và nhấn **"Import"**.

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow được chia thành **2 chu kỳ tự động**:
- **Chu kỳ 1: Thu thập & Lưu trữ** (daily).
- **Chu kỳ 2: Phân tích & Gửi báo cáo** (tuần/Tháng).

#### **🔹 Chu kỳ 1: Thu thập đánh giá từ Airtable**
| **Node**               | **Cần Chỉnh Sửa Gì?** | **Hướng Dẫn** |
|------------------------|-----------------------|----------------|
| **Search records (Airtable)** | ✅ **Credentials** | - Chọn **"airtableOAuth2Api"** (đã cấu hình trước khi import). <br> - Điền **Base ID** và **Table Name** (nơi lưu link đánh giá). <br> - **Filter**: `"Links"` (cột chứa URL đánh giá). |
| **Decodo**             | ✅ **API Key** | - Nhấn **"Add"** → Chọn **"decodo"** (nếu chưa có). <br> - Điền **API Key** từ Decodo. |
| **Loop Over Items**    | ❌ **Không cần chỉnh** | Node này tự động xử lý batch. |
| **Append row in sheet (Google Sheets)** | ✅ **Credentials** | - Chọn **"googleSheetsOAuth2Api"** (đã cấu hình). <br> - Điền **Sheet Name** (ví dụ: `"Reviews_Database"`). <br> - **Headers**: `"Date", "Rating", "ReviewText", "Sentiment"` (cần phải khớp với dữ liệu từ AI). |

#### **🔹 Chu kỳ 2: Phân tích & Gửi báo cáo**
| **Node**               | **Cần Chỉnh Sửa Gì?** | **Hướng Dẫn** |
|------------------------|-----------------------|----------------|
| **Get row(s) in sheet (Google Sheets)** | ✅ **Credentials** | - Chọn **"googleSheetsOAuth2Api"** (cùng credentials với node trước). <br> - **Range**: `"Reviews_Database!A:D"` (lấy toàn bộ sheet). |
| **Google Gemini Chat Model** | ✅ **API Key** | - Chọn **"googlePalmApi"** (đã cấu hình). <br> - **Prompt**: Sử dụng template mặc định (n8n sẽ tự động trích xuất ngày, điểm số, và phân tích sentiment). |
| **AI Agent (Analyzer)** | ❌ **Không cần chỉnh** | Node này tự động xử lý logic phân tích. |
| **Send a message (Gmail)** | ✅ **Credentials** | - Chọn **"gmailOAuth2"** (đã cấu hình). <br> - **To**: Điền email của bạn. <br> - **Subject**: `"Báo cáo Sentiment Đánh Giá - [Ngày]`". <br> - **Body**: Sử dụng template HTML (n8n sẽ tự động điền dữ liệu). |

#### **🔹 Schedule Trigger (Lịch chạy tự động)**
| **Node**               | **Cần Chỉnh Sửa Gì?** | **Hướng Dẫn** |
|------------------------|-----------------------|----------------|
| **Run Daily**          | ✅ **Thời gian chạy** | - Chọn **"Daily"** → Đặt giờ (ví dụ: **8h sáng** để chạy mỗi ngày). |
| **Run Weekly/Monthly** | ✅ **Thời gian báo cáo** | - Chọn **"Cron"** (ví dụ: `"0 0 1 * *"` để chạy hàng tháng ngày 1). |

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** (để kiểm tra logic):
   - Nhấn **"Run Workflow"** trên node **"Run Daily"**.
   - Kiểm tra **Google Sheets** có xuất hiện dữ liệu không?
   - Kiểm tra **Gmail** có nhận được email báo cáo không?

2. **Bật Active**:
   - Sau khi test thành công, nhấn **"Active"** trên node **"Run Daily"** và **"Run Weekly/Monthly"**.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[**CÁCH LÀM ĐẸP HƠN**]
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để thông báo khi có báo cáo mới.
   - **Hướng dẫn**: Sử dụng node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram`.

2. **Lưu log vào Google Sheets**:
   - Thêm node **Google Sheets (Append)** sau **"Send a message"** để lưu lịch sử báo cáo.

3. **Tự động gửi báo cáo cho nhiều người**:
   - Sử dụng node **Gmail (Bcc)** hoặc **Google Drive** để lưu bản sao báo cáo.

4. **Cập nhật sentiment real-time**:
   - Thêm node **Webhook** để nhận dữ liệu mới từ khách hàng và phân tích ngay lập tức.
:::

---

## 📌 **Kết Luận: Hãy Tự Động Hóa Ngay Hôm Nay!**
Workflow này **giải phóng bạn khỏi công việc thủ công** và đưa ra **báo cáo sentiment chính xác** mỗi ngày. Bằng cách kết hợp **Airtable, Decodo, Google Gemini và Gmail**, bạn có thể:
✔ **Tiết kiệm 10+ giờ/tháng**.
✔ **Nhận dữ liệu phân tích AI chất lượng cao**.
✔ **Quản lý feedback khách hàng một cách chuyên nghiệp**.

**👉 Bắt đầu ngay bằng cách import workflow và cấu hình theo hướng dẫn trên!**
Nếu có vấn đề, hãy để lại comment dưới đây hoặc liên hệ với **Zain Khan** (tác giả) qua [LinkedIn](https://www.linkedin.com/in/zainkhan/) để hỗ trợ.

---
:::note[**LƯU Ý CUỐI CUNG**]
- **N8N Self-hosted** chạy ổn định hơn Cloud (tránh gián đoạn).
- 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
- 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::