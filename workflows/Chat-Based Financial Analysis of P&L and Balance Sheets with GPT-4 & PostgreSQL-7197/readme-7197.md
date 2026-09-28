---
title: "💰 **Tự Động Hóa Phân Tích Tài Chính P&L & Bảng Cân Đối với GPT-4 + PostgreSQL (Không Cần Code!)**"
description: "Workflow tự động hóa phân tích báo cáo lợi nhuận (P&L) và bảng cân đối tài sản bằng trí tuệ nhân tạo GPT-4, kết nối trực tiếp với cơ sở dữ liệu PostgreSQL. Giúp các sếp tiết kiệm hàng giờ công sức phân tích thủ công, phát hiện xu hướng tài chính nhanh chóng và đưa ra quyết định dựa trên dữ liệu chính xác 100%."
slug: "tieu-dong-hoa-phan-tich-tai-chinh-gpt4-postgresql"
tags: [n8n, automation, no-code, ai-gpt4, postgresql, financial-analysis]
keywords: [n8n workflow tài chính, phân tích P&L tự động, GPT-4 phân tích báo cáo, PostgreSQL + AI, tự động hóa báo cáo tài chính]
---

# 🚀 **Phân Tích Tài Chính P&L & Bảng Cân Đối với GPT-4: Giải Pháp Tự Động Hóa Cho Các Sếp Bận Rộn**

Bạn có bao giờ phải mất **hàng giờ** để phân tích báo cáo lợi nhuận (P&L) và bảng cân đối tài sản (Balance Sheets) thủ công? Hay phải đối mặt với **rủi ro sai sót** khi đọc số liệu từ Excel hoặc PDF? Hoặc thậm chí **không đủ thời gian** để so sánh xu hướng tài chính giữa các kỳ?

**Workflow này giải quyết tất cả những vấn đề trên!** Với sự kết hợp **GPT-4 (trí tuệ nhân tạo tiên tiến nhất hiện nay)** và **PostgreSQL (cơ sở dữ liệu mạnh mẽ)**, các sếp có thể:
✅ **Nhập dữ liệu** từ báo cáo tài chính (P&L, Balance Sheets) qua chatbot.
✅ **Được GPT-4 phân tích tự động**, phát hiện xu hướng, điểm yếu, và đề xuất giải pháp.
✅ **Lưu kết quả vào PostgreSQL**, dễ dàng truy xuất và báo cáo định kỳ.
✅ **Hoạt động 24/7**, không cần can thiệp thủ công.

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[**3 Lợi Ích Cốt Lõi**]
- **Tiết kiệm thời gian**: Phân tích báo cáo chỉ trong **vài giây** thay vì nhiều giờ.
- **Chính xác 100%**: Tránh sai sót do con người khi so sánh dữ liệu thủ công.
- **Quản lý thông minh**: GPT-4 không chỉ đọc số liệu mà còn **phát hiện xu hướng**, dự đoán rủi ro, và đề xuất chiến lược.
- **Hoạt động liên tục**: Workflow chạy tự động, không phụ thuộc vào giờ làm việc của nhân viên.
:::

---
### 🔧 **Yêu cầu cần thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI LẮP ĐỘNG**]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản PostgreSQL** (để lưu trữ và truy xuất dữ liệu tài chính):
   - **Link đăng ký VPS PostgreSQL** (nếu chưa có): [👉 Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (mã giảm giá: **VPSN8N**).
   - **Bảng dữ liệu** đã chuẩn bị với 2 sheet chính:
     - `P_L_Reports` (báo cáo lợi nhuận).
     - `Balance_Sheets` (bảng cân đối tài sản).
   - **Credentials PostgreSQL**: Host, Port, Database Name, Username, Password.

2. **Tài khoản OpenAI API** (để sử dụng GPT-4):
   - **API Key** từ [OpenAI](https://platform.openai.com/account/api-keys).
   - **Model**: Chọn `gpt-4` (hoặc `gpt-4-turbo` nếu có).

3. **n8n Self-hosted** (để chạy workflow 24/7):
   - **👉 Đăng ký VPS n8n** (tối thiểu 2GB RAM): [TinoHost](https://tino.vn/vps-n8n?affid=388) (giảm 39% với mã **VPSN8N**).
   - **Cài đặt n8n** theo hướng dẫn: [n8n.io/docs](https://n8n.io/docs/).

---
### 🚀 **Cách Import & Lưu ý khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/7197) hoặc copy toàn bộ JSON dưới đây vào **n8n Editor**:
  ```json
  {
    "nodes": [
      {
        "parameters": {},
        "name": "When chat message received",
        "type": "chatTrigger",
        "typeVersion": 1,
        "position": [250, 300]
      },
      {
        "parameters": {
          "query": "SELECT * FROM \"P_L_Reports\"",
          "connection": {
            "host": "your-postgres-host",
            "port": "5432",
            "database": "your-database",
            "user": "your-username",
            "password": "your-password"
          }
        },
        "name": "P_L_Reports",
        "type": "postgresTool",
        "typeVersion": 1,
        "position": [450, 300]
      },
      {
        "parameters": {
          "query": "SELECT * FROM \"Balance_Sheets\"",
          "connection": {
            "host": "your-postgres-host",
            "port": "5432",
            "database": "your-database",
            "user": "your-username",
            "password": "your-password"
          }
        },
        "name": "Balance_Sheets",
        "type": "postgresTool",
        "typeVersion": 1,
        "position": [450, 500]
      },
      {
        "parameters": {
          "memoryKey": "chat_history",
          "windowSize": 5
        },
        "name": "Simple Memory",
        "type": "memoryBufferWindow",
        "typeVersion": 1,
        "position": [250, 600]
      },
      {
        "parameters": {
          "model": "gpt-4",
          "apiKey": {
            "name": "OpenAI_API_Key",
            "value": "your-openai-api-key"
          },
          "temperature": 0.7,
          "maxTokens": 1000
        },
        "name": "OpenAI Chat Model",
        "type": "lmChatOpenAi",
        "typeVersion": 1,
        "position": [650, 450]
      },
      {
        "parameters": {
          "agentType": "openai",
          "model": "gpt-4",
          "tools": [
            {
              "name": "P_L_Reports",
              "description": "Fetch P&L data from PostgreSQL",
              "parameters": {
                "query": {
                  "type": "string",
                  "description": "SQL query to fetch P&L data"
                }
              }
            },
            {
              "name": "Balance_Sheets",
              "description": "Fetch Balance Sheets data from PostgreSQL",
              "parameters": {
                "query": {
                  "type": "string",
                  "description": "SQL query to fetch Balance Sheets data"
                }
              }
            }
          ],
          "apiKey": {
            "name": "OpenAI_API_Key",
            "value": "your-openai-api-key"
          },
          "temperature": 0.7
        },
        "name": "AI Agent",
        "type": "agent",
        "typeVersion": 1,
        "position": [850, 450]
      }
    ],
    "connections": {
      "When chat message received": {
        "main": [
          [
            {
              "node": "AI Agent",
              "connection": "input"
            }
          ]
        ]
      },
      "AI Agent": {
        "main": [
          [
            {
              "node": "OpenAI Chat Model",
              "connection": "input"
            }
          ]
        ]
      },
      "OpenAI Chat Model": {
        "main": [
          [
            {
              "node": "Simple Memory",
              "connection": "input"
            }
          ]
        ]
      },
      "Simple Memory": {
        "main": [
          [
            {
              "node": "AI Agent",
              "connection": "memory"
            }
          ]
        ]
      },
      "P_L_Reports": {
        "main": [
          [
            {
              "node": "AI Agent",
              "connection": "toolOutput"
            }
          ]
        ]
      },
      "Balance_Sheets": {
        "main": [
          [
            {
              "node": "AI Agent",
              "connection": "toolOutput"
            }
          ]
        ]
      }
    }
  }
  ```
  - **Lưu ý**: Copy toàn bộ JSON trên vào **n8n Editor** (chứ không phải chỉ phần `nodes`).

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình PostgreSQL**
- Trong node `P_L_Reports` và `Balance_Sheets`:
  - Thay thế `your-postgres-host`, `your-database`, `your-username`, `your-password` bằng thông tin thực tế.
  - **Kiểm tra query**: Đảm bảo `SELECT * FROM "P_L_Reports"` và `SELECT * FROM "Balance_Sheets"` trỏ đến bảng đúng.

##### **B. Cấu hình OpenAI API**
- Trong node `OpenAI Chat Model` và `AI Agent`:
  - Thay thế `your-openai-api-key` bằng **API Key** từ OpenAI.
  - **Model**: Đảm bảo chọn `gpt-4` (hoặc `gpt-4-turbo` nếu có).

##### **C. Cấu hình AI Agent**
- **Tools**: Đảm bảo hai tool `P_L_Reports` và `Balance_Sheets` được liên kết với query PostgreSQL đúng.
- **Prompt mặc định**: GPT-4 sẽ tự động phân tích dữ liệu, nhưng các sếp có thể **cập nhật prompt** trong node `OpenAI Chat Model` để điều chỉnh logic phân tích (ví dụ: "So sánh P&L kỳ này với kỳ trước và đề xuất giải pháp").

##### **D. Cấu hình Simple Memory**
- **memoryKey**: Đặt là `chat_history` để lưu lịch sử chat.
- **windowSize**: Đặt là `5` (lưu 5 lần chat gần nhất).

#### **3. Kích hoạt ⚡️**
1. **Test run**:
   - Gửi một **tin nhắn chat** (ví dụ: *"Phân tích báo cáo P&L kỳ Q3"*).
   - Kiểm tra kết quả trả về từ GPT-4.
2. **Bật Active workflow**:
   - Đảm bảo tất cả node đều **đỏ chấm** (⚠️) và chuyển sang **xanh** (✅).

---
### ✍️ **Mẹo & gợi ý nâng cao**
:::info[**CÁCH SỬ DỤNG HIỆU QUẢ NHẤT**]
1. **Kết nối với Slack/Telegram**:
   - Thêm node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram` để nhận báo cáo tự động qua chat.

2. **Lưu log phân tích**:
   - Thêm node `n8n-nodes-base.ftp` hoặc `n8n-nodes-base.googleDrive` để lưu kết quả phân tích vào Google Drive hoặc FTP.

3. **Báo cáo định kỳ**:
   - Sử dụng **n8n Cron Trigger** để chạy phân tích tự động hàng tháng và gửi báo cáo qua email (node `n8n-nodes-base.email`).

4. **Tối ưu hóa prompt**:
   - Cập nhật prompt trong node `OpenAI Chat Model` để GPT-4 tập trung vào:
     - **Xu hướng tăng/giảm** so với kỳ trước.
     - **Điểm yếu** trong P&L (ví dụ: chi phí cao, lợi nhuận thấp).
     - **Đề xuất cải thiện** (ví dụ: giảm chi phí, tăng doanh thu).

5. **Bảo mật dữ liệu**:
   - Sử dụng **PostgreSQL với TLS** để bảo mật kết nối.
   - **Mask API Key** trong n8n bằng cách sử dụng biến môi trường.
:::

---
### 📌 **Kết luận**
Workflow này không chỉ **giải phóng thời gian** cho các sếp khỏi công việc phân tích tài chính thủ công, mà còn **tăng cường quyết định dựa trên dữ liệu** với sự hỗ trợ của GPT-4. **Đừng để báo cáo tài chính trở thành gánh nặng nữa!**

👉 **Bắt đầu ngay**:
1. **Cài đặt n8n** trên VPS (🎁 Giảm 39% với mã **VPSN8N**).
2. **Import workflow** và cấu hình PostgreSQL + OpenAI.
3. **Test run** và **bật Active** để phân tích tự động!

**Nếu có vấn đề**, để lại comment bên dưới hoặc liên hệ tôi qua [email/telegram]. Chúc các sếp thành công! 🚀