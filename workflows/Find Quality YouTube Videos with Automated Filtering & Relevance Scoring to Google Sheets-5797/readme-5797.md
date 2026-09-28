---
title: "🚀 Tự động tìm kiếm và chấm điểm video YouTube chất lượng cao với n8n"
description: "Hướng dẫn xây dựng workflow n8n giúp tự động tìm kiếm, lọc chất lượng, chấm điểm mức độ liên quan của video YouTube và lưu kết quả vào Google Sheets."
slug: "tu-dong-tim-kiem-video-youtube-chat-luong-cao-n8n"
tags: [n8n, automation, youtube-api, google-sheets, market-research, ai-workflow]
keywords: [n8n workflow, tự động hóa youtube, lọc video youtube, google sheets automation, nghiên cứu thị trường youtube]
---

# 🚀 Tự động tìm kiếm và chấm điểm video YouTube chất lượng cao với n8n

Việc nghiên cứu thị trường, tìm kiếm các video giáo dục chất lượng trên YouTube để phân tích xu hướng hoặc thu thập nội dung thường ngốn rất nhiều thời gian của các sếp. Việc phải cào tay, lọc từng video rác, video quảng cáo rồi copy vào Excel thực sự là một "cực hình".

Đừng lo, workflow n8n được thiết kế bởi **Zach @BrightWayAI** sẽ giải quyết triệt để bài toán này. Workflow sẽ tự động hóa từ A-Z: tìm kiếm từ khóa, lấy metadata chi tiết (lượt xem, lượt thích, ngày đăng), lọc bỏ video rác/quảng cáo, chấm điểm mức độ liên quan, loại bỏ trùng lặp và tự động đẩy top video xuất sắc nhất thẳng vào Google Sheets cho các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần thủ công tìm kiếm và lọc hàng trăm video trên YouTube nữa.
- **Dữ liệu sạch, chất lượng cao:** Tự động loại bỏ các video rác, nội dung quảng cáo/lừa đảo nhờ hệ thống bộ lọc thông minh.
- **Chấm điểm thông minh:** Tự động tính toán điểm số liên quan (Relevance Score) để chọn ra những video đáng xem nhất.
- **Đồng bộ tập trung:** Toàn bộ danh sách tinh gọn được cập nhật tự động vào Google Sheets để team dễ dàng khai thác.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** (Self-hosted hoặc n8n Cloud).
- **YouTube Data API v3 Credentials:** Để gọi API tìm kiếm và lấy thông tin video.
- **Google Sheets Credentials:** Để workflow có quyền ghi dữ liệu vào file Google Sheet của các sếp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và paste trực tiếp vào n8n Editor của mình, hoặc tải file JSON về và chọn **Import from File**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 16 nodes hoạt động nhịp nhàng, các sếp cần chú ý cấu hình các điểm sau:

- **Node `Set Query`**: Nơi các sếp định nghĩa từ khóa muốn tìm kiếm trên YouTube. Có thể thay đổi từ khóa bất cứ lúc nào tùy theo chiến dịch nghiên cứu thị trường.
- **Node `Search YouTube` & `Get Video Metadata`**: 
  - Cần bật **YouTube Data API v3** trong Google Cloud Console.
  - Tạo Credentials loại OAuth2 cho YouTube và kết nối vào hai node này.
- **Node `Filter for Quality` & `Filter for Relevance`**: Các sếp có thể tùy chỉnh lại điều kiện lọc (dựa trên view, like, độ dài, hoặc từ khóa) trong các node này để phù hợp hơn với nhu cầu thực tế của doanh nghiệp.
- **Node `Send to Google Sheets`**:
  - Chuẩn bị trước một Google Sheet với các cột: `Title`, `Channel`, `Published At`, `Views`, `Likes`, `Description`, `URL`.
  - Kết nối tài khoản Google Sheets thông qua OAuth2 trong n8n và chọn đúng file Google Sheet vừa tạo.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để chạy thử nghiệm (Manual Trigger) và kiểm tra dữ liệu đầu ra ở Google Sheets.
- Sau khi kiểm tra mọi thứ mượt mà, gạt công tắc sang **Active** để hoàn tất quá trình tự động hóa.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm một node Telegram hoặc Slack ở cuối workflow để bắn thông báo ngay về máy cho team mỗi khi có bộ video chất lượng mới được cập nhật vào Google Sheets.
- **Tự động hóa định kỳ:** Thay thế node `When clicking ‘Execute workflow’` bằng node **Schedule Trigger** để workflow tự động chạy mỗi tuần/tháng một lần phục vụ nghiên cứu xu hướng.
- **Tùy chỉnh điểm số:** Tinh chỉnh công thức trong node `Generate Relevance Score` để ưu tiên các tiêu chí riêng của sếp (ví dụ: ưu tiên kênh có nhiều tương tác hơn hoặc video mới đăng tải).

### 📌 Kết luận
Với workflow này, việc thu thập và nghiên cứu nội dung video trên YouTube trở nên tự động hóa hoàn toàn, giúp các sếp giải phóng thời gian để tập trung vào việc phân tích chiến lược thay vì làm tay chân. Chúc các sếp cài đặt thành công!