---
title: "🚀 Tự động giám sát thầu IT BOAMP và chấm điểm bằng GPT-4o Mini lưu vào Supabase"
description: "Hướng dẫn xây dựng workflow n8n tự động săn thầu công nghệ từ BOAMP, sử dụng AI phân tích, chấm điểm độ phù hợp và lưu trữ tập trung vào Supabase."
slug: "tu-dong-giam-sat-thau-it-boamp-gpt-4o-mini-supabase"
tags: [n8n, automation, no-code, ai, openai, supabase, market-research]
keywords: [n8n workflow, tự động hóa đấu thầu, BOAMP IT tenders, GPT-4o Mini, Supabase integration, AI summarization]
---

# 🚀 Tự động giám sát thầu IT BOAMP và chấm điểm bằng GPT-4o Mini lưu vào Supabase

Việc thủ công tìm kiếm các gói thầu công nghệ (IT tenders) trên các cổng thông tin công công như BOAMP (Chính phủ Pháp) cực kỳ tốn thời gian và dễ bỏ lỡ các cơ hội vàng. Doanh nghiệp thường mất hàng giờ mỗi ngày chỉ để lọc qua danh sách dài các dự án không phù hợp.

Giải pháp? Workflow n8n này sẽ tự động hóa toàn bộ quy trình: Tự động quét dữ liệu thầu, sử dụng trí tuệ nhân tạo (GPT-4o Mini) để phân tích, đánh giá độ phù hợp với năng lực công ty, và tự động lưu kết quả vào cơ sở dữ liệu Supabase để đội ngũ sales hoặc dev tiến hành tiếp cận ngay lập tức.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100%:** Không cần cử nhân sự ngồi canh cổng thông tin đấu thầu hàng ngày.
- **AI chấm điểm thông minh:** GPT-4o Mini giúp đọc hiểu mô tả dự án và chấm điểm độ khớp (matching score) dựa trên tiêu chí của công ty.
- **Lưu trữ chuẩn hóa:** Mọi thông tin dự án, điểm số và tóm tắt được đổ thẳng vào bảng Supabase, sẵn sàng để truy vấn.
- **Tiết kiệm chi phí & Thời gian:** Phản hồi nhanh chóng với các cơ hội thầu tiềm năng trước đối thủ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu "lên đồ", các sếp cần chuẩn bị sẵn:
- Một hệ thống n8n (Cloud hoặc Self-hosted).
- Tài khoản **OpenAI API Key** (để sử dụng GPT-4o Mini).
- Tài khoản **Supabase** và một bảng (Table) đã tạo sẵn để hứng dữ liệu thầu.
- Nguồn cấp dữ liệu thầu từ BOAMP (thông qua Webhook hoặc Schedule Trigger kết hợp HTTP Request).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ trang chủ n8n hoặc copy đoạn mã JSON tương ứng, sau đó dán trực tiếp vào n8n Editor của mình bằng phím tắt `Ctrl + V` (hoặc `Cmd + V`).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình kỹ các node trọng điểm sau:
- **Schedule Trigger / Webhook Node:** Cấu hình thời gian định kỳ chạy quét dữ liệu (ví dụ: chạy mỗi sáng lúc 8:00 AM) hoặc kích hoạt bằng webhook từ nguồn bên ngoài.
- **HTTP Request Node:** Trỏ tới API nguồn của BOAMP để lấy danh sách các gói thầu IT mới nhất trong ngày.
- **AI / OpenAI Node (GPT-4o Mini):** 
  - Chọn đúng Credentials của OpenAI.
  - Viết Prompt rõ ràng yêu cầu AI đóng vai chuyên gia đấu thầu, đọc nội dung gói thầu và trả về kết quả dạng JSON (gồm: Tiêu đề, Mô tả tóm tắt, Điểm số từ 1-10, và Lý do phù hợp).
- **If Node:** Thiết lập điều kiện lọc. Chỉ cho phép các gói thầu đạt điểm số từ AI vượt mức tối thiểu (ví dụ: `> 7`) được đi tiếp vào hệ thống.
- **Supabase Node:** 
  - Cấu hình Credentials kết nối đến dự án Supabase của các sếp.
  - Chọn đúng Table Name đã chuẩn bị để insert dữ liệu thầu đã qua lọc.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử với một vài bản ghi mẫu để kiểm tra dữ liệu trả về từ AI và Supabase.
- Sau khi chắc chắn mọi thứ trơn tru, hãy bật công tắc **Active** ở góc trên bên phải để n8n tự động hóa 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node Telegram hoặc Slack ngay sau khi lưu vào Supabase để bắn thông báo nóng về điện thoại cho Sales Lead khi có gói thầu siêu chất lượng (`Score = 10`).
- **Lưu log lỗi:** Sử dụng Error Trigger để bắt các lỗi phát sinh khi API OpenAI hoặc Supabase quá tải, tránh việc workflow bị treo âm thầm.
- **Mở rộng nguồn thầu:** Không chỉ BOAMP, các sếp có thể bổ sung thêm các cổng đấu thầu quốc tế hoặc khu vực khác vào chung một luồng xử lý AI.

### 📌 Kết luận
Tự động hóa săn thầu IT bằng n8n kết hợp GPT-4o Mini và Supabase là vũ khí cực mạnh giúp doanh nghiệp CNTT tiết kiệm hàng chục giờ nhân sự mỗi tuần và không bao giờ bỏ lỡ các hợp đồng béo bở. Hãy thiết lập ngay hôm nay để tối ưu hóa năng lực cạnh tranh cho doanh nghiệp của các sếp!