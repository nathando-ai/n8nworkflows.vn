---
title: "🔍 Tự Động Hoá Nghiên Cứu Thị Trường Sử Dụng AI Agent + Web Search + Báo Cáo Tự Động (OpenRouter + Jina AI)"
description: "Workflow tự động hóa nghiên cứu thị trường chuyên nghiệp với AI agent thông minh, kết hợp tìm kiếm web (Serper), phân tích dữ liệu (Jina AI), và sinh báo cáo tự động hóa 100% bằng OpenRouter. Giúp các sếp tiết kiệm 80% thời gian so với cách làm thủ công, với độ chính xác cao và khả năng chống hallucination."
slug: "tieu-dong-hoa-nghien-cuu-thi-trieu-ai-agent-jina-ai"
tags: [n8n, automation, ai-agent, market-research, openrouter, jina-ai, no-code]
keywords: [n8n workflow nghiên cứu thị trường, tự động hóa nghiên cứu AI, OpenRouter AI agent, Jina AI web scraping, báo cáo tự động hóa, tự động hóa không code]
---

# 🚀 **Tự Động Hoá Nghiên Cứu Thị Trường Với AI Agent + Web Search + Báo Cáo Tự Động**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp**
Bạn đã bao giờ phải:
- **Tốn hàng giờ** để tìm kiếm và tổng hợp thông tin từ nhiều nguồn khác nhau (LinkedIn, Twitter, Semantic Scholar, trang web công ty)?
- **Lo lắng về độ chính xác** của dữ liệu do AI sinh ra, đặc biệt là khi gặp hallucination (sai lệch logic)?
- **Không có thời gian** để viết báo cáo tổng hợp một cách chuyên nghiệp và logic?
- **Cần báo cáo định kỳ** nhưng lại phải làm thủ công, mất nhiều công sức?

Workflow này **giải quyết tất cả** những vấn đề trên bằng cách:
✅ **Tự động hóa toàn bộ quy trình** từ tìm kiếm đến viết báo cáo, chỉ cần gửi yêu cầu qua Webhook.
✅ **Sử dụng AI Agent thông minh** (OpenRouter) kết hợp với **web search (Serper)** và **scraping công cụ (Jina AI)** để thu thập dữ liệu chính xác.
✅ **Xây dựng báo cáo tự động** với cấu trúc Markdown sạch sẽ, dễ đọc và tái sử dụng.
✅ **Kiểm tra và sửa hallucination** bằng hệ thống 3 lớp AI (Writing Report → Verifying Report → Fixing Hallucinations) để đảm bảo **độ tin cậy cao nhất**.
✅ **Hoạt động 24/7** trên VPS riêng, không phụ thuộc vào người dùng.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** so với cách làm thủ công (từ 10h xuống còn 2h cho một báo cáo).
- **Báo cáo chuyên nghiệp** với cấu trúc logic, dễ đọc và tái sử dụng.
- **Độ chính xác cao** nhờ hệ thống kiểm tra hallucination tự động.
- **Hoạt động liên tục** (24/7) trên VPS riêng, không cần can thiệp người dùng.
- **Kết hợp nhiều nguồn dữ liệu** (LinkedIn, Twitter, Semantic Scholar, trang web công ty) trong một báo cáo duy nhất.
- **Mở rộng dễ dàng** bằng cách thêm các công cụ scraping mới (Google Sheets, APIs khác).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản API** (cần đăng ký và lấy API Key):
   - **[OpenRouter API](https://openrouter.ai/)** (miễn phí hoặc trả phí, tùy thuộc vào lượng sử dụng).
     - *Lưu ý*: OpenRouter hỗ trợ nhiều mô hình AI như `openrouter/auto`, `qwen/qwen3-235b`, `anthropic/claude-opus-4.5`, `anthropic/claude-sonnet-4.5`.
   - **[Jina AI](https://jina.ai/)** (dùng để đọc nội dung từ URL).
   - **[Serper API](https://serper.dev/)** (tìm kiếm web tự động, miễn phí cho 1000+ query/tháng).
   - **[ScrapingDog API](https://www.scrapingdog.com/)** (dùng để scraping LinkedIn, Twitter/X, Instagram).
     - *Lưu ý*: ScrapingDog yêu cầu API Key và có giới hạn request.

2. **VPS Self-hosted** (để workflow chạy 24/7):
   - 👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này).

3. **N8n Community Edition** (cài đặt trên VPS):
   - Hướng dẫn cài đặt: [N8n Self-hosted](https://docs.n8n.io/hosting/installation/).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/12504](https://n8n.io/workflows/12504) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/12504) và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **36 node** và được chia thành **3 phần chính**:
- **Phần 1: Tìm kiếm và thu thập dữ liệu** (Serper, Jina AI, ScrapingDog).
- **Phần 2: Xử lý và viết báo cáo** (AI Agent + OpenRouter).
- **Phần 3: Kiểm tra và sửa hallucination** (Verifying Report + Fixing Hallucinations).

##### **A. Cấu Hình Credentials (API Keys)**
Các node cần thiết và cách cấu hình:
| **Node**               | **Credentials**               | **Hướng Dẫn Cấu Hình**                                                                 |
|------------------------|-------------------------------|----------------------------------------------------------------------------------------|
| OpenRouter Chat Model  | `openRouterApi`               | Điền `API Key` từ OpenRouter vào **Credentials** của n8n.                              |
| Jina AI Tool           | `jinaAiApi`                   | Điền `API Key` từ Jina AI.                                                             |
| Serper API             | `httpHeaderAuth`              | Điền `API Key` từ Serper vào **HTTP Headers** của node `Serper API 2`.               |
| ScrapingDog (LinkedIn, Twitter, Instagram) | `httpQueryAuth` | Điền `API Key` từ ScrapingDog vào **Query Parameters** của các node scraping.       |

##### **B. Cấu Hình Webhook (Trigger)**
- Node **"Trigger research request (Webhook)"** được cấu hình với:
  - **Path**: `general-research`
  - **HTTP Method**: `POST`
- **Lưu ý**: Sau khi import, **không thay đổi path** trừ khi bạn muốn thay đổi URL nhận request.

##### **C. Cấu Hình AI Agent**
- **Prompt mặc định** đã được tối ưu hóa cho nghiên cứu thị trường.
- **Không cần chỉnh sửa** trừ khi bạn muốn thay đổi logic của AI (ví dụ: thay đổi mô hình AI từ `openrouter/auto` sang `qwen/qwen3-235b`).

##### **D. Kiểm Tra Hallucination**
Workflow tự động kích hoạt **3 bước kiểm tra**:
1. **Verifying Report Agent**: Kiểm tra tính logic và độ hỗ trợ của báo cáo.
2. **Fixing Hallucinations Agent**: Sửa các phần sai lệch nếu có.
3. **Structured Output Parser**: Đảm bảo báo cáo có cấu trúc Markdown chuẩn.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi một request POST đến URL Webhook (ví dụ: `http://<your-vps-ip>:5678/general-research`).
   - Dữ liệu mẫu:
     ```json
     {
       "query": "Tình hình thị trường AI tại Việt Nam năm 2024",
       "sources": ["linkedin", "twitter", "semantic-scholar"]
     }
     ```
2. **Bật Active workflow** sau khi kiểm tra kết quả.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[MỞ RỘNG THÊM CÔNG CỤ]
- **Thêm Google Sheets/Excel**: Kết nối với node `n8n-nodes-base.googleSheets` để lưu báo cáo tự động vào bảng tính.
- **Gửi báo cáo qua Slack/Telegram**: Sử dụng node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram` để thông báo kết quả.
- **Lưu log hoạt động**: Kết nối với `n8n-nodes-base.log` để theo dõi lịch sử request và kết quả.
- **Tự động hóa báo cáo định kỳ**: Sử dụng node `n8n-nodes-base.cron` để chạy workflow hàng tuần/tháng.
:::

:::tip[CẢI TIẾN ĐỘ CHÍNH XÁC]
- **Thêm mô hình AI khác**: Bạn có thể thay thế `openrouter/auto` bằng mô hình `mistral/mistral-7b` hoặc `google/gemini` nếu muốn.
- **Tăng giới hạn request**: Nếu Serper/ScrapingDog giới hạn request, đăng ký gói trả phí để tăng số lượng query.
- **Tối ưu prompt**: Nếu báo cáo không phù hợp, chỉnh sửa node `Set Prompt` để AI hiểu rõ yêu cầu hơn.
:::

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần nghiên cứu thị trường nhanh chóng, chính xác và tự động hóa. Bằng cách kết hợp **AI Agent thông minh (OpenRouter)**, **web search (Serper)**, và **scraping công cụ (Jina AI)**, bạn sẽ:
✔ **Tiết kiệm thời gian** so với cách làm thủ công.
✔ **Nhận báo cáo chuyên nghiệp** với cấu trúc logic và dễ đọc.
✔ **Đảm bảo độ tin cậy** nhờ hệ thống kiểm tra hallucination tự động.
✔ **Hoạt động 24/7** trên VPS riêng, không phụ thuộc vào người dùng.

**Hành động ngay hôm nay!**
1. **Đăng ký VPS** và cài đặt n8n.
2. **Import workflow** và cấu hình API Keys.
3. **Test run** với một query mẫu.
4. **Bật workflow** và tự động hóa nghiên cứu thị trường của bạn!

👉 **[Tải workflow ngay](https://n8n.io/workflows/12504)** và bắt đầu tự động hóa! 🚀