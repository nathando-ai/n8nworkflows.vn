---
title: "🛡️ Tự Động Giám Sát & Làm Mới SSL Certificate với Notion và Telegram"
description: "Workflow n8n tự động kiểm tra hạn SSL, cập nhật trạng thái lên Notion và gửi cảnh báo qua Telegram khi chứng chỉ sắp hết hạn, giúp bảo mật website luôn an toàn 24/7."
slug: "tu-dong-giam-sat-lam-moi-ssl-certificate"
tags: [n8n, automation, no-code, ssl, cybersecurity, notion, telegram]
keywords: [n8n workflow, tự động hóa SSL, giám sát chứng chỉ, bảo mật website, notional automation]
---

# 🛡️ Tự Động Giám Sát & Làm Mới SSL Certificate với Notion và Telegram

Việc quản lý chứng chỉ SSL (Secure Sockets Layer) cho nhiều website hoặc server thường là một "mỏ đau" đối với các đội ngũ DevOps hoặc quản trị viên hệ thống. Bạn có bao giờ lo lắng rằng một chứng chỉ SSL sẽ hết hạn vào giữa đêm, khiến website của bạn bị trình duyệt báo lỗi bảo mật, mất uy tín và ảnh hưởng đến SEO? Việc kiểm tra thủ công từng domain, ghi chép hạn hết vào Excel và nhớ lịch làm mới là một quy trình dễ sai sót và tốn thời gian.

Workflow này giải quyết triệt để vấn đề đó bằng cách tự động hóa toàn bộ quy trình:
1. **Kiểm tra** hạn SSL của các domain được lưu trữ trong Notion.
2. **Cập nhật** trạng thái và ngày hết hạn trực tiếp lên bảng Notion.
3. **Gửi cảnh báo** qua Telegram khi chứng chỉ sắp hết hạn.
4. **Tự động làm mới** (Renew) chứng chỉ trên server thông qua SSH (nếu cấu hình sẵn lệnh).

Tất cả diễn ra hoàn toàn tự động, không cần code, giúp các sếp yên tâm ngủ ngon mà không lo "đứt" bảo mật.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, đặc biệt là các tác vụ kiểm tra định kỳ (Schedule Trigger) và SSH, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Bảo mật liên tục:** Không bao giờ bỏ sót chứng chỉ SSL sắp hết hạn, tránh rủi ro bị tấn công hoặc mất khách hàng do lỗi bảo mật.
- **Trung tâm dữ liệu tập trung:** Tất cả thông tin SSL (Domain, Ngày hết hạn, Trạng thái) được lưu trữ và cập nhật tự động trên Notion, dễ dàng theo dõi.
- **Cảnh báo tức thì:** Nhận thông báo qua Telegram ngay khi phát hiện vấn đề, cho phép phản ứng nhanh chóng.
- **Tự động hóa vận hành:** Giảm tải công việc thủ công cho đội ngũ kỹ thuật, tập trung vào các tác vụ giá trị cao hơn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n:** Đã cài đặt và chạy (khuyến nghị Self-hosted).
2. **Tài khoản Notion:**
   - Tạo một Database (Bảng) để lưu danh sách các Domain/Website cần giám sát.
   - Các cột (Properties) cần có trong Database:
     - `Domain` (Text): Tên miền cần kiểm tra.
     - `Expiry Date` (Date): Ngày hết hạn (workflow sẽ tự cập nhật).
     - `Status` (Select/Text): Trạng thái (Valid, Expiring Soon, Expired).
   - Lấy **Integration Token** từ Notion Settings.
3. **Tài khoản Telegram:**
   - Tạo Bot qua @BotFather để lấy **Bot Token**.
   - Lấy **Chat ID** của kênh hoặc cá nhân nhận thông báo.
4. **SSH Access (Tùy chọn - cho chức năng Renew):**
   - Nếu muốn tự động làm mới SSL trên server, cần có **SSH Private Key** và quyền truy cập vào server nơi lưu trữ chứng chỉ.
   - Lệnh làm mới SSL (ví dụ: `certbot renew` hoặc lệnh riêng của server) cần được cấu hình trong node SSH.
5. **API Key (Tùy chọn):** Một số node HTTP Request có thể cần API key nếu sử dụng dịch vụ kiểm tra SSL bên thứ ba (workflow mặc định có thể dùng HTTPS request trực tiếp hoặc service như SSL Labs/Checkly, tùy cấu hình gốc).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow từ link gốc hoặc copy nội dung JSON.
2. Mở n8n Editor.
3. Chọn **Import from URL** (nếu có link) hoặc **Import from File** (nếu đã tải JSON).
4. Hoặc đơn giản nhất: Copy toàn bộ JSON, vào n8n, bấm `Ctrl + V` (hoặc `Cmd + V`) để dán trực tiếp vào canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này khá phức tạp với 21 nodes, bao gồm logic điều khiển (If/Merge), xử lý dữ liệu (Code/Set), và tích hợp dịch vụ (Notion/Telegram/SSH). Dưới đây là các điểm quan trọng cần cấu hình:

**A. Cấu hình Notion (Nodes: `Get SSL Info`, `Update SSL Info`)**
- **Credentials:** Chọn hoặc tạo credential `notionApi`.
- **Database ID:** Trong node `Get SSL Info`, các sếp cần điền đúng **Database ID** của bảng Notion chứa danh sách domain.
  - *Cách lấy:* Mở bảng Notion, vào Settings (biểu tượng bánh răng) -> Copy Database ID.
- **Mapping Fields:** Đảm bảo các trường trong Code node `Refresh SSL Status` và `Merge Content` khớp với tên cột trong Notion (ví dụ: `Domain`, `Expiry Date`).

**B. Cấu hình Logic Kiểm Tra (Nodes: `Check SSL`, `If`, `If1`, `If3`)**
- **Node `Check SSL` (HTTP Request):**
  - Kiểm tra URL mà node này gọi để lấy thông tin SSL. Nếu nó gọi một API bên thứ 3 (như SSL Labs), hãy đảm bảo API key (nếu có) được điền vào Header.
  - Nếu nó chỉ làm HTTPS request trực tiếp đến domain, hãy đảm bảo logic trong Code node tiếp theo xử lý được response.
- **Nodes `If`, `If1`, `If3`:**
  - Đây là các điểm rẽ nhánh logic. Các sếp cần kiểm tra điều kiện (Condition) trong mỗi node.
  - Ví dụ: `If` có thể kiểm tra xem SSL có hợp lệ không? `If1` có thể kiểm tra xem còn bao nhiêu ngày nữa thì hết hạn (ví dụ: < 7 ngày)?
  - Điều chỉnh ngưỡng cảnh báo (ví dụ: 7 ngày, 14 ngày) theo nhu cầu thực tế của doanh nghiệp.

**C. Cấu hình Telegram (Nodes: `Telegram`, `Telegram1`)**
- **Credentials:** Chọn hoặc tạo credential `telegramApi` với Bot Token.
- **Chat ID:** Trong phần `To`, điền **Chat ID** của kênh hoặc cá nhân nhận thông báo.
  - *Mẹo:* Gửi tin nhắn cho bot, sau đó dùng API `getUpdates` để lấy chat_id.
- **Nội dung tin nhắn:** Kiểm tra phần `Message` trong node Telegram. Workflow thường động (dynamic) dựa trên dữ liệu từ Notion (Domain, Ngày hết hạn). Đảm bảo cú pháp template string (`{{ $json.domain }}`) đúng.

**D. Cấu hình SSH (Node: `Renew Server Cert`)**
- **Credentials:** Chọn hoặc tạo credential `sshPrivateKey`.
  - **Host:** IP hoặc Domain của server cần làm mới SSL.
  - **Username:** User có quyền thực thi lệnh làm mới SSL (thường là `root` hoặc user có sudo).
  - **Private Key:** Dán nội dung file `.pem` hoặc `.key` vào ô Private Key.
- **Command:** Trong phần `Command`, điền lệnh làm mới SSL.
  - Ví dụ cho Let's Encrypt: `certbot renew --quiet`
  - Ví dụ cho Caddy: `systemctl reload caddy` (sau khi certbot renew).
  - *Lưu ý:* Chỉ bật node này nếu các sếp thực sự muốn tự động làm mới. Nếu chỉ muốn cảnh báo, có thể bỏ qua hoặc comment node này.

**E. Logic Trigger (Nodes: `Weekly Trigger`, `When clicking ‘Execute workflow’`, `When Executed by Another Workflow`)**
- Workflow hỗ trợ 3 cách kích hoạt:
  1. **Định kỳ:** `Weekly Trigger` (Mặc định chạy hàng tuần). Các sếp có thể đổi thành `Daily` hoặc `Hourly` tùy mức độ quan trọng.
  2. **Thủ công:** `When clicking ‘Execute workflow’` để test nhanh.
  3. **Từ workflow khác:** `When Executed by Another Workflow` để tích hợp vào hệ thống lớn hơn.
- Các node `Set Click Triggered`, `Set Weekly Triggered`, `Set anotherWorkflow Triggered` và `Select Who Triggered` (Merge) được dùng để đánh dấu nguồn kích hoạt, giúp logic xử lý linh hoạt hơn (ví dụ: chỉ gửi Telegram khi chạy định kỳ, không gửi khi test thủ công).

#### 3. Kích hoạt ⚡️
1. **Test Run:**
   - Bấm vào nút **Execute Workflow** (hoặc chọn trigger thủ công) để chạy thử.
   - Kiểm tra output của từng node, đặc biệt là `Check SSL` và `Update SSL Info`.
   - Đảm bảo dữ liệu được cập nhật đúng trên Notion và tin nhắn Telegram được gửi (nếu có điều kiện cảnh báo).
2. **Bật Active:**
   - Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải.
   - Workflow sẽ tự động chạy theo lịch `Weekly Trigger` (hoặc lịch đã chỉnh).

### ✍️ Mẹo & gợi ý nâng cao
- **Tăng tần suất kiểm tra:** Thay vì hàng tuần, các sếp có thể đổi `Weekly Trigger` thành `Daily` hoặc thậm chí `Hourly` cho các domain quan trọng. Chi phí API (nếu có) vẫn rất thấp.
- **Phân loại cảnh báo:** Sử dụng thêm node `If` để phân biệt mức độ nghiêm trọng. Ví dụ:
  - Hết hạn trong 3 ngày: Gửi Telegram + Email + Slack (Cấp độ cao).
  - Hết hạn trong 7 ngày: Chỉ gửi Telegram (Cấp độ trung bình).
- **Tích hợp Slack/Email:** Thêm node `Slack` hoặc `Email` bên cạnh `Telegram` để đa dạng kênh cảnh báo, đảm bảo không bỏ sót thông tin.
- **Lưu Log lịch sử:** Tạo một Database Notion khác để lưu lịch sử các lần kiểm tra và làm mới, giúp truy vết khi có sự cố.
- **Tự động làm mới cho nhiều server:** Nếu có nhiều server, có thể dùng node `Loop Over Items` để lặp qua danh sách server và thực thi lệnh SSH cho từng cái.

### 📌 Kết luận
Việc giám sát SSL thủ công là một rủi ro tiềm ẩn mà nhiều doanh nghiệp bỏ qua. Với workflow n8n này, các sếp có thể biến quy trình bảo mật thành một hệ thống tự động, thông minh và đáng tin cậy. Không chỉ tiết kiệm thời gian, mà còn tăng cường an ninh cho toàn bộ hệ thống website. Hãy import workflow, cấu hình Notion và Telegram, và để n8n lo phần còn lại!

Chúc các sếp triển khai thành công và luôn an toàn trên không gian mạng! 🚀🔒