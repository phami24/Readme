## Quy Trình Xử Lý Pull Request

### Tạo Pull Request

1. **Tạo nhánh mới**:
   - Khi bạn bắt đầu làm việc trên một tính năng mới hoặc sửa lỗi, hãy tạo một nhánh mới từ nhánh chính (main hoặc master):
     ```bash
     git checkout -b ten-nhanh-moi
     ```
   - Đặt tên cho nhánh sao cho phản ánh rõ ràng mục đích của nó (ví dụ: `feature/ten-tinh-nang` hoặc `fix/ten-loi`).

2. **Thực hiện thay đổi**:
   - Thực hiện các thay đổi cần thiết trong mã nguồn. Sau khi hoàn tất, commit các thay đổi:
     ```bash
     git add .
     git commit -m "Mô tả ngắn gọn về các thay đổi"
     ```

3. **Đẩy nhánh lên remote**:
   - Đẩy nhánh vừa tạo lên repository trên GitHub:
     ```bash
     git push origin ten-nhanh-moi
     ```

4. **Tạo Pull Request**:
   - Truy cập vào trang GitHub của repository và bạn sẽ thấy một thông báo cho phép bạn tạo Pull Request cho nhánh vừa đẩy lên.
   - Nhấn vào nút "Compare & pull request".
   - Mô tả chi tiết về các thay đổi bạn đã thực hiện, giải thích lý do cho các thay đổi và chỉ định người xem xét nếu cần thiết.

### Ai sẽ thực hiện merge?

- **Người có quyền merge**: Pull Request sẽ được xem xét và thực hiện merge bởi các thành viên có quyền quản lý repository, thường là:
  - Maintainers của dự án
  - Quản lý dự án hoặc các thành viên có kinh nghiệm trong nhóm

- **Quy trình xem xét**:
  - Các thành viên được chỉ định sẽ xem xét mã, thực hiện kiểm tra, và đưa ra nhận xét. Nếu có yêu cầu thay đổi, bạn cần thực hiện các thay đổi cần thiết và cập nhật Pull Request.

- **Thực hiện merge**:
  - Khi Pull Request được chấp nhận, người có quyền merge sẽ thực hiện thao tác merge để kết hợp các thay đổi vào nhánh chính.
  - Nếu có xung đột giữa nhánh Pull Request và nhánh chính, người merge sẽ cần giải quyết các xung đột này trước khi thực hiện merge.

### Lưu ý

- **Kiểm tra tự động**: Nếu dự án sử dụng CI/CD, các bài kiểm tra sẽ tự động chạy khi có Pull Request được tạo ra để đảm bảo không có lỗi phát sinh.
- **Đóng Pull Request**: Nếu không muốn tiếp tục, bạn có thể đóng Pull Request mà không cần merge.
