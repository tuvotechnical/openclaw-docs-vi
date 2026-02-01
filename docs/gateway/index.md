---
layout: default
title: "Gateway & Hoạt Động Hệ Thống"
nav_exclude: true
---

# Gateway & Hoạt Động Hệ Thống (Dịch Tiếng Việt)

## Tổng Quan Về Gateway

Gateway là thành phần trung tâm của OpenClaw. Nó đóng vai trò như một "cổng kết nối" giữa các kênh truyền thông (WhatsApp, Telegram, Discord, v.v.) và các tác nhân AI.

### Vai Trò Chính Của Gateway

1. **Quản lý kết nối kênh**: Duy trì kết nối với các nền tảng truyền thông
2. **Điều phối tác nhân**: Gửi tin nhắn đến tác nhân AI phù hợp
3. **Quản lý phiên làm việc**: Theo dõi và lưu trữ các cuộc trò chuyện
4. **Bảo mật và xác thực**: Kiểm soát quyền truy cập và bảo vệ hệ thống

## Kiến Trúc Gateway

```
[WhatsApp/Telegram/Discord/iMessage]
         │
         ▼
┌─────────────────────────────────┐
│            Gateway              │
│  (quản lý kết nối & phiên làm  │
│   việc duy nhất trên máy tính) │
└─────────┬───────────────────────┘
          │
    ┌─────┴─────┐
    │           │
    ▼           ▼
Tác nhân AI   CLI/Ứng dụng
  (Pi, v.v.)   điều khiển
```

### Mô Hình Mạng

- **Một Gateway mỗi máy tính** (khuyến nghị): Đây là quy trình duy nhất được phép sở hữu phiên WhatsApp Web
- **Ưu tiên loopback**: Gateway WS mặc định là ws://127.0.0.1:18789
- **Hỗ trợ từ xa**: Có thể truy cập từ xa qua SSH tunnel hoặc Tailscale

## Cấu Hình Gateway

### Cấu Hình Cơ Bản

Tệp cấu hình chính: `~/.openclaw/openclaw.json`

```json
{
  "gateway": {
    "port": 18789,
    "bind": "127.0.0.1",
    "auth": {
      "token": "mã-token-bảo-mật"
    },
    "tailscale": {
      "enabled": false
    }
  }
}
```

### Cấu Hình Nâng Cao

```json
{
  "gateway": {
    "reconnect": {
      "initialMs": 1000,
      "maxMs": 30000,
      "factor": 1.5,
      "jitter": 0.1,
      "maxAttempts": 10
    },
    "heartbeatSeconds": 60,
    "lock": {
      "enabled": true,
      "timeoutMs": 30000
    }
  }
}
```

## Quản Lý Gateway

### Khởi Động Gateway

Chạy thủ công:
```
openclaw gateway --port 18789
```

Dùng dịch vụ nền (sau khi cài đặt qua trình hướng dẫn):
```
openclaw gateway status  # Kiểm tra trạng thái
```

### Giám Sát Hoạt Động

Gateway có các tính năng giám sát:
- **Nhịp tim (Heartbeat)**: Kiểm tra sức khỏe định kỳ
- **Nhật ký (Logs)**: Ghi lại hoạt động hệ thống
- **Sức khỏe (Health)**: Kiểm tra trạng thái toàn hệ thống

## Bảo Mật Gateway

### Xác Thực

- **Mã token**: Gateway tạo mã token để xác thực kết nối
- **Chỉ loopback**: Mặc định chỉ cho phép kết nối từ cùng máy tính
- **Xác thực kênh**: Mỗi kênh có cơ chế xác thực riêng

### Kiểm Soát Truy Cập

- **Danh sách cho phép**: Chỉ người trong danh sách mới được tương tác
- **Chế độ ghé nối**: Người chưa biết nhận mã xác nhận trước khi tương tác
- **Phân quyền công cụ**: Giới hạn hành động của tác nhân AI

## Tích Hợp Với Các Thành Phần Khác

### Với Tác Nhân AI

Gateway giao tiếp với tác nhân AI qua giao thức RPC:
- Gửi tin nhắn đến tác nhân
- Nhận phản hồi từ tác nhân
- Quản lý phiên làm việc

### Với Kênh Truyền Thông

Gateway duy trì kết nối với các kênh:
- WhatsApp Web qua Baileys
- Telegram Bot API
- Discord Bot API
- iMessage (macOS)

### Với Giao Diện Người Dùng

Gateway cung cấp giao diện điều khiển:
- Web UI tại http://127.0.0.1:18789
- CLI qua lệnh openclaw
- Ứng dụng desktop

## Vấn Đề Thường Gặp

### Kết Nối Bị Mất

**Triệu chứng**: Kênh hiển thị "disconnected"

**Giải pháp**:
- Kiểm tra trạng thái gateway: `openclaw gateway status`
- Khởi động lại gateway nếu cần
- Kiểm tra kết nối internet

### Không Nhận Được Tin Nhắn

**Triệu chứng**: Tin nhắn gửi đi không nhận được phản hồi

**Giải pháp**:
- Kiểm tra cấu hình kênh
- Đảm bảo gateway đang chạy
- Kiểm tra danh sách cho phép/ghé nối

### Hiệu Suất Thấp

**Triệu chứng**: Phản hồi chậm, hệ thống ì

**Giải pháp**:
- Kiểm tra tài nguyên hệ thống
- Tối ưu cấu hình tác nhân
- Cân nhắc chạy trên phần cứng mạnh hơn

## Mẹo Quản Lý

💡 **Sử dụng dịch vụ nền**: Cài đặt gateway như dịch vụ để tự động chạy khi khởi động

💡 **Bảo mật token**: Luôn sử dụng mã token để bảo vệ gateway, ngay cả khi chỉ chạy cục bộ

💡 **Giám sát thường xuyên**: Kiểm tra nhật ký định kỳ để phát hiện vấn đề sớm

💡 **Sao lưu cấu hình**: Luôn sao lưu tệp cấu hình quan trọng

💡 **Cập nhật định kỳ**: Giữ Gateway luôn ở phiên bản mới nhất để bảo mật và tính năng

## Kết Luận

Gateway là trái tim của hệ thống OpenClaw. Hiểu rõ cách nó hoạt động sẽ giúp bạn quản lý hệ thống hiệu quả và giải quyết vấn đề nhanh chóng khi cần.

---

**Lưu ý**: Đây là tài liệu hướng dẫn, không phải tài liệu tham khảo đầy đủ. Để biết thông tin chi tiết kỹ thuật, vui lòng tham khảo tài liệu chính thức.