---
title: "🚀 Tự động trích xuất Kinh Thánh động từ getBible API với n8n"
description: "Hướng dẫn xây dựng và sử dụng workflow n8n để gọi getBible API, xử lý JSON động và trả về dữ liệu Kinh Thánh chuẩn xác theo yêu cầu."
slug: "tu-dong-trich-xuat-kinh-thanh-get-bible-api"
tags: [n8n, automation, no-code, api-integration, json, productivity]
keywords: [n8n workflow, getBible API, tự động hóa kinh thánh, trích xuất dữ liệu api, n8n httpRequest]
---

# 🚀 Tự động trích xuất Kinh Thánh động từ getBible API với n8n

Các sếp đang xây dựng một ứng dụng, chatbot hoặc hệ thống nội dung có tích hợp trích xuất các câu Kinh Thánh (Scriptures) nhưng lại gặp khó khăn trong việc viết code gọi API, xử lý định dạng phức tạp và chuẩn hóa kết quả trả về? Việc xử lý thủ công từng phân đoạn, dịch bản (translation) hay quản lý nhiều định dạng tham chiếu khác nhau tốn rất nhiều thời gian và dễ phát sinh lỗi.

Giải pháp ở đây là gì? Workflow n8n **Fetch Scriptures Dynamically from getBible API** sẽ giúp các sếp tự động hóa 100% quy trình này. Chỉ cần truyền vào một đối tượng JSON chứa danh sách các câu cần tra cứu và bản dịch mong muốn, workflow sẽ lo phần còn lại và trả về kết quả chuẩn xác, sẵn sàng tích hợp vào bất kỳ dự án nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Nhận input danh sách tham chiếu (References) và tự động bóc tách để gọi API getBible.
- **Linh hoạt đa phiên bản/bản dịch:** Hỗ trợ linh hoạt các bản dịch Kinh Thánh khác nhau (ví dụ: KJV) và phiên bản API v2.
- **Chuẩn hóa dữ liệu đầu ra:** Trả về cấu trúc JSON sạch, đúng định dạng nguyên bản từ getBible API, giúp dễ dàng tích hợp vào các hệ thống khác qua Sub-workflow.
- **Tiết kiệm thời gian phát triển:** Không cần viết code xử lý logic phức tạp ở tầng ứng dụng, tận dụng mô hình Sub-workflow module hóa cực kỳ gọn gàng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống n8n (Cloud hoặc Self-hosted).
- Không cần API Key riêng vì **getBible API** hoàn toàn công khai và miễn phí.
- Đầu vào là một cấu trúc JSON chuẩn bao gồm danh sách references, translation và version.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ mã JSON của workflow **Fetch Scriptures Dynamically from getBible API** và dán trực tiếp vào giao diện n8n Editor (hoặc import file JSON gốc).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 4 nodes chính hoạt động nhịp nhàng:

- **Entry (`executeWorkflowTrigger`):** Đóng vai trò là điểm kích hoạt khi workflow này được gọi từ một workflow chính khác (Sub-workflow). Node này nhận dữ liệu JSON đầu vào. Cấu trúc JSON mẫu cần truyền vào:
  ```json
  {
    "references": [
        "1 John 3:16",
        "Jn 3:16",
        "James 3:16",
        "Rom 3:16"
    ],
    "translation": "kjv",
    "version": "v2"
  }
  ```
- **ModelJson (`code`):** Node JavaScript xử lý việc phân tích và chuẩn hóa dữ liệu đầu vào từ `Entry`, chuẩn bị các tham số cần thiết để gọi API.
- **API Query to GetBible (`httpRequest`):** Node thực hiện gọi trực tiếp đến API của getBible dựa trên dữ liệu đã xử lý. Các sếp cần đảm bảo URL endpoint cấu hình đúng định dạng API v2 của getBible (`https://api.getbible.net/...`).
- **Map API Respons to Result (`set`):** Node định hình lại cấu trúc dữ liệu phản hồi trả về cho người gọi, đảm bảo tính đồng nhất với định dạng API gốc:
  ```json
  {
    "result": {
      "kjv_62_3": {
        "translation": "King James Version",
        "abbreviation": "kjv",
        "lang": "en",
        "language": "English",
        "direction": "LTR",
        "encoding": "UTF-8",
        "book_nr": 62,
        "book_name": "1 John",
        "chapter": 3,
        "name": "1 John 3",
        "ref": [
          "1 John 3:16"
        ],
        "verses": [
          {
            "chapter": 3,
            "verse": 16,
            "name": "1 John 3:16",
            "text": "Hereby perceive we the love of God, because he laid down his life for us: and we ought to lay down our lives for the brethren."
          }
        ]
      }
    }
  }
  ```

#### 3. Kích hoạt ⚡️
- Thực hiện chạy thử (Test run) với dữ liệu JSON mẫu để kiểm tra xem API getBible có trả về đúng kết quả không.
- Bật công tắc **Active** để đưa workflow vào trạng thái sẵn sàng nhận request từ các workflow khác.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Telegram/Slack Bot:** Các sếp có thể tạo một workflow chat bot, nhận câu lệnh tra cứu Kinh Thánh từ người dùng, sau đó gọi workflow này làm Sub-workflow để trả nội dung câu Kinh Thánh về chat.
- **Lưu lịch sử tra cứu:** Thêm node Google Sheets hoặc Database (PostgreSQL/Supabase) phía sau để lưu lại những câu Kinh Thánh mà người dùng hay tra cứu nhằm phân tích nhu cầu.
- **Xử lý lỗi (Error Handling):** Thêm Error Trigger để bắt trường hợp người dùng nhập sai tên sách Kinh Thánh hoặc lỗi kết nối mạng từ getBible API.

### 📌 Kết luận
Workflow **Fetch Scriptures Dynamically from getBible API** là một công cụ cực kỳ hữu ích và tinh gọn giúp tự động hóa việc truy xuất dữ liệu Kinh Thánh. Bằng cách áp dụng mô hình Sub-workflow, các sếp có thể dễ dàng tái sử dụng logic này trong bất kỳ dự án tự động hóa nào liên quan đến Kinh Thánh mà không cần lặp lại code. Lên đồ và áp dụng ngay thôi các sếp ơi!