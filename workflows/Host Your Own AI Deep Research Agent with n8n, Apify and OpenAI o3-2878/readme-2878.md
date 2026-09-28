---
title: "🚀 Tự chế tạo AI Deep Research Agent riêng với n8n, Apify và OpenAI o3"
description: "Hướng dẫn xây dựng hệ thống Deep Research tự động tương tự OpenAI o3 bằng n8n, kết hợp Apify crawl web thông minh và lưu báo cáo tự động vào Notion."
slug: "tu-che-tao-ai-deep-research-agent-voi-n8n-apify-openai"
tags: [n8n, automation, ai-agent, openai, notion, apify]
keywords: [n8n workflow, ai deep research, openai o3-mini, apify web scraper, tu dong hoa nghien cuu]
---

# 🚀 Tự chế tạo AI Deep Research Agent riêng với n8n, Apify và OpenAI o3

Các sếp có bao giờ cảm thấy ghen tị với tính năng **Deep Research** cực đỉnh của OpenAI (vốn chỉ dành cho tài khoản Pro) chưa? Việc tốn hàng giờ để tìm kiếm, tổng hợp tài liệu, đọc hàng tá trang web và viết báo cáo thủ công thực sự là một "cực hình" ngốn thời gian. 

Thay vì phụ thuộc vào các gói trả phí đắt đỏ, hôm nay tôi sẽ hướng dẫn các sếp tự dựng một **AI Deep Research Agent 100% tự động** ngay trên n8n của mình. Workflow này kết hợp sức mạnh của mô hình suy luận đỉnh cao **OpenAI o3-mini**, khả năng crawl web siêu tốc của **Apify**, và tự động đóng gói kết quả lên **Notion**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 (đặc biệt là các tiến trình nghiên cứu kéo dài), các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn quy trình nghiên cứu:** Chỉ cần nhập chủ đề qua Form, AI sẽ tự động lên câu hỏi làm rõ, tìm kiếm hàng loạt, cào dữ liệu web và tổng hợp báo cáo chuyên sâu.
- **Sử dụng mô hình suy luận o3-mini:** Đảm bảo độ chính xác, logic cao nhờ cơ chế "suy nghĩ" (chain-of-thought) vượt trội.
- **Chạy ngầm bất đồng bộ (Asynchronous):** Không cần treo trình duyệt, agent tự chạy ngầm và gửi thông báo khi hoàn tất.
- **Lưu trữ chuyên nghiệp:** Tự động tạo trang báo cáo hoàn chỉnh định dạng Markdown/Blocks cực đẹp trên Notion.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance** (Hỗ trợ sub-workflow và các node nâng cao).
- **Tài khoản OpenAI API** (Có quyền truy cập model `o3-mini`).
- **Tài khoản Apify** (Dùng để thay thế Firecrawl với chi phí rẻ hơn và tốc độ cực nhanh, lấy API Key tại [Apify](https://www.apify.com?fpr=414q6)).
- **Tài khoản Notion & Template Database** (Du-pli-cate mẫu Notion database tại [Jim's n8n DeepResearcher Database](https://jimleuk.notion.site/19486dd60c0c80da9cb7eb1468ea9afd?v=19486dd60c0c805c8e0c000ce8c87acf)).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n (Template ID: 2878) và Import trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Vì workflow này sử dụng kiến trúc Subworkflow và Recursive Looping (vòng lặp đệ quy) khá phức tạp với 64 nodes, các sếp cần chú ý các điểm sau:
- **Cấu hình Credentials:** 
  - Kết nối **OpenAI API Key** cho các node `OpenAI Chat Model`, `OpenAI Chat Model1`, `OpenAI Chat Model2`, `OpenAI Chat Model3`, `OpenAI Chat Model4`. Đảm bảo chọn model là `o3-mini`.
  - Kết nối **Apify API Key** tại node `RAG Web Browser` để thực hiện crawl web.
  - Kết nối **Notion API Key** cho các node như `Create Row`, `Get Existing Row`, `Set In-Progress`, `Set Done`, `Upload to Notion Page`.
- **Form Trigger & Subworkflow:**
  - Public workflow để form nhận diện truy vấn từ người dùng hoạt động trơn tru.
  - Kiểm tra kỹ các node gọi Subworkflow (`Initiate DeepResearch`, `Generate Report`, `Generate Learnings`) để đảm bảo chúng trỏ đúng ID của các subworkflow con trong hệ thống của bạn.
- **Thiết lập Độ sâu (Depth & Breadth):**
  - Mặc định hệ thống để Depth=1, Breadth=2 (mất tầm 5-10 phút). Nếu các sếp đẩy Depth=3, Breadth=5, thời gian chạy có thể lên tới hơn 2 tiếng và tốn nhiều token OpenAI hơn, hãy cân nhắc nhu cầu thực tế!

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test execution) bằng cách điền thông tin qua Form đầu vào (`On form submission`).
- Sau khi kiểm tra dữ liệu trả về Notion thành công, hãy bật **Active workflow** để đưa vào sử dụng chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo:** Thay vì chỉ lưu Notion, các sếp có thể gắn thêm node Telegram hoặc Slack ở cuối luồng để nhận thông báo ngay khi AI viết xong báo cáo.
- **Tối ưu hóa chi phí:** Có thể kết hợp thêm các công cụ như Jina.ai hoặc Perplexity.ai tại bước crawl dữ liệu để tăng độ phong phú cho nguồn tài liệu.
- **Self-hosting Notion blocks:** Nếu tự host n8n, có thể cài thêm các Community Node chuyển đổi Markdown sang Notion blocks để tăng tốc độ đẩy dữ liệu và giảm lỗi API.

### 📌 Kết luận
Với workflow này, các sếp đã sở hữu ngay một "chuyên gia nghiên cứu AI" thu nhỏ, sẵn sàng bóc tách mọi chủ đề phức tạp nhất mà không tốn một xu chi phí thuê dịch vụ ngoài. Chúc các sếp cài đặt thành công và "hacks" hiệu suất công việc tối đa!