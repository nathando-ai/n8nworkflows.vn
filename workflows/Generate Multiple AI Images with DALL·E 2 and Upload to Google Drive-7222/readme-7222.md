---
title: "🚀 Tự Động Tạo Hàng Loạt Ảnh AI Bằng DALL·E 2 và Lưu Trực Tiếp Lên Google Drive"
description: "Hướng dẫn xây dựng workflow n8n tự động tạo nhiều biến thể hình ảnh từ một câu lệnh (prompt) sử dụng OpenAI DALL·E 2 và lưu trữ có tổ chức vào Google Drive."
slug: "tao-nhieu-anh-ai-dalle2-google-drive-n8n"
tags: [n8n, automation, ai, openai, dalle2, google-drive, content-creation]
keywords: [n8n workflow, tạo ảnh ai tự động, dalle2 n8n, google drive integration, openAI api n8n]
---

# 🚀 Tự Động Tạo Hàng Loạt Ảnh AI Bằng DALL·E 2 và Lưu Trực Tiếp Lên Google Drive

Các sếp có bao giờ cảm thấy mất quá nhiều thời gian khi cần tạo ra nhiều biến thể hình ảnh cho cùng một ý tưởng thiết kế? Việc phải nhập đi nhập lại một prompt trên OpenAI, tải ảnh về máy rồi lại thủ công upload lên Google Drive thực sự là một cơn ác mộng tốn thời gian.

Đừng lo, bài toán này sẽ được giải quyết triệt để với workflow n8n tự động hóa 100%. Chỉ với một cú click, hệ thống sẽ tự động nhân bản prompt, gọi API DALL·E 2 để vẽ ảnh và phân loại, lưu trữ gọn gàng trên Google Drive của các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Tự động hóa hoàn toàn quy trình tạo và lưu trữ ảnh hàng loạt mà không cần thao tác thủ công.
- **Tạo đa dạng biến thể:** Dễ dàng sinh ra nhiều hình ảnh khác nhau từ một mô tả duy nhất trong một lần chạy.
- **Quản lý khoa học:** Ảnh được đổi tên tự động theo cấu trúc chuẩn và lưu đúng thư mục trên Google Drive.
- **Hoạt động liền mạch:** Kết nối trực tiếp giữa OpenAI và Google Cloud thông qua nền tảng n8n mạnh mẽ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **OpenAI Account:** Có API Key và số dư để sử dụng dịch vụ DALL·E 2.
- **Google Cloud Console:** Đã tạo project và cấu hình OAuth 2.0 Credentials cho Google Drive API.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ n8n template (ID: 7222) hoặc copy toàn bộ mã JSON dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 6 nodes chính, các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Set Image Prompt (`Set` Node):** 
  - Khai báo biến `Prompt` (nội dung mô tả bức ảnh) và `Name` (tên gốc của file khi lưu).
  - *Ví dụ:* Prompt = `"Make an image of an attractive woman standing in New York City"`, Name = `"woman-nyc"`.

- **Duplicate Rows (`Code` Node):** 
  - Node này dùng đoạn mã JavaScript để nhân bản prompt thành 3 lần chạy (variations) khác nhau:
    ```javascript
    const original = items[0].json;

    return [
      { json: { ...original, run: 1 } },
      { json: { ...original, run: 2 } },
      { json: { ...original, run: 3 } },
    ];
    ```
  - Các sếp có thể sửa số lượng bản sao tùy theo nhu cầu.

- **Loop Over Items (`Split In Batches` Node):** 
  - Đặt Batch Size là `1` để hệ thống xử lý từng biến thể một cách tuần tự, tránh bị lỗi rate limit từ OpenAI.

- **Generate an image (`OpenAI` Node):** 
  - Chọn model: `dall-e-2`.
  - Tham số Prompt: `={{ $json.Prompt }}`.
  - Kết nối thông tin `OpenAI API Credentials` của các sếp.

- **Upload to Google Drive (`Google Drive` Node):** 
  - Cấu hình tên file lưu trữ: `={{ $('Set Image Prompt').item.json.Name }} - {{ $('Duplicate Rows').item.json.run }}`
  - Chọn `Folder ID` là thư mục đích trên Google Drive của các sếp.
  - Kết nối `Google Drive OAuth2 API Credentials`.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm thủ công với dữ liệu mẫu.
- Kiểm tra kết quả trên Google Drive xem ảnh đã được tạo và lưu đúng tên chưa.
- Bật công tắc **Active** để đưa workflow vào trạng thái sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Google Sheets:** Thay vì gán cứng prompt trong node Set, các sếp có thể lấy danh sách prompt từ một file Google Sheets để tạo ảnh hàng loạt theo chiến dịch marketing.
- **Gửi thông báo:** Thêm node Telegram hoặc Slack vào cuối workflow để nhận thông báo ngay khi bộ ảnh được tạo và lưu thành công lên Drive.
- **Tự động hóa theo lịch:** Thay thế node Manual Trigger bằng Schedule Trigger để tự động sinh ảnh mới mỗi ngày/tuần theo ý muốn.

### 📌 Kết luận
Với workflow n8n này, việc sản xuất hình ảnh bằng AI cho các chiến dịch truyền thông nay đã trở nên tự động và chuyên nghiệp hơn bao giờ hết. Hãy áp dụng ngay vào hệ thống của các sếp để tối ưu hóa hiệu suất làm việc!