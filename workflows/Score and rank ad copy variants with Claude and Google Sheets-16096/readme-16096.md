---
title: "🚀 Tự Động Học AI Claude Đánh Giá & Xếp Hạng Các Biến Thể Quảng Cáo - Log Lịch Sử Vào Google Sheets"
description: "Workflow tự động hóa sử dụng AI Claude để đánh giá, xếp hạng và lưu trữ biến thể quảng cáo, giúp các sếp tiết kiệm thời gian tối đa 80% trong quá trình A/B testing. Kết quả được tự động xếp hạng và ghi log vào Google Sheets để theo dõi dài hạn."
slug: "tieu-dong-hoa-danh-gia-xep-hang-quang-cao-voi-claude-google-sheets"
tags: [n8n, automation, ai-claude, google-sheets, content-creation, no-code]
keywords: [tự động hóa quảng cáo, ai đánh giá copy, xếp hạng biến thể quảng cáo, google sheets log, claude ai tự động hóa]
---

# 🚀 **Tự Động Học AI Claude Đánh Giá & Xếp Hạng Biến Thể Quảng Cáo - Log Lịch Sử Vào Google Sheets**

### **Nỗi Đau Của Các Sếp Trong Quá Trình A/B Testing Quảng Cáo**
Các sếp thường phải mất **từ 5-10 giờ/tuần** để:
- **So sánh thủ công** hàng chục biến thể quảng cáo (copy, hình ảnh, video).
- **Đánh giá chủ quan** dựa trên cảm nhận cá nhân, dẫn đến kết quả không nhất quán.
- **Lưu trữ lịch sử** đánh giá trong Excel/Google Sheets một cách rắc rối và dễ bị lỗi.
- **Không có hệ thống xếp hạng tự động**, phải tự tính toán và sắp xếp lại sau mỗi lần test.

**Workflow này giải quyết tất cả vấn đề trên bằng AI Claude + n8n, giúp các sếp:**
✅ **Tiết kiệm 80% thời gian** so sánh và đánh giá biến thể.
✅ **Đánh giá khách quan** dựa trên logic AI và tiêu chí doanh nghiệp.
✅ **Lưu trữ lịch sử** tự động vào Google Sheets, dễ dàng theo dõi và phân tích.
✅ **Xếp hạng tự động** theo điểm số, giúp lựa chọn biến thể tốt nhất chỉ trong vài giây.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ cao cho AI Claude)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa đánh giá biến thể quảng cáo** bằng AI Claude (không cần viết code).
- **Xếp hạng tự động** theo điểm số, giúp lựa chọn biến thể hiệu quả nhất.
- **Lưu trữ lịch sử** vào Google Sheets, dễ dàng **so sánh qua nhiều lần test**.
- **Gửi kết quả ngay về ứng dụng/website** thông qua webhook, không cần xử lý thủ công.
- **Cá nhân hóa tiêu chí đánh giá** theo **ICP, brand voice, và mục tiêu chiến dịch** của doanh nghiệp.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Claude AI** (Anthropic API Key) – [Đăng ký miễn phí](https://www.anthropic.com/api)
✔ **Google Sheets** với:
   - **Bảng dữ liệu** để lưu lịch sử đánh giá (cấu trúc sẽ được hướng dẫn).
   - **Thông tin API Key** của Google Sheets (tạo ở [Google Cloud Console](https://console.cloud.google.com/)).
✔ **Webhook URL** để nhận dữ liệu từ ứng dụng/website (ví dụ: từ **Zapier, Make, hoặc ứng dụng nội bộ**).
✔ **Dữ liệu mẫu biến thể quảng cáo** (JSON) để test workflow (mẫu sẽ được cung cấp).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
**Bước 1:** Tải file JSON từ [n8n.io/workflows/16096](https://n8n.io/workflows/16096) hoặc copy toàn bộ JSON dưới đây vào **n8n Editor**:
```json
{
  "nodes": {
    "1": {
      "parameters": {
        "path": "ad-copy-evaluator",
        "httpMethod": "POST"
      },
      "name": "When Variants Received",
      "type": "n8n-nodes-base.webhook"
    },
    "2": {
      "name": "Prepare Evaluation Settings",
      "type": "n8n-nodes-base.set"
    },
    "3": {
      "name": "Normalize Variants Data",
      "type": "n8n-nodes-base.code"
    },
    "4": {
      "name": "Post to Claude for Critic Notes",
      "type": "n8n-nodes-base.httpRequest"
    },
    "5": {
      "name": "Post to Claude for Scoring",
      "type": "n8n-nodes-base.httpRequest"
    },
    "6": {
      "name": "Parse and Sort Scores",
      "type": "n8n-nodes-base.code"
    },
    "7": {
      "name": "Append Scores to Google Sheets",
      "type": "n8n-nodes-base.googleSheets",
      "parameters": {
        "operation": "append"
      }
    },
    "8": {
      "name": "Return Ranked Variants Response",
      "type": "n8n-nodes-base.respondToWebhook"
    }
  },
  "connections": {
    "main": [
      {
        "from": "1",
        "to": "2"
      },
      {
        "from": "2",
        "to": "3"
      },
      {
        "from": "3",
        "to": "4"
      },
      {
        "from": "4",
        "to": "5"
      },
      {
        "from": "5",
        "to": "6"
      },
      {
        "from": "6",
        "to": "7"
      },
      {
        "from": "6",
        "to": "8"
      }
    ]
  }
}
```
**Bước 2:** Nhấn **"Import"** trong n8n Editor.

---

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Sau khi import, các sếp **cần cấu hình** các node quan trọng như sau:

##### **🔹 Node 1: "When Variants Received" (Webhook)**
- **Không cần chỉnh** nếu sử dụng URL mặc định (`https://<tên-n8n>/webhook/ad-copy-evaluator`).
- **Lưu ý:** Đảm bảo **ứng dụng/website** gửi dữ liệu theo **mẫu JSON** sau:
  ```json
  {
    "variants": [
      {
        "id": "variant_1",
        "copy": "Biến thể quảng cáo 1",
        "image_url": "https://example.com/image1.jpg"
      },
      {
        "id": "variant_2",
        "copy": "Biến thể quảng cáo 2",
        "image_url": "https://example.com/image2.jpg"
      }
    ]
  }
  ```

##### **🔹 Node 2: "Prepare Evaluation Settings" (Set)**
- **Thêm các tiêu chí đánh giá** vào biến `evaluationSettings` (ví dụ):
  ```json
  {
    "campaign_brief": "Giúp khách hàng tìm hiểu về dịch vụ SEO của chúng tôi",
    "icp": "Doanh nghiệp nhỏ và trung bình cần tăng traffic website",
    "brand_voice": "Chuyên nghiệp, thân thiện, giải pháp thực tế",
    "target_platform": "Facebook Ads"
  }
  ```
- **Lưu ý:** Các tiêu chí này sẽ được **gửi cùng với biến thể** để Claude đánh giá.

##### **🔹 Node 4 & 5: "Post to Claude for Critic Notes" & "Post to Claude for Scoring" (HTTP Request)**
- **Cấu hình API Key Claude:**
  - **Headers:**
    ```json
    {
      "Authorization": "Bearer YOUR_ANTHROPIC_API_KEY",
      "Content-Type": "application/json"
    }
    ```
  - **Body (Prompt cho Claude):**
    - **Đánh giá chi tiết (Critic Notes):**
      ```json
      {
        "prompt": "You are an expert copywriter evaluating ad variants for {{ evaluationSettings.campaign_brief }}. Provide detailed feedback on each variant's strengths and weaknesses based on the following criteria: {{ evaluationSettings.icp }}, {{ evaluationSettings.brand_voice }}, and {{ evaluationSettings.target_platform }}. Return feedback in JSON format with keys: 'variant_id', 'notes', 'suggestions'."
      }
      ```
    - **Đánh giá điểm số (Scoring):**
      ```json
      {
        "prompt": "Score each ad variant from 1-10 based on effectiveness for {{ evaluationSettings.campaign_brief }}. Consider the following criteria: relevance to {{ evaluationSettings.icp }}, alignment with {{ evaluationSettings.brand_voice }}, and performance potential on {{ evaluationSettings.target_platform }}. Return scores in JSON format with keys: 'variant_id', 'overall_score', 'criteria_scores' (with sub-criteria: 'icp_relevance', 'brand_alignment', 'platform_potential')."
      }
      ```
- **Lưu ý:**
  - **Thay thế `YOUR_ANTHROPIC_API_KEY`** bằng API Key thực tế.
  - **Kiểm tra tài liệu Claude API** để cập nhật cấu trúc prompt nếu cần.

##### **🔹 Node 6: "Parse and Sort Scores" (Code)**
- **Mã JavaScript mặc định** đã xử lý việc **sắp xếp biến thể theo điểm số**.
- **Không cần chỉnh** trừ khi các sếp muốn **cá nhân hóa logic xếp hạng**.

##### **🔹 Node 7: "Append Scores to Google Sheets" (Google Sheets)**
- **Cấu hình Google Sheets:**
  - **Spreadsheet ID:** (Tìm trong URL của Google Sheets: `https://docs.google.com/spreadsheets/d/SPREADSHEET_ID/edit`).
  - **Sheet Name:** (Tên tab trong Google Sheets, ví dụ: "Ad Copy Evaluation").
  - **Range:** (Cột đầu tiên để ghi dữ liệu, ví dụ: `A1`).
  - **Headers:** (Các tiêu đề cột trong Google Sheets, ví dụ: `variant_id, copy, overall_score, notes`).
- **Lưu ý:**
  - **Tạo một bảng mới** với cấu trúc:
    | variant_id | copy | overall_score | notes | date |
    |------------|------|--------------|-------|------|
    | variant_1  | ...  | 8.5           | ...   | ...  |

##### **🔹 Node 8: "Return Ranked Variants Response" (Respond To Webhook)**
- **Không cần chỉnh** nếu muốn trả về **tất cả dữ liệu đã xếp hạng**.
- **Lưu ý:** Nếu ứng dụng cần **chỉ một số trường nhất định**, các sếp có thể chỉnh **mã JavaScript** trong node này.

---

#### **3. Kích Hoạt ⚡️**
**Bước 1:** **Test Run** với dữ liệu mẫu:
```json
{
  "variants": [
    {
      "id": "variant_1",
      "copy": "Tìm hiểu cách SEO tăng traffic website chỉ trong 30 ngày!",
      "image_url": "https://example.com/seo.jpg"
    },
    {
      "id": "variant_2",
      "copy": "SEO là cách tối ưu website để Google yêu thích bạn!",
      "image_url": "https://example.com/seo2.jpg"
    }
  ]
}
```
**Bước 2:** Nhấn **"Active"** để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram:**
   - Thêm node **Slack/Telegram** sau node **"Return Ranked Variants Response"** để **báo cáo kết quả tự động** cho team.
   - **Mẫu thông báo:**
     ```
     📢 **Kết quả đánh giá biến thể quảng cáo:**
     - Biến thể 1: Điểm 8.5/10
     - Biến thể 2: Điểm 7.2/10
     - **Biến thể tốt nhất:** [Tên biến thể]
     ```

2. **Lưu log chi tiết vào Google Sheets:**
   - Thêm **cột "date"** và **"user"** (người gửi yêu cầu) để theo dõi lịch sử.
   - **Cấu trúc Google Sheets nâng cao:**
     | variant_id | copy | overall_score | notes | date | user | campaign_name |

3. **Tự động gửi báo cáo định kỳ:**
   - Sử dụng **n8n Trigger (Schedule)** để **gửi báo cáo hàng tuần** về biến thể hiệu quả nhất.
   - **Cấu hình:**
     - **Node Trigger:** `n8n-nodes-base.schedule`
     - **Thời gian:** `0 0 * * 1` (tối thứ 2 hàng tuần).
     - **Node sau:** Gửi email (Gmail) hoặc Slack thông báo.

4. **Cá nhân hóa tiêu chí đánh giá:**
   - **Thay đổi prompt Claude** để phù hợp với **mục tiêu khác nhau**:
     - **Cho chiến dịch bán hàng:** Nhấn mạnh **CTA (Call to Action)** và **hiệu quả chuyển đổi**.
     - **Cho chiến dịch brand awareness:** Nhấn mạnh **độ hấp dẫn và nhớ thương hiệu**.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** của các sếp khỏi công việc **so sánh và đánh giá biến thể quảng cáo thủ công**, thay vào đó **AI Claude tự động đánh giá, xếp hạng và lưu trữ** kết quả vào Google Sheets.

**Hành động ngay:**
1. **Import workflow** và cấu hình theo hướng dẫn trên.
2. **Test với dữ liệu thực tế** của doanh nghiệp.
3. **Tích hợp với ứng dụng/website** để nhận dữ liệu tự động.
4. **Theo dõi và tối ưu hóa** chiến dịch quảng cáo của mình **bằng dữ liệu khách quan**.

**🚀 Cùng tự động hóa quảng cáo của mình ngay hôm nay!** Nếu có vấn đề, các sếp có thể **đăng câu hỏi trên [Community n8n](https://community.n8n.io/)** hoặc liên hệ tác giả [Milos Vranes](https://www.linkedin.com/in/milosvranes/) để hỗ trợ thêm.