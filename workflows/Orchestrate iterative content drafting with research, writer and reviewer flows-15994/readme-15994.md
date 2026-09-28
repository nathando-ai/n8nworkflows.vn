---
title: "🚀 Pipeline Viết Bài AI Tự Động: Nghiên Cứu, Viết & Chỉnh Sửa Lặp Lại"
description: "Workflow n8n tự động hóa quy trình sáng tạo nội dung với 3 AI chuyên biệt: Nghiên cứu, Viết lách và Đánh giá. Tự động lặp lại cho đến khi đạt chất lượng yêu cầu."
slug: "pipeline-viet-bai-ai-tu-dong"
tags: [n8n, ai-content, automation, llm, no-code]
keywords: [n8n workflow, tự động hóa viết bài, ai content pipeline, n8n subworkflow, content automation]
---

# 🚀 Pipeline Viết Bài AI Tự Động: Nghiên Cứu, Viết & Chỉnh Sửa Lặp Lại

Viết nội dung chất lượng cao thường là một quá trình đau đầu: bạn phải tự tìm kiếm thông tin, nháp bài, rồi tự đọc lại để chỉnh sửa ngữ pháp, giọng văn và độ chính xác. Làm thủ công không chỉ tốn thời gian mà còn dễ bị "mù" do nhìn quá nhiều lần vào cùng một nội dung.

Workflow này giải quyết triệt để vấn đề đó bằng cách mô phỏng quy trình làm việc của một đội ngũ biên tập viên chuyên nghiệp, nhưng hoàn toàn tự động và không cần code. Nó sử dụng 3 "AI chuyên gia" độc lập:
1. **Researcher (Nghiên cứu viên):** Thu thập thông tin nền tảng.
2. **Writer (Biên tập viên):** Viết bản nháp dựa trên nghiên cứu.
3. **Reviewer (Giám đốc nội dung):** Đánh giá điểm số và đưa ra phản hồi chỉnh sửa.

Nếu bài viết chưa đạt điểm chuẩn, hệ thống sẽ tự động gửi phản hồi cho Writer để viết lại (chỉ sửa phần lỗi, không viết lại từ đầu) cho đến khi đạt yêu cầu hoặc hết số lần chỉnh sửa tối đa.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Chất lượng đồng đều:** Mỗi bài viết đều được "chấm điểm" và kiểm duyệt bởi AI Reviewer, đảm bảo tiêu chuẩn nhất quán.
- **Tiết kiệm thời gian chỉnh sửa:** AI tự động phát hiện lỗi logic, giọng văn hoặc thiếu sót thông tin và tự sửa, giảm 80% thời gian proofreading thủ công.
- **Tùy biến linh hoạt:** Các sếp có thể thay đổi model AI cho từng bước (ví dụ: dùng model rẻ cho Research, model mạnh cho Writer) để tối ưu chi phí.
- **Hoạt động tự động 100%:** Chỉ cần gửi 1 request qua Webhook, nhận về bài viết hoàn chỉnh sau vài phút.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Bản Cloud hoặc Self-hosted.
- **API Keys cho LLM:** Cần ít nhất 1 API key (OpenAI, Anthropic, hoặc các provider khác hỗ trợ) để kết nối vào các subworkflows.
- **3 Subworkflows riêng biệt:** Workflow chính này là "Orchestrator" (người điều phối). Các sếp cần import thêm 3 workflow con:
    1. Research Subworkflow
    2. Writer Subworkflow
    3. Reviewer Subworkflow
    *(Lưu ý: 3 workflow con này thường đi kèm trong bộ template của tác giả Elvis Sarvia. Nếu chỉ có file JSON của workflow chính, các sếp cần tìm và import 3 file con trước).*
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Vào n8n, chọn **Import from URL** hoặc **Import from File**.
2. Import **3 Subworkflows** (Research, Writer, Reviewer) trước tiên.
3. Sau khi import xong, **Save** (Lưu) từng subworkflow.
4. Import **Workflow chính** (Orchestrator) từ link gốc hoặc file JSON.
5. Lưu workflow chính.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

**A. Cấu hình Credentials cho Subworkflows**
Mỗi subworkflow (Research, Writer, Reviewer) đều có node `Chat Model` riêng.
- Mở từng subworkflow.
- Tại node `Chat Model`, chọn **Credentials** tương ứng với API key AI của các sếp.
- *Mẹo:* Có thể dùng cùng 1 model cho cả 3, hoặc dùng model "nhẹ" hơn (ví dụ: GPT-4o-mini) cho Research và model "mạnh" hơn (ví dụ: GPT-4o hoặc Claude 3.5 Sonnet) cho Writer/Reviewer để tối ưu chi phí.

**B. Cấu hình Workflow Chính (Orchestrator)**
1. **Node: Webhook - Content Request**
   - Mặc định path là `content-pipeline`. Các sếp có thể đổi path này nếu muốn.
   - Method: `POST`.

2. **Node: Normalize Request (Code Node)**
   - Node này chuẩn hóa dữ liệu đầu vào. Các sếp có thể kiểm tra lại logic nếu muốn thay đổi cấu trúc payload đầu vào.
   - Các trường bắt buộc trong payload: `topic`, `brief`, `qualityThreshold` (điểm chuẩn, ví dụ: 8/10), `maxRevisions` (số lần sửa tối đa, ví dụ: 3).

3. **Node: Call Research / Writer / Reviewer Subworkflow**
   - Các node `Execute Workflow` này sẽ tự động tìm các subworkflow đã lưu.
   - **Quan trọng:** Đảm bảo tên của các subworkflow trong n8n khớp với tên được gọi trong các node Execute Workflow này. Nếu các sếp đổi tên subworkflow, phải cập nhật lại tại đây.

4. **Node: Evaluate Review (Code Node)**
   - Node này xử lý kết quả từ Reviewer.
   - Các sếp có thể chỉnh sửa logic chấm điểm nếu cần (ví dụ: thêm trọng số cho tiêu chí "Tính chính xác" cao hơn "Giọng văn").

5. **Node: Approved or Max Revisions? (IF Node)**
   - Điều kiện: `overallScore >= qualityThreshold` HOẶC `revisionCount >= maxRevisions`.
   - Nếu `true`: Chuyển sang Finalize.
   - Nếu `false`: Quay lại Writer để sửa bài.

#### 3. Kích hoạt ⚡️
1. **Test Run:**
   - Copy **Webhook Test URL** từ node Webhook.
   - Dùng Postman hoặc cURL để gửi request POST với body JSON mẫu:
     ```json
     {
       "topic": "Lợi ích của việc tập thể dục buổi sáng",
       "brief": "Viết bài 400 từ, giọng văn thân thiện, hướng đến người mới bắt đầu.",
       "qualityThreshold": 8,
       "maxRevisions": 2
     }
     ```
   - Chạy workflow và kiểm tra output.
2. **Bật Active:**
   - Sau khi test thành công, bật nút **Active** ở góc trên bên phải.
   - Copy **Webhook Production URL** để tích hợp vào hệ thống khác (CRM, Website, App...).

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp với CMS:** Sau khi có bài viết hoàn chỉnh, thêm node `WordPress` hoặc `Webflow` để tự động đăng bài lên website.
- **Gửi thông báo qua Slack/Telegram:** Thêm node `Slack` hoặc `Telegram` sau bước `Respond to Client` để gửi thông báo "Bài viết đã hoàn thành" kèm link xem trước.
- **Lưu log vào Google Sheets:** Thêm node `Google Sheets` để lưu lại `topic`, `score`, `revisionCount` và `finalContent` vào bảng tính, giúp các sếp theo dõi hiệu suất và chi phí AI theo thời gian.
- **Đa ngôn ngữ:** Thay đổi prompt trong subworkflow Writer để yêu cầu viết bằng tiếng Việt, tiếng Anh, hoặc bất kỳ ngôn ngữ nào khác.

### 📌 Kết luận
Workflow này là một ví dụ điển hình cho việc xây dựng **AI Pipeline** chuyên nghiệp trong n8n. Thay vì dùng 1 AI duy nhất làm mọi việc (dễ bị "mù" và thiếu chuyên sâu), việc tách biệt các vai trò Nghiên cứu - Viết - Đánh giá giúp tăng đáng kể chất lượng đầu ra.

Các sếp có thể bắt đầu ngay với cấu hình mặc định, sau đó tinh chỉnh `qualityThreshold` và prompt trong các subworkflow để phù hợp với ngách nội dung của mình. Chúc các sếp tự động hóa thành công!