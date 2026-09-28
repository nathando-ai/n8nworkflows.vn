---
title: "🔍 Tự Động Hóa Tìm Kiếm Subreddit Reddit Nhiều Lớp Lớn (OAuth2) - Tiết Kiệm 20 Phút/Ngày Cho Market Research"
description: "Workflow tự động hóa tìm kiếm subreddit Reddit với xác thực OAuth2, trả về danh sách subreddit phù hợp theo keyword và tiêu chí thành viên, giúp các sếp tiết kiệm thời gian nghiên cứu thị trường và tối ưu chiến lược marketing."
slug: "tu-dong-hoa-tim-kiem-subreddit-reddit-oauth2"
tags: [n8n, automation, market-research, reddit-api, oauth2, no-code]
keywords: [tự động hóa tìm kiếm subreddit reddit, market research reddit, api reddit oauth2, tự động hóa nghiên cứu thị trường, tìm kiếm subreddit theo keyword]
---

# 🔍 **Tự Động Hóa Tìm Kiếm Subreddit Reddit Nhiều Lớp Lớn (OAuth2) - Giải Pháp Tiết Kiệm Thời Gian Cho Market Research**

### **Nỗi Đau Của Các Sếp Trong Nghiên Cứu Thị Trường**
Bạn có bao giờ phải mất **20 phút/ngày** để thủ công tìm kiếm và lọc subreddit Reddit phù hợp với chiến lược marketing của mình? Hay phải đối mặt với **lỗi xác thực API** khi sử dụng các node cơ bản như *Get Many Subreddit*? Thậm chí, việc này còn tốn thêm **4 giờ** để tự xây dựng một workflow ổn định nếu không có kiến thức về OAuth2?

Workflow này được **Christian Moises** thiết kế để giải quyết vấn đề này **100% tự động hóa**, không cần code, và chỉ mất **20 phút** để triển khai. Hãy tưởng tượng: Bạn chỉ cần nhập **keyword**, **tiêu chí thành viên**, và **số lượng subreddit** cần tìm, workflow sẽ tự động trả về danh sách subreddit phù hợp, sẵn sàng để bạn phân tích và ứng dụng vào chiến lược!

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Thay vì mất 20 phút/ngày tìm kiếm thủ công, workflow hoạt động **liên tục 24/7** và trả về kết quả ngay lập tức.
- **Chính xác và toàn diện**: Lọc subreddit theo **keyword**, **số lượng thành viên** (min/max), và **số lượng kết quả** (limit), tránh bỏ sót hoặc sai sót.
- **Xác thực OAuth2 ổn định**: Khắc phục lỗi "Authorization Credentials" thường gặp khi sử dụng API Reddit trực tiếp.
- **Dữ liệu sạch và sẵn sàng phân tích**: Workflow **tự động xử lý và tổng hợp** dữ liệu, trả về format dễ dàng nhập vào Google Sheets, Excel, hoặc các công cụ BI khác.
- **Tích hợp dễ dàng**: Có thể kết nối với **Slack**, **Telegram**, hoặc **email** để thông báo kết quả tự động.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Reddit**:
   - Đăng ký tại [Reddit Developer Portal](https://www.reddit.com/prefs/apps) để tạo **OAuth2 Application**.
   - Lấy **Client ID** và **Client Secret** từ trang này.
2. **API Key và Credentials**:
   - Thêm **credentials OAuth2** trong n8n với tên `redditOAuth2Api` (cấu hình chi tiết ở phần sau).
3. **Tham số tìm kiếm**:
   - **Keyword**: Từ khóa để tìm subreddit (ví dụ: "tech", "marketing", "startup").
   - **min_members**: Số thành viên tối thiểu (ví dụ: 1000).
   - **max_members**: Số thành viên tối đa (ví dụ: 1000000).
   - **limit**: Số lượng subreddit trả về (ví dụ: 20).
4. **n8n Self-hosted** (khuyến nghị):
   - Để workflow chạy **liên tục** và không bị giới hạn bởi phiên bản cloud.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/7646) hoặc copy/paste JSON từ trang này.
- Mở **n8n Editor** và chọn **Import Workflow** (từ menu hàng đầu).
- Chọn file JSON đã tải hoặc dán JSON vào ô nhập liệu.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này bao gồm **5 node chính**, nhưng có **2 bước quan trọng** cần chú ý:

##### **A. Cấu Hình Credentials OAuth2 cho Reddit**
- Node **"Get many Subreddit"** yêu cầu **credentials OAuth2** để xác thực.
- **Cách thiết lập**:
  1. Trong n8n, vào **Credentials** (menu hàng đầu > Credentials).
  2. Nhấn **Add Credential** > Chọn **OAuth2**.
  3. Điền thông tin:
     - **Name**: `redditOAuth2Api` (phải trùng với node trong workflow).
     - **Authorization URL**: `https://www.reddit.com/api/v1/authorize`.
     - **Access Token URL**: `https://www.reddit.com/api/v1/access_token`.
     - **Client ID** và **Client Secret**: Lấy từ [Reddit Developer Portal](https://www.reddit.com/prefs/apps).
     - **Scopes**: `identity history modconfig modflair modlog modmail modposts modwiki modwiki_edit modconfig edit flair`.
     - **Grant Type**: `authorization_code`.
  4. Lưu và chọn `redditOAuth2Api` trong node **"Get many Subreddit"**.

##### **B. Thiết Lập Tham Số Tìm Kiếm**
- Node **"Edit Fields"** (type: `set`) là nơi bạn **cấu hình các tham số tìm kiếm**:
  - **Query**: Điền **keyword** bạn muốn tìm (ví dụ: `tech`).
  - **min_members**: Số thành viên tối thiểu (ví dụ: `1000`).
  - **max_members**: Số thành viên tối đa (ví dụ: `1000000`).
  - **limit**: Số lượng subreddit trả về (ví dụ: `20`).
- **Lưu ý**:
  - Các tham số này **phải được truyền vào node "Get many Subreddit"** thông qua **Execute a SubWorkflow** (nếu bạn muốn sử dụng cách tối ưu như hướng dẫn của tác giả).

##### **C. Sử Dụng SubWorkflow (Nếu Muốn Tối Ưu)**
Theo hướng dẫn của tác giả, nếu bạn gặp lỗi với node **"Get many Subreddit"** trực tiếp, hãy:
  1. Thay thế node này bằng **Execute a SubWorkflow**.
  2. Chọn **workflow này** (của bạn) làm subworkflow.
  3. Trong subworkflow, **node "Get many Subreddit"** sẽ hoạt động ổn định hơn.

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Nhấn **Run Workflow** và kiểm tra kết quả trong **Execution View**.
  - Đảm bảo dữ liệu trả về đúng format (danh sách subreddit với `name`, `members`, `url`).
- **Bật Active**:
  - Sau khi test thành công, chuyển workflow sang **Active**.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁCH TIẾP CẬN THÊM]
1. **Gửi Kết Quả Sang Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** sau node **Aggregate** để thông báo kết quả tự động.
   - Ví dụ: Khi workflow hoàn thành, nó sẽ gửi danh sách subreddit đến kênh Slack của bạn.

2. **Lưu Log Vào Google Sheets**:
   - Sử dụng node **Google Sheets** để ghi lại lịch sử tìm kiếm (keyword, ngày giờ, số lượng subreddit).
   - Cấu hình **append row** để dữ liệu mới được thêm vào sheet mỗi lần chạy.

3. **Tự Động Chạy Định Kỳ**:
   - Sử dụng **n8n Trigger Node** (ví dụ: **HTTP Request** hoặc **Schedule Node**) để chạy workflow hàng ngày/lần tuần.
   - Ví dụ: Chạy vào **sáng 7h hàng ngày** để cập nhật dữ liệu mới nhất.

4. **Tích Hợp Với LLM (AI Chatbot)**:
   - Sau khi lấy danh sách subreddit, bạn có thể gửi dữ liệu vào **LLM Node** (n8n-nodes-base.llm) để AI phân tích và tổng kết xu hướng thị trường.
   - Ví dụ: *"Tóm tắt 3 xu hướng chính trong subreddit tech có từ 1000-10000 thành viên"*.

5. **Lọc và Xử Lý Dữ Liệu**:
   - Sử dụng node **Set** hoặc **Function Node** để **lọc subreddit** theo tiêu chí cụ thể (ví dụ: chỉ giữ subreddit có `members > 5000`).
   - Sau đó, **tổng hợp** dữ liệu vào một format dễ đọc (JSON, CSV).

---
### 📌 **Kết Luận**
Workflow này không chỉ **giải quyết vấn đề lỗi OAuth2** mà còn **tự động hóa toàn bộ quy trình tìm kiếm subreddit**, giúp các sếp **tiết kiệm thời gian**, **tăng hiệu quả nghiên cứu thị trường**, và **cập nhật dữ liệu liên tục** mà không cần can thiệp thủ công.

**Hành động ngay hôm nay**:
1. **Import workflow** và cấu hình credentials OAuth2.
2. **Test với keyword** của bạn và điều chỉnh tham số `min_members`, `max_members`, `limit`.
3. **Kết nối với Slack/Google Sheets** để tự động hóa báo cáo.
4. **Chạy định kỳ** và theo dõi xu hướng thị trường một cách chuyên nghiệp!

---
**💡 Lưu ý cuối cùng**:
Nếu bạn gặp lỗi hoặc cần hỗ trợ, hãy tham khảo [hướng dẫn chính thức của Reddit API](https://www.reddit.com/dev/api/) hoặc để lại comment dưới bài viết này. Chúc các sếp thành công với chiến lược marketing của mình! 🚀