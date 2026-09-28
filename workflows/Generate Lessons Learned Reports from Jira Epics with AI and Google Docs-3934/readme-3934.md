---
title: "🚀 Tự động hóa tạo Báo cáo Bài học kinh nghiệm (Lessons Learned) từ Jira Epic bằng AI và Google Docs"
description: "Hướng dẫn xây dựng workflow n8n tự động phân tích Jira Epic khi hoàn thành, sử dụng AI Agent để tổng hợp và xuất báo cáo Lessons Learned chuyên nghiệp trực tiếp lên Google Docs."
slug: "tu-dong-hoa-tao-bao-cao-jira-epic-ai-google-docs"
tags: [n8n, automation, jira, ai-agent, openai, google-docs, product-management]
keywords: [n8n workflow, jira epic lessons learned, tự động hóa jira, ai tổng hợp báo cáo, n8n google docs openai]
---

# 🚀 Tự động hóa tạo Báo cáo Bài học kinh nghiệm từ Jira Epic bằng AI và Google Docs

Các sếp làm Product, Project Manager hay Tech Lead chắc chắn hiểu rõ cảm giác "vật lộn" mỗi khi một Epic hay dự án hoàn thành (Done). Việc ngồi thủ công bới lại hàng loạt issue, đọc từng comment, tổng hợp lại xem team đã làm tốt cái gì, vấp ngã ở đâu và rút ra bài học gì (Lessons Learned) thường ngốn cả tiếng đồng hồ mà báo cáo chưa chắc đã sâu sắc.

Đừng làm việc thủ công đó nữa! Bài viết này sẽ hướng dẫn các sếp cách "lên đồ" một workflow n8n cực kỳ xịn sò được thiết kế bởi chuyên gia Tarek Mustafa. Workflow này sẽ tự động "bắt sóng" khi một Jira Epic chuyển sang trạng thái **Done**, gom toàn bộ issue và comment, nhờ AI (OpenAI GPT-4o-mini) phân tích và tự động viết một bản báo cáo hoàn chỉnh gửi thẳng vào Google Docs. Hoàn toàn tự động 100%!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Ngay khi Epic chuyển sang Done, quy trình tổng hợp tự khởi chạy mà không cần con người nhúng tay.
- **AI thông minh tổng hợp đa chiều:** AI Agent phân tích toàn bộ mô tả issue (`Jira Get All Issues`) và ý kiến trao đổi (`Jira Get All Comments`) để rút ra các bài học thực tế, khách quan.
- **Báo cáo chuyên nghiệp tức thì:** Kết quả được định dạng sẵn và đẩy thẳng vào Google Docs (`Google Docs`), sẵn sàng để chia sẻ ngay với ban quản lý và team.
- **Tiết kiệm hàng giờ đồng hồ:** Thay vì mất buổi sáng để làm báo cáo tổng kết, các sếp chỉ cần bấm một nút (hoặc để tự động) là có ngay tài liệu chỉn chu.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow chạy mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
1. **Tài khoản n8n** (Cloud hoặc Self-hosted).
2. **Jira Software Cloud**: Tài khoản có quyền kết nối API / Webhook (`Jira Trigger`, `Jira Get All Issues`, `Jira Get All Comments`).
3. **OpenAI API Key**: Để sử dụng mô hình `OpenAI Chat Model` (`gpt-4o-mini`).
4. **Google Drive / Google Docs**: Tài khoản Google để cấp quyền tạo và cập nhật tài liệu (`Google Docs`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ nguồn gốc hoặc copy toàn bộ JSON cấu trúc workflow và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 10 nodes phối hợp nhịp nhàng. Các sếp chú ý cấu hình kỹ các điểm mấu chốt sau:

- **Jira Trigger**: Node này lắng nghe sự kiện thay đổi trên Jira. Các sếp cần cấu hình thông tin kết nối (`jiraSoftwareCloudApi`) và thiết lập điều kiện lọc để trigger chỉ hoạt động khi một Epic chuyển sang trạng thái **Done** (như ghi chú trên canvas).
- **If**: Dùng để rà soát lại logic kiểm tra xem trạng thái Epic đã thực sự hoàn thành chưa trước khi cho phép đi tiếp.
- **Jira Get All Issues** & **Jira Get All Comments**: Cần cấu hình đúng thông tin dự án/Epic để kéo toàn bộ các issue con và chuỗi thảo luận liên quan.
- **Edit Fields** & **Summarize**: Chuẩn hóa dữ liệu đầu vào, gom nhóm thông tin trước khi chuyển cho AI.
- **AI Agent**, **OpenAI Chat Model** & **Simple Memory**: 
  - Chọn model `gpt-4o-mini` cho `OpenAI Chat Model`.
  - Tại `AI Agent`, thiết lập **System Message** (Prompt hệ thống) để định nghĩa rõ cấu trúc báo cáo Lessons Learned mong muốn (ví dụ: Tổng quan Epic, Những điểm đã làm tốt, Thách thức gặp phải, Bài học rút ra cho tương lai).
- **Google Docs**: Chọn credential OAuth2 của Google, trỏ tới file tài liệu mẫu (hoặc tạo mới) và chọn thao tác `update` để AI chèn nội dung báo cáo vào đúng nơi quy định.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử thay đổi trạng thái một Epic trên Jira thành **Done** để test run dữ liệu mẫu.
- Kiểm tra kết quả trong Google Docs xem nội dung đã đúng ý chưa.
- Sau khi kiểm tra ngon lành, bật nút **Active** ở góc trên bên phải để đưa workflow vào vận hành chính thức 24/7.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống quản lý dự án thông minh hơn nữa, các sếp có thể mở rộng workflow này:
- **Tích hợp thông báo:** Thêm node Slack hoặc Telegram ở cuối luồng để bắn tin nhắn thông báo kèm link Google Docs vừa tạo vào group chat của team/quản lý.
- **Lưu trữ Log:** Lưu thông tin tóm tắt vào Google Sheets hoặc Notion để dễ dàng tra cứu về sau.
- **AI Đa ngôn ngữ:** Tùy chỉnh prompt trong AI Agent để tự động dịch báo cáo sang tiếng Anh hoặc tiếng Nhật tùy theo đối tác/khách hàng của doanh nghiệp.

### 📌 Kết luận
Việc tổng kết dự án chưa bao giờ nhẹ nhàng đến thế! Với sự kết hợp giữa Jira, AI thông minh và Google Docs trong n8n, các sếp vừa tiết kiệm được thời gian, vừa nâng tầm tính chuyên nghiệp cho quy trình vận hành của team. Lên đồ ngay thôi nào các sếp ơi!