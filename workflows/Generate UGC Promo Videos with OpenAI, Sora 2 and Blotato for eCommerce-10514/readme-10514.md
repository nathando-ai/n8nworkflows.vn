---
title: "🚀 Tự động tạo video quảng cáo UGC bằng OpenAI, Sora 2 và Blotato cho Thương mại điện tử"
description: "Hướng dẫn chi tiết workflow n8n biến hình ảnh sản phẩm và mô tả từ Telegram thành video quảng cáo UGC chuyên nghiệp bằng Sora 2 AI và tự động đăng đa nền tảng."
slug: "tu-dong-tao-video-ugc-openai-sora-2-blotato-e-commerce"
tags: [n8n, automation, ai, openai, sora, ecommerce, telegram]
keywords: [n8n workflow, tao video ugc tu dong, sora 2 ai, blotato automation, ai e-commerce marketing]
---

# 🚀 Tự động tạo video quảng cáo UGC bằng OpenAI, Sora 2 và Blotato cho Thương mại điện tử

Các sếp làm trong ngành thương mại điện tử (eCommerce) chắc chắn hiểu rõ tầm quan trọng của video UGC (User Generated Content) trong việc chạy quảng cáo. Tuy nhiên, việc thuê creator quay dựng, viết kịch bản và chỉnh sửa tốn rất nhiều thời gian, chi phí và nhân lực. 

Giải pháp gì để tự động hóa 100% quy trình này? Bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực kỳ mạnh mẽ, kết hợp giữa **Telegram**, **OpenAI (GPT-4o)**, **Sora 2 (qua FAL.ai)** và **Blotato** để biến một bức ảnh sản phẩm bình thường thành video quảng cáo triệu view và tự động đăng lên mạng xã hội chỉ trong vài phút!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện**: Chỉ cần gửi ảnh sản phẩm và mô tả qua Telegram, hệ thống tự lo phần còn lại.
- **Kịch bản AI thông minh**: Phân tích sản phẩm bằng Vision API và tạo kịch bản video 12 giây chuẩn marketing.
- **Video AI chất lượng cao**: Sử dụng công nghệ Sora 2 (Image-to-Video) tạo thước phim chân thực, bắt mắt.
- **Đa kênh mạng xã hội**: Tự động phân phối video qua Blotato lên TikTok, YouTube, Instagram, Facebook, LinkedIn...
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị các tài khoản và API Keys sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Telegram Bot Token** (tạo qua `@BotFather`).
- **OpenAI API Key** (hoặc dùng credits sẵn có trên n8n).
- **FAL.ai API Key** (để gọi mô hình Sora 2).
- **Blotato Account & API Key** (để quản lý và đăng video đa nền tảng).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow từ nguồn cung cấp, sau đó mở n8n Editor, chọn **Add workflow** -> **Import from JSON** và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 28 nodes, được chia thành các bước chính sau cần cấu hình kỹ:

- **Telegram Trigger & Telegram Nodes**: 
  - Tạo Bot mới thông qua `@BotFather` trên Telegram để lấy API Token.
  - Cấu hình các node như *Telegram Trigger*, *Get Photo File from Telegram*, *Send Video to Telegram*, *Send Error Message* bằng cách tạo credential loại `telegramApi` và dán token vào.
- **Workflow Configuration (Node Set)**:
  - Nơi lưu trữ các cấu hình quan trọng. Các sếp nhớ điền `falApiKey` lấy từ dashboard của FAL.ai.
  - Các thông số video mặc định như `maxPollingAttempts: 20`, `model: sora-2`, `aspect_ratio: 9:16`, `duration: 12` có thể tùy chỉnh trực tiếp tại đây.
- **Cài đặt Blotato Community Node (Publishing)**:
  - Vào **Settings → Community Nodes** trong n8n, nhấn **Install** và thêm gói: `@blotato/n8n-nodes-blotato`.
  - Lấy API Key từ tài khoản Blotato (**Settings → API Keys**) và tạo credential loại **Blotato API** để cấu hình cho các node đăng bài như *TikTok*, *Youtube*, *Instagram*, *Facebook*, v.v.

#### 3. Kích hoạt ⚡️
- Gửi tin nhắn `/start` kèm ảnh sản phẩm và mô tả vào Bot Telegram vừa tạo để test thử luồng chạy.
- Sau khi kiểm tra mọi thứ hoạt động trơn tru, bật công tắc **Active workflow** lên trạng thái chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ dữ liệu**: Kết nối thêm node Google Sheets hoặc Airtable sau bước phân tích sản phẩm để lưu lại lịch sử các kịch bản và video đã tạo.
- **Thông báo đội ngũ**: Tích hợp thêm Slack hoặc kênh Telegram nội bộ để gửi thông báo mỗi khi video được tạo thành công hoặc khi có lỗi xảy ra.
- **Tùy chỉnh thời lượng**: Có thể điều chỉnh `duration` thành 5s hoặc 10s trong cấu hình để tối ưu chi phí API tùy theo nhu cầu chiến dịch quảng cáo.

### 📌 Kết luận
Workflow tự động hóa tạo video UGC với OpenAI, Sora 2 và Blotato là vũ khí cực mạnh giúp các sếp tối ưu hóa chi phí sản xuất content và chiếm lĩnh các nền tảng video ngắn (TikTok, Reels, Shorts). Hãy cài đặt ngay hôm nay để bứt phá doanh thu thương mại điện tử!