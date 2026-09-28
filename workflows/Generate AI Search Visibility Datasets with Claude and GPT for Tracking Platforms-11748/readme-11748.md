---
title: "🚀 Tự Động Hóa Tạo Dataset Prompt AI Search (GEO) với Claude & GPT"
description: "Workflow n8n tự động nghiên cứu doanh nghiệp và tạo ra 50 prompt tìm kiếm AI (tiếng Anh & Đức) để theo dõi khả năng hiển thị trên các nền tảng AI, giúp tối ưu chiến lược GEO."
slug: "tao-dataset-prompt-ai-search-geo"
tags: [n8n, automation, no-code, ai-search, geo, seo]
keywords: [n8n workflow, tự động hóa marketing, ai search visibility, geo optimization, prompt engineering]
---

# 🚀 Tự Động Hóa Tạo Dataset Prompt AI Search (GEO) với Claude & GPT

Trong kỷ nguyên của AI Search, việc xuất hiện trên các nền tảng như ChatGPT, Perplexity hay các trợ lý AI khác không còn là điều xa xỉ mà là yêu cầu sống còn. Tuy nhiên, để đo lường và tối ưu khả năng hiển thị (Visibility) này, bạn cần một bộ dữ liệu (dataset) các câu hỏi tìm kiếm (prompts) chính xác, đa dạng và phản ánh đúng hành vi của khách hàng mục tiêu.

Việc tạo thủ công hàng chục đến hàng trăm prompt chất lượng cao, đảm bảo tính tự nhiên và không chứa thương hiệu (unbranded), là một quá trình tốn thời gian và dễ mắc sai lệch. Workflow này giải quyết triệt để nỗi đau đó bằng cách kết hợp sức mạnh nghiên cứu web của **GPT** và khả năng sáng tạo ngôn ngữ tự nhiên của **Claude** để tự động sinh ra bộ dataset hoàn chỉnh, sẵn sàng để import vào các công cụ theo dõi AI Search Visibility (như allmo.ai).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, đặc biệt khi cần xử lý song song nhiều doanh nghiệp hoặc chạy định kỳ, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian nghiên cứu:** Tự động thu thập thông tin về persona, tính năng và giá trị cốt lõi của doanh nghiệp từ website.
- **Dataset chất lượng cao, đa dạng:** Kết hợp 3 phương pháp tạo prompt (câu hỏi phổ biến, từ khóa do GPT sinh, câu hỏi tự nhiên do Claude sinh) để đảm bảo độ phủ rộng.
- **Đa ngôn ngữ:** Tự động dịch dataset sang tiếng Đức (có thể chỉnh sửa prompt để dịch sang bất kỳ ngôn ngữ nào khác).
- **Sẵn sàng triển khai:** Xuất file CSV chuẩn, có thể import trực tiếp vào các nền tảng theo dõi GEO/AI Visibility.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Bản self-hosted hoặc cloud.
- **API Keys:**
    - **Anthropic API Key:** Cho các node Claude (cần quyền sử dụng model Claude Sonnet).
    - **OpenAI API Key:** Cho các node GPT (cần quyền sử dụng model GPT-4o-mini hoặc tương đương có hỗ trợ web search).
- **Dữ liệu đầu vào:** Tên công ty và URL website công khai (publicly accessible) của doanh nghiệp cần phân tích.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON workflow từ link gốc hoặc copy toàn bộ code JSON.
2. Mở n8n Editor, chọn **Import from URL** hoặc **Import from File**.
3. Dán JSON vào hoặc chọn file đã tải về.
4. Workflow sẽ hiển thị 23 nodes được kết nối logic từ Form Trigger đến Convert to File.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Đây là phần quan trọng nhất để workflow hoạt động đúng ý đồ của tác giả. Các sếp cần kiểm tra kỹ các node sau:

*   **Node `On form submission` (Form Trigger):**
    *   Đây là điểm bắt đầu. Đảm bảo form có 2 trường: `Company Name` và `Website URL`.
    *   Các sếp có thể thay đổi trigger này thành Webhook hoặc Google Sheets nếu muốn tự động hóa hàng loạt từ danh sách khách hàng.

*   **Node `GPT_company_research` (HTTP Request):**
    *   **Credentials:** Chọn credentials OpenAI đã tạo.
    *   **Model:** Đảm bảo model được chọn hỗ trợ **Web Search** (ví dụ: `gpt-4o-search-preview` hoặc các model mới nhất có tính năng này) để nó có thể "đọc" website của công ty.
    *   **Prompt:** Kiểm tra prompt trong body request. Nó yêu cầu AI trích xuất: Buyer Personas, Key Features, Value Proposition. Đây là nền tảng cho toàn bộ dataset.

*   **Node `Claude_text_writer` (Anthropic):**
    *   **Credentials:** Chọn credentials Anthropic.
    *   **Model:** Khuyến nghị dùng `claude-sonnet-4-5` hoặc model mạnh nhất hiện có để đảm bảo chất lượng ngôn ngữ tự nhiên.
    *   **Vai trò:** Node này chịu trách nhiệm biến dữ liệu thô từ GPT thành các câu hỏi tìm kiếm tự nhiên, giống con người thật.

*   **Node `GPT_keywords_return 5` (HTTP Request):**
    *   **Credentials:** OpenAI.
    *   **Vai trò:** Sinh ra 5 từ khóa tìm kiếm không chứa thương hiệu (non-branded keywords).
    *   **Lưu ý:** Prompt yêu cầu output dạng JSON. Đảm bảo model GPT tuân thủ format này.

*   **Node `Claude_text_writer_return7` (Anthropic):**
    *   **Vai trò:** Sinh ra 7 câu hỏi prompt tự nhiên dựa trên các yếu tố đã nghiên cứu.
    *   **Tùy chỉnh:** Nếu muốn tăng số lượng prompt, các sếp có thể sửa prompt trong node này (ví dụ: thay "7" bằng "10").

*   **Node `English full dataset` & `Code in JavaScript` (Các node Code):**
    *   Các node này xử lý logic gộp dữ liệu (Merge), làm sạch (Clean-up) và định dạng lại.
    *   **Lưu ý:** Nếu các sếp thay đổi số lượng prompt sinh ra ở các node AI phía trước, có thể cần điều chỉnh logic trong các node Code này để tránh lỗi index hoặc thiếu dữ liệu.

*   **Node `Claude_text_writer-first12` (Anthropic - Optional Translation):**
    *   **Vai trò:** Dịch dataset tiếng Anh sang tiếng Đức (theo mặc định của workflow gốc).
    *   **Tùy chỉnh:** Nếu các sếp không cần tiếng Đức, hãy **xóa nhánh này** hoặc sửa prompt để dịch sang tiếng Việt/Tiếng Tây Ban Nha... tùy nhu cầu. Nếu không cần dịch, hãy nối trực tiếp từ `Merge2` sang `Set required fields for upload`.

*   **Node `Set required fields for upload` (Code):**
    *   Node này thêm các trường metadata như `model`, `language`, `source` vào từng dòng dữ liệu.
    *   Các sếp nên kiểm tra xem các trường này có khớp với yêu cầu import của công cụ theo dõi AI Search mà các sếp đang dùng (ví dụ: allmo.ai) không.

*   **Node `Convert to File`:**
    *   Đảm bảo output là file **CSV**. Đây là định dạng phổ biến nhất để import vào các dashboard marketing.

#### 3. Kích hoạt ⚡️
1. **Test Run:**
    *   Nhấn nút **Execute Workflow**.
    *   Một form sẽ hiện ra. Nhập tên công ty (ví dụ: "TinoHost") và URL website (ví dụ: "https://tino.vn").
    *   Chờ khoảng 2-5 phút. Workflow sẽ chạy qua các bước: Nghiên cứu -> Sinh Prompt EN -> Dịch Prompt DE -> Gộp -> Xuất file.
    *   Kiểm tra node `Convert to File` để tải về file CSV và xem thử nội dung.
2. **Bật Active:**
    *   Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải.
    *   Copy link Form Trigger để chia sẻ hoặc nhúng vào website/email cho team marketing sử dụng.

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động hóa hàng loạt:** Thay vì dùng Form Trigger, hãy thay bằng **Google Sheets Trigger**. Mỗi khi có một dòng mới trong Sheet chứa tên công ty và URL, workflow sẽ tự động chạy và gửi file CSV về email hoặc lưu vào Google Drive.
- **Mở rộng ngôn ngữ:** Workflow gốc có nhánh dịch sang tiếng Đức. Các sếp có thể nhân bản nhánh này và sửa prompt trong node Claude để dịch sang tiếng Nhật, tiếng Pháp... nhằm theo dõi visibility trên thị trường quốc tế.
- **Tích hợp Slack/Telegram:** Thêm node **Slack** hoặc **Telegram** sau bước `Convert to File` để gửi thông báo "Dataset đã sẵn sàng" kèm link tải file xuống kênh làm việc của team.
- **Lưu trữ lịch sử:** Thêm node **Google Sheets** hoặc **Postgres** trước bước xuất file để lưu lại toàn bộ dataset đã tạo theo thời gian, giúp các sếp so sánh sự thay đổi của các prompt theo từng quý.

### 📌 Kết luận
Việc theo dõi AI Search Visibility (GEO) đang trở thành kỹ năng bắt buộc cho các đội ngũ Growth và Marketing hiện đại. Workflow này không chỉ giúp các sếp tiết kiệm hàng giờ làm việc thủ công mà còn đảm bảo chất lượng dataset nhờ sự kết hợp hoàn hảo giữa khả năng thu thập dữ liệu thực tế của GPT và sự tinh tế trong ngôn ngữ của Claude.

Hãy import workflow, cấu hình API keys và bắt đầu xây dựng bộ dữ liệu theo dõi AI Search đầu tiên của bạn ngay hôm nay! 🚀