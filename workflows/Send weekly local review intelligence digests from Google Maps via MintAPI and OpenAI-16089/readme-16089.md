---
title: "🚀 Gửi Báo Cáo Đánh Giá Địa Phương Hàng Tuần Từ Google Maps Bằng MintAPI & OpenAI"
description: "Tự động thu thập, tổng hợp và gửi báo cáo đánh giá doanh nghiệp trên Google Maps mỗi tuần chỉ với một workflow n8n – không cần viết code."
slug: "gui-bao-cao-danh-gia-dia-phuong-hang-tuan"
tags: [n8n, automation, no-code, market-research, ai, email]
keywords: [n8n workflow, tự động hóa, Google Maps, MintAPI, OpenAI, review digest]
---

# 🚀 Gửi Báo Cáo Đánh Giá Địa Phương Hàng Tuần Từ Google Maps Bằng MintAPI & OpenAI

Doanh nghiệp thường phải tốn hàng giờ mỗi tuần để **thu thập** các đánh giá trên Google Maps, **đọc** từng bình luận, rồi **tổng hợp** thành báo cáo cho bộ phận marketing hoặc quản lý.  
Quá trình này không chỉ mất thời gian mà còn dễ sai sót, và hầu như không thể thực hiện **liên tục** 24/7.

**Workflow n8n** này giải quyết toàn bộ chuỗi công việc trên bằng cách:

1. **Kích hoạt** tự động mỗi thứ Hai lúc 9h sáng (hoặc thủ công).  
2. **Lấy danh sách doanh nghiệp** trong khu vực mục tiêu qua **MintAPI**.  
3. **Thu thập các review mới nhất** của từng doanh nghiệp.  
4. **Dùng OpenAI** để tóm tắt, phân tích và tạo “digest” thông minh.  
5. **Soạn email** và gửi báo cáo tới người nhận chỉ trong vài giây.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động thu thập và tóm tắt review trong vòng vài phút.  
- **Độ chính xác cao**: OpenAI xử lý ngôn ngữ tự nhiên, giảm thiểu lỗi con người.  
- **Cá nhân hoá**: Thay đổi query, khu vực, tiêu chí để phù hợp với chiến dịch cụ thể.  
- **Hoạt động liên tục**: Không cần can thiệp thủ công, báo cáo luôn được gửi đúng lịch.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **MintAPI Key** – đăng ký tại https://mintapi.dev/.  
- **OpenAI API Key** – có quyền truy cập `gpt-3.5-turbo` hoặc `gpt-4`.  
- **Máy chủ email** (SMTP) – để node `Email Send` có thể gửi báo cáo.  
- **n8n** (cài đặt trên VPS hoặc Docker) – phiên bản mới nhất.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở **n8n Editor**.  
2. Nhấn **Import** → **Upload JSON** và chọn file workflow (hoặc copy toàn bộ JSON từ nguồn).  
3. Xác nhận để workflow xuất hiện trên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là **điểm danh** các node quan trọng và hướng dẫn cấu hình chi tiết:

| Node | Loại | Hướng dẫn cấu hình |
|------|------|-------------------|
| **Manual Execution Trigger** | manualTrigger | Không cần cấu hình – dùng để chạy thử nhanh. |
| **When Monday at 9am** | scheduleTrigger | - **Cron**: `0 9 * * 1` (thứ Hai 09:00). <br> - Đánh dấu **Active** để tự động chạy. |
| **Set Template Parameters** | set | Thêm các trường: <br> - `searchQuery` (ví dụ: `"cafe Ho Chi Minh City"`). <br> - `location` (lat,lng). <br> - `radius` (mét). <br> - `language` (ví dụ: `"vi"`). <br> - `maxResults` (số doanh nghiệp tối đa). |
| **Fetch Google Maps Businesses** | httpRequest | - **Method**: `GET`. <br> - **URL**: `https://api.mintapi.dev/v1/places/search`. <br> - **Query Parameters**: `query={{$json["searchQuery"]}}&location={{$json["location"]}}&radius={{$json["radius"]}}&language={{$json["language"]}}&limit={{$json["maxResults"]}}`. <br> - **Authentication**: Chọn **httpHeaderAuth** → nhập **MintAPI Key** trong header `Authorization: Bearer <YOUR_MINTAPI_KEY>`. |
| **Prepare Competitor Data** | code | JavaScript code (được cung cấp trong workflow) để lọc các trường cần thiết (place_id, name, address, rating, …). Không cần thay đổi nếu không muốn tùy biến. |
| **Fetch Latest Business Reviews** | httpRequest | - **Method**: `GET`. <br> - **URL**: `https://api.mintapi.dev/v1/places/{{ $json["place_id"] }}/reviews`. <br> - **Authentication**: Cũng dùng **httpHeaderAuth** với MintAPI Key. |
| **Build AI Review Prompt** | code | Tạo chuỗi prompt cho OpenAI, ví dụ: <br>```js\nreturn `Bạn là chuyên gia marketing. Hãy tóm tắt các review sau cho doanh nghiệp {{name}}:\n{{reviews}}\nCung cấp insight về điểm mạnh, điểm yếu và đề xuất cải thiện.`;\n``` |
| **Generate Review Digest via OpenAI** | httpRequest | - **Method**: `POST`. <br> - **URL**: `https://api.openai.com/v1/chat/completions`. <br> - **Headers**: `Authorization: Bearer <YOUR_OPENAI_KEY>`, `Content-Type: application/json`. <br> - **Body** (JSON): <br>```json\n{\n  "model": "gpt-3.5-turbo",\n  "messages": [{ "role": "user", "content": "{{$node[\"Build AI Review Prompt\"].json}}" }],\n  "temperature": 0.7\n}\n``` |
| **Prepare Final Email Report** | code | Định dạng HTML cho email: tiêu đề, danh sách doanh nghiệp, digest, link tới Google Maps. Có thể tùy chỉnh màu sắc, logo công ty. |
| **Send Final Email Report** | emailSend | - **To**: địa chỉ nhận (có thể dùng biến môi trường). <br> - **Subject**: `"📊 Báo cáo đánh giá địa phương tuần {{ $today }}"` <br> - **HTML**: kết quả từ node `Prepare Final Email Report`. <br> - **Credentials**: cấu hình SMTP (host, port, user, password). |

> **Lưu ý:** Đảm bảo **Credentials** (`httpHeaderAuth` cho MintAPI & OpenAI, `SMTP` cho email) đã được tạo trong n8n **Credentials** trước khi gán vào node.

#### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow bằng nút **Execute Workflow** (hoặc trigger thủ công) và kiểm tra log từng node.  
2. Nếu mọi thứ OK → **Bật** nút **Active** trên thanh công cụ.  
3. Kiểm tra hộp thư nhận để xác nhận email báo cáo đã tới.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm Slack/Telegram**: Dùng node `Slack` hoặc `Telegram` để gửi thông báo ngắn gọn đồng thời với email.  
- **Lưu log vào Google Sheets**: Thêm node `Google Sheets` để ghi lại số lượng review, rating trung bình mỗi tuần, giúp theo dõi xu hướng.  
- **Báo cáo định kỳ**: Kết hợp node `Schedule Trigger` để gửi báo cáo tổng hợp tháng một lần.  
- **Tùy chỉnh Prompt**: Thêm yêu cầu “phân tích cảm xúc” hoặc “đề xuất chiến lược nội dung” để nhận insight sâu hơn.  

### 📌 Kết luận
Với **10 node duy nhất**, workflow này biến công việc “thu thập & tóm tắt review” thành một quy trình **tự động, nhanh chóng và chính xác**. Các sếp chỉ cần thiết lập một lần, sau đó mỗi tuần sẽ nhận được bản tin thông minh, giúp đưa ra quyết định marketing nhanh hơn và hiệu quả hơn.  

**Áp dụng ngay** để không bỏ lỡ bất kỳ phản hồi quan trọng nào từ khách hàng trên Google Maps! 🚀