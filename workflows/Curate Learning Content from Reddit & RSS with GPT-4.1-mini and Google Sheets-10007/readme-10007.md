---
title: "🚀 Tự động tổng hợp và lọc nội dung học tập từ Reddit & RSS bằng AI và Google Sheets"
description: "Xây dựng hệ thống tự động quét, lọc nội dung học tập chất lượng cao từ Reddit và các nguồn RSS dựa trên từ khóa, sau đó lưu trữ gọn gàng vào Google Sheets."
slug: "tu-dong-tong-hop-noi-dung-hoc-tap-reddit-rss-ai"
tags: [n8n, automation, no-code, ai-summarization, market-research, google-sheets, openai]
keywords: [n8n workflow, tự động hóa học tập, lọc nội dung AI, tích hợp Reddit RSS, Google Sheets automation]
---

# 🚀 Tự động tổng hợp và lọc nội dung học tập từ Reddit & RSS bằng AI và Google Sheets

Các sếp có đang cảm thấy quá tải khi mỗi ngày phải thủ công tìm kiếm tài liệu, bài viết hướng dẫn, khóa học hay tin tức chuyên ngành từ hàng loạt trang web, blog RSS và các cộng đồng lớn như Reddit không? Việc này vừa tốn thời gian, dễ bỏ sót thông tin quan trọng lại vừa mệt mỏi.

Giải pháp ở đây là gì? Workflow n8n này sẽ tự động hóa 100% quy trình: Quét thông tin theo từ khóa định sẵn $\rightarrow$ Lọc qua AI thông minh để bỏ qua rác/quảng cáo $\rightarrow$ Lưu kết quả chất lượng cao thẳng vào Google Sheets. Các sếp chỉ việc mở bảng ra và đọc những kiến thức tinh hoa nhất mỗi ngày!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần tự tay lướt Reddit hay check từng trang RSS feed nữa.
- **Nội dung cực kỳ chất lượng:** Nhờ sức mạnh của AI (GPT-4.1-mini), hệ thống tự động loại bỏ các bài viết quảng cáo, kém chất lượng và chỉ giữ lại tài liệu học tập thực sự hữu ích.
- **Hoạt động tự động 24/7:** Chạy định kỳ 2 lần mỗi ngày (sáng và chiều) theo lịch trình cài sẵn.
- **Lưu trữ khoa học:** Mọi bài viết hay, tóm tắt và nguồn đều được gom gọn gàng vào Google Sheets để dễ dàng tra cứu, ôn tập bất cứ lúc nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google Sheets:** Tài khoản Google để đọc từ khóa và lưu kết quả bài viết.
- **OpenAI API Key:** Để sử dụng model `gpt-4.1-mini` trong việc phân tích và lọc nội dung.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ n8n template hoặc copy toàn bộ JSON, sau đó paste trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node trọng điểm sau:
- **`Get Keywords from Google Sheets`** & **`Save to Google Sheets`**: Kết nối tài khoản Google trong phần Credentials. Trỏ đúng đến file Google Sheet quản lý từ khóa, nguồn RSS và nơi lưu trữ kết quả.
- **`Workflow Configuration`** (Node `set`): Khai báo các biến cấu hình chung nếu cần thiết (ví dụ: giới hạn số lượng bài viết quét mỗi lần).
- **`OpenAI Chat Model`** (`lmChatOpenAi`): Chọn model `gpt-4.1-mini` và đảm bảo đã điền OpenAI API Key hợp lệ trong Credentials của n8n.
- **`Schedule Trigger - Twice Daily`**: Mặc định workflow chạy 2 lần/ngày (8 giờ sáng và 6 giờ tối). Các sếp có thể thay đổi thời gian này tùy theo nhu cầu cá nhân.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử thủ công một lần với dữ liệu mẫu để kiểm tra xem từ khóa, RSS, Reddit API và AI hoạt động thông suốt chưa.
- Nếu mọi thứ xanh mướt (success), hãy gạt công tắc sang **Active** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa dạng hóa nguồn dữ liệu:** Ngoài RSS và Reddit, các sếp có thể mở rộng thêm node gọi API từ Medium, Dev.to hoặc YouTube để vét toàn bộ tri thức về một mối.
- **Tích hợp thông báo:** Nối thêm node Telegram Bot hoặc Slack vào cuối quy trình để mỗi khi AI tìm được bài viết hay, hệ thống sẽ bắn tin nhắn "ting ting" trực tiếp vào điện thoại cho các sếp đọc ngay.
- **Tùy chỉnh Prompt AI:** Tinh chỉnh tiêu chí trong AI Agent (ví dụ: ưu tiên bài viết lập trình Python, Marketing, hoặc Kinh doanh...) để AI phục vụ chính xác mục tiêu học tập của bạn.

### 📌 Kết luận
Một trợ lý ảo tự động tổng hợp tri thức hoàn toàn miễn phí (chi phí gọi API cực thấp với `gpt-4.1-mini`) đang nằm trong tầm tay. Cài đặt ngay hôm nay để tối ưu hóa thời gian học tập và nâng cấp bản thân mỗi ngày các sếp nhé!