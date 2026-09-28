---
title: "🚀 Phát hiện ảo giác AI (Hallucination) tự động với Ollama và Bespoke-Minicheck trên n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động kiểm tra và phát hiện ảo giác trong câu trả lời của AI sử dụng mô hình chuyên biệt bespoke-minicheck và qwen qua Ollama."
slug: "phat-hien-ao-giac-ai-ollama-bespoke-minicheck-n8n"
tags: [n8n, automation, ai, ollama, llm, hallucination-detection]
keywords: [n8n workflow, phát hiện ảo giác ai, hallucination detection, ollama n8n, bespoke-minicheck, qwen2.5]
---

# 🚀 Phát hiện ảo giác AI (Hallucination) tự động với Ollama và Bespoke-Minicheck

Các sếp khi ứng dụng Generative AI hay LLM vào hệ thống chắc chắn đã từng đau đầu với tình trạng "AI nói phét" (ảo giác - hallucination). Việc kiểm tra thủ công từng câu trả lời của AI so với tài liệu gốc tốn rất nhiều thời gian và không thể scale cho hệ thống lớn.

Bài viết này sẽ giới thiệu một workflow n8n cực kỳ thông minh do chuyên gia Guido Zockoll xây dựng, giúp tự động hóa hoàn toàn quá trình kiểm tra thực tế (fact-checking) và phát hiện ảo giác của AI sử dụng mô hình chuyên biệt `bespoke-minicheck` chạy local qua Ollama.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và kết nối mượt mà với Ollama local, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Kiểm tra câu trả lời của AI ngay lập tức trước khi trả về cho khách hàng hoặc lưu trữ.
- **Độ chính xác cao:** Sử dụng mô hình chuyên dụng `bespoke-minicheck` được tối ưu hóa riêng cho việc phát hiện fact-check và hallucination.
- **Tiết kiệm chi phí:** Chạy hoàn toàn trên hạ tầng Local (Ollama) nên không mất tiền API calls cho OpenAI hay Anthropic.
- **Tích hợp linh hoạt:** Có thể hoạt động như một Sub-workflow (gọi từ các Agentic workflow khác) hoặc chạy test độc lập.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Ollama Server:** Đã cài đặt Ollama trên máy chủ cục bộ hoặc VPS có hỗ trợ API.
- **Ollama Models:** Đã tải sẵn các mô hình cần thiết bằng cách chạy lệnh trên terminal:
  - `ollama pull bespoke-minicheck` (Dùng để checkfact chuyên dụng)
  - `ollama pull qwen2.5:1.5b` (Dùng để tổng hợp kết quả)
- **Credentials:** Ollama API credentials cấu hình trên n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow (hoặc tải file từ n8n.io/workflows/2922) và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow được chia thành các phân đoạn rõ ràng trên canvas:
- **Node `Ollama Chat Model` & `Ollama Model`:** Kiểm tra lại cấu hình thông tin kết nối (Credentials) tới Ollama của các sếp. Đảm bảo model name đúng chuẩn:
  - Model check fact: `bespoke-minicheck:latest`
  - Model tổng hợp: `qwen2.5:1.5b`
- **Node `Edit Fields` / `Code`:** Nơi đầu vào nhận dữ liệu câu trả lời của AI và ngữ cảnh gốc (context) để tiến hành tách câu (`Split Out1`) và đối chiếu.
- **Node `Basic LLM Chain` & `Basic LLM Chain4`:** Thực hiện chuỗiLangChain gọi đến LLM để thực hiện nhiệm vụ fact-checking từng câu và tổng hợp thành báo cáo hoàn chỉnh.

#### 3. Kích hoạt ⚡️
- Nhấn **‘Test workflow’** bằng node `When clicking ‘Test workflow’` để kiểm tra với dữ liệu mẫu xem mô hình trả về kết quả chính xác chưa.
- Sau khi test ngon lành, bật **Active** để sẵn sàng nhận dữ liệu từ các workflow khác thông qua node `When Executed by Another Workflow`.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp vào Agentic Workflow:** Gọi workflow này như một bước trung gian (Sub-workflow) mỗi khi AI Agent sinh ra một đoạn văn bản dài cần kiểm chứng.
- **Lưu Log vào Google Sheets / Airtable:** Thêm node Google Sheets ở cuối workflow để ghi lại các trường hợp bị phát hiện ảo giác nhằm cải thiện prompt hệ thống sau này.
- **Cảnh báo qua Slack/Telegram:** Nếu tỷ lệ hallucination vượt quá ngưỡng cho phép, cấu hình thêm điều kiện gửi cảnh báo tức thì cho đội ngũ kỹ thuật.

### 📌 Kết luận
Việc kiểm soát chất lượng câu trả lời của AI là chìa khóa sống còn để đưa ứng dụng AI vào môi trường sản xuất thực tế (Production). Với workflow n8n kết hợp Ollama và Bespoke-Minicheck này, các sếp đã có ngay một "vũ khí" mạnh mẽ, bảo mật và hoàn toàn miễn phí để triệt tiêu tình trạng AI nói phét. Lên đồ và áp dụng ngay thôi các sếp!