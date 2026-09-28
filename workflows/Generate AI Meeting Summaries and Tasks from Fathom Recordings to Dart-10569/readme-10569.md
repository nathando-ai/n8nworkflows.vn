---
title: "🚀 Tự động hóa tóm tắt cuộc họp từ Fathom và tạo Task vào Dart với n8n & OpenAI"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n tích hợp Fathom, OpenAI và Dart để tự động tóm tắt nội dung cuộc họp và tạo task giao việc không cần thủ công."
slug: "tu-dong-hoa-tom-tat-cuoc-hop-fathom-dart-n8n"
tags: [n8n, automation, no-code, fawthom, dart, openai, ai-summarization]
keywords: [n8n workflow, tự động hóa cuộc họp, fathom to dart, openai meeting summary, n8n ai agent]
---

# 🚀 Tự động hóa tóm tắt cuộc họp từ Fathom và tạo Task vào Dart với n8n & OpenAI

Các sếp có bao giờ cảm thấy mệt mỏi sau một chuỗi các cuộc họp dài lê thê? Việc phải ngồi nghe lại ghi âm, tự tay chép lại biên bản (meeting minutes), lọc ra các công việc cần làm (action items) rồi lại lọ mọ tạo task thủ công lên phần mềm quản lý dự án như Dart thực sự ngốn quá nhiều thời gian và năng lượng quý báu.

Đừng lo nữa! Bài viết này sẽ hướng dẫn các sếp cách thiết lập một **n8n workflow tự động hóa 100%**: Nhận bản ghi âm từ **Fathom**, dùng sức mạnh AI của **OpenAI** để phân tích, tóm tắt và tự động lưu tài liệu vào **Dart**, đồng thời tạo luôn task review kèm link ghi âm gốc. Không một thao tác thủ công nào nữa!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần tự tay soạn biên bản hay tạo task thủ công sau mỗi cuộc họp.
- **Tóm tắt thông minh, chuẩn xác:** AI phân tích chi tiết các điểm chính (Key takeaways), chủ đề, bước tiếp theo và danh sách việc cần làm (Action items).
- **Đồng bộ hóa liền mạch:** Tự động tạo Document trong thư mục định sẵn trên Dart và tạo Task review kèm link Fathom gốc ngay lập tức.
- **Hoạt động 24/7 tự động:** Chỉ cần kết thúc cuộc họp trên Fathom, mọi thứ còn lại cứ để n8n lo.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản Fathom:** Nơi lưu trữ bản ghi âm cuộc họp và cấu hình Webhook.
- **Tài khoản OpenAI:** Lấy OpenAI API Key để AI Agent xử lý văn bản (`gpt-4o-mini` hoặc model tương đương).
- **Tài khoản Dart:** Công cụ quản lý dự án (lấy Workspace, Folder ID và Dartboard ID).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng mã nguồn JSON của workflow (ID: `10569` từ n8n.io) bằng cách copy và paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 9 nodes hoạt động nhịp nhàng với nhau. Các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Webhook Node:** 
  - Lấy Production URL của node này và cấu hình vào phần Webhook settings trên Fathom API ([Tham khảo tài liệu Fathom Webhooks](https://developers.fathom.ai/webhooks)). Node này sẽ hứng dữ liệu ngay khi cuộc họp kết thúc.
- **OpenAI Chat Model Node:** 
  - Thêm Credentials `openAiApi` bằng API Key của các sếp.
  - Chọn model AI mong muốn (khuyến nghị `gpt-4o-mini` cho tốc độ nhanh và chi phí tối ưu).
- **AI Agent Node:** 
  - Nơi cấu hình Prompts để AI hiểu và phân loại nội dung cuộc họp thành các mục: *Key takeaways, Topics covered, Next items, Action items*. Các sếp có thể tùy chỉnh tone giọng hoặc cấu trúc summary tại đây.
- **Code in JavaScript Node:** 
  - Xử lý và parse output từ AI Agent thành định dạng JSON chuẩn để các node tiếp theo dễ dàng đọc hiểu.
- **Retrieve an existing folder & Create a new doc (Dart Nodes):** 
  - Thêm `dartApi` credentials. 
  - Thay thế Folder ID mẫu bằng **Folder ID thực tế** trong workspace Dart của các sếp để document được lưu đúng nơi quy định.
- **Retrieve an existing dartboard & Create a new task (Dart Nodes):** 
  - Thay thế Dartboard ID mẫu bằng **Dartboard ID thực tế**.
  - Node tạo task cuối cùng sẽ tự động đính kèm CTA trỏ thẳng đến Document tóm tắt vừa tạo và Link ghi âm Fathom gốc để đội ngũ dễ dàng theo dõi, review.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và kích hoạt một sự kiện test từ Fathom để kiểm tra xem dữ liệu có chạy trơn tru qua các node không.
- Sau khi test thành công, bật công tắc **Active** góc trên cùng bên phải để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Slack/Telegram:** Thêm một node Slack hoặc Telegram ngay sau khi tạo task thành công để bắn tin nhắn thông báo "Đã có biên bản cuộc họp mới" vào group chat của team.
- **Lưu trữ backup:** Kết hợp thêm node Google Sheets hoặc Notion để lưu trữ dự phòng toàn bộ nội dung tóm tắt cuộc họp.
- **Tùy biến Prompt AI:** Nếu team của các sếp làm về kỹ thuật, hãy hướng dẫn AI tập trung trắc lọc các technical requirements; nếu làm sales, hãy hướng dẫn AI lọc ra pain points của khách hàng.

### 📌 Kết luận
Việc tự động hóa quy trình hậu-cuộc-hợp chưa bao giờ dễ dàng đến thế. Với sự kết hợp hoàn hảo giữa Fathom, OpenAI và Dart trên nền tảng n8n, các sếp sẽ giải phóng hoàn toàn thời gian hành chính để tập trung vào các chiến lược kinh doanh cốt lõi. Hãy setup ngay hôm nay và trải nghiệm sự khác biệt!