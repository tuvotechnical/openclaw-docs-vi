---
layout: default
title: "Khái Niệm Cốt Lõi"
nav_exclude: true
---

# Khái Niệm Cốt Lõi Của OpenClaw (Dịch Tiếng Việt)

## Tổng Quan

OpenClaw là một hệ thống phức tạp nhưng mạnh mẽ. Để hiểu rõ cách nó hoạt động, bạn cần nắm vững một số khái niệm cốt lõi. Trang này sẽ giải thích các khái niệm quan trọng theo cách dễ hiểu.

## 1. Gateway Là Gì?

Gateway là "cổng kết nối trung tâm" của OpenClaw. Nó đóng vai trò như một cầu nối giữa các kênh truyền thông (như WhatsApp, Telegram, Discord) và các tác nhân AI (AI agents).

**Tưởng tượng như thế này**: Gateway giống như một "tổng đài" - nó nhận cuộc gọi từ nhiều đường dây khác nhau (các kênh), xử lý thông tin, và chuyển cho người phù hợp (tác nhân AI) để xử lý.

### Tính năng chính của Gateway:
- Quản lý các kết nối kênh (WhatsApp, Telegram, v.v.)
- Điều phối các tác nhân AI
- Quản lý phiên làm việc
- Xử lý bảo mật và xác thực

## 2. Tác Nhân AI (AI Agents)

Tác nhân AI là "trí tuệ" thực sự phía sau OpenClaw. Đây là những chương trình thông minh có thể:
- Hiểu và phân tích tin nhắn
- Thực hiện tác vụ trên máy tính
- Tương tác với các công cụ và dịch vụ
- Học hỏi và cải thiện theo thời gian

**So sánh**: Nếu Gateway là tổng đài, thì tác nhân AI là "nhân viên tổng đài" - người thực sự trò chuyện và giúp đỡ người dùng.

## 3. Kênh Truyền Thông (Channels)

Kênh truyền thông là nơi người dùng tương tác với hệ thống OpenClaw:
- **WhatsApp**: Gửi tin nhắn qua WhatsApp
- **Telegram**: Gửi tin nhắn qua Telegram
- **Discord**: Gửi tin nhắn qua Discord
- **iMessage**: Gửi tin nhắn qua iMessage (macOS)

Tất cả các kênh này đều được kết nối thông qua Gateway, tạo nên một hệ thống thống nhất.

## 4. Phiên Làm Việc (Sessions)

Phiên làm việc là "cuộc trò chuyện" giữa người dùng và tác nhân AI. Mỗi phiên:
- Lưu trữ lịch sử trò chuyện
- Giữ trạng thái hiện tại
- Cho phép tiếp tục cuộc trò chuyện sau khi tạm dừng

**Ví dụ**: Khi bạn trò chuyện với bot qua WhatsApp, toàn bộ cuộc trò chuyện được lưu trong một phiên riêng biệt.

## 5. Công Cụ (Tools)

Công cụ là các chức năng mà tác nhân AI có thể sử dụng để thực hiện tác vụ:
- **exec**: Chạy lệnh hệ thống
- **web_fetch**: Lấy nội dung từ web
- **browser**: Điều khiển trình duyệt
- **message**: Gửi tin nhắn
- **file**: Đọc/ghi tệp tin

Các công cụ này giúp tác nhân AI "tương tác" với thế giới thực, không chỉ trả lời câu hỏi.

## 6. Kỹ Năng (Skills)

Kỹ năng là các mô-đun chức năng được đóng gói sẵn để thực hiện các tác vụ chuyên biệt:
- Kết nối với các dịch vụ bên ngoài
- Xử lý dữ liệu đặc biệt
- Tự động hóa quy trình phức tạp

**So sánh**: Nếu công cụ là "dụng cụ", thì kỹ năng là "hướng dẫn sử dụng" cho các công cụ đó.

## 7. Mô Hình Ngôn Ngữ (Language Models)

OpenClaw có thể sử dụng nhiều loại mô hình ngôn ngữ khác nhau:
- **OpenAI**: GPT-4, GPT-4 Turbo, v.v.
- **Anthropic**: Claude 3, Claude 3.5 Sonnet
- **Mô hình cục bộ**: Các mô hình được chạy trên máy tính của bạn
- **Các nhà cung cấp khác**: Nhiều lựa chọn khác nhau

Mô hình ngôn ngữ là "bộ não" giúp tác nhân AI hiểu và tạo ra ngôn ngữ con người.

## 8. Cấu Hình (Configuration)

Tất cả hành vi của OpenClaw được điều khiển thông qua tệp cấu hình:
- Vị trí: `~/.openclaw/openclaw.json`
- Định dạng: JSON
- Có thể thay đổi để tùy chỉnh hành vi

Cấu hình bao gồm:
- Cài đặt kênh
- Cài đặt tác nhân
- Cài đặt bảo mật
- Cài đặt công cụ

## 9. Bảo Mật

OpenClaw có nhiều lớp bảo mật:
- **Xác thực**: Đảm bảo chỉ người được phép mới sử dụng
- **Phân quyền**: Giới hạn những gì tác nhân AI có thể làm
- **Mô phỏng**: Chạy các tác vụ trong môi trường an toàn
- **Ghé nối**: Kiểm soát ai có thể tương tác với hệ thống

## 10. Tự Động Hóa và Lập Lịch

OpenClaw hỗ trợ tự động hóa thông qua:
- **Cron jobs**: Lập lịch thực hiện tác vụ
- **Webhooks**: Phản ứng với sự kiện bên ngoài
- **Heartbeat**: Kiểm tra định kỳ

## Ví Dụ Thực Tế

Hãy tưởng tượng bạn có một trợ lý AI cá nhân:

1. **Bạn gửi tin nhắn** qua WhatsApp
2. **Gateway nhận tin nhắn** và chuyển cho tác nhân AI phù hợp
3. **Tác nhân AI phân tích** và quyết định hành động
4. **Sử dụng công cụ** nếu cần (như tìm kiếm web, đọc tệp tin)
5. **Trả lời bạn** qua cùng kênh WhatsApp
6. **Lưu phiên làm việc** để tiếp tục sau

Toàn bộ quá trình này được quản lý bởi các khái niệm cốt lõi đã nêu trên.

## Mẹo Cho Người Mới

💡 **Hiểu rõ các khái niệm này** sẽ giúp bạn thiết lập và sử dụng OpenClaw hiệu quả hơn

💡 **Bắt đầu từ đơn giản**: Không cần hiểu hết mọi thứ ngay lập tức

💡 **Thử nghiệm an toàn**: Luôn kiểm tra trong môi trường an toàn trước khi triển khai

💡 **Tận dụng cộng đồng**: Có nhiều tài nguyên và hỗ trợ từ cộng đồng người dùng

---

## Các Khái Niệm Nâng Cao

- [Đa tác nhân](multi-agent.md): Sử dụng nhiều tác nhân riêng biệt
- [Mô phỏng an toàn](sandboxing.md): Chạy tác nhân trong môi trường an toàn
- [Định tuyến kênh](channel-routing.md): Điều hướng tin nhắn giữa các kênh
- [Quản lý phiên](session-management.md): Quản lý các cuộc trò chuyện
- [Tích hợp OAuth](oauth.md): Xác thực an toàn với các dịch vụ