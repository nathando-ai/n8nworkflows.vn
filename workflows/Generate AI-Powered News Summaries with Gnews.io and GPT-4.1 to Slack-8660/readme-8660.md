---
title: "🚀 Tự động tổng hợp và tóm tắt tin tức bằng AI (Gnews.io & GPT-4.1) gửi thẳng vào Slack"
description: "Xây dựng AI Agent tự động tìm kiếm tin tức thời gian thực từ Gnews.io, sử dụng GPT-4.1 để tóm tắt và gửi báo cáo chuyên nghiệp qua Slack chỉ với 1 form nhập liệu."
slug: "tu-dong-tong-hop-tom-tat-tin-tuc-gnews-gpt4-slack"
tags: [n8n, automation, no-code, ai-summarization, gnews, openai, slack]
keywords: [n8n workflow, tóm tắt tin tức tự động, gnews io, gpt 4.1, slack automation, ai agent n8n]
---

# 🚀 Tự động tổng hợp và tóm tắt tin tức bằng AI (Gnews.io & GPT-4.1) gửi thẳng vào Slack

Các sếp có đang tốn hàng giờ mỗi ngày chỉ để lướt web, đọc báo, chọn lọc và tóm tắt thông tin thị trường, đối thủ cạnh tranh hoặc công nghệ mới? Việc làm thủ công này không chỉ ngốn thời gian mà còn dễ bỏ sót các tin tức quan trọng. 

Đừng lo, bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ thông minh do chuyên gia Omer Fayyaz thiết kế. Workflow này sẽ đóng vai trò như một **AI News Agent** thực thụ: Nhận chủ đề từ form, tự động quét tin mới nhất từ Gnews.io, nhờ GPT-4.1 chắt lọc và tóm tắt, sau đó bắn thẳng kết quả đẹp mắt về Slack cho team cùng đọc!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần tự đọc và tổng hợp thủ công hàng chục bài báo mỗi ngày.
- **Thông tin chắt lọc thông minh:** AI tự động chọn ra top 15 bài viết chất lượng và liên quan nhất từ Gnews.io.
- **Định dạng chuyên nghiệp:** Báo cáo trả về Slack có sẵn tiêu đề, ngày tháng và link gốc rõ ràng, dễ đọc.
- **Giao diện thân thiện:** Kích hoạt dễ dàng thông qua một Web Form đơn giản do người dùng tự nhập chủ đề quan tâm.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản OpenAI:** Lấy OpenAI API Key để kết nối với model GPT-4.1.
- **Tài khoản Gnews.io:** Đăng ký tài khoản miễn phí/ trả phí tại [gnews.io](https://gnews.io) để lấy API Key.
- **Slack Workspace:** Quyền cấu hình hoặc tích hợp Webhook/Bot để nhận tin nhắn thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sao chép mã JSON của workflow từ nguồn cung cấp và dán trực tiếp vào giao diện n8n Editor của mình (hoặc sử dụng tính năng import từ file JSON).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 6 nodes chính hoạt động nhịp nhàng với nhau. Các sếp cần cấu hình kỹ các điểm sau:

- **Node `On form submission` (Form Trigger):** Node này tạo một giao diện Web Form để người dùng nhập chủ đề tin tức muốn tìm kiếm. Các sếp có thể tuỳ chỉnh giao diện form nếu muốn.
- **Node `Get GNews articles` (HTTP Request):** 
  - Đây là nơi gọi API của Gnews.io.
  - Các sếp nhớ thay thế đoạn `"ADD YOUR API HERE"` bằng **Gnews.io API Key** thực tế của mình.
- **Node `GPT-4.1 Model` (OpenAI Chat Model):** 
  - Cần chọn credentials tài khoản OpenAI của các sếp.
  - Đảm bảo model được cấu hình chính xác là `gpt-4.1`.
- **Node `AI News Summarizer` (Advanced AI Agent):** Node cốt lõi điều phối việc xử lý dữ liệu từ Gnews, kết hợp với OpenAI để lọc và viết tóm tắt.
- **Node `Map to articles` (Set):** Dùng để chuẩn hóa dữ liệu đầu ra trước khi gửi đi.
- **Node `Completed Notification` (Slack):** 
  - Kết nối với tài khoản Slack của doanh nghiệp (`slackApi`).
  - Chọn kênh (Channel) trên Slack mà các sếp muốn bot gửi bản tin tóm tắt vào đó mỗi khi hoàn thành.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách điền một chủ đề bất kỳ lên Web Form để kiểm tra dòng dữ liệu chạy qua từng node.
- Nếu mọi thứ hiển thị mượt mà trên Slack, hãy gạt công tắc sang **Active** để hệ thống tự động hóa vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa quy trình hơn nữa, các sếp có thể mở rộng workflow này bằng cách:
- **Tích hợp thêm Google Sheets:** Lưu lại lịch sử các bản tin đã tóm tắt để tra cứu lại sau này.
- **Đa kênh thông báo:** Ngoài Slack, có thể duplicate nhánh gửi sang Telegram Bot hoặc Email cho sếp lớn.
- **Lên lịch tự động (Schedule Trigger):** Thay vì dùng Form thủ công, các sếp có thể cài đặt giờ cố định mỗi sáng (ví dụ 8:00 AM) để AI tự động quét tin tức về một lĩnh vực quen thuộc (như AI, Crypto, Bất động sản) và gửi báo cáo chào ngày mới.

### 📌 Kết luận
Với workflow n8n kết hợp Gnews.io và GPT-4.1 này, việc cập nhật tin tức thị trường chưa bao giờ dễ dàng và tự động đến thế. Hãy "lên đồ" ngay cho hệ thống của mình để tối ưu hóa năng suất làm việc ngay hôm nay các sếp nhé!