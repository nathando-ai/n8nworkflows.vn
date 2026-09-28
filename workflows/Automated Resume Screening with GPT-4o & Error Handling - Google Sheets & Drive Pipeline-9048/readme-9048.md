---
title: "🚀 AI Tự Động Xử Lý Hồ Sơ Đơn Việc & Đánh Giá Ứng Viên"
description: "Giải pháp tự động hóa 100% nhận hồ sơ, phân tích bằng GPT-4o, ghi nhận dữ liệu vào Google Sheets và gửi thông báo lỗi ngay khi có sự cố."
slug: "ai-tu-dong-xu-ly-ho-so-don-viec"
tags: [n8n, automation, no-code, HR, AI]
keywords: [n8n workflow, tự động hóa, AI tuyển dụng, GPT-4o, xử lý hồ sơ, resume screening]
---

# 🚀 AI Tự Động Xử Lý Hồ Sơ Đơn Việc & Đánh Giá Ứng Viên

Bạn đang phải xử lý hàng trăm hồ sơ mỗi ngày? Mỗi lần mở file, trích xuất thông tin, so sánh với yêu cầu công việc và ghi nhận vào bảng tính là một công việc tốn thời gian và dễ sai sót. Workflow này sẽ giúp bạn:

- **Nhận hồ sơ tự động** từ Gmail.
- **Xử lý đa dạng định dạng** (PDF, DOCX, TXT) chỉ bằng một chuỗi logic.
- **Phân tích bằng GPT‑4o** để đánh giá ứng viên, so sánh kỹ năng, kinh nghiệm và văn hóa phù hợp.
- **Ghi nhận dữ liệu** vào Google Sheets một cách chính xác.
- **Xử lý lỗi** ngay lập tức: gửi email cảnh báo, ghi log và tránh mất dữ liệu.

:::info[Hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: giảm 70% công việc thủ công.  
- **Độ chính xác cao**: AI phân tích dữ liệu, giảm sai sót do con người.  
- **Tự động hóa liên tục**: chạy 24/7 mà không cần can thiệp.  
- **Cảnh báo kịp thời**: email thông báo lỗi ngay khi có sự cố.  
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **Tài khoản Gmail** (đã bật OAuth2).  
- **Google Drive** (đã cấp quyền đọc/ghi).  
- **Google Sheets** (đã tạo bảng tính mẫu).  
- **OpenAI API key** (đã bật GPT‑4o).  
- **Email nhận thông báo lỗi** (được cấu hình trong node “Send Error Notification”).  
:::

## 🚀 Cách import & Lưu ý khi “lên đồ”

### 1. Import Workflow 📥

1. Tải file JSON từ link gốc: <https://n8n.io/workflows/9048>.  
2. Trong n8n Editor, chọn **Import** → **Upload JSON** hoặc **Paste JSON**.  
3. Nhấn **Import** và workflow sẽ xuất hiện trong danh sách.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Tên Node | Mô tả | Cài đặt cần chỉnh |
|------|----------|-------|--------------------|
| 1 | Monitor Resumes | Gửi email Gmail có đính kèm hồ sơ | Credentials: `gmailOAuth2` |
| 2 | Save to Drive | Lưu file vào Google Drive | Credentials: `googleDriveOAuth2Api` |
| 3 | Upload Success? | Kiểm tra upload thành công | Không cần chỉnh |
| 4 | Route by File Type | Chọn đường dẫn dựa trên MIME type | Không cần chỉnh |
| 5 | Extract PDF Text | Trích xuất nội dung PDF | Không cần chỉnh |
| 6 | Convert DOCX to Docs | Chuyển DOCX sang Google Docs | Credentials: `googleDriveOAuth2Api` |
| 7 | Get Doc as Text | Tải nội dung Google Docs | Không cần chỉnh |
| 8 | Download TXT | Tải file TXT | Không cần chỉnh |
| 9 | Extract TXT Content | Trích xuất nội dung TXT | Không cần chỉnh |
| 10 | Text Extracted? | Kiểm tra trích xuất thành công | Không cần chỉnh |
| 11 | Standardize Resume Data | Chuẩn hoá dữ liệu | Định dạng trường dữ liệu (JSON) |
| 12 | Resume Quality Check | Kiểm tra chất lượng hồ sơ | Định nghĩa tiêu chí (độ dài, có CV, v.v.) |
| 13 | Job Description | Định nghĩa mô tả công việc | Cập nhật nội dung mô tả |
| 14 | AI Recruiter Analysis | Gửi prompt tới GPT‑4o | Credentials: `openAiApi` |
| 15 | Structured Output Parser | Phân tích JSON trả về | Định nghĩa schema (JSON Schema) |
| 16 | GPT‑4o Model | Chọn mô hình GPT‑4o-mini | Đảm bảo key `model` = `gpt-4o-mini` |
| 17 | AI Analysis Success? | Kiểm tra thành công AI | Không cần chỉnh |
| 18 | Extract Candidate Info | Trích xuất thông tin ứng viên | Định nghĩa trường (tên, email, phone, v.v.) |
| 19 | Final Data Valid? | Kiểm tra dữ liệu cuối cùng | Định nghĩa tiêu chí |
| 20 | Log Successful Processing | Ghi dữ liệu vào Google Sheets | Credentials: `googleSheetsOAuth2Api` |
| 21‑25 | Set Upload/Error… | Định nghĩa thông báo lỗi | Đặt nội dung email, sheet columns |
| 26 | Merge All Errors | Kết hợp lỗi | Không cần chỉnh |
| 27 | Send Error Notification | Gửi email lỗi | Credentials: `gmailOAuth2` |
| 28 | Log Error to Sheet | Ghi lỗi vào Google Sheets | Credentials: `googleSheetsOAuth2Api` |
| 29 | Get Doc | Tải lại file nếu cần | Không cần chỉnh |

> **Lưu ý**: Mỗi node “Set” và “If” cần cấu hình đúng trường dữ liệu (field names) để workflow hoạt động trơn tru. Kiểm tra kỹ các “Output” của node trước khi chuyển sang node tiếp theo.

### 3. Kích hoạt ⚡️

1. **Test run**: Chạy workflow với một email mẫu có đính kèm file PDF/DOCX/TXT.  
2. Kiểm tra Google Drive, Google Sheets và email inbox để xác nhận dữ liệu đã ghi nhận.  
3. Khi mọi thứ ổn, bật **Active** cho workflow.

## ✍️ Mẹo & gợi ý nâng cao

- **Slack/Telegram**: Thêm node “Slack” hoặc “Telegram” để nhận thông báo lỗi ngay tức thì.  
- **Lưu log chi tiết**: Sử dụng node “Write Binary Data” để lưu file log vào Drive.  
- **Báo cáo định kỳ**: Thêm node “Cron” + “Google Sheets” để gửi báo cáo hàng ngày/tuần.  
- **Tùy chỉnh AI**: Thay đổi prompt trong node “AI Recruiter Analysis” để phù hợp với từng vị trí công việc.  
- **Phân loại ứng viên**: Thêm node “Switch” sau “Structured Output Parser” để phân loại “Top”, “Consider”, “Reject” và ghi vào các sheet riêng.

## 📌 Kết luận

Workflow “Automated Resume Screening with GPT‑4o” là giải pháp hoàn hảo cho các bộ phận HR, agency tuyển dụng và startup muốn **tối ưu hoá quy trình tuyển dụng** mà không cần viết code. Với khả năng xử lý đa dạng file, AI phân tích chuyên sâu và hệ thống cảnh báo lỗi mạnh mẽ, các sếp sẽ tiết kiệm thời gian, giảm sai sót và tập trung vào quyết định chiến lược.  

Hãy **đưa workflow vào thực tiễn ngay hôm nay** và trải nghiệm sự tự động hóa 100%!