---
title: "🚀 Tự Động Kiểm Tra Tuân Thủ Pre-Release Jira, Monday.com và Slack với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động giám sát tiến độ Jira, kiểm tra tiêu chí hoàn thành (DoD), đồng bộ lỗi lên Monday.com và bắn cảnh báo Slack."
slug: "tu-dong-kiem-tra-tuan-thu-pre-release-jira-monday-slack"
tags: [n8n, automation, jira, monday-com, slack, devops]
keywords: [n8n workflow, tự động hóa jira, monday.com n8n, slack alert automation, pre-release compliance]
---

# 🚀 Tự Động Kiểm Tra Tuân Thủ Pre-Release Jira, Monday.com và Slack với n8n

Các sếp làm trong ngành phát triển phần mềm chắc chắn đã từng đau đầu với tình trạng "giao hẹn release nhưng thiếu task", lỗi Definition of Done (DoD) chưa hoàn thiện mà vẫn cố đưa lên production, dẫn đến bug ngập tràn. Việc kiểm tra thủ công từng ticket Jira tốn rất nhiều thời gian và dễ bỏ sót lỗi con người.

Workflow n8n này do chuyên gia **Rahul Joshi** thiết kế sẽ giải quyết triệt để nỗi đau đó. Nó tự động hóa 100% quy trình kiểm tra trạng thái pre-release, phân loại các task chưa đạt chuẩn, ghi nhận vào Monday.com để theo dõi dạng centralize và gửi thông báo trực tiếp về kênh Slack của team. Không cần code phức tạp, chỉ vài cú click là hệ thống tự chạy 24/7!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Kiểm soát tuyệt đối chất lượng Release:** Đảm bảo 100% các issue đưa lên production đều đã hoàn tất tiêu chí Definition of Done (DoD).
- **Tự động hóa đa nền tảng:** Đồng bộ mượt mà dữ liệu giữa Jira Software, Monday.com và Slack mà không cần thao tác thủ công.
- **Minh bạch tiến độ blocker:** Tự động tạo item trên Monday.com cho các issue chưa tuân thủ giúp Product Owner / Project Manager dễ dàng tracking.
- **Cảnh báo tức thì:** Bắn notification real-time về kênh Slack của team để kịp thời xử lý trước giờ G.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API credentials sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Jira Cloud Account** với quyền cấu hình Webhooks và API Token (`jiraSoftwareCloudApi`).
- **Monday.com Account** cùng API Key để tạo Board tracking (`mondayComApi`).
- **Slack Workspace** với quyền Bot Token để gửi tin nhắn (`slackOAuth2Api`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này, vào giao diện n8n Editor chọn **Add workflow** -> Nhấn tổ hợp `Ctrl + V` (hoặc `Cmd + V`) để paste toàn bộ các node vào canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 7 nodes chính được liên kết chặt chẽ. Các sếp cần cấu hình kỹ các điểm sau:

- **Jira Webhook - Detect Issue Changes (`jiraTrigger`)**: 
  - Chọn credential `jiraSoftwareCloudApi`.
  - Cấu hình sự kiện lắng nghe: *Issue Updated* hoặc *Issue Link Created* để kích hoạt workflow tự động mỗi khi có thay đổi trên Jira.
- **Fetch Full Issue Details (`jira`)**:
  - Node này dùng để lấy thông tin chi tiết đầy đủ (vì Webhook chỉ gửi dữ liệu cơ bản). Đảm bảo chọn đúng operation `get` và truyền Issue ID từ trigger sang.
- **Process Issues One by One (`splitInBatches`)**:
  - Giúp xử lý từng issue một, tránh quá tải và dễ dàng kiểm soát lỗi cho từng task độc lập.
- **Is Definition of Done Complete? (`if`)**:
  - Thiết lập điều kiện check trường custom field DoD (`customfield_DoD == true`). 
  - Nếu **TRUE**: Chuyển sang nhánh sẵn sàng release.
  - Nếu **FALSE**: Chuyển sang nhánh xử lý issue chưa đạt chuẩn.
- **Flag Issue as Non-Compliant (`set`)**:
  - Gán nhãn cho issue với các thông tin: Issue Key, Reason ("Definition of Done not met"), Status ("Non-Compliant").
- **Track in Monday.com Board (`mondayCom`)**:
  - Chọn credential `mondayComApi`.
  - Chọn Resource là `boardItem`. Trỏ tới Board "Release Issues" và Group "Topics" đã chuẩn bị sẵn trên Monday.com để tự động tạo item tracking các blocker.
- **Send Slack Alert to Team (`slack`)**:
  - Chọn credential `slackOAuth2Api`.
  - Cấu hình kênh nhận thông báo (ví dụ: `#release-updates`) để gửi tổng hợp tên version, số lượng issue đạt/chưa đạt chuẩn kèm link Monday.com.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử với một vài issue mẫu để kiểm tra log dữ liệu qua lại giữa các node.
- Sau khi test ngon lành, gạt công tắc sang **Active** để hệ thống tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Có thể kết hợp thêm node Telegram hoặc Microsoft Teams nếu team công ty không dùng Slack.
- **Lưu log vào Google Sheets:** Thêm một node Google Sheets ở cuối chuỗi để lưu lại lịch sử các lần kiểm tra pre-release phục vụ việc audit hàng tháng.
- **Tự động gán nhãn trên Jira:** Bổ sung thêm một node cập nhật Jira để tự động thêm nhãn `needs-review` vào các task non-compliant giúp lập trình viên dễ nhận biết.

### 📌 Kết luận
Tự động hóa quy trình kiểm tra pre-release với n8n, Jira, Monday.com và Slack là bước tiến lớn giúp tối ưu hóa vận hành cho team kỹ thuật, giảm thiểu rủi ro khi deploy sản phẩm lên production. Chúc các sếp áp dụng thành công và xây dựng được hệ thống automation mượt mà!