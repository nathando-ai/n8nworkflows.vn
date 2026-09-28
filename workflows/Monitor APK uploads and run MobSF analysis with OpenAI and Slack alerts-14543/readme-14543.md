---
title: "🚀 Tự động quét bảo mật APK và phân tích mã nguồn với MobSF, OpenAI và Slack"
description: "Hướng dẫn xây dựng workflow n8n tự động theo dõi file APK trên Google Drive, chạy phân tích tĩnh MobSF, đánh giá rủi ro bằng AI và gửi báo cáo qua Slack."
slug: "tu-dong-quet-bao-mat-apk-mobsf-openai-slack"
tags: [n8n, automation, devops, security, mobsf, openai, slack]
keywords: [n8n workflow, tự động hóa bảo mật APK, MobSF n8n, OpenAI code review, thông báo Slack tự động]
---

# 🚀 Tự động hóa kiểm tra bảo mật APK: MobSF, AI & Slack

Các sếp làm trong lĩnh vực phát triển ứng dụng di động chắc hẳn đều hiểu cảm giác "đau đầu" khi phải kiểm tra bảo mật, rà soát mã nguồn và các thư viện thừa (unused packages) trên tệp APK trước khi phát hành. Quy trình thủ công này vừa tốn thời gian, dễ bỏ sót lỗ hổng lại vừa làm gián đoạn tiến độ của anh em dev.

Giải pháp là đây! Workflow n8n siêu việt này sẽ tự động hóa **100%** quy trình từ lúc file APK được tải lên Google Drive, đẩy qua công cụ quét bảo mật **MobSF**, sử dụng **OpenAI** để tóm tắt và đánh giá rủi ro, cuối cùng gửi báo cáo trực quan đến kênh **Slack** của team. Không cần code phức tạp, chỉ cần "lên đồ" là chạy!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Ngay khi có file APK mới trên Google Drive, hệ thống tự bắt sự kiện và xử lý mà không cần con người can thiệp.
- **Phân tích bảo mật chuyên sâu:** Kết hợp MobSF để quét tĩnh ứng dụng, tìm ra các gói thư viện thừa, thư viện rủi ro cao.
- **AI tóm tắt thông minh:** Sử dụng OpenAI để chuyển hóa các báo cáo kỹ thuật phức tạp thành ngôn ngữ thân thiện, dễ hiểu cho lập trình viên.
- **Cảnh báo tức thì:** Đẩy toàn bộ kết quả phân tích và đánh giá rủi ro trực tiếp vào Slack channel để team cùng nắm bắt.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Google Drive Account:** Nơi lưu trữ file APK đầu vào.
- **MobSF Server:** Một instance MobSF đang hoạt động (có API Key và Server URL).
- **OpenAI API Key:** Dùng cho node AI tóm tắt kết quả.
- **Slack Account:** Tài khoản kết nối với Workspace để nhận thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần tải file JSON của workflow này hoặc copy toàn bộ nội dung JSON, sau đó paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình chính xác các node sau:

- **Start Analysis Trigger (`googleDriveTrigger`):** Thêm Google Drive Credentials, sau đó chọn thư mục (Folder) cụ thể trên Drive mà các sếp muốn theo dõi. Mỗi khi có file APK mới được upload vào đây, workflow sẽ tự động kích hoạt.
- **Download Apk (`googleDrive`):** Sử dụng chung thông tin credentials với node Trigger để tải file APK về xử lý.
- **MobSF – Upload APK & MobSF – Start Static Analysis (`httpRequest`):** Điền chính xác URL của MobSF Server và API Key của các sếp vào phần Header/Authentication của HTTP Request để giao tiếp với MobSF API.
- **Extract, Compare & Classify Package / Identify Unused Packages / Classify Unused Package Risk Levels (`code`):** Các đoạn mã JavaScript đã được viết sẵn để trích xuất các gói đã dùng/chưa dùng và phân loại mức độ rủi ro (safe, maybe-required, high-risk). Các sếp giữ nguyên hoặc tùy chỉnh logic nếu muốn.
- **Generate Developer Summary (`openAi`):** Kết nối tài khoản OpenAI của các sếp (OpenAI API Key), chọn Model phù hợp (ví dụ: `gpt-4o-mini` hoặc `gpt-4o`) để hệ thống tạo báo cáo tóm tắt cho dev.
- **Notify Team on Slack (`slack`):** Kết nối tài khoản Slack, chọn Channel hoặc User cụ thể để nhận thông điệp cảnh báo kết quả quét.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và upload thử một file APK lên thư mục Google Drive đã chọn để test luồng chạy.
- Sau khi kiểm tra dữ liệu trả về trên Slack thành công, gạt công tắc sang **Active** để bật chế độ chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ lịch sử quét:** Thêm một node Google Sheets hoặc Supabase vào cuối luồng để lưu lại lịch sử quét của từng phiên bản APK, phục vụ việc kiểm tra sau này.
- **Cảnh báo mức độ nghiêm trọng:** Tùy chỉnh đoạn code phân loại rủi ro để nếu phát hiện lỗi bảo mật Critical, workflow sẽ bắn tin nhắn riêng qua Telegram hoặc gọi webhook khẩn cấp.
- **Tích hợp Jira/GitHub Issues:** Tự động tạo một Issue trên Jira hoặc GitHub dựa trên kết quả phân tích của AI nếu phát hiện các gói thư viện rủi ro cao.

### 📌 Kết luận
Việc tự động hóa kiểm tra bảo mật ứng dụng di động chưa bao giờ dễ dàng đến thế với sự kết hợp hoàn hảo giữa Google Drive, MobSF, OpenAI và Slack trên n8n. Hãy áp dụng ngay vào quy trình DevOps của công ty để tiết kiệm hàng giờ kiểm tra thủ công mỗi tuần!