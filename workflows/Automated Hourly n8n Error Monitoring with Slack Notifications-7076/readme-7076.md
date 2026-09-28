---
title: "🚀 Giám Sát Lỗi n8n Tự Động & Báo Cáo Slack Mỗi Giờ"
description: "Workflow n8n tự động quét các lỗi thực thi trong 60 phút qua và gửi báo cáo chi tiết lên Slack, giúp DevOps và đội phát triển phản ứng nhanh với sự cố."
slug: "giam-sat-loi-n8n-bao-cao-slack"
tags: [n8n, automation, devops, slack, monitoring, no-code]
keywords: [n8n workflow, giám sát lỗi, tự động hóa devops, báo cáo slack, n8n error monitoring]
---

# 🚀 Giám Sát Lỗi n8n Tự Động & Báo Cáo Slack Mỗi Giờ

Trong môi trường vận hành hệ thống tự động hóa bằng n8n, việc một workflow bị lỗi (failed execution) mà không ai hay biết là một rủi ro cực kỳ lớn. Các sếp có thể mất hàng giờ để debug khi sự cố đã ảnh hưởng đến dữ liệu hoặc quy trình kinh doanh. Làm thủ công việc kiểm tra từng workflow xem có lỗi không là điều bất khả thi khi số lượng workflow tăng lên.

Workflow này giải quyết triệt để nỗi đau đó bằng cách tự động quét toàn bộ các execution đã lỗi trong **60 phút gần nhất**, tổng hợp chúng thành một bảng báo cáo gọn gàng và đẩy thẳng lên kênh Slack của team. Không cần code phức tạp, không cần cài đặt thêm các tool monitoring đắt tiền, các sếp chỉ cần một workflow duy nhất để "canh chừng" hệ thống 24/7.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow giám sát này chạy ổn định 24/7 và không bị gián đoạn khi server n8n của bạn gặp sự cố (vì nó cần gọi API của chính n8n), các sếp nên cài n8n trên VPS riêng (Self-hosted) với cấu hình ổn định.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phát hiện sự cố tức thì:** Nhận thông báo lỗi trên Slack chỉ sau 1 giờ kể từ khi lỗi xảy ra, thay vì chờ đến khi khách hàng báo cáo.
- **Báo cáo trực quan:** Dạng bảng hiển thị rõ ID, Tên Workflow và Số lượng lỗi, giúp định vị vấn đề nhanh chóng.
- **Tiết kiệm thời gian vận hành:** Loại bỏ hoàn toàn thao tác kiểm tra thủ công trên giao diện n8n.
- **Tích hợp DevOps chuẩn mực:** Biến n8n thành một hệ thống tự giám sát (self-monitoring) chuyên nghiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n:** Đang chạy và có ít nhất 1 workflow khác để test.
2. **API Key n8n:** Tạo một API Key mới trong phần *Settings > API* của n8n. Workflow này cần quyền truy cập để đọc danh sách workflows và lịch sử execution.
3. **Tài khoản Slack:**
   - Tạo một Slack App hoặc sử dụng Bot Token hiện có.
   - Đảm bảo Bot có quyền gửi tin nhắn vào kênh (Channel) mà các sếp muốn nhận báo cáo.
   - Tạo Credentials `slackOAuth2Api` trong n8n.
4. **Credentials n8n API:** Tạo Credentials `n8nApi` trong n8n và dán API Key vào.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from File** hoặc **Import from URL**.
3. Dán link gốc: `https://n8n.io/workflows/7076` hoặc tải file JSON về và import.
4. Workflow với 9 nodes sẽ xuất hiện trên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Đây là phần quan trọng nhất. Các sếp cần cấu hình kỹ các node sau:

*   **Node `Config` (Set Node):**
    *   Đây là node chứa các tham số cấu hình chung.
    *   Kiểm tra tham số `channel`: Thay giá trị mặc định bằng tên kênh Slack của các sếp (ví dụ: `#devops-alerts` hoặc `#n8n-errors`).
    *   Kiểm tra tham số `minutes`: Mặc định là 60. Các sếp có thể chỉnh thành 30 hoặc 120 tùy theo tần suất quét mong muốn.

*   **Node `GetWorkflows` (n8n Node):**
    *   Chọn Credentials `n8nApi` đã tạo ở bước chuẩn bị.
    *   Đảm bảo resource là `workflow` và operation là `getAll`.

*   **Node `n8n` (Execution Resource):**
    *   Node này nằm trong vòng lặp `Loop`. Nó dùng để lấy lịch sử execution của từng workflow.
    *   Chọn cùng Credentials `n8nApi`.
    *   Resource: `execution`.
    *   Operation: `getAll`.
    *   *Lưu ý:* Các sếp cần đảm bảo filter trong node này khớp với logic lấy execution bị lỗi (failed).

*   **Node `Slack` (Slack Node):**
    *   Chọn Credentials `slackOAuth2Api`.
    *   Resource: `Message`.
    *   Operation: `Send`.
    *   Channel: Tham chiếu đến giá trị từ node `Config` (ví dụ: `={{ $json.channel }}`).
    *   Text: Tham chiếu đến nội dung báo cáo đã được tạo ở node `MakeMessage`.

*   **Node `MakeMessage` & `FilterLastHour` (Code Nodes):**
    *   Đây là các node JavaScript xử lý logic.
    *   `FilterLastHour`: Lọc các execution chỉ trong khoảng thời gian quy định (mặc định 60 phút).
    *   `MakeMessage`: Định dạng dữ liệu lỗi thành chuỗi text Markdown/Slack Block Kit để hiển thị đẹp mắt trên Slack.
    *   *Không cần sửa code* nếu các sếp giữ nguyên cấu trúc dữ liệu mặc định của n8n.

#### 3. Kích hoạt ⚡️
1. **Test Run:**
   *   Chạy workflow thủ công (Execute Workflow).
   *   Nếu không có lỗi nào trong 1 giờ qua, workflow sẽ chạy xong mà không gửi tin nhắn (hoặc gửi thông báo "Không có lỗi", tùy logic code).
   *   *Mẹo test:* Các sếp có thể cố tình tạo một lỗi nhỏ trong một workflow khác (ví dụ: để trống một trường bắt buộc) và chờ đến chu kỳ quét tiếp theo, hoặc chỉnh `minutes` trong node `Config` xuống 1 phút và chạy lại ngay sau khi gây lỗi.
2. **Bật Active:**
   *   Sau khi xác nhận tin nhắn Slack hiển thị đúng, bật công tắc **Active** ở góc trên bên phải.
   *   Workflow sẽ tự động chạy theo lịch `Schedule Trigger` (mỗi 1 giờ).

### ✍️ Mẹo & gợi ý nâng cao
- **Tùy biến nội dung báo cáo:** Sửa code trong node `MakeMessage` để thêm thông tin như: Thời gian lỗi cụ thể, ID execution, hoặc trích dẫn ngắn thông báo lỗi (error message) để debug nhanh hơn.
- **Gửi báo cáo định kỳ hàng ngày:** Thêm một nhánh khác hoặc một workflow riêng để tổng hợp số lượng lỗi trong 24h qua và gửi email báo cáo cuối ngày cho quản lý.
- **Tích hợp Telegram:** Thay thế hoặc bổ sung node `Slack` bằng node `Telegram` nếu team các sếp dùng Telegram nhiều hơn.
- **Cảnh báo theo mức độ nghiêm trọng:** Mở rộng logic trong `MakeMessage` để đổi màu hoặc thêm icon ⚠️/🔥 nếu số lượng lỗi vượt quá ngưỡng nhất định (ví dụ: > 5 lỗi/giờ).

### 📌 Kết luận
Việc giám sát hệ thống tự động hóa không nên là một gánh nặng thủ công. Với workflow **Automated Hourly n8n Error Monitoring**, các sếp đã có trong tay một "người gác cổng" trung thành, hoạt động 24/7, giúp đảm bảo mọi quy trình kinh doanh đều chạy trơn tru. Hãy import và cấu hình ngay hôm nay để ngủ ngon hơn vì biết rằng hệ thống của mình luôn được theo dõi!