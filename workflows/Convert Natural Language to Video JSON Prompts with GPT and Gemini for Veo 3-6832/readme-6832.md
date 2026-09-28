---
title: "🚀 Tự động chuyển ngôn ngữ tự nhiên thành Prompt JSON Video với GPT & Gemini cho Veo 3"
description: "Giải pháp workflow n8n giúp doanh nghiệp chuyển văn bản thành prompt JSON video một cách nhanh chóng, chính xác và không cần viết code."
slug: "tuy-dong-chuyen-ngon-ngu-tu-nhiem-thanh-prompt-json-video-gpt-gemini-veo-3"
tags: [n8n, automation, no-code, ai, video, content-creation]
keywords: [n8n workflow, tự động hóa, prompt video, GPT, Gemini, Veo 3]
---

# 🚀 Tự động chuyển ngôn ngữ tự nhiên thành Prompt JSON Video với GPT & Gemini cho Veo 3

Bạn đang phải mất hàng giờ để viết prompt cho video, chỉnh sửa lại nhiều lần, và vẫn chưa đạt được độ chính xác mong muốn? Workflow này sẽ giúp bạn **đưa ý tưởng thành prompt JSON video chỉ trong vài phút**, đồng thời tận dụng sức mạnh của GPT (Azure OpenAI) và Gemini (Google) để tạo nội dung đa phương tiện chất lượng cao. Không cần viết code, chỉ cần cấu hình một vài credential và chạy workflow.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài giờ viết prompt → chỉ vài phút tạo prompt JSON.
- **Độ chính xác cao**: GPT và Gemini cùng làm việc, giảm lỗi ngữ cảnh.
- **Tự động hóa 100%**: Không cần thao tác thủ công, workflow chạy liên tục.
- **Tích hợp dễ dàng**: Dễ dàng kết nối với Veo 3 hoặc bất kỳ nền tảng video nào hỗ trợ JSON prompt.
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
| Dịch vụ | Credential | Mô tả |
|---------|------------|-------|
| **Google Gemini** | `googlePalmApi` | API key từ Google Cloud (Palm). |
| **Azure OpenAI** | `azureOpenAiApi` | API key và endpoint Azure OpenAI. |
| **OpenRouter** | `openRouterApi` | API key từ OpenRouter (đối với fallback). |
| **Veo 3** | - | API hoặc endpoint của Veo 3 (nếu cần). |
| **n8n** | - | Đăng ký tài khoản n8n (Self-hosted hoặc n8n.cloud). |

> **Lưu ý**: Đảm bảo các key có quyền truy cập đầy đủ (đọc/viết) và đã được kích hoạt.

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥

1. Tải file JSON workflow từ link gốc: <https://n8n.io/workflows/6832>.
2. Trong n8n Editor, chọn **Import** → **Upload JSON** hoặc **Paste JSON**.
3. Nhấn **Import** để tải workflow vào workspace.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Tên Node | Tham số cần cấu hình | Hướng dẫn |
|------|----------|----------------------|-----------|
| 1 | `Prompt Input` | `chatTrigger` | Định nghĩa trigger khi nhận prompt từ người dùng (ví dụ: webhook, Slack, Telegram). |
| 2 | `Prompt converter` | `chainLlm` | Chọn **LLM**: `Azure OpenAI` (model `gpt`). Đặt prompt template: “Chuyển văn bản sau thành JSON prompt cho Veo 3: {{$json.text}}”. |
| 3 | `Openai` | `lmChatAzureOpenAi` | Chọn credential `azureOpenAiApi`. Đặt **Model**: `gpt`. |
| 4 | `Alternative` | `lmChatOpenRouter` | Chọn credential `openRouterApi`. Đặt **Model**: `gpt-4o`. Đây là fallback nếu Azure không phản hồi. |
| 5 | `Json parser` | `outputParserStructured` | Đặt **JSON Path**: `$.output` (để lấy output từ node trước). |
| 6 | `Generate a video` | `googleGemini` | Chọn credential `googlePalmApi`. Đặt **Resource**: `video`. Prompt: `={{ JSON.stringify($json.output) }}` (đưa JSON prompt vào). |

> **Tip**: Kiểm tra **Output** của từng node trong tab **Execute Workflow** để đảm bảo dữ liệu truyền đúng.

### 3. Kích hoạt ⚡️

1. **Test run**: Nhấn **Execute Workflow** với dữ liệu mẫu (ví dụ: “Tạo video giới thiệu sản phẩm X với phong cách năng động”). Xem kết quả tại tab **Execution**.
2. Nếu mọi node chạy thành công, bật **Active** để workflow tự động chạy khi trigger xảy ra.

## ✍️ Mẹo & gợi ý nâng cao

- **Kết nối Slack**: Thêm node Slack để nhận prompt từ kênh, gửi kết quả trả về ngay.
- **Lưu log**: Thêm node Google Sheets hoặc Airtable để ghi lại prompt, JSON prompt, và link video tạo.
- **Báo cáo định kỳ**: Sử dụng node **Cron** để gửi báo cáo hàng ngày về số video đã tạo.
- **Tùy chỉnh prompt**: Thêm node **Set** để thêm metadata (tiêu đề, tags) trước khi gửi tới Gemini.

## 📌 Kết luận

Workflow “Convert Natural Language to Video JSON Prompts with GPT and Gemini for Veo 3” là công cụ **đột phá** giúp các sếp chuyển đổi ý tưởng thành nội dung video một cách nhanh chóng, chính xác và hoàn toàn tự động. Hãy thử ngay, tích hợp vào quy trình làm việc hiện tại và cảm nhận sự khác biệt!

---