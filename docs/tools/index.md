---
layout: default
title: "Công Cụ & Kỹ Năng"
nav_exclude: true
---

# Công Cụ & Kỹ Năng Trong OpenClaw (Dịch Tiếng Việt)

## Tổng Quan

Công cụ và kỹ năng là hai thành phần quan trọng giúp tác nhân AI trong OpenClaw có thể tương tác với thế giới thực và thực hiện các tác vụ phức tạp.

## Công Cụ (Tools)

Công cụ là các chức năng cơ bản mà tác nhân AI có thể sử dụng để thực hiện tác vụ. Đây là "bộ công cụ" giúp tác nhân AI tương tác với hệ thống và thế giới bên ngoài.

### Các Công Cụ Cơ Bản

#### 1. **exec** - Chạy Lệnh Hệ Thống
- Cho phép chạy các lệnh shell/command-line
- Hữu ích để thực hiện tác vụ hệ thống
- Có thể chạy lệnh nền hoặc tương tác

#### 2. **read** - Đọc Tệp Tin
- Đọc nội dung các tệp tin văn bản và hình ảnh
- Hỗ trợ nhiều định dạng (txt, md, jpg, png, v.v.)
- Trích xuất nội dung để phân tích

#### 3. **write** - Ghi Tệp Tin
- Tạo hoặc ghi đè nội dung tệp tin
- Tự động tạo thư mục nếu chưa tồn tại
- An toàn và kiểm soát truy cập

#### 4. **edit** - Chỉnh Sửa Tệp Tin
- Thay thế văn bản chính xác trong tệp tin
- Hữu ích để cập nhật cấu hình hoặc nội dung
- Yêu cầu văn bản gốc phải khớp chính xác

#### 5. **web_fetch** - Lấy Nội Dung Web
- Trích xuất nội dung từ URL
- Chuyển HTML thành văn bản dễ đọc
- Không yêu cầu trình duyệt đầy đủ

#### 6. **browser** - Điều Khiển Trình Duyệt
- Tự động hóa tương tác với website
- Hỗ trợ click, nhập liệu, chụp màn hình
- Có thể điều khiển cả Chrome và Firefox

#### 7. **message** - Gửi Tin Nhắn
- Gửi tin nhắn đến các kênh đã kết nối
- Hỗ trợ nhiều định dạng và kiểu tin nhắn
- Có thể gửi hình ảnh, tệp đính kèm

#### 8. **image** - Phân Tích Hình Ảnh
- Phân tích nội dung hình ảnh bằng mô hình AI
- Nhận diện đối tượng, văn bản, cảnh vật
- Trích xuất thông tin từ hình ảnh

### Kiểm Soát Công Cụ

OpenClaw có hệ thống kiểm soát chặt chẽ:
- **Mô phỏng (Sandbox)**: Chạy công cụ trong môi trường an toàn
- **Phân quyền**: Giới hạn quyền truy cập của từng công cụ
- **Xác thực nâng cao**: Một số công cụ yêu cầu xác thực đặc biệt

## Kỹ Năng (Skills)

Kỹ năng là các mô-đun chức năng được đóng gói sẵn để thực hiện các tác vụ chuyên biệt. Chúng là sự kết hợp của nhiều công cụ để tạo thành các chức năng hoàn chỉnh.

### Các Kỹ Năng Phổ Biến

#### 1. **youtube-analyzer** - Phân Tích YouTube
- Phân tích xu hướng, bình luận, nội dung
- Tạo ý tưởng video, kịch bản, tiêu đề
- Tự động thu thập dữ liệu từ YouTube

#### 2. **bluebubbles** - Kết Nối iMessage
- Tích hợp với hệ thống iMessage trên macOS
- Gửi và nhận tin nhắn iMessage qua OpenClaw
- Hỗ trợ đa thiết bị

#### 3. **coding-agent** - Tác Nhân Lập Trình
- Hỗ trợ viết, sửa, kiểm thử mã nguồn
- Tích hợp với các công cụ lập trình
- Có thể xây dựng và triển khai ứng dụng

#### 4. **skill-creator** - Tạo Kỹ Năng
- Công cụ để tạo và quản lý kỹ năng mới
- Đóng gói chức năng thành kỹ năng tái sử dụng
- Quản lý tài nguyên và tài liệu đi kèm

## Cách Sử Dụng Công Cụ & Kỹ Năng

### Trong Cuộc Trò Chuyện

Tác nhân AI có thể sử dụng công cụ khi cần:
```
[Using tool: web_fetch to get content from https://example.com]
```

### Cấu Hình Công Cụ

Công cụ được cấu hình trong tệp `~/.openclaw/openclaw.json`:
```json
{
  "tools": {
    "exec": {
      "security": "allowlist",
      "allow": ["ls", "cat", "echo"]
    },
    "web_fetch": {
      "maxSize": 1000000
    }
  }
}
```

### Cài Đặt Kỹ Năng

Kỹ năng có thể được cài đặt qua lệnh:
```
openclaw skills install <skill-name>
```

## An Toàn & Bảo Mật

### Mô Phỏng (Sandboxing)
- Công cụ chạy trong môi trường cô lập
- Giới hạn quyền truy cập hệ thống
- Ngăn chặn hành vi độc hại

### Kiểm Duyệt
- Tất cả hành động công cụ được ghi nhật ký
- Có thể giám sát và kiểm tra
- Cảnh báo khi phát hiện hành vi bất thường

### Phân Quyền
- Không phải công cụ nào cũng có quyền cao
- Một số yêu cầu xác thực đặc biệt
- Có thể tùy chỉnh theo nhu cầu

## Ví Dụ Thực Tế

### Trường Hợp 1: Phân Tích Website
1. Tác nhân AI nhận yêu cầu phân tích một website
2. Sử dụng `web_fetch` để lấy nội dung
3. Sử dụng `edit` để ghi báo cáo phân tích
4. Sử dụng `message` để gửi kết quả

### Trường Hợp 2: Tự Động Hóa Công Việc
1. Tác nhân AI kiểm tra thư mục công việc hàng ngày
2. Sử dụng `read` để đọc các tệp công việc
3. Sử dụng `exec` để chạy script xử lý
4. Sử dụng `write` để cập nhật nhật ký

### Trường Hợp 3: Tương Tác Với Người Dùng
1. Người dùng gửi yêu cầu qua WhatsApp
2. Tác nhân AI sử dụng `browser` để tìm thông tin
3. Sử dụng `image` để phân tích hình ảnh người dùng gửi
4. Gửi phản hồi qua `message`

## Mẹo Sử Dụng

💡 **Hiểu rõ công cụ**: Mỗi công cụ có mục đích riêng, không nên lạm dụng

💡 **Kiểm tra an toàn**: Luôn kiểm tra hành vi công cụ trong môi trường an toàn

💡 **Tùy chỉnh phù hợp**: Có thể cấu hình công cụ theo nhu cầu sử dụng

💡 **Theo dõi hoạt động**: Giám sát nhật ký để đảm bảo hoạt động đúng cách

💡 **Bảo mật đầu tiên**: Không cấp quyền cao nếu không thực sự cần thiết

## Kết Luận

Công cụ và kỹ năng là nền tảng cho khả năng thực hiện tác vụ của tác nhân AI trong OpenClaw. Việc hiểu rõ và sử dụng đúng cách các thành phần này sẽ giúp bạn tận dụng tối đa sức mạnh của hệ thống.

---

**Ghi chú**: Đây là tài liệu hướng dẫn, không phải tài liệu tham khảo đầy đủ. Để biết thông tin chi tiết về từng công cụ, vui lòng tham khảo tài liệu chính thức.