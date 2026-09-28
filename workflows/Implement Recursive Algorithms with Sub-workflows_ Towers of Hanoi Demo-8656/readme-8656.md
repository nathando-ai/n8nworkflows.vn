---
title: "🚀 Giải Thuật Đệ Quy Trong n8n: Mô Phỏng Bài Toán Tháp Hà Nội (Towers of Hanoi)"
description: "Khám phá cách triển khai giải thuật đệ quy phức tạp bằng n8n sub-workflows qua mô phỏng bài toán Tháp Hà Nội (Towers of Hanoi Demo)."
slug: "giai-thuat-de-quy-n8n-thap-ha-noi"
tags: [n8n, automation, no-code, algorithms, recursion, sub-workflows]
keywords: [n8n workflow, tháp hà nội, towers of hanoi, đệ quy trong n8n, sub-workflow n8n]
---

# 🚀 Giải Thuật Đệ Quy Trong n8n: Mô Phỏng Bài Toán Tháp Hà Nội (Towers of Hanoi)

Các sếp có bao giờ nghĩ rằng n8n không chỉ dùng để kết nối API hay chuyển đổi dữ liệu, mà còn có thể giải quyết các bài toán khoa học máy tính kinh điển? Bài viết này sẽ giới thiệu một workflow cực kỳ độc đáo do tác giả Adrian xây dựng: **Implement Recursive Algorithms with Sub-workflows: Towers of Hanoi Demo**. 

Workflow này là một minh chứng xuất sắc (Proof of Concept) cho thấy chúng ta có thể hiện thực hóa các giải thuật đệ quy phức tạp ngay trong hệ thống n8n thông qua tính năng **Sub-workflows**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các vòng lặp đệ quy mượt mà, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Hiểu sâu về Sub-workflows:** Nắm vững cách gọi lồng nhau các sub-workflow để giải quyết bài toán đệ quy.
- **Trực quan hóa giải thuật:** Tự động chuyển các tầng đĩa từ cột A sang cột C qua cột trung gian B theo đúng luật chơi của Tháp Hà Nội.
- **Mở rộng tư duy No-Code:** Thấy được tiềm năng vượt giới hạn của n8n, không chỉ tự động hóa kinh doanh mà còn xử lý logic lập trình nâng cao.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n (Cloud hoặc Self-hosted).
- Workflow chính và các sub-workflow xử lý logic đệ quy (A B C, X Z Y, Y X Z).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ [n8n.io workflows (ID: 8656)](https://n8n.io/workflows/8656) hoặc copy mã nguồn JSON tương ứng để dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node `Set number of discs`**: Nơi các sếp cấu hình số lượng đĩa ban đầu (`numberOfDiscs`), mặc định đang để là `4`. Các sếp có thể thay đổi số lượng đĩa để thử nghiệm độ phức tạp của đệ quy (lưu ý số lượng lớn sẽ tăng số lượng sub-workflow được gọi).
- **Các Node `Execute Workflow` (`A B C`, `X Z Y`, `Y X Z`)**: Đây là các node gọi lại chính nó (đệ quy) với các tham số vị trí cột (X, Y, Z) và số lượng đĩa giảm đi 1 (`numberOfDiscs - 1`). Hãy đảm bảo đường dẫn trỏ chính xác đến các sub-workflow con đã import.
- **Các Node `Code` (`X to Z`, `Update`, `Create stacks`, `Solution`...)**: Xử lý logic thao tác mảng (pop, push) các đĩa trên các cột A, B, C và cập nhật trạng thái biến sau mỗi bước di chuyển.

#### 3. Kích hoạt ⚡️
- Nhấn **`Start`** (Manual Trigger) để chạy thử nghiệm.
- Kiểm tra kết quả hiển thị ở các node Code để xem từng bước di chuyển đĩa (Solution) từ cột A sang cột C.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Telegram/Slack**: Thay vì chỉ log ra màn hình, các sếp có thể tích hợp thêm node gửi tin nhắn qua Telegram để trực quan hóa từng bước di chuyển của đĩa theo thời gian thực.
- **Lưu lịch sử chạy**: Lưu các bước giải (Solution) vào Google Sheets hoặc cơ sở dữ liệu để phân tích số lượng bước đi tối ưu tương ứng với số đĩa.

### 📌 Kết luận
Bài toán Tháp Hà Nội qua sub-workflow trong n8n là một tài liệu học tập tuyệt vời cho những ai muốn khai phá sức mạnh của tự động hóa kết hợp tư duy lập trình cấu trúc. Hãy thử nghiệm ngay trên hệ thống n8n của các sếp!