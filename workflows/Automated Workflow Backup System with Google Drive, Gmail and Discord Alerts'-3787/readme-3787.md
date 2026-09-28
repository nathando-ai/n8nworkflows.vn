---
title: "🚀 Hệ thống sao lưu tự động workflow n8n lên Google Drive + Cảnh báo Gmail & Discord"
description: "Tự động sao lưu toàn bộ workflow n8n lên Google Drive, đồng thời gửi email và thông báo Discord khi sao lưu thành công hoặc thất bại."
slug: "he-thong-sao-luu-workflow-n8n-google-drive-discord"
tags: [n8n, automation, no-code, backup, google-drive, discord, gmail]
keywords: [n8n workflow, sao lưu workflow, tự động hóa, Google Drive backup, Discord alerts]
---

# 🚀 Hệ thống sao lưu tự động workflow n8n lên Google Drive + Cảnh báo Gmail & Discord

Bạn đã từng mất một workflow quan trọng vì lỗi hệ thống, quên sao lưu, hay chỉ đơn giản là không có thời gian để thực hiện sao lưu thủ công?  
Việc sao lưu định kỳ, lưu trữ an toàn và nhận thông báo ngay khi có sự cố là nhu cầu thiết yếu của mọi **sếp** đang vận hành n8n ở quy mô vừa và lớn.  

Workflow này giải quyết 100% vấn đề trên mà **không cần viết một dòng code nào**:  
- Lấy danh sách tất cả workflow hiện có trong n8n.  
- Chuyển đổi mỗi workflow thành file JSON và lưu lên Google Drive (cập nhật nếu đã tồn tại).  
- Gửi email báo cáo kết quả (thành công / thất bại) qua Gmail.  
- Đẩy thông báo nhanh lên Discord để **sếp** luôn nắm ngay tình hình.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Không còn phải sao lưu thủ công mỗi tuần.  
- **Đảm bảo an toàn**: Tất cả workflow được lưu trữ trên Google Drive, có thể khôi phục ngay.  
- **Thông báo tức thời**: Email + Discord giúp sếp luôn biết trạng thái sao lưu.  
- **Hoạt động liên tục**: Được kích hoạt tự động theo lịch, không gián đoạn.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **n8n** (đã cài và chạy).  
- **Google Drive OAuth2 API** credentials (để ghi/đọc file).  
- **Gmail OAuth2** credentials (để gửi email).  
- **Discord Bot API** token và ID kênh (để gửi tin nhắn).  
- **Google Drive folder URL** (thư mục sẽ lưu các file backup).  
- Quyền **Read/Write** trên thư mục Google Drive đã chọn.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow (được cung cấp ở cuối README) hoặc sao chép toàn bộ JSON.  
2. Vào **n8n Editor → Import** → Dán JSON → **Import**.  
3. Đặt tên cho workflow (mặc định: *Automated Workflow Backup System*).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là danh sách **node** quan trọng và các tham số cần cấu hình:

| Node | Loại | Cấu hình cần chỉnh |
|------|------|-------------------|
| **Schedule Trigger** | scheduleTrigger | Chọn tần suất (ví dụ: `Every day at 02:00 AM`). |
| **Get all n8n Workflows** | n8n | **Credentials**: `n8nApi` (điền URL và API Key của n8n). |
| **Backup to Google Drive2** | googleDrive (operation **update**) | **Credentials**: `googleDriveOAuth2Api`. <br> **File ID**: Để trống (sẽ được xác định trong luồng). |
| **Loop Over Items** | splitInBatches | **Batch Size**: `10` (hoặc tùy nhu cầu). |
| **Backup to Google Drive4** | googleDrive (operation **upload**) | **Credentials**: `googleDriveOAuth2Api`. <br> **Folder**: Đường dẫn thư mục Google Drive (được truyền từ node *Parameters*). |
| **ifDriveEmpty** | if | Kiểm tra xem file đã tồn tại trên Drive chưa → **Condition**: `{{ $json["exists"] === false }}`. |
| **firstWorkflowJson** | set | Đặt biến `fileName` = `{{ $json["name"] }}.json`. |
| **JsonToFile** | code | Script chuyển JSON workflow thành Blob/File. Không cần chỉnh sửa. |
| **CodeJsonToFile1** | code | Tương tự, dùng để tạo file tạm. |
| **Limit** | limit | Giới hạn số workflow được backup mỗi lần (mặc định `100`). |
| **Workflow Data** | executionData | Lấy dữ liệu chi tiết của workflow hiện tại. |
| **successEmail** | gmail | **Credentials**: `gmailOAuth2`. <br> **To**: Địa chỉ email nhận báo cáo thành công. <br> **Subject**: `✅ Backup workflow thành công`. |
| **failureEmail** | gmail | **Credentials**: `gmailOAuth2`. <br> **To**: Địa chỉ email nhận báo cáo lỗi. <br> **Subject**: `❌ Backup workflow thất bại`. |
| **getDriveFileData** | googleDrive (resource **fileFolder**) | **Credentials**: `googleDriveOAuth2Api`. <br> **Folder ID**: Lấy từ node *Parameters*. |
| **When Executed by Another Workflow** | executeWorkflowTrigger | Để workflow có thể được gọi từ workflow khác (không bắt buộc). |
| **Execute Workflow** | executeWorkflow | Nếu muốn trigger backup từ workflow khác, cấu hình ID workflow ở đây. |
| **Parameters** | set | **folderUrl**: URL của thư mục Google Drive nơi lưu backup. |
| **Discord** | discord (resource **message**) | **Credentials**: `discordBotApi`. <br> **Channel ID**: ID kênh Discord nhận thông báo. <br> **Message**: Nội dung thông báo (thành công/ thất bại). |

> **Lưu ý:** Sau khi import, **đừng quên** cập nhật **Credentials** cho các node Google Drive, Gmail và Discord. Nếu không, workflow sẽ dừng ở bước đầu tiên.

#### 3. Kích hoạt ⚡️
1. Nhấn **Save** → **Activate** workflow.  
2. Chạy **Test** một lần với dữ liệu mẫu (có thể tạm thời giảm tần suất schedule để kiểm tra nhanh).  
3. Kiểm tra:
   - File JSON đã xuất hiện trong Google Drive.  
   - Email báo cáo (thành công hoặc thất bại) đã tới hộp thư.  
   - Tin nhắn Discord đã hiện ra trong kênh đã chỉ định.  

Nếu mọi thứ ổn, workflow đã sẵn sàng chạy tự động theo lịch đã định.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm Slack**: Dùng node *Slack* để gửi thông báo song song với Discord.  
- **Lưu log chi tiết**: Kết nối node *Google Sheets* để ghi log mỗi lần backup (ngày, số workflow, trạng thái).  
- **Backup định kỳ toàn bộ dữ liệu n8n**: Thêm node *Execute Workflow* để gọi workflow sao lưu database (PostgreSQL, MySQL).  
- **Thông báo lỗi chi tiết**: Sử dụng node *Code* để trích xuất thông báo lỗi và đính kèm log trong email.  

### 📌 Kết luận
Với **Automated Workflow Backup System**, các sếp sẽ không còn lo lắng về mất mát dữ liệu workflow, đồng thời nhận được báo cáo nhanh chóng qua email và Discord. Hãy **import ngay**, **cấu hình credentials**, và **bật activation** để bảo vệ tài sản tự động hoá của mình ngay hôm nay!  

---

## 📥 File JSON workflow (để import)

```json
{
  "nodes": [
    {
      "parameters": {
        "cronExpression": "0 2 * * *"
      },
      "name": "Schedule Trigger",
      "type": "n8n-nodes-base.scheduleTrigger",
      "typeVersion": 1,
      "position": [250, 300]
    },
    {
      "parameters": {},
      "name": "Get all n8n Workflows",
      "type": "n8n-nodes-base.n8n",
      "typeVersion": 1,
      "credentials": {
        "n8nApi": "n8nApi"
      },
      "position": [450, 300]
    },
    {
      "parameters": {
        "operation": "update"
      },
      "name": "Backup to Google Drive2",
      "type": "n8n-nodes-base.googleDrive",
      "typeVersion": 1,
      "credentials": {
        "googleDriveOAuth2Api": "googleDriveOAuth2Api"
      },
      "position": [650, 300]
    },
    {
      "parameters": {
        "batchSize": 10
      },
      "name": "Loop Over Items",
      "type": "n8n-nodes-base.splitInBatches",
      "typeVersion": 1,
      "position": [850, 300]
    },
    {
      "parameters": {},
      "name": "Backup to Google Drive4",
      "type": "n8n-nodes-base.googleDrive",
      "typeVersion": 1,
      "credentials": {
        "googleDriveOAuth2Api": "googleDriveOAuth2Api"
      },
      "position": [1050, 300]
    },
    {
      "parameters": {
        "conditions": {
          "boolean": [
            {
              "value1": "={{ $json[\"exists\"] === false }}",
              "operation": "equal"
            }
          ]
        }
      },
      "name": "ifDriveEmpty",
      "type": "n8n-nodes-base.if",
      "typeVersion": 1,
      "position": [1250, 300]
    },
    {
      "parameters": {
        "values": {
          "string": [
            {
              "name": "fileName",
              "value": "={{ $json[\"name\"] + \".json\" }}"
            }
          ]
        },
        "options": {}
      },
      "name": "firstWorkflowJson",
      "type": "n8n-nodes-base.set",
      "typeVersion": 1,
      "position": [1450, 300]
    },
    {
      "parameters": {
        "functionCode": "const json = items[0].json;\nreturn [{ json: { data: JSON.stringify(json, null, 2) } }];"
      },
      "name": "JsonToFile",
      "type": "n8n-nodes-base.code",
      "typeVersion": 1,
      "position": [1650, 300]
    },
    {
      "parameters": {
        "functionCode": "return items.map(item => ({ binary: { file: { data: Buffer.from(item.json.data), mimeType: 'application/json', fileName: $node[\"firstWorkflowJson\"].json[\"fileName\"] } } }));"
      },
      "name": "CodeJsonToFile1",
      "type": "n8n-nodes-base.code",
      "typeVersion": 1,
      "position": [1850, 300]
    },
    {
      "parameters": {
        "limit": 100
      },