---
title: "🚀 Review PR Tự Động với GitHub, GPT‑4, và Google Sheets"
description: "Tự động nhận xét code khi PR được mở, giảm thời gian review và tăng độ chính xác nhờ AI."
slug: "review-pr-tu-dong-github-gpt4-google-sheets"
tags: [n8n, automation, no-code, github, openai, google-sheets]
keywords: [n8n workflow, tự động hóa, code review, GPT‑4, Google Sheets, GitHub]
---

# 🚀 Review PR Tự Động với GitHub, GPT‑4, và Google Sheets

Bạn đang phải chờ đợi hàng giờ, thậm chí cả ngày, để một thành viên trong team review pull request? Bạn muốn giảm thiểu lỗi, tăng tính nhất quán và vẫn giữ được tốc độ phát triển nhanh?  
Workflow này sẽ **đánh giá code ngay khi PR được mở**, gửi nhận xét tự động lên GitHub, và lưu trữ các best‑practice trong Google Sheets để AI luôn “đọc” đúng quy chuẩn của team.

:::info[Hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Review ngay khi PR được mở, giảm thời gian chờ 1‑2 ngày.  
- **Độ chính xác cao**: AI GPT‑4 hiểu ngữ cảnh, phát hiện lỗi logic, style, và đề xuất cải tiến.  
- **Cá nhân hóa**: Dùng Google Sheets để lưu quy chuẩn riêng của team, AI luôn “đọc” đúng.  
- **Hoạt động liên tục**: Không phụ thuộc vào thời gian làm việc của con người, 24/7.  
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **GitHub**:  
  - Tạo **OAuth2 App** → Credentials: `githubOAuth2Api` (để trigger & label).  
  - Tạo **Personal Access Token** → Credentials: `githubApi` (để post comment).  
- **OpenAI**:  
  - API Key → Credentials: `openAiApi` (để gọi GPT‑4o‑mini).  
- **Google Sheets**:  
  - Tạo Sheet chứa best‑practice → Credentials: `googleSheetsOAuth2Api`.  
- **LangChain**: Node `agent` đã được cài sẵn trong n8n.  
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥

1. Tải file JSON từ link gốc:  
   <https://n8n.io/workflows/3804> → `Download JSON`.  
2. Mở n8n Editor → `Import` → `Upload JSON` hoặc copy‑paste nội dung JSON vào ô `Import`.  
3. Nhấn **Import**.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Tên Node | Cấu hình cần chỉnh | Ghi chú |
|------|----------|---------------------|---------|
| `PR Trigger` | `githubTrigger` | **Repository** (đưa vào `Repository` field) | Trigger khi PR được mở. |
| `Get file's Diffs from PR` | `httpRequest` | **URL**: `https://api.github.com/repos/{{$json.body.sender.login}}/{{$json.body.repository.name}}/pulls/{{$json.body.number}}/files` | Đảm bảo `Authorization` header được tự động thêm bởi credential `githubOAuth2Api`. |
| `Create target Prompt from PR Diffs` | `code` | Kiểm tra script JS, không cần chỉnh. | Tạo prompt cho AI. |
| `Code Review Agent` | `agent` | **Prompt**: lấy từ node trước (`{{ $json.prompt }}`) | Đảm bảo `OpenAI Chat Model` được chọn. |
| `OpenAI Chat Model` | `lmChatOpenAi` | **Model**: `gpt-4o-mini` | Đặt API Key trong `openAiApi`. |
| `GitHub Robot` | `github` (resource: `review`) | **Comment**: lấy từ output của `agent`. | Post review comment. |
| `Add Label to PR` | `github` (operation: `edit`) | **Labels**: `ReviewedByAI` | Optional. |
| `Code Best Practices` | `googleSheetsTool` | **Sheet ID**: ID của Google Sheet chứa best‑practice. | AI sẽ đọc sheet này khi tạo prompt. |

> **Lưu ý**: Nếu bạn muốn thay thế Google Sheets bằng database khác, chỉ cần thay node `googleSheetsTool` bằng node tương ứng và cập nhật script tạo prompt.

### 3. Kích hoạt ⚡️

1. **Test run**: Chọn một PR mẫu, chạy workflow thủ công (`Execute Workflow`). Kiểm tra console logs, output của `agent` và comment trên PR.  
2. **Bật Active**: Khi mọi thứ hoạt động đúng, bật toggle `Active` ở góc trên bên phải. Workflow sẽ tự động chạy khi PR mới được mở.

## ✍️ Mẹo & gợi ý nâng cao

- **Slack/Telegram Notification**: Thêm node `slack` hoặc `telegram` để gửi thông báo khi AI đã review.  
- **Lưu log**: Dùng node `writeToFile` hoặc `googleSheetsTool` để ghi lại lịch sử review vào sheet riêng.  
- **Review định kỳ**: Thêm node `cron` để chạy review lại PR đã được đóng, kiểm tra lại code.  
- **Tùy chỉnh prompt**: Thêm biến `{{ $json.body.title }}` vào prompt để AI hiểu ngữ cảnh dự án.  

## 📌 Kết luận

Workflow này giúp các sếp **đưa AI vào quy trình code review** một cách nhanh chóng, dễ dàng và không cần viết code. Bạn chỉ cần cấu hình credential, import JSON, và bật workflow.  
Hãy thử ngay để thấy sự khác biệt: giảm thời gian review, tăng độ chính xác và giữ cho quy trình luôn “đi đúng hướng”.  

Chúc các sếp thành công! 🚀