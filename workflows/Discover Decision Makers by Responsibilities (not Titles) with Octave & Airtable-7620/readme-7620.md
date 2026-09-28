---
title: "🚀 Tìm kiếm người ra quyết định thông minh dựa trên trách nhiệm với Octave & Airtable trong n8n"
description: "Tự động hóa quy trình tìm kiếm khách hàng tiềm năng (Prospecting) dựa trên trách nhiệm thực tế thay vì chức danh đơn thuần, giúp đội ngũ Sales và ABM không bỏ lỡ key decision-makers."
slug: "tim-kiem-nguoi-ra-quyet-dinh-voi-octave-airtable"
tags: [n8n, automation, no-code, sales-automation, airtable, octave, lead-generation]
keywords: [n8n workflow, tự động hóa sales, tìm kiếm khách hàng tiềm năng, octave prospector, airtable automation, abm]
---

# 🚀 Tìm kiếm người ra quyết định thông minh dựa trên trách nhiệm với Octave & Airtable

Trong các chiến dịch Account-Based Marketing (ABM) và Sales Outbound, nỗi đau lớn nhất của các SDR (Sales Development Representative) là tìm kiếm khách hàng tiềm năng dựa trên **chức danh (job titles)**. Thực tế, chức danh vô cùng đa dạng và dễ gây bỏ sót. Ví dụ, bạn tìm kiếm "VP of Engineering", nhưng thực tế người quản lý trực tiếp dự án lại có title là "Head of Platform". 

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code, kết hợp giữa **Airtable** và **Octave** giúp định vị chính xác người ra quyết định dựa trên **trách nhiệm thực tế**, loại bỏ hoàn toàn việc tìm kiếm thủ công kém hiệu quả.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý dữ liệu khách hàng mượt mà, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Chính xác cao:** Tìm đúng người dựa trên bối cảnh và trách nhiệm công việc thay vì rà soát chức danh vô hồn.
- **Tiết kiệm 80% thời gian:** Tự động quét và gom danh sách liên hệ từ danh sách tài khoản mục tiêu (Target Accounts) trong Airtable.
- **Tối ưu hóa phễu Sales:** Không bỏ lỡ bất kỳ nhân sự chủ chốt nào ở các doanh nghiệp khách hàng tiềm năng.
- **Đồng bộ liền mạch:** Toàn bộ contacts tìm được sẽ được đẩy ngược lại Airtable để đội ngũ Sales chăm sóc ngay lập tức.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã sẵn sàng hoạt động (Self-hosted hoặc Cloud).
- **Airtable Account:** 
  - Bảng chứa danh sách các tài khoản mục tiêu (`Target Accounts`).
  - Bảng lưu trữ kết quả danh sách liên hệ (`Contact Output Table`).
- **Octave API:** Tài khoản OctaveHQ để sử dụng tính năng AI Prospector Agent.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ mã nguồn JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấp vào biểu tượng menu (3 chấm) ở góc trên bên phải -> Chọn **Import from File / Clipboard** và dán JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 4 nodes chính, các sếp cần cấu hình kỹ các điểm sau:

- **Manual Workflow Trigger:** 
  - Mặc định workflow chạy thủ công khi bấm nút Test. Các sếp có thể thay thế bằng node *Schedule Trigger* để tự động quét danh sách định kỳ (hàng tuần/hàng tháng).
- **Get Target Accounts (Node Airtable):**
  - Chọn Credentials: Kết nối tài khoản Airtable của các sếp (`airtableTokenApi`).
  - Chọn Base và Table chứa danh sách các công ty mục tiêu (`Target Accounts`). Cấu hình operation là `Search`.
- **Discover Relevant Contacts (Node Octave):**
  - Chọn Credentials: Nhập API key của Octave (`octaveApi`).
  - Cấu hình Agent ID và các tiêu chí tìm kiếm (personas, trách nhiệm, cấp bậc tổ chức) để AI tiến hành quét ngữ cảnh phù hợp.
- **Save Discovered Contacts (Node Airtable):**
  - Chọn Credentials: Sử dụng kết nối Airtable.
  - Chọn bảng đích (`Contact Output Table`) để lưu trữ toàn bộ thông tin chi tiết của các contact vừa tìm được từ Octave.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) bằng cách bấm nút ở node *Manual Workflow Trigger* để kiểm tra dòng dữ liệu từ Airtable qua Octave và ghi ngược lại Airtable.
- Sau khi test thành công, gạt công tắc **Active** ở góc trên bên phải để bật workflow chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp thông báo:** Thêm node *Slack* hoặc *Telegram* vào sau bước lưu contact để bắn thông báo ngay về group cho team Sales khi có danh sách lead chất lượng mới.
- **Tích hợp CRM:** Thay vì lưu vào Airtable ở bước cuối, các sếp có thể đổi thành node *HubSpot*, *Salesforce* hoặc *Pipedrive* để đẩy trực tiếp contact vào hệ thống CRM của công ty.
- **Mở rộng nguồn dữ liệu:** Thay thế Airtable bằng Google Sheets hoặc trực tiếp lấy dữ liệu từ các tool quản lý khách hàng hiện có.

### 📌 Kết luận
Việc tìm kiếm khách hàng tiềm năng dựa trên chức danh truyền thống đã lỗi thời. Với sự kết hợp thông minh giữa Octave và Airtable trên n8n, các sếp có thể tự động hóa hoàn toàn khâu nghiên cứu và tìm kiếm decision-makers một cách chuẩn xác nhất. Hãy áp dụng ngay vào quy trình Sales của doanh nghiệp mình thôi nào!