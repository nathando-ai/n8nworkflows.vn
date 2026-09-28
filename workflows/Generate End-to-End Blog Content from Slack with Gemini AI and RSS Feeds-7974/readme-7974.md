---
title: "🚀 Tự Động Viết Blog Chuyên Sâu Từ Slack Với Gemini AI & RSS Feeds"
description: "Workflow n8n giúp các sếp tạo nội dung blog chất lượng cao, có nguồn trích dẫn từ RSS, chỉ bằng một lệnh chat trong Slack. Tiết kiệm 90% thời gian nghiên cứu và viết lách."
slug: "tu-dong-viet-blog-slack-gemini-rss"
tags: [n8n, automation, no-code, gemini-ai, content-marketing, slack]
keywords: [n8n workflow, tự động hóa content, gemini ai, viết blog tự động, rss feed]
---

# 🚀 Tự Động Viết Blog Chuyên Sâu Từ Slack Với Gemini AI & RSS Feeds

Viết nội dung blog không chỉ là gõ chữ, mà là quá trình nghiên cứu, tổng hợp thông tin từ nhiều nguồn và chắt lọc ra những insight giá trị. Làm thủ công, các sếp thường mất hàng giờ mỗi ngày để đọc tin tức, ghi chú lại các link tham khảo và sau đó mới bắt đầu viết. Điều này không chỉ tốn thời gian mà còn dễ gây "bội thực" thông tin, dẫn đến nội dung thiếu chiều sâu hoặc thiếu nguồn trích dẫn uy tín.

Workflow này giải quyết triệt để vấn đề đó. Nó kết hợp sức mạnh của **Gemini AI** với dữ liệu thời gian thực từ **RSS Feeds** và giao diện trực quan của **Slack**. Các sếp chỉ cần gõ một lệnh đơn giản trong Slack, hệ thống sẽ tự động quét các nguồn tin tức, phân cụm chủ đề, và cuối cùng sinh ra một bản nháp blog hoàn chỉnh, có cấu trúc rõ ràng và kèm theo các nguồn tham khảo thực tế.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, đặc biệt khi cần xử lý các yêu cầu AI phức tạp, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian nghiên cứu:** AI tự động quét và tổng hợp dữ liệu từ RSS, loại bỏ bước tìm kiếm thủ công.
- **Nội dung có nguồn trích dẫn (Citation):** Không còn là "hallucination" (ảo giác) của AI, bài viết dựa trên dữ liệu thực tế từ các feed tin tức.
- **Quy trình làm việc liền mạch trong Slack:** Từ ý tưởng đến bản nháp, tất cả diễn ra ngay trong kênh chat làm việc, không cần chuyển đổi tab.
- **Cá nhân hóa chủ đề:** Các sếp có thể chọn chủ đề cụ thể từ danh sách gợi ý do AI phân cụm, đảm bảo nội dung đúng trọng tâm.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n:** Chạy local hoặc self-hosted.
2. **Slack Workspace:**
   - Tạo một App Slack (hoặc dùng App có sẵn) và cấp quyền: `chat:write`, `channels:history`, `reactions:read`.
   - Invite bot vào kênh mà các sếp muốn tương tác.
3. **Google Gemini API Key:**
   - Đăng ký tại [Google AI Studio](https://aistudio.google.com/).
   - Tạo API Key mới.
4. **RSS Feeds:**
   - Chuẩn bị 2-3 link RSS từ các nguồn tin tức/blog uy tín trong ngành của các sếp (ví dụ: TechCrunch, Hacker News, hoặc blog đối thủ).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from URL** hoặc **Import from File** (nếu các sếp đã tải file JSON về).
3. Dán link workflow gốc hoặc chọn file JSON đã tải.
4. Workflow sẽ hiển thị với 15 nodes chính.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Đây là phần quan trọng nhất. Các sếp cần cấu hình từng node sau:

**A. Cấu hình Credentials**
- **Slack:** Tại các node có icon Slack (`Slack: Incoming messages`, `Slack: post_topic_list`, `Slack: fetch_thread_replies`, `Slack: post_draft`), các sếp cần chọn credentials Slack đã tạo.
- **Google Gemini:** Tại các node `Gemini: cluster_to_topics` và `Gemini: write_draft`, chọn credentials Google Gemini (API Key).

**B. Cấu hình RSS Feeds (Nodes: `RSS Read`, `RSS Read1`, `RSS Read2`)**
- Mở từng node RSS.
- Điền **Feed URL** vào trường `Url`.
  - *Ví dụ:* `https://techcrunch.com/feed/`
- Các sếp có thể chỉnh `Limit` (số lượng bài đọc) để tối ưu tốc độ và chi phí API.

**C. Cấu hình Logic & AI**
1. **Node `Code: parse_slack_command`**:
   - Kiểm tra lại logic parse lệnh. Mặc định workflow có thể chờ lệnh như `/blog` hoặc `write blog`. Các sếp có thể sửa code trong node này để thay đổi trigger command cho phù hợp với team.
2. **Node `Switch: route_by_command`**:
   - Đảm bảo các điều kiện (conditions) khớp với lệnh mà các sếp định dùng trong Slack.
3. **Node `Gemini: cluster_to_topics`**:
   - Đây là bước AI phân cụm các bài RSS thành các chủ đề chính.
   - Các sếp nên chỉnh sửa **System Prompt** hoặc **User Prompt** để yêu cầu AI phân cụm theo góc nhìn cụ thể (ví dụ: "Phân cụm theo xu hướng kỹ thuật", "Phân cụm theo vấn đề kinh doanh").
4. **Node `Gemini: write_draft`**:
   - Đây là "trái tim" của workflow.
   - **Prompt Engineering:** Các sếp cần chỉnh prompt ở đây để định dạng đầu ra.
     - *Yêu cầu:* Bài viết cần có tiêu đề, intro, các section chính, và **bắt buộc** phải trích dẫn nguồn từ dữ liệu input.
     - *Giọng văn:* Chỉnh giọng văn (Tone of Voice) cho phù hợp với thương hiệu (ví dụ: chuyên nghiệp, thân thiện, kỹ thuật).
     - *Độ dài:* Quy định số từ mong muốn (ví dụ: 1000-1500 từ).

**D. Cấu hình Output Slack**
- **Node `Slack: post_topic_list`**: Chọn kênh (Channel ID) nơi AI sẽ gửi danh sách chủ đề gợi ý.
- **Node `Slack: post_draft`**: Chọn kênh nơi AI sẽ gửi bản nháp bài viết.

#### 3. Kích hoạt ⚡️
1. **Test Run:**
   - Bật nút **Active** (hoặc dùng nút **Test Workflow** ở góc trên bên phải).
   - Vào Slack, vào kênh đã cấu hình, gõ lệnh (ví dụ: `write blog`).
   - Chờ AI xử lý (có thể mất 30s - 2 phút tùy độ phức tạp).
   - Kiểm tra xem AI có trả về danh sách chủ đề không.
   - Reply vào thread với tên chủ đề mong muốn (hoặc số thứ tự, tùy logic code).
   - Chờ bản nháp blog được gửi lại.
2. **Bật Active:**
   - Nếu kết quả ưng ý, bật **Active** để workflow chạy nền liên tục.

### ✍️ Mẹo & gợi ý nâng cao

- **Tích hợp WordPress/Notion:** Thay vì chỉ post vào Slack, các sếp có thể thêm node `WordPress` hoặc `Notion` sau bước `Slack: post_draft` để tự động đẩy bài viết vào CMS hoặc lưu vào kho kiến thức.
- **Thêm bước Review Human-in-the-loop:** Thay vì AI tự động post draft, hãy để AI gửi draft vào Slack và yêu cầu người dùng gõ "Approve" để kích hoạt bước đăng bài lên website. Điều này đảm bảo chất lượng nội dung trước khi công khai.
- **Cá nhân hóa Prompt theo Ngành:** Nếu các sếp làm trong ngành Y tế, Tài chính, hãy cập nhật prompt trong node `Gemini: write_draft` để thêm các ràng buộc về độ chính xác và tuân thủ quy định ngành.
- **Lịch chạy định kỳ:** Thay vì chờ lệnh từ Slack, các sếp có thể thêm node `Schedule Trigger` để workflow tự động quét RSS và tạo bản nháp vào mỗi sáng thứ Hai, gửi vào kênh `#content-ideas` để team brainstorm.

### 📌 Kết luận

Việc kết hợp **RSS Feeds** (dữ liệu thực) với **Gemini AI** (sức mạnh tổng hợp) và **Slack** (giao diện làm việc) tạo nên một quy trình sản xuất nội dung cực kỳ hiệu quả. Các sếp không còn phải lo lắng về việc tìm kiếm thông tin hay viết từ số 0. Workflow này biến các sếp từ "người viết lách" thành "người biên tập", tập trung vào việc kiểm duyệt và tinh chỉnh thay vì làm việc nặng nhọc.

Hãy import workflow này, cấu hình theo ngành nghề của các sếp và trải nghiệm sự khác biệt trong quy trình Content Marketing ngay hôm nay! 🚀