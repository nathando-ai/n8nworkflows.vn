---
title: "🚀 Biến Website Thành Cơ Sở Dữ Liệu Tri Thức Cho AI (LLM-Ready) Với n8n"
description: "Tự động hóa quy trình trích xuất nội dung từ website, chuyển đổi sang định dạng Markdown/TXT và tạo file LLMs.txt chuẩn bị sẵn cho các mô hình ngôn ngữ lớn (LLM) sử dụng Firecrawl, Parsera và GPT-4.1-mini."
slug: "bien-website-thanh-llm-knowledge-base"
tags: [n8n, automation, no-code, RAG, LLM, Firecrawl, Parsera]
keywords: [n8n workflow, tự động hóa RAG, trích xuất website, LLMs.txt, Firecrawl n8n]
---

# 🚀 Biến Website Thành Cơ Sở Dữ Liệu Tri Thức Cho AI (LLM-Ready)

Trong kỷ nguyên của RAG (Retrieval-Augmented Generation), việc "nuôi" dữ liệu sạch cho các mô hình AI là yếu tố sống còn. Tuy nhiên, việc thủ công truy cập từng trang web, copy nội dung, làm sạch HTML và định dạng lại thành Markdown hoặc TXT để nạp vào hệ thống RAG là một quá trình cực kỳ tẻ nhạt, dễ sai sót và tốn thời gian.

Workflow này chính là giải pháp "chìa khóa trao tay" giúp các sếp tự động hóa toàn bộ quy trình: Từ việc nhập URL, sử dụng **Firecrawl** để map cấu trúc website, **Parsera** để trích xuất nội dung sạch, cho đến việc sử dụng **GPT-4.1-mini** để tạo ra file `LLMs.txt` chuẩn hóa. Kết quả cuối cùng là một thư mục trên Google Drive chứa đầy đủ tài liệu đã được "làm sạch" và tối ưu hóa, sẵn sàng để các hệ thống AI của bạn "ăn" vào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, đặc biệt khi xử lý hàng loạt URL, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian thủ công:** Chỉ cần nhập URL, hệ thống tự động crawl, trích xuất và lưu trữ.
- **Dữ liệu sạch chuẩn LLM:** Nội dung được chuyển đổi sang Markdown/TXT, loại bỏ các phần tử HTML rác, giúp AI hiểu ngữ cảnh tốt hơn.
- **Tạo file LLMs.txt tự động:** Sử dụng GPT-4.1-mini để tổng hợp và định dạng lại nội dung theo chuẩn `LLMs.txt`, tối ưu cho việc nạp vào RAG.
- **Lưu trữ tập trung:** Tất cả file được upload tự động vào Google Drive, dễ dàng quản lý và truy xuất.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n:** Bản Self-hosted hoặc Cloud.
2. **API Key Firecrawl:** Dùng để map và crawl URL (có thể dùng trial hoặc trả phí).
3. **API Key Parsera:** Dùng để trích xuất nội dung web thành Markdown.
4. **API Key OpenAI:** Dùng cho node GPT-4.1-mini để tạo file LLMs.txt.
5. **Tài khoản Google Drive:** Đã cấp quyền OAuth cho n8n (Credentials Google Drive).
6. **URL website:** Địa chỉ trang web cần trích xuất.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from URL** hoặc **Import from File**.
3. Dán link workflow gốc: [https://n8n.io/workflows/7260](https://n8n.io/workflows/7260) hoặc tải file JSON về và import.
4. Sau khi import, các sếp sẽ thấy một workflow với 15 nodes, được chia thành 2 luồng chính: **Batch** (xử lý nhiều URL) và **Single** (xử lý 1 URL).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Đây là phần quan trọng nhất. Các sếp cần click vào từng node và cấu hình credentials cũng như tham số:

1. **Node: `Trigger — Form (Create LLM KB)`**
   - Đây là điểm bắt đầu. Các sếp có thể chỉnh sửa các trường trong Form (ví dụ: thêm trường "Tên dự án" hoặc "Mô tả") nếu muốn.
   - Mặc định nó nhận input `URL` và `Mode` (Single/Batch).

2. **Node: `Firecrawl — Map URLs`**
   - **Credentials:** Chọn hoặc tạo mới credentials **Firecrawl**.
   - **Tham số:** Đảm bảo API Key Firecrawl đã được điền đúng. Node này sẽ gọi API để map các URL con từ URL gốc.

3. **Node: `Extract Markdown (Parsera)` & `Extract Markdown (Parsera - Single)`**
   - **Credentials:** Chọn hoặc tạo mới credentials **Parsera**.
   - **Tham số:** Kiểm tra endpoint API của Parsera. Đảm bảo API Key Parsera hợp lệ. Node này chịu trách nhiệm chuyển HTML thành Markdown sạch.

4. **Node: `LLMs.txt Generator (OpenAI - Single)` & `LLMs.txt Generator (OpenAI - Batch)`**
   - **Credentials:** Chọn hoặc tạo mới credentials **OpenAI**.
   - **Model:** Mặc định là `gpt-4.1-mini`. Các sếp có thể đổi sang `gpt-4o` nếu cần chất lượng cao hơn (nhưng chi phí cao hơn).
   - **Prompt:** Kiểm tra prompt bên trong node. Prompt này hướng dẫn GPT cách định dạng nội dung trích xuất được thành file `LLMs.txt` chuẩn. Các sếp có thể tùy chỉnh prompt này để phù hợp với cấu trúc dữ liệu mong muốn.

5. **Node: `Google Drive — Upload to folder (Batch)` & `Google Drive — Upload to folder(Single)`**
   - **Credentials:** Chọn hoặc tạo mới credentials **Google Drive**.
   - **Folder ID:** Đây là điểm dễ sai nhất. Các sếp cần tìm **ID của thư mục** trên Google Drive mà các sếp muốn lưu file.
     - *Cách lấy ID:* Mở thư mục trên Google Drive, nhìn vào URL. Phần sau `/folders/` chính là Folder ID.
     - Ví dụ: `https://drive.google.com/drive/folders/1AbC...` -> ID là `1AbC...`.
   - **File Name:** Kiểm tra biểu thức đặt tên file. Mặc định thường là tên miền + `.txt` hoặc `.md`.

6. **Node: `Decision — Generate For`**
   - Node Switch này phân luồng dựa trên input từ Form.
   - Nếu chọn "Single", luồng sẽ đi qua các node có hậu tố `(Single)`.
   - Nếu chọn "Batch", luồng sẽ đi qua `Batch URL Processor` và các node có hậu tố `(Batch)`.
   - **Lưu ý:** Đảm bảo giá trị trong Form khớp với các case trong node Switch (ví dụ: "single" và "batch").

#### 3. Kích hoạt ⚡️
1. **Test Run:**
   - Click vào node `Trigger — Form (Create LLM KB)`.
   - Chọn **Execute Workflow**.
   - Một form sẽ hiện ra. Nhập một URL đơn giản (ví dụ: `https://example.com`) và chọn Mode là "Single".
   - Chạy workflow. Theo dõi từng node.
   - Kiểm tra kết quả: Mở Google Drive, xem file `.txt` hoặc `.md` đã được tạo ra chưa. Mở file ra xem nội dung có sạch không, có đúng định dạng LLMs.txt không.
2. **Bật Active:**
   - Sau khi test thành công, click vào nút **Active** ở góc trên bên phải n8n Editor.
   - Workflow sẽ sẵn sàng nhận dữ liệu từ Form bất kỳ lúc nào.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram:** Thêm node `Slack` hoặc `Telegram` sau node Upload Google Drive để gửi thông báo "Hoàn thành trích xuất" kèm link file cho team.
- **Lọc nội dung:** Trước khi gửi vào Parsera, các sếp có thể thêm node `Code` hoặc `IF` để lọc bỏ các URL không cần thiết (ví dụ: trang login, trang 404) dựa trên kết quả từ Firecrawl.
- **Định kỳ cập nhật:** Thay vì dùng Form Trigger, các sếp có thể thay bằng `Cron Trigger` và dùng một Google Sheet chứa danh sách URL cần cập nhật hàng ngày. Workflow sẽ tự động chạy mỗi ngày để đảm bảo dữ liệu AI luôn mới nhất.
- **Chuyển đổi sang PDF:** Nếu hệ thống RAG của các sếp yêu cầu PDF, các sếp có thể thêm node `Convert to PDF` (dùng Puppeteer hoặc Headless Chrome) sau bước tạo TXT/MD.

### 📌 Kết luận
Việc chuẩn bị dữ liệu (Data Preparation) thường chiếm 80% thời gian trong dự án AI. Với workflow này, các sếp có thể giảm con số đó xuống gần bằng 0. Chỉ với vài cú click, các sếp đã có một kho tri thức sạch sẽ, chuẩn hóa, sẵn sàng để "nuôi" các mô hình AI của mình. Hãy import ngay và thử nghiệm với website của chính các sếp để cảm nhận sự khác biệt!