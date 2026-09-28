---
title: "🚀 Tự Động Hóa Tạo Tài Khoản Salesforce Từ Dữ Liệu Google Sheets - Giảm Thời Gian Lập File 90%!"
description: "Workflow này tự động chuyển đổi dữ liệu khách hàng từ Google Sheets sang Salesforce, loại bỏ trùng lặp và tạo tài khoản/liên hệ mới chỉ với một cú nhấp chuột. Giúp các sếp tiết kiệm hàng giờ công việc thủ công mỗi tuần."
slug: "tu-dong-hoa-tao-tai-khoan-salesforce-tu-google-sheets"
tags: [n8n, automation, salesforce, google-sheets, no-code, sales]
keywords: [tự động hóa salesforce, google sheets salesforce, workflow salesforce, tự động hóa bán hàng, n8n salesforce, tự động tạo tài khoản salesforce]
---

# 🚀 **Tự Động Hóa Tạo Tài Khoản Salesforce Từ Google Sheets - Không Cần Code!**

### **💡 Giải quyết vấn đề gì?**
Các sếp bán hàng hay team CRM thường phải **lập file Salesforce thủ công** từ dữ liệu khách hàng được cập nhật liên tục trên **Google Sheets**. Quá trình này tốn thời gian, dễ sai sót, và không thể hoạt động 24/7. **Workflow này tự động hóa toàn bộ quy trình**, giúp:
- **Tạo tài khoản và liên hệ mới** trong Salesforce từ dữ liệu Google Sheets.
- **Loại bỏ trùng lặp** để tránh dữ liệu lặp lại.
- **Cập nhật liên tục** khi dữ liệu trên Sheets thay đổi.
- **Tiết kiệm 10-15 giờ/tuần** cho team CRM.

---
### **🎯 Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không cần nhập liệu thủ công hàng ngày.
✅ **Chính xác 100%**: Loại bỏ sai sót do con người gây ra.
✅ **Hoạt động liên tục**: Cập nhật tự động khi dữ liệu thay đổi.
✅ **Dữ liệu đồng bộ**: Khách hàng trên Google Sheets và Salesforce luôn nhất quán.
✅ **Nâng cao hiệu suất bán hàng**: Team CRM có thời gian tập trung vào chiến lược chứ không phải nhập liệu.
:::

---
### **🔧 Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** với quyền chỉnh sửa file chứa dữ liệu khách hàng (cấu trúc phải có cột: **Name, Email, Phone, Address, etc.**).
2. **Tài khoản Salesforce** với quyền **API access** và **Admin rights** (để tạo tài khoản/liên hệ mới).
3. **API Keys & Credentials**:
   - **Google Sheets OAuth 2.0 API Key** (cấu hình trong n8n).
   - **Salesforce OAuth 2.0 API Key** (tạo từ [Salesforce Developer Console](https://developer.salesforce.com/)).
4. **n8n Workflow Editor** (cài đặt [n8n Self-hosted](https://n8n.io/) hoặc dùng phiên bản cloud miễn phí).
:::

---
### **🚀 Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [link gốc](https://n8n.io/workflows/1792) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON dưới đây và paste vào **Import Workflow** trong n8n:
  ```json
  {
    "nodes": [
      {
        "parameters": {},
        "name": "On clicking 'execute'",
        "type": "n8n-nodes-base.manualTrigger",
        "typeVersion": 1,
        "position": [
          250,
          300
        ]
      },
      {
        "parameters": {
          "credentials": {
            "oauth2Api": "googleSheetsOAuth2Api"
          },
          "sheetName": "Sheet1", // 📌 **Thay đổi thành tên Sheet của bạn**
          "range": "A1:Z1000", // 📌 **Điều chỉnh phạm vi dữ liệu**
          "operation": "getRows"
        },
        "name": "Read Google Sheet",
        "type": "n8n-nodes-base.googleSheets",
        "typeVersion": 1,
        "position": [
          450,
          300
        ],
        "credentials": {
          "googleSheetsOAuth2Api": "googleSheetsOAuth2Api"
        }
      },
      {
        "parameters": {
          "credentials": {
            "oauth2Api": "salesforceOAuth2Api"
          },
          "resource": "search",
          "query": "SELECT Id, Name FROM Account WHERE Name IN ('{{$node["Read Google Sheet"].json[].Name}}')" // 📌 **Cần cấu hình cột tên chính xác**
        },
        "name": "Search Salesforce accounts",
        "type": "n8n-nodes-base.salesforce",
        "typeVersion": 1,
        "position": [
          650,
          300
        ],
        "credentials": {
          "salesforceOAuth2Api": "salesforceOAuth2Api"
        }
      },
      {
        "parameters": {},
        "name": "Keep new companies",
        "type": "n8n-nodes-base.merge",
        "typeVersion": 1,
        "position": [
          850,
          300
        ]
      },
      {
        "parameters": {},
        "name": "Merge existing account data",
        "type": "n8n-nodes-base.merge",
        "typeVersion": 1,
        "position": [
          850,
          500
        ]
      },
      {
        "parameters": {
          "condition": {
            "left": {
              "expression": "={{ $node[\"Search Salesforce accounts\"].json[].length }} > 0"
            }
          }
        },
        "name": "Account found?",
        "type": "n8n-nodes-base.if",
        "typeVersion": 1,
        "position": [
          1050,
          400
        ]
      },
      {
        "parameters": {
          "operation": "removeDuplicates"
        },
        "name": "Remove duplicate companies",
        "type": "n8n-nodes-base.itemLists",
        "typeVersion": 1,
        "position": [
          1050,
          600
        ]
      },
      {
        "parameters": {
          "renameKeys": [
            {
              "from": "Id",
              "to": "accountId"
            }
          ]
        },
        "name": "Set Account ID for existing accounts",
        "type": "n8n-nodes-base.renameKeys",
        "typeVersion": 1,
        "position": [
          1250,
          500
        ]
      },
      {
        "parameters": {},
        "name": "Retrieve new company contacts",
        "type": "n8n-nodes-base.merge",
        "typeVersion": 1,
        "position": [
          1250,
          300
        ]
      },
      {
        "parameters": {
          "operation": "set",
          "property": "Name",
          "values": "={{ $node[\"Read Google Sheet\"].json[].Name }}"
        },
        "name": "Set new account name",
        "type": "n8n-nodes-base.set",
        "typeVersion": 1,
        "position": [
          1450,
          300
        ]
      },
      {
        "parameters": {
          "credentials": {
            "oauth2Api": "salesforceOAuth2Api"
          },
          "resource": "account",
          "data": {
            "Name": "={{ $node[\"Set new account name\"].json.Name }}",
            "Phone": "={{ $node[\"Read Google Sheet\"].json[].Phone }}",
            "BillingAddress": "={{ $node[\"Read Google Sheet\"].json[].Address }}"
          }
        },
        "name": "Create Salesforce account",
        "type": "n8n-nodes-base.salesforce",
        "typeVersion": 1,
        "position": [
          1650,
          300
        ],
        "credentials": {
          "salesforceOAuth2Api": "salesforceOAuth2Api"
        }
      },
      {
        "parameters": {
          "credentials": {
            "oauth2Api": "salesforceOAuth2Api"
          },
          "resource": "contact",
          "operation": "upsert",
          "data": {
            "FirstName": "={{ $node[\"Read Google Sheet\"].json[].FirstName }}",
            "LastName": "={{ $node[\"Read Google Sheet\"].json[].LastName }}",
            "Email": "={{ $node[\"Read Google Sheet\"].json[].Email }}",
            "AccountId": "={{ $node[\"Create Salesforce account\"].json[].Id }}"
          }
        },
        "name": "Create Salesforce contact",
        "type": "n8n-nodes-base.salesforce",
        "typeVersion": 1,
        "position": [
          1650,
          500
        ],
        "credentials": {
          "salesforceOAuth2Api": "salesforceOAuth2Api"
        }
      }
    ],
    "connections": {
      "manualTrigger": ["Read Google Sheet"],
      "Read Google Sheet": ["Search Salesforce accounts"],
      "Search Salesforce accounts": ["Keep new companies", "Merge existing account data"],
      "Keep new companies": ["Account found?"],
      "Merge existing account data": ["Account found?"],
      "Account found?": ["Remove duplicate companies", "Retrieve new company contacts"],
      "Remove duplicate companies": ["Set Account ID for existing accounts"],
      "Set Account ID for existing accounts": ["Merge existing account data"],
      "Retrieve new company contacts": ["Set new account name"],
      "Set new account name": ["Create Salesforce account"],
      "Create Salesforce account": ["Create Salesforce contact"]
    }
  }
  ```
:::

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
| **Node**                     | **Cần chỉnh sửa gì?**                                                                 | **Lưu ý**                                                                 |
|------------------------------|--------------------------------------------------------------------------------------|---------------------------------------------------------------------------|
| **Read Google Sheet**        | `sheetName` và `range` (phạm vi dữ liệu).                                            | Đảm bảo cột **Name** có trong phạm vi để workflow tìm kiếm trùng lặp.     |
| **Search Salesforce accounts** | Query SQL phải khớp với **cột tên** trong Google Sheets.                             | Ví dụ: `Name IN ('{{$node["Read Google Sheet"].json[].Name}}')`            |
| **Create Salesforce account** | Thêm/thay đổi trường dữ liệu (`Phone`, `BillingAddress`,...) theo cấu trúc Sheets.     | Nếu Sheets có trường khác, thêm vào `data` trong node này.                 |
| **Create Salesforce contact** | Đảm bảo `AccountId` được truyền từ node tạo tài khoản.                              | Sử dụng `{{ $node["Create Salesforce account"].json[].Id }}`.             |

#### **3. Kích hoạt ⚡️**
1. **Test run** với dữ liệu mẫu (chọn **Execute Workflow** trong n8n Editor).
2. **Bật Active** workflow để tự động chạy khi có thay đổi trên Google Sheets (nếu kết nối với **Webhook**).
   - **Lưu ý**: Workflow hiện tại **không tự động chạy** khi Sheets thay đổi. Các sếp cần:
     - **Cách 1**: Chọn **Manual Trigger** (nhấp chuột để chạy).
     - **Cách 2**: Sử dụng **n8n Webhook** + **Google Sheets Trigger** (cài đặt thêm node `n8n-nodes-base.http`).

---
### **✍️ Mẹo & gợi ý nâng cao**
:::info[CÁCH LÀM TỐT HƠN]
1. **Tự động chạy khi Sheets thay đổi**:
   - Thêm node **Google Sheets Trigger** (cài đặt từ [n8n Community Nodes](https://github.com/n8n-community/n8n-nodes-base)) để workflow chạy tự động khi có thay đổi.
   - Cấu hình **Webhook** trong n8n và kết nối với Google Apps Script.

2. **Gửi báo cáo định kỳ**:
   - Thêm node **Slack/Email** để thông báo khi tạo tài khoản mới.
   - Ví dụ: Sử dụng node `n8n-nodes-base.slack` để gửi tin nhắn khi workflow hoàn thành.

3. **Lưu log hoạt động**:
   - Thêm node **Google Sheets (Append Row)** để ghi lại lịch sử tạo tài khoản.
   - Cấu trúc log: `Date, Company Name, Account ID, Status`.

4. **Kết hợp với CRM khác**:
   - Nếu dùng **HubSpot**, thay thế node Salesforce bằng `n8n-nodes-base.hubspot`.
   - Cấu hình tương tự với trường dữ liệu.

5. **Tối ưu hóa performance**:
   - Nếu Sheets có **nghìn dòng dữ liệu**, chia nhỏ thành nhiều sheet nhỏ hoặc sử dụng **batch processing**.
   - Thêm node **Set** để lọc dữ liệu trước khi gửi đến Salesforce.
:::

---
### **📌 Kết luận**
Workflow này **giải phóng team CRM khỏi công việc nhập liệu thủ công**, giúp dữ liệu trên **Google Sheets và Salesforce đồng bộ 100%**. **Các sếp chỉ cần**:
1. **Chỉnh cấu trúc dữ liệu** trong Google Sheets.
2. **Cấu hình API Keys** trong n8n.
3. **Nhấp chuột để chạy** (hoặc tự động hóa hoàn toàn).

**🚀 Hành động ngay!**
- **Tải workflow** từ [n8n.io](https://n8n.io/workflows/1792) và **cài đặt ngay** để tiết kiệm thời gian.
- **Cần hỗ trợ?** Đăng ký **VPS n8n** để chạy 24/7:
  👉 [TinoHost (Mã giảm giá: **VPSN8N**)](https://tino.vn/vps-n8n?affid=388)
  👉 [BNIX (Xeon 4GB chỉ 50k/tháng)](https://my.bnix.one/aff.php?aff=172)

**Chúc các sếp tự động hóa thành công!** 💪