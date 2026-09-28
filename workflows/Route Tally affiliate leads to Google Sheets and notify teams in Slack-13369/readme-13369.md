---
title: "🚀 Tự Động Hóa Lead Affiliate Từ Tally.so → Google Sheets + Thông Báo Slack (Không Cần Code)"
description: "Giải pháp tự động hóa 100% tự động chuyển lead từ form Tally.so sang Google Sheets riêng biệt cho từng affiliate, đồng thời thông báo ngay cho đội ngũ Slack. Tiết kiệm thời gian quản lý lead lên đến 80% và giảm thiểu lỗi nhân sự."
slug: "tu-dong-hoa-lead-affiliate-tally-so-google-sheets-slack"
tags: [n8n, automation, lead-generation, google-sheets, slack-integration, tally-so]
keywords: [n8n workflow tự động hóa lead, tự động hóa affiliate marketing, Tally.so đến Google Sheets, Slack notification lead, tự động hóa không code]
---

# 🚀 **Tự Động Hóa Lead Affiliate Từ Tally.so → Google Sheets + Thông Báo Slack (Không Cần Code)**

### **🔥 Nỗi Đau Của Các Sếp Trong Quản Lý Lead Affiliate**
Các sếp đang phải:
- **Lặp đi lặp lại** việc copy-paste dữ liệu từ form Tally.so sang Google Sheets thủ công.
- **Mất thời gian** phân loại lead theo affiliate code, tạo sheet mới nếu chưa tồn tại.
- **Đợi lâu** để thông báo cho đội ngũ Slack khi có lead mới, dẫn đến phản hồi chậm.
- **Lo ngại lỗi** khi nhân viên quên ghi chép hoặc ghi nhầm thông tin.

**Giải pháp này tự động hóa toàn bộ quy trình trên chỉ trong vài phút cài đặt!**

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** với tài nguyên tối thiểu:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
*Lưu ý: N8n chạy ổn định nhất trên Linux (Ubuntu 22.04+).*
:::

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** quản lý lead: Không cần copy-paste thủ công.
- **Tự động phân loại lead** theo affiliate code: Tạo sheet riêng cho mỗi affiliate.
- **Thông báo tức thời** trên Slack: Đội ngũ phản hồi nhanh chóng.
- **Dữ liệu chính xác 100%**: Không lỗi nhân sự, dữ liệu luôn đồng bộ.
- **Hoạt động 24/7**: Nhận lead ngay cả khi các sếp ngủ.
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Tally.so**:
   - API Key từ [Tally.so Developer Dashboard](https://tally.so/api).
   - Form Tally.so công khai (cần webhook để trigger).
2. **Google Workspace**:
   - Google Drive folder để lưu sheet affiliate (ví dụ: `Affiliate_Submissions`).
   - Google Sheets OAuth 2.0 credentials (tạo tại [Google Cloud Console](https://console.cloud.google.com/)).
3. **Slack**:
   - Bot Token (`xoxb-...`) với scope `chat:write`.
   - Channel Slack để nhận thông báo (ví dụ: `#affiliate-leads`).
4. **n8n Self-hosted**:
   - Cài đặt n8n trên VPS (hướng dẫn tại [n8n.io](https://n8n.io/)).
   - Cài đặt **n8n-nodes-tallyforms** (node hỗ trợ Tally.so).

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [link gốc](https://n8n.io/workflows/13369) hoặc copy JSON dưới đây:
   ```json
   {
     "nodes": [
       {
         "parameters": {
           "resource": {
             "operation": "fileFolder",
             "folderId": "{{$node["Find Affiliate Sheet"].jsonpath("$.id")}}"
           }
         },
         "name": "Move to Target Folder",
         "type": "n8n-nodes-base.googleDrive",
         "credentials": {
           "googleDriveOAuth2Api": "googleDriveOAuth2Api"
         }
       },
       {
         "parameters": {},
         "name": "Sheet Exists?",
         "type": "n8n-nodes-base.if",
         "credentials": {}
       },
       {
         "parameters": {
           "resource": {
             "title": "{{$node["Extract Form Fields"].jsonpath("$.affiliationCode")}} Affiliate Leads",
             "mimeType": "application/vnd.google-apps.spreadsheet"
           }
         },
         "name": "Create Affiliate Sheet",
         "type": "n8n-nodes-base.googleSheets",
         "credentials": {
           "googleSheetsOAuth2Api": "googleSheetsOAuth2Api"
         }
       },
       {
         "parameters": {
           "operation": "append",
           "sheetName": "Leads",
           "data": "{{$node["Format Row Data"].json}}"
         },
         "name": "Append Data (New Sheet)",
         "type": "n8n-nodes-base.googleSheets",
         "credentials": {
           "googleSheetsOAuth2Api": "googleSheetsOAuth2Api"
         }
       },
       {
         "parameters": {
           "operation": "append",
           "sheetName": "Leads",
           "data": "{{$node["Format Row Data"].json}}"
         },
         "name": "Append Data (Existing Sheet)",
         "type": "n8n-nodes-base.googleSheets",
         "credentials": {
           "googleSheetsOAuth2Api": "googleSheetsOAuth2Api"
         }
       },
       {
         "parameters": {
           "code": "// Format data for Google Sheets\nconst data = [\n  {\n    \"Name\": \"{{$node[\"Extract Form Fields\"].jsonpath(\"$.name\")}}\",\n    \"Email\": \"{{$node[\"Extract Form Fields\"].jsonpath(\"$.email\")}}\",\n    \"Affiliate\": \"{{$node[\"Extract Form Fields\"].jsonpath(\"$.affiliationCode\")}}\",\n    \"Phone\": \"{{$node[\"Extract Form Fields\"].jsonpath(\"$.phone\")}}\",\n    \"Message\": \"{{$node[\"Extract Form Fields\"].jsonpath(\"$.message\")}}\"\n  }\n];\n\nmodule.exports = data;"
         },
         "name": "Format Row Data",
         "type": "n8n-nodes-base.code",
         "credentials": {}
       },
       {
         "parameters": {
           "code": "// Build Slack message\nconst lead = {\n  name: \"{{$node[\"Extract Form Fields\"].jsonpath(\"$.name\")}}\",\n  email: \"{{$node[\"Extract Form Fields\"].jsonpath(\"$.email\")}}\",\n  affiliate: \"{{$node[\"Extract Form Fields\"].jsonpath(\"$.affiliationCode\")}}\",\n  message: \"{{$node[\"Extract Form Fields\"].jsonpath(\"$.message\")}}\"\n};\n\nconst message = `*New Affiliate Lead:*\n**Name:** ${lead.name}\n**Email:** ${lead.email}\n**Affiliate:** ${lead.affiliate}\n**Message:** ${lead.message}\`;\n\nmodule.exports = { text: message };"
         },
         "name": "Build Slack Message",
         "type": "n8n-nodes-base.code",
         "credentials": {}
       },
       {
         "parameters": {
           "resource": {
             "query": {
               "name": "contains",
               "value": "{{$node[\"Extract Form Fields\"].jsonpath(\"$.affiliationCode\")}} Affiliate Leads"
             }
           }
         },
         "name": "Find Affiliate Sheet",
         "type": "n8n-nodes-base.googleDrive",
         "credentials": {
           "googleDriveOAuth2Api": "googleDriveOAuth2Api"
         }
       },
       {
         "parameters": {
           "credentials": "slackApi"
         },
         "name": "Send Lead Notification",
         "type": "n8n-nodes-base.slack",
         "credentials": {
           "slackApi": "slackApi"
         }
       },
       {
         "parameters": {
           "credentials": "tallyApi"
         },
         "name": "Submission Trigger",
         "type": "n8n-nodes-tallyforms.tallyTrigger",
         "credentials": {
           "tallyApi": "tallyApi"
         }
       },
       {
         "parameters": {},
         "name": "Extract Form Fields",
         "type": "n8n-nodes-base.set",
         "credentials": {}
       }
     ],
     "connections": {
       "Submission Trigger": {
         "main": ["Extract Form Fields"]
       },
       "Extract Form Fields": {
         "main": ["Sheet Exists?"]
       },
       "Sheet Exists?": {
         "true": ["Append Data (Existing Sheet)"],
         "false": ["Find Affiliate Sheet"]
       },
       "Find Affiliate Sheet": {
         "main": ["Sheet Exists?"]
       },
       "Append Data (Existing Sheet)": {
         "main": ["Send Lead Notification"]
       },
       "Create Affiliate Sheet": {
         "main": ["Append Data (New Sheet)"],
         "moveToTargetFolder": ["Move to Target Folder"]
       },
       "Append Data (New Sheet)": {
         "main": ["Send Lead Notification"]
       },
       "Build Slack Message": {
         "main": ["Send Lead Notification"]
       },
       "Move to Target Folder": {}
     }
   }
   ```
   - Nhấn **Import** trong n8n Editor.

#### **Phương pháp 2: Copy/Paste JSON**
1. Copy toàn bộ JSON trên vào **Import Workflow** trong n8n Editor.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
#### **🔹 Node "Submission Trigger" (Tally.so)**
- **Tham số cần thiết**:
  - **Tally Form ID**: Lấy từ URL của form Tally.so (ví dụ: `https://tally.so/r/abc123` → `abc123`).
  - **Credentials**: Điền `tallyApi` (tạo tại **Credentials** → **Add** → **Tally.so**).

#### **🔹 Node "Find Affiliate Sheet" (Google Drive)**
- **Tham số cần thiết**:
  - **Folder ID**: Lấy từ URL của folder Google Drive (ví dụ: `https://drive.google.com/drive/folders/1AbCdEfG` → `1AbCdEfG`).
  - **Credentials**: Điền `googleDriveOAuth2Api`.

#### **🔹 Node "Create Affiliate Sheet" & "Append Data" (Google Sheets)**
- **Tham số cần thiết**:
  - **Sheet Name**: Đặt mặc định là `{{$node["Extract Form Fields"].jsonpath("$.affiliationCode")}} Affiliate Leads`.
  - **Credentials**: Điền `googleSheetsOAuth2Api`.
  - **Header Row**: Bật `true` (nếu sheet mới).

#### **🔹 Node "Build Slack Message" (Code)**
- **Tham số cần thiết**:
  - **Channel ID**: Lấy từ URL Slack channel (ví dụ: `https://slack.com/archives/C12345678` → `C12345678`).
  - **Credentials**: Điền `slackApi`.

#### **🔹 Node "Send Lead Notification" (Slack)**
- **Tham số cần thiết**:
  - **Channel**: Chọn channel Slack để thông báo.
  - **Credentials**: Điền `slackApi`.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Execute Node** trên `Submission Trigger` và gửi một lead mẫu từ Tally.so.
   - Kiểm tra:
     - Dữ liệu có được append vào sheet Google Sheets không?
     - Thông báo Slack có xuất hiện không?
2. **Bật Active**:
   - Chuyển workflow sang **Active** trong n8n Editor.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm trường dữ liệu**:
   - Mở rộng form Tally.so để thu thập thông tin như **ngành nghề**, **ngân sách**, **mô tả chi tiết**.
   - Cập nhật node `Format Row Data` để hiển thị thêm cột trong Google Sheets.

2. **Tự động sắp xếp sheet**:
   - Sử dụng node **Google Drive** để di chuyển sheet affiliate vào folder con theo năm/tháng (ví dụ: `Affiliate_Submissions/2024/Q3`).

3. **Thông báo cá nhân hóa**:
   - Trong node `Build Slack Message`, thêm `@mention` cho thành viên cụ thể:
     ```javascript
     const message = `*New Lead for @affiliate_user:*\n**Name:** ${lead.name}\n...`;
     ```

4. **Lưu log hoạt động**:
   - Thêm node **Google Sheets** để ghi lịch sử hoạt động (thời gian, affiliate, trạng thái).

5. **Kết hợp với CRM**:
   - Sau khi lead được ghi vào Google Sheets, sử dụng node **HTTP Request** để push dữ liệu vào HubSpot/Zoho CRM.

---

## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc lặp đi lặp lại quản lý lead affiliate. Với chỉ **vài phút cài đặt**, các sếp sẽ:
✅ **Tự động hóa** toàn bộ quy trình từ form đến thông báo.
✅ **Tăng hiệu suất** đội ngũ bán hàng với dữ liệu chính xác.
✅ **Giảm thiểu lỗi** và tăng cường sự đồng bộ trong team.

**🚀 Hãy thử ngay và tự động hóa lead affiliate của mình!**
Nếu có vấn đề, các sếp có thể tham khảo [hướng dẫn cài đặt n8n](https://docs.n8n.io/) hoặc liên hệ cộng đồng [n8n.io/community](https://n8n.io/community).