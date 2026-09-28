---
title: "🚀 Kiểm thử Webhook trong n8n mà không cần thay đổi WEBHOOK_URL (Ví dụ PostBin & BambooHR)"
description: "Hướng dẫn chi tiết cách kiểm thử webhook trong n8n mà không cần thay đổi cấu hình WEBHOOK_URL, sử dụng PostBin và BambooHR để mô phỏng và kiểm tra tính năng webhook một cách hiệu quả."
slug: "kiem-thu-webhook-trong-n8n-khong-can-thay-doi-webhook-url"
tags: [n8n, automation, no-code, BambooHR, PostBin]
keywords: [n8n workflow, tự động hóa, webhook, BambooHR, PostBin]
---

# 🚀 Kiểm thử Webhook trong n8n mà không cần thay đổi WEBHOOK_URL (Ví dụ PostBin & BambooHR)

[Các sếp đang gặp khó khăn khi kiểm thử webhook trong n8n vì phải thay đổi cấu hình WEBHOOK_URL. Workflow này giúp các sếp kiểm thử webhook một cách nhanh chóng và hiệu quả mà không cần thay đổi cấu hình n8n.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Kiểm thử webhook nhanh chóng mà không cần thay đổi cấu hình n8n.
- Tiết kiệm thời gian và công sức trong quá trình phát triển và kiểm thử.
- Hiểu rõ cách webhook hoạt động và tương tác với các dịch vụ khác.
- Tự động hóa quá trình kiểm thử webhook một cách hiệu quả.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản BambooHR ([đăng ký thử nghiệm miễn phí](https://www.bamboohr.com/signup/))
- API key của BambooHR ([tài liệu hướng dẫn](https://documentation.bamboohr.com/docs/getting-started#authentication))
- Kết nối Slack ([tài liệu hướng dẫn](https://docs.n8n.io/integrations/builtin/credentials/slack/))
- Tài khoản PostBin (không cần xác thực)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow](https://n8n.io/workflows/2869).
2. Nhấn nút "Download" để tải file JSON về máy.
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON đã tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "When clicking ‘Test workflow’"**:
   - Không cần cấu hình gì, chỉ cần nhấn nút "Test workflow" để bắt đầu kiểm thử.

2. **Node "Create Bin"**:
   - Không cần cấu hình gì, node này sẽ tự động tạo một Bin mới trong PostBin.

3. **Node "GET Bin"**:
   - Không cần cấu hình gì, node này sẽ lấy thông tin Bin vừa tạo.

4. **Node "Format url for webhook"**:
   - Không cần cấu hình gì, node này sẽ định dạng URL cho webhook.

5. **Node "GET most recent request"**:
   - Không cần cấu hình gì, node này sẽ lấy yêu cầu gần nhất từ Bin.

6. **Node "MOCK request"**:
   - Không cần cấu hình gì, node này sẽ gửi một yêu cầu giả lập đến Bin.

7. **Node "Create Bin1"**:
   - Không cần cấu hình gì, node này sẽ tạo một Bin mới trong PostBin.

8. **Node "GET Bin1"**:
   - Không cần cấu hình gì, node này sẽ lấy thông tin Bin vừa tạo.

9. **Node "Format url for webhook1"**:
   - Không cần cấu hình gì, node này sẽ định dạng URL cho webhook.

10. **Node "SET BambooHR subdomain"**:
    - Cần cấu hình subdomain của BambooHR.

11. **Node "Split out fields"**:
    - Không cần cấu hình gì, node này sẽ tách các trường dữ liệu.

12. **Node "Combine fields to monitor"**:
    - Không cần cấu hình gì, node này sẽ kết hợp các trường dữ liệu để theo dõi.

13. **Node "Format payload for BambooHR webhook"**:
    - Không cần cấu hình gì, node này sẽ định dạng dữ liệu cho webhook BambooHR.

14. **Node "Create webhook in BambooHR"**:
    - Cần cấu hình credentials của BambooHR (API key).

15. **Node "Create dummy data for employees"**:
    - Không cần cấu hình gì, node này sẽ tạo dữ liệu giả lập cho nhân viên.

16. **Node "Keep only new employee fields"**:
    - Không cần cấu hình gì, node này sẽ giữ lại các trường dữ liệu mới của nhân viên.

17. **Node "GET all possible fields to monitor in BambooHR"**:
    - Cần cấu hình credentials của BambooHR (API key).

18. **Node "Register and test webhook"**:
    - Không cần cấu hình gì, node này sẽ đăng ký và kiểm thử webhook.

19. **Node "Check BambooHR for calls to webhook"**:
    - Cần cấu hình credentials của BambooHR (API key).

20. **Node "Create employee records with dummy data"**:
    - Cần cấu hình credentials của BambooHR (API key).

21. **Node "Split out employees"**:
    - Không cần cấu hình gì, node này sẽ tách các thông tin nhân viên.

22. **Node "Format displayName"**:
    - Không cần cấu hình gì, node này sẽ định dạng tên hiển thị của nhân viên.

23. **Node "OpenAI Chat Model"**:
    - Cần cấu hình credentials của OpenAI (API key).

24. **Node "Auto-fixing Output Parser"**:
    - Không cần cấu hình gì, node này sẽ tự động sửa lỗi đầu ra.

25. **Node "OpenAI Chat Model1"**:
    - Cần cấu hình credentials của OpenAI (API key).

26. **Node "Structured Output Parser"**:
    - Không cần cấu hình gì, node này sẽ phân tích đầu ra có cấu trúc.

27. **Node "Basic LLM Chain"**:
    - Không cần cấu hình gì, node này sẽ thực hiện chuỗi LLM cơ bản.

28. **Node "Combine employees into list"**:
    - Không cần cấu hình gì, node này sẽ kết hợp các thông tin nhân viên thành danh sách.

29. **Node "Pluralize key"**:
    - Không cần cấu hình gì, node này sẽ đổi số nhiều cho khóa.

30. **Node "Welcome employees on Slack"**:
    - Cần cấu hình credentials của Slack.

31. **Node "DELETE BambooHR webhook"**:
    - Cần cấu hình credentials của BambooHR (API key).

32. **Node "GET most recent request1"**:
    - Không cần cấu hình gì, node này sẽ lấy yêu cầu gần nhất từ Bin.

33. **Node "Wait 60 + 1 seconds for webhook to fire"**:
    - Không cần cấu hình gì, node này sẽ chờ 61 giây để webhook kích hoạt.

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong các node cần thiết, nhấn nút "Test workflow" để kiểm thử.
2. Kiểm tra kết quả trên các node tương ứng để đảm bảo webhook hoạt động đúng.
3. Bật Active workflow để chạy workflow liên tục.

### ✍️ Mẹo & gợi ý nâng cao
- Sử dụng PostBin để kiểm thử webhook nhanh chóng mà không cần thay đổi cấu hình n8n.
- Kết hợp với Slack để nhận thông báo khi có sự kiện mới.
- Lưu log các sự kiện để theo dõi và phân tích sau này.
- Tự động hóa quá trình gửi báo cáo định kỳ về các sự kiện quan trọng.

### 📌 Kết luận
Workflow này giúp các sếp kiểm thử webhook trong n8n một cách nhanh chóng và hiệu quả mà không cần thay đổi cấu hình WEBHOOK_URL. Các sếp có thể áp dụng workflow này để kiểm thử và phát triển các tính năng webhook một cách dễ dàng và hiệu quả.