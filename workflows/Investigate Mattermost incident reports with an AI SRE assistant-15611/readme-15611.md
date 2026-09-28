---
title: "🚀 Tự động hóa điều tra sự cố hạ tầng với AI SRE Assistant trên Mattermost"
description: "Hướng dẫn cài đặt workflow n8n tích hợp AI Agent, Qdrant Vector Store và các công cụ MCP để tự động phân tích, chẩn đoán sự cố hạ tầng từ Mattermost."
slug: "tu-dong-hoa-dieu-tra-su-co-ha-tang-ai-sre-assistant-mattermost"
tags: [n8n, automation, ai-agent, devops, sre, mattermost]
keywords: [n8n workflow, ai sre assistant, mattermost automation, qdrant vector store, mcp servers, devops automation]
---

# 🚀 Tự động hóa điều tra sự cố hạ tầng với AI SRE Assistant trên Mattermost

Các sếp làm DevOps hay SRE chắc chắn đã quá quen thuộc với cảnh nửa đêm nhận thông báo lỗi trên kênh chat, sau đó phải bì bõm nhảy vào Grafana, Kubernetes logs, GitHub commits để truy tìm nguyên nhân. Quá trình này vừa mất thời gian, vừa áp lực. 

Giải pháp cho các sếp đây: một workflow n8n đóng vai trò như một **AI SRE Assistant** chuyên nghiệp. Khi có người dùng báo cáo sự cố trên Mattermost, trợ lý AI này sẽ tự động thu thập ngữ cảnh, tra cứu cơ sở tri thức (Knowledge Base) qua Qdrant, kết nối với các hệ thống giám sát qua giao thức MCP (Model Context Protocol) và tự động phản hồi một báo cáo chẩn đoán chi tiết ngay trong thread thảo luận.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Báo cáo chuẩn 4 phần**: Nhận ngay bản tóm tắt sự cố (What happened), dòng thời gian (Event timeline), nguyên nhân gốc rễ (Root cause) và hướng khắc phục (Troubleshooting tips).
- **Tự động hóa 100%**: Giảm thiểu thời gian MTTR (Mean Time To Resolution) bằng cách tự động hóa khâu thu thập log và tra cứu tài liệu kỹ thuật.
- **Tích hợp sâu hệ thống**: Kết nối mượt mà với Grafana, Kubernetes, DigitalOcean, GitHub và Mattermost thông qua MCP servers.
- **Hoạt động liên tục 24/7**: Trợ lý AI luôn sẵn sàng phân tích ngay khi sự cố vừa chớm nở trên kênh chat.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (Khuyến nghị bản self-hosted).
- **API Keys**: 
  - OpenRouter / OpenAI / Anthropic API Key (cho AI Agent Model).
  - Google Gemini API Key (cho Embeddings).
  - Mattermost API Credentials.
- **Cơ sở dữ liệu Vector**: Qdrant Vector Store instance chứa tài liệu hạ tầng, runbook, service map.
- **MCP Servers**: Các remote MCP servers đã được cấu hình (Grafana, GitHub, Kubernetes, DigitalOcean, Mattermost).
- **Sub-workflow**: Một sub-workflow xử lý file đính kèm (`attachmentsAnalyzer`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp hãy lấy mã JSON của workflow từ tác giả Sergei Byvshev (ID: 15611) và import trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp cần cấu hình chính xác các thành phần sau:
- **OpenRouter Chat Model**: Chọn credentials `openRouterApi` và cấu hình model (ví dụ: `openai/gpt-5.3-codex` hoặc model phù hợp).
- **Embeddings Google Gemini**: Cấu hình credentials `googlePalmApi` để xử lý vector embeddings.
- **Qdrant Vector Store**: Kết nối với instance Qdrant của các sếp bằng credentials `qdrantApi` để AI có thể đọc tài liệu nội bộ.
- **Các MCP Client Tools (Grafana, DigitalOcean, K8S, Github, Mattermost)**: Cập nhật URL chính xác của các remote MCP servers tương ứng:
  - [grafana-mcp](https://github.com/grafana/mcp-grafana)
  - [github-mcp](https://github.com/github/github-mcp-server)
  - [kubernetes-mcp-server](https://github.com/containers/kubernetes-mcp-server)
  - [mattermost-mcp](https://github.com/cloud-ru-tech/mcp-server-mattermost)
  - [digitalocean-mcp](https://github.com/digitalocean/digitalocean-mcp)
- **Call 'attachmentsAnalyzer'**: Thay thế tham chiếu sub-workflow bằng sub-workflow xử lý hình ảnh/file đính kèm thực tế của hệ thống các sếp (`file_ids[]`).
- **AI Agent System Prompt**: Tinh chỉnh prompt hệ thống trong node `AI Agent` để thêm quy ước đặt tên dự án, thông tin sở hữu dịch vụ (ownership), quy tắc leo thang sự cố (escalation rules) và đặc thù hạ tầng công ty các sếp.

#### 3. Kích hoạt ⚡️
- Gửi payload thử nghiệm từ workflow cha thông qua trigger `When Executed by Another Workflow`.
- Kiểm tra kết quả trả về trên luồng Mattermost thread.
- Bật công tắc **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu lịch sử sự cố**: Kết hợp thêm node lưu log vào Google Sheets hoặc Notion để tổng hợp các sự cố hàng tuần.
- **Cảnh báo đa kênh**: Tích hợp thêm bước gửi thông báo song song lên kênh Telegram hoặc Slack của đội ngũ quản lý nếu mức độ sự cố nghiêm trọng.
- **Tự động tạo Jira Ticket**: Thêm nhánh gọi API tạo Task/Bug trên Jira nếu AI Agent xác định đây là một lỗi cần fix code hoặc cấu hình.

### 📌 Kết luận
Với workflow **AI SRE Assistant** này, việc điều tra sự cố hạ tầng không còn là cơn ác mộng giữa đêm. Hãy triển khai ngay lên hệ thống n8n của các sếp để tối ưu hóa quy trình vận hành và tiết kiệm hàng giờ đồng hồ troubleshooting thủ công!