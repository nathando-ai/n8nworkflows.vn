---
title: "🚀 Tự động hóa tóm tắt email và phân tích Knowledge Graph thông minh với n8n & InfraNodus"
description: "Hướng dẫn chi tiết cách xây dựng hệ thống tự động lọc email, phân tích nội dung bằng AI (Google Gemini), vẽ biểu đồ tri thức Knowledge Graph (InfraNodus) và gửi báo cáo qua Telegram."
slug: "tu-dong-hoa-tom-tat-email-knowledge-graph-infranodus-n8n"
tags: [n8n, automation, no-code, infranodus, ai, gmail, telegram]
keywords: [n8n workflow, tóm tắt email tự động, knowledge graph, infranodus, google gemini, phân tích văn bản ai]
---

# 🚀 Tự động hóa tóm tắt email và phân tích Knowledge Graph thông minh với n8n & InfraNodus

Các sếp có bao giờ cảm thấy quá tải khi hàng trăm email đổ về mỗi tuần? Việc đọc thủ công, tổng hợp ý chính hay tìm kiếm các chủ đề ẩn giấu trong hộp thư không chỉ tốn thời gian mà rất dễ bỏ lỡ những thông tin quan trọng. 

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code giúp các sếp giải quyết triệt để vấn đề đó. Hệ thống sẽ tự động trích xuất email theo điều kiện tùy chỉnh, phân tích nội dung bằng AI **Google Gemini**, tạo biểu đồ tri thức dạng **Knowledge Graph** qua **InfraNodus** để tìm ra các "khoảng trống thông tin" (structural gaps), và gửi báo cáo trực quan cùng câu hỏi gợi ý thẳng về **Telegram** của các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối:** Tự động hóa toàn bộ quy trình đọc, lọc, tổng hợp và phân tích email mà không cần đụng tay.
- **Phát hiện insights ẩn giấu:** Sử dụng công nghệ Knowledge Graph của InfraNodus để tìm ra các chủ đề lặp lại và khoảng trống tư duy trong các cuộc trò chuyện.
- **Cá nhân hóa linh hoạt:** Lọc email qua từ khóa, nhãn (labels), ngày tháng hoặc tiêu chí nâng cao do AI định nghĩa.
- **Nhận thông báo tức thì:** Cập nhật tóm tắt chủ đề và câu hỏi gợi ý qua Telegram mọi lúc, mọi nơi.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản sau:
- **Tài khoản n8n** (Self-hosted hoặc Cloud).
- **Tài khoản Gmail** (với Google Cloud OAuth Credentials để kết nối node Gmail).
- **Tài khoản InfraNodus** kèm API Key ([Lấy tại đây](https://infranodus.com/api-access)).
- **Google AI Studio API Key** (dành cho node Google Gemini, lấy cực nhanh trong 30 giây).
- **Telegram Bot Token** (tạo qua [@botfather](https://t.me/botfather) để nhận thông báo).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ hệ thống n8n hoặc copy toàn bộ mã nguồn JSON dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 27 nodes được thiết kế mạch lạc. Các sếp chú ý cấu hình kỹ các điểm sau:
- **Trigger Nodes (`User submits form`, `Schedule Trigger`, `When clicking ‘Test workflow’`):** Chọn phương thức kích hoạt phù hợp với nhu cầu (chạy định kỳ hàng ngày, qua form bảo mật, hoặc thủ công). Nhớ kích hoạt (Active) đúng trigger cần dùng và tắt các cái còn lại.
- **Node `Assign Processing Settings` (Bước 2):** Nơi cấu hình các thông số mặc định cho việc trích xuất email (chuỗi tìm kiếm, nhãn, khoảng thời gian, loại graph muốn xây dựng). Các sếp có thể dùng cú pháp tìm kiếm Gmail như `after:2025/06/01` hoặc `label:notes` để tăng tốc độ xử lý.
- **Nodes `Gmail` & `Get Full Message Content` (Bước 3 & 4):** Kết nối tài khoản Gmail thông qua **GmailOAuth2 credentials**. Node này sẽ quét các email thỏa mãn điều kiện lọc.
- **Node `Classify Emails` & `Google Gemini Chat Model` (Bước 5):** Cấu hình **GooglePalmApi credentials** bằng cách nhập API Key từ Google AI Studio. Node này giúp AI phân loại email nâng cao theo yêu cầu của các sếp.
- **Nodes `InfraNodus Build a Text Knowledge Graph`, `InfraNodus Build a Social Knowledge Graph`, `InfraNodus Question Generator` & `InfraNodus AI Summary & Graph Link` (Bước 7 & 8):** Cấu hình **HTTP Bearer Auth credentials** với InfraNodus API Key. Đảm bảo điền đúng tên Graph (`name`) mà các sếp muốn lưu dữ liệu trên InfraNodus.
- **Nodes `Send the graph link and summary via Telegram` & `Send an insight question via Telegram` (Bước 9):** Kết nối **Telegram API credentials** bằng Bot Token lấy từ `@botfather` và điền Chat ID của các sếp để nhận thông báo.

#### 3. Kích hoạt ⚡️
- Nhấn **Test workflow** để chạy thử nghiệm với một vài email mẫu và kiểm tra kết quả trả về trên Telegram.
- Sau khi mọi thứ mượt mà, gạt công tắc sang **Active** để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Ngoài Telegram, các sếp có thể gắn thêm node Slack hoặc Discord để gửi bản tóm tắt Knowledge Graph vào kênh chat chung của team.
- **Lưu trữ dữ liệu:** Kết nối thêm node Google Sheets hoặc Airtable để lưu lại lịch sử các bản tóm tắt và câu hỏi insight phục vụ cho việc tra cứu sau này.
- **Tối ưu hiệu suất:** Sử dụng kết hợp các nhãn Gmail (`label:sent`, `label:personal`) để giới hạn phạm vi quét email, giúp workflow chạy nhanh hơn và tiết kiệm tài nguyên AI.

### 📌 Kết luận
Với workflow n8n kết hợp giữa Gmail, Google Gemini và InfraNodus này, việc quản lý và khai thác thông tin từ hộp thư điện tử chưa bao giờ dễ dàng và trực quan đến thế. Hãy cài đặt ngay để biến hàng ngàn email rờm rà thành những biểu đồ tri thức sắc bén và những ý tưởng kinh doanh đắt giá!