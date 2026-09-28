---
title: "🚀 Tự Động So Sánh Phiên Bản n8n Của Bạn Với Bản Mới Nhất"
description: "Workflow n8n giúp kiểm tra nhanh phiên bản hiện tại và so sánh với bản release mới nhất, đảm bảo hệ thống luôn cập nhật và an toàn."
slug: "so-sanh-phien-ban-n8n"
tags: [n8n, automation, devops, version-control, self-hosted]
keywords: [n8n workflow, kiểm tra phiên bản n8n, cập nhật n8n, tự động hóa devops, n8n api]
---

# 🚀 Tự Động So Sánh Phiên Bản n8n Của Bạn Với Bản Mới Nhất

Việc quản lý hạ tầng tự động hóa bằng n8n là một lợi thế lớn, nhưng nó cũng đi kèm với trách nhiệm bảo trì. Một trong những nỗi đau lớn nhất của các "sếp" vận hành n8n là việc quên kiểm tra xem phiên bản hiện tại có đang bị lỗi thời (outdated) hay không. Việc chạy phiên bản cũ không chỉ khiến bạn bỏ lỡ các tính năng mới mà còn tiềm ẩn rủi ro bảo mật nghiêm trọng khi các bản vá lỗi quan trọng chưa được áp dụng.

Thay vì phải mở trình duyệt, vào trang tài liệu, rồi so sánh thủ công mỗi tuần, workflow này sẽ tự động hóa toàn bộ quy trình. Nó sẽ truy vấn API của n8n để lấy phiên bản hiện tại của instance của bạn, đồng thời kiểm tra phiên bản mới nhất từ nguồn chính thức, sau đó đưa ra kết luận rõ ràng: Bạn đang chạy bản mới nhất hay cần cập nhật ngay?

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và đảm bảo an toàn dữ liệu, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Đảm bảo An toàn (Security):** Phát hiện sớm các phiên bản có lỗ hổng bảo mật đã được vá trong các bản release mới.
- **Tiết kiệm Thời gian:** Loại bỏ thao tác kiểm tra thủ công, chỉ cần chạy workflow là có kết quả ngay lập tức.
- **Cảnh báo Chính xác:** So sánh trực tiếp phiên bản đang chạy với bản mới nhất, tránh nhầm lẫn giữa các bản beta hoặc stable.
- **Dễ dàng Tích hợp:** Có thể mở rộng để gửi thông báo qua Email/Slack khi phát hiện phiên bản cũ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n:** Instance n8n đang chạy (Self-hosted hoặc Cloud).
2. **n8n API Key:** Cần tạo API Key trong phần Admin Panel của n8n.
3. **Quyền truy cập:** Tài khoản cần có quyền truy cập vào API để đọc thông tin phiên bản.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể import workflow này vào n8n của mình bằng cách:
1. Tải xuống file JSON của workflow từ link gốc hoặc copy toàn bộ code JSON.
2. Mở n8n Editor.
3. Chọn **Import from File** (nếu có file) hoặc **Import from URL** (nếu có link trực tiếp).
4. Nếu copy/paste, hãy tạo một workflow mới, xóa các node mặc định, và dán JSON vào editor code (hoặc dùng tính năng import JSON nếu n8n hỗ trợ trực tiếp trong phiên bản mới).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này sử dụng 6 nodes chính. Dưới đây là các bước cấu hình quan trọng:

1. **Node: `Set up your n8n credentials` (Type: n8n)**
   - Đây là node dùng để xác thực API.
   - **Credentials:** Chọn credential `n8nApi` mà bạn đã tạo.
   - **Lưu ý:** Nếu chưa có, hãy vào **Credentials** -> **New Credential** -> Chọn **n8n API** -> Dán **API Key** của bạn vào.

2. **Node: `Get your n8n version` (Type: HTTP Request)**
   - Node này gọi API nội bộ của n8n để lấy phiên bản hiện tại.
   - **Credentials:** Đảm bảo đã gắn credential `n8nApi` vào node này.
   - **URL:** Mặc định sẽ trỏ tới endpoint `/api/v1/version` hoặc tương tự tùy phiên bản n8n. Hãy kiểm tra xem URL có đúng với instance của bạn không (thường là `http://localhost:5678/api/v1/version` hoặc domain của bạn).

3. **Node: `Get Most Recent n8n version` (Type: HTTP Request)**
   - Node này truy vấn nguồn bên ngoài (thường là GitHub API hoặc docs.n8n.io) để lấy phiên bản mới nhất.
   - **Kiểm tra URL:** Đảm bảo URL trỏ tới nguồn chính thức của n8n (ví dụ: `https://api.github.com/repos/n8n-io/n8n/releases/latest`).

4. **Node: `Extract Version` (Type: HTML)**
   - Node này dùng để trích xuất chuỗi phiên bản từ response JSON/HTML.
   - **Selector:** Kiểm tra xem selector CSS/JSON path có đúng với cấu trúc response của API không. Nếu API thay đổi cấu trúc, các sếp cần cập nhật selector ở đây.

5. **Node: `Clean Value` (Type: Code)**
   - Node JavaScript dùng để làm sạch chuỗi phiên bản (ví dụ: bỏ tiền tố `v`, loại bỏ khoảng trắng thừa).
   - **Code:** Kiểm tra logic trong node này. Nếu phiên bản mới nhất có định dạng khác, các sếp có thể cần chỉnh sửa code để parse đúng.

6. **Node: `Test your version` (Type: IF)**
   - Node này so sánh hai phiên bản.
   - **Logic:** Nó sẽ kiểm tra xem phiên bản hiện tại có bằng hoặc lớn hơn phiên bản mới nhất không.
   - **Output:** 
     - **True:** Phiên bản của bạn là mới nhất.
     - **False:** Phiên bản của bạn đã cũ, cần cập nhật.

#### 3. Kích hoạt ⚡️
1. **Test Run:** Nhấn nút **Execute Workflow** để chạy thử.
2. **Kiểm tra Output:** Xem kết quả ở node `Test your version`. Nếu nó trả về `False`, nghĩa là bạn cần cập nhật n8n.
3. **Bật Active:** Sau khi xác nhận workflow chạy đúng, bật công tắc **Active** ở góc trên bên phải để workflow có thể chạy định kỳ (nếu các sếp thêm node Schedule Trigger).

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm Schedule Trigger:** Thêm node **Schedule Trigger** (ví dụ: chạy mỗi tuần vào thứ Hai) để tự động kiểm tra phiên bản mà không cần thao tác thủ công.
- **Gửi Thông Báo:** Kết nối node `Test your version` (branch `False`) với node **Email** hoặc **Slack** để gửi cảnh báo ngay khi phát hiện phiên bản cũ.
- **Lưu Log:** Thêm node **Google Sheets** hoặc **Airtable** để ghi lại lịch sử kiểm tra phiên bản, giúp các sếp theo dõi quá trình cập nhật hệ thống.
- **Tự Động Cập Nhật (Nâng Cao):** Nếu các sếp có quyền SSH, có thể kết hợp với node **Execute Command** để tự động chạy lệnh `docker pull n8nio/n8n && docker compose up -d` (cẩn thận với rủi ro, chỉ áp dụng cho môi trường dev/test).

### 📌 Kết luận
Việc duy trì phiên bản n8n mới nhất không chỉ là thói quen tốt mà là yêu cầu bắt buộc để đảm bảo an toàn và hiệu suất hệ thống. Với workflow này, các sếp có thể loại bỏ hoàn toàn rủi ro quên cập nhật và tập trung vào việc xây dựng các quy trình tự động hóa giá trị hơn. Hãy import workflow, cấu hình API Key, và để n8n tự "chăm sóc" phiên bản của bạn!