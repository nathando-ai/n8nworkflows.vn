---
title: "🚀 Tự động lấy từ khóa gợi ý trên Xiaohongshu (RedNote) với JustOneAPI trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động nghiên cứu thị trường, khai thác từ khóa gợi ý cực chuẩn từ mạng xã hội Xiaohongshu (RedNote) qua JustOneAPI chỉ với 1 cú click."
slug: "tu-dong-lay-tu-khoa-goi-y-xiaohongshu-justoneapi-n8n"
tags: [n8n, automation, xiaohongshu, rednote, market-research, justoneapi, no-code]
keywords: [n8n workflow, xiaohongshu keyword suggestions, justoneapi, tự động hóa nghiên cứu thị trường, rednote automation]
---

# 🚀 Tự động lấy từ khóa gợi ý trên Xiaohongshu (RedNote) với JustOneAPI

Các sếp làm marketing, nghiên cứu thị trường hay xây dựng nội dung đa nền tảng chắc hẳn đều biết Xiaohongshu (RedNote) là mỏ vàng để bắt trend giới trẻ. Tuy nhiên, việc tìm kiếm và tổng hợp từ khóa thủ công trên nền tảng này vừa mất thời gian lại khó phân tích diện rộng. 

Giải pháp là đây! Workflow n8n này sẽ giúp các sếp tự động hóa 100% quá trình khai thác các từ khóa gợi ý (keyword suggestions) liên quan trên Xiaohongshu thông qua **JustOneAPI**. Không cần code phức tạp, chỉ cần vài thao tác cấu hình là các sếp đã có ngay danh sách từ khóa tối ưu cho chiến dịch nội dung của mình.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Thay vì tìm kiếm thủ công từng từ khóa, hệ thống trả về danh sách đầy đủ chỉ trong tích tắc.
- **Dữ liệu cấu trúc sạch sẽ:** Node code tùy chỉnh tự động làm sạch và gom nhóm dữ liệu thô thành danh sách gọn gàng, sẵn sàng sử dụng.
- **Bắt trend nhanh chóng:** Dễ dàng nắm bắt xu hướng tìm kiếm của người dùng trên Xiaohongshu để tối ưu SEO nội dung, lên kịch bản video TikTok/Reels/Xiaohongshu.
- **Linh hoạt mở rộng:** Dễ dàng kết nối tiếp với Google Sheets, Notion hoặc gửi thẳng về Telegram/Slack cho team Content.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động.
- Tài khoản và API Key tại **JustOneAPI** để gọi dữ liệu từ Xiaohongshu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần tải file JSON của workflow này từ kho lưu trữ n8n, sau đó chọn **Import from File** hoặc copy trực tiếp mã JSON và dán vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình chính xác các node sau để workflow có thể chạy mượt mà:

- **Node `Set API and Keyword Parameters` (Set):**
  - Cấu hình các tham số đầu vào bao gồm: Từ khóa gốc (keyword) mà các sếp muốn nghiên cứu và thông tin xác thực API.
  - Điền chính xác API Key hoặc các header yêu cầu từ JustOneAPI.

- **Node `Fetch Xiaohongshu Suggestions` (HTTP Request):**
  - Kiểm tra lại Method (thường là GET) và URL Endpoint cung cấp bởi JustOneAPI.
  - Đảm bảo truyền đúng query parameters được định nghĩa ở node Set phía trên.

- **Node `Build Suggestions List` (Code):**
  - Đây là nơi xử lý dữ liệu thô (`Raw Suggestions Data`) thành danh sách hoàn chỉnh. Các sếp có thể xem qua đoạn code JavaScript có sẵn để tùy chỉnh cách lọc hoặc định dạng lại cấu trúc đầu ra theo ý muốn.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** thủ công tại node `Manual Workflow Trigger` để test thử với một từ khóa mẫu xem dữ liệu trả về có chuẩn chỉnh hay không.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để sẵn sàng sử dụng bất cứ lúc nào.

---

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa workflow này cho công việc thực tế, các sếp có thể nâng cấp thêm:
1. **Lưu trữ tự động:** Nối thêm node *Google Sheets* hoặc *Notion* vào sau node `Output Final Suggestions` để lưu toàn bộ danh sách từ khóa phục vụ việc theo dõi dài hạn.
2. **Tích hợp Chatbot:** Gửi kết quả trực tiếp về nhóm Telegram hoặc Slack của team Content ngay khi chạy xong.
3. **Biến thành Webhook:** Thay thế node `Manual Workflow Trigger` bằng `Webhook` hoặc `Chat Trigger` để có thể tra cứu từ khóa trực tiếp qua giao diện chat nội bộ.

### 📌 Kết luận
Việc nghiên cứu thị trường và từ khóa trên các nền tảng mạng xã hội ngoại (như Xiaohongshu) nay đã trở nên cực kỳ đơn giản nhờ sự kết hợp giữa n8n và JustOneAPI. Hãy import ngay workflow này về hệ thống của các sếp để tối ưu hóa năng suất làm content ngay hôm nay!