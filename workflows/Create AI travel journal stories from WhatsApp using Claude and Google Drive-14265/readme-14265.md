---
title: "🌍 **Tự Động Hóa Sách Nhật Ký Du Lịch AI Từ WhatsApp: Chuyển Tin Nhắn & Ảnh Thành Câu Chuyện Đẹp**"
description: "Workflow này tự động chuyển đổi tin nhắn WhatsApp, ảnh và vị trí du lịch thành sách nhật ký du lịch AI hoàn chỉnh, lưu trữ trên Google Drive và gửi thông báo ngay lập tức. Giúp các sếp tiết kiệm thời gian ghi chép, đồng thời tạo ra những câu chuyện du lịch độc đáo, cá nhân hóa từ những khoảnh khắc thực tế."
slug: "tự-dộng-hoa-sách-nhật-ký-du-lịch-ai-whatsapp-google-drive"
tags: [n8n, automation, no-code, ai-content-creation, google-drive, whatsapp-api, anthropic-claude]
keywords: [tự động hóa du lịch, sách nhật ký du lịch AI, n8n workflow, Claude AI, Google Drive tự động, WhatsApp tự động hóa, tạo câu chuyện từ tin nhắn]
---

# 🌍 **Tự Động Hóa Sách Nhật Ký Du Lịch AI Từ WhatsApp: Chuyển Tin Nhắn & Ảnh Thành Câu Chuyện Đẹp**

## **😫 Nỗi Đau Của Các Sếp Khi Ghi Chép Nhật Ký Du Lịch**
Du lịch là trải nghiệm tuyệt vời, nhưng ghi chép lại những khoảnh khắc đó để tạo thành một cuốn sách nhật ký đẹp lại là một công việc tốn thời gian và dễ quên. Các sếp thường phải:
- **Làm thủ công**: Ghi chép từng tin nhắn, ảnh, và vị trí từ WhatsApp vào tài liệu.
- **Mất thời gian**: Phải sắp xếp lại thứ tự, thêm mô tả, và tạo câu chuyện từ những tin nhắn ngẫu nhiên.
- **Không chuyên nghiệp**: Những cuốn nhật ký thường thiếu cấu trúc, hình ảnh và cảm xúc thực sự.
- **Không liên tục**: Sau khi về nhà, nhiều người quên tiếp tục ghi chép, khiến cuốn sách trở nên rời rạc.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách tự động hóa toàn bộ quá trình!** Dựa trên **AI Claude (Anthropic)** và **Google Drive**, nó chuyển đổi tin nhắn WhatsApp, ảnh và vị trí thành **câu chuyện du lịch chuyên nghiệp**, lưu trữ trên Google Docs và gửi thông báo ngay lập tức.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động 24/7 mà không gián đoạn, các sếp nên **self-host n8n trên VPS** để đảm bảo tính ổn định và bảo mật cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải ghi chép thủ công, AI tự động tạo câu chuyện từ tin nhắn và ảnh.
- **Câu chuyện chuyên nghiệp**: AI Claude chuyển đổi tin nhắn ngẫu nhiên thành **lối văn mạch lạc, sinh động**, giống như một nhà văn du lịch chuyên nghiệp.
- **Lưu trữ tự động**: Tất cả nhật ký được lưu trên **Google Drive** với định dạng chuyên nghiệp (Google Docs).
- **Gửi thông báo ngay**: Sau khi hoàn thành, hệ thống sẽ gửi **tin nhắn WhatsApp** và **email** với liên kết đến cuốn nhật ký mới.
- **Tích hợp hình ảnh & vị trí**: Ảnh và vị trí du lịch được tự động chèn vào câu chuyện, làm cho nhật ký trở nên **hấp dẫn và thực tế hơn**.
- **Tự động liên kết các ngày**: Nếu du lịch nhiều ngày, hệ thống sẽ **liên kết các nhật ký** để tạo thành một cuốn sách hoàn chỉnh.
- **Bảo mật cao**: Tin nhắn và ảnh **không được lưu trữ lâu dài**, chỉ sử dụng để tạo câu chuyện một lần.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản WhatsApp Business API** hoặc **Twilio WhatsApp** (để nhận tin nhắn từ du lịch).
2. **Google Drive OAuth 2.0 API** (để lưu trữ và lấy nhật ký cũ).
3. **Anthropic API Key** (để sử dụng AI Claude Sonnet 4).
4. **SMTP Credentials** (nếu muốn gửi email thông báo).
5. **Folder Google Drive** riêng để lưu trữ nhật ký du lịch.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/14265](https://n8n.io/workflows/14265) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ link trên và **paste vào n8n Editor** (tab "Import").
- **Cách 3**: Sử dụng **n8n CLI** để import:
  ```bash
  n8n import workflow.json --name "AI Travel Journal"
  ```

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này gồm **14 node**, mỗi node đều có vai trò quan trọng. Dưới đây là hướng dẫn chi tiết:

##### **🔹 Node 1: Receive WhatsApp Messages (Webhook)**
- **Cấu hình**:
  - **Path**: `travel-journal` (không đổi).
  - **HTTP Method**: `POST`.
  - **URL Webhook**: Các sếp phải **cấu hình WhatsApp Business API** hoặc **Twilio** để gửi tin nhắn đến URL này.
    - Ví dụ: `https://tên-máy-chủ-n8n.com/webhook/travel-journal`
  - **Lưu ý**: WhatsApp phải gửi **tin nhắn, ảnh và vị trí** (nếu có) dưới dạng JSON.

##### **🔹 Node 2 & 3: JS #1 & Fetch Previous Journal Entries**
- **Node JS #1**: **Validate & Aggregate Messages**
  - **Chức năng**: Lọc tin nhắn, ảnh và vị trí, loại bỏ tin nhắn không liên quan.
  - **Lưu ý**: Các sếp **không cần chỉnh sửa** mã này (nếu không biết code), nó đã được tối ưu sẵn.
- **Node Google Drive**: **Fetch Previous Journal Entries**
  - **Cấu hình**:
    - **Credentials**: Chọn `googleDriveOAuth2Api` (đã cấu hình trước).
    - **Folder ID**: Điền **ID của folder Google Drive** nơi lưu nhật ký (tìm bằng cách chia sẻ folder và copy link).
    - **Query**: `mimeType='application/vnd.google-apps.document' and name contains 'Travel Journal'`.

##### **🔹 Node 4: JS #2: Prepare AI Context**
- **Chức năng**: Tạo **prompt AI** từ tin nhắn, ảnh và vị trí để Claude tạo câu chuyện.
- **Lưu ý**: Node này **tự động** lấy dữ liệu từ node trước, các sếp **không cần chỉnh sửa**.

##### **🔹 Node 5 & 6: Claude AI Story Generator & Claude Sonnet 4 Model**
- **Cấu hình**:
  - **Credentials**: Chọn `anthropicApi` (đã cấu hình API Key Claude).
  - **Model**: `claude-sonnet-4-20250514` (không đổi).
  - **Prompt**: Node JS #2 đã chuẩn bị sẵn, các sếp **không cần chỉnh sửa**.
- **Lưu ý**:
  - Nếu **API Key Claude hết hạn**, workflow sẽ **bị lỗi**. Các sếp cần **cập nhật API Key** trong n8n Credentials.
  - **Ngân sách API**: Claude Sonnet 4 có chi phí, các sếp nên **kiểm soát số lượng tin nhắn** để tránh chi phí quá cao.

##### **🔹 Node 7 & 8: Parse AI Story Response & JS #3: Format Document**
- **Chức năng**: AI trả về câu chuyện dưới dạng text, node này **chuyển đổi thành định dạng Google Docs**.
- **Lưu ý**: Node JS #3 **tự động** thêm tiêu đề, phân cách đoạn văn, và chuẩn bị cho Google Drive.

##### **🔹 Node 9: Wait for Processing**
- **Chức năng**: Đợi AI hoàn thành (thời gian chờ ~30 giây).
- **Lưu ý**: Thời gian này có thể thay đổi tùy thuộc vào **tải API Claude**.

##### **🔹 Node 10: Create/Update Google Doc**
- **Cấu hình**:
  - **Credentials**: Chọn `googleDriveOAuth2Api`.
  - **Folder ID**: Điền **ID folder** (như node 3).
  - **File Name**: `Travel Journal - [Ngày]` (ví dụ: `Travel Journal - 15-10-2024`).
- **Lưu ý**:
  - Nếu **không có file cũ**, nó sẽ tạo mới.
  - Nếu **có file cũ**, nó sẽ **cập nhật** nội dung.

##### **🔹 Node 11: Send WhatsApp Confirmation**
- **Cấu hình**:
  - **Credentials**: Chọn `whatsAppApi` (Twilio hoặc WhatsApp Business API).
  - **Body**: Tin nhắn thông báo thành công (có thể chỉnh sửa).
  - **Liên kết Google Doc**: Node này sẽ gửi **link trực tiếp** đến nhật ký mới.
- **Lưu ý**: Các sếp cần **cấu hình Twilio/WhatsApp API** trước.

##### **🔹 Node 12: Send Email with Journal Link**
- **Cấu hình**:
  - **Credentials**: Chọn `smtp` (nếu muốn gửi email).
  - **Người nhận**: Điền email của mình.
  - **Tiêu đề**: `📖 Nhật Ký Du Lịch AI Đã Hoàn Thành!`.
  - **Nội dung**: Gồm **link Google Doc** và mô tả ngắn.
- **Lưu ý**: Nếu **không cần email**, các sếp có thể **xóa node này**.

##### **🔹 Node 13 & 14: Build Success Response & Send Response to Webhook**
- **Chức năng**: Trả về **thông báo thành công** cho WhatsApp.
- **Lưu ý**: Node này **tự động** trả về JSON thành công, các sếp **không cần chỉnh sửa**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Slack/Telegram**:
   - Thay vì chỉ gửi **WhatsApp và email**, các sếp có thể thêm **node Slack/Telegram** để thông báo ngay khi nhật ký hoàn thành.
   - **Cách làm**:
     - Sử dụng **node `httpRequest`** để gửi thông báo đến Slack/Telegram API.
     - Ví dụ: `https://api.telegram.org/bot[TOKEN]/sendMessage?chat_id=[ID_CHAT]&text=[THÔNG BÁO]`.

2. **Lưu Log Cho Theo Dõi**:
   - Thêm **node `stickyNote`** để ghi lại **lịch sử xử lý** (tin nhắn nào đã được xử lý, thời gian, lỗi nếu có).
   - **Cách làm**:
     - Sử dụng **node `stickyNote`** sau node `Parse AI Story Response` để lưu log.

3. **Gửi Báo Cáo Định Kỳ**:
   - Nếu du lịch nhiều ngày, các sếp có thể **tự động gửi báo cáo tổng hợp** vào cuối ngày.
   - **Cách làm**:
     - Sử dụng **node `wait`** (thời gian chờ 24h) trước khi gửi báo cáo.
     - Sau đó, sử dụng **node `googleDrive`** để tạo **báo cáo tổng hợp** từ tất cả nhật ký.

4. **Tối Ưu API Claude**:
   - Nếu **chi phí API cao**, các sếp có thể:
     - **Giảm độ dài prompt** (loại bỏ tin nhắn không cần thiết).
     - **Sử dụng model Claude Haiku** (rẻ hơn nhưng chất lượng thấp hơn).
     - **Cập nhật API Key thường xuyên** để tránh bị chặn.

5. **Tự Động Xóa Tin Nhắn Sau Xử Lý**:
   - Nếu không muốn **tin nhắn WhatsApp bị lưu lâu**, các sếp có thể thêm **node `httpRequest`** để xóa tin nhắn sau khi tạo nhật ký.
   - **Cách làm**:
     - Sử dụng API của **Twilio/WhatsApp Business** để xóa tin nhắn.

---

### 📌 **Kết Luận: Hãy Tự Động Hóa Nhật Ký Du Lịch Ngay Hôm Nay!**
**Workflow này không chỉ tiết kiệm thời gian mà còn tạo ra những cuốn nhật ký du lịch đẹp, chuyên nghiệp và đầy cảm xúc** từ những tin nhắn và ảnh hàng ngày. Thay vì phải **ghi chép thủ công**, các sếp chỉ cần **nhận tin nhắn WhatsApp**, hệ thống sẽ tự động:
✅ **Tạo câu chuyện từ tin nhắn ngẫu nhiên**.
✅ **Chèn ảnh và vị trí** vào nhật ký.
✅ **Lưu trữ trên Google Drive** với định dạng chuyên nghiệp.
✅ **Gửi thông báo ngay** khi hoàn thành.

**Hành động ngay hôm nay!**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình API** (WhatsApp, Google Drive, Claude, SMTP).
3. **Bật workflow** và bắt đầu du lịch mà **không cần lo lắng ghi nhật ký**!

**🚀 [Tải workflow ngay từ n8n.io](https://n8n.io/workflows/14265) và tự động hóa nhật ký du lịch của mình!**

---
**💡 Cần hỗ trợ thêm?**
- **Hỏi đáp trên [Community n8n](https://community.n8n.io/)**.
- **Đăng ký VPS n8n** với mã giảm giá **VPSN8N** để tự host workflow 24/7.