---
title: "🚀 Tự động trích xuất và gộp chuỗi bài đăng Twitter (X) Threads bằng TwitterAPI.io trên n8n"
description: "Hướng dẫn chi tiết cách sử dụng workflow n8n để tự động lấy toàn bộ nội dung của một chuỗi bài đăng (Twitter Thread) thông qua TwitterAPI.io và gộp lại hoàn chỉnh."
slug: "trich-xuat-va-gop-twitter-threads-n8n"
tags: [n8n, automation, no-code, twitter, marketing, ai, api]
keywords: [n8n workflow, twitter threads, trich xuat twitter, twitterapi.io, tu dong hoa marketing]
keywords: [n8n workflow, trích xuất twitter threads, twitterapi.io, tự động hóa marketing, code n8n]
---

# 🚀 Tự động trích xuất và gộp chuỗi bài đăng Twitter (X) Threads bằng TwitterAPI.io

Các sếp làm nội dung, marketing hay nghiên cứu thị trường chắc chắn đã từng "đau đầu" khi muốn đọc hoặc lưu lại một chuỗi bài đăng dài (Twitter/X Thread). Việc phải copy từng tweet thủ công rồi dán lại vừa tốn thời gian, vừa dễ bị sót ý, đặc biệt là khi cần tổng hợp tài nguyên để làm báo cáo hay phân tích xu hướng.

Giải pháp là đây! Workflow n8n mang tên **"Extract and Merge Twitter (X) Threads using TwitterAPI.io"** do tác giả *enes cingoz* phát triển sẽ giúp các sếp tự động hóa 100% quy trình này: từ việc nhận link bài đăng, gọi API lấy toàn bộ các tweet trong chuỗi, cho đến việc lọc và gộp chúng lại thành một nội dung liền mạch hoàn chỉnh. Không cần code phức tạp, chỉ cần vài cú click!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối:** Thay vì mất hàng giờ đọc và copy thủ công, workflow xử lý toàn bộ thread chỉ trong vài giây.
- **Nội dung liền mạch:** Tự động sắp xếp và gộp các tweet thành một bài viết hoàn chỉnh, dễ đọc, dễ lưu trữ.
- **Linh hoạt tích hợp:** Có thể kích hoạt thủ công để test hoặc chạy ngầm tự động thông qua việc kết nối với các workflow khác (như nhận link từ Telegram, Slack, Webhook...).
- **Hoạt động liên tục:** Sử dụng TwitterAPI.io mạnh mẽ, đảm bảo tỷ lệ gọi API thành công cao và không lo gián đoạn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted phiên bản mới).
- **TwitterAPI.io Account:** Cần có tài khoản và API Key hợp lệ từ TwitterAPI.io để truy xuất dữ liệu từ nền tảng X (Twitter).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy đoạn JSON gốc.
- Mở giao diện n8n của các sếp, chọn **Workflows** -> **Import from File** (hoặc dán trực tiếp vào màn hình Editor).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 11 nodes phối hợp nhịp nhàng với nhau để bóc tách và ghép nối dữ liệu. Các sếp cần chú ý các điểm sau khi cấu hình:

- **When clicking ‘Test workflow’** & **When Executed by Another Workflow**: Điểm khởi đầu của luồng. Các sếp có thể dùng nút test thủ công hoặc gọi từ workflow khác truyền vào link/ID bài đăng gốc.
- **Extract Tweet ID and Username** (Node loại `function`): Xử lý chuỗi URL đầu vào để trích xuất chính xác Tweet ID và Username của tác giả.
- **Get first tweet** (Node loại `httpRequest`): Gọi API tới TwitterAPI.io để lấy thông tin chi tiết của tweet mở đầu. Các sếp cần cấu hình Header chứa API Key của TwitterAPI.io tại đây.
- **Extract Conversation and Author ID** (Node loại `function`): Lấy Conversation ID và Author ID từ kết quả của tweet đầu tiên làm cơ sở để tìm các tweet trả lời tiếp theo trong cùng chuỗi thread.
- **Get Tweet Replies** (Node loại `httpRequest`): Gọi API lấy danh sách các phản hồi/tweet liên quan trong cùng một conversation.
- **Fetch tweets which are connected to first tweet** (Node loại `code`): Sử dụng đoạn mã JavaScript tùy chỉnh để lọc ra những tweet thực sự thuộc về thread chính (cùng tác giả, liên kết chặt chẽ với bài gốc).
- **Filter empty ones** (Node loại `filter`): Lọc bỏ các giá trị rỗng hoặc không hợp lệ.
- **Merge first tweet and others** & **Merge all tweet infos** (Các node loại `merge`): Kết hợp tweet mở đầu với các tweet tiếp theo trong chuỗi theo đúng thứ tự thời gian.

#### 3. Kích hoạt ⚡️
- Nhấn **Test workflow** để chạy thử với một đường link Twitter Thread mẫu và kiểm tra xem kết quả trả về ở node cuối cùng đã gộp đủ các ý chưa.
- Sau khi kiểm tra mọi thứ chạy mượt mà, hãy gạt công tắc sang **Active** để đưa workflow vào trạng thái sẵn sàng hoạt động.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ tự động:** Kết nối node cuối cùng với Google Sheets hoặc Notion để tự động lưu lại nội dung các thread hay mà các sếp muốn sưu tầm.
- **Tóm tắt bằng AI:** Thêm một node AI (như OpenAI / Claude) ngay sau bước gộp thread để tự động tạo bản tóm tắt (summary) ngắn gọn cho bài đăng dài.
- **Gửi về Telegram/Slack:** Tích hợp thêm node thông báo để mỗi khi có chuỗi bài đăng quan trọng được trích xuất, nội dung sẽ được gửi thẳng về nhóm chat nội bộ cho team cùng đọc.

### 📌 Kết luận
Workflow "Extract and Merge Twitter (X) Threads using TwitterAPI.io" là một công cụ cực kỳ mạnh mẽ giúp các sếp tối ưu hóa việc nghiên cứu nội dung trên nền tảng X. Hãy cài đặt ngay hôm nay để biến những chuỗi bài đăng dài dòng thành dữ liệu gọn gàng, sẵn sàng phục vụ cho công việc của các sếp!