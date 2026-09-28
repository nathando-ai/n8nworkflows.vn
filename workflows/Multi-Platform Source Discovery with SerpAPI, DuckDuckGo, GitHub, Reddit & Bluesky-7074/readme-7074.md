---
title: "🚀 Tự động Khám phá Nguồn Thông tin Đa nền tảng với n8n, AI và SerpAPI"
description: "Hướng dẫn chi tiết cài đặt và sử dụng workflow n8n Multi-Platform Source Discovery để tự động tìm kiếm nguồn tài nguyên, bài báo, và website uy tín từ Google, DuckDuckGo, GitHub, Reddit và Bluesky."
slug: "tu-dong-kham-pha-nguon-thong-tin-da-nen-tang-n8n"
tags: [n8n, automation, market-research, ai-summarization, serpapi, mistral-ai]
keywords: [n8n workflow, tự động hóa khám phá nguồn tin, serpapi n8n, duckduckgo n8n, ai information extractor, nghiên cứu thị trường tự động]
---

# 🚀 Tự động Khám phá Nguồn Thông tin Đa nền tảng với n8n, AI và Mistral

Các sếp có đang cảm thấy mệt mỏi khi phải tốn hàng giờ đồng hồ lướt web, lục lọi trên Google, GitHub, Reddit hay các mạng xã hội để tìm kiếm các nguồn thông tin, bài viết hoặc tài nguyên mới phục vụ cho việc nghiên cứu thị trường, làm content marketing hay phân tích đối thủ? 

Công việc thủ công này vừa tẻ nhạt, vừa dễ bỏ sót các nguồn tin giá trị. Giải pháp là đây: **Multi-Platform Source Discovery** – một siêu workflow n8n được thiết kế bởi **Hybroht**, tự động hóa 100% quá trình tìm kiếm, lọc dữ liệu trùng lặp, loại bỏ nguồn rác và sử dụng AI (Mistral Cloud) để đánh giá độ hữu ích của từng nguồn thông tin.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Đa kênh tự động:** Quét đồng loạt từ Google News (qua SerpAPI), DuckDuckGo, Reddit, GitHub (kho lưu trữ README tổng hợp) và Bluesky.
- **Lọc thông minh:** Tự động loại bỏ các URL trùng lặp, các nguồn tin đã biết (`existing_sources`) và các trang web bị loại trừ (`sources_to_ignore`).
- **Đánh giá bằng AI:** Sử dụng mô hình Mistral Cloud kết hợp `Information Extractor` để chấm điểm, kiểm tra độ liên quan và tính thời sự của nội dung thu thập được.
- **Tiết kiệm 90% thời gian:** Thay vì tìm kiếm thủ công, hệ thống tự động chạy theo lịch trình (Schedule) hoặc kích hoạt thủ công khi cần.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI "LÊN ĐỒ"]
- **n8n Custom Nodes:** Cần cài đặt trước các node phụ thuộc: `n8n-nodes-serpapi`, `n8n-nodes-bluesky-enhanced`, và `n8n-nodes-duckduckgo-search`.
- **API Keys / Credentials:**
  - `SerpApi` (cho Google News/Search).
  - `Bluesky API` (cho Bluesky Search).
  - `Mistral Cloud API` (cho AI Information Extractor).
  - `Global Constants API` (Khuyến nghị, dùng để lưu cấu hình từ khóa tìm kiếm, danh sách nguồn loại trừ).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ [n8n.io/workflows/7074](https://n8n.io/workflows/7074), sau đó chọn **Import from File** hoặc copy/paste trực tiếp mã JSON vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Vì đây là một workflow quy mô lớn với 55 nodes, các sếp cần chú ý cấu hình kỹ các điểm sau:
- **Configure Workflow Args / Configure Workflow Args (Manual):** Nơi các sếp định nghĩa các tham số đầu vào quan trọng:
  - `search_themes`: Các chủ đề cần tìm kiếm (Ví dụ: `["technology", "scientific research"]`).
  - `existing_sources`: Các URL nguồn tin mà các sếp đã biết (hệ thống sẽ tự động lọc ra để tránh trùng lặp).
  - `sources_to_ignore`: Các URL/domain không muốn nhìn thấy.
- **Credentials Nodes:** Kết nối chính xác các tài khoản API cho các node:
  - `Google_news search` (chọn credentials SerpAPI).
  - `Bluesky Search` (chọn credentials Bluesky).
  - `Mistral Cloud Chat Model` (chọn credentials Mistral Cloud).
- **GitHub & Reddit Nodes:** Mặc dù GitHub Repo Search có thể chạy không cần credentials, việc thêm token GitHub cá nhân được khuyến nghị để tránh bị giới hạn Rate Limit.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công bằng nút `When clicking ‘Execute workflow’` hoặc node `Schedule` để kiểm tra luồng dữ liệu qua các bước Split, Filter và AI Extractor.
- Sau khi test thành công, bật trạng thái **Active** cho workflow để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo:** Kết nối thêm node Telegram hoặc Slack ở cuối workflow để nhận ngay danh sách các nguồn tin mới được AI chọn lọc mỗi ngày.
- **Lưu trữ dữ liệu:** Thêm node Google Sheets hoặc Airtable ngay sau bước `Information Extractor` để lưu lại lịch sử các nguồn website tiềm năng phục vụ nghiên cứu dài hạn.
- **Tùy chỉnh giới hạn (Limit):** Điều chỉnh node `Limit` để kiểm soát số lượng website được AI cào và đánh giá, tránh vượt quá hạn mức API LLM.

### 📌 Kết luận
Workflow **Multi-Platform Source Discovery** là một trợ lý nghiên cứu đắc lực, giúp tự động hóa hoàn toàn công đoạn tìm kiếm nguồn tài nguyên trên internet bằng sức mạnh của AI và Multi-Search Engines. Hãy áp dụng ngay vào hệ thống của các sếp để tối ưu hóa năng suất làm việc!