# Đóng Góp Cho Dự Án Tài Liệu OpenClaw Tiếng Việt

Cảm ơn bạn đã quan tâm đến việc đóng góp cho dự án! Mọi sự đóng góp đều được trân trọng và giúp dự án ngày càng hoàn thiện hơn.

## Cách Đóng Góp

### 1. Báo cáo lỗi hoặc vấn đề

Nếu bạn tìm thấy lỗi sai trong nội dung, lỗi chính tả, hoặc vấn đề kỹ thuật:

1. [Tạo issue mới](https://github.com/yourusername/openclaw-docs-vi/issues/new)
2. Mô tả chi tiết vấn đề bạn gặp phải
3. Nếu có thể, đề xuất cách sửa

### 2. Gửi cải thiện nội dung

Nếu bạn muốn cải thiện nội dung tài liệu:

1. Fork repository này
2. Tạo branch mới với tên mô tả thay đổi của bạn
3. Commit thay đổi của bạn
4. Push lên branch của bạn
5. Tạo Pull Request

### 3. Viết tài liệu mới

Nếu bạn muốn viết thêm phần tài liệu chưa có:

1. Xem [cấu trúc hiện tại](./README.md#cấu-trúc-tài-liệu)
2. Đảm bảo nội dung phù hợp với phong cách của dự án
3. Gửi Pull Request như trên

## Hướng Dẫn Viết Tài Liệu

### Ngôn Ngữ

- Sử dụng tiếng Việt chuẩn, dễ hiểu
- Tránh thuật ngữ kỹ thuật phức tạp nếu không cần thiết
- Nếu phải dùng thuật ngữ chuyên môn, giải thích ngắn gọn

### Định Dạng

Tài liệu sử dụng Markdown và được xử lý bởi Jekyll:

```markdown
---
layout: default
title: "Tên Trang"
nav_exclude: true
---

# Tiêu đề chính

## Tiêu đề phụ

Nội dung ở đây...

**In đậm** để nhấn mạnh
*In nghiêng* để làm nổi bật
`mã` cho tên lệnh hoặc biến
```

### Cấu Trúc Đề Xuất

Khi viết tài liệu mới, cố gắng bao gồm:

1. **Tổng quan**: Giới thiệu ngắn gọn về chủ đề
2. **Cài đặt/Hướng dẫn**: Các bước cụ thể để thực hiện
3. **Ví dụ**: Ví dụ thực tế minh họa
4. **Mẹo & Lưu ý**: Gợi ý cho người dùng
5. **Kết luận**: Tóm tắt hoặc hướng dẫn tiếp theo

## Phong Cách Viết

### Giọng Văn

- Thân thiện, dễ hiểu
- Sử dụng "bạn" thay vì "người dùng"
- Giải thích như đang hướng dẫn một người bạn

### Cấu Trúc

- Đầu tiên là khái niệm tổng quát
- Sau đó là hướng dẫn cụ thể
- Cuối cùng là mẹo và lưu ý

### Ví Dụ

**Tốt**: "Bạn có thể chạy lệnh sau để kiểm tra trạng thái: `openclaw status`"

**Chưa tốt**: "Lệnh `openclaw status` được sử dụng để kiểm tra trạng thái hệ thống"

## Các Loại Đóng Góp Được Hoan Nghênh

- **Sửa lỗi sai**: Chính tả, ngữ pháp, nội dung sai
- **Cải thiện rõ ràng**: Làm rõ nội dung khó hiểu
- **Thêm ví dụ**: Ví dụ thực tế giúp hiểu nhanh hơn
- **Dịch thêm**: Dịch các phần chưa được dịch
- **Cập nhật nội dung**: Cập nhật theo phiên bản mới của OpenClaw
- **Tạo tài liệu mới**: Viết phần tài liệu chưa có
- **Cải thiện trải nghiệm**: Cải thiện định dạng, cấu trúc, điều hướng

## Quy Trình Xét Duyệt

1. **Pull Request được tạo**: Bạn gửi yêu cầu đóng góp
2. **Xét duyệt ban đầu**: Kiểm tra định dạng, nội dung cơ bản
3. **Phản hồi**: Nhận phản hồi và đề xuất cải thiện
4. **Sửa đổi**: Cập nhật theo phản hồi (nếu cần)
5. **Chấp nhận**: Merge vào nhánh chính

## Công Cụ Hỗ Trợ

### Kiểm Tra Cú Pháp

Bạn có thể kiểm tra cú pháp Markdown trước khi gửi:

```bash
# Cài đặt công cụ kiểm tra
npm install -g markdownlint-cli

# Kiểm tra tất cả tệp markdown
markdownlint .
```

### Xem Trước Địa Phương

Bạn có thể chạy bản xem trước địa phương:

```bash
# Cài đặt Jekyll (nếu chưa có)
gem install bundler jekyll

# Chạy máy chủ địa phương
bundle exec jekyll serve
```

Truy cập [http://localhost:4000](http://localhost:4000) để xem bản xem trước.

## Ghi Công

Tất cả người đóng góp sẽ được ghi công trong:

- [README.md](./README.md)
- Các commit tương ứng
- Các bản cập nhật tài liệu

## Liên Hệ

Nếu bạn có câu hỏi về cách đóng góp:

- Gửi issue trên GitHub
- Gửi email theo địa chỉ trong [README.md](./README.md)
- Tham gia các cuộc thảo luận liên quan

## Giấy Phép

Khi bạn đóng góp cho dự án, bạn đồng ý rằng đóng góp của mình sẽ được phân phối theo cùng giấy phép với dự án (MIT).

---

💡 **Cảm ơn bạn đã đóng góp!** Mọi sự đóng góp dù nhỏ cũng giúp dự án ngày càng hoàn thiện hơn.