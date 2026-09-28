---
title: "🚀 Tự động tạo danh sách khách hàng tiềm năng trên Google Maps với SerpApi, Google Gemini và Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động tìm kiếm, phân tích và lưu trữ lead chất lượng cao từ Google Maps sử dụng AI Gemini và SerpApi."
slug: "tao-danh-sach-lead-google-maps-serpapi-gemini-sheets"
tags: [n8n, automation, no-code, lead-generation, ai, google-maps, google-sheets]
keywords: [n8n workflow, tạo lead google maps, serpapi n8n, google gemini ai, tự động hóa lead generation, google sheets automation]
---

# 🚀 Tự động tạo danh sách khách hàng tiềm năng trên Google Maps với SerpApi, Google Gemini và Google Sheets

Việc tìm kiếm và tổng hợp danh sách khách hàng tiềm năng (Lead Generation) thủ công trên Google Maps thường tốn rất nhiều thời gian và công sức: vừa phải tìm kiếm từng khu vực, vừa phải copy-paste thông tin tên, địa chỉ, số điện thoại, đánh giá của từng doanh nghiệp vào file Excel. 

Workflow n8n này sẽ giúp các sếp giải quyết triệt để bài toán trên bằng cách tự động hóa 100%: từ việc nhận yêu cầu tìm kiếm qua Form, gọi API lấy dữ liệu từ Google Maps, sử dụng AI thông minh (Google Gemini) để phân tích, tổng hợp và lưu thẳng kết quả vào Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Chỉ cần nhập từ khóa và khu vực vào Form, hệ thống sẽ tự động trả về danh sách lead sạch.
- **Sức mạnh AI Gemini:** Trợ lý AI giúp lọc, phân loại và đánh giá mức độ tiềm năng của doanh nghiệp dựa trên dữ liệu thu thập được.
- **Đồng bộ thời gian thực:** Toàn bộ thông tin chi tiết của khách hàng được cập nhật tự động vào Google Sheets để đội ngũ Sales gọi điện/chăm sóc ngay.
- **Tiết kiệm 90% thời gian:** Thay vì mất hàng giờ tìm kiếm thủ công, các sếp chỉ mất vài giây để có hàng chục/hàng trăm lead chất lượng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **SerpApi Account:** Lấy API Key để crawl dữ liệu từ Google Maps.
- **Google Gemini API Key:** Dành cho các node AI Agent phân tích dữ liệu.
- **Google Sheets:** Tài khoản Google để cấu hình node lưu trữ dữ liệu lead.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn hoặc copy toàn bộ mã nguồn JSON của workflow.
- Trong giao diện n8n Editor, bấm vào **Add workflow** -> Chọn **Import from File** hoặc dán trực tiếp (Paste) vào màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần chú ý cấu hình kỹ các node trọng điểm sau:
- **Form Trigger (`formTrigger`):** Điền các trường thông tin đầu vào mà các sếp muốn người dùng nhập (Ví dụ: Ngành nghề, Khu vực, Số lượng cần tìm...).
- **HTTP Request (`httpRequest` - SerpApi):** Cấu hình kết nối tới SerpApi để tìm kiếm địa điểm trên Google Maps. Các sếp cần nhập SerpApi Key và map các tham số `q` (Query) từ dữ liệu đầu vào của Form.
- **Google Gemini Agent (`@n8n/n8n-nodes-langchain.agent` & `lmChatGoogleGemini`):** Thêm Credentials cho Google Gemini, viết Prompt hướng dẫn AI cách đọc dữ liệu thô từ SerpApi, lọc và trích xuất các thông tin quan trọng (Tên doanh nghiệp, Địa chỉ, Số điện thoại, Website, Đánh giá...).
- **Google Sheets (`googleSheets`):** Kết nối tài khoản Google của các sếp, chọn đúng File Google Sheets và Sheet Name đã chuẩn bị sẵn để hệ thống ghi dữ liệu lead vào đúng cột.
- **Các node xử lý dữ liệu (`code`, `filter`, `sort`, `limit`, `splitOut`, `aggregate`, `set`):** Giúp làm sạch dữ liệu, loại bỏ các kết quả trùng lặp hoặc không hợp lệ trước khi đẩy lên Google Sheets.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và thử điền thông tin vào Form test để kiểm tra luồng chạy của dữ liệu qua từng node.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để đưa workflow vào trạng thái chạy chính thức (Production).

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối workflow để bắn thông báo ngay về nhóm chat khi có một danh sách lead mới vừa được tìm kiếm và lưu xong.
- **Gửi Email tự động:** Kết hợp thêm node Gmail để tự động gửi thư giới thiệu dịch vụ tới các lead có đính kèm website hoặc email trong danh sách.
- **Lên lịch định kỳ (Cron):** Thay vì dùng Form Trigger thủ công, các sếp có thể thay thế bằng Schedule Trigger để tự động quét lead cho các khu vực/ngành nghề mới mỗi tuần.

### 📌 Kết luận
Workflow tạo danh sách lead Google Maps kết hợp SerpApi và Google Gemini là một "vũ khí" tối ưu giúp đội ngũ Sales và Marketing tự động hóa hoàn toàn khâu tìm kiếm khách hàng tiềm năng. Hãy triển khai ngay hôm nay để tối ưu hóa năng suất cho doanh nghiệp của các sếp!