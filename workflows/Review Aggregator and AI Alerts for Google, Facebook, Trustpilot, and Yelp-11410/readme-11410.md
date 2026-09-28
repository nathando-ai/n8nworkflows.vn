---
title: "🚀 Tự Động Hóa Review Tất Cả Các Nơi: AI Phân Tích & Cảnh Báo Ngay Lập Tức (Google, Facebook, Trustpilot, Yelp)"
description: "Workflow tự động thu thập, phân tích cảm xúc và cảnh báo đánh giá tiêu cực từ 4 nền tảng lớn nhất trên thế giới. Giúp doanh nghiệp tiết kiệm 100+ giờ/tháng, phản hồi nhanh chóng và đưa ra quyết định dựa trên dữ liệu AI. Báo cáo tuần tự động gửi qua email cho quản lý."
slug: "tieu-dong-hoa-review-ai-canh-bao-google-facebook-trustpilot-yelp"
tags: [n8n, automation, no-code, market-research, ai-summarization, google-reviews, facebook-reviews, trustpilot, yelp]
keywords: [n8n workflow review tự động, phân tích cảm xúc AI, cảnh báo đánh giá tiêu cực, báo cáo tuần tự doanh nghiệp, tự động hóa market research]
---

# 🚀 **Tự Động Hóa Review Tất Cả Các Nơi: AI Phân Tích & Cảnh Báo Ngay Lập Tức**

### **Giải pháp cho nỗi đau của các sếp:**
Hàng ngày, doanh nghiệp phải mất **giờ đồng hồ** để theo dõi đánh giá từ Google, Facebook, Trustpilot và Yelp. Nhưng chỉ khi nào **đánh giá tiêu cực** xuất hiện, các sếp mới phát hiện và phản hồi muộn. Kết quả? **Thiệt hại uy tín**, mất khách hàng, và mất cơ hội cải thiện dịch vụ kịp thời.

Workflow này **tự động hóa toàn bộ quy trình**:
✅ **Thu thập** tất cả đánh giá từ 4 nền tảng lớn nhất.
✅ **Phân tích cảm xúc** bằng AI (GPT-4) để nhận biết **đánh giá tiêu cực** ngay lập tức.
✅ **Cảnh báo Slack** cho team phản hồi nhanh chóng.
✅ **Lưu trữ** tất cả dữ liệu vào Google Sheets với **báo cáo tuần tự** tự động gửi qua email.
✅ **Tiết kiệm 100+ giờ/tháng** cho các sếp và đội ngũ marketing.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host** n8n trên VPS riêng. Với chi phí thấp nhưng hiệu suất cao:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (Đảm bảo tốc độ cao, không lag)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Phản hồi nhanh chóng**: Nhận **cảnh báo Slack ngay lập tức** khi có đánh giá tiêu cực, giảm thiệt hại uy tín.
- **Dữ liệu thống kê chi tiết**: Tất cả đánh giá được **lưu vào Google Sheets** với phân tích cảm xúc, điểm số, và vấn đề chính.
- **Báo cáo tuần tự tự động**: **Chỉ cần vào thứ Hai**, workflow sẽ tự động gửi **báo cáo tổng hợp 7 ngày** qua email cho quản lý.
- **Tiết kiệm thời gian**: **Không cần theo dõi thủ công** nữa, AI làm tất cả công việc nặng nhọc.
- **Cải thiện dịch vụ**: Nhận biết **vấn đề thường gặp** từ khách hàng và điều chỉnh kịp thời.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản API** cho các nền tảng:
   - **Google My Business API** (để lấy đánh giá Google).
   - **Facebook Graph API** (để lấy đánh giá Facebook).
   - **Trustpilot API** (nếu có kế hoạch mở rộng).
   - **Yelp API** (nếu cần).
✔ **Tài khoản Slack** (để nhận cảnh báo tiêu cực).
✔ **Google Sheets** (để lưu trữ tất cả đánh giá và báo cáo).
✔ **Tài khoản Gmail** (để gửi báo cáo tuần tự).
✔ **API Key OpenAI** (để phân tích cảm xúc và tổng hợp báo cáo).
✔ **Thông tin cấu hình**:
   - **Business ID** của doanh nghiệp trên mỗi nền tảng.
   - **URL liên kết** đến trang doanh nghiệp trên Google/Facebook/Yelp.
   - **Thời gian khu vực** (để điều chỉnh lịch chạy hàng ngày).

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
- **Tải file JSON** từ [n8n.io/workflows/11410](https://n8n.io/workflows/11410) và import vào **n8n Editor**.
- **Copy toàn bộ JSON** từ link trên và **dán vào n8n Editor** (tab "Import").

:::note[Lưu ý quan trọng]
- **Không chạy workflow ngay lập tức** sau khi import. Các sếp cần **cấu hình các node quan trọng** trước.
- **Test run** với dữ liệu mẫu trước khi bật **Active**.
:::

---

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **20 node**, nhưng các sếp chỉ cần chú ý đến **các node sau** để cấu hình:

##### **A. Node "Workflow Configuration" (Set)**
- **Điền thông tin cơ bản**:
  - `businessIdGoogle`, `businessIdFacebook`, `businessIdYelp`, `businessIdTrustpilot`: **ID doanh nghiệp** trên từng nền tảng.
  - `googleBusinessUrl`, `facebookBusinessUrl`, `yelpBusinessUrl`, `trustpilotBusinessUrl`: **URL trang doanh nghiệp** trên mỗi nền tảng.
  - `slackChannel`: **#channel Slack** để nhận cảnh báo.
  - `googleSheetId`: **ID Google Sheets** để lưu trữ dữ liệu.
  - `emailReport`: **Email** để nhận báo cáo tuần tự.
  - `timezone`: **Thời gian khu vực** (ví dụ: `Asia/Ho_Chi_Minh`).

##### **B. Node "Get Google/Facebook/Trustpilot/Yelp Reviews" (HTTP Request)**
- **Mỗi node này** đều cần **API Key** và **Business ID** tương ứng.
- **Cấu hình URL API** theo tài liệu của từng nền tảng:
  - **Google**: `https://www.googleapis.com/...` (sử dụng `Google My Business API`).
  - **Facebook**: `https://graph.facebook.com/...` (sử dụng `Facebook Graph API`).
  - **Yelp**: `https://api.yelp.com/v3/...` (nếu có API Key).
  - **Trustpilot**: `https://api.trustpilot.com/...` (nếu có API Key).

##### **C. Node "Sentiment Analysis (GPT-4)" (OpenAI)**
- **Chọn credentials**: `openAiApi` (đã cấu hình trước).
- **Không cần chỉnh sửa Prompt** (đã tối ưu sẵn), nhưng các sếp có thể **cập nhật** nếu muốn:
  ```json
  "prompt": "Analyze the following review and provide:
  1. Sentiment (Positive/Negative/Neutral)
  2. Score (1-10)
  3. Key issues or highlights
  4. Short summary"
  ```

##### **D. Node "Alert - Negative Review" (Slack)**
- **Chọn credentials**: `slackApi` (đã cấu hình trước).
- **Cấu hình message template** (nếu muốn thay đổi nội dung cảnh báo):
  ```json
  "text": "🚨 **Negative Review Alert** 🚨\nPlatform: {{$node["Get {{platform}} Reviews"].json["platform"]}}\nRating: {{$node["Get {{platform}} Reviews"].json["rating"]}}\nReview: {{$node["Get {{platform}} Reviews"].json["text"]}}\nAuthor: {{$node["Get {{platform}} Reviews"].json["author"]}}\nURL: {{$node["Get {{platform}} Reviews"].json["url"]}}"
  ```

##### **E. Node "Log Review to Sheet" (Google Sheets)**
- **Chọn credentials**: `googleApi`.
- **Đảm bảo Sheet có cột** phù hợp với dữ liệu được gửi:
  - `platform`, `rating`, `text`, `date`, `author`, `url`, `sentiment`, `score`, `key_issues`, `summary`.

##### **F. Node "Daily Schedule - 09:00" (Schedule Trigger)**
- **Không cần chỉnh** nếu muốn chạy **mỗi ngày lúc 9h**.
- Nếu muốn **đổi giờ**, chỉnh `cron` trong node này (ví dụ: `0 3 9 * * ?` để chạy lúc 9h sáng).

##### **G. Node "Check If Monday (Weekly Report)" (If)**
- **Không cần chỉnh** nếu muốn **báo cáo tự động vào thứ Hai**.
- Nếu muốn **đổi ngày**, chỉnh `condition` trong node này (ví dụ: `{{$node["Daily Schedule - 09:00"].json["date"].split("-")[1]}} == "02"` để chạy vào ngày 2 của tháng).

---

#### **3. Kích hoạt ⚡️**
1. **Test run** với **dữ liệu mẫu** (chọn node "Daily Schedule - 09:00" và nhấn **Execute**).
2. **Kiểm tra**:
   - **Slack**: Có nhận được cảnh báo tiêu cực không?
   - **Google Sheets**: Dữ liệu có được lưu đúng không?
   - **Email**: Báo cáo tuần có được gửi không?
3. **Bật Active** workflow nếu tất cả chạy đúng.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH LÀM NÀY ĐỂ TIẾT KIỆM THÊM THỜI GIAN]
- **Kết hợp với Zapier/Integromat**: Nếu không muốn tự host n8n, các sếp có thể **mua plan Pro** của Zapier và tự tạo workflow tương tự.
- **Lưu log vào Notion**: Thay vì Google Sheets, các sếp có thể **lưu dữ liệu vào Notion** để dễ dàng chia sẻ với team.
- **Cảnh báo Telegram**: Thay vì Slack, các sếp có thể **cảnh báo qua Telegram** bằng node `telegram`.
- **Báo cáo định kỳ khác**: Ngoài tuần, các sếp có thể **cấu hình báo cáo tháng** bằng cách thêm node `scheduleTrigger` mới.
- **Phân tích từ khóa**: Sử dụng **node `code`** để **tách ra các từ khóa** trong đánh giá (ví dụ: "chậm", "tốt", "giá cao") và **tạo báo cáo từ khóa**.
- **Gửi báo cáo qua WhatsApp**: Sử dụng **node `whatsapp`** (nếu có API) để gửi báo cáo cho quản lý.
- **Tự động trả lời tiêu cực**: Nếu muốn **trả lời tự động**, các sếp có thể thêm node `email` hoặc `facebookMessenger` để gửi phản hồi chuẩn.
:::

---

### 📌 **Kết luận**
Workflow này **giải quyết hoàn toàn** vấn đề **tự động hóa theo dõi review** và **phân tích cảm xúc** cho doanh nghiệp. Với **AI GPT-4**, các sếp không chỉ **nhận cảnh báo tiêu cực** mà còn **nhận báo cáo tổng hợp chi tiết** mỗi tuần.

**Hành động ngay**:
1. **Import workflow** và **cấu hình các node quan trọng**.
2. **Test run** và **kiểm tra kết quả**.
3. **Bật Active** và **để AI làm việc cho bạn**.

**Kết quả?** **Tiết kiệm 100+ giờ/tháng**, **phản hồi nhanh chóng**, và **quản lý uy tín doanh nghiệp** một cách chuyên nghiệp!

---
**🚀 Cần hỗ trợ?** Đăng ký **hỗ trợ tự động hóa** tại [TinoHost](https://tino.vn/vps-n8n?affid=388) hoặc liên hệ với tác giả [Dragos Țugui](https://www.linkedin.com/in/dragostugui/) để **cải tiến workflow** phù hợp với doanh nghiệp của các sếp!