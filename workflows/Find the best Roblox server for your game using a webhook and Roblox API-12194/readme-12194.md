---
title: "🚀 Tự động tìm Server Roblox tốt nhất bằng Webhook và n8n API"
description: "Hướng dẫn xây dựng workflow n8n tự động quét, phân tích và tìm kiếm server Roblox mượt mà nhất, tối ưu ping và FPS cho game thủ."
slug: "tim-server-roblox-tot-nhat-bang-n8n"
tags: [n8n, automation, roblox, webhook, api, gaming]
keywords: [n8n workflow, tìm server roblox tốt nhất, roblox api, tự động hóa n8n, webhook roblox]
---

# 🚀 Tự động tìm Server Roblox tốt nhất với n8n và Webhook

Các sếp là game thủ Roblox và luôn cảm thấy khó chịu khi phải vào nhầm những server lag tung chảo, ping cao hoặc "vắng như chùa bà đanh"? Việc tìm kiếm thủ công một server mượt mà, nhiều người chơi thực sự tốn rất nhiều thời gian. 

Thay vì mò mẫm thủ công, bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ thông minh do tác giả **Gwa Shark** xây dựng. Workflow này sẽ tiếp nhận yêu cầu qua Webhook, gọi trực tiếp đến Roblox API, tính toán các thông số (Ping, FPS, số lượng người chơi) và trả về Deeplink dẫn trực tiếp đến server hoàn hảo nhất chỉ trong tích tắc!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và sẵn sàng phục vụ bất cứ lúc nào, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tối ưu trải nghiệm chơi game:** Tự động lọc ra server có ping thấp nhất, FPS cao nhất và đông vui nhất.
- **Tiết kiệm thời gian:** Không cần phải load vào game rồi thoát ra liên tục để tìm server ngon.
- **Tích hợp linh hoạt:** Hoạt động thông qua Webhook, dễ dàng gọi từ trình duyệt, extension hoặc các ứng dụng bên thứ ba.
- **Hoạt động tự động 24/7:** Không yêu cầu cấu hình phức tạp hay tài khoản trả phí từ Roblox.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động (Self-hosted hoặc n8n Cloud).
- Không bắt buộc phải có tài khoản hay Roblox Cookies (hoàn toàn tùy chọn).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy mã JSON của workflow từ n8n template (ID: `12194`) và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 11 nodes chính được thiết kế tối ưu, bao gồm:
- **Webhook**: Lắng nghe yêu cầu với đường dẫn mặc định là `/brsf`. Các sếp có thể thay đổi path này trong cài đặt node nếu muốn.
- **Place ID Set? & Auto Config**: Kiểm tra xem người dùng đã truyền tham số `plid` (Place ID của game Roblox) hay chưa. Nếu thiếu sẽ được chuyển hướng sang node **Error #1** và trả về thông báo lỗi.
- **Fetch Public Servers**: Node `httpRequest` thực hiện gọi API công khai của Roblox để lấy danh sách toàn bộ server hiện có của tựa game đó.
- **Filter For The Best**: Node `code` sử dụng Javascript để xử lý thuật toán thông minh lựa chọn server dựa trên các chế độ (Modes):
  - *Ping Mode*: Chọn server có ping thấp nhất.
  - *Latency Mode*: Ping thấp nhất kèm FPS cao nhất làm tiêu chí phụ.
  - *Auto Mode*: Nếu ping chênh lệch dưới 5ms, ưu tiên server có nhiều người chơi nhất để tránh server "dead".
- **Respond with Success / Respond to Webhook**: Trả về kết quả cuối cùng dưới định dạng JSON chứa Roblox Deeplink:
  ```json
  {
    "succsess": true,
    "result": "roblox:// Deeplink"
  }
  ```

#### 3. Ví dụ cách sử dụng (Example Usage) ⚡️
Sau khi Active workflow, các sếp có thể gọi API trực tiếp qua URL dạng:
`https://YOUR_INSTANCE.com/brsf?plid=1234567890&mode=auto&ar=true`

Trong đó:
- `plid`: Place ID của game Roblox cần tìm server.
- `mode`: Chế độ lọc (ping, latency, auto).
- `ar`: Tự động chuyển hướng (Auto Redirect).

#### 4. Kích hoạt ⚡️
- Thực hiện Test Run với một Place ID hợp lệ bất kỳ trên Roblox để kiểm tra kết quả trả về ở node `Respond with Success`.
- Bạt công tắc **Active** ở góc trên cùng bên phải để đưa workflow vào trạng thái hoạt động chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Extension trình duyệt:** Các sếp có thể viết một extension nhỏ trên Chrome gọi webhook này mỗi khi bấm nút "Play" trên trang chủ Roblox để tự động vào server xịn nhất.
- **Lưu lịch sử:** Thêm một node Google Sheets hoặc Database ở cuối luồng để lưu lại lịch sử các server tốt nhất cho từng tựa game.
- **Gửi thông báo Telegram:** Kết hợp thêm node Telegram để nhận thông báo trực tiếp về điện thoại khi tìm thấy server VIP cho bạn bè cùng chơi.

### 📌 Kết luận
Workflow tìm server Roblox này là một ví dụ tuyệt vời cho thấy sức mạnh của n8n trong việc tự động hóa các tác vụ giải trí hàng ngày. Hãy cài đặt ngay lên VPS của các sếp và tận hưởng những giây phút chơi game mượt mà không giật lag!