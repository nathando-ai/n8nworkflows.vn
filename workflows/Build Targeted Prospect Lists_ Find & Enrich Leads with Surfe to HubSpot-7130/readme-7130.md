---
title: "🚀 Tự Động Hóa Tìm Kiếm & Làm Giàu Dữ Liệu Khách Hàng Tiềm Năng Với Surfe & HubSpot"
description: "Workflow n8n giúp các sếp tự động tìm kiếm doanh nghiệp theo ICP, làm giàu dữ liệu cá nhân (email, SĐT) qua Surfe API và đồng bộ trực tiếp vào HubSpot CRM chỉ trong vài phút."
slug: "tu-dong-tim-kiem-lam-giau-du-lieu-lead-surfe-hubspot"
tags: [n8n, lead-generation, surfe, hubspot, crm-automation, b2b-sales]
keywords: [n8n workflow, tìm kiếm lead, làm giàu dữ liệu khách hàng, Surfe API, HubSpot CRM, tự động hóa bán hàng]
---

# 🚀 Tự Động Hóa Tìm Kiếm & Làm Giàu Dữ Liệu Khách Hàng Tiềm Năng Với Surfe & HubSpot

Trong môi trường B2B cạnh tranh khốc liệt, việc tìm kiếm khách hàng tiềm năng (Leads) chất lượng cao luôn là bài toán nan giải. Các sếp thường mất hàng giờ mỗi ngày để lướt LinkedIn, Google Maps, hay các trang danh bạ doanh nghiệp để tìm ra những người đúng vai trò (ICP - Ideal Customer Profile). Sau đó, lại phải tốn thêm thời gian để "săn" email và số điện thoại của họ, một quy trình thủ công, dễ sai sót và cực kỳ tốn kém nguồn lực.

Workflow n8n này chính là "vũ khí bí mật" giúp các sếp giải quyết triệt để vấn đề đó. Bằng cách kết hợp sức mạnh của **Surfe API** (chuyên gia trong việc tìm kiếm và làm giàu dữ liệu doanh nghiệp) với **HubSpot CRM**, quy trình này tự động hóa hoàn toàn từ khâu tìm kiếm công ty, xác định nhân sự chủ chốt, làm giàu thông tin liên lạc (email, SĐT) cho đến khi dữ liệu sạch sẽ nằm gọn trong hệ thống CRM của bạn. Không cần code, không cần copy-paste thủ công, chỉ cần một cú click.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, đặc biệt khi cần xử lý lượng lớn dữ liệu hoặc chạy theo lịch (schedule), các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian tìm kiếm:** Quy trình từ tìm kiếm công ty đến có email/SĐT diễn ra tự động trong vài phút thay vì hàng giờ.
- **Dữ liệu chính xác & mới nhất:** Surfe API đảm bảo dữ liệu liên lạc được xác thực, giảm thiểu tỷ lệ email bounce (lỗi gửi).
- **Tích hợp liền mạch với HubSpot:** Lead được tạo mới hoặc cập nhật tự động trong CRM, sẵn sàng cho đội sales tiếp cận ngay lập tức.
- **Cá nhân hóa quy trình:** Dễ dàng chỉnh đổi tiêu chí tìm kiếm (ngành nghề, vị trí, quy mô công ty) để phù hợp với chiến lược bán hàng cụ thể.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị các tài khoản và credentials sau:
1. **Tài khoản n8n:** Bản self-hosted hoặc cloud.
2. **Tài khoản Surfe:** Đăng ký tại [Surfe.com](https://www.surfe.com) và lấy **API Key**.
3. **Tài khoản HubSpot:** Có quyền truy cập vào CRM để tạo/cập nhật Contact. Cần **Private App Token** hoặc **OAuth2 Credentials**.
4. **Tài khoản Gmail:** (Tùy chọn) Nếu muốn nhận báo cáo kết quả qua email. Cần cấu hình OAuth2 cho Gmail.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow từ link gốc hoặc copy toàn bộ mã JSON.
2. Mở n8n Editor, chọn **Import from URL** hoặc **Import from File**.
3. Dán JSON vào và nhấn **Import**. Workflow sẽ hiển thị với 13 nodes chính.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Đây là phần quan trọng nhất. Các sếp cần cấu hình kỹ các node sau để workflow hoạt động đúng ý đồ:

**A. Node `Search ICP Companies` (HTTP Request)**
- **Mục đích:** Tìm kiếm danh sách công ty phù hợp với ICP.
- **Cấu hình:**
  - Chọn **Surfe API Key** trong phần Authentication.
  - Trong phần **Body/JSON**, các sếp cần chỉnh sửa các tham số tìm kiếm như:
    - `industry`: Ngành nghề (ví dụ: "SaaS", "Retail").
    - `location`: Khu vực địa lý.
    - `company_size`: Quy mô công ty.
    - `keywords`: Từ khóa đặc thù.
  - *Lưu ý:* Tham khảo tài liệu Surfe API để biết chính xác các trường dữ liệu hỗ trợ.

**B. Node `prepare JSON PAYLOAD WITH Company Domains` (Code)**
- **Mục đích:** Xử lý dữ liệu từ bước tìm kiếm công ty để chuẩn bị cho bước tìm người.
- **Cấu hình:** Kiểm tra logic code để đảm bảo nó trích xuất đúng `domain` hoặc `company_id` từ response của Surfe.

**C. Node `Search People in Companies` (HTTP Request)**
- **Mục đích:** Tìm kiếm nhân sự (Decision Makers) trong các công ty đã tìm được.
- **Cấu hình:**
  - Tiếp tục dùng **Surfe API Key**.
  - Chỉnh sửa Body để chỉ định các vị trí cần tìm (ví dụ: "CEO", "CTO", "Head of Sales").

**D. Node `Prepare JSON Payload Enrichment Request` (Code)**
- **Mục đích:** Gom nhóm dữ liệu nhân sự để gửi yêu cầu làm giàu (enrichment) email/SĐT.
- **Cấu hình:** Đảm bảo code xử lý đúng format mà Surfe Bulk Enrichments API yêu cầu.

**E. Node `Surfe Bulk Enrichments API` & `Surfe check enrichement status` (HTTP Request)**
- **Mục đích:** Gửi yêu cầu làm giàu dữ liệu và kiểm tra trạng thái xử lý.
- **Cấu hình:**
  - Dùng **Surfe API Key**.
  - Node `Surfe check enrichement status` sẽ chạy lặp lại (kết hợp với node `Wait 3 secondes` và `Is enrichment complete ?`) cho đến khi dữ liệu sẵn sàng.

**F. Node `Extract list of peoples from Surfe API response` (Code)**
- **Mục đích:** Phân tích response từ Surfe, tách ra danh sách người có email/SĐT hợp lệ.
- **Cấu hình:** Kiểm tra logic lọc dữ liệu để đảm bảo chỉ lấy những record có thông tin liên lạc đầy đủ.

**G. Node `Filter: phone AND email` (Filter)**
- **Mục đích:** Lọc lại lần cuối để đảm bảo lead có cả email và số điện thoại (hoặc theo tiêu chí các sếp muốn).
- **Cấu hình:** Chỉnh điều kiện lọc nếu cần (ví dụ: chỉ cần email, hoặc chỉ cần SĐT).

**H. Node `HubSpot: Create or Update` (HubSpot)**
- **Mục đích:** Đẩy dữ liệu lead vào HubSpot CRM.
- **Cấu hình:**
  - Chọn **HubSpot Credentials** (OAuth2 hoặc Private App Token).
  - Mapping các trường dữ liệu từ Surfe (First Name, Last Name, Email, Phone, Company Name, Job Title...) vào các trường tương ứng trong HubSpot.
  - Chọn chế độ **Create or Update** để tránh trùng lặp lead.

**I. Node `Gmail` (Gmail) - Tùy chọn**
- **Mục đích:** Gửi email báo cáo cho các sếp khi workflow hoàn tất.
- **Cấu hình:**
  - Chọn **Gmail Credentials**.
  - Điền email người nhận.
  - Chỉnh sửa nội dung email để tóm tắt số lượng lead mới tìm được.

#### 3. Kích hoạt ⚡️
1. **Test Run:** Nhấn nút **Execute Workflow** (Manual Trigger).
   - Quan sát từng node xem dữ liệu có chảy đúng không.
   - Kiểm tra xem Surfe có trả về dữ liệu không và HubSpot có nhận được lead không.
2. **Bật Active:** Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải.
3. **Chạy theo lịch (Tùy chọn):** Các sếp có thể thêm node **Schedule Trigger** thay thế cho Manual Trigger để workflow tự động chạy hàng ngày/tuần.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram:** Thay vì chỉ gửi Gmail, các sếp có thể thêm node Slack hoặc Telegram để nhận thông báo lead mới ngay trên điện thoại, giúp phản hồi nhanh hơn.
- **Lưu Log vào Google Sheets:** Thêm node Google Sheets để lưu lại lịch sử các lead đã tìm kiếm, giúp theo dõi hiệu quả chiến dịch và tránh trùng lặp trong các lần chạy sau.
- **Phân loại Lead (Scoring):** Sử dụng node Code hoặc HubSpot Custom Fields để chấm điểm lead dựa trên các tiêu chí (ví dụ: công ty lớn hơn 100 nhân viên = điểm cao hơn) để đội sales ưu tiên liên hệ.
- **Tự động gửi Email Outreach:** Sau khi lead vào HubSpot, các sếp có thể nối tiếp workflow này với một workflow khác để tự động gửi email chào hàng cá nhân hóa, tạo thành quy trình Lead-to-Deal hoàn chỉnh.

### 📌 Kết luận
Việc tìm kiếm và làm giàu dữ liệu khách hàng tiềm năng không còn là gánh nặng nếu các sếp biết tận dụng sức mạnh của tự động hóa. Workflow kết hợp Surfe và HubSpot này giúp các sếp tập trung vào việc bán hàng và xây dựng quan hệ, thay vì lãng phí thời gian vào các tác vụ hành chính lặp đi lặp lại. Hãy import workflow, cấu hình theo hướng dẫn và bắt đầu xây dựng pipeline khách hàng chất lượng cao ngay hôm nay!