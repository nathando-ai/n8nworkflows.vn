---
title: "🚀 Phân tích tính cách khách hàng tự động với BaZi, DISC, Thần số học bằng n8n và Gemini AI"
description: "Tự động hóa hoàn toàn quy trình phân tích khách hàng tiềm năng qua Thần số học, BaZi, và DISC bằng Gemini AI kết hợp Google Sheets, giúp sales chốt đơn mượt mà."
slug: "phan-tich-tinh-cach-khach-hang-bazi-disc-than-so-hoc-gemini-n8n"
tags: [n8n, automation, no-code, gemini-ai, google-sheets, lead-generation, ai-integration]
keywords: [n8n workflow, phân tích tính cách khách hàng, bazi, disc, thần số học, gemini ai, google sheets automation]
---

# 🚀 Tự Động Hóa Phân Tích Tính Cách Khách Hàng (BaZi, DISC, Thần Số Học) Với Gemini & Google Sheets

Các sếp có bao giờ đau đầu khi đội ngũ Sales phải mất hàng giờ nghiên cứu thông tin, sở thích, ngày sinh của khách hàng tiềm năng (Leads) để tìm ra cách tiếp cận phù hợp, nhưng kết quả lại hên xui và mất thời gian? 

Việc thấu hiểu tâm lý khách hàng qua các hệ thống khoa học hành vi như **DISC**, **Thần số học (Numerology)** hay **Tứ Trụ (BaZi)** là "vũ khí tối thượng" trong sales. Tuy nhiên, làm thủ công cho hàng trăm khách hàng là điều bất khả thi. 

Giải pháp cho các sếp đây: Workflow n8n tự động hóa 100% việc đọc dữ liệu từ **Google Sheets**, tính toán các chỉ số tâm lý/nhân tướng học, dùng **Google Gemini AI** để phân tích sâu sắc, sau đó tự động viết kịch bản chốt sale (Sales Script) cá nhân hóa cho từng khách hàng và đồng bộ ngược lại Google Sheets. Không cần code, setup một lần chạy mãi mãi!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100%:** Ngay khi có khách hàng mới điền form vào Google Sheets, hệ thống tự động kích hoạt phân tích.
- **Phân tích đa chiều:** Kết hợp hoàn hảo giữa BaZi (Tứ Trụ), Thần số học và mô hình hành vi DISC nhờ sức mạnh của Gemini AI.
- **Cá nhân hóa kịch bản Sales:** Tự động tạo ra kịch bản tư vấn riêng biệt phù hợp với tính cách từng khách hàng, giúp tăng tỷ lệ chuyển đổi (conversion rate) lên mức cao nhất.
- **Lưu trữ khoa học:** Mọi kết quả phân tích và kịch bản đều được cập nhật thẳng vào Google Sheets để đội ngũ sales dễ dàng truy xuất.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn:
1. **Hệ thống n8n:** Đã cài đặt sẵn sàng (Self-hosted hoặc n8n Cloud).
2. **Google Sheets:** Một file Google Sheet chứa thông tin khách hàng (Họ tên, Ngày tháng năm sinh...).
3. **Google Gemini API Key:** Tài khoản Google AI Studio để kết nối với các node Google Gemini.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này (hoặc tải file JSON từ nguồn) và import trực tiếp vào n8n Editor của mình bằng tính năng **Import from File / Paste JSON**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 21 nodes hoạt động nhịp nhàng, các sếp cần chú ý cấu hình kỹ các điểm sau:
- **Google Sheets Trigger:** Kết nối tài khoản Google của các sếp và trỏ tới đúng file Google Sheets chứa dữ liệu khách hàng, chọn đúng Trigger khi có dòng mới được thêm/cập nhật.
- **Node tính toán (Compute Bazi & Compute Numerology):** Sử dụng node `code` (JavaScript/Python) để thực hiện các thuật toán băm ngày tháng năm sinh ra chỉ số gốc. Kiểm tra lại logic đầu vào/đầu ra cho khớp với cột trong Google Sheets của các sếp.
- **Các node AI (Numerology Analysis, Bazi Analysis, DISC Analysis, Summary Customer Insight, Writing Script for Salers):** 
  - Chọn credential **Google Gemini** và điền API Key.
  - Tinh chỉnh system prompt trong từng node Gemini nếu muốn AI nói theo giọng văn (tone of voice) phù hợp với sản phẩm/dịch vụ bên mình.
- **Các node Update row (Update row in sheet, sheet1, sheet2...):** Map lại các trường dữ liệu (Fields) mà AI trả về với đúng các cột tương ứng trong Google Sheets (ví dụ: Cột *DISC Profile*, Cột *Bazi Result*, Cột *Sales Script*...).

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và test thử với 1 dòng dữ liệu mẫu trong Google Sheets để kiểm tra xem luồng chạy qua các node Code, Merge, Filter, Split in Batches và Gemini có mượt mà không.
- Sau khi test thành công, bật nút **Active** ở góc trên bên phải để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node **Telegram** hoặc **Slack** ngay sau node *Writing Script for Salers* để bắn ngay kịch bản chốt sale và phân tích tính cách về thẳng điện thoại cho sale phụ trách khách hàng đó.
- **Lưu lịch sử:** Thêm một bảng log phụ trong Google Sheets hoặc database ngoại vi để lưu lại lịch sử các lần tương tác.
- **Mở rộng mô hình:** Ngoài DISC, các sếp có thể yêu cầu Gemini phân tích thêm các mô hình nhân sự khác như MBTI hay Enneagram tùy theo đặc thù ngành hàng (B2B hay B2C).

### 📌 Kết luận
Việc thấu hiểu tâm lý khách hàng từ giây đầu tiên chưa bao giờ dễ dàng và tự động đến thế. Hãy ứng dụng ngay workflow này vào hệ thống CRM/Google Sheets của doanh nghiệp để giải phóng sức lao động cho đội ngũ sale và bứt phá doanh thu ngay hôm nay!