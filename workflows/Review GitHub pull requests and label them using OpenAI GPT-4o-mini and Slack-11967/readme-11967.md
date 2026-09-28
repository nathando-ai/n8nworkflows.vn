---
title: "🤖 Tự Động Hóa Review Pull Request GitHub Với AI GPT-4o-mini + Slack: Giảm Thời Gian Review 90% Cho Team Dev"
description: "Workflow tự động phân tích PR trên GitHub bằng AI, gán nhãn tự động, gửi comment review và thông báo Slack - giúp team phát triển tiết kiệm thời gian và cải thiện chất lượng code."
slug: "tieu-dong-hoa-review-pull-request-github-ai-gpt-4o-mini"
tags: [n8n, automation, ai-summarization, github, slack, openai, code-review]
keywords: [n8n workflow github, tự động hóa review code, ai gpt-4o-mini, tự động gán nhãn pull request, tự động hóa devops, tự động hóa team phát triển]
---

# 🚀 **Tự Động Hóa Review Pull Request GitHub Với AI GPT-4o-mini + Slack**

### **Giải pháp AI tự động phân tích PR, gán nhãn và thông báo Slack - giúp team dev tiết kiệm thời gian và nâng cao chất lượng code**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động 24/7 ổn định, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: AI tự động phân tích PR trong vài giây thay vì mất hàng giờ của dev.
- **Chất lượng code cao hơn**: Phát hiện lỗi an toàn, phức tạp và cải tiến code một cách tự động.
- **Tự động gán nhãn PR**: Nhãn như `needs-review`, `security-vulnerability`, `code-improvement` được gán chính xác.
- **Thông báo Slack tự động**: Team được cảnh báo ngay khi PR cần review hoặc có vấn đề.
- **Lưu lịch sử review**: Tất cả kết quả được ghi vào Google Sheets để theo dõi và phân tích.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản GitHub** với quyền:
   - Tạo Webhook cho repository.
   - Truy cập API GitHub (OAuth App).
2. **API Key OpenAI** (để sử dụng GPT-4o-mini).
3. **Slack Workspace** với:
   - Token Slack App (Bot Token).
   - Channel ID để gửi thông báo.
4. **Google Sheets** với:
   - Spreadsheet ID (để lưu log review).
   - Quyền chỉnh sửa cho n8n.
5. **VPS n8n** (self-hosted) để workflow chạy liên tục.

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/11967](https://n8n.io/workflows/11967) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ link trên và paste vào **Import Workflow** trong n8n.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
#### **A. Cấu hình Webhook GitHub**
- **Node**: `GitHub PR Webhook`
  - Đăng ký Webhook trên GitHub:
    - **URL**: `https://<tên-vps-n8n>/github-pr-review`
    - **Events**: Chọn `Pull Request` (các event: `opened`, `synchronize`, `reopened`).
    - **Secret**: Nhập một chuỗi ngẫu nhiên (để xác thực).

#### **B. Cấu hình GitHub OAuth**
- **Node**: `Get PR Files` và `Add PR Labels`
  - Tạo **OAuth App** trên GitHub:
    - **Application Name**: `n8n-GitHub-Reviewer`
    - **Homepage URL**: `https://<tên-vps-n8n>`
    - **Authorization Callback URL**: `https://<tên-vps-n8n>/oauth2/callback`
    - **Permissions**:
      - `repo` (full control of private repositories).
      - `admin:org` (nếu cần review trên org).
    - Sau khi tạo, lấy **Client ID** và **Client Secret** để điền vào n8n.

#### **C. Cấu hình OpenAI (GPT-4o-mini)**
- **Node**: `OpenAI Chat Model`
  - Điền **API Key OpenAI** vào n8n (Settings > Credentials > Add Credential).
  - **Model**: Đảm bảo chọn `gpt-4o-mini` (hoặc `gpt-4o` nếu có).

#### **D. Cấu hình Slack**
- **Node**: `Notify Slack`
  - Tạo **Slack App**:
    - **Token**: `xoxb-...` (Bot Token).
    - **Channel ID**: Lấy từ `https://api.slack.com/apps/<app-id>/conversations` (điền vào `channel`).
  - **Message Format**: Sử dụng template mặc định hoặc tùy chỉnh:
    ```json
    {
      "text": "🔍 **AI Review Result** for PR #{{$node["Get PR Files"].json.path("number")}}",
      "attachments": [
        {
          "title": "Review Summary",
          "text": "{{$node["Parse AI Review"].json.path("summary")}}",
          "fields": [
            {"title": "Labels Added", "value": "{{$node["Add PR Labels"].json.path("labels") | join(', ')}}", "short": true}
          ]
        }
      ]
    }
    ```

#### **E. Cấu hình Google Sheets**
- **Node**: `Log to Sheets`
  - Điền **Spreadsheet ID** (lấy từ URL của sheet: `https://docs.google.com/spreadsheets/d/<ID>/edit`).
  - **Sheet Name**: Đặt tên sheet (ví dụ: `PR_Reviews`).
  - **Headers**: Cấu hình cột như:
    ```
    PR_Number,Title,Files_Changed,Review_Summary,Labels_Added,Review_Date
    ```

#### **F. Code Customization (Node `Analyze File Changes` và `Parse AI Review`)**
- **Node `Analyze File Changes`**:
  - Mở **Code Editor** và chỉnh sửa logic phân tích file (nếu cần).
  - Ví dụ: Tăng giảm trọng số cho các loại file (JS, Python, etc.).
- **Node `Parse AI Review`**:
  - Chỉnh sửa logic để trích xuất thông tin từ AI (ví dụ: lấy `summary`, `recommendations`, `vulnerabilities`).

#### **G. Test Run & Active Workflow**
1. **Test với PR mẫu**:
   - Tạo một PR test trên GitHub và kích hoạt workflow.
   - Kiểm tra:
     - Slack có nhận được thông báo không?
     - PR có được gán nhãn và comment không?
     - Google Sheets có ghi log không?
2. **Active workflow**:
   - Sau khi kiểm tra thành công, chuyển trạng thái từ **Draft** sang **Active**.

---

## ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với GitHub Actions**:
   - Sử dụng workflow này cùng với GitHub Actions để tự động **merge PR** nếu AI đánh giá là `✅ Approved`.
2. **Lưu log chi tiết hơn**:
   - Thêm cột `AI_Confidence` vào Google Sheets để theo dõi độ tin cậy của AI.
3. **Thông báo cá nhân hóa**:
   - Tùy chỉnh Slack message để gửi **@mention** cho dev chủ PR nếu có vấn đề nghiêm trọng.
4. **Tích hợp với Jira**:
   - Sử dụng node `httpRequest` để tạo ticket Jira khi phát hiện lỗi an toàn.
5. **Monitoring lỗi**:
   - Thêm node `error` để log lỗi vào Google Sheets nếu AI hoặc API gặp vấn đề.

---

## 📌 **Kết luận**
Workflow này **giải phóng team dev khỏi công việc review PR thủ công**, giúp:
✅ **Tăng hiệu suất** với AI phân tích trong vài giây.
✅ **Nâng cao chất lượng code** bằng đánh giá tự động.
✅ **Tự động hóa thông báo** qua Slack và ghi log chi tiết.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với PR mẫu** trước khi áp dụng toàn bộ team.
3. **Tối ưu hóa** bằng cách chỉnh sửa code và Slack message.

👉 **Bắt đầu tự động hóa review PR của bạn ngay hôm nay!** 🚀