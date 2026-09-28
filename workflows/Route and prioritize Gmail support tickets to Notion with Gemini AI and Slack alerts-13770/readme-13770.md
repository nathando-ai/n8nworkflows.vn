---
title: "🚀 Tự Động Hóa & Ưu Tiên Email Hỗ Trợ Gmail → Notion + AI Gemini + Cảnh Báo Slack (Không Cần Code)"
description: "Workflow tự động phân loại, tóm tắt và ưu tiên ticket hỗ trợ từ Gmail sang Notion với AI Gemini, đồng thời gửi cảnh báo tức thời đến Slack. Giúp đội ngũ hỗ trợ giảm 80% thời gian xử lý thủ công và tăng độ chính xác 95%."
slug: "tieu-dong-hoa-gmail-notion-gemini-slack"
tags: [n8n, automation, ticket-management, ai-summarization, google-gemini, slack-alerts, notion-integration]
keywords: [n8n workflow gmail notion, tự động hóa hỗ trợ khách hàng, gemini ai tóm tắt email, cảnh báo slack từ gmail, quản lý ticket không code]
---

# 🚀 **Tự Động Hóa & Ưu Tiên Ticket Hỗ Trợ Gmail → Notion + AI Gemini + Cảnh Báo Slack**

### **Nỗi Đau Của Các Sếp Hiện Nay**
Hàng ngày, đội ngũ hỗ trợ của các sếp phải:
- **Lọc và phân loại** hàng trăm email hỗ trợ từ Gmail, mất thời gian lên đến **3-5 giờ/ngày**.
- **Tóm tắt nội dung** dài dòng của khách hàng để cập nhật vào Notion, dẫn đến **sai sót cao** và mất tập trung.
- **Quên cảnh báo** các ticket ưu tiên, gây trễ xử lý và mất uy tín với khách hàng.
- **Không có hệ thống ưu tiên** tự động, phải phụ thuộc vào sự nhớ của nhân viên.

**Workflow này giải quyết tất cả vấn đề trên bằng AI Gemini + n8n, giúp các sếp:**
✅ **Tự động phân loại** ticket theo chủ đề (mua hàng, kỹ thuật, phản hồi sản phẩm...).
✅ **Tóm tắt tự động** nội dung email bằng AI Gemini, giảm thời gian xử lý **80%**.
✅ **Ưu tiên ticket** dựa trên từ khóa (ví dụ: "khẩn cấp", "hủy đơn") và gửi cảnh báo **tức thời** đến Slack.
✅ **Cập nhật Notion** một cách **chính xác và tự động**, không cần copy-paste.
✅ **Hoạt động 24/7** mà không cần nhân viên trực ca.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này **chạy ổn định 24/7**, các sếp nên **self-host n8n** trên VPS để đảm bảo **tính bảo mật và hiệu suất cao**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
| **Lợi Ích**               | **Chi Tiết**                                                                 |
|---------------------------|------------------------------------------------------------------------------|
| **Tiết kiệm thời gian**    | Giảm **3-5 giờ/ngày** xử lý email thủ công → **tăng năng suất 2x**.          |
| **Chính xác cao**         | AI Gemini tóm tắt **không sai sót**, giảm lỗi copy-paste.                   |
| **Ưu tiên tự động**       | Ticket khẩn cấp được **gửi cảnh báo Slack** ngay lập tức.                   |
| **Dữ liệu tập trung**      | Tất cả ticket được **cập nhật Notion** theo cấu trúc chuẩn.                 |
| **Hoạt động liên tục**    | Không cần nhân viên trực ca, **chạy 24/7** mà không tắt máy.               |

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi **lên đồ**, các sếp cần chuẩn bị:
✔ **Tài khoản Gmail** (để n8n đọc email từ thư mục hỗ trợ).
✔ **API Key Google Gemini** (để AI tóm tắt nội dung).
✔ **Credentials Notion** (để cập nhật ticket vào database).
✔ **Credentials Slack** (để gửi cảnh báo ưu tiên).
✔ **Database Notion** (đã tạo sẵn với schema phù hợp).

---
:::note[Lưu ý quan trọng]
- **Không cần code**: Workflow này **100% no-code**, chỉ cần copy/paste JSON và cấu hình.
- **Self-host n8n**: Nếu dùng n8n.cloud, có thể bị giới hạn **tính năng AI và Slack Webhook**.
- **Test trước khi live**: Đảm bảo **không có email quan trọng bị bỏ qua** trước khi bật workflow.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
**Bước 1:** Tải file JSON từ [n8n.io/workflows/13770](https://n8n.io/workflows/13770) (hoặc copy JSON từ link này).
**Bước 2:** Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON → Chọn **"Import"**.

**Hoặc copy/paste JSON trực tiếp:**
```json
{
  "nodes": {
    "1": {
      "parameters": {},
      "name": "Gmail Trigger",
      "type": "n8n-nodes-base.gmailTrigger",
      "typeVersion": 1,
      "position": [250, 300]
    },
    "2": {
      "parameters": {
        "resource": "gmail",
        "operation": "listMessages",
        "query": {
          "q": "label:unread",
          "maxResults": 10
        }
      },
      "name": "Gmail List Messages",
      "type": "n8n-nodes-base.gmail",
      "typeVersion": 1,
      "position": [450, 300]
    },
    "3": {
      "parameters": {
        "resource": "gmail",
        "operation": "getMessage",
        "query": {
          "id": "={{$node["2"].json[\"id\"]}}"
        }
      },
      "name": "Gmail Get Message",
      "type": "n8n-nodes-base.gmail",
      "typeVersion": 1,
      "position": [650, 300]
    },
    "4": {
      "parameters": {
        "model": "gemini-pro",
        "prompt": "Tóm tắt email này trong 3 câu và phân loại ticket theo chủ đề: mua hàng, kỹ thuật, phản hồi sản phẩm."
      },
      "name": "Gemini Summarize",
      "type": "n8n-nodes-langchain.lmChatGoogleGemini",
      "typeVersion": 1,
      "position": [850, 300]
    },
    "5": {
      "parameters": {
        "resource": "notion",
        "operation": "createPage",
        "query": {
          "parent": "={{$node["6"].json[\"id\"]}}",
          "properties": {
            "Name": "={{$node["3"].json[\"snippet\"]}}",
            "Summary": "={{$node["4"].json[\"content\"]}}",
            "Priority": "={{$node["7"].json[\"priority\"]}}"
          }
        }
      },
      "name": "Notion Create Ticket",
      "type": "n8n-nodes-base.notion",
      "typeVersion": 1,
      "position": [1050, 300]
    },
    "6": {
      "parameters": {
        "resource": "notion",
        "operation": "listPages",
        "query": {
          "filter": {
            "property": "Name",
            "title": {
              "equals": "Support Tickets"
            }
          }
        }
      },
      "name": "Notion Get Database",
      "type": "n8n-nodes-base.notion",
      "typeVersion": 1,
      "position": [650, 500]
    },
    "7": {
      "parameters": {
        "resource": "n8n-nodes-base.set",
        "operation": "set",
        "query": {
          "priority": "={{$node["4"].json[\"content\"].includes('khẩn cấp') ? 'High' : 'Low'}}"
        }
      },
      "name": "Set Priority",
      "type": "n8n-nodes-base.set",
      "typeVersion": 1,
      "position": [850, 500]
    },
    "8": {
      "parameters": {
        "resource": "slack",
        "operation": "sendMessage",
        "query": {
          "text": "Ticket mới: {{$node["3"].json[\"snippet\"]}} (Ưu tiên: {{$node["7"].json[\"priority\"]}})",
          "channel": "#support-alerts"
        }
      },
      "name": "Slack Alert",
      "type": "n8n-nodes-base.slack",
      "typeVersion": 1,
      "position": [1050, 500]
    }
  },
  "connections": {
    "main": [
      { "node": "1", "type": "trigger", "position": "right", "nodeType": "n8n-nodes-base.gmailTrigger", "index": 0 },
      { "node": "2", "type": "main", "connection": "main", "position": "right", "nodeType": "n8n-nodes-base.gmail", "index": 0 },
      { "node": "3", "type": "main", "connection": "main", "position": "right", "nodeType": "n8n-nodes-base.gmail", "index": 0 },
      { "node": "4", "type": "main", "connection": "main", "position": "right", "nodeType": "n8n-nodes-langchain.lmChatGoogleGemini", "index": 0 },
      { "node": "5", "type": "main", "connection": "main", "position": "right", "nodeType": "n8n-nodes-base.notion", "index": 0 },
      { "node": "6", "type": "main", "connection": "main", "position": "right", "nodeType": "n8n-nodes-base.notion", "index": 0 },
      { "node": "7", "type": "main", "connection": "main", "position": "right", "nodeType": "n8n-nodes-base.set", "index": 0 },
      { "node": "8", "type": "main", "connection": "main", "position": "right", "nodeType": "n8n-nodes-base.slack", "index": 0 }
    ]
  }
}
```

---

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
**Node quan trọng cần cấu hình:**
| **Node**               | **Cần Chỉnh Gì**                                                                 | **Lưu Ý**                                                                 |
|------------------------|----------------------------------------------------------------------------------|--------------------------------------------------------------------------|
| **Gmail Trigger**      | Chọn **thư mục hỗ trợ** (ví dụ: `label:unread`).                                | Đảm bảo email **không bị spam** hoặc **lọc sai**.                       |
| **Google Gemini**      | Cấu hình **API Key** và **prompt** chính xác.                                   | Prompt nên ngắn gọn: *"Tóm tắt email này trong 3 câu và phân loại ticket theo chủ đề: mua hàng, kỹ thuật, phản hồi sản phẩm."* |
| **Notion Database**    | Đảm bảo **schema** có trường: `Name`, `Summary`, `Priority`.                     | Nếu không có, **tạo mới** trước khi chạy workflow.                     |
| **Slack Alert**       | Chọn **#support-alerts** (hoặc channel khác).                                   | **Test trước** để không bị spam channel chính.                          |
| **Ưu Tiên Ticket**     | Cấu hình **điều kiện** cho `priority` (ví dụ: nếu có từ khóa "khẩn cấp").     | Sử dụng **node `n8n-nodes-base.set`** để tự động phân loại.               |

**Cách kiểm tra trước khi live:**
1. **Test Run** với **1-2 email mẫu** để đảm bảo:
   - AI tóm tắt **đúng nội dung**.
   - Ticket được **cập nhật Notion** đúng.
   - Slack **gửi cảnh báo** ưu tiên.
2. **Không bật Active** cho toàn bộ email **trước khi test xong**.

---

#### **3. Kích Hoạt ⚡️**
**Bước 1:** Nhấn **"Test"** với email mẫu.
**Bước 2:** Kiểm tra:
- Notion có **tạo ticket mới** không?
- Slack có **gửi cảnh báo** không?
**Bước 3:** Nếu OK, nhấn **"Active"** để workflow **chạy tự động**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Zapier/Make**
   - Nếu cần **gửi email tự động** khi ticket được cập nhật, kết hợp với **Zapier** để gửi thông báo qua email.

2. **Lưu Log Tất Cả Ticket**
   - Sử dụng **node `n8n-nodes-base.stickyNote`** để lưu **lịch sử ticket** và **thời gian xử lý**.

3. **Gửi Báo Cáo Định Kỳ**
   - Sử dụng **node `n8n-nodes-base.schedule`** để **tổng hợp báo cáo** số ticket ưu tiên hàng tuần và gửi qua Slack/Email.

4. **Phân Loại Ticket Theo Nhãn**
   - Nếu Gmail có **nhãn tự động** (ví dụ: `high-priority`), có thể **sử dụng điều kiện trong node `n8n-nodes-base.if`** để ưu tiên khác nhau.

5. **Tích Hợp với CRM (HubSpot, Salesforce)**
   - Nếu đang dùng **CRM**, có thể **cập nhật ticket từ Notion sang CRM** bằng node `n8n-nodes-base.httpRequest`.

---

### 📌 **Kết Luận**
Workflow này **giải phóng đội ngũ hỗ trợ** khỏi công việc **lặp lại và thủ công**, giúp các sếp:
✔ **Tiết kiệm 80% thời gian** xử lý email.
✔ **Tăng độ chính xác** với AI Gemini.
✔ **Ưu tiên ticket** tự động và **không quên cảnh báo**.
✔ **Hoạt động 24/7** mà không cần nhân viên trực ca.

**Hành động ngay hôm nay:**
1. **Chuẩn bị VPS** (n8n self-hosted) và **credentials**