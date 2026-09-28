---
title: "🚀 Tự động hóa tóm tắt Jira hàng ngày & Báo cáo tuần với Azure OpenAI và Gmail"
description: "Hướng dẫn sử dụng n8n workflow giúp tự động tổng hợp công việc Jira cuối ngày bằng AI, lưu trữ vào Google Sheets và gửi báo cáo tuần qua Gmail chuyên nghiệp."
slug: "tu-dong-hoa-tom-tat-jira-hang-ngay-va-bao-cao-tuan-azure-openai-gmail"
tags: [n8n, automation, no-code, jira, openai, gmail, google-sheets]
keywords: [n8n workflow, tóm tắt jira tự động, azure openai, báo cáo tuần jira, tự động hóa n8n]
---

# 🚀 Tự động hóa tóm tắt Jira hàng ngày & Báo cáo tuần với Azure OpenAI và Gmail

Việc tổng hợp báo cáo tiến độ công việc (End-of-Day report) từ Jira và viết báo cáo tuần (Weekly Report) gửi sếp hoặc các stakeholders thường ngốn rất nhiều thời gian của các Team Lead và Project Manager mỗi ngày. Việc làm thủ công này dễ dẫn đến sai sót, quên nhiệm vụ hoặc mất thời gian cấu trúc lại dữ liệu.

Được thiết kế bởi chuyên gia **Rahul Joshi**, workflow n8n này sẽ giải quyết triệt để vấn đề trên bằng cách tự động hóa 100%: Lấy dữ liệu Jira, dùng AI (Azure OpenAI) phân tích, lưu trữ lịch sử vào Google Sheets và tự động gửi báo cáo qua Gmail vào cuối tuần. Các sếp không cần phải viết code một dòng nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 5+ giờ mỗi tuần:** Không còn mất công lọc ticket Jira, gom nhóm task hay gõ báo cáo thủ công.
- **Báo cáo chuyên nghiệp:** Sử dụng sức mạnh của Azure OpenAI (GPT-4o-mini) để phân tích chi tiết trạng thái, mức độ ưu tiên và người thực hiện một cách mạch lạc, sắc bén.
- **Lưu trữ minh bạch:** Tự động ghi nhận tóm tắt hàng ngày vào Google Sheets để làm dữ liệu nền tảng cho báo cáo tuần.
- **Tự động hóa toàn trình:** Chạy ngầm định kỳ vào mỗi tối làm việc (Daily) và tối thứ Sáu (Weekly) mà không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và thông tin kết nối (Credentials) sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Jira Software Cloud Account** (API Token / OAuth).
- **Azure OpenAI Service Account** (với mô hình `gpt-4o-mini` đã được deploy).
- **Google Sheets Account** (Tạo sẵn một file Sheet để lưu nhật ký công việc).
- **Gmail Account** (Kết nối qua OAuth2 để gửi email).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Copy đoạn mã JSON của workflow này (hoặc tải file JSON từ n8n template 9683), sau đó dán trực tiếp vào giao diện n8n Editor của các sếp qua tính năng **Import from JSON**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các thông số quan trọng sau trong các node:
- **Get ALL issues (Jira):** Kết nối tài khoản Jira Cloud của doanh nghiệp, cấu hình lấy danh sách các issue trong ngày theo project cần theo dõi.
- **Azure OpenAI Chat Model / Chat Model1:** Chọn credential Azure OpenAI, xác thực thông tin Endpoint, API Key và chọn đúng model `gpt-4o-mini`.
- **Append Summary & Get all stored data (Google Sheets):** Trỏ tới file Google Sheet chuẩn bị sẵn, chọn đúng Sheet Name để workflow ghi dữ liệu EOD (End-of-Day) và đọc lại dữ liệu cho báo cáo tuần.
- **Email to Stakeholders (Gmail):** Kết nối tài khoản Gmail cá nhân hoặc Workspace, điền danh sách người nhận (Stakeholders) ở phần cài đặt gửi email.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** chạy thử thủ công một lần với Daily Evening Trigger hoặc Friday Evening Trigger để kiểm tra kết quả trả về từ Jira và AI.
- Sau khi test thành công, bật công tắc **Active** góc trên cùng bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh chat:** Bổ sung thêm node Telegram hoặc Slack ở bước cuối để bắn thông báo tóm tắt nóng lên group chat nội bộ ngay sau khi AI tạo xong báo cáo.
- **Tùy biến Prompt AI:** Các sếp có thể điều chỉnh system prompt bên trong các AI Agent (`Create Summary`, `Create Weekly Summary`) để AI viết báo cáo theo văn phong riêng của công ty (Thân thiện, nghiêm túc, hoặc báo cáo OKRs chi tiết).
- **Mở rộng nguồn dữ liệu:** Kết nối thêm Trello, Asana hoặc GitHub vào cùng luồng nếu team sử dụng nhiều công cụ quản lý dự án khác nhau.

### 📌 Kết luận
Workflow tự động hóa tóm tắt Jira và báo cáo tuần bằng Azure OpenAI này là mảnh ghép hoàn hảo giúp các đội ngũ kỹ thuật và quản lý tối ưu hóa thời gian, nâng cao tính minh bạch trong công việc. Hãy cài đặt ngay lên hệ thống n8n của các sếp để giải phóng sức lao động thủ công ngay hôm nay!