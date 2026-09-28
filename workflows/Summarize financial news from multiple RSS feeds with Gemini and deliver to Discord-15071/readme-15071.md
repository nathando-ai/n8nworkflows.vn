---
title: "📈 Tự động tổng hợp tin tài chính từ nhiều nguồn với Gemini và gửi đến Discord"
description: "Workflow n8n tự động thu thập tin tức tài chính từ Yahoo Finance, CoinDesk và Federal Reserve, lọc nội dung quan trọng, tổng hợp bằng AI Gemini và gửi báo cáo hàng ngày đến Discord"
slug: "tu-dong-tong-hop-tin-tai-chinh-voi-gemini-discord"
tags: [n8n, automation, no-code, ai, discord]
keywords: [n8n workflow, tự động hóa, tổng hợp tin tức, ai gemini, discord]
---

# 📈 Tự động tổng hợp tin tài chính từ nhiều nguồn với Gemini và gửi đến Discord

[Các sếp] có biết không? Với lượng tin tức tài chính ngày càng tăng, việc theo dõi thủ công đã trở thành gánh nặng không nhỏ. Bạn phải mở nhiều tab, cuộn chuột liên tục và cố gắng hiểu được những tin tức quan trọng nào. Đó là lúc workflow này ra đời để giải phóng thời gian quý giá của các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không còn phải theo dõi thủ công nhiều nguồn tin
- **Nhận thông tin chính xác**: Lọc bỏ tin tức không liên quan, chỉ giữ lại những tin quan trọng
- **Nhận báo cáo hàng ngày**: Có bản tóm tắt tài chính hàng ngày được tổng hợp bởi AI Gemini
- **Tích hợp Discord**: Nhận báo cáo ngay trên kênh Discord quen thuộc
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google AI Studio (để lấy API key cho Google Gemini)
- Tài khoản Discord và quyền tạo bot (để lấy token)
- Kiến thức cơ bản về n8n (không cần lập trình)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/15071](https://n8n.io/workflows/15071)
2. Click vào nút "Import" ở góc trên bên phải
3. Copy toàn bộ JSON workflow và dán vào n8n Editor của bạn

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "01 | Click to Start Workflow"**:
   - Thay đổi từ Manual Trigger thành Schedule Trigger (ví dụ: hàng ngày lúc 8h sáng)

2. **Node "02 - Fetch - Yahoo Finance RSS"**:
   - Đảm bảo URL RSS của Yahoo Finance vẫn hoạt động
   - Có thể cần cập nhật URL nếu nó thay đổi

3. **Node "03 - Fetch - CoinDesk RSS"**:
   - Tương tự như Yahoo Finance, kiểm tra URL RSS

4. **Node "04 - Fetch - Federal Reserve RSS"**:
   - Kiểm tra URL RSS của Federal Reserve

5. **Node "10 - AI - Generate Wealth Summary"**:
   - Thêm credentials cho Google Gemini API
   - Có thể điều chỉnh prompt để phù hợp với nhu cầu cụ thể

6. **Node "13 | Send a message" và "13 | Send a Error message"**:
   - Thêm credentials cho Discord Bot API
   - Cấu hình kênh Discord nhận thông báo

#### 3. Kích hoạt ⚡️
1. Click vào nút "Test Workflow" để kiểm tra dữ liệu mẫu
2. Sau khi kiểm tra thành công, click vào nút "Activate" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Thêm nguồn tin**: Có thể thêm các nguồn tin khác như Bloomberg, Reuters để đa dạng hóa thông tin
2. **Tùy chỉnh báo cáo**: Điều chỉnh prompt trong node "10 - AI - Generate Wealth Summary" để phù hợp với ngành nghề của bạn
3. **Thông báo lỗi**: Cấu hình kênh Discord riêng để nhận thông báo lỗi khi workflow gặp sự cố
4. **Lịch sử báo cáo**: Có thể lưu trữ các báo cáo hàng ngày trong Google Sheets hoặc Notion để theo dõi dài hạn

### 📌 Kết luận
Workflow này không chỉ giúp các sếp tiết kiệm thời gian mà còn cung cấp thông tin tài chính chất lượng, được tổng hợp bởi AI Gemini. Với việc tích hợp Discord, các sếp có thể nhận báo cáo ngay trên kênh chat quen thuộc. Hãy thử ngay và trải nghiệm cách làm việc thông minh hơn!