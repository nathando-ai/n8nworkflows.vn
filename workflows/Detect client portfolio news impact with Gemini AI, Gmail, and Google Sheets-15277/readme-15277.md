---
title: "🚀 Tự động phát hiện tác động tin tức tài chính đến danh mục khách hàng với Gemini AI và n8n"
description: "Hướng dẫn cấu hình workflow n8n tự động quét tin tức tài chính mỗi ngày, dùng Gemini AI phân tích tác động và gửi cảnh báo qua Gmail cho khách hàng."
slug: "tu-dong-phat-hien-tac-dong-tin-tuc-tai-chinh-gemini-ai-n8n"
tags: [n8n, automation, no-code, ai, gemini, google-sheets, gmail]
keywords: [n8n workflow, tu dong hoa tin tuc, gemini ai, phan tich tin tuc tai chinh, google sheets automation]
---

# 🚀 Tự động phát hiện tác động tin tức tài chính với Gemini AI, Gmail và Google Sheets

Các sếp làm trong lĩnh vực tài chính, đầu tư hay quản lý danh mục khách hàng chắc chắn hiểu rõ cảm giác "ngợp thở" khi mỗi ngày có hàng trăm bản tin kinh tế, tài chính được phát hành. Việc phải ngồi đọc, đối chiếu xem tin tức nào ảnh hưởng đến danh mục đầu tư hay khách hàng nào của mình vừa tốn hàng giờ đồng hồ, lại rất dễ bỏ sót các tin tức quan trọng (High Impact).

Giải pháp ư? Để công nghệ lo! Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ mạnh mẽ giúp tự động hóa toàn bộ quy trình: Tự động quét tin tức mỗi sáng, lọc bỏ tin trùng lặp, dùng **Gemini AI** phân tích mức độ ảnh hưởng đến từng khách hàng, lưu log vào **Google Sheets** và tự động bắn cảnh báo qua **Gmail** nếu gặp tin "nóng".

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không sợ sập, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100% mỗi 8h sáng**: Không cần tốn nhân sự trực quét tin tức tài chính thủ công.
- **AI thông minh phân tích chuyên sâu**: Sử dụng Google Gemini AI để đánh giá chính xác mức độ tác động (High/Medium/Low) và chỉ định rõ khách hàng nào bị ảnh hưởng.
- **Chống trùng lặp thông minh**: Tự động chuẩn hóa URL và kiểm tra log lịch sử để không bao giờ xử lý lại một bài báo cũ.
- **Cảnh báo tức thời**: Gửi email qua Gmail ngay lập tức khi phát hiện tin tức có tác động mạnh đến danh mục.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **n8n Instance**: Đã cài đặt sẵn (Self-hosted hoặc Cloud).
- **Google Gemini API Key**: Để kết nối với node AI.
- **Google Sheets**: 
  - 1 Sheet chứa danh sách khách hàng (`Client Dataset`).
  - 1 Sheet dùng làm nhật ký xử lý bài viết (`Article Processing Log`).
- **Gmail Account**: Tài khoản Gmail đã cấp quyền OAuth2 để gửi email cảnh báo.
- **News API**: Key truy cập API lấy tin tức tài chính/kinh doanh (dùng trong node `Fetch Latest Finance News`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow từ nguồn cung cấp, sau đó vào giao diện n8n Editor chọn **Import from JSON** và dán vào là xong. Toàn bộ 21 nodes sẽ hiện ra gọn gàng trên màn hình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà không báo lỗi đỏ, các sếp nhớ cấu hình kỹ các điểm sau:

- **Daily News Trigger (8AM)**: Mặc định lịch chạy là 8 giờ sáng mỗi ngày. Các sếp có thể đổi lại múi giờ (Timezone) cho phù hợp với giờ Việt Nam (Asia/Ho_Chi_Minh).
- **Fetch Latest Finance News**: Cấu hình URL và API Key của nguồn cấp tin tức (News API) cùng danh mục tin tức (business/finance).
- **Fetch Client Dataset & Fetch Already Processed Articles**: Kết nối tài khoản `Google Sheets OAuth2` và trỏ đúng đường dẫn tới File Google Sheets quản lý khách hàng và bảng log.
- **AI Impact Classification**: Chọn credentials `Google Palm/Gemini API`, cấu hình prompt để AI trả về định dạng JSON chuẩn gồm các trường: mức độ ảnh hưởng (impact level) và khách hàng bị tác động.
- **Filter High Impact News**: Thiết lập điều kiện (`IF`) chỉ cho phép các tin tức có mức độ tác động cao (`High`) đi tiếp nhánh gửi email.
- **Send High Impact Alert Email**: Cấu hình tài khoản `Gmail OAuth2` để hệ thống tự động gửi email cho người quản lý hoặc khách hàng.
- **Wait Before Next Article**: Node này mặc định đặt độ trễ 1 phút giữa các bài báo để tránh vượt quá giới hạn rate-limit của Gemini API.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để chạy thử với dữ liệu mẫu xem hệ thống có nuốt trọn luồng dữ liệu hay không.
- Nếu mọi thứ xanh mướt (success), các sếp bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm hàng ngày.

### ✍️ Mẹo & gợi ý nâng cao
Để workflow "xịn xò" hơn nữa, các sếp có thể mở rộng thêm một vài ý tưởng sau:
- **Tích hợp Telegram/Slack**: Thay vì chỉ nhận email, hãy bắn một thông báo nhanh vào nhóm Telegram nội bộ công ty để team kịp thời nắm bắt tin "nóng".
- **Lưu log chi tiết**: Tùy biến bảng Google Sheets Log để phân loại rõ ràng màu sắc cho từng mức độ High/Medium/Low giúp dễ quan sát trực quan.
- **Mở rộng nguồn tin**: Kết hợp thêm nhiều nguồn RSS Feed hoặc Twitter/X API để quét tin tức đa kênh thay vì chỉ 1 nguồn API.

### 📌 Kết luận
Việc tự động hóa quy trình phân tích tin tức tài chính bằng n8n và Gemini AI không chỉ giúp các sếp tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần mà còn đảm bảo không bỏ lỡ bất kỳ cơ hội hay rủi ro nào từ thị trường. Triển khai ngay hôm nay để tối ưu hóa năng suất vận hành doanh nghiệp nào!