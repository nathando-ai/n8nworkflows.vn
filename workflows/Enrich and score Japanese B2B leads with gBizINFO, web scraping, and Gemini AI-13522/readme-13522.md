---
title: "🚀 Tự động hóa làm giàu và chấm điểm khách hàng tiềm năng B2B Nhật Bản với gBizINFO và Gemini AI"
description: "Hướng dẫn xây dựng workflow n8n tự động tra cứu dữ liệu doanh nghiệp Nhật Bản qua gBizINFO, cào dữ liệu web, chấm điểm qua Google Gemini AI và cảnh báo Hot Lead qua Slack."
slug: "tu-dong-hoa-lam-giau-va-cham-diem-lead-b2b-nhat-ban-n8n"
tags: [n8n, automation, lead-generation, ai, gemini, b2b, japan]
keywords: [n8n workflow, gBizINFO, Gemini AI, B2B lead generation, tự động hóa n8n, chấm điểm lead Nhật Bản]
---

# 🚀 Tự động hóa làm giàu và chấm điểm khách hàng tiềm năng B2B Nhật Bản với gBizINFO và Gemini AI

Việc tìm kiếm và đánh giá khách hàng tiềm năng (Lead Generation) B2B tại thị trường Nhật Bản thường tiêu tốn rất nhiều thời gian của đội ngũ sales. Các sếp phải thủ công tra cứu mã số doanh nghiệp, đọc báo cáo tài chính từ cổng thông tin chính phủ gBizINFO, kiểm tra đánh giá Google Maps, lướt xem website công ty và tự phỏng đoán tiềm năng. Quá trình thủ công này vừa chậm chạp, vừa dễ bỏ lỡ những "khách hàng tiềm năng nóng" (Hot Lead).

Giải pháp hoàn hảo là đây! Workflow n8n này sẽ tự động hóa toàn bộ quy trình: từ việc tiếp nhận thông tin tên công ty/mã số qua form, gọi API chính phủ Nhật Bản, cào dữ liệu web, sử dụng sức mạnh siêu việt của Google Gemini AI để phân tích và chấm điểm, sau đó tự động lưu vào Google Sheets và bắn thông báo nóng hổi lên Slack nếu gặp khách hàng tiềm năng chất lượng cao.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Chỉ cần điền thông tin cơ bản, hệ thống tự động gom dữ liệu đa nguồn từ chính phủ Nhật Bản đến internet.
- **AI thông minh:** Google Gemini AI sẽ phân tích ngữ cảnh, đánh giá quy mô, uy tín và chấm điểm Lead cực kỳ chính xác.
- **Tốc độ chớp nhoáng:** Giảm thời gian nghiên cứu từ 30 phút/lead xuống còn chưa đầy 30 giây.
- **Không bỏ lỡ cơ hội:** Tự động phân loại và gửi cảnh báo ngay lập tức qua Slack khi xuất hiện Hot Lead.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã thiết lập sẵn sàng (Cloud hoặc Self-hosted).
- **gBizINFO API Key:** Tài khoản truy cập cổng thông tin doanh nghiệp Nhật Bản.
- **Google Gemini API Key:** Để sử dụng model AI phân tích và chấm điểm.
- **Google Sheets:** File sẵn sàng để lưu trữ danh sách lead đã làm giàu.
- **Slack Workspace & Webhook:** Để nhận cảnh báo Hot Lead.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy mã JSON của workflow, dán trực tiếp vào giao diện n8n Editor của mình hoặc tạo mới và import file tương ứng.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình chính xác các node cốt lõi sau:

- **Lead Input Form (`formTrigger`):** Thiết lập các trường thông tin đầu vào cơ bản (ví dụ: Tên công ty, Website, Tên người liên hệ...).
- **Corporate Number API & gBizINFO Enrichment (`httpRequest`):** Điền các endpoint API chính phủ Nhật Bản và gắn Header chứa **gBizINFO API Key** để hệ thống gọi dữ liệu đăng ký kinh doanh.
- **Parse Corporate Data, Merge Government Data, Merge Reputation Data, Extract Website Intel & Prepare Final Output (`code`):** Các node xử lý code JavaScript/Python trung gian để làm sạch và gộp dữ liệu. Kiểm tra lại cấu trúc JSON đầu ra cho khớp với bước tiếp theo.
- **Google Maps Reputation & Fetch Company Website (`httpRequest`):** Cấu hình các tham số gọi dữ liệu website công ty và thông tin đánh giá (có thể sử dụng Serper API hoặc tích hợp trực tiếp).
- **Google Gemini Chat Model & AI Lead Scorer (`chainLlm` & `lmChatGoogleGemini`):** 
  - Chọn credential **Google Gemini API**.
  - Tinh chỉnh Prompt trong node AI để yêu cầu Gemini đọc dữ liệu đã gom được, phân tích tiềm năng hợp tác và trả về điểm số kèm lý do chi tiết.
- **Save to Google Sheets (`googleSheets`):** Kết nối tài khoản Google, chọn đúng file Sheet và map các cột dữ liệu (Tên công ty, Điểm AI, Doanh thu, Trạng thái,...) vào các trường tương ứng.
- **Hot Lead Filter (`filter`):** Đặt điều kiện lọc (Ví dụ: Chỉ cho phép các lead có Điểm AI $> 80$ đi qua).
- **Slack Hot Lead Alert (`slack`):** Kết nối Slack Bot/Webhook để bắn tin nhắn chúc mừng và thông tin chi tiết về kênh sales ngay khi có Hot Lead thỏa mãn điều kiện.

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** từng node để kiểm tra dữ liệu trả về không bị lỗi cú pháp.
- Sau khi test run thành công toàn bộ luồng, bật công tắc **Active workflow** ở góc trên bên phải để hệ thống bắt đầu làm việc tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Email tự động:** Nối thêm node Gmail hoặc SendGrid ngay sau chuỗi xử lý để tự động gửi email giới thiệu dịch vụ (đã được AI cá nhân hóa) tới các Hot Lead.
- **Lưu lịch sử vào Database:** Thay vì chỉ lưu Google Sheets, các sếp có thể đồng bộ sang Airtable hoặc PostgreSQL để dễ dàng quản lý CRM lâu dài.
- **Mở rộng kênh thông báo:** Ngoài Slack, có thể tích hợp thêm Telegram Bot để đội ngũ sales nhận thông báo ngay trên điện thoại di động mọi lúc mọi nơi.

### 📌 Kết luận
Workflow "Enrich and score Japanese B2B leads with gBizINFO, web scraping, and Gemini AI" là một cỗ máy tối ưu hóa quy trình sales B2B cực kỳ mạnh mẽ tại thị trường Nhật Bản. Hãy thiết lập ngay hôm nay để giải phóng thời gian cho đội ngũ nhân sự và chốt deal nhanh chóng hơn!