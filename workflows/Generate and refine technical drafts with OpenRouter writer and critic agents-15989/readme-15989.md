---
title: "🚀 Tự động tạo và kiểm duyệt nội dung kỹ thuật chất lượng cao với AI Writer & Critic Agents trong n8n"
description: "Xây dựng hệ thống AI tự động sinh và phản biện bản thảo (Self-Critiquing Loop) sử dụng OpenRouter, giúp tạo ra các bài viết kỹ thuật đạt chuẩn chất lượng khắt khe."
slug: "tu-dong-tao-va-kiem-duyet-noi-dung-ky-thuat-ai-writer-critic"
tags: [n8n, automation, no-code, ai-agents, openrouter, content-generation]
keywords: [n8n workflow, tự động hóa ai, openrouter writer critic, self-critiquing agent, tạo nội dung tự động]
---

# 🚀 Tự động tạo và kiểm duyệt nội dung kỹ thuật với AI Writer & Critic Agents

Các sếp có bao giờ cảm thấy mệt mỏi khi phải viết đi viết lại một bài kỹ thuật, tài liệu hướng dẫn (technical docs) vì bản nháp đầu tiên của AI thường quá chung chung, thiếu chiều sâu hoặc không đúng trọng tâm? Việc thuê người kiểm duyệt hoặc tự tay sửa từng câu chữ tốn rất nhiều thời gian và công sức.

Giải pháp ở đây là gì? Hãy để tự động hóa lo! Workflow n8n này ứng dụng mô hình **Self-Critiquing Loop** gồm hai AI Agent phối hợp nhịp nhàng: một Agent chuyên viết (Writer) và một Agent chuyên "vạch lá tìm sâu" (Critic) để phản biện, chấm điểm và yêu cầu sửa đổi cho đến khi bài viết đạt chất lượng hoàn hảo. Tất cả chạy tự động 100% qua API của OpenRouter mà không cần viết một dòng code phức tạp nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Chất lượng vượt trội:** Bài viết được đánh giá chéo dựa trên các tiêu chí khắt khe (độ chính xác, sự rõ ràng, tính liên quan, tính cô đọng).
- **Tiết kiệm 80% thời gian:** Không còn cảnh biên tập thủ công nhiều lần; AI tự vòng lặp sửa lỗi cho đến khi đạt điểm số mong muốn (`minScore`).
- **Linh hoạt chi phí:** Dễ dàng cấu hình dùng mô hình tiết kiệm cho Writer và mô hình thông minh hơn cho Critic.
- **Hoạt động 24/7:** Nhận yêu cầu qua Webhook bất cứ lúc nào và trả về kết quả hoàn chỉnh cho ứng dụng/client của các sếp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã hoạt động (Cloud hoặc Self-hosted).
- **Tài khoản OpenRouter:** Cần có API Key để kết nối với các mô hình ngôn ngữ lớn (OpenRouter - Writer & OpenRouter - Critic).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này, vào n8n editor, chọn **New Workflow**, nhấn `Ctrl + V` (hoặc `Cmd + V`) để dán vào không gian làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần chú ý các node quan trọng sau:
- **OpenRouter - Writer & OpenRouter - Critic:** 
  - Cần cấu hình **Credentials** bằng OpenRouter API Key của các sếp.
  - Mặc định template sử dụng mô hình `openai/gpt-4o-mini` cho cả hai, nhưng các sếp có thể đổi sang các model mạnh hơn tùy nhu cầu.
- **Webhook - Brief In:** 
  - Sử dụng phương thức `POST` tại đường dẫn `self-critiquing-writer`. 
  - Khi gửi request (qua Postman, cURL hoặc app khác), payload JSON cần truyền các trường: `topic`, `brief`, `minScore`, `maxIterations`.
  - *Mẹo:* Bắt đầu test với `minScore: 7.5` cho luồng nhanh, sau đó tăng lên `9.0` để ép hệ thống kích hoạt vòng lặp phản biện khắt khe hơn.

#### 3. Kích hoạt ⚡️
- Gửi một request mẫu qua Webhook để test run (Test execution) xem các node Agent hoạt động và vòng lặp (Loop) vét cạn/chấm điểm chạy chính xác chưa.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để đưa workflow vào trạng thái vận hành tự động thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo:** Nối thêm một node Telegram hoặc Slack sau node `Respond to Client` để nhận thông báo ngay khi có bài viết hoàn thành hoặc khi bài viết không đạt điểm phải chuyển sang review thủ công.
- **Lưu trữ dữ liệu:** Thêm node Google Sheets hoặc Airtable để lưu lịch sử các bản nháp, điểm số và số lần lặp (iterations) nhằm phân tích chất lượng AI theo thời gian.
- **Tùy biến tiêu chí chấm điểm:** Chỉnh sửa System Prompt trong node *Critic Agent* để thay đổi các trọng số hoặc tiêu chí đánh giá phù hợp với lĩnh vực đặc thù của doanh nghiệp các sếp (ví dụ: tài chính, y tế, lập trình...).

### 📌 Kết luận
Workflow *Generate and refine technical drafts with OpenRouter writer and critic agents* là một "vũ khí" cực kỳ lợi hại giúp tự động hóa khâu sáng tạo và kiểm duyệt nội dung chuyên sâu. Hãy áp dụng ngay vào hệ thống của các sếp để nâng tầm chất lượng tài liệu và tiết kiệm tối đa nguồn lực con người!