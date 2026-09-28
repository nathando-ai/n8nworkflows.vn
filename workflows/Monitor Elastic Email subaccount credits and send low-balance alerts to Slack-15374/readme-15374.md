---
title: "🚀 Tự động giám sát số dư Elastic Email và cảnh báo qua Slack với n8n"
description: "Hướng dẫn cài đặt workflow n8n tự động kiểm tra số lượng credit của các subaccount Elastic Email định kỳ và gửi cảnh báo về Slack khi tài khoản sắp cạn kiệt."
slug: "giam-sat-elastic-email-credit-va-canh-bao-slack-n8n"
tags: [n8n, automation, devops, elastic-email, slack, monitoring]
keywords: [n8n workflow, giám sát elastic email, cảnh báo slack credit, tự động hóa devops, n8n http request]
---

# 🚀 Tự động giám sát số dư Elastic Email và cảnh báo qua Slack

Trong quá trình vận hành hệ thống gửi email marketing hoặc transactional email, việc tài khoản phụ (subaccount) bị cạn kiệt credit mà không hay biết sẽ dẫn đến việc gián đoạn toàn bộ chiến dịch gửi mail của doanh nghiệp. Việc kiểm tra thủ công hàng ngày rất tốn thời gian và dễ bị bỏ sót. 

Workflow n8n này sẽ giải quyết triệt để vấn đề đó bằng cách tự động hóa 100 quy trình kiểm tra số dư Elastic Email và bắn thông báo trực tiếp lên Slack ngay khi phát hiện tài khoản có lượng credit thấp hơn ngưỡng cho phép.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Giám sát 24/7:** Chủ động nắm bắt tình trạng credit của tất cả các subaccount Elastic Email mà không cần thao tác thủ công.
- **Cảnh báo tức thì:** Nhận thông báo trực tiếp qua kênh Slack ngay khi subaccount chạm ngưỡng "báo động đỏ".
- **Ngăn ngừa gián đoạn hệ thống:** Tránh tình trạng email gửi đi thất bại do tài khoản hết credit bất ngờ.
- **Tùy biến linh hoạt:** Dễ dàng điều chỉnh ngưỡng credit tối thiểu và kênh nhận thông báo theo ý muốn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **Elastic Email** và API Key (Auth Token).
- Tài khoản **Slack** có quyền cấu hình và kết nối App (Slack OAuth2 API).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow hoặc copy trực tiếp mã JSON từ hệ thống n8n và dán vào màn hình n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình chính xác các node sau:

- **Schedule Trigger:** Thiết lập lịch chạy định kỳ (ví dụ: chạy mỗi ngày 1 lần hoặc vài tiếng một lần tùy theo nhu cầu).
- **Config:** Đặt số lượng credit tối thiểu cho phép trong node này. Nếu subaccount nào có số dư thấp hơn mức này, workflow sẽ kích hoạt cảnh báo.
- **Load EE Subaccounts (HTTP Request node):** 
  - Tạo Generic Credential loại **Custom Auth**.
  - Trong trường JSON, điền cấu trúc API Key của Elastic Email như sau:
    ```json
    {
        "headers": {
            "X-ElasticEmail-ApiKey": "<Your EE Auth token>"
        }
    }
    ```
    *(Các sếp có thể lấy Auth Token tại [Elastic Email API Settings](https://app.elasticemail.com/marketing/settings/new/manage-api)).*
- **Check if account has enough email credits (Filter):** Kiểm tra điều kiện lọc các tài khoản có số dư dưới mức cấu hình.
- **Prepare message content (Code):** Xử lý định dạng nội dung tin nhắn trước khi gửi đi.
- **Send notification about low Email Credits & Send an Error message (Slack):** Kết nối tài khoản Slack của các sếp thông qua **Slack OAuth2 API** để chọn kênh (channel) nhận tin nhắn cảnh báo.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử dữ liệu mẫu và kiểm tra xem thông báo đã bắn về Slack chính xác chưa.
- Nếu mọi thứ mượt mà, hãy gạt nút **Active** để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa dạng hóa kênh nhận:** Ngoài Slack, các sếp có thể nhân bản node thông báo để bắn thêm tin nhắn về Telegram Bot hoặc Email cá nhân của đội ngũ kỹ thuật.
- **Lưu log vào Google Sheets:** Thêm một node Google Sheets ở cuối luồng để ghi lại lịch sử các lần cảnh báo, giúp dễ dàng thống kê và theo dõi lịch sử tiêu thụ credit của từng subaccount.
- **Tự động hóa nâng cao:** Kết hợp thêm các bước tự động tạo Task trên Trello/Jira cho bộ phận kế toán/vận hành khi tài khoản sắp hết tiền để tiến hành nạp credit kịp thời.

### 📌 Kết luận
Với workflow giám sát Elastic Email này, các sếp sẽ hoàn toàn yên tâm rằng hệ thống gửi email của mình luôn được kiểm soát chặt chẽ, loại bỏ hoàn toàn rủi ro gián đoạn do hết credit. Hãy cài đặt ngay hôm nay để tối ưu hóa quy trình DevOps của doanh nghiệp!