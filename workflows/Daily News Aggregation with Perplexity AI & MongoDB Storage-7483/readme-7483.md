---
title: "🚀 Tự động tổng hợp tin tức hằng ngày với Perplexity AI và lưu trữ vào MongoDB qua n8n"
description: "Xây dựng hệ thống tự động cào tin tức nóng hổi mỗi ngày bằng Perplexity AI (Sonar Pro), chuẩn hóa dữ liệu, lưu vào MongoDB và gửi báo cáo qua Gmail."
slug: "tu-dong-tong-hop-tin-tuc-perplexity-ai-mongodb-n8n"
tags: [n8n, automation, perplexity, mongodb, ai-agents, gmail]
keywords: [n8n workflow, tổng hợp tin tức tự động, perplexity ai, mongodb n8n, automation no-code]
keywords: [n8n workflow, tổng hợp tin tức tự động, perplexity ai, mongodb n8n, automation no-code]
---

# 🚀 Tự động tổng hợp tin tức hằng ngày với Perplexity AI và lưu trữ vào MongoDB

Các sếp có tốn quá nhiều thời gian mỗi sáng để lướt các trang tin tức nhằm nắm bắt tình hình thị trường, công nghệ hay ngách kinh doanh của mình không? Việc tổng hợp thủ công này vừa tốn thời gian, lại dễ bỏ sót các thông tin quan trọng.

Đừng lo, workflow n8n này sẽ giúp các sếp giải quyết triệt để bài toán đó! Hệ thống sẽ tự động hóa 100% quy trình: Dùng **Perplexity AI** quét tin tức toàn cầu theo yêu cầu, xử lý và lưu trữ gọn gàng vào **MongoDB**, đồng thời gửi một email tổng hợp báo cáo qua **Gmail** mỗi ngày. Không cần code phức tạp, các sếp chỉ cần "lên đồ" và chạy!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 99% thời gian:** Không cần tự tìm kiếm, phân loại tin tức mỗi ngày.
- **Cập nhật thông tin thông minh:** Tận dụng sức mạnh AI của Perplexity (model Sonar Pro) để lấy dữ liệu tin tức mới nhất kèm nguồn uy tín.
- **Lưu trữ dữ liệu có cấu trúc:** Tự động đẩy toàn bộ tin tức vào MongoDB để tiện tra cứu, phân tích về sau.
- **Báo cáo trực quan qua email:** Nhận ngay bản tổng hợp tin tức gọn gàng vào hòm thư Gmail định kỳ mỗi sáng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow này chạy mượt mà, các sếp cần chuẩn bị sẵn:
- **Tài khoản/Server n8n** (Cloud hoặc Self-hosted).
- **Perplexity API Key** (để gọi model AI lấy tin tức).
- **MongoDB** (Database để lưu trữ tin tức, có thể dùng MongoDB Atlas miễn phí).
- **Tài khoản Gmail** (Kết nối qua OAuth2 để gửi email thông báo).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ nguồn gốc hoặc copy toàn bộ JSON cấu trúc và dán trực tiếp vào n8n Editor của mình. Workflow bao gồm 7 nodes chính liên kết chặt chẽ với nhau.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống hoạt động trơn tru, các sếp cần cấu hình chính xác các node sau:

- **Schedule Trigger:** Mặc định được cấu hình chạy tự động mỗi ngày (ví dụ: lúc 8:00 sáng). Các sếp có thể tùy chỉnh lại Cron expression theo khung giờ mong muốn.
- **Perplexity:** 
  - Chọn Credentials: `perplexityApi` và điền API Key của các sếp.
  - Key Parameters: Chọn Model `sonar-pro`.
  - Prompt: Viết câu lệnh yêu cầu AI lấy tin tức theo chủ đề mong muốn và bắt buộc trả về định dạng JSON (bao gồm: headline, timestamp, source, url, category, metadata).
- **Response Perplexity (Code Node):** Node này dùng đoạn script JavaScript để làm sạch dữ liệu trả về từ Perplexity (loại bỏ markdown như ```json, ```) và chuyển đổi thành dạng mảng (array) để chuẩn bị loop.
- **Loop Over News (Split In Batches):** Đóng vai trò lặp qua từng bản tin để xử lý đưa vào Database mà không sợ bị quá tải.
- **DB News (MongoDB):** 
  - Chọn Credentials: `mongoDb`.
  - Key Parameters: Chọn Operation là `Insert`.
  - Cấu hình Collection name (ví dụ: `daily_news`) để lưu trữ các trường dữ liệu tin tức.
- **News (Code Node):** Gom nhóm lại các kết quả sau khi đã lưu xong vào database để chuẩn bị nội dung gửi email.
- **Send Message (Gmail):** 
  - Chọn Credentials: `gmailOAuth2`.
  - Cấu hình địa chỉ email nhận báo cáo và tiêu đề email tự động.

#### 3. Kích hoạt ⚡️
- Nhấn **Test Workflow** để chạy thử nghiệm xem dữ liệu có chảy mượt từ Perplexity qua MongoDB và gửi email thành công hay không.
- Nếu mọi thứ xanh mướt, hãy gạt công tắc sang **Active** để workflow tự động chạy ngầm mỗi ngày!

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống "xịn sò" hơn nữa, các sếp có thể mở rộng workflow này với các ý tưởng:
- **Tích hợp thêm Telegram/Slack:** Thay vì chỉ gửi Gmail, bắn một bản tin tóm tắt lên nhóm Telegram công ty để team cùng đọc mỗi sáng.
- **Lọc tin thông minh:** Thêm một node AI hoặc điều kiện (If) để chỉ lấy những tin tức có chứa từ khóa liên quan trực tiếp đến ngành nghề của công ty.
- **Lưu trữ Google Sheets:** Nếu không dùng MongoDB, các sếp hoàn toàn có thể đổi sang node Google Sheets để lưu tin dạng bảng tính dễ nhìn.

### 📌 Kết luận
Chỉ với một workflow n8n gọn nhẹ, các sếp đã xây dựng thành công một "trợ lý AI" tự động điểm tin mỗi ngày. Hãy áp dụng ngay để tối ưu hóa nguồn thông tin cho bản thân hoặc doanh nghiệp của mình nhé! Chúc các sếp thao tác thành công!