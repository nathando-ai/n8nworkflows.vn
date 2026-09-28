---
title: "🚀 Tự Động Hóa Nhận Feedback Hội Thảo qua Form + Lưu Excel OneDrive + Thông Báo Outlook (Không Code)"
description: "Workflow tự động hóa thu thập phản hồi hội thảo từ form, ghi dữ liệu vào Excel OneDrive và gửi thông báo qua Outlook - tiết kiệm thời gian, giảm sai sót, tối ưu quản lý."
slug: "tu-dong-hoa-nhan-feedback-hoi-thao-form-excel-onedrive-outlook"
tags: [n8n, automation, marketing, microsoft-excel, microsoft-outlook, one-drive, no-code]
keywords: [n8n workflow feedback hội thảo, tự động hóa nhận phản hồi, lưu dữ liệu Excel OneDrive, thông báo Outlook tự động, tự động hóa marketing]
---

# 🚀 Tự Động Hóa Nhận Feedback Hội Thảo qua Form + Lưu Excel OneDrive + Thông Báo Outlook

### 📌 **Nỗi Đau Của Các Sếp**
Các sếp thường phải:
- **Làm thủ công** thu thập phản hồi sau hội thảo qua Google Form, Typeform hay các công cụ khác.
- **Sao chép dữ liệu** vào Excel để lưu trữ, dễ gây lỗi và mất thời gian.
- **Quên thông báo** cho đội ngũ hỗ trợ khi có phản hồi mới, dẫn đến trễ xử lý.
- **Không theo dõi được** phản hồi theo thời gian thực, ảnh hưởng đến cải tiến sản phẩm/dịch vụ.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ Thu thập phản hồi từ form (Google Form, Typeform, hoặc form n8n).
✅ Lưu dữ liệu vào **Excel OneDrive** (không cần tải xuống/tải lên thủ công).
✅ **Gửi thông báo qua Outlook** cho đội ngũ hỗ trợ khi có phản hồi mới.
✅ **Tự động append** dữ liệu mới vào file Excel đã tồn tại (không xóa dữ liệu cũ).

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần sao chép dữ liệu từ form sang Excel.
- **Chính xác 100%**: Dữ liệu tự động append vào file Excel, không sai sót.
- **Hoạt động 24/7**: Thông báo phản hồi mới ngay lập tức qua email.
- **Dữ liệu tập trung**: Tất cả phản hồi được lưu trong **Excel OneDrive**, dễ dàng theo dõi và phân tích.
- **Cải tiến liên tục**: Đội ngũ hỗ trợ được thông báo kịp thời để xử lý phản hồi.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Microsoft 365** (để sử dụng OneDrive, Excel và Outlook).
2. **API Key/Credentials** cho:
   - **Microsoft OneDrive OAuth2** (để tìm và append file Excel).
   - **Microsoft Excel OAuth2** (để ghi dữ liệu vào file).
   - **Microsoft Outlook OAuth2** (để gửi email thông báo).
3. **File Excel mẫu** đã tồn tại trên OneDrive (để lưu trữ phản hồi).
4. **Form thu thập phản hồi** (có thể là Google Form, Typeform, hoặc form n8n).
5. **Địa chỉ email** của đội ngũ hỗ trợ (để nhận thông báo).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/4389](https://n8n.io/workflows/4389) (hoặc copy JSON từ link trên).
- **Mở n8n Editor** (self-hosted hoặc n8n.cloud) → **Import Workflow** → Dán JSON và nhấn **Import**.

:::note[Lưu ý]
- Nếu sử dụng **n8n.cloud**, các sếp cần **nâng cấp plan** để hỗ trợ Microsoft 365 nodes.
- Đối với **self-hosted**, các sếp nên cài **n8n trên VPS** để workflow hoạt động 24/7.
:::

---

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **3 phần quan trọng** cần cấu hình kỹ:

##### **A. Cấu Hình Form Thu thập Phản hồi**
- Node **"On form submission"** (formTrigger) cần kết nối với form của các sếp.
  - **Lựa chọn loại form**:
    - **Google Form**: Sử dụng node `n8n-nodes-base.googleSheets` (thêm vào workflow).
    - **Typeform**: Sử dụng node `n8n-nodes-base.typeform`.
    - **Form n8n**: Sử dụng node `n8n-nodes-base.formTrigger` (đã có trong workflow).
  - **Cấu hình**:
    - Điền **URL của form** (ví dụ: `https://docs.google.com/forms/d/e/...`).
    - Chọn **fields** (cột) cần thu thập (ví dụ: `Name`, `Email`, `Feedback`).

##### **B. Cấu Hình OneDrive & Excel**
- Node **"Search Document"** (microsoftOneDrive):
  - **Credentials**: Chọn `microsoftOneDriveOAuth2Api` (đã cấu hình trước).
  - **Query**: Điền tên file Excel mẫu (ví dụ: `Feedback_HoiThao_2024.xlsx`).
  - **Lưu ý**:
    - File Excel **phải tồn tại trên OneDrive** trước khi chạy workflow.
    - Nếu file không tìm thấy, workflow sẽ **tạo file mới** (nhưng không append dữ liệu).

- Node **"Append Data"** (microsoftExcel):
  - **Credentials**: Chọn `microsoftExcelOAuth2Api`.
  - **Sheet Name**: Điền tên sheet trong file Excel (ví dụ: `Sheet1`).
  - **Header Row**: Chọn `true` (để append dữ liệu dưới header).
  - **Lưu ý**:
    - **Không chỉnh sửa tên sheet** trong file Excel mẫu, trừ khi cập nhật trong node này.

##### **C. Cấu Hình Email Thông Báo (Outlook)**
- Node **"Notify Support"** (microsoftOutlook):
  - **Credentials**: Chọn `microsoftOutlookOAuth2Api`.
  - **Email Settings**:
    - **Subject**: Cập nhật nội dung (ví dụ: `"Phản hồi mới từ Hội thảo [Tên Hội thảo]"`).
    - **Body**: Sử dụng **template** trong node `Code` (xem phần dưới).
      - **Cấu trúc email mẫu**:
        ```plaintext
        Xin chào đội ngũ hỗ trợ,

        Có phản hồi mới từ hội thảo:
        - Tên: {{ $node["Parse Data"].json["name"] }}
        - Email: {{ $node["Parse Data"].json["email"] }}
        - Nội dung: {{ $node["Parse Data"].json["feedback"] }}

        Xin vui lòng xử lý kịp thời.
        Trân trọng,
        Đội ngũ tổ chức
        ```
    - **To**: Điền email của đội ngũ hỗ trợ (ví dụ: `support@doanhnghiep.com`).

##### **D. Node "Code" (Tùy Chỉnh Email)**
- Node **"Code"** (type: code) sử dụng **JavaScript** để định dạng email.
  - **Mã mặc định**:
    ```javascript
    $input.all().forEach((item) => {
      item.json = {
        subject: `Phản hồi mới từ Hội thảo: ${item.json.name}`,
        body: `Xin chào đội ngũ hỗ trợ,\n\nCó phản hồi mới từ hội thảo:\n- Tên: ${item.json.name}\n- Email: ${item.json.email}\n- Nội dung: ${item.json.feedback}\n\nXin vui lòng xử lý kịp thời.\nTrân trọng,\nĐội ngũ tổ chức`
      };
    });
    ```
  - **Lưu ý**:
    - **Không thay đổi logic** của node này trừ khi các sếp biết code.
    - Nếu muốn **thêm/diệt các field**, cập nhật trong `item.json`.

---

#### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Run Workflow** và điền thông tin phản hồi vào form.
   - Kiểm tra:
     - Dữ liệu có được append vào Excel OneDrive không?
     - Email thông báo có được gửi không?
2. **Bật Active**:
   - Sau khi test thành công, chuyển **Active** sang `true`.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Gửi thông báo Slack/Telegram**:
   - Thêm node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram` sau node `Notify Support` để gửi thông báo đến kênh nhóm.

2. **Lưu log hoạt động**:
   - Thêm node `n8n-nodes-base.googleSheets` (hoặc `microsoftOneDrive`) để lưu **log hoạt động** (thời gian, người gửi, trạng thái xử lý).

3. **Phân loại phản hồi tự động**:
   - Sử dụng node `n8n-nodes-base.if` hoặc `n8n-nodes-base.code` để **phân loại phản hồi** (ví dụ: "Tốt", "Không tốt", "Yêu cầu cải tiến") và gửi đến các nhóm khác nhau.

4. **Gửi báo cáo định kỳ**:
   - Tạo workflow riêng để **tổng hợp dữ liệu Excel** và gửi báo cáo qua email (sử dụng node `n8n-nodes-base.email` hoặc `microsoftOutlook`).

5. **Tích hợp với CRM**:
   - Nếu sử dụng **HubSpot, Salesforce**, thêm node tương ứng để **tự động thêm phản hồi vào CRM**.
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc thủ công, đồng thời **tối ưu hóa quản lý phản hồi hội thảo** với tính tự động hóa cao. Bằng cách kết hợp **form thu thập dữ liệu**, **Excel OneDrive** và **thông báo Outlook**, các sếp có thể:
✔ **Tiết kiệm thời gian** lên đến **50%** trong việc xử lý phản hồi.
✔ **Giảm sai sót** do sao chép dữ liệu.
✔ **Cải thiện trải nghiệm khách hàng** bằng phản hồi kịp thời.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn trên.
2. **Test với dữ liệu mẫu** trước khi kích hoạt.
3. **Mở rộng** với các tính năng nâng cao như gửi Slack hoặc tích hợp CRM.

**🎁 Đăng ký VPS TinoHost để self-host n8n ổn định 24/7:**
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

---