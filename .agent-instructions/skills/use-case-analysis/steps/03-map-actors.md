# Bước 3 — Ánh xạ Actor & Mô tả Quy trình Nghiệp vụ

**Mục tiêu:** Xác định Actor cho mỗi UC Chính và viết mô tả quy trình nghiệp vụ hoàn chỉnh cho Mục 2.3.

## Cách xác định Actor

1. Đọc **mục 4.2** (Vai trò) trong FR để lấy danh sách Actor chính thức của hệ thống (ví dụ: `Guest`, `User`, `Admin`, `Moderator`, `Banned User`, v.v.).
2. Đọc **mục 4.3** (Ma trận quyền) để xem Actor nào có quyền tương tác thực hiện chức năng.
3. Với mỗi UC Chính: xác định Actor là tác nhân **chủ động khởi đầu** UC (người thao tác trực tiếp trên UI hoặc hệ thống kích hoạt).

## Cách viết Quy trình Nghiệp vụ Hoàn chỉnh

Với mỗi UC Chính, cấu trúc mô tả gồm:
- **Actor chính:** Tên Actor thực hiện UC này (khớp với mục 4.2 của FR).
- **Mục tiêu:** Kết quả nghiệp vụ kỳ vọng khi Use Case kết thúc thành công (1 câu súc tích).
- **Quy trình nghiệp vụ hoàn chỉnh:** Các bước diễn tiến theo trình tự thời gian:
  1. *Khởi đầu:* Actor bắt đầu hành động gì từ màn hình nào.
  2. *Thực hiện & Kiểm tra:* Hệ thống kiểm tra điều kiện gì, xử lý ra sao.
  3. *Phân nhánh (nếu có):* Các nhánh nghiệp vụ chính (dùng *Nhánh 1*, *Nhánh 2*).
  4. *Kết thúc:* Hệ thống phản hồi kết quả gì, cập nhật trạng thái ra sao và đưa người dùng đến đâu.

## Nguyên tắc nghiệp vụ

- Sử dụng đúng thuật ngữ và mã trạng thái chuẩn từ FR (`ACTIVE`, `BANNED`, `PENDING`, `username`, v.v.).
- Không đưa chi tiết cài đặt kỹ thuật (tên bảng CSDL, câu lệnh SQL, tên file mã nguồn).
- Diễn giải logic rõ ràng để bất kỳ ai đọc cũng nắm được trọn vẹn luồng tương tác.

## Kiểm tra trước khi trình cổng

- [ ] Tên Actor chuẩn xác theo mục 4.2 của tài liệu FR.
- [ ] Mỗi UC Chính đều có đầy đủ: Actor chính, Mục tiêu, Quy trình hoàn chỉnh.
- [ ] Luồng quy trình có điểm bắt đầu (Khởi đầu) và điểm kết thúc (Kết thúc) rõ ràng.

## Cổng xác nhận

Gửi tin nhắn theo mẫu trong SKILL.md và chờ.

