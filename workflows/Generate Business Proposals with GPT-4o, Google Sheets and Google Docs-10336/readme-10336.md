---
title: "🚀 Tự động tạo hồ sơ năng lực và đề xuất kinh doanh chuyên nghiệp với GPT-4o, Google Sheets và Google Docs"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa 100% quy trình tạo Business Proposal bằng AI từ Google Sheets, điền mẫu Google Docs và lưu trữ trên Google Drive."
slug: "tu-dong-tao-de-xuat-kinh-doanh-voi-gpt4o-google-sheets-docs"
tags: [n8n, automation, ai-agent, openai, google-workspace, no-code]
keywords: [n8n workflow, tạo proposal tự động, gpt-4o ai agent, google docs automation, tự động hóa n8n]
---

# 🚀 Tự động tạo hồ sơ năng lực và đề xuất kinh doanh chuyên nghiệp với GPT-4o, Google Sheets và Google Docs

Các sếp có đang cảm thấy mệt mỏi mỗi khi có khách hàng mới điền form hoặc gửi yêu cầu, mà đội ngũ lại phải mất hàng giờ đồng hồ để ngồi viết điền tay từng mục trong file Google Docs (Executive Summary, Scope of Work, bảng giá 4 tháng, timeline...) không? Việc làm thủ công này không chỉ tốn thời gian mà còn dễ sai sót, thiếu tính cá nhân hóa cho từng khách hàng.

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một siêu workflow n8n được xây dựng bởi chuyên gia Rahul Joshi. Workflow này sẽ tự động hóa toàn bộ quy trình: Lắng nghe dữ liệu khách hàng từ Google Sheets $\rightarrow$ Dùng AI (GPT-4o) viết nội dung chuẩn chỉnh $\rightarrow$ Điền tự động vào Google Docs $\rightarrow$ Xuất file PDF và lưu trữ gọn gàng trên Google Drive!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 không lo mất kết nối, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Ngay khi có dòng dữ liệu mới trong Google Sheets, hệ thống tự động khởi chạy mà không cần chạm tay.
- **AI thông minh & chuẩn cấu trúc:** Sử dụng GPT-4o kết hợp JSON Output Parser để đảm bảo dữ liệu đầu ra luôn đúng định dạng cấu trúc mà Google Docs yêu cầu.
- **Đồng bộ tài liệu chuyên nghiệp:** Tự động điền dữ liệu vào template có sẵn, tạo bản Proposal hoàn chỉnh, lưu trữ khoa học trên Google Drive và reset template cho lần tiếp theo.
- **Tiết kiệm 90% thời gian:** Rút ngắn thời gian từ vài tiếng xuống chỉ còn vài giây cho mỗi đề xuất kinh doanh gửi tới khách hàng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **OpenAI API Key** (có hạn mức sử dụng model GPT-4o).
- **Google Sheets:** File chứa thông tin khách hàng.
- **Google Docs:** File mẫu (Template) chứa các placeholder (thẻ đánh dấu).
- **Google Drive:** Thư mục để lưu trữ các file Proposal đã hoàn thiện.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ nguồn gốc (ID: 10336 trên n8n.io) hoặc copy đoạn JSON và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động mượt mà, các sếp cần cấu hình chính xác các node sau trong danh sách:

- **Trigger: New Sheet Row (`googleSheetsTrigger`):** 
  - Kết nối tài khoản Google Sheets của các sếp.
  - Chọn đúng file Google Sheet và Sheet Name.
  - Đảm bảo Sheet có các cột: `clientName` (Cột A) và `jobDescription` (Cột B). Thay thế Sheet ID mẫu bằng Sheet ID thực tế của các sếp.
- **Filter: Latest Row Only (`code`):** Node này dùng để lọc và chỉ lấy dòng dữ liệu mới nhất được thêm vào (tránh việc trigger quét lại toàn bộ bảng).
- **Model: GPT-4o (`lmChatOpenAi`) & Parser: JSON Output (`outputParserStructured`):**
  - Nhập OpenAI API Key vào credentials.
  - Đảm bảo chọn đúng model `gpt-4o`. Parser sẽ ép AI trả về các trường dữ liệu chuẩn xác như: Tóm tắt điều hành (`executive_summary`), phạm vi công việc (`scope_of_work`), chi phí 4 tháng (`month1_cost` đến `month4_cost`), tổng chi phí, timeline và kết luận.
- **Populate: Template Document (`googleDocs`):**
  - Cấu hình operation là `update`.
  - Trỏ tới Google Docs Template của các sếp. Trong file Docs, hãy đặt các placeholder dạng `{{executive_summary}}`, `{{scope_of_work}}`, `{{month1_cost}}`, `{{total_cost}}`,... để node tự động thay thế bằng nội dung AI sinh ra.
- **Download: Completed Proposal & Archive: Save to Drive (`googleDrive`):**
  - Cấu hình node tải file về dưới dạng PDF và node lưu trữ vào đúng thư mục (Folder ID) trên Google Drive cá nhân hoặc doanh nghiệp.
- **Reset: Template Placeholders (`googleDocs`):** Node giúp dọn dẹp/đưa template về trạng thái ban đầu sau khi xuất file, sẵn sàng cho khách hàng tiếp theo.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (Test step / Execute node) với một dòng dữ liệu mẫu trong Google Sheets để kiểm tra kết quả trả về ở từng bước.
- Sau khi kiểm tra mọi thứ chạy mượt mà, hãy gạt công tắc sang **Active** để hệ thống tự động hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node **Slack** hoặc **Telegram** ngay sau bước lưu file thành công để gửi thông báo về group team sales ngay khi có đề xuất mới được tạo.
- **Lưu log chi tiết:** Lưu thêm thông tin trạng thái tạo proposal vào một cột phụ trong Google Sheets để dễ dàng theo dõi tiến độ.
- **Tùy chỉnh Prompt AI:** Tinh chỉnh System Prompt trong `AI Agent: Generate Proposal` để văn phong phù hợp với giọng điệu thương hiệu (Brand Voice) riêng của công ty các sếp.

### 📌 Kết luận
Việc tự động hóa quy trình tạo Business Proposals không chỉ giúp tiết kiệm thời gian, nhân lực mà còn nâng cao tính chuyên nghiệp trong mắt khách hàng nhờ tốc độ phản hồi chớp nhoáng. Hãy áp dụng ngay workflow này vào hệ thống n8n của các sếp để tối ưu hóa hiệu suất kinh doanh ngay hôm nay!