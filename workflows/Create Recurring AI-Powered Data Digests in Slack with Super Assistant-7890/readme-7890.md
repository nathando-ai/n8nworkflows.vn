---
title: "🤖 Tự Động Tạo Báo Cáo AI Hàng Ngày Cho Slack - Không Cần Code!"
description: "Workflow tự động hóa gửi báo cáo tổng hợp thông tin từ Jira, Notion, Trello... qua Slack hàng ngày bằng AI, tiết kiệm 10+ giờ làm việc mỗi tuần cho các sếp."
slug: "tự-dộng-tạo-báo-cáo-ai-hàng-ngày-slack"
tags: [n8n, automation, ai-rag, slack, super-work, no-code]
keywords: [n8n workflow tự động hóa, báo cáo hàng ngày AI, Slack automation, Super Assistant API, tự động hóa công việc hàng ngày]
---

# 🚀 **Tự Động Tạo Báo Cáo AI Hàng Ngày Cho Slack - Không Cần Code!**

### **Giải pháp cho các sếp bị "ngập" trong báo cáo hàng ngày**
Hàng ngày, các sếp phải mất **30-60 phút** để tổng hợp thông tin từ Jira, Notion, Trello, Google Sheets... rồi gửi qua Slack cho đội nhóm. **Workflow này tự động hóa toàn bộ quá trình** bằng AI, giúp bạn:
✅ **Tiết kiệm 10+ giờ/tuần** cho công việc thủ công.
✅ **Nhận báo cáo tổng hợp chính xác** từ nhiều nguồn dữ liệu khác nhau.
✅ **Cá nhân hóa thông tin** theo nhu cầu của từng nhóm.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Báo cáo tự động** hàng ngày từ Jira, Notion, Trello, Google Sheets...
- **Tích hợp AI** để tổng hợp và trình bày thông tin một cách logic.
- **Gửi qua Slack** ngay lập tức, không cần copy-paste.
- **Cấu hình 1 lần, hoạt động mãi** với lịch trình tự động.
:::

---
### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản Super.work** (để tạo AI Assistant):
   - [Đăng ký Super.work](https://super.work/) (mã giảm giá: **SUPERN8N** - giảm 20%).
   - **API Token** và **Assistant ID** từ Super.work.
2. **Tài khoản Slack** và **API Token Slack** (để gửi báo cáo).
3. **Dữ liệu nguồn** (Jira, Notion, Trello, Google Sheets...) đã kết nối với Super.work.
:::

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Bước 1:** Tải file JSON từ [n8n.io/workflows/7890](https://n8n.io/workflows/7890).
- **Bước 2:** Trên n8n Editor, nhấn **Import** và chọn file JSON.
- **Bước 3:** Chọn **Create Recurring AI-Powered Data Digests in Slack**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **4 node chính**, các sếp cần cấu hình như sau:

##### **🔹 Node 1: Schedule Trigger (Lịch trình tự động)**
- **Cấu hình:**
  - Chọn **Recurrence** (lặp lại hàng ngày, hàng tuần...).
  - Ví dụ: **Lặp lại hàng ngày lúc 9h sáng** (thời gian Việt Nam: `Asia/Ho_Chi_Minh`).
  - **Lưu ý:** Nếu không chọn timezone, workflow có thể chạy sai giờ.

##### **🔹 Node 2: Set the query (Đặt câu hỏi cho AI)**
- **Cấu hình:**
  - **Query:** Nhập câu hỏi tổng hợp dữ liệu từ Super Assistant.
  - **Ví dụ:**
    ```json
    "Tóm tắt công việc mới nhất từ Jira trong tuần qua, bao gồm tiến độ, người phụ trách và deadline."
    ```
  - **Lưu ý:** Câu hỏi càng cụ thể, báo cáo càng chính xác.

##### **🔹 Node 3: Query Super Assistant (Gọi API Super)**
- **Cấu hình:**
  - **Method:** `POST`
  - **URL:** `https://api.super.work/v1/assistants/{ASSISTANT_ID}/run`
  - **Headers:**
    - `Authorization: Bearer {API_TOKEN}`
    - `Content-Type: application/json`
  - **Body (JSON):**
    ```json
    {
      "query": "{{$node["Set the query"].json["query"]}}"
    }
    ```
  - **Lưu ý:**
    - Thay `{ASSISTANT_ID}` bằng ID Assistant từ Super.work.
    - Thay `{API_TOKEN}` bằng API Token từ Super.work.
    - **Không quên chọn "Bearer Token" credential** trong n8n.

##### **🔹 Node 4: Send digest in Slack (Gửi báo cáo qua Slack)**
- **Cấu hình:**
  - **Method:** `POST`
  - **URL:** `https://slack.com/api/chat.postMessage`
  - **Headers:**
    - `Authorization: Bearer xoxp-{SLACK_API_TOKEN}`
  - **Body (JSON):**
    ```json
    {
      "channel": "#tên-channel-của-bạn",
      "text": "📊 **Báo cáo hàng ngày**",
      "blocks": [
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": "{{$node["Query Super Assistant"].json.body}}"
          }
        }
      ]
    }
    ```
  - **Lưu ý:**
    - Thay `#tên-channel-của-bạn` bằng tên channel Slack muốn gửi.
    - **Không quên chọn "slackApi" credential** đã cấu hình trước.

#### **3. Kích hoạt ⚡️**
- **Bước 1:** Nhấn **Test Run** để kiểm tra workflow với dữ liệu mẫu.
- **Bước 2:** Nếu thành công, nhấn **Active** để bật workflow.

---
### ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁCH LÀM NÂNG CAO]
1. **Tích hợp với Google Drive/OneDrive** để lưu báo cáo hàng ngày.
2. **Gửi báo cáo qua Email** bằng node `n8n-nodes-base.email` nếu Slack không phù hợp.
3. **Cập nhật câu hỏi AI** theo từng nhóm (VD: Báo cáo kỹ thuật vs. báo cáo marketing).
4. **Dùng Sticky Note** để ghi chú lỗi hoặc cập nhật nhanh.
5. **Kết hợp với Zapier** nếu cần thêm tính năng như gửi báo cáo qua Telegram.
:::

---
### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc thủ công, đồng thời **cung cấp báo cáo AI chính xác** từ nhiều nguồn dữ liệu. **Chỉ cần cấu hình 1 lần**, nó sẽ hoạt động tự động hàng ngày!

👉 **Bắt đầu ngay:**
1. [Tải workflow JSON](https://n8n.io/workflows/7890).
2. [Đăng ký Super.work](https://super.work/) (mã giảm giá: **SUPERN8N**).
3. [Cài đặt n8n trên VPS](https://docs.n8n.io/hosting/installation/) (Self-hosted ổn định 24/7).

**Hãy tự động hóa công việc của mình ngay hôm nay!** 🚀