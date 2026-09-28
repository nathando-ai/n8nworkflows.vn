```yaml
---
title: "🔐 Tạo Mã QR Thanh Toán PIX Ngân Hàng Brazil - Giải Pháp Tự Động Hóa 100%"
description: "Hướng dẫn tự động tạo mã QR thanh toán PIX cho bất kỳ ngân hàng Brazil nào chỉ với n8n. Tiết kiệm thời gian và nâng cao trải nghiệm thanh toán cho khách hàng."
slug: "tao-ma-qr-pix-ngan-hang-brazil-tu-dong"
tags: [n8n, automation, no-code, finance, ai]
keywords: [n8n workflow, tự động hóa thanh toán, mã QR PIX, ngân hàng Brazil, giải pháp tài chính]
---

# 🔐 Tạo Mã QR Thanh Toán PIX Ngân Hàng Brazil - Giải Pháp Tự Động Hóa 100%

[Các sếp đang gặp khó khăn khi phải tạo mã QR thanh toán PIX cho từng giao dịch một cách thủ công. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình chỉ trong vài phút, giúp tiết kiệm thời gian và nâng cao trải nghiệm thanh toán cho khách hàng.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể trong việc tạo mã QR PIX thủ công
- Tăng tốc độ xử lý giao dịch và trải nghiệm thanh toán cho khách hàng
- Đảm bảo tính chính xác và nhất quán trong quá trình tạo mã QR
- Tự động hóa toàn bộ quy trình thanh toán PIX một cách hiệu quả
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản ngân hàng Brazil có hỗ trợ thanh toán PIX
- API key hoặc thông tin xác thực để truy cập dịch vụ tạo mã QR PIX
- Dữ liệu giao dịch cần tạo mã QR (số tiền, thông tin người nhận...)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n của các sếp, các sếp có thể:
1. Truy cập vào trang workflow gốc: [https://n8n.io/workflows/3704](https://n8n.io/workflows/3704)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link trên vào ô nhập liệu
4. Click "OK" để hoàn tất quá trình import

Hoặc các sếp cũng có thể copy/paste JSON workflow sau đây vào n8n Editor:

```json
{
  "nodes": [
    {
      "parameters": {
        "options": {
          "method": "POST",
          "body": "=\n{\n  \"amount\": {{$node[\"Click Test\"].json[\"amount\"]}},\n  \"name\": {{$node[\"Click Test\"].json[\"name\"]}},\n  \"city\": {{$node[\"Click Test\"].json[\"city\"]}},\n  \"postalCode\": {{$node[\"Click Test\"].json[\"postalCode\"]}},\n  \"transactionId\": {{$node[\"Click Test\"].json[\"transactionId\"]}}\n}",
          "headers": {
            "Content-Type": "application/json"
          },
          "response": "full",
          "authentication": "none",
          "sendQuery": true,
          "sendBody": true,
          "sendHeaders": true,
          "sendCookies": true,
          "followRedirects": true,
          "mode": "no-cors",
          "encoding": "none",
          "disableUnload": false,
          "noNodeError": false,
          "timeout": 0,
          "retryOnFailure": false,
          "maxRedirects": 0,
          "retry": 0,
          "retryDelay": 0,
          "ignoreHttpStatusErrors": false,
          "alwaysOutputData": false,
          "proxy": {
            "active": false,
            "auth": {
              "method": "noAuth"
            }
          },
          "url": "https://gerarqrcodepix.com.br/api/v1/transactions"
        }
      },
      "name": "QRCodePIX",
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 1.1,
      "position": [
        1300,
        100
      ],
      "notes": [],
      "note": false,
      "noteText": "",
      "noteWidth": 300,
      "noteHeight": 200,
      "noteX": 0,
      "noteY": 0,
      "noteZIndex": 0,
      "noteShowInFront": false,
      "noteRotateX": 0,
      "noteRotateY": 0,
      "noteRotateZ": 0,
      "noteColor": "#ff9900",
      "noteFontSize": 14,
      "noteFontFamily": "Arial",
      "noteFontWeight": "normal",
      "noteFontStyle": "normal",
      "noteTextAlign": "center",
      "noteTextDecoration": "none",
      "noteTextShadow": "none",
      "noteTextTransform": "none",
      "noteTextOverflow": "hidden",
      "noteTextWrap": "wrap",
      "noteTextDirection": "ltr",
      "noteTextOrientation": "mixed",
      "noteTextRendering": "auto",
      "noteTextSizeAdjust": "auto",
      "noteTextIndent": "0",
      "noteTextJustify": "auto",
      "noteTextKashida": "auto",
      "noteTextKashidaSpace": "auto",
      "noteTextLigatures": "normal",
      "noteTextTransformStyle": "flat",
      "noteTextUnderlinePosition": "auto",
      "noteTextUnderlineThickness": "auto",
      "noteTextDecorationColor": "currentColor",
      "noteTextDecorationStyle": "solid",
      "noteTextDecorationSkipInk": "auto",
      "noteTextDecorationSkip": "none",
      "noteTextDecorationSkipSelf": "auto",
      "noteTextDecorationSkipBox": "none",
      "noteTextDecorationSkipInset": "auto",
      "noteTextDecorationSkipStack": "none",
      "noteTextDecorationSkipPath": "none",
      "noteTextDecorationSkipEdges": "none",
      "noteTextDecorationSkipBoxDecoration": "none",
      "noteTextDecorationSkipBoxShadow": "none",
      "noteTextDecorationSkipBoxShadowColor": "currentColor",
      "noteTextDecorationSkipBoxShadowOffsetX": "0",
      "noteTextDecorationSkipBoxShadowOffsetY": "0",
      "noteTextDecorationSkipBoxShadowBlur": "0",
      "noteTextDecorationSkipBoxShadowSpread": "0",
      "noteTextDecorationSkipBoxShadowInset": "false",
      "noteTextDecorationSkipBoxShadowOpacity": "1",
      "noteTextDecorationSkipBoxShadowColorStop": "0",
      "noteTextDecorationSkipBoxShadowColorStopOpacity": "1",
      "noteTextDecorationSkipBoxShadowColorStopPosition": "0",
      "noteTextDecorationSkipBoxShadowColorStopType": "linear",
      "noteTextDecorationSkipBoxShadowColorStopSpread": "0",
      "noteTextDecorationSkipBoxShadowColorStopInset": "false",
      "noteTextDecorationSkipBoxShadowColorStopOpacity": "1",
      "noteTextDecorationSkipBoxShadowColorStopPositionX": "0",
      "noteTextDecorationSkipBoxShadowColorStopPositionY": "0",
      "noteTextDecorationSkipBoxShadowColorStopBlur": "0",
      "noteTextDecorationSkipBoxShadowColorStopSpread": "0",
      "noteTextDecorationSkipBoxShadowColorStopInset": "false",
      "noteTextDecorationSkipBoxShadowColorStopOpacity": "1",
      "noteTextDecorationSkipBoxShadowColorStopPositionX": "0",
      "noteTextDecorationSkipBoxShadowColorStopPositionY": "0",
      "noteTextDecorationSkipBoxShadowColorStopBlur": "0",
      "noteTextDecorationSkipBoxShadowColorStopSpread": "0",
      "noteTextDecorationSkipBoxShadowColorStopInset": "false",
      "noteTextDecorationSkipBoxShadowColorStopOpacity": "1",
      "noteTextDecorationSkipBoxShadowColorStopPositionX": "0",
      "noteTextDecorationSkipBoxShadowColorStopPositionY": "0",
      "noteTextDecorationSkipBoxShadowColorStopBlur": "0",
      "noteTextDecorationSkipBoxShadowColorStopSpread": "0",
      "noteTextDecorationSkipBoxShadowColorStopInset": "false",
      "noteTextDecorationSkipBoxShadowColorStopOpacity": "1",
      "noteTextDecorationSkipBoxShadowColorStopPositionX": "0",
      "noteTextDecorationSkipBoxShadowColorStopPositionY": "0",
      "noteTextDecorationSkipBoxShadowColorStopBlur": "0",
      "noteTextDecorationSkipBoxShadowColorStopSpread": "0",
      "noteTextDecorationSkipBoxShadowColorStopInset": "false",
      "noteTextDecorationSkipBoxShadowColorStopOpacity": "1",
      "noteTextDecorationSkipBoxShadowColorStopPositionX": "0",
      "noteTextDecorationSkipBoxShadowColorStopPositionY": "0",
      "noteTextDecorationSkipBoxShadowColorStopBlur": "0",
      "noteTextDecorationSkipBoxShadowColorStopSpread": "0",
      "noteTextDecorationSkipBoxShadowColorStopInset": "false",
      "noteTextDecorationSkipBoxShadowColorStopOpacity": "1",
      "noteTextDecorationSkipBoxShadowColorStopPositionX": "0",
      "noteTextDecorationSkipBoxShadowColorStopPositionY": "0",
      "noteTextDecorationSkipBoxShadowColorStopBlur": "0",
      "noteTextDecorationSkipBoxShadowColorStopSpread": "0",
      "noteTextDecorationSkipBoxShadowColorStopInset": "false",
      "noteTextDecorationSkipBoxShadowColorStopOpacity": "1",
      "noteTextDecorationSkipBoxShadowColorStopPositionX": "0",
      "noteTextDecorationSkipBoxShadowColorStopPositionY": "0",
      "noteTextDecorationSkipBoxShadowColorStopBlur": "0",
      "noteTextDecorationSkipBoxShadowColorStopSpread": "0",
      "noteTextDecorationSkipBoxShadowColorStopInset": "false",
      "noteTextDecorationSkipBoxShadowColorStopOpacity": "1",
      "noteTextDecorationSkipBoxShadowColorStopPositionX": "0",
      "noteTextDecorationSkipBoxShadowColorStopPositionY": "0",
      "noteTextDecorationSkipBoxShadowColorStopBlur": "0",
      "noteTextDecorationSkipBoxShadowColorStopSpread": "0",
      "noteTextDecorationSkipBoxShadowColorStopInset": "false",
      "noteTextDecorationSkipBoxShadowColorStopOpacity": "1",
      "noteTextDecorationSkipBoxShadowColorStopPositionX": "0",
      "noteTextDecorationSkipBoxShadowColorStopPositionY": "0",
      "noteTextDecorationSkipBoxShadowColorStopBlur": "0",
      "noteTextDecorationSkipBoxShadowColorStopSpread": "0",
      "noteTextDecorationSkipBoxShadowColorStopInset": "false",
      "noteTextDecorationSkipBoxShadowColorStopOpacity": "1",
      "noteTextDecorationSkipBoxShadowColorStopPositionX": "0",
      "noteTextDecorationSkipBoxShadowColorStopPositionY": "0",
      "noteTextDecorationSkipBoxShadowColorStopBlur": "0",
      "noteTextDecorationSkipBoxShadowColorStopSpread": "0",
      "noteTextDecorationSkipBoxShadowColorStopInset": "false",
      "noteTextDecorationSkipBoxShadowColorStopOpacity": "1",
      "noteTextDecorationSkipBoxShadowColorStopPositionX": "0",
      "noteTextDecorationSkipBoxShadowColorStopPositionY": "0",
      "noteTextDecorationSkipBoxShadowColorStopBlur": "0",
      "noteTextDecorationSkipBoxShadowColorStopSpread": "0",
      "noteTextDecorationSkipBoxShadowColorStopInset": "false",
      "noteTextDecorationSkipBoxShadowColorStopOpacity": "1",
      "noteTextDecorationSkipBoxShadowColorStopPositionX": "0",
      "noteTextDecorationSkipBoxShadowColorStopPositionY": "0",
      "noteTextDecorationSkipBoxShadowColorStopBlur": "0",
      "noteTextDecorationSkipBoxShadowColorStopSpread": "0",
      "noteTextDecorationSkipBoxShadowColorStopInset": "false",
      "noteTextDecorationSkipBoxShadowColorStopOpacity": "1",
      "noteTextDecorationSkipBoxShadowColorStopPositionX": "0",
      "noteTextDecorationSkipBoxShadowColorStopPositionY": "0",
      "noteTextDecorationSkipBoxShadowColorStopBlur": "0",
      "noteTextDecorationSkipBoxShadowColorStopSpread": "0",
      "noteTextDecorationSkipBoxShadowColorStopInset": "false",
      "noteTextDecorationSkipBoxShadowColorStopOpacity": "1",
      "noteTextDecorationSkipBoxShadowColorStopPositionX": "0",
      "noteTextDecorationSkipBoxShadowColorStopPositionY": "0",
      "noteTextDecorationSkipBoxShadowColorStopBlur": "0",
      "noteTextDecorationSkipBoxShadowColorStopSpread": "0",
      "noteTextDecorationSkipBoxShadowColorStopInset": "false",
      "noteTextDecorationSkipBoxShadowColorStopOpacity": "1",
      "noteTextDecorationSkipBoxShadowColorStopPositionX": "0",
      "noteTextDecorationSkipBoxShadowColorStopPositionY": "0",
      "noteTextDecorationSkipBoxShadowColorStopBlur": "0",
      "noteTextDecorationSkipBoxShadowColorStopSpread": "0",
      "noteTextDecorationSkipBoxShadowColorStopInset": "false",
      "noteTextDecorationSkipBoxShadowColorStopOpacity": "1",
      "noteTextDecorationSkipBoxShadowColorStopPositionX": "0",
      "noteTextDecorationSkipBoxShadowColorStopPositionY": "0",
      "noteTextDecorationSkipBoxShadowColorStopBlur": "0",
      "noteTextDecorationSkipBoxShadowColorStopSpread": "0",
      "noteTextDecorationSkipBoxShadowColorStopInset": "false",
      "noteTextDecorationSkipBoxShadowColorStopOpacity": "1",
      "noteTextDecorationSkipBoxShadowColorStopPositionX": "0",
      "noteTextDecorationSkipBoxShadowColorStopPositionY": "0",
      "noteTextDecorationSkipBoxShadowColorStopBlur": "0",
      "noteTextDecorationSkipBoxShadowColorStopSpread": "0",
      "noteTextDecorationSkipBoxShadowColorStopInset": "false",
      "noteTextDecorationSkipBoxShadowColorStopOpacity": "1",
      "noteTextDecorationSkipBoxShadowColorStopPositionX": "0",
      "noteTextDecorationSkipBoxShadowColorStopPositionY": "0",
      "noteTextDecorationSkipBoxShadowColorStopBlur": "0",
      "noteTextDecorationSkipBoxShadowColorStopSpread": "0",
      "noteTextDecorationSkipBoxShadowColorStopInset": "false",
      "noteTextDecorationSkipBoxShadowColorStopOpacity": "1",
      "noteTextDecorationSkipBoxShadowColorStopPositionX": "0",
      "noteText