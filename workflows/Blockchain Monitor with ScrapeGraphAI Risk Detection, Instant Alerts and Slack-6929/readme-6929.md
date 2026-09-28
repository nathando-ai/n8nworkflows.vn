---
title: "🚀 **Blockchain Monitor AI: Dò Tìm Rủi Ro & Cảnh Báo Ngay Lập Tức Trên Slack**"
description: "Tự động hóa giám sát blockchain (Ethereum, Bitcoin, BSC, Polygon) với AI ScrapeGraphAI để phát hiện giao dịch cao rủi ro (>$10k), phân tích điểm số rủi ro và gửi cảnh báo tức thời đến Slack. Giúp các sếp crypto giảm thiểu mất mát và phản ứng nhanh chóng với sự kiện bất thường."
slug: "blockchain-monitor-ai-detec-rủi-ro-cảnh-báo-slack"
tags: [n8n, blockchain, crypto-trading, ai-summarization, slack-alert, scrapegraphai]
keywords: [n8n workflow blockchain, tự động hóa giám sát crypto, cảnh báo rủi ro giao dịch, AI phân tích blockchain, Slack alert crypto]
---

# 🚀 **Blockchain Monitor AI: Cảnh Báo Rủi Ro Giao Dịch Trên Slack Với AI**

### **💥 Nỗi Đau Của Các Sếp Crypto Hiện Nay**
Giám sát hàng ngàn giao dịch blockchain thủ công là như **"đánh cá bằng chổi"** – tốn thời gian, dễ bỏ lỡ rủi ro, và không thể phản ứng kịp thời với giao dịch cao giá (>$10k) hoặc block có nguy cơ thất bại (>10%). Với **Blockchain Monitor AI**, các sếp có thể:
✅ **Tự động dò tìm** giao dịch rủi ro trên Ethereum, Bitcoin, BSC và Polygon.
✅ **Phân tích điểm số rủi ro** (High/Medium/Low) bằng AI ScrapeGraphAI.
✅ **Nhận cảnh báo tức thời** trên Slack với thông tin chi tiết, không cần code.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
- **Tiết kiệm 20+ giờ/ngày** so với giám sát thủ công.
- **Phát hiện rủi ro ngay lập tức** với ngưỡng cảnh báo tự động ($10k/giao dịch, >10% thất bại).
- **Cảnh báo Slack thông minh** với định dạng rõ ràng (emoji, điểm số, thống kê).
- **Hoạt động 24/7** trên VPS riêng (Self-hosted) để không bỏ lỡ bất kỳ sự kiện nào.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI LẮP ĐỘNG**]
Để workflow hoạt động, các sếp cần:
1. **ScrapeGraphAI API Key** (đăng ký tại [ScrapeGraphAI](https://scrapegraph.ai/)).
2. **Slack Webhook URL** (tạo tại `Apps > Incoming Webhooks` trong Slack).
3. **Blockchain Webhook URL** (cung cấp bởi node blockchain hoặc API như Moralis/Alchemy).
4. **VPS Self-hosted** (để workflow chạy liên tục, không phụ thuộc vào n8n.io free tier).
   👉 **[Đăng ký VPS TinoHost (Mã giảm giá: VPSN8N)](https://tino.vn/vps-n8n?affid=388)** – Giảm tới 39%.
   👉 **[VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho AI).
:::

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/6929](https://n8n.io/workflows/6929) hoặc copy/paste JSON vào **n8n Editor**.
- **Cách import nhanh**:
  ```bash
  curl -X POST https://YOUR_N8N_URL/api/v1/workflows/new -H "Authorization: Bearer YOUR_API_KEY" -H "Content-Type: application/json" -d @workflow.json
  ```

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này gồm **6 node chính**, mỗi node đều cần cấu hình cẩn thận:

##### **🔗 Node 1: Blockchain Webhook**
- **Chức năng**: Nhận dữ liệu block từ nguồn bên ngoài (API blockchain, node riêng).
- **Cấu hình**:
  - **Path**: `eed656b3-6a7f-4460-92e0-802bca2522d0` (không thay đổi).
  - **Method**: POST (để nhận dữ liệu từ webhook).
  - **Lưu ý**: Nếu dùng API bên thứ ba (Moralis/Alchemy), cấu hình **Trigger** thành `Polling` với thời gian refresh (ví dụ: 30 giây).

##### **🔄 Node 2: Normalize Data (Code)**
- **Chức năng**: Chuẩn hóa dữ liệu block từ nhiều chain khác nhau (Ethereum, Bitcoin, BSC, Polygon) thành định dạng thống nhất.
- **Lưu ý**:
  - **Mã JavaScript** trong node này đã được tối ưu sẵn. **Không chỉnh sửa** trừ khi biết code.
  - **Dữ liệu đầu vào cần có**:
    ```json
    {
      "blockNumber": "12345678",
      "chain": "ethereum",
      "timestamp": "2024-05-20T10:00:00Z",
      "transactions": [...]  // Danh sách giao dịch trong block
    }
    ```

##### **🤖 Node 3: ScrapeGraphAI**
- **Chức năng**: Trích xuất và phân tích giao dịch bằng AI để phát hiện rủi ro.
- **Cấu hình**:
  - **API Key**: Nhập **ScrapeGraphAI API Key** từ tài khoản của bạn.
  - **Prompt mặc định** (không cần chỉnh):
    ```json
    {
      "prompt": "Analyze this blockchain transaction for risk factors. Return structured JSON with 'highValue', 'riskScore', 'failureRate', and 'chainInfo'."
    }
    ```
  - **Lưu ý**:
    - Nếu API trả về lỗi, kiểm tra **API Key** và **dữ liệu đầu vào**.
    - **Ngưỡng rủi ro mặc định**:
      - **High Value**: >$10,000.
      - **Failure Rate**: >10%.

##### **⚡ Node 4: Risk Analyzer (Code)**
- **Chức năng**: Tính toán **điểm số rủi ro** (0-100) dựa trên dữ liệu từ ScrapeGraphAI.
- **Lưu ý**:
  - **Mã JavaScript** đã tính toán điểm số theo công thức:
    ```javascript
    const riskScore = (highValue ? 50 : 0) + (failureRate > 10 ? 30 : 0) + (blockVolume > 100000 ? 20 : 0);
    ```
  - **Không chỉnh sửa** trừ khi muốn thay đổi logic rủi ro.

##### **🚨 Node 5: Risk Filter (If)**
- **Chức năng**: Lọc block chỉ khi **rủi ro cao (>=50 điểm)** hoặc có giao dịch >$10k.
- **Cấu hình**:
  - **Condition**:
    ```json
    {
      "condition": "$node['ScrapeGraphAI'].json()['riskScore'] >= 50 || $node['ScrapeGraphAI'].json()['highValue']"
    }
    ```
  - **Lưu ý**: Nếu muốn thay đổi ngưỡng rủi ro, chỉnh **`>= 50`** thành giá trị mong muốn.

##### **📱 Node 6: Slack Alert**
- **Chức năng**: Gửi cảnh báo đến Slack với thông tin chi tiết.
- **Cấu hình**:
  - **Slack Webhook URL**: Nhập URL từ `Incoming Webhooks` trong Slack.
  - **Channel ID**: Chọn channel muốn nhận cảnh báo (ví dụ: `#crypto-alerts`).
  - **Message Template** (không cần chỉnh, nhưng có thể tùy chỉnh):
    ```json
    {
      "text": ":rotating_light: **RISK ALERT** :rotating_light",
      "blocks": [
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": "*Blockchain*: <${chain}> | *Block*: ${blockNumber} | *Risk Score*: ${riskScore}/100"
          }
        },
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": "*High-Value Transactions*:\n${highValueTransactions}"
          }
        }
      ]
    }
    ```
  - **Lưu ý**:
    - **Kiểm tra Slack Bot Permission**: Bot cần quyền `write` vào channel.
    - **Test trước**: Gửi một cảnh báo mẫu để kiểm tra định dạng.

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Nhập dữ liệu mẫu từ **Blockchain Webhook** (ví dụ: block Ethereum có giao dịch >$10k).
  - Kiểm tra **Slack Alert** có hiển thị đúng không.
- **Bật Active**:
  - Chuyển trạng thái workflow từ **Draft** sang **Active**.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[**Tăng Cường Hiệu Quả**]
1. **Kết hợp với Telegram**:
   - Thêm node **Telegram Bot** để cảnh báo song song với Slack.
   - Cấu hình tại [Telegram Bot API](https://core.telegram.org/bots/api).

2. **Lưu Log Dữ Liệu**:
   - Thêm node **Google Sheets** hoặc **Airtable** để lưu lịch sử cảnh báo.
   - Cấu hình tại [n8n Google Sheets Node](https://docs.n8n.io/integrations/builtins/nodes/base/googleSheets/).

3. **Báo Cáo Định Kỳ**:
   - Sử dụng **n8n Scheduler** để gửi báo cáo tuần/month về rủi ro blockchain.
   - Cấu hình tại [n8n Scheduler](https://docs.n8n.io/integrations/builtins/nodes/base/scheduler/).

4. **Thay Đổi Ngưỡng Rủi Ro**:
   - Mở node **Risk Analyzer (Code)** và chỉnh sửa logic để phù hợp với chiến lược của bạn.
   - Ví dụ: Đặt ngưỡng **High Value** thành $5k thay vì $10k.
:::

---
### **📌 Kết Luận**
**Blockchain Monitor AI** là công cụ **tự động hóa hoàn chỉnh** để các sếp crypto:
✔ **Giám sát blockchain 24/7** mà không cần code.
✔ **Phát hiện rủi ro ngay lập tức** với cảnh báo Slack thông minh.
✔ **Tiết kiệm thời gian và tiền bạc** bằng việc tránh mất mát từ giao dịch cao rủi ro.

**Hành động ngay!**
1. **Cài đặt VPS** (n8n + ScrapeGraphAI API).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Active** và bắt đầu giám sát!

👉 **[Tải workflow JSON ngay](https://n8n.io/workflows/6929)** và **cài đặt VPS** với mã giảm giá **VPSN8N** để tiết kiệm chi phí! 🚀