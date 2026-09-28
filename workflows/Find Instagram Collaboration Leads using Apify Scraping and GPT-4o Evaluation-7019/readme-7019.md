---
title: "🚀 Tự động tìm kiếm và đánh giá Leads Instagram bằng Apify & GPT-4o"
description: "Hướng dẫn xây dựng workflow n8n tự động cào dữ liệu bài viết, profile Instagram qua Apify và sử dụng AI (GPT-4o-mini) để chấm điểm, lọc leads hợp tác chất lượng cao."
slug: "tu-dong-tim-kiem-va-danh-gia-leads-instagram-apify-gpt-4o"
tags: [n8n, automation, no-code, instagram, apify, openai, ai-agent, lead-generation]
keywords: [n8n workflow, cào instagram apify, ai lead scoring, gpt-4o-mini instagram, tự động hóa marketing, tìm kiếm leads instagram]
---

# 🚀 Tự động tìm kiếm và đánh giá Leads Instagram bằng Apify & GPT-4o

Các sếp có đang mệt mỏi vì phải lướt Instagram hàng giờ, thủ công tìm kiếm từng hashtag, bấm vào từng profile để đọc tiểu sử (bio), đếm số lượng người theo dõi (followers) xem họ có phù hợp để hợp tác hay không? Công việc thủ công này ngốn rất nhiều thời gian mà hiệu quả lại thấp.

Đừng lo, trong bài viết này, các sếp sẽ được hướng dẫn chi tiết cách thiết lập một workflow n8n tự động hóa 100% quy trình: Quét hashtag trên Instagram thông qua **Apify**, trích xuất thông tin profile, và để **GPT-4o-mini (AI Agent)** phân tích, chấm điểm, trả về dữ liệu JSON cực kỳ gọn gàng. Giải pháp này giúp các sếp tìm kiếm khách hàng tiềm năng (leads) mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Thay vì cào tay và đọc từng profile, AI sẽ tự động phân tích hàng loạt tài khoản trong vài giây.
- **Lọc leads chính xác:** AI Agent sử dụng prompt thông minh để đánh giá tiềm năng hợp tác dựa trên tiểu sử và lượng follower thực tế.
- **Dữ liệu cấu trúc sạch sẽ:** Kết quả đầu ra trả về dạng JSON chuẩn hóa, dễ dàng đẩy tiếp vào Google Sheets, CRM hoặc gửi thông báo qua Slack/Telegram.
- **Hoạt động linh hoạt:** Dễ dàng thay đổi từ khóa hashtag tìm kiếm chỉ với 1 thao tác nhỏ trên n8n.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow chạy mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
1. **Tài khoản n8n** (Cloud hoặc Self-hosted).
2. **Tài khoản Apify**: Lấy API Token tại [Apify Console](https://console.apify.com/).
3. **Tài khoản OpenAI**: Lấy API Key tại [OpenAI Platform](https://platform.openai.com/account/api-keys).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON của workflow này, copy và paste trực tiếp vào n8n Editor của mình để bắt đầu.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 8 nodes chính, các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Node `Create Search Term` (Set):** 
  - Mặc định workflow đang đặt từ khóa tìm kiếm hashtag Instagram là `"n8n"`. 
  - Các sếp có thể sửa lại giá trị này thành bất kỳ hashtag nào phù hợp với ngách kinh doanh của mình (ví dụ: `"marketing"`, `"dropshipping"`, `"fitness"`...).

- **Node `Find Recent Posts` (HTTP Request):**
  - Sử dụng Apify Instagram Hashtag Scraper.
  - Cần tạo **HTTP Query Auth** credential bằng cách lấy Token từ Apify Console và điền vào tham số `token` (dạng `?token=yourTokenHere`).

- **Node `Scrape Accounts` (HTTP Request):**
  - Sử dụng Apify Instagram Profile Scraper để cào chi tiết từng tài khoản tìm được từ bước trước.
  - Sử dụng chung một **HTTP Query Auth** credential như node bên trên.

- **Node `Set bio and follower count` (Set):**
  - Node này có nhiệm vụ bóc tách các trường dữ liệu quan trọng như `biography` và `followersCount` từ JSON thô của profile để chuẩn bị đầu vào cho AI.

- **Node `OpenAI Chat Model` & `AI Agent`:**
  - Chọn model `gpt-4o-mini`.
  - Kết nối tài khoản OpenAI của các sếp thông qua **OpenAI API** credential (dùng OpenAI API Key).

- **Node `Structured Output Parser`:**
  - Giúp ép kiểu phản hồi từ AI trả về đúng định dạng JSON có cấu trúc rõ ràng để tiện cho các bước xử lý tự động tiếp theo.

#### 3. Kích hoạt ⚡️
- Bấm nút **`When clicking ‘Execute workflow’`** để test chạy thử với dữ liệu mẫu.
- Kiểm tra kết quả đầu ra ở các node AI xem thông tin trả về đã chuẩn chưa.
- Sau khi mọi thứ mượt mà, hãy gạt công tắc **Active** góc trên bên phải để workflow chạy tự động theo lịch hoặc trigger.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa quy trình tìm kiếm leads hơn nữa, các sếp có thể mở rộng workflow bằng cách:
- **Lưu tự động:** Nối thêm node **Google Sheets** hoặc **Airtable** ngay sau Output Parser để tự động lưu danh sách tài khoản tiềm năng kèm điểm số đánh giá của AI.
- **Cảnh báo thời gian thực:** Thêm node **Telegram** hoặc **Slack** để bắn thông báo ngay lập tức về máy khi AI tìm được một lead "siêu chất lượng" (ví dụ: follower > 50k và điểm đánh giá > 9/10).
- **Chạy định kỳ:** Thay thế Manual Trigger bằng **Schedule Trigger** (ví dụ chạy 1 lần/tuần) để hệ thống tự động đi tìm leads mới mà không cần can thiệp thủ công.

### 📌 Kết luận
Việc ứng dụng AI và công cụ No-code như n8n kết hợp với Apify sẽ giúp tối ưu hóa cực tốt các chiến dịch outreach và tìm kiếm khách hàng. Hãy triển khai ngay workflow này để tối ưu hóa thời gian và gia tăng tỷ lệ chuyển đổi cho doanh nghiệp của các sếp nhé!