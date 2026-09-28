---
title: "🚀 Tự Động Phân Loại & Chuyển GitHub Issues Thành Jira Tickets Với OpenAI"
description: "Workflow n8n tự động nhận GitHub Issues, phân loại bug hay task bằng AI, rồi tạo ticket Jira tương ứng, giảm 100% công việc thủ công."
slug: "tu-dong-phan-loai-chuyen-github-issues-thanh-jira-tickets"
tags: [n8n, automation, no-code, project-management, ai, jira, github]
keywords: [n8n workflow, tự động hóa, GitHub Issues, Jira tickets, OpenAI, AI summarization]
---

# 🚀 Tự Động Phân Loại & Chuyển GitHub Issues Thành Jira Tickets Với OpenAI

Khi các dự án phần mềm phát triển nhanh, **GitHub Issues** thường tràn ngập và việc tạo **Jira tickets** thủ công gây tốn thời gian, dễ sai sót và làm chậm tiến độ. Các sếp thường phải dành hàng giờ mỗi tuần để:
- Kiểm tra từng issue, xác định nó là bug hay task.
- Sao chép nội dung, mô tả, và gán đúng loại ticket trong Jira.
- Đảm bảo thông tin luôn đồng bộ giữa hai hệ thống.

**Giải pháp:** Workflow n8n “Classify and Convert GitHub Issues to Jira Tickets with OpenAI” tự động lắng nghe các issue mới trên GitHub, dùng OpenAI phân loại và tóm tắt, sau đó tạo ticket Jira tương ứng (Bug hoặc Task) chỉ trong vài giây. Không cần viết code, chỉ cần cấu hình một lần và để nó chạy 24/7.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Tự động tạo ticket ngay khi issue được mở.  
- **Độ chính xác cao:** AI phân loại và tóm tắt nội dung, giảm lỗi nhập liệu.  
- **Đồng bộ liên tục:** Không còn mất đồng bộ giữa GitHub và Jira.  
- **Tùy biến linh hoạt:** Dễ dàng mở rộng thêm các bước xử lý (gửi thông báo, lưu log...).  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản GitHub** với quyền **Read** (hoặc **Read & Write** nếu muốn phản hồi).  
- **Tài khoản Jira** (Cloud hoặc Server) với quyền **Create Issue** trong dự án mục tiêu.  
- **API Key OpenAI** (hoặc OpenAI Organization + API Key) để sử dụng mô hình ChatGPT.  
- **n8n** đã cài đặt và truy cập được UI (Self‑hosted hoặc n8n.cloud).  
- (Tùy chọn) **Credential** cho Slack/Telegram nếu muốn nhận thông báo.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow (từ link gốc hoặc file đính kèm).  
2. Vào **n8n → Workflows → Import** → Chọn file JSON → **Import**.  
3. Hoặc mở **n8n Editor**, nhấn **+** → **Import from Clipboard**, dán toàn bộ JSON và **Import**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là các node quan trọng và cách cấu hình:

| Node | Loại | Cấu hình cần làm |
|------|------|------------------|
| **GitHub Trigger** | `githubTrigger` | - Chọn **Credential**: GitHub OAuth (cung cấp token). <br> - Event: **Issue Created** (hoặc **Issue Updated** tùy nhu cầu). |
| **Is it a bug?** | `if` | - Điều kiện: `{{$json["labels"]?.some(l => l.name.toLowerCase().includes("bug"))}}` <br> - Nếu **True** → đi tới **Create Jira Ticket (Bug)**, ngược lại → **Create Jira Ticket (Task)**. |
| **Create Jira Ticket (Bug)** | `jira` | - Credential: **Jira API** (email + API token). <br> - Project Key: nhập key dự án bug. <br> - Issue Type: **Bug**. <br> - Summary & Description: dùng output của **Structured Output Parser** (fields `title`, `description`). |
| **Create Jira Ticket (Task)** | `jira` | - Credential: **Jira API** (cùng như trên). <br> - Project Key: key dự án task. <br> - Issue Type: **Task**. <br> - Summary & Description: lấy từ parser. |
| **AI Agent** | `agent` (LangChain) | - **Model**: trỏ tới **OpenAI Chat Model** node. <br> - Prompt: “Phân loại issue này là Bug hay Task và tạo tiêu đề, mô tả ngắn gọn cho Jira.” <br> - Output: JSON với các trường `type`, `title`, `description`. |
| **OpenAI Chat Model** | `lmChatOpenAi` | - Credential: **OpenAI API Key**. <br> - Model: `gpt-4o-mini` (hoặc `gpt-3.5-turbo`). <br> - Temperature: `0.2` để có kết quả ổn định. |
| **Simple Memory** | `memoryBufferWindow` | - Giữ lại **2** tin nhắn cuối để ngữ cảnh cho AI (không bắt buộc thay đổi). |
| **Structured Output Parser** | `outputParserStructured` | - Schema JSON: <br>```json { "type": "string", "title": "string", "description": "string" }``` <br> - Đảm bảo output của **AI Agent** khớp schema này. |

> **Lưu ý:** Đảm bảo **Credential** cho GitHub, Jira và OpenAI đã được tạo trong n8n → **Credentials** trước khi gán vào node.

#### 3. Kích hoạt ⚡️
1. Nhấn **Execute Workflow** với một issue mẫu để kiểm tra.  
2. Kiểm tra kết quả trong **Jira** và **GitHub** (có thể thêm comment để xác nhận).  
3. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên bên phải) để workflow chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram:** Thêm node **Slack** hoặc **Telegram** sau mỗi ticket được tạo để báo cho team ngay lập tức.  
- **Lưu log vào Google Sheets:** Dùng node **Google Sheets** để ghi lại ID issue, ID ticket, thời gian tạo – tiện cho báo cáo.  
- **Báo cáo định kỳ:** Kết hợp **Cron** + **Jira Search** để gửi báo cáo tổng hợp số ticket mới mỗi tuần.  
- **Kiểm soát ngưỡng:** Thêm node **If** để chỉ tạo ticket khi issue có mức độ ưu tiên cao (label “high”, “critical”).  

### 📌 Kết luận
Với workflow này, các sếp có thể **loại bỏ hoàn toàn công đoạn sao chép thủ công**, giảm lỗi và tăng tốc độ phản hồi cho đội phát triển. Hãy triển khai ngay, tùy chỉnh theo quy trình nội bộ và để n8n làm việc thay bạn 24/7! 🚀