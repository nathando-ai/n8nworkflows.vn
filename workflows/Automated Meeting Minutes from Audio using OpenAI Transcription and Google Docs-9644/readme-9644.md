---
title: "🎙️ Tự Động Hóa Biên Bản Họp Từ Audio: OpenAI + Google Docs"
description: "Biến file ghi âm cuộc họp thành biên bản chuyên nghiệp, có hành động cụ thể (Action Items) và lưu tự động vào Google Docs chỉ trong vài giây."
slug: "tu-dong-hoa-bien-ban-hop-tu-audio-openai-google-docs"
tags: [n8n, automation, ai, openai, google-docs, meeting-minutes]
keywords: [n8n workflow, biên bản họp, openai transcription, google docs automation, tự động hóa văn phòng]
---

# 🎙️ Tự Động Hóa Biên Bản Họp Từ Audio: OpenAI + Google Docs

Các sếp có bao giờ cảm thấy mệt mỏi khi phải nghe lại những file ghi âm cuộc họp dài dòng để soạn biên bản? Hay đơn giản là lãng phí hàng giờ mỗi tuần chỉ để tóm tắt những ý chính và phân công công việc?

Workflow này chính là "trợ lý ảo" hoàn hảo cho các sếp. Thay vì làm thủ công, các sếp chỉ cần upload file ghi âm (mp3, m4a, wav) và điền vài thông tin cơ bản. Hệ thống sẽ tự động:
1. Chuyển giọng nói thành văn bản (Transcribe) bằng OpenAI.
2. Phân tích nội dung, trích xuất ý chính, các hành động cần thực hiện (Action Items) và mối quan tâm.
3. Tạo một tài liệu Google Docs mới, định dạng chuyên nghiệp và chèn nội dung biên bản vào đó.
4. Trả về link tài liệu để các sếp chia sẻ ngay lập tức.

Tất cả diễn ra tự động, không cần code, chính xác và cực kỳ nhanh chóng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, đặc biệt khi xử lý file audio có dung lượng lớn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian khổng lồ:** Biến 1 giờ nghe lại và soạn thảo thành 30 giây chờ đợi.
- **Biên bản chuẩn hóa:** Luôn có cấu trúc rõ ràng: Ý chính, Hành động (Người phụ trách, Hạn chót), và Mối quan tâm.
- **Lưu trữ tập trung:** Biên bản được lưu tự động vào Google Drive/Docs, dễ dàng tìm kiếm và truy cập.
- **Độ chính xác cao:** Sử dụng sức mạnh của OpenAI để hiểu ngữ cảnh và tóm tắt đúng trọng tâm, tránh sót ý quan trọng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n:** Chạy local hoặc trên VPS.
2. **Tài khoản OpenAI:** Cần API Key để sử dụng chức năng Transcribe (chuyển giọng nói thành chữ) và Chat (tóm tắt).
3. **Tài khoản Google:** Cần kết nối OAuth2 cho Google Docs để tạo và chỉnh sửa tài liệu.
4. **File ghi âm mẫu:** Định dạng mp3, m4a hoặc wav (khuyến nghị dưới 50MB để xử lý nhanh).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from File** hoặc **Import from URL**.
3. Dán link workflow gốc hoặc upload file JSON.
4. Workflow sẽ hiển thị 5 nodes chính: `Meeting Intake`, `Transcribe recording`, `Generate Meeting Minutes`, `Create Minutes Doc`, và `Insert Minutes Content`.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Đây là phần quan trọng nhất. Các sếp cần cấu hình từng node để khớp với tài khoản của mình:

**1. Node: `Meeting Intake` (Form Trigger)**
- Đây là nơi các sếp tạo form nhập liệu.
- **Tham số cần kiểm tra:**
    - `Audio`: Đảm bảo loại file cho phép là `audio/mpeg`, `audio/mp4`, `audio/wav`.
    - `Manager`, `Partner`, `Situation`: Các trường văn bản này sẽ được đưa vào prompt để AI hiểu bối cảnh cuộc họp.
- **Mẹo:** Các sếp có thể thêm trường `Project Name` hoặc `Date` nếu muốn biên bản chi tiết hơn.

**2. Node: `Transcribe recording` (OpenAI)**
- **Credentials:** Chọn credential OpenAI đã tạo.
- **Model:** Mặc định thường dùng `whisper-1`. Đây là model chuẩn để chuyển giọng nói sang văn bản.
- **Input:** Node này nhận binary data từ node Form Trigger. Đảm bảo rằng output của Form Trigger được map đúng vào input của node này.

**3. Node: `Generate Meeting Minutes` (OpenAI - Chat)**
- **Credentials:** Chọn credential OpenAI.
- **Model:** Chọn model chat mạnh như `gpt-4o` hoặc `gpt-3.5-turbo` (tùy ngân sách).
- **System Prompt / User Prompt:**
    - Node này nhận input `{{ $json.text }}` (kết quả từ bước Transcribe) và các trường từ Form.
    - **Quan trọng:** Các sếp nên chỉnh sửa prompt để phù hợp với phong cách biên bản của công ty. Ví dụ:
      > "Bạn là một thư ký chuyên nghiệp. Dựa trên nội dung cuộc họp dưới đây, hãy tạo biên bản với cấu trúc:
      > 1. **Ý Chính**: Tóm tắt ngắn gọn.
      > 2. **Hành Động Tiếp Theo**: Liệt kê dạng bảng hoặc danh sách, mỗi mục gồm: Việc cần làm, Người phụ trách, Hạn chót.
      > 3. **Mối Quan Tâm/Rủi Ro**: Các vấn đề cần lưu ý.
      >
      > Nội dung cuộc họp: {{ $json.text }}
      > Người quản lý: {{ $json.manager }}
      > Đối tác: {{ $json.partner }}"
    - **Max Tokens:** Cài đặt khoảng 1000-2000 tokens để đảm bảo đủ chỗ cho biên bản chi tiết.

**4. Node: `Create Minutes Doc` (Google Docs)**
- **Credentials:** Chọn credential Google (OAuth2).
- **Folder ID:** Các sếp cần tìm ID của thư mục trên Google Drive nơi muốn lưu biên bản.
    - *Cách lấy Folder ID:* Mở thư mục trên Drive, nhìn vào URL. Phần sau `folders/` chính là Folder ID.
- **Document Name:** Có thể đặt tên động, ví dụ: `Biên bản họp - {{ $json.date }} - {{ $json.partner }}`.

**5. Node: `Insert Minutes Content` (Google Docs)**
- **Operation:** Chọn `Update` (hoặc `Append` nếu muốn thêm vào cuối tài liệu đã có sẵn).
- **Document ID:** Lấy từ output của node `Create Minutes Doc` (thường là `{{ $json.id }}`).
- **Content:** Đây là nơi chèn nội dung biên bản đã được AI tạo ra.
    - Đảm bảo map đúng trường chứa text biên bản từ node `Generate Meeting Minutes`.
    - Các sếp có thể thêm header/footer tĩnh bằng cách hardcode vào trường này hoặc dùng template.

#### 3. Kích hoạt ⚡️
1. **Test Run:**
    - Nhấn nút **Execute Workflow**.
    - Một form sẽ hiện ra. Các sếp upload một file audio ngắn (dưới 2 phút để test nhanh) và điền thông tin mẫu.
    - Chạy workflow và kiểm tra xem có tài liệu Google Docs mới được tạo ra không.
    - Mở tài liệu đó để kiểm tra độ chính xác của nội dung biên bản.
2. **Bật Active:**
    - Nếu mọi thứ ổn, bật công tắc **Active** ở góc trên bên phải.
    - Copy link Form từ node `Meeting Intake` để chia sẻ cho team.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram:** Thêm một node `Slack` hoặc `Telegram` sau cùng để gửi thông báo "Biên bản họp đã sẵn sàng" kèm link tài liệu vào kênh làm việc.
- **Gửi Email tự động:** Thêm node `Gmail` để gửi biên bản vào email của các thành viên tham gia họp.
- **Tùy chỉnh Prompt theo ngành:** Nếu các sếp làm trong lĩnh vực pháp lý hoặc y tế, hãy điều chỉnh prompt để AI sử dụng ngôn ngữ chuyên ngành và nhấn mạnh các điều khoản quan trọng.
- **Xử lý lỗi:** Thêm một node `Error Trigger` để xử lý các trường hợp file audio quá lớn hoặc không rõ tiếng, gửi thông báo lỗi cho admin.

### 📌 Kết luận
Việc tự động hóa biên bản họp không chỉ giúp tiết kiệm thời gian mà còn đảm bảo tính nhất quán và chuyên nghiệp trong cách làm việc của doanh nghiệp. Với workflow n8n kết hợp OpenAI và Google Docs này, các sếp có thể biến những file ghi âm "chết" thành những tài liệu sống động, có hành động cụ thể.

Hãy thử ngay hôm nay và trải nghiệm sự khác biệt! Nếu có bất kỳ khó khăn nào trong quá trình setup, đừng ngại chia sẻ để cộng đồng cùng hỗ trợ. Chúc các sếp thành công! 🚀