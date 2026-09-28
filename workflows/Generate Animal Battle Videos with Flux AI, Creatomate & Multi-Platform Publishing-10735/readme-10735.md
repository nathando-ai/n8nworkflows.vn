---
title: "🚀 Tạo Video Trận Đấu Động Vật Tự Động với Flux AI, Creatomate & Đăng Tải Đa Nền Tảng"
description: "Giải pháp tự động tạo video trận đấu động vật, từ ý tưởng đến xuất bản trên Instagram, TikTok, YouTube mà không cần viết code."
slug: "tac-vien-dang-video-tran-dau-dong-vat-tot-dung"
tags: [n8n, automation, no-code, ai, video, content-creation, multi-platform]
keywords: [n8n workflow, tự động hóa, video, AI, Creatomate, Flux AI, multi-platform publishing]
---

# 🚀 Tạo Video Trận Đấu Động Vật Tự Động với Flux AI, Creatomate & Đăng Tải Đa Nền Tảng

Bạn đang phải mất hàng giờ lên kế hoạch, tạo kịch bản, vẽ storyboard, dựng video, rồi đăng lên nhiều nền tảng?  
Workflow này sẽ biến “điều chỉnh thủ công” thành “điều khiển tự động 100%” – từ Google Sheet nhập dữ liệu, AI sinh kịch bản, hình ảnh, video, tới tự động đăng lên Instagram, TikTok, YouTube.  

:::info[Hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ 8‑12h → 30 phút.  
- **Độ chính xác cao**: AI sinh kịch bản, hình ảnh, video dựa trên dữ liệu thực tế.  
- **Tự động hóa liên tục**: Đăng lên 3 nền tảng mà không cần can thiệp.  
- **Tăng tương tác**: Video chất lượng, nội dung hấp dẫn, thời gian phát sóng tối ưu.  
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
| Dịch vụ | Mô tả | Credentials cần thiết |
|---------|-------|------------------------|
| **Google Sheets** | Tài liệu nhập dữ liệu nhân vật, kịch bản, kết quả | Google API key (OAuth 2.0) |
| **OpenRouter** | ChatGPT 4.1 mini & 4.1 | `openRouterApi` key |
| **PiAPi** | Tạo hình ảnh AI | API key |
| **Creatomate** | Render video dựa template | `Creatomate API key`, `Template ID`, `Account ID` |
| **Blotato** | Đăng lên Instagram, TikTok, YouTube | API key |
| **Schedule Trigger** | Lịch tự động | Không cần credential |
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON từ link gốc: <https://n8n.io/workflows/10735>.  
2. Trong n8n Editor, chọn **Import** → **Upload JSON** hoặc **Paste JSON**.  
3. Xác nhận import, workflow sẽ xuất hiện trong danh sách.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên node | Hướng dẫn cấu hình |
|------|----------|---------------------|
| **Get Main Character** | `googleSheets` | Chọn sheet “Main Character”, cột dữ liệu cần. |
| **Scene Creator** | `agent` | Đưa prompt “Generate scenes for animal battle” vào. |
| **GPT 4.1-mini** | `lmChatOpenRouter` | Chọn credential `openRouterApi`. |
| **Image Prompt Generator** | `agent` | Prompt “Generate image prompt for each scene”. |
| **Winner Image Prompt** | `agent` | Prompt “Generate winner image prompt”. |
| **Render Video** | `httpRequest` | URL endpoint của Creatomate, truyền template ID. |
| **Get Video** | `httpRequest` | Lấy URL video đã render. |
| **Upload to Blotato** | `httpRequest` | API endpoint Blotato, truyền token. |
| **Instagram / TikTok / YouTube** | `httpRequest` | Đăng video lên từng nền tảng, cấu hình tiêu đề, hashtag. |
| **Schedule Trigger** | `scheduleTrigger` | Đặt lịch (ví dụ: hàng ngày lúc 08:00). |
| **Google Sheets (update)** | `googleSheets` | Cập nhật cột “Video URL”, “Status” sau khi đăng. |

> **Lưu ý**: Mỗi node `httpRequest` cần cấu hình `Authentication` (Bearer token) và `Body Parameters` theo tài liệu API của dịch vụ tương ứng.

### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow với dữ liệu mẫu (đảm bảo các API key hoạt động).  
2. Kiểm tra log, xác nhận video được tạo và URL xuất hiện trong Google Sheet.  
3. Khi mọi thứ ổn, bật **Active** cho workflow.  
4. Đảm bảo VPS hoặc môi trường hosting có kết nối internet ổn định.

## ✍️ Mẹo & gợi ý nâng cao

:::tip[Đẩy mạnh hiệu quả]
- **Slack/Telegram notifications**: Thêm node `Slack` hoặc `Telegram` để nhận thông báo khi video hoàn thành.  
- **Log to Google Sheets**: Ghi lại thời gian, trạng thái, lỗi để phân tích sau.  
- **Custom prompts**: Thay đổi prompt trong `Scene Creator` để tạo nội dung đa dạng (ví dụ: “Add comedic twist”).  
- **Scheduled publishing**: Sử dụng `Schedule Trigger` để đăng video vào thời điểm cao điểm người dùng.  
:::

## 📌 Kết luận

Workflow “Generate Animal Battle Videos with Flux AI, Creatomate & Multi-Platform Publishing” là công cụ mạnh mẽ giúp các sếp tiết kiệm thời gian, giảm chi phí và tăng tương tác trên mạng xã hội.  
Hãy thử ngay, tùy chỉnh prompt và template cho phù hợp với thương hiệu của mình, và quan sát doanh thu tăng lên!

---

## 🛠️ Setup Guide  
**Author: [Jadai kongolo](https://www.instagram.com/jadai_ai_automation/)**

1. **Google Sheet**  
   - Tạo bản sao của mẫu: <https://docs.google.com/spreadsheets/d/1hBjE1LR5rmSlEkwkNIwf_NnbjBS_cALS5FJ0r6vh7nM/edit?usp=sharing>.  
   - Kết nối 5 node `googleSheets` trong workflow với sheet này (đặt `Sheet ID`, `Range`, `Operation`).

2. **OpenRouter**  
   - Đăng ký tại <https://openrouter.ai/>.  
   - Nhập API key vào hai node `lmChatOpenRouter` (`GPT 4.1-mini` & `GPT 4.1`).

3. **PiAPi**  
   - Tạo tài khoản tại <https://piapi.ai/workspace>.  
   - Kết nối API key vào node `agent` “Image Prompt Generator”.

4. **Creatomate**  
   - Đăng ký tại <https://creatomate.com/>.  
   - Lấy `Template ID` và `Account ID`, nhập vào node `httpRequest` “Render Video”.  
   - Sử dụng mã nguồn template giống trong video (được chia sẻ trong Skool post).

5. **Blotato**  
   - Tạo tài khoản tại <https://blotato.com/>.  
   - Nhận API key, cấu hình node `httpRequest` “Upload to Blotato” và các node “Instagram”, “TikTok”, “YouTube”.

6. **Schedule Trigger**  
   - Đặt lịch chạy tự động (ví dụ: hàng ngày lúc 08:00).  
   - Kiểm tra log để đảm bảo workflow không bị timeout.

> **Tip**: Nếu gặp lỗi “Rate limit exceeded”, hãy giảm tần suất gọi API hoặc nâng cấp gói dịch vụ.

---