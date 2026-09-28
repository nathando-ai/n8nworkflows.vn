---
title: "🚀 Tự Động Hóa Audit SEO Kỹ Thuật Tích Hợp SE Ranking & Google Sheets - Giúp Các Sếp Tiết Kiệm 20h/Tháng"
description: "Workflow tự động hóa kiểm tra SEO kỹ thuật cho website bằng SE Ranking và lưu kết quả vào Google Sheets, giúp các sếp theo dõi sức khỏe SEO liên tục mà không cần code. Giảm thời gian kiểm tra từ 20h/tháng xuống 5 phút/ngày."
slug: "tieu-dong-hoa-audit-seo-se-ranking-google-sheets"
tags: [n8n, automation, seo, se-ranking, google-sheets, market-research]
keywords: [tự động hóa audit seo, se ranking n8n, google sheets seo, kiểm tra seo kỹ thuật tự động, seo audit workflow]
---

# 🚀 **Tự Động Hóa Audit SEO Kỹ Thuật với SE Ranking & Google Sheets: Giúp Các Sếp Theo Dõi Website 24/7 Mà Không Cần Code**

### **Nỗi Đau Của Các Sếp Hiện Nay**
Các sếp SEO, chủ website hoặc nhà phát triển web thường phải **tốn thời gian và công sức** để:
- **Kiểm tra SEO kỹ thuật thủ công** (kiểm tra lỗi crawl, meta tags, speed, mobile-friendly, internal linking...) trên nhiều trang web.
- **So sánh kết quả giữa các lần audit** để theo dõi tiến bộ.
- **Lưu trữ và phân tích dữ liệu** trong nhiều file Excel hoặc Google Sheets rối rắm.
- **Bị mất thời gian** vì phải đợi SE Ranking crawl xong mới lấy báo cáo.

**Kết quả?** Thời gian và công sức bị "chôn vùi" trong công việc lặp đi lặp lại, trong khi **SEO kỹ thuật lại là yếu tố quyết định thứ hạng Google**.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
Sau khi áp dụng workflow này, các sếp sẽ:
✅ **Tiết kiệm 20h/tháng** (từ việc kiểm tra thủ công) → **Tăng hiệu suất 400%**.
✅ **Nhận báo cáo SEO kỹ thuật đầy đủ** (score health 0-100, lỗi, cảnh báo, và phân loại theo danh mục).
✅ **Theo dõi lịch sử audit** trong Google Sheets, giúp **phân tích trend** qua thời gian (tối đa 10 lần audit gần nhất).
✅ **Cập nhật tự động** mỗi khi có thay đổi trên website (không cần can thiệp).
✅ **Chia sẻ báo cáo với khách hàng** một cách chuyên nghiệp, giúp **tăng tin tưởng và giá trị dịch vụ**.

---
### **🔧 Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
📌 **Tài khoản SE Ranking** (đã có API Key) → [Đăng ký miễn phí](https://seranking.com/).
📌 **Tài khoản Google Sheets** (để lưu trữ lịch sử audit).
📌 **Domain website** muốn audit (ví dụ: `example.com` → thay bằng domain thực tế).
📌 **N8n Self-hosted** (để workflow chạy 24/7) →
   :::info[Gợi ý hạ tầng cho n8n]
   Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
   :::

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể **import workflow** từ file JSON hoặc **copy/paste JSON** vào n8n Editor:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/12811) (nếu có).
- **Hoặc copy toàn bộ JSON** từ dưới đây và dán vào **Import Workflow** trong n8n:
  ```json
  {
    "nodes": [
      {
        "parameters": {},
        "name": "When clicking 'Execute workflow'",
        "type": "manualTrigger",
        "typeVersion": 1,
        "position": [250, 300]
      },
      {
        "parameters": {
          "operation": "createStandard",
          "resource": "websiteAudit"
        },
        "name": "Create standard audit",
        "type": "@seranking/n8n-nodes-seranking.seRanking",
        "typeVersion": 1,
        "credentials": ["seRankingApi"],
        "position": [250, 500]
      },
      {
        "parameters": {
          "time": 300
        },
        "name": "Wait for crawl (5 min)",
        "type": "wait",
        "typeVersion": 1,
        "position": [250, 700]
      },
      {
        "parameters": {
          "operation": "getStatus",
          "resource": "websiteAudit"
        },
        "name": "Check audit status",
        "type": "@seranking/n8n-nodes-seranking.seRanking",
        "typeVersion": 1,
        "credentials": ["seRankingApi"],
        "position": [250, 900]
      },
      {
        "parameters": {},
        "name": "If audit complete",
        "type": "if",
        "typeVersion": 1,
        "position": [450, 900]
      },
      {
        "parameters": {
          "operation": "getReport",
          "resource": "websiteAudit"
        },
        "name": "Get audit report",
        "type": "@seranking/n8n-nodes-seranking.seRanking",
        "typeVersion": 1,
        "credentials": ["seRankingApi"],
        "position": [650, 900]
      },
      {
        "parameters": {
          "time": 120
        },
        "name": "Wait and retry (2 min)",
        "type": "wait",
        "typeVersion": 1,
        "position": [650, 1100]
      },
      {
        "parameters": {
          "resource": "websiteAudit"
        },
        "name": "List all audits for domain",
        "type": "@seranking/n8n-nodes-seranking.seRanking",
        "typeVersion": 1,
        "credentials": ["seRankingApi"],
        "position": [650, 1300]
      },
      {
        "parameters": {
          "code": "// Format data for Google Sheets\n// Example: Convert SE Ranking JSON to array of objects\nconst audits = $input.all();\n\n// Lấy audit gần nhất và 9 audit trước đó\nconst recentAudits = audits.slice(0, 10).map(audit => (\n  {\n    \"Date\": new Date(audit.createdAt).toLocaleDateString(),\n    \"Health Score\": audit.score,\n    \"Errors\": audit.errors.length,\n    \"Warnings\": audit.warnings.length,\n    \"Notices\": audit.notices.length,\n    \"URL\": audit.url\n  }\n));\n\nreturn { audits: recentAudits };"
        },
        "name": "Format audits for Sheet",
        "type": "code",
        "typeVersion": 1,
        "position": [850, 1300]
      },
      {
        "parameters": {
          "operation": "appendOrUpdate",
          "sheetName": "Audit History",
          "range": "A1:F1000"
        },
        "name": "Export to Google Sheets",
        "type": "googleSheets",
        "typeVersion": 1,
        "credentials": ["googleSheetsOAuth2Api"],
        "position": [1050, 1300]
      }
    ],
    "connections": {
      "manualTrigger": ["Create standard audit"],
      "Create standard audit": ["Wait for crawl (5 min)"],
      "Wait for crawl (5 min)": ["Check audit status"],
      "Check audit status": ["If audit complete"],
      "If audit complete ifTrue": ["Get audit report"],
      "Get audit report": ["Wait and retry (2 min)"],
      "Wait and retry (2 min)": ["List all audits for domain"],
      "List all audits for domain": ["Format audits for Sheet"],
      "Format audits for Sheet": ["Export to Google Sheets"]
    }
  }
  ```
  *(Lưu ý: Các sếp cần **thay `sheetName` và `range`** trong node `Export to Google Sheets` theo cấu trúc bảng của mình.)*

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
#### **A. Cấu Hình SE Ranking API**
1. **Tải và cài đặt node SE Ranking** (nếu chưa có):
   ```bash
   npm install @seranking/n8n-nodes-seranking
   ```
2. **Thêm credentials SE Ranking**:
   - Trong n8n, đi đến **Credentials** → **Add** → **SE Ranking API**.
   - Điền:
     - **API Key**: Lấy từ [SE Ranking Dashboard](https://seranking.com/dashboard/api).
     - **Domain**: Nhập domain muốn audit (ví dụ: `example.com`).

#### **B. Cấu Hình Google Sheets**
1. **Kết nối Google Sheets**:
   - Trong n8n, đi đến **Credentials** → **Add** → **Google Sheets OAuth2**.
   - Theo hướng dẫn để **đăng nhập và cấp quyền**.
2. **Chỉnh node `Export to Google Sheets`**:
   - **sheetName**: Nhập tên sheet muốn lưu (ví dụ: `Audit History`).
   - **range**: Đặt từ `A1:F1000` (đủ cho 1000 dòng, điều chỉnh nếu cần).

#### **C. Cấu Hình Node `Format audits for Sheet`**
- **Code mặc định** đã được tối ưu để chuyển đổi JSON của SE Ranking thành **dạng phù hợp với Google Sheets**.
- Các sếp **không cần chỉnh sửa** trừ khi muốn thay đổi cấu trúc dữ liệu xuất ra.

#### **D. Thay Domain Default**
- Trong node **`Create standard audit`**, thay `example.com` bằng domain thực tế của các sếp.

---
### **3. Kích Hoạt ⚡️**
1. **Test Run với dữ liệu mẫu**:
   - Chạy workflow **manual trigger** để kiểm tra.
   - Kiểm tra **Google Sheets** xem có xuất dữ liệu không.
2. **Bật Active workflow**:
   - Sau khi test thành công, **bật Active** để workflow chạy tự động.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
### **1. Chạy Tự Động Hàng Tuần**
- Thay **manual trigger** bằng **Schedule Trigger** để chạy hàng tuần:
  ```json
  {
    "parameters": {
      "cronTime": "0 0 * * 0" // Chạy vào Chủ Nhật 00:00
    },
    "name": "Schedule Trigger",
    "type": "scheduleTrigger",
    "typeVersion": 1,
    "position": [250, 300]
  }
  ```
  *(Thay `0 0 * * 0` thành thời gian mong muốn.)*

### **2. Gửi Báo Cáo SEO Sang Slack/Email**
- Thêm node **Slack** hoặc **Email** sau `Export to Google Sheets` để tự động gửi báo cáo:
  ```json
  {
    "parameters": {
      "text": "🚀 Audit SEO mới hoàn tất!\n- Domain: {{ $node["Create standard audit"].jsonpath("$.url") }}\n- Health Score: {{ $node["Get audit report"].jsonpath("$.score") }}\n- Link báo cáo: [Google Sheets](https://sheets.example.com)",
      "channel": "#seo-alerts"
    },
    "name": "Send Slack Notification",
    "type": "slack",
    "typeVersion": 1,
    "credentials": ["slackApi"],
    "position": [1050, 1500]
  }
  ```

### **3. Lưu Log Lịch Sử Audit**
- Thêm node **HTTP Request** để lưu log vào **Google Drive** hoặc **Firebase**:
  ```json
  {
    "parameters": {
      "method": "POST",
      "url": "https://api.example.com/logs",
      "body": {
        "domain": "{{ $node["Create standard audit"].jsonpath("$.url") }}",
        "score": "{{ $node["Get audit report"].jsonpath("$.score") }}",
        "timestamp": "{{ $node["Get audit report"].jsonpath("$.createdAt") }}"
      }
    },
    "name": "Log to API",
    "type": "httpRequest",
    "typeVersion": 1,
    "position": [1050, 1700]
  }
  ```

### **4. Phân Tích Trend SEO**
- Sử dụng **Google Sheets** để vẽ biểu đồ trend:
  - Tạo biểu đồ **line chart** với trục X là `Date`, trục Y là `Health Score`.
  - Cài đặt **trendline** để dự đoán xu hướng.

---
## **📌 Kết Luận**
Workflow này **giải phóng thời gian** của các sếp để tập trung vào **strategy SEO cao cấp** thay vì việc **kiểm tra thủ công lặp đi lặp lại**. Với **SE Ranking + Google Sheets**, các sếp có thể:
✔ **Theo dõi sức khỏe SEO website** 24/7.
✔ **So sánh kết quả qua thời gian** một cách dễ dàng.
✔ **Chia sẻ báo cáo chuyên nghiệp** với khách hàng.

**Hành động ngay hôm nay!**
1. **Import workflow** vào n8n.
2. **Cấu hình SE Ranking & Google Sheets**.
3. **Bật tự động hóa** và **quên đi việc kiểm tra SEO thủ công**!

---
**💡 Cần hỗ trợ thêm?**
- **Đăng ký VPS n8n** để chạy 24/7: [TinoHost](https://tino.vn/vps-n8n?affid=388) (giảm 39%).
- **Hỏi đáp** về workflow: [Diễn đàn n8n Việt Nam](https://vi.n8n.io/community).