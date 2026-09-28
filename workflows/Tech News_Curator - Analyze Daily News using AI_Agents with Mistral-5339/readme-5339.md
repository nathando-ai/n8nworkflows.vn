---
title: "🚀 Tự động hóa tổng hợp tin tức công nghệ hàng ngày với AI Agents và Mistral"
description: "Hướng dẫn tự động hóa tổng hợp tin tức công nghệ hàng ngày từ nhiều nguồn bằng n8n và AI Agents của Mistral. Tiết kiệm thời gian và nhận được báo cáo tin tức cá nhân hóa mỗi ngày."
slug: "tu-dong-hoa-tong-hop-tin-tuc-cong-nghe-hang-ngay-voi-ai-agents"
tags: [n8n, automation, no-code, AI, automation, tin tức công nghệ]
keywords: [n8n workflow, tự động hóa, AI, tin tức công nghệ, tự động hóa báo cáo]
---

# 🚀 Tự động hóa tổng hợp tin tức công nghệ hàng ngày với AI Agents và Mistral

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có thể đã từng phải mất hàng giờ mỗi ngày để theo dõi và tổng hợp tin tức công nghệ từ nhiều nguồn khác nhau. Từ các trang báo lớn đến các diễn đàn kỹ thuật, việc thu thập và phân tích thông tin quan trọng là một thách thức lớn. Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình này chỉ trong vài phút, nhận được báo cáo tin tức cá nhân hóa mỗi ngày mà không cần phải can thiệp thủ công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động thu thập và tổng hợp tin tức từ nhiều nguồn trong vòng vài phút mỗi ngày.
- **Chính xác và cá nhân hóa**: AI Agents của Mistral sẽ lọc và phân tích tin tức quan trọng nhất, phù hợp với nhu cầu cụ thể của doanh nghiệp.
- **Hoạt động liên tục**: Workflow được cấu hình để chạy tự động hàng ngày, đảm bảo các sếp luôn nhận được thông tin mới nhất.
- **Dễ dàng mở rộng**: Có thể thêm hoặc bớt các nguồn tin tức và từ khóa lọc theo nhu cầu cụ thể.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Mistral Cloud API (để sử dụng AI Agents).
- Các nguồn tin tức RSS (ScienceDaily, AlternativeTo, MIT Technology Review, lobste.rs, Silicone Republic, TheHackersNews).
- Node DuckDuckGo Search đã được cài đặt trong n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào [n8n.io/workflows/5339](https://n8n.io/workflows/5339) để tải file JSON của workflow.
2. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON đã tải về.
3. Hoặc copy toàn bộ nội dung JSON và paste vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Mistral Cloud Chat Model**:
   - Tạo credentials cho Mistral Cloud API trong n8n.
   - Chọn model "mistral-small-latest" trong node này.

2. **RSS Feed Read Nodes**:
   - Đảm bảo các nguồn tin tức RSS được cấu hình chính xác.
   - Kiểm tra định dạng đầu ra của các node này để đảm bảo chúng được chuẩn hóa trước khi merge.

3. **Filter Nodes**:
   - Cấu hình node "Filter by Datetime" để chỉ lấy tin tức hàng ngày.
   - Cấu hình node "Remove Certain Content" để loại bỏ tin tức không mong muốn bằng cách sử dụng từ khóa.

4. **DuckDuckGo Node**:
   - Đảm bảo node này đã được cài đặt trong n8n.
   - Cấu hình operation là "searchNews".

5. **Sub-Workflow "Get Webpage Content"**:
   - Chuyển đổi sub-workflow theo hướng dẫn [tại đây](https://docs.n8n.io/workflows/subworkflow-conversion/).

6. **Schedule Node**:
   - Cấu hình node này để chạy workflow hàng ngày sau 12:00 PM.

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động như mong đợi.
2. Bật Active workflow để chạy tự động hàng ngày.

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh nguồn tin tức**: Thêm hoặc bớt các nguồn tin tức RSS theo nhu cầu cụ thể của doanh nghiệp.
2. **Tối ưu hóa từ khóa lọc**: Cập nhật danh sách từ khóa trong node "Remove Certain Content" để lọc tin tức phù hợp hơn.
3. **Kết hợp với Slack/Telegram**: Thêm node để gửi báo cáo tin tức tự động đến các kênh Slack hoặc Telegram.
4. **Lưu log hoạt động**: Thêm node để lưu log hoạt động của workflow để theo dõi và phân tích hiệu suất.

### 📌 Kết luận
Workflow này cung cấp một giải pháp toàn diện để tự động hóa việc tổng hợp tin tức công nghệ hàng ngày. Với sự kết hợp của AI Agents và các nguồn tin tức đa dạng, các sếp có thể tiết kiệm thời gian và nhận được thông tin quan trọng một cách nhanh chóng và chính xác. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc của mình!