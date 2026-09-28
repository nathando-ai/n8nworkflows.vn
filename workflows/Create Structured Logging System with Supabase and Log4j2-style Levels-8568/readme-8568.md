---
title: "🚀 Hệ Thống Log Hóa Cấu Trúc với Supabase & Log4j2 - Tự Động Hóa Log Cho n8n"
description: "Workflow này giúp các sếp tự động hóa việc ghi log cấu trúc (DEBUG, INFO, WARN, ERROR, FATAL) từ n8n vào cơ sở dữ liệu Supabase PostgreSQL, tối ưu cho việc theo dõi, debug và phân tích hiệu suất 24/7. Đặc biệt phù hợp cho DevOps, team tự động hóa và các dự án cần logging chuyên nghiệp."
slug: "he-thong-log-hoa-cau-truc-supabase-log4j2"
tags: [n8n, automation, devops, logging, supabase, no-code]
keywords: [n8n workflow logging, tự động hóa log cho n8n, supabase postgresql, log4j2 trong n8n, hệ thống log cấu trúc, devops automation]
---

# 🚀 **Hệ Thống Log Hóa Cấu Trúc với Supabase & Log4j2 - Giải Pháp Tự Động Hóa Log Cho n8n**

---

## **Tại sao các sếp cần hệ thống log hóa tự động?**
Hiện nay, khi các sếp xây dựng các workflow phức tạp trên **n8n**, việc theo dõi, debug và phân tích lỗi thủ công là một **đầu mối đau đầu**:
- **Thời gian mất nhiều**: Phải tra cứu log thủ công trên nhiều nơi (Slack, email, console).
- **Không thống nhất**: Logs phân tán, khó so sánh giữa các workflow.
- **Không linh hoạt**: Không thể lọc, phân tích hoặc báo cáo log theo thời gian thực.
- **Rủi ro mất dữ liệu**: Logs chỉ tồn tại tạm thời trên console, dễ bị xóa khi workflow kết thúc.

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✅ **Tự động hóa ghi log** từ mọi node trong workflow vào **Supabase PostgreSQL** (cơ sở dữ liệu cloud mạnh mẽ).
✅ **Cấu trúc log theo chuẩn Log4j2** (TRACE, DEBUG, INFO, WARN, ERROR, FATAL) để dễ dàng phân loại và phân tích.
✅ **Theo dõi toàn diện** mọi hoạt động của workflow, từ debug đến lỗi nghiêm trọng.
✅ **Dễ dàng truy xuất và báo cáo** thông qua **Supabase Dashboard** hoặc kết nối với **Tableau/Power BI**.

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian debug**: Logs được tự động lưu vào Supabase, các sếp chỉ cần truy xuất thay vì ghi chép thủ công.
- **Chính xác & toàn diện**: Mỗi log bao gồm **thông tin chi tiết** (node, execution ID, metadata) giúp phân tích lỗi hiệu quả.
- **Linh hoạt & mở rộng**: Dễ dàng kết nối với **Slack/Telegram** để thông báo lỗi thời gian thực.
- **Báo cáo tự động**: Sử dụng **Supabase SQL** hoặc **n8n** để tạo báo cáo log định kỳ.
- **An toàn & bảo mật**: Supabase cung cấp **tính năng bảo mật cao** (RBAC, encryption) cho dữ liệu logs.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Supabase**:
   - [Đăng ký miễn phí Supabase](https://supabase.com/) (đã hỗ trợ 500MB storage miễn phí).
   - **API Key** và **Project URL** (tìm trong **Project Settings** → **API**).

2. **Cấu trúc cơ sở dữ liệu Supabase**:
   - **Enumerated Type `log_level_type`** với giá trị: `TRACE`, `DEBUG`, `INFO`, `WARN`, `ERROR`, `FATAL`.
   - **Bảng `logs`** với các trường như sau:
     | Trường          | Kiểu dữ liệu          | Ghi chú                          |
     |------------------|-----------------------|----------------------------------|
     | `id`             | `bigserial` (PK)      | ID tự động sinh.                 |
     | `created_at`     | `timestamp`           | Thời gian ghi log (default: `now()`). |
     | `workflow_name`  | `text` (không nullable)| Tên workflow ghi log.            |
     | `node_name`      | `text` (không nullable)| Tên node thực hiện log.          |
     | `execution_id`   | `text` (không nullable)| ID của execution n8n.             |
     | `log_level`      | `log_level_type` (không nullable) | Mức độ log (TRACE, ERROR,...). |
     | `message`        | `text` (không nullable)| Nội dung log.                     |
     | `metadata`       | `jsonb`               | Thông tin bổ sung (optional).    |

   - **SQL để tạo cấu trúc** (nếu cần):
     ```sql
     -- Tạo enum type
     CREATE TYPE log_level_type AS ENUM ('TRACE', 'DEBUG', 'INFO', 'WARN', 'ERROR', 'FATAL');

     -- Tạo bảng logs
     CREATE TABLE logs (
       id BIGSERIAL PRIMARY KEY,
       created_at TIMESTAMPTZ DEFAULT NOW() NOT NULL,
       workflow_name TEXT NOT NULL,
       node_name TEXT NOT NULL,
       execution_id TEXT NOT NULL,
       log_level log_level_type NOT NULL,
       message TEXT NOT NULL,
       metadata JSONB
     );
     ```

3. **Credentials Supabase trong n8n**:
   - Tạo **credentials mới** trong n8n:
     - **Tên credentials**: `supabaseApi`
     - **Project URL**: `https://<project-ref>.supabase.co`
     - **API Key**: `your-supabase-anon-key` (tìm trong **Project Settings** → **API**).
     - **Database URL**: `postgresql://postgres:<password>@db.<project-ref>.supabase.co:5432/postgres`
     - **Database Password**: `<your-supabase-password>` (nếu sử dụng auth).

4. **Workflow phụ (Sub-Workflow)**:
   - Workflow này sử dụng **2 sub-workflow** để xử lý log theo mức độ (ví dụ: `Log Fatal` và `Log Info`).
   - Các sếp có thể **tạo mới** hoặc sử dụng sub-workflow đã có trong workflow chính.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow bằng **2 cách**:
- **Tải file JSON** từ [n8n.io/workflows/8568](https://n8n.io/workflows/8568) và import vào **n8n Editor**.
- **Copy/paste JSON** từ [đây](https://n8n.io/workflows/8568) vào **Import Workflow** trong n8n.

:::note[Lưu ý]
- **Không cần thay đổi cấu trúc** của workflow chính, chỉ cần **cấu hình credentials Supabase** và **sub-workflow**.
- **Test run** trước khi kích hoạt để đảm bảo kết nối Supabase hoạt động.
:::

---

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này bao gồm **7 node chính**, các sếp cần chú ý cấu hình sau:

##### **A. Node `Create Log` (Supabase)**
- **Credentials**: Chọn `supabaseApi` (đã tạo trước).
- **Query**:
  ```json
  {
    "insert": {
      "into": "logs",
      "columns": ["workflow_name", "node_name", "execution_id", "log_level", "message", "metadata"],
      "values": [
        {
          "workflow_name": "{{$json.workflow_name}}",
          "node_name": "{{$json.node_name}}",
          "execution_id": "{{$json.execution_id}}",
          "log_level": "{{$json.log_level}}",
          "message": "{{$json.message}}",
          "metadata": "{{$json.metadata}}"
        }
      ]
    }
  }
  ```
  - **Lưu ý**:
    - `$json.workflow_name` sẽ được truyền từ **node `When Log Traced`**.
    - `$json.log_level` phải là một trong `TRACE`, `DEBUG`, `INFO`, `WARN`, `ERROR`, `FATAL`.

##### **B. Node `Log Fatal` & `Log Info` (Code)**
- **Mục đích**: Xử lý log theo mức độ (ví dụ: `FATAL` sẽ gọi sub-workflow để thông báo lỗi).
- **Cấu trúc code mẫu**:
  ```javascript
  // Ví dụ cho node Log Fatal
  return {
    json: {
      workflow_name: "{{$input.currentNode.name}}",
      node_name: "{{$input.currentNode.name}}",
      execution_id: "{{$input.current.executionId}}",
      log_level: "FATAL",
      message: "Lỗi nghiêm trọng: {{$input.current.json.message}}",
      metadata: {
        error: "{{$input.current.json.error}}",
        stack: "{{$input.current.json.stack}}"
      }
    }
  };
  ```
  - **Lưu ý**:
    - Các sếp cần **điền nội dung log** phù hợp với từng node.
    - **Sub-workflow** sẽ được gọi từ node `Call Logger SubWorkflow 1` và `Call Logger SubWorkflow 2`.

##### **C. Node `Call Logger SubWorkflow 1` & `Call Logger SubWorkflow 2`**
- **Mục đích**: Gọi sub-workflow để xử lý log theo mức độ (ví dụ: `FATAL` sẽ gửi thông báo đến Slack/Telegram).
- **Cấu hình**:
  - **Workflow ID**: Điền ID của sub-workflow đã tạo.
  - **Data**: Truyền dữ liệu log từ node `Log Fatal`/`Log Info`.

##### **D. Node `Error Trigger`**
- **Mục đích**: Xử lý lỗi từ workflow chính.
- **Cấu hình**:
  - **Credentials**: Không cần (sử dụng mặc định).
  - **Lưu ý**: Node này sẽ tự động gọi `Log Fatal` khi có lỗi.

##### **E. Node `When Log Traced` (ExecuteWorkflowTrigger)**
- **Mục đích**: Khởi động workflow khi có log mới.
- **Lưu ý**:
  - Node này **không cần cấu hình thêm**, chỉ cần **bật Active**.

---

#### **3. Kích hoạt ⚡️**
1. **Test run** với dữ liệu mẫu:
   - Gửi một log mẫu từ **node `Log Info`** hoặc **node `Log Fatal`**.
   - Kiểm tra **Supabase Dashboard** (trang `Table Editor` → `logs`) để xác nhận log được lưu.
2. **Bật Active workflow**:
   - Sau khi test thành công, **bật Active** để workflow hoạt động liên tục.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết nối với Slack/Telegram**:
   - Tạo sub-workflow mới để **gửi thông báo lỗi** (ví dụ: `FATAL`) đến Slack/Telegram.
   - Sử dụng **node `webhook`** để gửi tin nhắn tự động.

2. **Lưu log vào file CSV/Excel**:
   - Sử dụng **node `file`** trong n8n để xuất log từ Supabase vào file định kỳ.

3. **Báo cáo log định kỳ**:
   - Tạo **workflow mới** để lấy dữ liệu từ Supabase và gửi báo cáo qua email (sử dụng **node `email`**).

4. **Phân tích log với Supabase SQL**:
   - Sử dụng **Supabase SQL Editor** để tạo query phân tích:
     ```sql
     -- Đếm số lượng lỗi ERROR trong 1 ngày
     SELECT log_level, COUNT(*) as count
     FROM logs
     WHERE created_at > NOW() - INTERVAL '1 day'
     GROUP BY log_level;
     ```

5. **Tự động xóa log cũ**:
   - Tạo **workflow cron** để xóa log cũ hơn 30 ngày:
     ```sql
     DELETE FROM logs WHERE created_at < NOW() - INTERVAL '30 days';
     ```

6. **Kết hợp với n8n Dashboard**:
   - Hiển thị **bảng điều khiển log** trong n8n Dashboard để theo dõi thời gian thực.
:::

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** để các sếp **tự động hóa logging** cho n8n, giúp:
✔ **Tiết kiệm thời gian debug** với logs cấu trúc hóa.
✔ **Theo dõi toàn diện** mọi hoạt động của workflow.
✔ **Mở rộng khả năng phân tích** với Supabase SQL.

**Hành động ngay!**
1. **Chuẩn bị Supabase** và cấu trúc cơ sở dữ liệu theo hướng dẫn.
2. **Import workflow** và cấu hình credentials.
3. **Test run** và kích hoạt để bắt đầu ghi log tự động.

👉 **Nếu cần hỗ trợ**, các sếp có thể liên hệ với tác giả [Elodie Tasia](https://n8n.io/workflows/8568) hoặc tham khảo [tài liệu chính thức n8n](https://docs.n8n.io/).

---
:::success[CHUYÊN GIA N8N CỦA TINOHOST]
👉 **Đăng ký VPS TinoHost** để tự động hóa workflow 24/7:
- [VPS N8N với mã giảm giá **VPSN8N**](https://tino.vn/vps-n8n?affid=388) (giảm tới 39%).
- [VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo ổn định).
:::

---
**Happy automating!** 🚀