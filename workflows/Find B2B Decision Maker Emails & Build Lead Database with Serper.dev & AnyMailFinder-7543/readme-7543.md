---
title: "🚀 Tự động hóa tìm kiếm email người ra quyết định B2B với Serper.dev và AnyMailFinder trên n8n"
description: "Xây dựng cơ sở dữ liệu khách hàng tiềm năng B2B hoàn toàn tự động bằng n8n, tích hợp AI, Serper.dev và AnyMailFinder để tìm email CEO, Sales, Marketing."
slug: "tu-dong-hoa-tim-kiem-email-b2b-serper-anymailfinder-n8n"
tags: [n8n, automation, no-code, b2b-lead-generation, ai-automation, serper, anymailfinder]
keywords: [n8n workflow, tìm kiếm email b2b, lead generation tự động, anymailfinder n8n, serper.dev n8n, nocodb automation]
---

# 🚀 Tự động hóa tìm kiếm email người ra quyết định B2B với Serper.dev và AnyMailFinder

Việc tìm kiếm thông tin liên hệ của các cấp lãnh đạo, quản lý cấp cao (CEO, Sales Director, Marketing Manager) để làm Sales B2B thủ công tốn rất nhiều thời gian và công sức của đội ngũ nhân sự. Các sếp thường phải mất hàng giờ lướt LinkedIn, tra cứu Google và check thủ công từng domain công ty.

Giải pháp? Workflow n8n siêu việt này sẽ giúp các sếp tự động hóa 100% quy trình từ việc tìm kiếm domain công ty, trích xuất thông tin qua AI, cho đến việc "săn" email chuẩn xác của các nhân sự cấp cao thông qua **Serper.dev** và **AnyMailFinder**, sau đó tự động lưu trữ toàn bộ vào **NocoDb**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Gom nhóm, tìm kiếm domain và quét email người ra quyết định (CEO, Sales, Marketing) mà không cần thao tác tay.
- **Dữ liệu chất lượng cao:** Tích hợp AI (`openAi`) để lọc chính xác URL và domain, kết hợp AnyMailFinder trả về trạng thái email (valid/risky) và thông tin LinkedIn.
- **Quản lý thông minh:** Lưu trữ và cập nhật trạng thái liên tục trên NocoDb theo từng lô (Batch), giúp tránh mất dữ liệu nếu xảy ra lỗi giữa chừng.
- **Tiết kiệm chi phí API:** Cơ chế lọc thông minh chỉ tìm kiếm các công ty chưa xử lý hoặc quét thêm email tổng khi cần thiết.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn (Self-hosted hoặc Cloud).
- **Tài khoản & API Keys:**
  - **OpenAI API Key** (dùng cho node `extract url & domain`).
  - **Serper.dev API Key** (dùng cho node `serper search domains`).
  - **AnyMailFinder API Key** (dùng cho các node `Get Sales Decision Maker Email`, `Get Marketing Email`, `Get CEO Email`, `Get All Company Emails`).
  - **NocoDb API Token** (dùng cho các node quản lý dữ liệu NocoDb).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã nguồn.
- Mở n8n Editor, chọn **Add workflow** -> Dán (Paste) workflow vào giao diện.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình kỹ các node sau:
- **NocoDb Nodes (`Get many rows`, `Update Companies Domains`, `Update Company Status`, `Get All Company Status`, `Update Company Emails`, `Create Contacts`):** Kết nối với tài khoản NocoDb của các sếp bằng `nocoDbApiToken`, sau đó trỏ chính xác đến bảng (Table) quản lý công ty và danh bạ liên hệ (Contacts).
- **Node `serper search domains` & Các node gọi AnyMailFinder:** Cấu hình thông tin xác thực `httpHeaderAuth` với các API Key tương ứng của Serper và AnyMailFinder.
- **Node `extract url & domain` (`openAi`):** Chọn model OpenAI phù hợp (khuyên dùng `gpt-4o-mini` hoặc `gpt-4o`) và kiểm tra lại System Prompt để đảm bảo trích xuất chính xác domain từ kết quả tìm kiếm.
- **Trigger Nodes (`Schedule Trigger2` hoặc `When clicking ‘Execute workflow’`):** Cấu hình lịch chạy tự động định kỳ (ví dụ: chạy hàng ngày) hoặc chạy thủ công tùy nhu cầu.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm với 1 vài dòng dữ liệu mẫu (Test run) ở node `When clicking ‘Execute workflow’` để kiểm tra luồng dữ liệu qua các bước Filter, Merge, Code.
- Sau khi test thành công, bật công tắc **Active workflow** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node Telegram hoặc Slack vào cuối workflow để gửi báo cáo tổng kết số lượng email CEO/Sales/Marketing tìm được sau mỗi lần chạy.
- **Mở rộng CRM:** Ngoài NocoDb, các sếp có thể đồng bộ dữ liệu contact sang HubSpot, Google Sheets hoặc Salesforce bằng cách thay thế/thêm các node tương ứng.
- **Kiểm soát Rate Limit:** Sử dụng hiệu quả node `Wait` để tránh việc gửi quá nhiều request đồng thời tới API của AnyMailFinder hoặc Serper.dev trong thời gian ngắn.

### 📌 Kết luận
Workflow này là một "vũ khí" cực kỳ lợi hại cho các đội ngũ Sales và Growth Marketing B2B. Hãy thiết lập ngay hôm nay để tự động hóa việc tìm kiếm khách hàng tiềm năng và tối ưu hóa hiệu suất kinh doanh của các sếp!