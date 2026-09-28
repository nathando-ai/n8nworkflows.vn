---
title: "🚀 Tự Động Hóa Onboarding Khách Hàng: Từ Form Tally → Google Drive, Notion & Slack (Không Cần Code)"
description: "Giải pháp tự động hóa hoàn toàn cho quá trình onboarding khách hàng, kết nối form Tally với Google Drive, Notion và Slack để tiết kiệm thời gian lên đến 80% và giảm thiểu lỗi thủ công. Đơn giản, mạnh mẽ và hoạt động 24/7."
slug: "tuy-dong-hoa-onboarding-khach-hang-tally-google-drive-notion-slack"
tags: [n8n, automation, CRM, no-code, google-drive, notion, slack]
keywords: [tự động hóa onboarding khách hàng, n8n workflow, tự động hóa form tally, google drive automation, notion automation, slack notification]
---

# 🚀 **Tự Động Hóa Onboarding Khách Hàng: Từ Form Tally → Google Drive, Notion & Slack (Không Cần Code)**

### **💡 Giải pháp cho nỗi đau của các sếp:**
Hàng ngày, các sếp phải mất **giờ đồng hồ** để:
- Nhập liệu khách hàng mới từ form Tally vào Google Drive, Notion và gửi thông báo trên Slack.
- Lo lắng về **lỗi nhập liệu thủ công** (ví dụ: quên gửi link onboarding, sai thông tin email).
- **Không có thời gian** để tập trung vào chiến lược kinh doanh vì bị mắc kẹt trong công việc lặp lại.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Tạo folder Google Drive** riêng cho mỗi khách hàng mới.
✅ **Nhập dữ liệu vào Notion** (cập nhật tự động khi khách hàng submit form).
✅ **Gửi thông báo Slack** để team biết khách hàng mới đã đăng ký.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này **ổn định và an toàn**, các sếp nên **self-host n8n** trên VPS riêng thay vì dùng phiên bản cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**).
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này).
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Giảm **80% công việc thủ công** (không cần nhập liệu vào Google Drive/Notion).
- **Chính xác 100%**: Không còn sai sót do nhập liệu sai (ví dụ: email, tên khách hàng).
- **Cá nhân hóa**: Mỗi khách hàng được tạo **folder riêng** trên Google Drive và **trang Notion riêng**.
- **Team đồng bộ**: Thông báo Slack giúp toàn bộ đội ngũ biết khách hàng mới đã đăng ký.
- **Hoạt động liên tục**: Workflow chạy **24/7** mà không cần can thiệp của con người.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✅ **Tài khoản Tally Forms** (để nhận dữ liệu từ form).
✅ **Google Drive OAuth2**:
   - Tạo **credentials OAuth2** tại [Google Cloud Console](https://console.cloud.google.com/).
   - Cấp quyền: `Google Drive API`.
✅ **Notion API**:
   - Tạo **credentials OAuth2** tại [Notion Developer Platform](https://www.notion.so/my-integrations).
   - Chọn **database** có các trường: **Name, Email, Project Type, Budget, Onboarding Link**.
✅ **Slack OAuth2**:
   - Tạo **credentials OAuth2** tại [Slack API](https://api.slack.com/apps).
   - Chọn **scopes**: `chat:write`, `users:read`.
✅ **Domain n8n** (để nhận webhook từ Tally Forms).

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
**Bước 1:** Tải workflow từ [n8n.io](https://n8n.io/workflows/6351) hoặc copy JSON từ trang này.
**Bước 2:** Mở **n8n Editor** và nhấn **"Import"** → Dán JSON hoặc tải file `.json`.
**Bước 3:** Workflow sẽ xuất hiện trên canvas với **7 nodes** chính.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này **có nhiều giá trị hardcoded**, các sếp **phải thay đổi** để phù hợp với môi trường của mình.

##### **🔹 Node "Webhook" (Lắng nghe form Tally)**
- **Path**: `/tally-submission` (không cần thay đổi).
- **HTTP Method**: `POST` (không cần thay đổi).
- **Lưu ý**:
  - Đảm bảo **Tally Forms** được cấu hình gửi dữ liệu POST đến:
    `https://<your-n8n-domain>/webhook/tally-submission`
  - **Fields bắt buộc** trong form:
    - `Name` (Tên khách hàng)
    - `Email` (Email liên lạc)
    - `Project Type` (Loại dự án)
    - `Budget` (Ngân sách)

##### **🔹 Node "Create folder" (Google Drive)**
- **Credentials**: Chọn `googleDriveOAuth2Api` (đã cấu hình trước).
- **Giá trị hardcoded cần thay đổi**:
  - **Parent folder ID** (hiện tại là `1rCt7cyX7b3FQSJRDB8bRT4ho9QEUh0mA`).
    - **Cách lấy ID**:
      1. Mở Google Drive.
      2. Tạo **1 folder test** (ví dụ: "Test Onboarding").
      3. Click chuột phải → **Share** → Copy **link shareable**.
      4. Trích xuất ID từ URL: `https://drive.google.com/drive/folders/<ID>` → **ID** là `1rCt7cyX7b3FQSJRDB8bRT4ho9QEUh0mA` (thay bằng ID của folder test).
  - **Folder name**: `{$.json.name}_Onboarding` (tự động tạo tên folder từ tên khách hàng).

##### **🔹 Node "Create a database page" (Notion)**
- **Credentials**: Chọn `notionApi` (đã cấu hình trước).
- **Giá trị hardcoded cần thay đổi**:
  - **Database ID** (hiện tại là `230bb34e-b122-800a-87e4-c5f2e30500b9`).
    - **Cách lấy ID**:
      1. Mở **Notion Database** của bạn.
      2. Click vào **3 dấu chấm (⋮)** → **Share** → Copy **link shareable**.
      3. Trích xuất ID từ URL: `https://www.notion.so/workspace/<ID>` → **ID** là `230bb34e-b122-800a-87e4-c5f2e30500b9` (thay bằng ID của database).
  - **Fields bắt buộc trong database**:
    - `Name` (Tên khách hàng)
    - `Email` (Email liên lạc)
    - `Project Type` (Loại dự án)
    - `Budget` (Ngân sách)
    - `Onboarding Link` (Link folder Google Drive + Notion).

##### **🔹 Node "Send a message" (Slack)**
- **Credentials**: Chọn `slackOAuth2Api` (đã cấu hình trước).
- **Giá trị hardcoded cần thay đổi**:
  - **Channel**: `#client-notifications` (hiện tại).
    - **Lưu ý**: Nếu team dùng channel khác, thay đổi ở **field "channel"** trong node này.
  - **Message template**:
    ```json
    {
      "text": "🚀 New Client Onboarding: {{ $json.name }}",
      "blocks": [
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": "*New Client:* <{{ $json.email }}|{{ $json.name }}> 📧"
          }
        },
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": "*Project:* {{ $json.projectType }} | *Budget:* {{ $json.budget }}"
          }
        },
        {
          "type": "actions",
          "elements": [
            {
              "type": "button",
              "text": {
                "type": "plain_text",
                "text": "View Onboarding Link"
              },
              "url": "{{ $json.onboardingLink }}"
            }
          ]
        }
      ]
    }
    ```
    - **Thay đổi**:
      - `{{ $json.onboardingLink }}` sẽ tự động được tạo từ **folder Google Drive** và **trang Notion**.

##### **🔹 Node "Extract Client Fields" (Code)**
- **Lưu ý**: Node này **không cần chỉnh sửa**, nó tự động **trích xuất và định dạng** dữ liệu từ form Tally.
- **Output**:
  - Tạo **folder Google Drive** với tên: `{Tên khách hàng}_Onboarding`.
  - Tạo **trang Notion** với tất cả thông tin khách hàng.
  - Tạo **link onboarding** (Google Drive + Notion).

##### **🔹 Node "Merge"**
- **Lưu ý**: Node này **kết hợp dữ liệu** từ các node trước để gửi Slack notification.
- **Không cần chỉnh sửa**.

---

#### **3. Kích hoạt ⚡️**
**Bước 1: Test run với dữ liệu mẫu**
1. Mở **node Webhook** → Nhấn **"Test"** → Gửi **dữ liệu mẫu** (ví dụ):
   ```json
   {
     "name": "Nguyễn Văn A",
     "email": "a@example.com",
     "projectType": "Website Development",
     "budget": "50000000"
   }
   ```
2. Kiểm tra:
   - **Google Drive**: Folder `{Nguyễn Văn A}_Onboarding` được tạo.
   - **Notion**: Trang khách hàng được thêm vào database.
   - **Slack**: Thông báo được gửi.

**Bước 2: Bật Active workflow**
- Nhấn **"Active"** ở góc trên bên phải → Workflow sẽ **chạy tự động** khi có form Tally mới.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tự động gửi email onboarding**
   - Thêm **node `n8n-nodes-base.email`** sau node **Merge** để gửi email tự động với link onboarding.
   - **Template email**:
     ```html
     <p>Xin chào {{ $json.name }},</p>
     <p>Dữ liệu onboarding của bạn đã được tạo thành công:</p>
     <ul>
       <li><a href="{{ $json.onboardingLink }}">Mở folder Google Drive</a></li>
       <li><a href="{{ $json.notionLink }}">Mở trang Notion</a></li>
     </ul>
     <p>Trân trọng,</p>
     <p>Team {{ $json.projectType }}</p>
     ```

2. **Lưu log hoạt động**
   - Thêm **node `n8n-nodes-base.stickyNote`** để ghi lại lịch sử onboarding (giúp theo dõi và debug).

3. **Tích hợp với CRM khác**
   - Thay thế **Notion** bằng **HubSpot, Salesforce** hoặc **Airtable** bằng cách thay đổi node `notion` thành `hubspot`, `salesforce`, hoặc `airtable`.

4. **Tự động tạo contract**
   - Sử dụng **node `n8n-nodes-base.googleDocs`** để tạo **contract mẫu** cho khách hàng mới.

5. **Báo cáo định kỳ**
   - Thêm **node `n8n-nodes-base.googleSheets`** để ghi dữ liệu onboarding vào **Google Sheets** và tự động tạo **báo cáo tháng**.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** của các sếp để tập trung vào **kinh doanh và chiến lược**, trong khi công việc lặp lại được tự động hóa hoàn toàn. **Không cần code**, chỉ cần **cấu hình vài bước** là xong!

**🚀 Hành động ngay:**
1. **Import workflow** vào n8n của mình.
2. **Thay đổi các giá trị hardcoded** (Google Drive ID, Notion Database ID, Slack Channel).
3. **Test run** với dữ liệu mẫu.
4. **Bật Active** và **nhận khách hàng mới tự động onboarding!**

**💬 Cần hỗ trợ?** Để lại comment bên dưới hoặc liên hệ qua [Slack Community n8n](https://n8n.io/community) để được hỗ trợ chi tiết!