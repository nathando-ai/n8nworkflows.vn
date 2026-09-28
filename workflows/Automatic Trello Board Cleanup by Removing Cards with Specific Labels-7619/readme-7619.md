---
title: "🧹 **Tự Động Xóa Bảng Trello Sạch Sẽ: Xóa Thẻ "Đã Đánh Dấu Xóa" Với n8n (Không Cần Code!)**"
description: "Giải pháp tự động hóa hoàn toàn tự động xóa các thẻ Trello có nhãn 'Mark for Deletion' (Đã đánh dấu xóa), giúp các sếp tiết kiệm thời gian quản lý bảng và duy trì sự sạch sẽ của công việc. Hoạt động liên tục 24/7, không cần can thiệp thủ công."
slug: "tieu-dong-xoa-thanh-to-trello-nhan-mark-for-deletion"
tags: [n8n, trello, automation, no-code, project-management]
keywords: [tự động hóa trello, xóa thẻ trello tự động, n8n workflow trello, quản lý dự án tự động, xóa nhãn mark for deletion]
---

# 🚀 **Tự Động Xóa Thẻ Trello Có Nhãn "Đã Đánh Dấu Xóa" – Giải Pháp Tiết Kiệm Thời Gian Cho Quản Lý Dự Án**

---

## **🔍 Nỗi Đau Thực Tế Của Các Sếp**
Quản lý một bảng Trello với hàng trăm thẻ, các sếp thường phải **tìm kiếm và xóa thủ công** các thẻ đã cũ, không cần thiết, hoặc có nhãn **"Mark for Deletion"** (Đã đánh dấu xóa). Đây là công việc **lặp đi lặp lại, tốn thời gian và dễ gây lỗi** nếu không kiểm tra kỹ. Hơn nữa, khi bảng Trello trở nên rối loạn, hiệu suất làm việc của cả đội nhóm sẽ bị ảnh hưởng.

**Giải pháp của n8n?**
Một **workflow tự động hóa hoàn toàn** sẽ:
✅ **Quét tất cả thẻ** trên bảng Trello của bạn.
✅ **Xác định và xóa** các thẻ có nhãn **"Mark for Deletion"** (hoặc nhãn tùy chỉnh khác).
✅ **Hoạt động liên tục 24/7**, không cần can thiệp thủ công.
✅ **Giảm thiểu rủi ro sai sót** so với việc xóa thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này **chạy ổn định 24/7**, các sếp nên cài đặt n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính liên tục và bảo mật.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ và ổn định)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải quét và xóa thẻ thủ công hàng tuần/month.
- **Duy trì bảng Trello sạch sẽ**: Giúp các thành viên dễ dàng theo dõi công việc quan trọng.
- **Giảm thiểu rủi ro**: Tránh xóa nhầm thẻ quan trọng do lỗi thủ công.
- **Hoạt động tự động**: Workflow chạy định kỳ (hoặc khi kích hoạt) mà không cần can thiệp.
- **Tùy chỉnh linh hoạt**: Có thể thay đổi nhãn cần xóa theo nhu cầu dự án.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Trello** và **API Key + Token** của Trello (xem hướng dẫn dưới đây).
2. **Bảng Trello** muốn tự động xóa thẻ (cần biết **URL của bảng**).
3. **Nhãn "Mark for Deletion"** (hoặc nhãn tùy chỉnh khác) được sử dụng để đánh dấu thẻ cần xóa.
4. **n8n Workflow Editor** (cài đặt trên máy hoặc VPS).

---
:::info[CHUẨN BỊ]
**Cách lấy API Key và Token Trello:**
1. Truy cập [Trello Developer Portal](https://trello.com/app-key).
2. Nhấp vào **"Get an API key"** để lấy **API Key**.
3. Sau đó, tạo **Token** từ cùng trang (điền **Callback URL** là `https://n8n.io`).
4. Trong n8n, đi đến **Credentials → New → Trello API**, nhập **API Key** và **Token**, sau đó lưu.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ **file JSON** hoặc **copy/paste JSON** vào n8n Editor.

**Bước 1:** Tải file JSON từ [n8n Workflow Official](https://n8n.io/workflows/7619) hoặc sử dụng mã JSON dưới đây:
```json
{
  "nodes": [
    {
      "parameters": {},
      "name": "When clicking ‘Execute workflow’",
      "type": "n8n-nodes-base.manualTrigger",
      "typeVersion": 1,
      "position": [250, 300]
    },
    {
      "parameters": {
        "operation": "get",
        "resource": "board",
        "board": {
          "id": "board_id_here" // Thay bằng ID bảng Trello
        }
      },
      "name": "Get Board4",
      "type": "n8n-nodes-base.trello",
      "typeVersion": 1,
      "credentials": {
        "trelloApi": "your_trello_credentials"
      },
      "position": [250, 500]
    },
    {
      "parameters": {
        "operation": "getAll",
        "resource": "list",
        "board": {
          "id": "board_id_here" // Thay bằng ID bảng Trello
        }
      },
      "name": "Get Lists4",
      "type": "n8n-nodes-base.trello",
      "typeVersion": 1,
      "credentials": {
        "trelloApi": "your_trello_credentials"
      },
      "position": [250, 700]
    },
    {
      "parameters": {
        "operation": "getCards",
        "resource": "list",
        "list": {
          "id": "list_id_here" // Thay bằng ID danh sách (nếu cần)
        },
        "board": {
          "id": "board_id_here" // Thay bằng ID bảng Trello
        }
      },
      "name": "Get Cards4",
      "type": "n8n-nodes-base.trello",
      "typeVersion": 1,
      "credentials": {
        "trelloApi": "your_trello_credentials"
      },
      "position": [250, 900]
    },
    {
      "parameters": {
        "operation": "delete",
        "card": {
          "id": "card_id"
        }
      },
      "name": "Delete a card",
      "type": "n8n-nodes-base.trello",
      "typeVersion": 1,
      "credentials": {
        "trelloApi": "your_trello_credentials"
      },
      "position": [650, 1100]
    },
    {
      "parameters": {
        "property": "labels"
      },
      "name": "Split Labels",
      "type": "n8n-nodes-base.splitOut",
      "typeVersion": 1,
      "position": [450, 900]
    },
    {
      "parameters": {
        "resource": "json",
        "operation": "filter",
        "filterExpression": "$.name === 'Mark for Deletion'" // Thay đổi nhãn cần xóa
      },
      "name": "Filter Marked for Delete",
      "type": "n8n-nodes-base.filter",
      "typeVersion": 1,
      "position": [450, 1100]
    }
  ],
  "connections": {
    "manualTrigger": {
      "main": [
        [
          {
            "node": "Get Board4",
            "connectionIndex": 0
          }
        ]
      ]
    },
    "Get Board4": {
      "main": [
        [
          {
            "node": "Get Lists4",
            "connectionIndex": 0
          }
        ]
      ]
    },
    "Get Lists4": {
      "main": [
        [
          {
            "node": "Get Cards4",
            "connectionIndex": 0
          }
        ]
      ]
    },
    "Get Cards4": {
      "main": [
        [
          {
            "node": "Split Labels",
            "connectionIndex": 0
          }
        ]
      ],
      "labels": [
        [
          {
            "node": "Filter Marked for Delete",
            "connectionIndex": 0
          }
        ]
      ]
    },
    "Filter Marked for Delete": {
      "main": [
        [
          {
            "node": "Delete a card",
            "connectionIndex": 0
          }
        ]
      ]
    }
  }
}
```

**Bước 2:** Import vào n8n bằng cách:
- Nhấp vào **"Import"** trong n8n Editor.
- Chọn file JSON hoặc **copy/paste** mã JSON vào ô **"Import Workflow"**.

---

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Sau khi import, các sếp cần **cấu hình chính xác** các node sau:

##### **🔹 Node "Get Board4" (Lấy Bảng Trello)**
- **Tham số quan trọng:**
  - **Resource: Board** → Chọn **"URL"** và nhập **URL của bảng Trello** (ví dụ: `https://trello.com/b/DCpuJbnd/administrative-tasks`).
  - Sau khi chạy, node sẽ tự động lấy **ID của bảng** (sử dụng cho các node sau).

##### **🔹 Node "Get Lists4" (Lấy Danh Sách)**
- **Tham số cần thiết:**
  - **Board ID** → Sử dụng **ID bảng** được lấy từ node **"Get Board4"**.

##### **🔹 Node "Get Cards4" (Lấy Thẻ)**
- **Tham số cần thiết:**
  - **Board ID** → Sử dụng **ID bảng** từ node **"Get Board4"**.
  - **List ID** (nếu cần): Nếu muốn lấy thẻ từ danh sách cụ thể, nhập **ID danh sách** (có thể bỏ trống để lấy tất cả danh sách).

##### **🔹 Node "Filter Marked for Delete" (Lọc Thẻ Có Nhãn)**
- **Tham số cần chỉnh:**
  - **Filter Expression**: Thay đổi `"$.name === 'Mark for Deletion'"` thành **nhãn tùy chỉnh** của bạn (ví dụ: `"$.name === 'Archive'"`).
  - **Lưu ý:** Nếu nhãn có dấu cách, sử dụng **khoá đơn** (`"`) hoặc **trích dẫn kép** (`"`).

##### **🔹 Node "Delete a card" (Xóa Thẻ)**
- **Tham số tự động:**
  - Node này sẽ **xóa thẻ** có ID từ node **"Filter Marked for Delete"**.
  - **Không cần chỉnh** nếu cấu hình các node trước đúng.

---

#### **3. Kích Hoạt ⚡️**
- **Test Run (Kiểm Tra):**
  - Nhấp vào **"Execute Workflow"** để chạy thử với **1-2 thẻ mẫu**.
  - Kiểm tra **log** để đảm bảo workflow xóa đúng thẻ có nhãn **"Mark for Deletion"**.
- **Bật Active:**
  - Sau khi kiểm tra thành công, **bật "Active"** để workflow chạy tự động khi kích hoạt.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự động chạy định kỳ:**
   - Sử dụng **n8n Cron Trigger** để chạy workflow hàng tuần/tháng (ví dụ: `0 0 * * 0` để chạy vào Chủ Nhật 00:00).
   - **Cách thêm:** `n8n-nodes-base.cron` → Chọn **Schedule** và nhập biểu thức cron.

2. **Gửi thông báo khi xóa thành công:**
   - Thêm **Slack/Telegram Notification** sau node **"Delete a card"** để được báo khi workflow hoàn thành.
   - **Node cần thêm:** `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram`.

3. **Lưu log hoạt động:**
   - Thêm **Google Sheets/Notion** để ghi lại lịch sử thẻ đã xóa.
   - **Node cần thêm:** `n8n-nodes-base.googleSheets` hoặc `n8n-nodes-base.notion`.

4. **Tùy chỉnh nhãn:**
   - Nếu muốn xóa thẻ có **nhiều nhãn khác nhau**, chỉnh sửa **Filter Expression** thành:
     ```json
     "$.name === 'Mark for Deletion' || $.name === 'Archive' || $.name === 'Old'"
     ```

5. **Xóa thẻ cũ hơn 30 ngày:**
   - Thêm **node "Date Filter"** (sử dụng `n8n-nodes-base.filter`) để chỉ xóa thẻ có ngày tạo **trước 30 ngày**.

---

### 📌 **Kết Luận**
**Tự động hóa xóa thẻ Trello với nhãn "Đã đánh dấu xóa" không chỉ tiết kiệm thời gian mà còn giúp các sếp duy trì **sự sạch sẽ và hiệu quả** trong quản lý dự án.** Bằng cách sử dụng n8n, các sếp không cần **code hay kiến thức kỹ thuật sâu**, chỉ cần **cấu hình vài bước đơn giản** là có thể tự động hóa công việc lặp đi lặp lại này.

**🚀 Hành động ngay:**
1. **Cài đặt n8n** trên VPS (nếu chưa có).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Active** và **quên đi công việc xóa thẻ thủ công**!

---
**💡 Cần hỗ trợ?**
- Liên hệ với tác giả: [Robert Breen](https://www.linkedin.com/in/robert-breen-29429625/) hoặc [ynteractive.com](https://ynteractive.com).
- **Hỏi đáp cộng đồng n8n:** [n8n Community](https://community.n8n.io/).