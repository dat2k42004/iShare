# Bước 3 — Ánh xạ Actor & Mô tả Quy trình Nghiệp vụ

**Mục tiêu:** Xác định Actor cho mỗi UC Chính và viết mô tả quy trình nghiệp vụ hoàn chỉnh cho Mục 2.3.

## Cách xác định Actor

1. Đọc **mục 4.2** (Vai trò) trong FR để lấy danh sách Actor chính thức của hệ thống (ví dụ: `Guest`, `User`, `Admin`, `Moderator`, `Banned User`, v.v.).
2. Đọc **mục 4.3** (Ma trận quyền) để xem Actor nào có quyền tương tác thực hiện chức năng.
3. Với mỗi UC Chính: xác định Actor là tác nhân **chủ động khởi đầu** UC (người thao tác trực tiếp trên UI hoặc hệ thống kích hoạt).
4. **Xử lý UC Chính có nhiều Actor khác nhau theo từng nhánh nghiệp vụ:**
   - Trong một UC Chính đủ lớn, có thể có nhiều Actor tham gia vào các nhánh nghiệp vụ khác nhau. Phải ghi rõ Actor gắn liền với bối cảnh/nhánh cụ thể.
   - *Ví dụ chuẩn vàng US-M01:*
     + `UC-C02` (Đăng nhập): Actor gồm `Guest` (người chưa vào phiên) và `Banned User` (chủ tài khoản bị khóa đăng nhập để thấy màn hình vi phạm).
     + `UC-C03` (Quản lý & Khôi phục MK): `User` (cho nhánh Đổi mật khẩu chủ động khi đang trong phiên), `Guest` / `Banned User` (cho nhánh Quên mật khẩu khi ở ngoài màn hình đăng nhập).
     + `UC-C04` (Vòng đời tài khoản): `User` (khi chủ động Vô hiệu hóa tài khoản), `Guest` (chủ tài khoản đã bị vô hiệu hóa truy cập trang kích hoạt lại bằng OTP).

## Cách viết Quy trình Nghiệp vụ Hoàn chỉnh

Với mỗi UC Chính, cấu trúc mô tả gồm:
- **Actor chính:** Tên (các) Actor thực hiện UC này kèm ngữ cảnh nhánh (khớp với mục 4.2 của FR).
- **Mục tiêu:** Kết quả nghiệp vụ kỳ vọng khi Use Case kết thúc thành công (1 câu súc tích).
- **Quy trình nghiệp vụ hoàn chỉnh:** Áp dụng 1 trong 2 cấu trúc phù hợp:

  ### Kiểu A: Quy trình tuần tự từng bước (Linear Flow)
  Dùng cho các UC là chuỗi bước nối tiếp nhau từ đầu đến cuối (ví dụ Đăng ký, Nhắc tên `@mention`):
  1. *Khởi đầu:* Actor bắt đầu hành động gì từ màn hình nào.
  2. *Thực hiện bước đầu:* Nhập thông tin, gửi yêu cầu.
  3. *Xác thực / Xử lý:* Hệ thống kiểm tra điều kiện, phản hồi trung gian.
  4. *Kết thúc:* Hệ thống hoàn tất nghiệp vụ, cập nhật trạng thái và chuyển hướng.

  ### Kiểu B: Quy trình phân nhánh song song (Branching / Parallel Journeys)
  Dùng cho các UC bao hàm các con đường nghiệp vụ độc lập để đạt mục tiêu lớn (ví dụ Quản lý mật khẩu, Vòng đời tài khoản):
  - *Nhánh 1 — [Tên hành trình 1]:* Điều kiện kích hoạt $\to$ Các bước tương tác của Actor $\to$ Xử lý của hệ thống $\to$ Kết quả đạt được.
  - *Nhánh 2 — [Tên hành trình 2]:* Điều kiện kích hoạt $\to$ Các bước tương tác của Actor $\to$ Xử lý của hệ thống $\to$ Kết quả đạt được.

## Nguyên tắc nghiệp vụ

- Sử dụng đúng thuật ngữ và mã trạng thái chuẩn từ FR (`ACTIVE`, `BANNED`, `PENDING`, `username`, v.v.).
- Không đưa chi tiết cài đặt kỹ thuật (tên bảng CSDL, câu lệnh SQL, tên file mã nguồn).
- Diễn giải logic rõ ràng để bất kỳ ai đọc cũng nắm được trọn vẹn luồng tương tác.

## Kiểm tra trước khi trình cổng

- [ ] Tên Actor chuẩn xác theo mục 4.2 của tài liệu FR, nêu rõ vai trò từng Actor nếu có nhiều nhánh.
- [ ] Mỗi UC Chính đều có đầy đủ: Actor chính, Mục tiêu, Quy trình hoàn chỉnh (theo Kiểu A tuần tự hoặc Kiểu B phân nhánh).
- [ ] Luồng quy trình có điểm bắt đầu và kết quả kết thúc rõ ràng cho mọi nhánh.

## Cổng xác nhận

Gửi tin nhắn theo mẫu trong SKILL.md và chờ.

