---
title: "🚀 Tự Động Cập Nhật n8n Lên Phiên Bản Mới Nhất (DevOps)"
description: "Workflow n8n tự động kiểm tra và cập nhật phiên bản n8n trên VPS của bạn theo lịch trình, giúp hệ thống luôn mới nhất và an toàn mà không cần thao tác thủ công."
slug: "tu-dong-cap-nhat-n8n-version"
tags: [n8n, devops, automation, self-hosted, system-admin]
keywords: [n8n workflow, tự động hóa, cập nhật n8n, devops, vps]
---

# 🚀 Tự Động Cập Nhật n8n Lên Phiên Bản Mới Nhất (DevOps)

Việc quản lý hệ thống n8n self-hosted trên VPS đôi khi trở thành một gánh nặng khi các bản cập nhật mới được phát hành liên tục. Nếu các sếp quên cập nhật, hệ thống có thể gặp lỗi bảo mật hoặc thiếu các tính năng mới. Ngược lại, việc cập nhật thủ công qua SSH mỗi khi có bản mới lại tốn thời gian và dễ gây gián đoạn dịch vụ nếu không cẩn thận.

Workflow **"Automatically update n8n version"** do Weilun phát triển chính là giải pháp "chốt hạ" cho bài toán này. Nó hoạt động như một kỹ sư DevOps tự động, định kỳ kiểm tra phiên bản hiện tại của n8n và so sánh với phiên bản mới nhất trên npm. Nếu có bản mới, nó sẽ tự động thực hiện lệnh cập nhật qua SSH, đảm bảo hệ thống của các sếp luôn trong trạng thái tối ưu nhất mà không cần can thiệp thủ công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và có quyền SSH để cập nhật chính nó, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian quản trị:** Không cần nhớ lịch kiểm tra bản cập nhật, hệ tự động lo liệu.
- **Luôn mới nhất & An toàn:** Đảm bảo n8n luôn chạy trên phiên bản có vá lỗi bảo mật mới nhất.
- **Giảm rủi ro con người:** Loại bỏ sai sót khi gõ lệnh SSH thủ công.
- **Hoạt động liên tục:** Workflow chạy theo lịch trình (Schedule Trigger), có thể đặt chạy hàng ngày hoặc hàng tuần.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **VPS Self-hosted n8n:** Workflow này yêu cầu quyền truy cập SSH vào máy chủ nơi n8n đang chạy.
2. **Tài khoản SSH:** Username và Password (hoặc Private Key) có quyền thực thi lệnh `npm` hoặc `docker` trên VPS.
3. **API Key n8n (Bearer Token):** Để gọi API nội bộ của n8n nhằm lấy phiên bản hiện tại (Node "Get Local n8n version").
4. **Truy cập Internet:** Để node "Get the latest n8n version" kiểm tra phiên bản mới nhất từ registry npm.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from File** hoặc **Import from URL**.
3. Dán link gốc: `https://n8n.io/workflows/4335` hoặc tải file JSON về và import.
4. Workflow sẽ hiện ra với 5 nodes chính.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Đây là phần quan trọng nhất. Các sếp cần cấu hình kỹ từng node sau:

*   **Node: `Schedule Trigger`**
    *   Mặc định có thể chạy hàng ngày. Các sếp có thể chỉnh tần suất (ví dụ: 1 lần/ngày vào lúc 02:00 sáng để tránh giờ cao điểm).

*   **Node: `Get Local n8n version` (HTTP Request)**
    *   **Method:** GET
    *   **URL:** `http://localhost:5678/api/v1/health` (hoặc endpoint phù hợp để lấy version, thường là `/api/v1/info` hoặc tương tự tùy phiên bản n8n). *Lưu ý: Kiểm tra tài liệu API n8n để đảm bảo URL chính xác.*
    *   **Authentication:** Chọn **Header Auth** hoặc **Bearer Auth**.
    *   **Credentials:** Tạo mới hoặc chọn credentials `httpBearerAuth` đã có. Điền **API Key** của n8n (tìm trong Settings > API) vào trường Bearer Token.

*   **Node: `Get the latest n8n version` (HTTP Request)**
    *   **Method:** GET
    *   **URL:** `https://registry.npmjs.org/n8n/latest`
    *   **Authentication:** Không cần (Public API).
    *   Node này sẽ trả về JSON chứa phiên bản mới nhất của n8n trên npm.

*   **Node: `If`**
    *   Logic so sánh: So sánh phiên bản từ node "Get Local" với phiên bản từ node "Get Latest".
    *   Điều kiện: Nếu `Local Version` khác `Latest Version` (hoặc `Local Version` < `Latest Version`), thì đi vào nhánh **True** (Thực hiện cập nhật). Nếu bằng nhau, đi vào nhánh **False** (Bỏ qua).

*   **Node: `SSH1` (SSH)**
    *   **Command:** Đây là lệnh thực thi cập nhật. Tùy thuộc vào cách cài đặt n8n (npm hay docker), lệnh sẽ khác nhau.
        *   *Nếu cài bằng npm:* `npm install -g n8n@latest && pm2 restart n8n` (hoặc lệnh restart tương ứng).
        *   *Nếu cài bằng Docker:* `docker pull n8nio/n8n:latest && docker compose up -d` (cần đảm bảo lệnh chạy đúng trong môi trường container).
    *   **Credentials:** Chọn hoặc tạo credentials `sshPassword`.
        *   **Host:** IP hoặc Domain của VPS.
        *   **Username:** User có quyền root hoặc sudo.
        *   **Password:** Mật khẩu SSH.
        *   *Lưu ý bảo mật:* Nên dùng SSH Key thay vì Password nếu có thể, nhưng workflow mẫu dùng Password cho đơn giản.

#### 3. Kích hoạt ⚡️
1. **Test Run:** Chạy thử workflow. Kiểm tra xem node "Get Local" và "Get Latest" có trả về đúng phiên bản không.
2. **Kiểm tra logic If:** Đảm bảo rằng nếu phiên bản khác nhau, nó sẽ kích hoạt node SSH.
3. **Bật Active:** Sau khi test thành công, bật công tắc **Active** để workflow chạy tự động theo lịch trình.

### ✍️ Mẹo & gợi ý nâng cao
- **Gửi thông báo qua Telegram/Slack:** Thêm node Telegram hoặc Slack sau node SSH để gửi tin nhắn "Cập nhật n8n thành công lên phiên bản X" hoặc "Lỗi cập nhật" về điện thoại.
- **Backup trước khi cập nhật:** Thêm node SSH trước bước cập nhật để chạy lệnh backup database (Postgres/SQLite) và thư mục data.
- **Rollback tự động:** Nếu cập nhật thất bại (n8n không khởi động lại được), có thể thêm logic để khôi phục backup (phức tạp hơn, cần thêm các node kiểm tra health check sau cập nhật).
- **Chạy vào giờ thấp điểm:** Đặt Schedule Trigger chạy vào lúc 02:00 - 04:00 sáng để tránh gián đoạn các workflow khác đang chạy.

### 📌 Kết luận
Việc tự động hóa việc cập nhật n8n là một bước đi chuyên nghiệp hóa hệ thống DevOps của các sếp. Với workflow này, các sếp có thể yên tâm ngủ ngon mà không lo hệ thống bị lỗi thời hay thiếu vá bảo mật. Hãy import, cấu hình credentials SSH và API Key, rồi để n8n tự lo phần còn lại!