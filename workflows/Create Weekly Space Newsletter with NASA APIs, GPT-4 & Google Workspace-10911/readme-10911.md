---
title: "🚀 Tự động tạo bản tin khám phá vũ trụ hàng tuần với NASA API, GPT-4 & Google Workspace"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy dữ liệu từ NASA, sử dụng OpenAI viết nội dung bản tin, xuất bản Google Docs, gửi Email và lưu trữ Notion."
slug: "tu-dong-tao-ban-tin-vu-tru-nasa-gpt4-google-workspace"
tags: [n8n, automation, nasa-api, openai, google-workspace, notion, slack]
keywords: [n8n workflow, tự động hóa bản tin, NASA API, OpenAI GPT-4, Google Docs, Gmail automation]
---

# 🚀 Tự động tạo bản tin khám phá vũ trụ hàng tuần với NASA API, GPT-4 & Google Workspace

Các sếp có bao giờ tốn hàng giờ mỗi tuần để tổng hợp thông tin, viết bài, định dạng tài liệu và gửi bản tin (newsletter) cập nhật cho đội ngũ hay khách hàng chưa? Công việc thủ công này cực kỳ nhàm chán và dễ bỏ sót thông tin. 

Với workflow n8n cực đỉnh này, toàn bộ quy trình từ việc **"hút" dữ liệu khoa học vũ trụ mới nhất từ NASA**, dùng **AI (GPT-4) nhào nặn thành bài viết hấp dẫn**, tự động **tạo Google Docs**, **chuyển đổi thành PDF**, **gửi email qua Gmail**, **lưu trữ vào Notion** và **báo cáo lên Slack** sẽ diễn ra hoàn toàn tự động 100% mà không cần tốn một giọt mồ hôi!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100%:** Định kỳ thứ Hai hàng tuần, hệ thống tự động càn quét dữ liệu vũ trụ mới nhất từ NASA.
- **Nội dung thông minh, sống động:** GPT-4 biên tập dữ liệu khô khan thành một bản tin hấp dẫn, lôi cuốn người đọc.
- **Chuyên nghiệp hóa tài liệu:** Tự động tạo Google Docs, xuất file PDF đẹp mắt và phân phối qua Gmail.
- **Lưu trữ & Báo cáo minh bạch:** Tự động backup bản tin vào Notion và bắn thông báo thành công lên Slack để team cùng theo dõi.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **NASA API Key:** Đăng ký miễn phí tại [api.nasa.gov](https://api.nasa.gov)
- **OpenAI API Key:** Tài khoản OpenAI có sẵn credit để gọi GPT-4.
- **Google Workspace Account:** Tài khoản Google để kết nối Google Docs, Google Drive và Gmail.
- **Notion Integration & Database:** (Tùy chọn) Để lưu trữ bản tin vào workspace Notion.
- **Slack Webhook / Integration:** (Tùy chọn) Để nhận thông báo trạng thái chạy workflow.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow (hoặc tải file JSON từ n8n.io/workflows/10911) và paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 14 nodes hoạt động nhịp nhàng với nhau. Các sếp chú ý cấu hình kỹ các điểm sau:

- **Weekly Monday Trigger:** Node này mặc định chạy vào 9 giờ sáng thứ Hai hàng tuần. Các sếp có thể đổi lại lịch nếu muốn.
- **Prepare NASA API URLs (Code node):** Đây là nơi quan trọng. Các sếp nhớ **thay thế chữ `'DEMO_KEY'`** bằng API Key thực tế lấy từ trang NASA. Node này sẽ gọi 3 API chính:
  - *APOD* (Astronomy Picture of the Day - Ảnh thiên văn trong ngày)
  - *DONKI* (Space Weather - Thời tiết không gian)
  - *NeoWS* (Near Earth Objects - Các tiểu hành tinh gần Trái Đất)
- **Generate Newsletter with AI (OpenAI node):** Cấu hình OpenAI Credentials. Các sếp có thể tinh chỉnh lại Prompt trong node này để thay đổi phong cách văn bản (vui tươi, trang trọng, ngắn gọn...) hoặc chuyển đổi ngôn ngữ sang Tiếng Việt hoàn toàn.
- **Create Google Doc & Insert Newsletter Content:** Kết nối tài khoản Google Docs, chỉ định thư mục lưu trữ file bản tin hàng tuần.
- **Convert to PDF (Google Drive node):** Node này lấy Google Doc vừa tạo và tải về dưới định dạng PDF để chuẩn bị đính kèm.
- **Send Newsletter Email (Gmail node):** Cấu hình danh sách người nhận (To, CC), tiêu đề và nội dung email đính kèm file PDF.
- **Archive to Notion (Notion node):** *(Mặc định có thể bị tắt)* Các sếp bật node này lên, chọn Database ID trên Notion để hệ thống tự động thêm một trang mới lưu trữ nội dung bản tin mỗi tuần.
- **Notify Success on Slack (Slack node):** Chọn kênh (Channel) trên Slack để nhận thông báo mỗi khi bản tin được phát hành thành công.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm thủ công (Test Run) kiểm tra toàn bộ luồng từ NASA -> AI -> Google Docs -> Gmail -> Slack.
- Nếu mọi thứ xanh mướt (success), các sếp gạt công tắc sang **Active** để hệ thống tự động chạy ngầm từ tuần tới!

### ✍️ Mẹo & gợi ý nâng cao
- **Đa dạng hóa kênh phân phối:** Ngoài Gmail và Slack, các sếp có thể gắn thêm node Telegram Bot để bắn bản tin thẳng vào nhóm chat Telegram của công ty/cộng đồng.
- **Tùy biến ngôn ngữ:** Mặc định NASA trả về tiếng Anh, sếp có thể yêu cầu OpenAI dịch và biên tập hoàn toàn bằng tiếng Việt để phù hợp với độc giả Việt Nam.
- **Lưu log lỗi:** Thêm nhánh Error Trigger để nếu API NASA lỗi hoặc OpenAI hết tiền, hệ thống sẽ cảnh báo ngay qua Telegram/Slack cho admin xử lý.

### 📌 Kết luận
Workflow tự động hóa tạo bản tin vũ trụ này là một minh chứng tuyệt vời cho sức mạnh kết hợp giữa No-Code (n8n), Open Data (NASA) và Generative AI. Hãy áp dụng ngay để tiết kiệm hàng chục giờ làm việc thủ công mỗi tháng và mang lại trải nghiệm cực kỳ chuyên nghiệp cho khách hàng của các sếp nhé!