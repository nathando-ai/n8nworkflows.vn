---
title: "🚀 Tự Động Hóa Cập Nhật Mock API & Gửi Báo Cáo Thay Đổi OpenAPI Với GitHub & Postman (DevOps)"
description: "Workflow này tự động hóa toàn bộ quy trình cập nhật spec OpenAPI từ GitHub đến Postman, so sánh diff, ghi chú PR và thông báo team - tiết kiệm 80% thời gian kiểm tra thủ công. Phù hợp cho devops, backend engineer và team API management."
slug: "tieu-dong-hoa-cap-nhat-mock-api-va-bao-cao-diff-openapi"
tags: [n8n, automation, devops, api-management, github-actions, postman, openapi]
keywords: [n8n workflow devops, tự động hóa openapi, postman mock server, diff api, github webhook, tự động hóa api management]
---

# 🚀 **Tự Động Hóa Cập Nhật Mock API & Gửi Báo Cáo Thay Đổi OpenAPI Với GitHub & Postman**

### **Giải pháp cho nỗi đau của các sếp DevOps & Backend Engineer**
Hàng ngày, các sếp phải:
- **Thủ công refresh mock server** trên Postman sau mỗi thay đổi spec OpenAPI.
- **So sánh diff** giữa phiên bản cũ và mới bằng tay, dễ bỏ sót lỗi breaking change.
- **Ghi chú PR** và **thông báo team** về thay đổi, gây trễ thời gian review.
- **Rủi ro cao** khi không phát hiện kịp thời các thay đổi ảnh hưởng đến frontend/backend.

**Workflow này tự động hóa toàn bộ quy trình chỉ trong 3 bước:**
1. **Khi có push lên branch `develop`**, GitHub Webhook kích hoạt.
2. **Tự động refresh mock server** trên Postman và tải xuống 2 phiên bản spec OpenAPI.
3. **So sánh diff**, **ghi chú PR** và **gửi email báo cáo** cho team với định dạng Markdown sẵn sàng review.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động 24/7 ổn định, các sếp nên **self-host n8n** trên VPS riêng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
*Lưu ý:* **Không bao giờ commit API key hoặc token vào repo** - sử dụng n8n credentials.
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** so sánh diff và refresh mock thủ công.
- **Phát hiện sớm breaking change** với diff tự động và ghi chú PR chi tiết.
- **Thông báo team** qua email với định dạng Markdown dễ đọc.
- **Hoạt động liên tục** 24/7 khi có thay đổi trên `develop`.
- **Tích hợp hoàn hảo** với GitHub Actions và Postman.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Postman** (API Key + Mock Server ID).
2. **Tài khoản GitHub** với:
   - **Personal Access Token** (scope: `repo`).
   - **Repo** có file `openapi_old.yaml` và `openapi_new.yaml` trên `develop`.
3. **Tài khoản Gmail** (để gửi email báo cáo).
4. **GitHub Actions** (cài đặt `openapi-diff` Docker và cấu hình webhook).
5. **n8n Self-hosted** (không dùng phiên bản cloud).

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/15123](https://n8n.io/workflows/15123).
- **Import vào n8n Editor**:
  - Nhấn `Import` → Chọn file JSON → `Import`.
  - **Hoặc** copy toàn bộ JSON và paste vào `Create Workflow` → `Import JSON`.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình `Set: Config` (Node quan trọng nhất!)**
Mở node này và cập nhật **các tham số sau**:
```json
{
  "postman": {
    "apiKey": "YOUR_POSTMAN_API_KEY",          // Lấy từ Postman: Settings → Developer → API Key
    "mockId": "YOUR_MOCK_SERVER_ID"            // ID của Mock Server trên Postman
  },
  "github": {
    "repo": "owner/repo",                      // Ví dụ: "your-org/your-api-repo"
    "token": "ghp_XXXXXXXXXXXXXXXXXXXXXXXX",   // Token Personal Access Token (scope: repo)
    "prId": "123"                              // Pull Request ID để ghi chú diff
  },
  "email": {
    "sendTo": "team@example.com"              // Email của team để nhận báo cáo
  }
}
```
*Lưu ý:* **Không commit `postman.apiKey` hoặc `github.token` vào repo** - n8n sẽ lưu an toàn trong credentials.

##### **B. Cấu hình GitHub Webhook**
1. Trong n8n, mở node **`GitHub Webhook`** (path: `/webhook/api-update`).
2. **Cấu hình webhook trên GitHub**:
   - Đi đến `Settings → Webhooks → Add webhook`.
   - **Payload URL**: `https://[your-n8n-domain]/webhook/api-update` (ví dụ: `https://n8n.yourdomain.com/webhook/api-update`).
   - **Content type**: `application/json`.
   - **Branch**: Chỉ `develop`.
   - **Events**: Chọn `Push` và `Pull request`.

##### **C. Cấu hình Gmail**
1. Mở node **`Send Summary Email1`**.
2. **Connect Gmail**:
   - Nhấn `Connect` → Đăng nhập tài khoản Gmail.
   - Chọn **OAuth2** (n8n sẽ lưu token an toàn).
3. **Cập nhật `sendTo`** trong `Set: Config` (trên).

##### **D. Cấu hình GitHub Actions (openapi-diff)**
1. Tạo file `.github/workflows/openapi-diff.yml` trong repo GitHub:
   ```yaml
   name: OpenAPI Diff
   on:
     push:
       branches: [ develop ]
   jobs:
     diff:
       runs-on: ubuntu-latest
       steps:
         - uses: actions/checkout@v4
         - name: Run openapi-diff
           run: |
             docker run --rm -v $(pwd):/data openapitools/openapi-diff \
               /data/openapi_old.yaml /data/openapi_new.yaml \
               --output /data/diff_result.json
             curl -X POST -H "Content-Type: application/json" \
               -d '{"diff": $(cat diff_result.json)}' \
               "https://[your-n8n-domain]/webhook/api-diff-result"
   ```
2. **Cập nhật `openapi_old.yaml` và `openapi_new.yaml`** trong repo:
   - `openapi_old.yaml`: Phiên bản cũ (được tải từ branch `develop` trước khi push).
   - `openapi_new.yaml`: Phiên bản mới (được tạo khi có thay đổi).

##### **E. Cấu hình Postman Mock**
1. Tạo **Mock Server** trên Postman:
   - Đi đến `Mock Servers → Create`.
   - Chọn **New Mock Server** và copy `mockId`.
2. **Refresh Mock** khi cần:
   - Node **`Update Postman Mock`** sẽ tự động gọi API Postman với `mockId` và `apiKey`.

#### **3. Kích hoạt ⚡️**
1. **Test run** với dữ liệu mẫu:
   - Nhấn `Run Workflow` → Chọn `Run Once`.
   - Kiểm tra **log** để đảm bảo tất cả node hoạt động.
2. **Bật Active**:
   - Nhấn `Active` trên tab Workflow.

---
### ✍️ **Mẹo & gợi ý nâng cao**
1. **Lưu log diff** vào file CSV/JSON:
   - Thêm node **`n8n-nodes-base.file`** sau `Get Fields` để lưu diff vào file.
   - Dùng để **audit lịch sử thay đổi** dài hạn.

2. **Gửi báo cáo định kỳ**:
   - Sử dụng **`n8n-nodes-base.cron`** để chạy workflow hàng tuần và gửi email tổng hợp.

3. **Tích hợp Slack/Telegram**:
   - Thay thế node `Send Summary Email1` bằng **`n8n-nodes-base.slack`** hoặc **`n8n-nodes-base.telegram`** để thông báo team nhanh hơn.

4. **Tự động tạo PR từ diff**:
   - Sử dụng **`n8n-nodes-base.github`** để tạo PR tự động từ diff nếu có thay đổi nghiêm trọng.

5. **Báo cáo cho Stakeholder**:
   - Thêm node **`n8n-nodes-base.notion`** hoặc **`n8n-nodes-base.confluence`** để ghi chú diff vào wiki team.

---
### 📌 **Kết luận**
Workflow này **giải phóng thời gian** của các sếp DevOps & Backend Engineer khỏi công việc thủ công mệt mỏi, đồng thời **giảm thiểu rủi ro** khi có thay đổi spec OpenAPI. **Hãy áp dụng ngay** để:
✅ **Tự động refresh mock** trên Postman.
✅ **So sánh diff** và ghi chú PR chi tiết.
✅ **Thông báo team** với định dạng Markdown sẵn sàng review.
✅ **Hoạt động liên tục** 24/7 khi có thay đổi.

**Bắt đầu tự động hóa ngay hôm nay!** 🚀
*Cần hỗ trợ cấu hình?* Đăng ký **VPS n8n** từ [TinoHost](https://tino.vn/vps-n8n?affid=388) và liên hệ team hỗ trợ để được cài đặt workflow chi tiết!