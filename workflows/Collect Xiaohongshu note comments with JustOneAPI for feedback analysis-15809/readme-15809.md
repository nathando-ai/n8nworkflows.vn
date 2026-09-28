---
title: "🚀 Thu thập bình luận Xiaohongshu bằng JustOneAPI cho phân tích phản hồi"
description: "Tự động lấy bình luận từ bài viết Xiaohongshu qua JustOneAPI, chuẩn bị dữ liệu phân tích phản hồi nhanh chóng và chính xác."
slug: "thu-thap-binh-luan-xiaohongshu-justoneapi"
tags: [n8n, automation, no-code, market-research, api-integration, data-analysis]
keywords: [n8n workflow, tự động lấy bình luận, JustOneAPI, Xiaohongshu, phân tích phản hồi]
---

# 🚀 Thu thập bình luận Xiaohongshu bằng JustOneAPI cho phân tích phản hồi

Khi các sếp muốn hiểu sâu hơn về cảm nhận của người dùng trên Xiaohongshu, việc **copy‑paste thủ công** từng bình luận vào bảng tính không chỉ tốn thời gian mà còn dễ gây sai sót. Thêm vào đó, mỗi lần cần lấy bình luận mới lại phải lặp lại quy trình, khiến việc phân tích phản hồi trở nên chậm chạp và không đồng nhất.

**Workflow này** sẽ tự động:
1. Gửi yêu cầu tới JustOneAPI để lấy toàn bộ bình luận của một note trên Xiaohongshu.  
2. Xử lý dữ liệu thô, chuyển thành danh sách bình luận có cấu trúc.  
3. Xuất ra kết quả sẵn sàng cho các công cụ phân tích (Google Sheets, PowerBI, AI sentiment…).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Lấy hàng trăm bình luận trong vài giây, không còn thao tác copy‑paste.  
- **Độ chính xác cao**: Dữ liệu được lấy nguyên bản từ API, không bị mất ký tự hay format.  
- **Dễ dàng tích hợp**: Kết quả xuất ra JSON, có thể đẩy ngay vào Google Sheets, DB, hoặc công cụ AI.  
- **Hoạt động liên tục**: Khi kết hợp với trigger cron, workflow tự động cập nhật bình luận mới mỗi ngày.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **JustOneAPI Key**: Đăng ký và lấy API Key tại https://justoneapi.com.  
- **Xiaohongshu Note ID**: ID của note (bài viết) mà các sếp muốn thu thập bình luận.  
- **n8n**: Đã cài đặt và truy cập được editor.  
- **Kết nối internet ổn định** để gọi API.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow (từ trang gốc hoặc file đính kèm).  
2. Vào **n8n → Workflows → Import**, chọn file JSON và nhấn **Import**.  
3. Hoặc mở **n8n Editor**, nhấn **+** → **Import from Clipboard**, dán toàn bộ JSON và **Save**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Loại | Hướng dẫn cấu hình |
|------|------|-------------------|
| **Start Workflow** | `manualTrigger` | Không cần thay đổi, chỉ dùng để khởi chạy thủ công hoặc gắn cron later. |
| **Set API and Comment Parameters** | `set` | - **apiKey**: Điền JustOneAPI Key.<br>- **noteId**: Nhập ID của note Xiaohongshu.<br>- **limit** (tùy chọn): Số bình luận muốn lấy mỗi lần (mặc định 100). |
| **Fetch Xiaohongshu Comments via API** | `httpRequest` | - **Method**: `GET`.<br>- **URL**: `https://api.justoneapi.com/xiaohongshu/comments` (hoặc URL tùy chỉnh).<br>- **Query Parameters**: `note_id={{$json["noteId"]}}&limit={{$json["limit"]}}&api_key={{$json["apiKey"]}}`.<br>- **Authentication**: Không cần nếu đã truyền `api_key` trong query. |
| **Output Raw API Response** | `set` | Để debug, không cần thay đổi. Bạn có thể bật **Execute Node** để xem dữ liệu thô trả về từ API. |
| **Parse and Build Comment List** | `code` (JavaScript) | Script mặc định sẽ: <br>```js\nconst comments = items[0].json.data.map(c => ({ author: c.author, content: c.content, likes: c.like_count, createdAt: c.created_at }));\nreturn [{ json: { comments } }];\n```<br>Kiểm tra xem trường `data` có đúng với cấu trúc API trả về không; nếu khác, chỉnh sửa tên trường tương ứng. |
| **Output Final Comment Data** | `set` | Đưa ra kết quả cuối cùng dưới dạng `{ comments: [...] }`. Bạn có thể thêm **Google Sheets**, **Slack**, hoặc **Email** node phía sau để lưu/đẩy dữ liệu. |

> **Lưu ý:** Sau khi cấu hình xong, nhấn **Execute Workflow** để kiểm tra từng node. Nếu API trả về lỗi 401, kiểm tra lại `apiKey`. Nếu không có dữ liệu, xác nhận `noteId` có tồn tại và note công khai.

#### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow một lần với dữ liệu mẫu, kiểm tra `Output Final Comment Data` có danh sách bình luận hợp lệ.  
2. **Bật Active**: Khi mọi thứ ổn, bật **Active** ở góc phải màn hình.  
3. (Tùy chọn) **Lên lịch**: Thêm node **Cron** trước `Start Workflow` để tự động chạy hàng ngày/giờ.

### ✍️ Mẹo & gợi ý nâng cao
- **Gửi báo cáo định kỳ**: Thêm node **Email** hoặc **Telegram** để gửi danh sách bình luận mới mỗi sáng.  
- **Lưu vào Google Sheets**: Kết nối node **Google Sheets** → `Append` để xây dựng cơ sở dữ liệu bình luận theo thời gian.  
- **Phân tích cảm xúc**: Sau node `Parse and Build Comment List`, chèn node **LLM (OpenAI, Claude…)** để thực hiện sentiment analysis và gắn nhãn `positive/negative`.  
- **Lưu log**: Dùng node **Write Binary File** hoặc **MongoDB** để lưu toàn bộ phản hồi API cho mục đích audit.  
- **Mở rộng nguồn**: Thay đổi URL trong node `httpRequest` để lấy bình luận từ các nền tảng khác (TikTok, Instagram) nếu JustOneAPI hỗ trợ.

### 📌 Kết luận
Với workflow này, các sếp có thể **tự động thu thập và chuẩn bị dữ liệu bình luận** từ Xiaohongshu chỉ trong vài giây, giảm thiểu công sức thủ công và tăng độ tin cậy cho các phân tích thị trường. Hãy triển khai ngay, kết hợp với các công cụ báo cáo hoặc AI để biến dữ liệu thành insight giá trị! 🚀