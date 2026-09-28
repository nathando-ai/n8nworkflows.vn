---
title: "🧹 Xóa Lịch Sử Thực Thi n8n Trên MySQL Tự Động - Giải Pháp Tiết Kiệm Dung Lượng & Tăng Tốc Hiệu Suất"
description: "Workflow tự động hóa xóa lịch sử thực thi n8n trên cơ sở dữ liệu MySQL định kỳ, giúp các sếp giảm thiểu dung lượng lưu trữ, tăng tốc độ hoạt động và duy trì hiệu suất tối ưu cho hệ thống."
slug: "xoa-li-su-thuc-thi-n8n-tren-mysql"
tags: [n8n, automation, mysql, database, cron, self-hosted]
keywords: [xóa lịch sử n8n, tự động hóa mysql, cron job n8n, giảm dung lượng lưu trữ, tối ưu hiệu suất n8n]
---

# 🚀 **Xóa Lịch Sử Thực Thi n8n Trên MySQL Tự Động - Giải Pháp Cho Các Sếp Quản Trị Hệ Thống**

### **Nỗi Đau Của Các Sếp Khi Quản Lý Lịch Sử Thực Thi n8n**
Khi hệ thống n8n của các sếp hoạt động liên tục trong nhiều tháng, lượng **lịch sử thực thi** (execution history) trên cơ sở dữ liệu MySQL sẽ ngày càng tăng. Điều này không chỉ **tăng dung lượng lưu trữ**, mà còn làm chậm tốc độ truy vấn và ảnh hưởng đến hiệu suất của workflows. Các sếp phải **thủ công xóa dữ liệu** hoặc lo lắng về việc hệ thống sẽ bị chậm hoặc ngừng hoạt động do không gian lưu trữ đầy.

**Workflow này giải quyết vấn đề này bằng cách:**
✅ **Xóa tự động** lịch sử thực thi cũ trên MySQL theo lịch trình (cron).
✅ **Giảm dung lượng lưu trữ** đáng kể, giúp hệ thống hoạt động nhanh hơn.
✅ **Không cần code**, chỉ cần cấu hình đơn giản trên n8n.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm không gian lưu trữ**: Giảm thiểu dung lượng MySQL, tránh tình trạng cơ sở dữ liệu bị đầy.
- **Tăng tốc độ truy vấn**: Hệ thống n8n hoạt động mượt mà hơn, không bị chậm do dữ liệu quá nhiều.
- **Duy trì hiệu suất ổn định**: Không cần lo lắng về việc xóa dữ liệu thủ công.
- **Tự động hóa hoàn toàn**: Chỉ cần bật cron, workflow sẽ tự động thực hiện định kỳ.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần:
1. **Tài khoản MySQL** có quyền truy cập và xóa dữ liệu từ bảng `n8n_executions`.
2. **n8n Self-hosted** (không thể chạy trên n8n.cloud vì không hỗ trợ cron).
3. **Tham số cron** (ví dụ: `0 0 * * *` để chạy hàng ngày lúc 00:00).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
```json
{
  "nodes": {
    "1": {
      "parameters": {},
      "name": "Cron",
      "type": "n8n-nodes-base.cron",
      "typeOptions": {
        "function": "executeQuery"
      }
    },
    "2": {
      "parameters": {
        "operation": "executeQuery",
        "query": "DELETE FROM n8n_executions WHERE createdAt < DATE_SUB(NOW(), INTERVAL 30 DAY)"
      },
      "name": "MySQL",
      "type": "n8n-nodes-base.mySql",
      "credentials": {
        "mySql": "mySql"
      }
    },
    "3": {
      "parameters": {},
      "name": "On clicking 'execute'",
      "type": "n8n-nodes-base.manualTrigger"
    }
  },
  "connections": {
    "main": [
      {
        "node": "1",
        "connection": "main",
        "port": "trigger"
      },
      {
        "node": "2",
        "connection": "main",
        "port": "trigger"
      },
      {
        "node": "3",
        "connection": "main",
        "port": "output"
      }
    ]
  }
}
```
**Hướng dẫn import:**
1. Mở **n8n Editor** → Nhấn **"Import"** → Chọn file JSON hoặc dán JSON trên.
2. Workflow sẽ tự động tạo 3 node: **Cron**, **MySQL**, và **Manual Trigger**.

---

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
##### **Node 1: Cron (n8n-nodes-base.cron)**
- **Cấu hình cron**:
  - Sử dụng **syntax cron** để xác định thời gian chạy (ví dụ: `0 0 * * *` = hàng ngày lúc 00:00).
  - **Không nên chạy quá thường xuyên** (ví dụ: hàng giờ) nếu bảng `n8n_executions` lớn, để tránh ảnh hưởng đến hiệu suất MySQL.
- **Lưu ý**:
  - Nếu sử dụng **n8n Self-hosted**, cron sẽ hoạt động 24/7.
  - Nếu sử dụng **n8n.cloud**, **không thể** sử dụng node cron (do không hỗ trợ).

##### **Node 2: MySQL (n8n-nodes-base.mySql)**
- **Tham số quan trọng**:
  - **Credentials**: Chọn **mySql** (đã cấu hình trước trong n8n).
  - **Operation**: Chọn **"executeQuery"**.
  - **Query**: Câu lệnh SQL để xóa dữ liệu cũ (ví dụ:
    ```sql
    DELETE FROM n8n_executions WHERE createdAt < DATE_SUB(NOW(), INTERVAL 30 DAY)
    ```
    - Thay đổi `30 DAY` thành số ngày phù hợp (ví dụ: `7 DAY` để xóa dữ liệu 7 ngày trước).
  - **Test query**: Trước khi chạy thực tế, các sếp nên **test query** trên MySQL để đảm bảo không xóa dữ liệu quan trọng.

##### **Node 3: Manual Trigger (n8n-nodes-base.manualTrigger)**
- **Dùng để test thủ công**:
  - Các sếp có thể nhấn **"Execute"** để chạy workflow một lần trước khi bật cron.

---

#### **3. Kích Hoạt ⚡️**
1. **Test run**:
   - Nhấn **"Execute"** trên node **Manual Trigger** để kiểm tra query MySQL có hoạt động đúng không.
   - Kiểm tra **log** trong MySQL để xác nhận dữ liệu đã được xóa.
2. **Bật Active workflow**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::note[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Lưu log xóa dữ liệu**:
   - Thêm node **Slack/Telegram** để thông báo khi workflow xóa dữ liệu thành công/thất bại.
   - Ví dụ:
     ```json
     {
       "name": "Notify Slack",
       "type": "n8n-nodes-base.slack",
       "parameters": {
         "message": "Workflow xóa lịch sử n8n thành công! Xóa {{ $node["MySQL"].json["affectedRows"] }} bản ghi."
       }
     }
     ```

2. **Xóa dữ liệu theo điều kiện cụ thể**:
   - Thay vì xóa tất cả dữ liệu cũ, các sếp có thể thêm điều kiện như:
     ```sql
     DELETE FROM n8n_executions WHERE createdAt < NOW() - INTERVAL 30 DAY AND status = 'finished'
     ```
     (Chỉ xóa những workflow đã hoàn thành).

3. **Dùng node **n8n-nodes-base.if** để kiểm tra trước khi xóa**:
   - Tránh xóa dữ liệu nếu bảng `n8n_executions` đang bị khóa hoặc có lỗi.

4. **Tự động tạo báo cáo**:
   - Thêm node **Google Sheets** hoặc **Email** để gửi báo cáo định kỳ về số lượng dữ liệu đã xóa.
:::

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa việc xóa lịch sử thực thi n8n**, giảm thiểu dung lượng lưu trữ và duy trì hiệu suất tối ưu cho hệ thống. **Không cần code**, chỉ cần cấu hình đơn giản và bật cron là xong!

**Hãy áp dụng ngay để hệ thống n8n của các sếp luôn hoạt động mượt mà!** 🚀

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::