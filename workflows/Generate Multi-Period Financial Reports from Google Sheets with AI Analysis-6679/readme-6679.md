---
title: "🚀 Tự động tạo báo cáo tài chính đa kỳ từ Google Sheets với AI DeepSeek"
description: "Hướng dẫn xây dựng workflow n8n tích hợp AI DeepSeek để tự động trích xuất, phân tích và báo cáo tài chính đa kỳ từ Google Sheets một cách chuyên nghiệp."
slug: "tao-bao-cao-tai-chinh-da-ky-google-sheets-ai-deepseek"
tags: [n8n, automation, ai-agent, google-sheets, deepseek, tai-chinh]
keywords: [n8n workflow, báo cáo tài chính tự động, google sheets ai, deepseek n8n, ai agent tài chính]
---

# 🚀 Tự động tạo báo cáo tài chính đa kỳ từ Google Sheets với AI DeepSeek

Các sếp có bao giờ cảm thấy mệt mỏi khi phải tốn hàng giờ đồng hồ mỗi cuối tháng để tổng hợp số liệu doanh thu, chi phí từ Google Sheets, sau đó lại tiếp tục chật vật phân tích chênh lệch giữa các kỳ (tháng này với tháng trước, hoặc so với cùng kỳ năm ngoái)? Việc làm thủ công này không chỉ tốn thời gian mà còn dễ dẫn đến sai sót, khiến ban lãnh đạo chậm trễ trong việc ra quyết định.

Đừng lo nữa các sếp ơi! Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ mạnh mẽ do tác giả **DuyTran** thiết kế. Workflow này kết hợp sức mạnh của **Google Sheets**, các thuật toán xử lý dữ liệu thông minh (**Code, Aggregate, Merge, Set**) và **AI Agent (sử dụng mô hình DeepSeek)** để tự động hóa hoàn toàn quy trình trích xuất, tổng hợp và phân tích báo cáo tài chính đa kỳ chỉ qua khung chat tương tác.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Trích xuất dữ liệu từ Google Sheets, xử lý và so sánh giữa các chu kỳ (hiện tại, kỳ trước, cùng kỳ năm ngoái) mà không cần can thiệp thủ công.
- **Trợ lý AI thông minh:** Tích hợp DeepSeek Chat Model giúp các sếp trò chuyện trực tiếp, đặt câu hỏi và nhận phân tích tài chính sâu sắc ngay lập tức qua giao diện chat.
- **Độ chính xác tuyệt đối:** Sử dụng các node Code và Aggregate để pivot, sum và chuẩn hóa dữ liệu tài chính sạch sẽ trước khi đưa vào AI phân tích.
- **Hoạt động linh hoạt:** Vừa hỗ trợ kích hoạt trực tiếp qua khung chat (`When chat message received`), vừa có thể chạy ngầm dưới dạng sub-workflow thông qua `When Executed by Another Workflow`.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Hệ thống n8n:** Đã cài đặt n8n (phiên bản hỗ trợ LangChain và các AI Agent nodes).
- **Google Sheets:** File Google Sheets chứa dữ liệu doanh thu, chi phí tài chính đã được cấu trúc rõ ràng.
- **API Credentials:**
  - Tài khoản kết nối Google Sheets (`Google Sheets OAuth2 API`).
  - API Key từ DeepSeek (`DeepSeek API`) để vận hành mô hình ngôn ngữ lớn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sao chép đoạn mã JSON của workflow từ [n8n.io/workflows/6679](https://n8n.io/workflows/6679), sau đó dán (Paste) trực tiếp vào giao diện n8n Editor của mình hoặc import dưới dạng file JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru với dữ liệu thực tế của công ty, các sếp cần chú ý cấu hình các node cốt lõi sau:
- **Get revenual from google sheet:** 
  - Chọn tài khoản kết nối `Google Sheets OAuth2 API`.
  - Cung cấp chính xác **Document ID** và **Sheet Name** chứa dữ liệu doanh thu/tài chính của các sếp.
- **DeepSeek Chat Model:** 
  - Thêm `DeepSeek API Key` vào phần credentials của node này để mô hình AI có thể phản hồi các câu hỏi tài chính.
- **Các node Code & Set (`Format Date`, `Pivot current circle`, `Pivot last circle`, `Pivot last year cirle`, v.v.):** 
  - Kiểm tra lại các trường (columns) dữ liệu trong code JavaScript của các node `Code` sao cho khớp với tên cột thực tế trong Google Sheets của các sếp (ví dụ: cột ngày tháng, cột giá trị, danh mục...).
- **Call n8n Workflow Tool & AI Agent:** 
  - Đảm bảo công cụ gọi sub-workflow được liên kết chính xác để AI Agent có thể gọi dữ liệu tài chính theo yêu cầu từ khung chat (`When chat message received`).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi một câu lệnh test qua khung chat để kiểm tra xem dữ liệu từ Google Sheets có được kéo về, tính toán và phân tích chính xác hay không.
- Sau khi test thành công, hãy bật công tắc **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa quy trình tài chính doanh nghiệp, các sếp có thể mở rộng workflow này bằng cách:
- **Tích hợp kênh thông báo:** Kết nối thêm node Slack hoặc Telegram để AI tự động gửi bản tóm tắt báo cáo tài chính hàng tuần/hàng tháng vào nhóm chat của ban giám đốc.
- **Lưu trữ lịch sử:** Lưu các câu hỏi và câu trả lời phân tích tài chính của AI vào một bảng Google Sheets riêng hoặc cơ sở dữ liệu để làm nhật ký theo dõi.
- **Mở rộng nguồn dữ liệu:** Không chỉ Google Sheets, các sếp có thể kết nối thêm các nguồn dữ liệu từ CRM hoặc phần mềm kế toán để AI phân tích bức tranh tài chính toàn diện hơn.

### 📌 Kết luận
Với sự kết hợp hoàn hảo giữa n8n, Google Sheets và AI DeepSeek, việc lập và phân tích báo cáo tài chính đa kỳ không còn là cơn ác mộng tốn thời gian. Hãy triển khai ngay workflow này để nâng cấp năng lực quản trị tài chính doanh nghiệp lên một tầm cao mới nhé các sếp!