---
title: "🚀 Tự động hóa gửi báo cáo Pull Request bị bỏ quên (Stale PR) hàng ngày qua GitHub và Slack"
description: "Hướng dẫn cấu hình workflow n8n tự động quét GitHub PRs, tính toán thời gian chờ review và gửi tóm tắt qua Slack mỗi sáng."
slug: "tu-dong-hoa-gui-bao-cao-stale-pr-github-slack"
tags: [n8n, automation, devops, github, slack, productivity]
keywords: [n8n workflow, github pr digest, slack automation, devops workflow, quan ly pull request]
---

# 🚀 Tự động hóa gửi báo cáo Pull Request bị bỏ quên (Stale PR) hàng ngày qua GitHub và Slack

Các sếp làm kỹ thuật (Tech Lead, Engineering Manager) chắc chắn đã từng đau đầu với tình trạng các Pull Request (PR) bị "treo" lâu ngày mà không ai review, làm chậm tiến độ phát triển sản phẩm. Nhắc nhở thủ công thì mất thời gian và dễ quên. 

Giải pháp ở đây là để n8n tự động "gọi hồn" những chiếc PR bị bỏ quên này! Workflow này sẽ tự động quét qua các kho lưu trữ (repositories) GitHub, tính toán thời gian chờ review (review lag), xếp hạng mức độ nghiêm trọng và gửi bảng tóm tắt trực quan thẳng vào kênh Slack của đội ngũ vào 9 giờ sáng các ngày trong tuần.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Không cần ai phải ngồi check hay tổng hợp thủ công mỗi tuần.
- **Tăng tốc độ code review:** Giúp đội ngũ không bỏ sót PR nào, giải quyết nhanh các điểm nghẽn (bottleneck).
- **Cá nhân hóa cấu hình:** Dễ dàng tùy chỉnh ngưỡng ngày quá hạn (`stale_days`), chọn các repo cần theo dõi và lọc các PR dạng Draft.
- **Thông báo đúng nơi, đúng thời điểm:** Báo cáo chỉ được gửi đi nếu phát hiện có PR bị "đắp chiếu", tránh làm phiền đội ngũ khi không cần thiết.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **GitHub Personal Access Token (PAT):** Cần cấp quyền truy cập repository (`repo` scope) để gọi GitHub API.
- **Slack Bot Token / Webhook:** Để gửi tin nhắn thông báo vào kênh tương ứng.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow hoặc sao chép mã nguồn JSON, sau đó dán trực tiếp vào n8n Editor của các sếp. Workflow sử dụng tổng cộng 10 nodes phối hợp nhịp nhàng từ lập lịch, gọi API, xử lý dữ liệu code đến gửi thông báo.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các nodes sau trước khi kích hoạt:

- **Node `When Weekday at 9am` (scheduleTrigger):** Kiểm tra và điều chỉnh múi giờ (Timezone) cho phù hợp với giờ làm việc của team (ví dụ: `Asia/Ho_Chi_Minh`).
- **Node `Set PR Monitor Config` (set):** 
  - Khai báo mảng repository cần theo dõi (ví dụ: `['owner/repo1', 'owner/repo2']`).
  - Thiết lập ngưỡng số ngày quá hạn (`stale_days`).
  - Cấu hình tên kênh Slack (`slack_channel`) và tùy chọn lọc Draft (`exclude_drafts`).
- **Node `Fetch GitHub Open PRs` & `Fetch PR Review Data` (httpRequest):** Kết nối với tài khoản GitHub thông qua **GitHub API Credentials** (sử dụng Personal Access Token).
- **Node `Send Digest to Slack` (slack):** Chọn thông tin xác thực Slack (Slack Bot Token hoặc Webhook) và trỏ tới kênh nhận thông báo đã cấu hình ở bước trên.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm thủ công với dữ liệu mẫu và kiểm tra kết quả trả về trên Slack.
- Nếu mọi thứ mượt mà, hãy gạt công tắc sang **Active** để hệ thống tự động chạy theo lịch hẹn.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng thông báo:** Kết hợp thêm node Telegram hoặc Microsoft Teams nếu team của sếp không dùng Slack.
- **Lưu log báo cáo:** Thêm node Google Sheets ở cuối luồng để ghi lại lịch sử các PR bị trễ theo thời gian, giúp đánh giá hiệu suất review của team.
- **Tùy chỉnh độ ưu tiên:** Sửa đổi logic trong các Code Node (`Expand Repos to Items`, `Build Slack Digest`, v.v.) để sắp xếp PR theo nhãn (labels) hoặc số lượng bình luận.

### 📌 Kết luận
Một workflow gọn gàng nhưng giải quyết cực kỳ hiệu quả bài toán quản lý quy trình review code trong các đội ngũ phát triển phần mềm. Hãy triển khai ngay hôm nay để tối ưu hóa tốc độ "ship code" cho team của các sếp nhé!