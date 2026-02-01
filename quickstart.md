---
layout: page
title: Hướng Dẫn Nhanh
permalink: /quickstart/
---

# Hướng Dẫn Nhanh - Bắt Đầu Với OpenClaw

## Giới Thiệu

Trang này sẽ hướng dẫn bạn cài đặt và chạy OpenClaw trong vòng chưa đầy 10 phút. Đây là hướng dẫn dành cho người mới bắt đầu.

## Yêu Cầu Hệ Thống

Trước khi bắt đầu, hãy đảm bảo hệ thống của bạn đáp ứng các yêu cầu sau:

- **Node.js**: Phiên bản 22 trở lên
- **npm hoặc pnpm**: Để cài đặt gói
- **Git**: Để clone repository (nếu cần)

Kiểm tra phiên bản Node.js:
```
node --version
```

Nếu chưa có Node.js, bạn có thể tải từ [nodejs.org](https://nodejs.org/).

## Bước 1: Cài Đặt OpenClaw

### Cách 1: Sử dụng script cài đặt (khuyến nghị)

Chạy lệnh sau trong terminal:

**Linux/macOS:**
```bash
curl -fsSL https://openclaw.ai/install.sh | bash
```

**Windows (PowerShell):**
```powershell
iwr -useb https://openclaw.ai/install.ps1 | iex
```

### Cách 2: Cài đặt toàn cục

```bash
npm install -g openclaw@latest
```
hoặc
```bash
pnpm add -g openclaw@latest
```

## Bước 2: Chạy Trình Hướng Dẫn Cài Đặt

Chạy lệnh sau để bắt đầu trình hướng dẫn:
```
openclaw onboard --install-daemon
```

Trình hướng dẫn sẽ giúp bạn:
- Cấu hình xác thực (API key hoặc OAuth)
- Thiết lập gateway
- Cấu hình các kênh (WhatsApp, Telegram, v.v.)
- Cài đặt dịch vụ nền (tự động chạy khi khởi động)

## Bước 3: Khởi Động Gateway

Nếu bạn cài đặt dịch vụ nền trong bước trước, gateway đã tự động chạy. Kiểm tra trạng thái:
```
openclaw gateway status
```

Nếu chưa cài đặt dịch vụ, bạn có thể chạy thủ công:
```
openclaw gateway --port 18789
```

## Bước 4: Trò Chuyện Thử Nghiệm

Mở giao diện điều khiển trong trình duyệt:
```
openclaw dashboard
```

Hoặc truy cập trực tiếp: [http://127.0.0.1:18789/](http://127.0.0.1:18789/)

## Bước 5: Kết Nối Kênh (Tùy Chọn)

### Kết Nối WhatsApp

1. Chạy lệnh:
```
openclaw channels login
```

2. Quét mã QR bằng WhatsApp trên điện thoại của bạn:
   - Mở WhatsApp
   - Vào Cài đặt → Thiết Bị Đã Kết Nối
   - Quét mã QR hiển thị trên màn hình

### Kết Nối Telegram

1. Tạo bot với [@BotFather](https://t.me/BotFather) trên Telegram
2. Sao chép bot token
3. Trong trình hướng dẫn, chọn cấu hình Telegram và nhập token

## Bước 6: Gửi Tin Nhắn Thử Nghiệm

Gửi tin nhắn thử để kiểm tra:
```
openclaw message send --target +15555550123 --message "Xin chào từ OpenClaw!"
```

## Các Lệnh Thường Dùng

### Kiểm Tra Trạng Thái
```
openclaw status
openclaw health
```

### Gửi Tin Nhắn
```
openclaw message send --target +số-điện-thoại --message "Nội dung tin nhắn"
```

### Quản Lý Phiên
```
openclaw sessions list
openclaw sessions clear
```

### Nhật Ký Hệ Thống
```
openclaw logs --follow
```

## Cấu Hình Nhanh

Nếu bạn muốn cấu hình nhanh mà không dùng trình hướng dẫn:

Tạo tệp `~/.openclaw/openclaw.json` với nội dung tối thiểu:
```json
{
  "agents": {
    "defaults": {
      "model": "openai/gpt-4o-mini",
      "workspace": "~/.openclaw/workspace"
    }
  },
  "gateway": {
    "port": 18789,
    "bind": "127.0.0.1",
    "auth": {
      "token": "mã-token-bảo-mật-của-bạn"
    }
  }
}
```

## Mẹo Bắt Đầu Nhanh

💡 **Dùng trình hướng dẫn**: Trình hướng dẫn `openclaw onboard` là cách dễ nhất để bắt đầu

💡 **Bắt đầu từ đơn giản**: Không cần kết nối tất cả các kênh ngay từ đầu

💡 **Kiểm tra thường xuyên**: Dùng `openclaw health` để kiểm tra trạng thái hệ thống

💡 **Sao lưu cấu hình**: Luôn sao lưu tệp cấu hình quan trọng

💡 **Theo dõi nhật ký**: Dùng `openclaw logs --follow` để theo dõi hoạt động

## Vấn Đề Thường Gặp

### Lỗi "Command not found"
- Kiểm tra lại việc cài đặt
- Đảm bảo thư mục cài đặt được thêm vào PATH

### Lỗi kết nối gateway
- Kiểm tra trạng thái gateway: `openclaw gateway status`
- Đảm bảo cổng 18789 chưa được sử dụng

### Không nhận được phản hồi từ AI
- Kiểm tra cấu hình xác thực (API key, OAuth)
- Đảm bảo mô hình được chọn hợp lệ

## Những Bước Tiếp Theo

Sau khi hoàn thành hướng dẫn nhanh này, bạn có thể:

1. [Tìm hiểu các khái niệm cốt lõi](./docs/concepts/index.md)
2. [Kết nối thêm các kênh truyền thông](./docs/channels/whatsapp.md)
3. [Tìm hiểu về công cụ và kỹ năng](./docs/tools/index.md)
4. [Tùy chỉnh cấu hình nâng cao](./docs/gateway/index.md)
5. [Khám phá các trường hợp sử dụng thực tế](./about.md)

## Hỗ Trợ

Nếu bạn gặp vấn đề trong quá trình cài đặt:

- [Xem câu hỏi thường gặp](./faq.md)
- [Kiểm tra nhật ký hệ thống](./docs/gateway/index.md#giám-sát-hoạt-động)
- [Tạo issue trên GitHub](https://github.com/yourusername/openclaw-docs-vi/issues)

---

💡 **Lưu ý**: Đây là hướng dẫn nhanh, không phải tài liệu tham khảo đầy đủ. Để biết thông tin chi tiết, vui lòng tham khảo các phần tương ứng trong tài liệu.