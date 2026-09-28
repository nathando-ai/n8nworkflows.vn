---
title: "🚀 Tự động viết và chỉnh sửa bài viết kỹ thuật với OpenRouter trong Content Pipeline"
description: "Hướng dẫn xây dựng subworkflow n8n sử dụng OpenRouter AI Agent để tự động soạn thảo và tối ưu bài viết kỹ thuật chuyên sâu dựa trên phản hồi."
slug: "viet-va-chinh-sua-bai-viet-ky-thuat-openrouter-n8n"
tags: [n8n, automation, openrouter, ai-agent, content-creation, no-code]
keywords: [n8n workflow, tự động hóa viết bài, OpenRouter AI, Content Pipeline, AI Agent n8n]
---

# 🚀 Tự động viết và chỉnh sửa bài viết kỹ thuật với OpenRouter trong Content Pipeline

Các sếp có đang đau đầu vì việc sản xuất nội dung kỹ thuật (technical content) tốn quá nhiều thời gian từ việc lên outline, viết nháp cho đến chỉnh sửa theo feedback? Việc viết thủ công vừa chậm, vừa khó duy trì phong độ đều đặn cho blog hay tài liệu sản phẩm.

Giải pháp ở đây là gì? Hãy để tự động hóa lo! Bài viết này sẽ hướng dẫn các sếp triển khai một **Subworkflow** cực kỳ mạnh mẽ trong n8n, đóng vai trò là "Cây bút AI" (Writer Agent) nhận brief, tự động viết nháp và tự động sửa bài dựa trên phản hồi thông qua sức mạnh của **OpenRouter**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% khâu sáng tạo nội dung:** Biến các brief khô khan và tài liệu nghiên cứu thành bài viết hoàn chỉnh.
- **Quy trình khép kín thông minh:** Khi có feedback từ Reviewer, AI không viết lại từ đầu mà khéo léo chỉnh sửa dựa trên bản nháp trước đó.
- **Tiết kiệm 80% thời gian:** Tối ưu hóa toàn bộ chuỗi cung ứng nội dung (Content Pipeline) mà không cần can thiệp thủ công.
- **Linh hoạt chọn mô hình AI:** Tận dụng hàng trăm mô hình ngôn ngữ lớn (LLM) thông qua OpenRouter với chi phí tối ưu nhất.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống n8n (Cloud hoặc Self-hosted).
- Tài khoản và API Key tại [OpenRouter](https://openrouter.ai/).
- Workflow này được thiết kế làm **Subworkflow**, được gọi từ một Workflow cha (Parent Content Pipeline).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ n8n template (ID: 15952) và tiến hành Import trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 4 nodes chính, các sếp cần chú ý cấu hình kỹ các điểm sau:

- **When Executed by Parent (`executeWorkflowTrigger`)**: Node này nhận toàn bộ trạng thái từ workflow cha (bao gồm: brief, tài liệu nghiên cứu, bản nháp trước đó, feedback của reviewer, và số lần chỉnh sửa `revisionCount`). Không cần chỉnh sửa gì ở node này.
- **OpenRouter - Writer (`lmChatOpenRouter`)**: 
  - Tạo Credentials kết nối với OpenRouter bằng API Key của các sếp.
  - Chọn model AI mạnh mẽ (ví dụ: Claude 3.5 Sonnet hoặc GPT-4o) vì đây là bước quyết định chất lượng nội dung của toàn bộ pipeline.
- **Writer Agent (`agent`)**: 
  - Cấu hình System Prompt cho Agent để định hình giọng văn (brand voice), phong cách viết kỹ thuật.
  - Thiết lập mục tiêu độ dài bài viết (mặc định khoảng 400 từ cho mỗi phiên bản nháp).
- **Parse Writer Output (`code`)**: Node chạy mã JavaScript để bóc tách kết quả đầu ra từ AI, trích xuất nội dung bài viết (`currentDraft`) và đếm số từ (`wordCount`), sau đó trả về cấu trúc dữ liệu chuẩn để chuyển tiếp cho workflow cha.

#### 3. Kích hoạt ⚡️
- Test thử bằng cách truyền dữ liệu mẫu từ workflow cha.
- Sau khi kiểm tra dữ liệu trả về chính xác, các sếp bật **Active** cho subworkflow này.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp đa mô hình:** Các sếp có thể thử nghiệm các mô hình open-source mạnh như Llama 3 hay Mistral qua OpenRouter để tiết kiệm chi phí.
- **Mở rộng Brand Voice:** Bổ sung thêm các quy chuẩn viết bài (Glossary, thuật ngữ kỹ thuật riêng của công ty) trực tiếp vào System Prompt của Writer Agent.
- **Lưu log tự động:** Kết nối thêm node Google Sheets hoặc Notion ở workflow cha để lưu trữ lại tất cả các phiên bản bài viết qua mỗi vòng chỉnh sửa (revision).

### 📌 Kết luận
Việc tự động hóa quy trình viết lách kỹ thuật chưa bao giờ dễ dàng đến thế với mô hình AI Agent kết hợp cùng n8n và OpenRouter. Hãy áp dụng ngay subworkflow này vào hệ thống Content Pipeline của các sếp để tối ưu hóa năng suất sản xuất nội dung ngay hôm nay!