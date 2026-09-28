---
title: "🚀 Tự Động Quét GitHub Để Phát Hiện AWS IAM Keys Bị Lộ"
description: "Workflow n8n tự động quét GitHub tìm các AWS IAM Access Key bị lộ, đánh giá rủi ro và gửi cảnh báo Slack, giúp các sếp nhanh chóng vô hiệu hoá chìa khóa nguy hiểm."
slug: "tu-dong-quet-github-aws-iam-keys-bi-lo"
tags: [n8n, automation, no-code, security, secops, aws, github]
keywords: [n8n workflow, tự động hóa, AWS IAM, GitHub scanning, security automation]
---

# 🚀 Tự Động Quét GitHub Để Phát Hiện AWS IAM Keys Bị Lộ

Trong môi trường DevOps hiện đại, việc **đánh mất hoặc vô tình công khai AWS Access Key** trên các repository công khai là mối nguy hiểm nghiêm trọng. Các sếp thường phải mất hàng giờ để:

- **Kiểm tra thủ công** từng repo trên GitHub.  
- **Xác định** chìa khóa còn hoạt động hay đã bị thu hồi.  
- **Gửi thông báo** cho đội ngũ bảo mật và thực hiện remediate.

**Workflow này** giải quyết toàn bộ quy trình trên **100% tự động**, không cần viết một dòng code nào. Khi bạn nhấn “Execute workflow”, hệ thống sẽ:

1. Lấy danh sách người dùng AWS và Access Key của họ.  
2. Lọc chỉ những key **đang hoạt động**.  
3. Tìm kiếm trên GitHub các file có chứa key này.  
4. Tổng hợp, đánh giá mức độ rủi ro và **gửi cảnh báo Slack** kèm nút hành động.  
5. (Tùy chọn) **Vô hiệu hoá** key ngay lập tức qua API AWS.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Quét hàng nghìn repo trong vài phút, thay vì ngày/tuần.  
- **Độ chính xác cao**: Chỉ xử lý các Access Key đang hoạt động, giảm false‑positive.  
- **Phản hồi nhanh**: Cảnh báo Slack ngay lập tức, kèm nút “Disable Key” để remediate trong giây lát.  
- **Hoạt động liên tục**: Có thể lên lịch chạy định kỳ, luôn giám sát môi trường AWS của bạn.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản AWS** với IAM permissions: `iam:ListUsers`, `iam:ListAccessKeys`, `iam:UpdateAccessKey`.  
- **API Key GitHub** (Personal Access Token) có quyền `repo` để thực hiện search code.  
- **Workspace Slack** và **Slack Bot Token** (scope `chat:write`, `chat:write.public`).  
- **n8n** đã cài đặt và có các credentials: `aws`, `githubApi`, `slackApi`.  
- (Tùy chọn) Đặt **cron** hoặc **trigger** để chạy định kỳ.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. **Tải file JSON** của workflow (được cung cấp ở link gốc).  
2. Vào **n8n → Workflows → Import**, kéo thả file hoặc dán nội dung JSON.  
3. Nhấn **Import** → **Save**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là danh sách các node quan trọng và cách cấu hình chúng:

| Node | Loại | Hướng dẫn cấu hình |
|------|------|-------------------|
| **When clicking ‘Execute workflow’** | manualTrigger | Không cần thay đổi, dùng để khởi chạy thủ công hoặc kết hợp với cron. |
| **Split Users for Processing** | splitInBatches | Đặt **Batch Size** (ví dụ: `10`) để tránh vượt rate‑limit AWS. |
| **List AWS Users1** | httpRequest (AWS) | Chọn **Credential** → `aws`. Method: `GET`. URL: `https://iam.amazonaws.com/`. Body: XML request `ListUsers`. |
| **Extract AWS Usernames** | code | Không cần thay đổi, script sẽ trích xuất `UserName` từ response. |
| **Get User Access Keys** | httpRequest (AWS) | Credential `aws`. Method: `GET`. URL: `https://iam.amazonaws.com/`. Body: XML `ListAccessKeys` với `UserName` từ node trước. |
| **Filter Active Keys Only** | if | Condition: `{{$json["AccessKeyMetadata"][0]["Status"]}} === "Active"` (hoặc lặp qua mảng). |
| **Prepare Github Search** | code | Script tạo query search GitHub: `{{"\""+$json["AccessKeyId"]+"\""}}` và gán vào `searchQuery`. |
| **Search GitHub for Exposed Keys** | httpRequest (GitHub) | Credential `githubApi`. Method: `GET`. URL: `https://api.github.com/search/code?q={{$node["Prepare Github Search"].json["searchQuery"]}}+repo:YOUR_ORG/*`. |
| **Rate Limit Wait** | wait | Đặt **Wait Time** = `60` giây (hoặc dựa trên `X-RateLimit-Remaining` từ header GitHub). |
| **Aggregate Search Results** | code | Kết hợp các kết quả, loại bỏ trùng lặp, tạo danh sách `exposedFindings`. |
| **Check For Compromised Keys** | if | Condition: `{{$json["exposedFindings"].length > 0}}`. |
| **Generate Security Report** | code | Tạo markdown hoặc JSON báo cáo, bao gồm: User, AccessKeyId, Repo, File, Line, Risk Level. |
| **Format Slack Alert** | code | Định dạng message Slack (blocks) với **button** “Disable Key”. |
| **Slack** | slack | Credential `slackApi`. Channel: `#security-alerts` (hoặc tùy chỉnh). Payload: output của node “Format Slack Alert”. |
| **Disable Access Keys** | httpRequest (AWS) | Credential `aws`. Method: `POST`. URL: `https://iam.amazonaws.com/`. Body: XML `UpdateAccessKey` với `AccessKeyId` và `Status=Inactive`. Kết nối với **button action** trong Slack (Webhook hoặc n8n webhook). |
| **Continue Scanning** | noOp | Dùng để nối luồng khi không có key bị lộ, không cần thay đổi. |
| **Sticky Note** (nếu có) | stickyNote | Chỉ để ghi chú, không ảnh hưởng tới luồng. |

> **Lưu ý:** Đối với node **Search GitHub for Exposed Keys**, hãy thay `YOUR_ORG/*` bằng tên tổ chức hoặc để trống nếu muốn quét toàn bộ GitHub. Kiểm tra **rate‑limit** trong header `X-RateLimit-Remaining`; nếu gần hết, tăng thời gian `Rate Limit Wait`.

#### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow với một người dùng AWS mẫu để kiểm tra toàn bộ chuỗi.  
2. Kiểm tra **Slack** nhận được thông báo đúng định dạng.  
3. Nếu mọi thứ ổn, bật **Active** và (tùy chọn) đặt **cron trigger** để chạy hàng ngày/giờ.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Telegram**: Thêm node Telegram để nhận cảnh báo đồng thời trên nhiều kênh.  
- **Lưu log vào Google Sheets**: Dùng node Google Sheets để ghi lại mỗi lần phát hiện, giúp tạo báo cáo tháng.  
- **Tự động tạo ticket**: Kết nối với Jira hoặc ServiceNow để mở ticket remediation tự động.  
- **Phân loại rủi ro nâng cao**: Sử dụng node `LLM` (OpenAI) để phân tích ngữ cảnh file và đưa ra mức độ nguy hiểm chi tiết hơn.  

### 📌 Kết luận
Với workflow **Automated GitHub Scanner for Exposed AWS IAM Keys**, các sếp sẽ không còn lo lắng về việc chìa khóa AWS bị lộ trên GitHub nữa. Tự động quét, đánh giá, cảnh báo và thậm chí vô hiệu hoá ngay lập tức – tất cả trong một giải pháp **no‑code**, nhanh chóng triển khai và mở rộng. Hãy **import ngay**, cấu hình credentials, và để n8n làm việc thay bạn! 🚀