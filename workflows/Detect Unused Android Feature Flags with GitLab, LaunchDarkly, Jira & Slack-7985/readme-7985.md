---
title: "🚀 Tự động phát hiện Feature Flag thừa trên Android với GitLab, LaunchDarkly, Jira & Slack"
description: "Giải pháp n8n workflow tự động quét mã nguồn Android hàng tuần, tìm các feature flag không còn sử dụng so với LaunchDarkly, đồng thời tự động ghi log Sheets, tạo Jira ticket và thông báo Slack."
slug: "tu-dong-phat-hien-android-feature-flags-thua-gitlab-launchdarkly-jira-slack"
tags: [n8n, automation, devops, gitlab, launchdarkly, jira, slack]
keywords: [n8n workflow, tu dong hoa devops, android feature flags, cleanup feature flags, launchdarkly gitlab integration]
---

# 🚀 Tự động phát hiện Feature Flag thừa trên Android với GitLab, LaunchDarkly, Jira & Slack

Trong quá trình phát triển ứng dụng Android (Kotlin/Java), đội ngũ lập trình thường xuyên sử dụng Feature Flag (LaunchDarkly) để bật/tắt tính năng. Tuy nhiên, sau khi tính năng đã hoàn thiện và phát hành ổn định, các đoạn code cũ và flag thừa (dead flags) thường bị bỏ quên, gây ra "nợ kỹ thuật" (technical debt) nặng nề cho mã nguồn.

Việc rà soát thủ công hàng trăm flag là cơn ác mộng đối với các kỹ sư. Workflow n8n này sẽ thay thế hoàn toàn công việc thủ công đó bằng hệ thống tự động 100%, giúp quét mã nguồn Android, đối chiếu với LaunchDarkly, lưu báo cáo vào Google Sheets, tự động tạo Jira ticket và bắn thông báo cảnh báo trực tiếp lên Slack.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Dọn sạch nợ kỹ thuật:** Tự động phát hiện các feature flag không còn được sử dụng trong codebase Android Kotlin/Java.
- **Tiết kiệm hàng giờ rà soát:** Thay vì kiểm tra thủ công mỗi tuần/tháng, hệ thống tự động chạy theo lịch định sẵn.
- **Đồng bộ đa nền tảng mượt mà:** Tự động ghi log vào Google Sheets để lưu trữ, mở Jira ticket cho team Dev xử lý và thông báo cảnh báo tức thì qua Slack.
- **Chủ động 24/7:** Hoạt động hoàn toàn tự động, đảm bảo mã nguồn Android luôn sạch sẽ, gọn gàng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow chạy trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và thông tin sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **GitLab Account & Credentials** (OAuth2 API) để quét mã nguồn repository Android.
- **LaunchDarkly API Key** (thông qua node HTTP Request) để lấy danh sách tất cả các flags và trạng thái của chúng.
- **Google Sheets Credentials** (OAuth2 API) để lưu báo cáo danh sách cờ "chết".
- **Jira Software Account** để tự động tạo task xóa code/flag thừa.
- **Slack Workspace** để gửi cảnh báo đến channel kỹ thuật.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp đoạn mã JSON từ trang chủ n8n.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File / Clipboard** và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node trọng điểm sau:
- **Schedule Trigger**: Thiết lập lịch chạy định kỳ (Ví dụ: Chạy mỗi tuần một lần vào sáng Thứ Hai).
- **GitLab**: Kết nối tài khoản GitLab qua `gitlabOAuth2Api`, sau đó trỏ tới Project Repository chứa mã nguồn ứng dụng Android Kotlin/Java cần quét.
- **HTTP Request (LaunchDarkly)**: Điền Endpoint API của LaunchDarkly kèm theo các Header xác thực (API Token) để lấy toàn bộ danh sách Feature Flags hiện tại.
- **Find dead flags & Detect flags (Code nodes)**: Các đoạn mã JavaScript/Python có sẵn sẽ tiến hành so sánh logic giữa danh sách flag tìm thấy trong mã nguồn GitLab và trạng thái thực tế từ LaunchDarkly để lọc ra các "dead flags".
- **Google Sheets**: Chọn file Google Sheet đích và trỏ tới Sheet dùng để lưu danh sách flag thừa.
- **Check Dead Flags (If node)**: Kiểm tra xem có tìm thấy flag thừa nào không. Nếu có (`true`), luồng sẽ rẽ nhánh sang bước tạo Jira và Slack.
- **Jira Software & Slack**: Thiết lập dự án Jira nhận task tự động và chọn Channel Slack nhận tin nhắn cảnh báo.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm (Test run) với dữ liệu mẫu xem các node có kết nối và truyền dữ liệu thành công hay không.
- Sau khi kiểm tra kỹ lưỡng, gạt công tắc sang **Active** để workflow chính thức tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng thông báo:** Có thể kết hợp thêm node Telegram hoặc Microsoft Teams nếu đội ngũ của các sếp không sử dụng Slack.
- **Tự động hóa sâu hơn:** Thay vì chỉ tạo Jira ticket, các sếp có thể cấu hình thêm bước tự động tạo Merge Request (MR) trên GitLab để xóa các dòng code khai báo flag thừa đó luôn (nếu code đơn giản).
- **Gửi báo cáo tổng kết:** Thiết lập thêm một nhánh gửi email tóm tắt hàng tháng cho Tech Lead về tổng số nợ kỹ thuật đã được dọn dẹp.

### 📌 Kết luận
Việc quản lý và dọn dẹp Feature Flag trên Android chưa bao giờ dễ dàng đến thế. Với workflow n8n này, đội ngũ của các sếp sẽ tiết kiệm được rất nhiều thời gian, giữ cho mã nguồn luôn tinh gọn và hiệu suất ứng dụng luôn ở mức cao nhất. Hãy import workflow và áp dụng ngay hôm nay!