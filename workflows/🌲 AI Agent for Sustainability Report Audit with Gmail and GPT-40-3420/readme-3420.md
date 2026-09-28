---
title: "🌱 Tự động hóa báo cáo CSRD với Gmail và GPT-4o-mini - Workflow n8n"
description: "Hướng dẫn tự động hóa kiểm tra báo cáo CSRD từ email bằng n8n và AI Agent. Tiết kiệm thời gian và nâng cao độ chính xác trong quản lý báo cáo bền vững."
slug: "tu-dong-hoa-bao-cao-csrd-voi-gmail-va-gpt-4o-mini"
tags: [n8n, automation, no-code, CSRD, AI, sustainability]
keywords: [n8n workflow, tự động hóa báo cáo, CSRD, AI Agent, GPT-4o-mini]
---

# 🌱 Tự động hóa báo cáo CSRD với Gmail và GPT-4o-mini - Workflow n8n

[Các sếp đang gặp khó khăn khi phải kiểm tra và phản hồi các báo cáo CSRD (Corporate Sustainability Reporting Directive) thủ công từ email. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ nhận email đến gửi phản hồi kiểm tra bằng AI, giúp tiết kiệm thời gian và nâng cao độ chính xác.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động xử lý báo cáo CSRD mà không cần can thiệp thủ công.
- **Nâng cao độ chính xác**: Sử dụng AI để phân tích và kiểm tra nội dung báo cáo một cách chi tiết.
- **Tự động hóa toàn bộ quy trình**: Từ nhận email đến gửi phản hồi kiểm tra, mọi thứ được thực hiện tự động.
- **Tích hợp với hệ thống email hiện tại**: Hoạt động liền mạch với Gmail của các sếp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail API đã được kích hoạt và cấu hình.
- API Key cho OpenAI (đặc biệt là model GPT-4o-mini).
- Quyền truy cập vào các email chứa báo cáo CSRD (các email có chủ đề chứa từ "CSRD Reporting").
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/3420](https://n8n.io/workflows/3420) để tải file JSON của workflow.
2. Trong n8n Editor, nhấn vào **Import from File** và chọn file JSON đã tải về.
3. Hoặc copy toàn bộ nội dung JSON và dán vào ô **Import from JSON** trong n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Email Trigger Node**:
   - Cấu hình credentials cho Gmail API.
   - Đảm bảo email trigger chỉ kích hoạt khi chủ đề chứa từ "CSRD Reporting".

2. **Download Attachment Node**:
   - Cấu hình credentials cho Gmail API.
   - Đảm bảo node này chỉ tải các file đính kèm có định dạng xHTML.

3. **HTML from binary Node**:
   - Không cần cấu hình thêm, node này tự động trích xuất nội dung HTML từ file đính kèm.

4. **Extract the HTML Node**:
   - Sử dụng đoạn code sau để trích xuất nội dung HTML:
     ```javascript
     const htmlContent = $input.all()[0].json.content;
     return { htmlContent };
     ```

5. **Check the format Node**:
   - Sử dụng đoạn code sau để kiểm tra định dạng của báo cáo:
     ```javascript
     const htmlContent = $input.all()[0].json.htmlContent;
     const isValid = htmlContent.includes('<html') && htmlContent.includes('</html>');
     return { isValid };
     ```

6. **If Node**:
   - Cấu hình điều kiện để chỉ tiếp tục xử lý nếu định dạng báo cáo hợp lệ.

7. **AI Agent Node**:
   - Cấu hình credentials cho OpenAI (model GPT-4o-mini).
   - Cập nhật system prompt để phù hợp với định dạng báo cáo CSRD của các sếp.

8. **OpenAI Chat Model Node**:
   - Chọn model là `gpt-4o-mini`.
   - Cấu hình credentials cho OpenAI.

9. **Structured Output Parser Node**:
   - Không cần cấu hình thêm, node này tự động phân tích kết quả từ AI Agent.

10. **Reply Node**:
    - Cấu hình credentials cho Gmail API.
    - Cập nhật nội dung email phản hồi để phù hợp với định dạng báo cáo CSRD.

#### 3. Kích hoạt ⚡️
1. **Test run dữ liệu mẫu**:
   - Gửi một email mẫu chứa báo cáo CSRD đến tài khoản Gmail được cấu hình.
   - Kiểm tra xem workflow có xử lý đúng và gửi phản hồi kiểm tra không.

2. **Bật Active workflow**:
   - Sau khi kiểm tra và đảm bảo workflow hoạt động đúng, bật chế độ Active để workflow tự động kích hoạt khi nhận email mới.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Teams**: Thêm node để gửi thông báo kết quả kiểm tra đến kênh Slack/Teams của các sếp.
- **Lưu log kiểm tra**: Thêm node để lưu log kiểm tra vào Google Sheets hoặc cơ sở dữ liệu để theo dõi lịch sử kiểm tra.
- **Gửi báo cáo định kỳ**: Cấu hình workflow để gửi báo cáo tổng hợp về kết quả kiểm tra định kỳ đến các sếp.
- **Tích hợp với các hệ thống khác**: Kết nối với các hệ thống khác như ERP, CRM để tự động cập nhật kết quả kiểm tra vào hệ thống quản lý của các sếp.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình kiểm tra báo cáo CSRD từ email đến gửi phản hồi kiểm tra bằng AI. Với việc tích hợp n8n và OpenAI, các sếp có thể tiết kiệm thời gian và nâng cao độ chính xác trong quản lý báo cáo bền vững. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc của các sếp!