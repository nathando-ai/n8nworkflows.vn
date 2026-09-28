---
title: "🚀 Tự động tạo báo cáo nghiên cứu khách hàng tiềm năng và chiến lược kết nối với Claude AI"
description: "Hướng dẫn sử dụng workflow n8n để tự động hóa việc nghiên cứu profile khách hàng tiềm năng và xây dựng chiến lược tiếp cận siêu cá nhân hóa bằng Claude AI qua OpenRouter."
slug: "tao-bao-cao-nghien-cuu-khach-hang-tiem-nang-voi-claude-ai"
tags: [n8n, automation, no-code, ai, claude-ai, lead-generation, openrouter]
keywords: [n8n workflow, tự động hóa nghiên cứu khách hàng, Claude AI, OpenRouter, lead generation, chiến lược kết nối]
---

# 🚀 Tự động tạo báo cáo nghiên cứu khách hàng tiềm năng và chiến lược kết nối với Claude AI

Các sếp có bao giờ mất hàng giờ để "soi" Facebook, LinkedIn, website của một khách hàng tiềm năng lớn trước khi gửi tin nhắn kết nối không? Việc nghiên cứu thủ công này cực kỳ tốn thời gian, dễ bỏ sót thông tin quan trọng và rất khó scale (mở rộng) khi đội ngũ sales phải làm cho hàng trăm leads mỗi ngày.

Đừng lo, hôm nay chúng ta sẽ cùng "lên đồ" một automation workflow cực đỉnh được phát triển bởi **Open Paws**. Workflow này sử dụng sức mạnh của **Claude AI (qua OpenRouter)** để tự động hóa toàn bộ quy trình: nghiên cứu sâu về khách hàng, đối chiếu profile của người gửi và người nhận, sau đó tổng hợp thành một báo cáo HTML đẹp mắt, chuyên nghiệp kèm chiến lược tiếp cận sát sườn!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian**: Bỏ qua công đoạn "Google dạo" thủ công, AI tự động quét và tổng hợp toàn bộ thông tin lịch sử làm việc, học vấn, sở thích của khách hàng.
- **Chiến lược tiếp cận siêu cá nhân hóa**: Đưa ra các điểm chung (connection points) giữa người gửi và khách hàng, giúp tăng tỷ lệ phản hồi (response rate) lên mức tối đa.
- **Báo cáo chuẩn chỉnh, trực quan**: Xuất ra định dạng HTML mobile-friendly, sẵn sàng để gửi qua email, đăng lên web hoặc tích hợp vào hệ thống CRM.
- **Hoạt động linh hoạt**: Thiết kế dưới dạng Sub-workflow, dễ dàng gọi từ bất kỳ hệ thống nào khác (Webhook, Telegram, CRM, Google Sheets).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị sẵn các tài nguyên sau:
1. **Hệ thống n8n**: Đã cài đặt sẵn sàng (phiên bản khuyên dùng >= 1.0).
2. **Tài khoản OpenRouter**: Cần có API Key và số dư tối thiểu để gọi mô hình AI.
3. **Sub-workflow nghiên cứu (Multi-tool Research Agent)**: Workflow này gọi một workflow phụ (`Call Research Agent`) để thu thập dữ liệu thô từ internet (tham khảo link gốc [tại đây](https://n8n.io/workflows/5588-multi-tool-research-agent-for-animal-advocacy-with-openrouter-serper-and-open-paws-db/)).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy mã JSON của workflow hoặc tải file JSON về máy.
- Mở n8n Editor -> Chọn **Add workflow** -> **Import from File** (hoặc Paste trực tiếp JSON vào giao diện).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 5 nodes chính, các sếp cần chú ý cấu hình kỹ các điểm sau:

- **When Executed by Another Workflow (`executeWorkflowTrigger`)**: Node này đóng vai trò nhận dữ liệu đầu vào bao gồm: Tên người bán/đại diện (Prospector name), Tên khách hàng (Prospect name), các URL mạng xã hội của cả hai, và mục tiêu kết nối (Outreach goal). Hãy đảm bảo các sếp truyền đúng cấu trúc JSON từ workflow cha sang.
- **OpenRouter Chat Model1 (`lmChatOpenRouter`)**: 
  - Chọn hoặc tạo mới **OpenRouter Credentials** bằng cách nhập API Key của sếp.
  - Kiểm tra lại thông số Model: Workflow được cấu hình sẵn với `anthropic/claude-sonnet-4` (hoặc các sếp có thể đổi sang model Claude 3.5 Sonnet mới nhất để có chất lượng phân tích sắc bén nhất).
- **Report Writer (`chainLlm`)**: Node LangChain chịu trách nhiệm tổng hợp thông tin từ agent nghiên cứu và viết thành báo cáo chi tiết theo prompt đã được thiết lập sẵn (Executive Summary, Background, Personal Interests, Connection Points, Engagement Strategy...).
- **Call Research Agent (`executeWorkflow`)**: Node này gọi sub-workflow làm nhiệm vụ crawl và xác thực thông tin profile. Các sếp nhớ trỏ đường dẫn đến đúng ID của workflow Research Agent trên hệ thống n8n của mình.
- **Set HTML (`set`)**: Node định dạng lại kết quả đầu ra thành đoạn mã HTML hoàn chỉnh, tối ưu hiển thị trên cả máy tính lẫn điện thoại di động.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** với một bộ dữ liệu mẫu (Test data) gồm tên và URL mạng xã hội của một khách hàng thực tế để kiểm tra kết quả.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để đưa workflow vào trạng thái sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa quy trình làm sales và outreach, các sếp có thể mở rộng workflow này bằng cách:
- **Tích hợp Email/Slack**: Thêm node Gmail hoặc Slack ở cuối workflow để tự động gửi bản báo cáo HTML vừa tạo trực tiếp đến nhân sự sales phụ trách lead đó ngay khi có yêu cầu.
- **Lưu trữ vào Google Sheets / Notion**: Thêm node lưu log kết quả nghiên cứu và chiến lược kết nối để đội ngũ dễ dàng tra cứu lại lịch sử.
- **Tự động hóa toàn diện**: Kết hợp trigger từ Google Sheets (khi có dòng lead mới được thêm vào) -> Gọi workflow này -> Gửi kết quả về Telegram cho sếp duyệt trước khi gửi tin nhắn.

### 📌 Kết luận
Với sức mạnh của Claude AI và hệ thống automation từ n8n, việc nghiên cứu khách hàng tiềm năng giờ đây chỉ tính bằng giây thay vì tốn hàng tiếng đồng hồ mò mẫm. Hãy áp dụng ngay workflow này vào phễu bán hàng của doanh nghiệp để tạo sự khác biệt hoàn toàn với đối thủ nhờ sự thấu hiểu sâu sắc về khách hàng! Chúc các sếp "lên đồ" thành công! 🚀