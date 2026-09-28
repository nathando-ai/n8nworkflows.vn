---
title: "📊 Tự Động Hóa Báo Cáo Phân Tích Giữ Nhân Sự với GPT-4o & Email Tóm Tắt Hàng Tuần (N8N + AI)"
description: "Workflow tự động hóa hoàn toàn không cần code để phân tích dữ liệu nhân sự, tính điểm giữ chân nhân viên, và gửi báo cáo định kỳ với GPT-4o qua email. Giúp các sếp tiết kiệm 10+ giờ/tháng, phát hiện xu hướng giữ chân nhân viên, và đưa ra quyết định dựa trên dữ liệu chính xác."
slug: "tieu-dong-hoa-bao-cao-phan-tich-giu-nhan-su-gpt-4o-email"
tags: [n8n, automation, no-code, ai-driven, google-sheets, gmail, azure-openai, retention-analytics]
keywords: [tự động hóa nhân sự n8n, phân tích giữ chân nhân viên, báo cáo AI GPT-4o, email tự động hóa doanh nghiệp, workflow n8n google sheets]
---

# 🚀 **Tự Động Hóa Báo Cáo Phân Tích Giữ Nhân Sự với GPT-4o & Email (N8N + AI)**

### **Nỗi Đau Của Các Sếp: Phân Tích Dữ Liệu Nhân Sự Thủ Công Làm Mất Thời Gian & Chưa Chính Xác**
Hàng tuần, các sếp phải:
- **Lấy dữ liệu** từ Google Sheets về nhân viên mới, thời gian ở lại, và đặc điểm cá nhân.
- **Tính toán thủ công** điểm giữ chân (retention score) dựa trên các yếu tố như kỹ năng, văn hóa công ty, hoặc phản hồi đánh giá.
- **Viết báo cáo** tóm tắt xu hướng, điểm mạnh/điểm yếu của đội ngũ.
- **Gửi email** cho ban lãnh đạo với dữ liệu chưa được tối ưu hóa, mất thời gian và dễ bị lỗi.

**Kết quả?** Dữ liệu không được cập nhật kịp thời, quyết định dựa trên cảm nhận chứ không phải dữ liệu, và công việc phân tích chiếm đến **10+ giờ/tháng** của các sếp.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
Sau khi triển khai workflow này, các sếp sẽ:
✅ **Tiết kiệm 10+ giờ/tháng** bằng cách loại bỏ công việc thủ công.
✅ **Nhận báo cáo tự động hóa** với phân tích sâu về xu hướng giữ chân nhân viên (top traits giữ chân, yếu tố làm nhân viên rời đi).
✅ **Được cung cấp 3 gợi ý cụ thể** về cách cải thiện mô tả công việc (Job Description) để thu hút và giữ chân nhân viên.
✅ **Dữ liệu chính xác 100%**, không bị sai sót như khi nhập thủ công.
✅ **Hoạt động 24/7**, không phụ thuộc vào thời gian làm việc của ai.

---
### **🔧 Yêu Cầu Cần Thiết**
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** với 2 bảng dữ liệu:
   - **Bảng "Hires Tracking"**: Gồm thông tin nhân viên (tên, vai trò, đặc điểm, ngày bắt đầu làm việc, trạng thái giữ chân).
   - **Bảng "Retention Summary"**: Gồm thống kê tổng hợp về các đặc điểm (trait) ảnh hưởng đến việc giữ chân (ví dụ: "Kỹ năng mềm", "Phù hợp văn hóa", "Mức lương").
2. **Tài khoản Gmail** để gửi báo cáo tự động hàng tuần.
3. **API Key Azure OpenAI** (mô hình **gpt-4o-mini**) để xử lý logic AI.
4. **Thiết lập OAuth2** cho:
   - Google Sheets (để đọc/ghi dữ liệu).
   - Gmail (để gửi email).

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/9236](https://n8n.io/workflows/9236) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/9236) và dán vào **Import Workflow** trong n8n.
- **Cách 3**: Sử dụng **n8n CLI** để import:
  ```bash
  n8n import workflow.json --name "Retention Analytics"
  ```

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này gồm **10 node** quan trọng, mỗi node cần cấu hình kỹ lưỡng:

##### **A. Cấu Hình Google Sheets**
1. **Candidate Data Fetch** (Bảng "Hires Tracking"):
   - **Credentials**: Chọn `googleSheetsOAuth2Api`.
   - **Sheet Name**: Đặt tên chính xác là **"Hires Tracking"** (hoặc chỉnh trong node).
   - **Range**: Chọn toàn bộ dữ liệu (ví dụ: `Sheet1!A1:Z1000`).
   - **Lưu ý**: Bảng phải có cột: `Name`, `Role`, `Traits`, `Start Date`, `Retention Status`.

2. **Trait Summary Fetch** (Bảng "Retention Summary"):
   - **Credentials**: Cùng `googleSheetsOAuth2Api`.
   - **Sheet Name**: Đặt tên chính xác là **"Retention Summary"**.
   - **Range**: Chọn toàn bộ dữ liệu (ví dụ: `Sheet1!A1:Z500`).
   - **Lưu ý**: Bảng phải có cột: `Trait`, `Weight`, `Hires`, `Stayed`, `Left`, `Retention %`.

3. **Error Handling Logic**:
   - **Sheet Name**: Đặt tên là **"Error Log"** (nếu chưa có, tạo mới).
   - **Columns**: Cần có cột `error_id` và `error_message` để ghi lỗi.

##### **B. Cấu Hình Azure OpenAI**
- **AI Processing Backend** (Node `lmChatAzureOpenAi`):
  - **Credentials**: Chọn `azureOpenAiApi`.
  - **API Key**: Điền key từ Azure Portal (đảm bảo có quyền sử dụng `gpt-4o-mini`).
  - **Model**: Đặt là `gpt-4o-mini` (mô hình miễn phí, hiệu suất cao).
  - **Prompt Template**: Workflow đã tự động cấu hình, **không cần chỉnh sửa** (trừ khi muốn tùy biến nội dung báo cáo).

- **Retention Digest Generator** (Node `chainLlm`):
  - **Model**: Gắn với `lmChatAzureOpenAi` trên.
  - **Output Format**: Workflow sẽ trả về **HTML tóm tắt** với cấu trúc:
    ```html
    <h1>Retention Analysis Digest</h1>
    <section>Top Traits (Positive)</section>
    <section>Weak Traits (Negative)</section>
    <section>Candidate Highlights</section>
    <section>3 Actionable JD Refinement Tips</section>
    ```

##### **C. Cấu Hình Gmail**
- **Email Delivery** (Node `gmail`):
  - **Credentials**: Chọn `gmailOAuth2`.
  - **From Email**: Điền địa chỉ email muốn gửi (ví dụ: `nhansu@doanhnghiep.com`).
  - **To Email**: Điền địa chỉ của ban lãnh đạo (ví dụ: `banhieuquyet@doanhnghiep.com`).
  - **Subject**: Đặt là **"Retention Analysis Digest – Weekly Update"**.
  - **Lưu ý**: Đảm bảo email này **không bị đánh dấu spam** (n8n không hỗ trợ SMTP, chỉ OAuth2).

##### **D. Cấu Hình Node Code (Candidate Scoring)**
- **Code Node**: Workflow đã tự động hóa logic tính điểm giữ chân (`Candidate_Score`), **không cần chỉnh sửa** trừ khi:
  - Bạn muốn thay đổi **công thức tính điểm** (ví dụ: thay vì `weight * retention_score`, bạn muốn thêm yếu tố khác).
  - **Mẫu code tham khảo**:
    ```javascript
    // Dữ liệu đầu vào từ Google Sheets
    const candidates = $input.all().candidates;
    const traits = $input.all().traits;

    // Tính điểm giữ chân cho mỗi nhân viên
    const scoredCandidates = candidates.map(candidate => {
      const traitScore = traits.find(t => t.Trait === candidate.Trait)?.Weight || 0;
      return {
        ...candidate,
        Candidate_Score: traitScore * (candidate.RetentionStatus === "Stayed" ? 1 : 0.5)
      };
    });

    // Trả về kết quả
    return { json: { candidates: scoredCandidates, traits } };
    ```

##### **E. Cấu Hình Data Validation**
- Node `if` sẽ kiểm tra:
  - `candidates.length > 0` **và** `traits.length > 0`.
  - **Nếu sai**: Dữ liệu sẽ được ghi vào **Error Log Sheet** (Google Sheets).
  - **Nếu đúng**: Tiến hành xử lý AI.

---
#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Execute Workflow** và kiểm tra:
     - Dữ liệu từ Google Sheets có được fetch đúng không?
     - AI có trả về HTML báo cáo không?
     - Email có được gửi thành công không?
2. **Bật Active**:
   - Chuyển trạng thái workflow từ **Inactive** sang **Active**.
   - **Lưu ý**: Để workflow chạy tự động hàng tuần, bạn cần:
     - Sử dụng **n8n Trigger** (n8n Cloud) hoặc **n8n Self-hosted** với **cron job** (ví dụ: `0 0 * * 1` để chạy mỗi thứ 2 hàng tuần).

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Tự động gửi báo cáo hàng tuần**:
   - Sử dụng **n8n Trigger** (n8n Cloud) hoặc **n8n Self-hosted** với **cron job**:
     ```bash
     # Chạy mỗi thứ 2 hàng tuần lúc 8h sáng
     0 8 * * 1 n8n exec "Retention Analytics" --cron
     ```
   - **Đăng ký VPS TinoHost** (Self-hosted) để workflow chạy 24/7:
     👉 [🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%](https://tino.vn/vps-n8n?affid=388)

2. **Lưu log hoạt động**:
   - Thêm node **Google Sheets** mới để ghi **log hoạt động** (thời gian chạy, status thành công/thất bại).
   - **Cấu trúc log**:
     ```
     | Time          | Workflow ID | Status   | Notes          |
     |---------------|------------|----------|----------------|
     | 2024-05-20    | 12345      | Success  | Data processed |
     ```

3. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để thông báo khi báo cáo được gửi thành công/thất bại.
   - **Mẫu thông báo Slack**:
     ```
     *📊 Retention Digest Sent!*
     *Time*: {{ $json["executionDate"] }}
     *Status*: {{ $json["status"] }}
     *Link*: [View Report](https://mail.google.com/mail/u/0/#inbox)
     ```

4. **Tùy biến nội dung báo cáo**:
   - Sửa **prompt** trong node `chainLlm` để thay đổi cấu trúc báo cáo (ví dụ: thêm/loại bỏ phần nào).
   - **Ví dụ prompt tùy biến**:
     ```json
     {
       "prompt": "Tóm tắt báo cáo giữ chân nhân viên với các phần sau:
       1. **TL;DR**: 1 câu tóm tắt chính.
       2. **Top 3 Traits giữ chân**: Danh sách các đặc điểm quan trọng.
       3. **3 Gợi ý cải thiện JD**: Cách thu hút nhân viên tương tự.
       4. **Danh sách nhân viên có điểm thấp**: Top 5 nhân viên cần theo dõi.
       Đảm bảo không có hallucination, chỉ sử dụng dữ liệu từ dataset."
     }
     ```

5. **Xử lý dữ liệu lớn**:
   - Nếu bảng Google Sheets có **trên 1000 dòng**, hãy chia dữ liệu thành nhiều sheet nhỏ hoặc sử dụng **pagination** trong node Google Sheets.

---
### **📌 Kết Luận**
Workflow này **giải phóng thời gian** của các sếp để tập trung vào chiến lược nhân sự chứ không phải phân tích dữ liệu thủ công. Với **GPT-4o**, báo cáo không chỉ được tự động hóa mà còn **cá nhân hóa** và **cung cấp ý tưởng thực tế** để cải thiện đội ngũ.

**Hành động ngay**:
1. **Import workflow** và cấu hình theo hướng dẫn trên.
2. **Test run** với dữ liệu mẫu trước khi bật chế độ tự động.
3. **Bật Active** và **lên lịch chạy hàng tuần** để nhận báo cáo tự động.

**🚀 Cần hỗ trợ thêm?** Đăng ký **VPS Self-hosted** để workflow chạy ổn định 24/7:
👉 [🎁 Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (mã giảm giá **N8N50K**).

---
**Chúc các sếp thành công với việc tự động hóa phân tích nhân sự!** 💼🤖