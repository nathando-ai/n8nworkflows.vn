---
title: "🚀 Tự Động Hóa Theo Dõi & Thông Báo Nhiệm Vụ Bài Viết với Airtable & Motion (Không Cần Code)"
description: "Giải pháp tự động hóa hoàn toàn cho các nhà quản lý dự án, biên tập viên và đội ngũ marketing để theo dõi tiến độ bài viết, nhận thông báo khi hoàn thành các milestone quan trọng, và cập nhật tự động trên Airtable. Tiết kiệm thời gian lên đến 80% trong quản lý nội dung!"
slug: "tu-dong-hoa-theo-doi-nhiem-vu-bai-viet-airtable-motion"
tags: [n8n, automation, project-management, multimodal-ai, airtable, motion, gmail, no-code]
keywords: [n8n workflow tự động hóa bài viết, theo dõi tiến độ bài viết, thông báo hoàn thành nhiệm vụ, Airtable + Motion, tự động hóa nội dung, quản lý dự án biên tập]
---

# 🚀 **Tự Động Hóa Theo Dõi & Thông Báo Nhiệm Vụ Bài Viết với Airtable & Motion**

### **Giải pháp cho ai?**
Các **sếp quản lý dự án**, **nhà biên tập**, **quản lý nội dung**, và **nhóm marketing** đang mệt mỏi vì phải:
- **Tra cứu thủ công** tiến độ bài viết trên nhiều dự án khác nhau.
- **Nhớ gửi thông báo** khi bài viết hoàn thành (hay quên).
- **Cập nhật Airtable** sau mỗi lần hoàn thành nhiệm vụ.
- **Phải check nhiều công cụ** (Motion, Gmail, Airtable) để theo dõi một dự án.

**Workflow này tự động hóa toàn bộ quy trình** – chỉ cần **cấu hình 1 lần**, hệ thống sẽ:
✅ **Lấy dữ liệu dự án** từ Airtable và Motion.
✅ **Lọc ra những nhiệm vụ "Todo" liên quan đến SEO** (hoặc tùy chỉnh theo yêu cầu).
✅ **Kiểm tra hoàn thành** và **cập nhật tự động** trên Airtable.
✅ **Gửi email thông báo** cho bạn và khách hàng khi nhiệm vụ hoàn thành.
✅ **Chạy tự động hàng tháng** (hoặc theo lịch bạn đặt).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên **VPS riêng** thay vì dùng phiên bản cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** – giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** trong việc theo dõi và thông báo tiến độ bài viết.
- **Tránh quên gửi thông báo** nhờ hệ thống tự động gửi email khi nhiệm vụ hoàn thành.
- **Cập nhật Airtable tự động**, không cần phải làm thủ công.
- **Theo dõi nhiều dự án cùng lúc** mà không lo bỏ sót.
- **Cá nhân hóa thông báo** với tên dự án, nhiệm vụ hoàn thành, và liên kết đến Airtable.
- **Chỉ cần cấu hình 1 lần**, workflow sẽ hoạt động **một mình** hàng tháng.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Airtable**:
   - Tài khoản Airtable với **bảng dữ liệu dự án** có các trường sau:
     - **Tên dự án** (Project names)
     - **Motion Workspace ID** (ID của workspace Motion)
     - **Trạng thái** (`Status - Calendrier éditorial`) → Đặt thành **"Actif"** cho dự án đang hoạt động.
     - **Lần gửi cuối** (`Last sent - Calendrier éditorial`) → Để theo dõi không gửi trùng lặp.
     - **Email liên hệ** (Client và thành viên nhóm).
   - **Token API Airtable** (Personal Access Token) để n8n truy cập bảng dữ liệu.

2. **Motion**:
   - Tài khoản Motion với **API access** (đăng ký tại [Motion API](https://motion.ai/developers)).
   - **Authentication Header** cho HTTP Request (cấu hình trong n8n).

3. **Gmail**:
   - Tài khoản Gmail để gửi email thông báo.
   - **OAuth2 credentials** cho n8n (cấu hình trong n8n).

4. **n8n**:
   - **Self-hosted n8n** (không dùng phiên bản cloud để tránh giới hạn).
   - **VPS 2GB RAM trở lên** (đủ cho workflow này).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow:
- **Tải file JSON** từ [n8n.io/workflows/7383](https://n8n.io/workflows/7383) và import vào **n8n Editor**.
- **Copy toàn bộ JSON** từ link trên và **paste vào n8n Editor** (tab "Import").

:::note[Lưu ý]
- **Không chỉnh sửa tên node** trong workflow (nếu không muốn bị lỗi).
- **Không xóa node** nào, chỉ cần **cấu hình lại credentials** và tham số.
:::

---

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **11 node**, các sếp cần **cấu hình kỹ** các node sau:

| **Node**               | **Loại Node**       | **Lưu ý cấu hình**                                                                 |
|------------------------|---------------------|-----------------------------------------------------------------------------------|
| **Schedule Trigger**   | `scheduleTrigger`    | - **Thời gian chạy mặc định**: 10-31 tháng mỗi ngày lúc 8h sáng. <br> - **Cron expression**: `0 8 10-31 * *` (có thể thay đổi). |
| **Récupération infos airtable** | `airtable` | - **Credentials**: Chọn `airtableTokenApi`. <br> - **Operation**: `search`. <br> - **Base ID**: ID của bảng Airtable bạn dùng. <br> - **View**: Chọn view phù hợp (ví dụ: "Dự án đang hoạt động"). |
| **Actif**              | `if`                | - **Condition**: Kiểm tra `Status - Calendrier éditorial = "Actif"`.              |
| **Loop Over Items**    | `splitInBatches`    | - **Batch size**: 10 (đủ để xử lý nhiều dự án cùng lúc).                          |
| **Récupération des projets** | `httpRequest` | - **Credentials**: Chọn `httpHeaderAuth` (cấu hình từ Motion API). <br> - **URL**: `https://api.motion.ai/v1/workspaces/{workspaceId}/projects` (đặt `{workspaceId}` từ Airtable). <br> - **Headers**: Thêm `Authorization: Bearer {your_motion_api_token}`. |
| **Tri des projets**    | `code`              | - **Mã JavaScript**: Lọc ra dự án có tên chứa **"SEO"** và trạng thái **"Todo"**. <br> **Gợi ý mã**:
  ```javascript
  // Lọc dự án có "SEO" trong tên và trạng thái "Todo"
  return {
    json: {
      projects: $input.all().filter(project =>
        project.name.includes("SEO") &&
        project.status === "Todo"
      )
    }
  };
  ``` |
| **Todo**               | `filter`            | - **Condition**: Lọc dự án có `status = "Todo"`.                                  |
| **HTTP Request**       | `httpRequest`        | - **URL**: `https://api.motion.ai/v1/projects/{projectId}/tasks` (lấy `projectId` từ Airtable). <br> - **Headers**: Thêm `Authorization: Bearer {your_motion_api_token}`. <br> - **Query**: `status=completed&taskName=Intégrer%20les%20articles%20de%20blog` (tùy chỉnh tên nhiệm vụ). |
| **If1**                | `if`                | - **Condition**: Kiểm tra nếu nhiệm vụ đã hoàn thành (`status = "Completed"`).     |
| **Airtable (Update)**  | `airtable`          | - **Credentials**: `airtableTokenApi`. <br> - **Operation**: `update`. <br> - **Record ID**: Lấy từ Airtable. <br> - **Fields**: Cập nhật `Last sent` thành thời gian hiện tại. |
| **Send a message**     | `gmail`             | - **Credentials**: `gmailOAuth2`. <br> - **To**: Email của khách hàng/nhóm. <br> - **Subject**: `📢 Bài viết "{projectName}" đã hoàn thành!`. <br> - **Body (HTML)**:
  ```html
  <p>Xin chào,</p>
  <p>Bài viết <strong>"{{ $json.projectName }}</strong>" đã được hoàn thành thành công!</p>
  <p>Nhiệm vụ: <strong>"{{ $json.taskName }}</strong></p>
  <p>Liên kết dự án: <a href="https://airtable.com/{{ $json.airtableLink }}">Xem trên Airtable</a></p>
  <p>Trân trọng,<br>Đội ngũ {{ $json.companyName }}</p>
  ``` |

---

#### **3. Kích hoạt ⚡️**
Sau khi cấu hình xong:
1. **Test run** với **dữ liệu mẫu** (chọn node **Schedule Trigger** → **Run once**).
2. Kiểm tra:
   - Email có được gửi không?
   - Airtable có được cập nhật không?
   - Motion có trả về dữ liệu dự án không?
3. Nếu **không có lỗi**, bật **Active workflow**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
#### **1. Tùy chỉnh nhiệm vụ theo dự án**
- **Thay đổi tên nhiệm vụ** trong node `HTTP Request` (ví dụ: `"Intégrer les articles de blog"` → `"Chỉnh sửa bài viết SEO"`).
- **Lọc nhiều nhiệm vụ khác nhau** bằng cách thêm **node `code`** để lọc ra nhiều task name.

#### **2. Thêm Slack/Telegram thông báo**
- Thêm **node `slack`** hoặc **`webhook`** sau node `If1` để gửi thông báo đến Slack/Telegram.
- **Mẫu thông báo Slack**:
  ```json
  {
    "text": `📢 Bài viết **${projectName}** đã hoàn thành!\nNhiệm vụ: **${taskName}**`,
    "attachments": [
      {
        "title": "Liên kết dự án",
        "title_link": "https://airtable.com/${airtableLink}",
        "color": "#36a64f"
      }
    ]
  }
  ```

#### **3. Lưu log hoạt động**
- Thêm **node `stickyNote`** sau node `Airtable (Update)` để ghi log:
  ```javascript
  // Ghi log vào stickyNote
  return {
    stickyNote: {
      title: `Cập nhật dự án ${$input.item().json.projectName}`,
      content: `Nhiệm vụ "${$input.item().json.taskName}" đã hoàn thành và cập nhật Airtable.`
    }
  };
  ```

#### **4. Gửi báo cáo định kỳ**
- **Thêm node `scheduleTrigger`** mới với thời gian khác (ví dụ: **mỗi cuối tháng**) để gửi **báo cáo tổng hợp** tất cả dự án đã hoàn thành.

#### **5. Hỗ trợ nhiều loại dự án**
- **Thêm trường `Project Type`** vào Airtable (ví dụ: "SEO", "Blog", "Video").
- **Cập nhật node `code`** để lọc theo loại dự án:
  ```javascript
  return {
    json: {
      projects: $input.all().filter(project =>
        project.name.includes("SEO") &&
        project.status === "Todo" &&
        project.projectType === "Blog" // Thêm điều kiện loại dự án
      )
    }
  };
  ```

---

### 📌 **Kết luận**
Workflow này **giải phóng bạn khỏi việc theo dõi thủ công** và **tự động hóa toàn bộ quy trình quản lý bài viết** với Airtable và Motion. **Chỉ cần cấu hình 1 lần**, hệ thống sẽ:
✔ **Lấy dữ liệu dự án** từ Motion.
✔ **Kiểm tra hoàn thành nhiệm vụ**.
✔ **Cập nhật Airtable**.
✔ **Gửi email thông báo** tự động.

**Hành động ngay!**
1. **Import workflow** vào n8n của bạn.
2. **Cấu hình Airtable, Motion và Gmail**.
3. **Test run** và **bật Active**.
4. **Quên đi việc theo dõi thủ công** – hệ thống sẽ làm tất cả!

**Nếu cần hỗ trợ**, các sếp có thể:
- **Đăng ký VPS** từ [TinoHost](https://tino.vn/vps-n8n?affid=388) để self-host n8n.
- **Tùy chỉnh workflow** theo nhu cầu riêng bằng cách thêm node `code` hoặc `filter`.
- **Mở rộng** bằng cách kết nối Slack, Telegram, hoặc các công cụ khác.

**🚀 Hãy tự động hóa ngay hôm nay!**