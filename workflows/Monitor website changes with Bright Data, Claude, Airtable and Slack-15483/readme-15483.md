---
title: "🚀 Tự động giám sát thay đổi website đối thủ bằng Bright Data, Claude AI và Slack"
description: "Hướng dẫn cài đặt workflow n8n tự động cào dữ liệu web, phân tích thay đổi nội dung bằng AI Claude và gửi cảnh báo qua Slack."
slug: "giam-sat-thay-doi-website-bright-data-claude-slack"
tags: [n8n, automation, ai-summarization, bright-data, claude, slack, airtable]
keywords: [n8n workflow, giám sát website, cào dữ liệu web, bright data, claude ai, slack notification]
keywords: [n8n workflow, giám sát website, cào dữ liệu web, bright data, claude ai, slack notification]
---

# 🚀 Tự động giám sát thay đổi website đối thủ bằng Bright Data, Claude AI và Slack

Các sếp có đang đau đầu vì phải thủ công kiểm tra giá cả của đối thủ, cập nhật thay đổi tính năng trên trang sản phẩm hay theo dõi các tài liệu chính sách mới? Việc này cực kỳ mất thời gian và rất dễ bỏ sót các thông tin quan trọng. 

Giải pháp ư? Hãy để workflow n8n này làm thay các sếp! Sự kết hợp hoàn hảo giữa **Bright Data** (vượt qua mọi tường lửa, CAPTCHA), **Claude AI** (thông minh phân tích nội dung, loại bỏ nhiễu) và **Slack** (gửi cảnh báo tức thì) sẽ giúp các sếp tự động hóa 100% quy trình này mà không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần F5 kiểm tra website thủ công hàng ngày.
- **AI thông minh lọc nhiễu:** Claude tự động bỏ qua các thay đổi rác như thời gian, build ID, CSS và chỉ tập trung vào nội dung thực sự thay đổi.
- **Cảnh báo tức thì:** Nhận thông báo trực tiếp qua Slack ngay khi website đối thủ có biến động.
- **Hoạt động 24/7:** Chạy tự động theo lịch trình cài đặt sẵn, lưu trữ lịch sử snapshot đầy đủ trên CRM.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản [Bright Data](https://brightdata.com) kèm Web Unlocker zone.
- API Key từ [Anthropic](https://anthropic.com) (dùng cho Claude).
- Tài khoản Airtable (hoặc CRM/Database bất kỳ) để lưu danh sách URL và snapshot.
- Workspace và Channel trên [Slack](https://slack.com) để nhận thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào n8n Editor của các sếp (hoặc copy toàn bộ JSON và Paste trực tiếp vào giao diện n8n).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm các node chính sau đây, các sếp cần cấu hình chính xác:
- **Schedule Trigger**: Thiết lập khoảng thời gian chạy (hàng giờ, hàng ngày...).
- **Get URLs to Monitor (Airtable)**: Kết nối tài khoản Airtable, trỏ đến Base chứa danh sách URL cần theo dõi (điều kiện lọc `Active = TRUE`).
- **Loop Over URLs (Split In Batches)**: Giúp xử lý từng URL một cách tuần tự, tránh quá tải và đảm bảo lỗi một URL không làm sập toàn bộ luồng.
- **Scrape Page with Bright Data**: Kết nối tài khoản Bright Data để cào trang (xử lý tốt các trang nặng về JavaScript, bị chặn bởi CAPTCHA hoặc giới hạn địa lý).
- **Truncate HTML (Code)**: Node này giới hạn HTML ở mức 90.000 ký tự đầu tiên để vừa vặn với ngữ cảnh của LLM.
- **AI Diff Analyzer (Anthropic / Claude Sonnet)**: Cấu hình credentials Anthropic, AI sẽ so sánh HTML mới với snapshot cũ. Trả về `FIRST_RUN` (nếu chạy lần đầu), `NO_CHANGE` (nếu không có thay đổi thực sự), hoặc bản tóm tắt 2-3 câu về điểm thay đổi.
- **Save Snapshot to CRM (Airtable)**: Cập nhật HTML mới và tóm tắt của AI trở lại Airtable.
- **Change Detected? (If)**: Lọc kết quả, chỉ cho phép đi tiếp nếu có thay đổi thực sự (loại bỏ `NO_CHANGE` và `FIRST_RUN`).
- **Notify Slack**: Gửi thông báo chi tiết về nội dung thay đổi vào kênh Slack của đội ngũ.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) với dữ liệu mẫu để đảm bảo kết nối thông suốt từ Cào dữ liệu -> AI -> Slack.
- Bật công tắc **Active** để workflow chính thức tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa dạng hóa kênh thông báo:** Thay vì chỉ dùng Slack, các sếp có thể kết hợp thêm Telegram, Email, hoặc Microsoft Teams tùy theo thói quen của team.
- **Mở rộng nguồn dữ liệu:** Có thể thay thế Airtable bằng Google Sheets, Notion, hoặc PostgreSQL để lưu trữ lịch sử snapshot.
- **Tùy biến AI Prompt:** Tinh chỉnh câu lệnh trong node Claude AI nếu các sếp muốn tập trung sâu hơn vào một số khía cạnh cụ thể (ví dụ: chỉ theo dõi thay đổi về giá, hoặc thay đổi về tính năng sản phẩm).

### 📌 Kết luận
Workflow giám sát website tự động này là "vũ khí bí mật" giúp doanh nghiệp nắm bắt nhanh chóng mọi biến động từ đối thủ hoặc thị trường. Hãy cài đặt ngay hôm nay để tối ưu hóa thời gian và nâng cao năng lực cạnh tranh cho đội ngũ của các sếp!