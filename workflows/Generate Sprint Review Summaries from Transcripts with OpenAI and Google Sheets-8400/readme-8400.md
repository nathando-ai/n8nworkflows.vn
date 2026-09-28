---
title: "🚀 Tự động tóm tắt Sprint Review từ file ghi hình bằng OpenAI và Google Sheets"
description: "Biến file ghi âm hoặc transcript buổi họp Sprint Review thành báo cáo tóm tắt chuyên nghiệp bằng AI và tự động lưu trữ vào Google Sheets chỉ trong vài giây."
slug: "tu-dong-tom-tat-sprint-review-openai-google-sheets"
tags: [n8n, automation, ai-summarization, project-management, openai, google-sheets]
keywords: [n8n workflow, tóm tắt họp sprint, ai summary transcript, openai gpt, google sheets automation]
---

# 🚀 Tự động tóm tắt Sprint Review từ file ghi hình với OpenAI và Google Sheets

Các sếp có bao giờ cảm thấy mệt mỏi sau mỗi buổi Sprint Review khi phải ngồi nghe lại hàng giờ đồng hồ ghi hình, tự tay chép lại các quyết định quan trọng, việc cần làm (action items) và cập nhật vào báo cáo? Việc làm thủ công này vừa tốn thời gian, dễ bỏ sót ý, lại làm gián đoạn dòng chảy công việc của đội ngũ.

Đừng lo, giải pháp ở đây rồi! Workflow n8n này sẽ giúp các sếp tự động hóa 100% quy trình: Nhận file transcript/VTT, dùng AI phân tích và tạo báo cáo tóm tắt chuẩn chỉnh định dạng Markdown, hiển thị xem trước để duyệt, và cuối cùng tự động lưu trữ vào Google Sheets. Tiết kiệm thời gian, tăng năng suất cho cả team!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh nghe lại audio hay đọc hàng nghìn dòng transcript thủ công.
- **Báo cáo chuẩn mực:** AI tự động chia tách ý chính, tạo bảng tóm tắt và danh sách việc cần làm (Action Items) theo định dạng Markdown cực kỳ chuyên nghiệp.
- **Kiểm soát trực quan:** Xem trước kết quả trực tiếp ngay trên giao diện form trước khi lưu trữ chính thức.
- **Lưu trữ tập trung:** Tự động đồng bộ toàn bộ metadata, transcript gốc và bản tóm tắt lên Google Sheets để tra cứu bất cứ lúc nào.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Hệ thống n8n:** Đã cài đặt sẵn sàng (Self-hosted hoặc Cloud).
- **Tài khoản OpenAI:** Cần có API Key hợp lệ và quyền sử dụng model (workflow cấu hình mặc định sử dụng model `gpt-5-mini-2025-08-07`).
- **Google Sheets:** Chuẩn bị sẵn một trang tính (Sheet) để lưu trữ thông tin gồm các cột: Ngày, Tên Sprint, Lĩnh vực (Domain), Transcript gốc và Bản tóm tắt.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ mã nguồn JSON của workflow.
- Mở giao diện n8n Editor, nhấn vào **Add workflows** -> Chọn **Import from JSON** và dán nội dung vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 6 nodes chính hoạt động nhịp nhàng với nhau. Các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Collect Sprint Review Input (`formTrigger`):** Node khởi chạy dạng Form. Các sếp có thể tùy chỉnh các trường nhập liệu trên giao diện như: File transcript (định dạng VTT hoặc text), Tên Sprint (Sprint Name), và Lĩnh vực (Domain).
- **Parse Transcript (`code`):** Node chạy mã JavaScript có sẵn giúp chuẩn hóa định dạng transcript thành cấu trúc `[HH:MM:SS] Speaker: text` hỗ trợ cả file VTT lẫn text thuần túy.
- **Generate Summary (`agent`) & OpenAI LLM (`lmChatOpenAi`):** 
  - Tại node **OpenAI LLM**, các sếp cần chọn **Credentials** là tài khoản OpenAI của mình và kiểm tra lại model đang chọn (`gpt-5-mini-2025-08-07` hoặc thay đổi sang model phù hợp).
  - AI Agent sẽ nhận dữ liệu từ bước parse, thực hiện nhiệm vụ tạo tóm tắt gồm các gạch đầu dòng điều hành (executive bullets), bảng tổng kết và danh sách việc cần làm.
- **Preview Summary (`form`):** Hiển thị bản tóm tắt dạng Markdown với CSS tùy chỉnh để người quản lý đọc duyệt trực tiếp trên giao diện form hoàn thành (`completion`).
- **Save to Google Sheets (`googleSheets`):** 
  - Cấu hình **Credentials** cho tài khoản Google OAuth2.
  - Chọn file Spreadsheet và Worksheet cụ thể.
  - Thiết lập thao tác `appendOrUpdate` để ghi lại dữ liệu bao gồm: bản tóm tắt, transcript gốc và các thông tin metadata (ngày tháng, domain, tên sprint, tên file).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách điền một form mẫu với file transcript giả lập để kiểm tra toàn bộ luồng chạy.
- Nếu mọi thứ mượt mà, hãy gạt công tắc **Active** ở góc trên bên phải để đưa workflow vào trạng thái vận hành tự động thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm một node Slack hoặc Telegram ngay sau bước lưu Google Sheets để tự động bắn link báo cáo tóm tắt vào kênh chung của team.
- **Tự động hóa lịch họp:** Kết hợp Google Calendar Trigger để tự động nhắc nhở gửi form thu thập transcript ngay sau khi lịch hẹn Sprint Review kết thúc.
- **Quản lý lịch sử:** Sử dụng thêm tính năng phân loại tag tự động theo Domain để dễ dàng lọc báo cáo theo từng bộ phận sản phẩm/kỹ thuật.

### 📌 Kết luận
Việc tự động hóa quy trình tổng hợp họp Sprint Review chưa bao giờ dễ dàng đến thế với sức mạnh kết hợp giữa n8n và OpenAI. Hãy triển khai ngay hôm nay để giải phóng thời gian cho đội ngũ quản lý và tập trung vào những giá trị cốt lõi hơn! Chúc các sếp thao tác thành công!