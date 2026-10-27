# Bước 2 — Xác định Use Case Chính & Macro Diagram

**Mục tiêu:** Từ danh sách chức năng con, nhóm thành 3–6 Use Case Chính và vẽ Macro Use Case Diagram.

## Tiêu chí phân rã Use Case Chính (bắt buộc đáp ứng cả 3)

1. **Đủ lớn & Độc lập:** Đại diện cho một mục tiêu nghiệp vụ trọn vẹn (User Goal) của người dùng hoặc hệ thống.
2. **Có tương tác giao diện trực tiếp:** Bắt đầu bằng hành động chủ động của Actor trên giao diện (UI), kết thúc khi đạt kết quả mong đợi.
   - *Lưu ý về Actor:* Điểm khởi đầu phải là thao tác chủ động từ UI (ví dụ bấm nút Đăng nhập, gửi Form). Một UC Chính có thể tiếp nhận nhiều loại Actor với kết quả điều phối khác nhau (ví dụ: tại Cổng đăng nhập, `Guest` hợp lệ được vào trang chủ, còn `Banned User` bị điều hướng cô lập sang Màn hình khóa — cả hai vẫn thuộc chung một quy trình nghiệp vụ Đăng nhập).
3. **Bao hàm chức năng con:** Chứa các bước thực hiện mang tính nghiệp vụ bắt buộc hoặc tùy chọn mở rộng (ít nhất 2 chức năng con hoặc 1 quy trình nghiệp vụ nhiều bước phức tạp).

## Quy trình thực hiện

1. Đọc toàn bộ mục 5.x trong FR để nắm rõ hành vi của từng chức năng.
2. Nhóm các chức năng con có cùng "mục tiêu nghiệp vụ hoàn chỉnh" vào một Use Case Chính.
3. **Đặt tên UC Chính bao quát:**
   - Tên UC Chính phải **đủ rộng** để bao quát toàn bộ các con đường/phương thức con bên trong, không lấy tên của một chức năng con đơn lẻ làm tên UC Chính.
   - *Ví dụ sai:* `UC-C01: Đăng ký tài khoản bằng email` (quá hẹp, bỏ sót Google OAuth).
   - *Ví dụ đúng (chuẩn vàng US-M01):* `UC-C01: Đăng ký tài khoản mới (User Registration & Onboarding)` (bao trùm cả 3 bước email, xác minh magic link và đăng ký nhanh qua Google).
   - Format chuẩn: `UC-C01: Tên tiếng Việt (English Name)`.
4. Ghi tiêu chí phân rã và danh sách UC Chính vào **Mục 2.1** của US.
5. Vẽ **Macro Diagram** (Mục 2.2) bằng `flowchart LR`:
   - Actor ở bên trái, các UC Chính trong subgraph ở bên phải.
   - Chỉ hiển thị UC Chính (không vẽ chi tiết UC con ở bước này).
   - Áp dụng classDef `actorStyle` và `coreUC`.

## Lưu ý phân loại quan trọng

- **Tiến trình ngầm (Background Jobs / Daemons):** Cron job, auto-cleanup, token rotation, background sync... do hệ thống tự chạy ngầm, **KHÔNG** phải UC Chính. Chúng sẽ được ghi là `*(Tiến trình ngầm)*` trong ma trận truy vết ở Bước 5.
- **Tầng hiển thị thụ động (Display Logic / Filters):** Các logic kiểm soát hiển thị nội dung, bộ lọc danh sách (ví dụ: ẩn bài viết của tài khoản đã xóa, thay thế tên tác giả) **KHÔNG** phải UC Chính vì người dùng không chủ động thực hiện hành động này. Chúng sẽ được ghi nhận là `*(Tầng hiển thị)*` trong ma trận truy vết.
- **Số lượng UC Chính khuyến nghị:** 3–6 Use Case Chính cho một module.

## Kiểm tra trước khi trình cổng

- [ ] Mỗi UC Chính đáp ứng đủ cả 3 tiêu chí phân rã.
- [ ] Tiến trình ngầm KHÔNG bị nhầm lẫn thành UC Chính.
- [ ] Macro Diagram tuân thủ đúng Quy tắc Mermaid (chuỗi bọc nháy kép, không dùng `\n`).
- [ ] Mọi chức năng con đều có định hướng thuộc ít nhất 1 UC Chính.

## Cổng xác nhận

Gửi tin nhắn theo mẫu trong SKILL.md và chờ.

