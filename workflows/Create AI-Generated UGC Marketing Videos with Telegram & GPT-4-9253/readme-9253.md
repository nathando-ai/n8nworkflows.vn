---
title: "🎬 Tự Động Hóa Video UGC AI: Tạo Quảng Cáo Từ Ảnh Sản Phẩm Chỉ Với 1 Tin Nhắn Telegram"
description: "Biến ảnh sản phẩm thành video quảng cáo UGC chuyên nghiệp, chân thực như người thật quay. Workflow n8n kết hợp GPT-4 và Key.AI giúp tiết kiệm 90% chi phí sản xuất nội dung."
slug: "tu-dong-hoa-video-ugc-ai-telegram"
tags: [n8n, automation, no-code, ai-video, marketing, telegram]
keywords: [n8n workflow, tạo video ai, ugc marketing, telegram bot, tự động hóa marketing]
---

# 🎬 Tự Động Hóa Video UGC AI: Tạo Quảng Cáo Từ Ảnh Sản Phẩm Chỉ Với 1 Tin Nhắn Telegram

Trong kỷ nguyên của TikTok và Reels, nội dung dạng UGC (User-Generated Content) đang thống trị thị trường. Tuy nhiên, việc sản xuất video UGC chất lượng cao thường đòi hỏi chi phí lớn cho diễn viên, quay phim và hậu kỳ. Làm sao để có hàng chục video quảng cáo chân thực, đa dạng nhân vật và kịch bản chỉ với chi phí vài đô la?

Workflow này chính là "vũ khí bí mật" giúp các sếp giải quyết bài toán đó. Chỉ cần gửi một bức ảnh sản phẩm (hoặc ảnh sản phẩm kèm nhân vật) vào Telegram Bot, hệ thống sẽ tự động phân tích, viết kịch bản, tạo hình ảnh nền, sinh video ngắn và ghép chúng lại thành một video quảng cáo hoàn chỉnh, sẵn sàng chạy ads. Toàn bộ quy trình diễn ra tự động 100%, không cần code, không cần can thiệp thủ công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, đặc biệt khi xử lý các tác vụ AI nặng (sinh video, ghép video), các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm chi phí khổng lồ:** Chi phí tạo 1 video UGC chỉ từ $0.5 - $2 (tùy chất lượng), thay vì hàng triệu đồng cho một clip thuê ngoài.
- **Tốc độ tức thì:** Từ lúc gửi ảnh đến lúc nhận video chỉ mất vài phút, thay vì vài ngày chờ duyệt kịch bản và quay.
- **Đa dạng hóa nội dung:** Có thể tạo video với nhiều nhân vật, bối cảnh, ngôn ngữ khác nhau từ cùng một sản phẩm để test A/B testing hiệu quả.
- **Cá nhân hóa sâu:** AI phân tích ảnh sản phẩm để tạo mô tả chính xác, đảm bảo video quảng cáo đúng với đặc tính thực tế của hàng hóa.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị các tài khoản và API keys sau:
1. **Tài khoản n8n:** Self-hosted hoặc Cloud.
2. **Telegram Bot:** Tạo qua @BotFather để nhận Bot Token.
3. **OpenAI API Key:** Dùng cho GPT-4.1 (phân tích ảnh, viết prompt) và mô hình phân tích hình ảnh.
4. **Key.AI API Key:** Dịch vụ tạo ảnh và video (AI Video Generation). Cần có gói trả phí hoặc credit để sinh video.
5. **File.AI API Key (hoặc dịch vụ tương tự):** Dùng cho node `Combine Clips` để ghép các đoạn video ngắn thành một file duy nhất (thường dùng FFmpeg).
6. **HTTP Header Auth:** Cấu hình cho các node gọi API của Key.AI và File.AI.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON workflow từ link gốc hoặc copy toàn bộ code JSON.
2. Mở n8n Editor, chọn **Import from URL** hoặc **Import from File**.
3. Dán JSON vào và nhấn **Import**.
4. Workflow sẽ hiển thị với 25 nodes, bao gồm các agent AI, node Telegram, và các node HTTP Request để gọi API.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Đây là phần quan trọng nhất. Các sếp cần cấu hình credentials và tham số cho các node chính sau:

**A. Nhóm Node Telegram (Input & Output)**
- **`Telegram Trigger`**: Chọn credentials Telegram Bot đã tạo. Đảm bảo bot đang ở chế độ Polling hoặc Webhook (tùy cấu hình n8n).
- **`Bot ID`**: Node `Set` này thường chứa thông tin ID của bot hoặc user. Kiểm tra lại giá trị mặc định nếu cần.
- **`In Progress`** & **`Send Video`**: Chọn cùng credentials Telegram. Node `Send Video` sẽ gửi video hoàn chỉnh về chat.

**B. Nhóm Node AI (OpenAI & Agents)**
- **`GPT` (lmChatOpenAi)**: Chọn credentials OpenAI. Model mặc định là `gpt-4.1`. Các sếp có thể đổi sang `gpt-4o` hoặc `gpt-4-turbo` tùy ngân sách và tốc độ.
- **`UGCRobo - Image AI Agent`** & **`UGCRobo - Video AI Agent`**:
    - Đây là các Agent LangChain. Kiểm tra phần **System Prompt** bên trong agent.
    - Agent Image: Nhiệm vụ là phân tích ảnh đầu vào và tạo prompt để sinh ảnh UGC (giống ảnh chụp bằng iPhone).
    - Agent Video: Nhiệm vụ là viết kịch bản video, chia cảnh (scenes) và tính toán số lượng clip cần tạo dựa trên độ dài video mong muốn (ví dụ: 20s -> 3 clip 8s).
- **`Describe Img` (openAi)**: Chọn credentials OpenAI. Operation là `analyze`, resource là `image`. Node này dùng để trích xuất thông tin chi tiết từ ảnh sản phẩm (thương hiệu, màu sắc, mô tả).
- **`Structured Output 1` & `2`**: Đảm bảo schema output khớp với yêu cầu của các node HTTP Request phía sau (ví dụ: trả về JSON chứa `prompt`, `aspect_ratio`, `clips_count`).

**C. Nhóm Node HTTP Request (Key.AI & File.AI)**
- **`Create Image`**, **`Get Image`**, **`Create Video`**, **`Get Video`**:
    - Chọn credentials **HTTP Header Auth** đã cấu hình với API Key của **Key.AI**.
    - Kiểm tra URL endpoint và Body Request. Key.AI thường yêu cầu gửi `prompt`, `image_url` (nếu có), `aspect_ratio`.
    - Node `Get Image` và `Get Video` là các node **Polling** (kết hợp với node `Wait`). Chúng sẽ gọi API liên tục cho đến khi video/ảnh được sinh xong.
- **`Combine Clips`**:
    - Chọn credentials **HTTP Header Auth** cho **File.AI** (hoặc dịch vụ ghép video khác).
    - Body request cần chứa danh sách URL các đoạn video clip.
- **`Get Final Video`**: Gọi API để download video đã ghép xong.

**D. Nhóm Node Logic & Control**
- **`Split Out`**: Tách các item (các cảnh video) để xử lý song song.
- **`Wait`**, **`Wait 2`**, **`Wait 3`**: Các node chờ để tránh gọi API quá nhanh (rate limit) hoặc chờ quá trình sinh video hoàn tất. Các sếp có thể điều chỉnh thời gian chờ (ví dụ: 10s, 30s) tùy tốc độ xử lý của Key.AI.
- **`If`** & **`If 2`**: Kiểm tra trạng thái phản hồi từ API (thành công/thất bại) hoặc kiểm tra điều kiện logic (ví dụ: nếu video quá dài thì chia thêm clip).
- **`Aggregate`**: Gom lại tất cả các URL video clip sau khi sinh xong để gửi vào node ghép video.

#### 3. Kích hoạt ⚡️
1. **Test Run**:
    - Nhấn nút **Execute Workflow** hoặc gửi một tin nhắn mẫu từ Telegram Bot: *"Tạo video UGC 15 giây cho chai nước hoa này"* kèm theo ảnh sản phẩm.
    - Theo dõi log execution trong n8n. Đảm bảo các node AI trả về prompt đúng, node HTTP gọi API Key.AI thành công, và node ghép video hoạt động.
    - Kiểm tra video nhận được trên Telegram.
2. **Bật Active**:
    - Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải n8n.
    - Workflow sẽ bắt đầu lắng nghe tin nhắn từ Telegram Bot.

### ✍️ Mẹo & gợi ý nâng cao

- **Tối ưu Prompt cho Kịch bản**: Trong node `UGCRobo - Video AI Agent`, các sếp có thể chỉnh sửa System Prompt để yêu cầu AI tập trung vào các tính năng bán hàng cụ thể (USP) của sản phẩm. Ví dụ: *"Nhấn mạnh vào thành phần tự nhiên và giá thành rẻ"*.
- **Đa dạng hóa Nhân vật**: Thay vì chỉ dùng một nhân vật, các sếp có thể tạo nhiều workflow hoặc thêm logic để thay đổi nhân vật (nam/nữ, trẻ trung/trưởng thành) tùy theo đối tượng khách hàng mục tiêu.
- **Lưu trữ Video**: Thay vì chỉ gửi về Telegram, các sếp có thể thêm node `Google Drive` hoặc `Dropbox` sau node `Get Final Video` để lưu trữ tất cả video đã tạo, tạo thành một thư viện nội dung marketing.
- **Tích hợp lên Ads**: Kết nối thêm node `Facebook Ads` hoặc `TikTok Ads` để tự động tải video lên tài khoản quảng cáo và tạo chiến dịch mới ngay khi video được sinh ra.
- **Kiểm soát Chi phí**: Key.AI có hai chế độ `Fast` (rẻ, ~$0.40/clip) và `Quality` (đắt, ~$2/clip). Các sếp có thể thêm node `If` để hỏi người dùng chọn chất lượng nào trước khi sinh video, giúp kiểm soát ngân sách.

### 📌 Kết luận

Workflow **Create AI-Generated UGC Marketing Videos** là một giải pháp đột phá giúp các sếp chuyển đổi từ việc sản xuất nội dung thủ công, tốn kém sang quy trình tự động hóa thông minh. Với sự kết hợp giữa sức mạnh phân tích của GPT-4 và khả năng sinh video của Key.AI, các sếp có thể tạo ra hàng loạt video quảng cáo chất lượng cao, chân thực và đa dạng chỉ với chi phí cực thấp.

Hãy import workflow này vào n8n, cấu hình API keys và bắt đầu tạo ra những video UGC "khủng" cho chiến dịch marketing của bạn ngay hôm nay! 🚀