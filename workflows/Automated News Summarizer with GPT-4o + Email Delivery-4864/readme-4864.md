---
title: "📰 Tự Động Hóa Tin Tức: Tóm Tắt AI GPT-4o & Gửi Mail Hàng Ngày"
description: "Workflow n8n tự động kéo tin tức, tóm tắt bằng GPT-4o và gửi báo cáo cá nhân hóa qua Gmail cho danh sách khách hàng trong Google Sheets."
slug: "tu-dong-hoa-tin-tuc-gpt-4o-gui-mail"
tags: [n8n, automation, no-code, ai, openai, gmail, google-sheets]
keywords: [n8n workflow, tự động hóa tin tức, ai summarizer, gửi mail tự động, gpt-4o]
---

# 📰 Tự Động Hóa Tin Tức: Tóm Tắt AI GPT-4o & Gửi Mail Hàng Ngày

Trong kỷ nguyên thông tin bùng nổ, việc cập nhật tin tức hàng ngày là một thách thức lớn. Các sếp thường phải dành hàng giờ mỗi sáng để lướt qua hàng chục trang báo, mạng xã hội và blog chuyên ngành chỉ để tìm ra những thông tin thực sự giá trị. Làm thủ công không chỉ tốn thời gian mà còn dễ bỏ sót những insight quan trọng, hoặc ngược lại, bị "ngập" trong những tin tức không liên quan.

Workflow **"Automated News Summarizer with GPT-4o + Email Delivery"** chính là giải pháp "cứu cánh" cho vấn đề này. Với sự kết hợp giữa **OpenAI GPT-4o** (hoặc GPT-4o-mini) và **n8n**, quy trình này sẽ tự động thu thập tin tức từ các nguồn tin cậy, sử dụng AI để tóm tắt ngắn gọn, dễ hiểu và gửi thẳng vào hộp thư Gmail của các sếp hoặc danh sách khách hàng của bạn. Toàn bộ quá trình diễn ra tự động 100%, không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian cực đại:** Biến hàng giờ đọc tin thành 5 phút xem bản tin tóm tắt.
- **Thông tin chính xác & Tập trung:** AI lọc bỏ nhiễu, chỉ giữ lại các điểm chính quan trọng nhất.
- **Cá nhân hóa quy mô lớn:** Dễ dàng gửi bản tin riêng biệt cho hàng trăm/thousands người nhận qua Google Sheets.
- **Hoạt động liên tục:** Chạy tự động theo lịch (ví dụ: 7h sáng mỗi ngày) mà không cần sự can thiệp của con người.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị:
1. **Tài khoản OpenAI:** Có API Key để sử dụng mô hình GPT-4o hoặc GPT-4o-mini.
2. **Tài khoản Google:**
   - **Gmail:** Để gửi email (cần cấp quyền OAuth2).
   - **Google Sheets:** Để lưu danh sách email người nhận (cần cấp quyền OAuth2).
3. **Nguồn tin tức (News Source):** Một URL RSS feed hoặc API tin tức mà các sếp muốn theo dõi (ví dụ: TechCrunch, BBC, VnExpress...).
4. **Tài khoản n8n:** Cloud hoặc Self-hosted.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from URL** và dán link: `https://n8n.io/workflows/4864` HOẶC copy toàn bộ JSON code của workflow và dán vào **Import from Clipboard**.
3. Sau khi import, các sếp sẽ thấy 6 nodes chính được kết nối sẵn.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Đây là phần quan trọng nhất. Các sếp cần cấu hình lại các node sau để phù hợp với nhu cầu của mình:

*   **Node: `Schedule Trigger`**
    *   Mặc định có thể chạy theo giờ nhất định. Các sếp nên chỉnh lại thời gian gửi mail (ví dụ: `07:00` sáng mỗi ngày) để người nhận có thể đọc ngay khi bắt đầu ngày làm việc.

*   **Node: `Pull News` (HTTP Request)**
    *   Đây là node đi lấy dữ liệu tin tức.
    *   **URL:** Thay thế URL mặc định bằng RSS feed hoặc API tin tức mà các sếp quan tâm.
    *   **Method:** Thường là `GET`.
    *   **Response Format:** Chọn `JSON` hoặc `Text` tùy thuộc vào nguồn tin. Nếu dùng RSS, có thể cần thêm một node XML Parser (workflow gốc có thể đã xử lý hoặc cần các sếp thêm vào nếu dữ liệu đầu vào là XML). *Lưu ý: Workflow gốc dùng HTTP Request, hãy đảm bảo URL trả về định dạng mà AI có thể đọc được (thường là JSON hoặc Text thuần).*

*   **Node: `AI Agent`**
    *   Đây là "bộ não" của workflow.
    *   **System Prompt:** Các sếp nên chỉnh sửa prompt để định hướng AI tóm tắt theo phong cách mong muốn. Ví dụ: *"Bạn là một biên tập viên tin tức chuyên nghiệp. Hãy tóm tắt các tin tức sau thành 5 điểm chính, ngắn gọn, dễ hiểu và hấp dẫn. Sử dụng bullet points."*
    *   **Input:** Đảm bảo dữ liệu từ node `Pull News` được truyền vào đúng chỗ.

*   **Node: `OpenAI Chat Model`**
    *   **Credentials:** Chọn hoặc tạo mới credential OpenAI API.
    *   **Model:** Mặc định là `gpt-4o-mini` (rẻ và nhanh). Các sếp có thể đổi sang `gpt-4o` nếu cần độ chính xác cao hơn (chi phí cao hơn).

*   **Node: `Email list` (Google Sheets)**
    *   **Credentials:** Chọn credential Google Sheets OAuth2.
    *   **Document ID & Sheet Name:** Điền ID của file Google Sheets chứa danh sách email.
    *   **Columns:** Chọn cột chứa địa chỉ email (ví dụ: `Email`).
    *   **Lưu ý:** File Sheet cần có ít nhất một cột chứa email người nhận.

*   **Node: `Send Mail` (Gmail)**
    *   **Credentials:** Chọn credential Gmail OAuth2.
    *   **To:** Tham chiếu đến trường `email` từ node `Email list` (ví dụ: `={{ $json.email }}`).
    *   **Subject:** Có thể để tĩnh (ví dụ: "Bản tin công nghệ hôm nay") hoặc động (ví dụ: `={{ "Bản tin " + $now.format('DD/MM/YYYY') }}`).
    *   **Message:** Tham chiếu đến output của node `AI Agent` (nội dung tóm tắt).

#### 3. Kích hoạt ⚡️
1. **Test Run:** Nhấn nút **Execute Workflow** để chạy thử. Kiểm tra xem email có được gửi đi không và nội dung tóm tắt có đúng ý không.
2. **Bật Active:** Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow chạy tự động theo lịch đã thiết lập.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa dạng hóa nguồn tin:** Thay vì chỉ dùng 1 URL, các sếp có thể thêm nhiều node `HTTP Request` song song để kéo tin từ nhiều nguồn khác nhau (Tech, Tài chính, Kinh doanh) rồi gộp lại trước khi đưa vào AI.
- **Gửi qua Telegram/Slack:** Thay vì (hoặc bên cạnh) Gmail, các sếp có thể thêm node `Telegram` hoặc `Slack` để gửi bản tin trực tiếp vào nhóm chat công việc.
- **Lưu lịch sử:** Thêm node `Google Sheets` hoặc `Airtable` để lưu lại nội dung bản tin đã gửi, giúp các sếp có thể xem lại các tin tức quan trọng trong quá khứ.
- **Phân khúc người nhận:** Trong Google Sheets, thêm cột `Category` (ví dụ: Tech, Finance). Dùng node `IF` hoặc `Switch` để gửi các bản tin tóm tắt khác nhau cho các nhóm người nhận khác nhau.

### 📌 Kết luận
Workflow **Automated News Summarizer** là một công cụ cực kỳ hữu ích cho bất kỳ ai muốn cập nhật thông tin nhanh chóng và hiệu quả. Với sự hỗ trợ của AI GPT-4o, các sếp không chỉ tiết kiệm thời gian mà còn nâng cao chất lượng thông tin tiếp nhận. Hãy import workflow này ngay hôm nay, tùy chỉnh theo nhu cầu và bắt đầu trải nghiệm sự tiện lợi của tự động hóa! 🚀