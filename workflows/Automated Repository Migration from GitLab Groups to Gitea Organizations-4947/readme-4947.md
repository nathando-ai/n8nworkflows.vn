---
title: "🚀 Tự Động Hoá Di Chuyển Repository Từ GitLab Sang Gitea - Không Cần Code!"
description: "Giải pháp hoàn toàn tự động hóa việc di chuyển tất cả các repository từ nhóm GitLab sang tổ chức Gitea chỉ với một lần click. Tiết kiệm hàng giờ công sức thủ công và giảm thiểu rủi ro lỗi."
slug: "tự-dộng-hoá-di-chuyển-gitlab-sang-gitea"
tags: [n8n, automation, gitlab, gitea, devops, no-code, migration]
keywords: [n8n workflow gitlab gitea, tự động hóa di chuyển repository, migrate gitlab to gitea, tự động hóa devops, giải pháp không code]
---

# 🚀 **Tự Động Hoá Di Chuyển Repository Từ GitLab Sang Gitea - Không Cần Code!**

### **Nỗi Đau Của Các Sếp DevOps**
Làm việc với nhiều nhóm dự án trên GitLab nhưng muốn chuyển sang Gitea để tận hưởng tính mở rộng, chi phí thấp hơn và cộng đồng thân thiện? **Thủ công di chuyển từng repository một là một công việc tẻ nhạt, dễ sai sót và tốn thời gian!** Một lần nhấp nháy sai tên folder hoặc quyền truy cập có thể khiến toàn bộ dự án bị mất hoặc bị hỏng.

**Workflow này giải quyết hoàn toàn vấn đề đó:**
- **Tự động hóa 100%** việc di chuyển tất cả repository từ nhóm GitLab sang tổ chức Gitea.
- **Không cần viết code** - chỉ cần cấu hình và chạy.
- **Giảm thiểu rủi ro** bằng cách kiểm tra trước và xử lý lỗi tự động.
- **Hoạt động liên tục** - có thể chạy vào ban đêm hoặc khi không bận.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Di chuyển hàng chục repository chỉ trong vài phút thay vì hàng giờ.
- **Chính xác 100%**: Không lo sai sót tên repository hoặc quyền truy cập.
- **Không gián đoạn công việc**: Chạy tự động vào thời gian rảnh rỗi.
- **Dễ dàng mở rộng**: Thêm hoặc loại bỏ repository một cách linh hoạt.
- **Giảm chi phí**: Gitea là giải pháp miễn phí và mở rộng tốt hơn so với GitLab.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản GitLab** với quyền **Maintainer** trên nhóm dự án cần di chuyển.
2. **Tài khoản Gitea** với quyền **Admin** trên tổ chức đích.
3. **API Token** của cả hai dịch vụ:
   - **GitLab Personal Access Token** (có quyền `api`).
   - **Gitea Personal Access Token** (có quyền `repo`).
4. **Danh sách nhóm dự án** trên GitLab (nếu cần lọc).
5. **Tên tổ chức đích** trên Gitea (ví dụ: `my-gitea-org`).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Bước 1:** Tải file JSON của workflow từ [đây](https://n8n.io/workflows/4947) hoặc sao chép JSON từ trang này.
- **Bước 2:** Mở **n8n Editor** và chọn **Import Workflow** (hay paste JSON vào ô `Import Workflow`).
- **Bước 3:** Chọn **Active** để kích hoạt workflow.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **3 node quan trọng** cần cấu hình cẩn thận:

##### **A. Node "Setup (CHANGE ME)"**
- **Mục đích:** Đặt các biến môi trường cần thiết cho workflow.
- **Cách cấu hình:**
  - Thêm biến `GITLAB_GROUP_ID` (ID của nhóm GitLab bạn muốn di chuyển).
  - Thêm biến `GITEA_ORG_NAME` (tên tổ chức Gitea đích).
  - Thêm biến `GITLAB_TOKEN` và `GITEA_TOKEN` (API Token của hai dịch vụ).
  - **Ví dụ:**
    ```json
    {
      "json": {
        "GITLAB_GROUP_ID": "12345678",
        "GITEA_ORG_NAME": "my-gitea-org",
        "GITLAB_TOKEN": "glpat-xxxxxxxxxxxxx",
        "GITEA_TOKEN": "gitea_xxxxxxxxxxxxx"
      }
    }
    ```

##### **B. Node "GitLab: Get Projects"**
- **Mục đích:** Lấy danh sách tất cả repository trong nhóm GitLab.
- **Cấu hình:**
  - **Method:** `GET`
  - **URL:** `https://gitlab.com/api/v4/groups/{GITLAB_GROUP_ID}/projects`
  - **Headers:**
    - `PRIVATE-TOKEN: $GITLAB_TOKEN`
  - **Lưu ý:** Đảm bảo `GITLAB_GROUP_ID` và `GITLAB_TOKEN` đã được đặt trong node `Setup`.

##### **C. Node "Gitea: Search for repo" và "Gitea: Migrate repo"**
- **Mục đích:**
  - **Search for repo:** Kiểm tra repository đã tồn tại trên Gitea để tránh trùng lặp.
  - **Migrate repo:** Di chuyển repository từ GitLab sang Gitea.
- **Cấu hình chung:**
  - **Headers:**
    - `Authorization: token $GITEA_TOKEN`
  - **URL:**
    - **Search:** `https://<GITEA_DOMAIN>/api/v1/repos/search?q=name:{REPO_NAME}&type=repository`
    - **Migrate:** `https://<GITEA_DOMAIN>/api/v1/repos/migrate`
  - **Tham số:**
    - Đảm bảo `REPO_NAME` và `GITEA_ORG_NAME` được truyền từ node `Loop Over Items`.

##### **D. Node "Switch error codes" và "Stop and Error"**
- **Mục đích:** Xử lý lỗi tự động nếu di chuyển thất bại.
- **Cấu hình:**
  - **Switch:** Đặt điều kiện kiểm tra lỗi (ví dụ: `statusCode` = `404` hoặc `500`).
  - **Stop and Error:** Hiển thị thông báo lỗi chi tiết nếu có vấn đề.

---

#### **3. Kích Hoạt ⚡️**
- **Bước 1:** Nhấn **Execute Workflow** để chạy thử với dữ liệu mẫu.
- **Bước 2:** Kiểm tra **Execution Log** để xác nhận tất cả repository đã di chuyển thành công.
- **Bước 3:** Đặt workflow vào chế độ **Active** để chạy tự động khi cần.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram:**
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để nhận thông báo khi workflow hoàn tất.
   - **Cách làm:**
     - Sau node `Loop Over Items`, thêm node `Slack` với nội dung:
       ```json
       {
         "text": "🚀 Migration completed! {{ $json.length }} repositories moved."
       }
       ```

2. **Lưu Log Lịch Sử:**
   - Thêm node **Google Sheets** hoặc **Notion** để ghi lại lịch sử di chuyển (tên repository, thời gian, trạng thái).
   - **Ưu điểm:** Dễ dàng theo dõi và báo cáo cho team.

3. **Chạy Định Kỳ:**
   - Sử dụng **n8n Cron Trigger** để chạy workflow hàng tháng (ví dụ: cuối tháng) để cập nhật repository mới.

4. **Xử Lý Lỗi Tự Động:**
   - Nếu một repository bị lỗi, workflow sẽ **dừng lại** và hiển thị thông báo. Các sếp có thể:
     - Xem lại **Execution Log** để biết lỗi cụ thể.
     - Cập nhật quyền API hoặc cấu hình lại node `Gitea: Migrate repo`.

---

### 📌 **Kết Luận**
**Workflow này là giải pháp hoàn hảo** cho các sếp DevOps muốn di chuyển repository từ GitLab sang Gitea **không cần viết một dòng code nào**. Bằng cách tự động hóa quy trình, các sếp sẽ:
✅ **Tiết kiệm hàng giờ công sức**.
✅ **Tránh sai sót thủ công**.
✅ **Hoạt động liên tục** mà không cần can thiệp.

**Hãy thử ngay và tự động hóa quy trình của mình!** Nếu có vấn đề, hãy để lại comment bên dưới hoặc liên hệ với cộng đồng n8n để hỗ trợ.

---
**💡 Chia sẻ workflow này với đồng nghiệp của bạn để cùng tự động hóa công việc!** 🚀