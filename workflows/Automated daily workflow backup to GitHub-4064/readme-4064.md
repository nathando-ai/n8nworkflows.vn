---
title: "🚀 Tự Động Hoàn Chỉnh & Backup Workflow n8n Hàng Ngày Sang GitHub - Giảm Thiểu Rủi Ro & Tiết Kiệm Thời Gian"
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp tự động backup và cập nhật tất cả workflow n8n hàng ngày lên GitHub, đảm bảo an toàn dữ liệu và dễ dàng quản lý phiên bản. Giúp tránh mất mát dữ liệu khi có lỗi hoặc thay đổi cấu hình."
slug: "tự-dộng-hoàn-chỉnh-backup-workflow-n8n-sang-github"
tags: [n8n, automation, devops, backup, github, self-hosted]
keywords: [tự động hóa n8n, backup workflow n8n, tự động hóa devops, lưu trữ phiên bản workflow, tự động hóa hàng ngày]
---

# 🚀 **Tự Động Hoàn Chỉnh & Backup Workflow n8n Sang GitHub - Bảo Vệ Dữ Liệu & Quản Lý Phiên Bản Dễ Dàng**

### **🔥 Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Các sếp đã từng gặp phải tình huống nào sau đây chưa?
- **Mất dữ liệu workflow** do lỗi cấu hình, xóa nhầm hoặc hệ thống bị crash.
- **Không theo dõi được lịch sử thay đổi** của workflow, khiến việc rollback trở nên phức tạp.
- **Phải làm thủ công** việc backup workflow hàng ngày, tốn thời gian và dễ xảy ra sai sót.
- **Không có phiên bản backup** để phục hồi khi cần thiết, đặc biệt là khi làm việc trên môi trường self-hosted.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách tự động:**
✅ **Backup toàn bộ workflow n8n** hàng ngày lên GitHub.
✅ **Cập nhật phiên bản mới** nếu có thay đổi.
✅ **Kiểm tra và xử lý trùng lặp** để tránh mất dữ liệu.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **An toàn tuyệt đối**: Dữ liệu workflow được sao lưu hàng ngày, tránh mất mát do lỗi kỹ thuật.
- **Quản lý phiên bản dễ dàng**: Theo dõi lịch sử thay đổi và phục hồi phiên bản cũ nếu cần.
- **Tiết kiệm thời gian**: Không cần phải làm thủ công việc backup hàng ngày.
- **Tự động hóa hoàn chỉnh**: Workflow hoạt động liên tục, không phụ thuộc vào sự can thiệp của người dùng.
- **Dễ dàng chia sẻ và hợp tác**: Các sếp có thể chia sẻ workflow với team thông qua GitHub.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản GitHub** với quyền push vào một repository cụ thể.
   - **Credentials GitHub**: Tạo một **Personal Access Token (PAT)** với quyền `repo` (xem [hướng dẫn tạo PAT](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens)).
   :::
   ![Tạo PAT GitHub](https://docs.github.com/assets/cb-1677791e3e1d46b386f6c6f077707133.png)
   - **Repository GitHub**: Tạo một repo mới (ví dụ: `n8n-workflows-backup`) và chọn **Initialize with a README** (không bắt buộc).

2. **n8n Self-hosted** (không thể chạy trên n8n.cloud).
   - **Lưu ý**: Workflow này **không hoạt động** trên phiên bản n8n.cloud vì không có quyền truy cập vào API nội bộ của n8n.

3. **Tên file backup**: Workflow sẽ tự động đặt tên file theo định dạng `n8n-workflows-<ngày-tháng-năm>.json` (ví dụ: `n8n-workflows-2024-05-20.json`).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/4064) hoặc sao chép từ đây:
  ```json
  {
    "nodes": [
      {
        "parameters": {
          "functionCode": "return { cronTab: \"0 0 * * *\" }"
        },
        "name": "Schedule Trigger",
        "type": "n8n-nodes-base.scheduleTrigger",
        "typeVersion": 1,
        "position": [100, 300]
      },
      {
        "parameters": {
          "operation": "listWorkflows"
        },
        "name": "Retrieve workflows",
        "type": "n8n-nodes-base.n8n",
        "typeVersion": 1,
        "position": [300, 300]
      },
      {
        "parameters": {},
        "name": "Aggregate",
        "type": "n8n-nodes-base.aggregate",
        "typeVersion": 1,
        "position": [500, 300]
      },
      {
        "parameters": {
          "operation": "list",
          "resource": "file",
          "repository": "n8n-workflows-backup",
          "path": "/"
        },
        "name": "List files from repo",
        "type": "n8n-nodes-base.github",
        "typeVersion": 1,
        "position": [700, 300]
      },
      {
        "parameters": {
          "operation": "edit",
          "resource": "file",
          "repository": "n8n-workflows-backup",
          "path": "/n8n-workflows-{{ $node["Commit date & file name"].json["$"].date }}.json",
          "content": "{{ $json }}"
        },
        "name": "Update file",
        "type": "n8n-nodes-base.github",
        "typeVersion": 1,
        "position": [900, 500]
      },
      {
        "parameters": {
          "operation": "create",
          "resource": "file",
          "repository": "n8n-workflows-backup",
          "path": "/n8n-workflows-{{ $node["Commit date & file name"].json["$"].date }}.json",
          "content": "{{ $json }}"
        },
        "name": "Upload file",
        "type": "n8n-nodes-base.github",
        "typeVersion": 1,
        "position": [900, 300]
      },
      {
        "parameters": {
          "resource": "file",
          "operation": "list",
          "repository": "n8n-workflows-backup",
          "path": "/",
          "condition": {
            "propertyName": "name",
            "operator": "equals",
            "values": ["n8n-workflows-{{ $node["Commit date & file name"].json["$"].date }}.json"]
          }
        },
        "name": "Check if file exists",
        "type": "n8n-nodes-base.if",
        "typeVersion": 1,
        "position": [700, 500]
      },
      {
        "parameters": {
          "operation": "toJson",
          "data": "{{ $json }}"
        },
        "name": "Json file",
        "type": "n8n-nodes-base.convertToFile",
        "typeVersion": 1,
        "position": [500, 500]
      },
      {
        "parameters": {
          "operation": "binaryToProperty",
          "propertyName": "json",
          "filePropertyName": "file"
        },
        "name": "To base64",
        "type": "n8n-nodes-base.extractFromFile",
        "typeVersion": 1,
        "position": [300, 500]
      },
      {
        "parameters": {
          "values": [
            {
              "propertyName": "date",
              "value": "{{ $node[\"Retrieve workflows\"].json[\"$\"].timestamp | date(\"YYYY-MM-DD\") }}"
            }
          ]
        },
        "name": "Commit date & file name",
        "type": "n8n-nodes-base.set",
        "typeVersion": 1,
        "position": [100, 500]
      }
    ],
    "connections": {
      "Schedule Trigger": {
        "main": [
          [
            {
              "node": "Retrieve workflows",
              "connection": "main"
            }
          ]
        ]
      },
      "Retrieve workflows": {
        "main": [
          [
            {
              "node": "Aggregate",
              "connection": "main"
            }
          ]
        ]
      },
      "Aggregate": {
        "main": [
          [
            {
              "node": "Json file",
              "connection": "main"
            }
          ]
        ]
      },
      "Json file": {
        "main": [
          [
            {
              "node": "To base64",
              "connection": "main"
            }
          ]
        ]
      },
      "To base64": {
        "main": [
          [
            {
              "node": "Commit date & file name",
              "connection": "main"
            }
          ]
        ]
      },
      "Commit date & file name": {
        "main": [
          [
            {
              "node": "List files from repo",
              "connection": "main"
            }
          ]
        ]
      },
      "List files from repo": {
        "main": [
          [
            {
              "node": "Check if file exists",
              "connection": "main"
            }
          ]
        ]
      },
      "Check if file exists": {
        "iftrue": [
          [
            {
              "node": "Update file",
              "connection": "main"
            }
          ]
        ],
        "iffalse": [
          [
            {
              "node": "Upload file",
              "connection": "main"
            }
          ]
        ]
      }
    }
  }
  ```
  - **Cách import**:
    1. Mở **n8n Editor** → Nhấn **Import** → Chọn **Paste JSON**.
    2. Dán JSON trên và nhấn **Import**.

---

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Sau khi import, các sếp cần **cấu hình chi tiết** các node quan trọng:

##### **🔹 Node "Schedule Trigger"**
- **Cấu hình lịch chạy**:
  - Mặc định là `0 0 * * *` (chạy hàng ngày lúc 00:00).
  - Các sếp có thể thay đổi theo nhu cầu (ví dụ: `0 12 * * *` để chạy vào giờ làm việc).

##### **🔹 Node "Retrieve workflows" (n8n)**
- **Không cần cấu hình thêm**, vì nó tự động lấy tất cả workflow từ n8n self-hosted.

##### **🔹 Node "List files from repo" (GitHub)**
- **Cấu hình**:
  - **Repository**: Điền tên repo GitHub (`n8n-workflows-backup`).
  - **Path**: Đặt là `/` (để danh sách tất cả file trong root).
  - **Credentials**: Chọn **Personal Access Token (PAT)** đã tạo trước đó.

##### **🔹 Node "Update file" & "Upload file" (GitHub)**
- **Cấu hình chung**:
  - **Repository**: Điền tên repo (`n8n-workflows-backup`).
  - **Path**: Sử dụng định dạng `n8n-workflows-{{ $node["Commit date & file name"].json["$"].date }}.json`.
    - Ví dụ: `n8n-workflows-2024-05-20.json`.
  - **Content**: Sử dụng `{{ $json }}` (tự động lấy từ node `Json file`).
  - **Credentials**: Chọn **PAT** tương tự như node `List files from repo`.

##### **🔹 Node "Check if file exists" (If)**
- **Không cần cấu hình thêm**, vì nó tự động kiểm tra file đã tồn tại hay chưa.

##### **🔹 Node "Commit date & file name" (Set)**
- **Không cần cấu hình thêm**, vì nó tự động lấy ngày tháng năm hiện tại.

##### **🔹 Node "Json file" (ConvertToFile)**
- **Không cần cấu hình thêm**, vì nó tự động chuyển dữ liệu workflow thành file JSON.

##### **🔹 Node "To base64" (ExtractFromFile)**
- **Không cần cấu hình thêm**, vì nó tự động chuyển file thành định dạng base64 để GitHub xử lý.

---

#### **3. Kích Hoạt ⚡️**
1. **Test run** với dữ liệu mẫu:
   - Nhấn **Run Workflow** để kiểm tra nếu workflow chạy đúng.
   - Kiểm tra **GitHub repo** xem file đã được tạo/ cập nhật chưa.

2. **Bật Active**:
   - Sau khi test thành công, chuyển trạng thái workflow sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Gửi thông báo Slack/Email khi backup thành công/lỗi**:
   - Sử dụng node **Slack** hoặc **Email** để thông báo kết quả backup hàng ngày.
   - Ví dụ: `"Backup workflow n8n thành công vào ngày {{ $node["Commit date & file name"].json["$"].date }}!"`

2. **Lưu log hoạt động**:
   - Sử dụng node **StickyNote** hoặc **Google Sheets** để ghi lại lịch sử backup (ngày giờ, trạng thái thành công/thất bại).

3. **Tự động xóa file cũ**:
   - Thêm node **GitHub Delete File** để xóa file backup cũ sau 30 ngày (để tránh repo bị quá tải).

4. **Kết hợp với CI/CD**:
   - Nếu các sếp sử dụng GitHub Actions, có thể tự động **deploy workflow** từ repo backup vào môi trường staging/production.

5. **Backup nhiều lần trong ngày**:
   - Thay đổi `cronTab` trong node **Schedule Trigger** để backup nhiều lần (ví dụ: `0 */6 * * *` để backup hàng giờ).
:::

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn chỉnh** để các sếp tự động hóa việc backup và quản lý phiên bản workflow n8n hàng ngày. Với chỉ vài bước cấu hình, các sếp sẽ:
✔ **Tránh mất mát dữ liệu** do lỗi hoặc xóa nhầm.
✔ **Dễ dàng phục hồi phiên bản cũ** nếu cần.
✔ **Tiết kiệm thời gian** và tập trung vào công việc quan trọng hơn.

**🚀 Hãy áp dụng ngay workflow này và bảo vệ dữ liệu của mình!**

---
:::info