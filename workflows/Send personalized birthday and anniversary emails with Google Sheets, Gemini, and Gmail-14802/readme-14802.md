---
title: "🎂 Tự Động Gửi Email Chúc Mừng Sinh Nhật & Kỷ Niệm Ngày Với AI Gemini & Gmail"
description: "Workflow n8n tự động kiểm tra danh sách khách hàng trên Google Sheets, sử dụng AI Gemini để viết lời chúc cá nhân hóa kèm gợi ý đầu tư thông minh và gửi email qua Gmail mỗi ngày."
slug: "tu-dong-gui-email-chuc-mung-sinh-nhat-khoi-nhanh"
tags: [n8n, automation, no-code, google-sheets, gemini-ai, gmail, lead-nurturing]
keywords: [n8n workflow, tự động hóa email, chúc mừng sinh nhật tự động, gemini ai, google sheets automation]
---

# 🎂 Tự Động Gửi Email Chúc Mừng Sinh Nhật & Kỷ Niệm Ngày Với AI Gemini & Gmail

Trong lĩnh vực dịch vụ tài chính, ngân hàng hoặc bất kỳ ngành nào cần chăm sóc khách hàng (Customer Care), việc nhớ và gửi lời chúc sinh nhật hay kỷ niệm ngày thành lập cho khách hàng là một yếu tố then chốt để xây dựng mối quan hệ bền vững. Tuy nhiên, làm việc này thủ công là cực kỳ tốn thời gian, dễ bỏ sót và thiếu sự cá nhân hóa.

Workflow này giải quyết triệt để vấn đề đó bằng cách tự động hóa 100% quy trình:
1. **Quét danh sách khách hàng** trên Google Sheets mỗi ngày.
2. **Lọc ra** những người có sinh nhật hoặc kỷ niệm ngày hôm nay.
3. **Phân tích dữ liệu** (tuổi, mức độ rủi ro) để chọn gợi ý đầu tư phù hợp.
4. **Dùng AI Gemini** để viết một lời chúc ấm áp, chuyên nghiệp và cá nhân hóa.
5. **Gửi email** trực tiếp qua Gmail.

Không cần code, không cần thuê lập trình viên, các sếp chỉ cần setup một lần là có một "nhân viên chăm sóc khách hàng" AI hoạt động 24/7.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian thủ công:** Không cần ngồi gõ email chúc mừng hàng ngày.
- **Cá nhân hóa cực cao:** AI Gemini không chỉ chúc mừng mà còn đưa ra gợi ý đầu tư dựa trên tuổi và khẩu vị rủi ro của từng khách hàng, tạo cảm giác được quan tâm đặc biệt.
- **Chính xác & Không bỏ sót:** Hệ thống tự động đối chiếu ngày tháng, đảm bảo không ai bị "quên".
- **Nâng cao hình ảnh chuyên nghiệp:** Email được viết bằng ngôn ngữ tự nhiên, ấm áp, giúp tăng tỷ lệ phản hồi và lòng trung thành của khách hàng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google:** Để kết nối Google Sheets, Gmail và Gemini.
2. **Google Sheets:** Một bảng tính chứa danh sách khách hàng với các cột bắt buộc (xem chi tiết bên dưới).
3. **Google Gemini API Key:** Có thể lấy miễn phí từ [Google AI Studio](https://aistudio.google.com/).
4. **Tài khoản Gmail:** Dùng để gửi email (nên dùng tài khoản chuyên dụng cho chăm sóc khách hàng).
5. **Tài khoản n8n:** Cloud hoặc Self-hosted.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Vào trang [n8n.io/workflows/14802](https://n8n.io/workflows/14802).
- Nhấn nút **"Use this workflow"**.
- Nếu dùng n8n Self-hosted, các sếp có thể copy JSON và dán vào n8n Editor, hoặc import file JSON trực tiếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Sau khi import, các sếp cần cấu hình lại các node sau đây để workflow chạy đúng với dữ liệu của mình:

**A. Node: `Settings — Change These Before Running` (Loại: Set)**
Đây là node cấu hình trung tâm. Các sếp cần vào node này và chỉnh sửa các biến:
- **Sheet ID:** ID của file Google Sheet chứa danh sách khách hàng.
- **Sheet Name:** Tên tab trong Google Sheet (mặc định thường là `Sheet1`).
- **From Email:** Địa chỉ email người gửi (phải khớp với tài khoản Gmail đã kết nối).
- **Advisor Name:** Tên cố vấn hoặc tên công ty (dùng trong lời chào).

**B. Node: `Read Client List from Google Sheet` (Loại: Google Sheets)**
- Chọn **Credential**: Chọn tài khoản Google Sheets OAuth2 đã kết nối.
- Kiểm tra **Document ID** và **Sheet Name** khớp với cấu hình ở node `Settings`.
- **Lưu ý quan trọng về Cột dữ liệu:** Google Sheet của các sếp **BẮT BUỘC** phải có các cột sau (tên cột phải khớp chính xác hoặc các sếp cần chỉnh mapping trong node này):
    - `Client Name`
    - `Email`
    - `Advisor Name`
    - `Birthday` (Định dạng: YYYY-MM-DD hoặc DD/MM/YYYY tùy cấu hình)
    - `Anniversary`
    - `Relationship Type`
    - `Client Age`
    - `Risk Profile` (Ví dụ: Low, Medium, High)

**C. Node: `Ask Gemini to Write Personalised Wish` (Loại: Google Gemini)**
- Chọn **Credential**: Chọn API Key của Google Gemini.
- Kiểm tra **Prompt**: Node này đã được viết sẵn prompt để yêu cầu Gemini viết lời chúc dựa trên các biến đầu vào. Các sếp có thể chỉnh sửa prompt nếu muốn thay đổi giọng văn (ví dụ: trang trọng hơn, thân mật hơn).

**D. Node: `Send Personalised Wish Email to Client` (Loại: Gmail)**
- Chọn **Credential**: Chọn tài khoản Gmail OAuth2.
- Kiểm tra các trường `To`, `Subject`, `Html` đã được map từ node `Format Email Body and Delivery Fields` chưa.

**E. Node: `Run Every Day at 9 AM` (Loại: Schedule Trigger)**
- Mặc định chạy lúc 9:01 AM. Các sếp có thể chỉnh giờ tùy theo múi giờ và thời điểm khách hàng hay đọc email nhất.

#### 3. Kích hoạt ⚡️
1. **Test Run:** Nhấn nút **Execute Workflow** (hoặc chọn 1 dòng dữ liệu mẫu trong Google Sheet và nhấn Execute Node) để kiểm tra xem email có được tạo ra đúng ý không.
2. **Kiểm tra Email:** Mở hộp thư Gmail để xem email mẫu. Đảm bảo định dạng HTML đẹp, nội dung AI tự nhiên.
3. **Bật Active:** Nhấn công tắc **Active** ở góc trên bên phải để workflow bắt đầu chạy tự động mỗi ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm kênh thông báo nội bộ:** Thêm node **Slack** hoặc **Telegram** sau khi gửi email thành công để báo cho đội ngũ Sales/Care biết khách hàng nào vừa nhận được lời chúc, giúp họ follow-up kịp thời.
- **Lưu Log gửi email:** Thêm node **Google Sheets** (Append) hoặc **Airtable** để ghi lại lịch sử gửi email (ngày gửi, nội dung, trạng thái) nhằm tránh gửi trùng và phục vụ báo cáo.
- **Cá nhân hóa sâu hơn:** Nếu khách hàng có thêm thông tin như "Sở thích", "Lịch sử giao dịch", các sếp có thể thêm các cột này vào Google Sheet và cập nhật Prompt Gemini để lời chúc trở nên "thần thánh" hơn.
- **A/B Testing:** Tạo 2 nhánh với 2 phong cách lời chúc khác nhau (một bên trang trọng, một bên thân mật) và gửi ngẫu nhiên để đo lường tỷ lệ mở email (Open Rate) của khách hàng.

### 📌 Kết luận
Việc chăm sóc khách hàng không chỉ là bán hàng, mà là xây dựng niềm tin. Với workflow này, các sếp có thể biến những ngày đặc biệt của khách hàng thành cơ hội vàng để thể hiện sự chuyên nghiệp và quan tâm, tất cả đều được tự động hóa hoàn toàn bằng sức mạnh của AI Gemini và n8n.

Hãy import workflow, cấu hình Google Sheet của bạn và để AI làm phần còn lại! 🚀