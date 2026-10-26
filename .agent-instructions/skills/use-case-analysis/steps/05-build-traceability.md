# Bước 5 — Xây dựng Ma trận Truy vết Toàn bộ Chức năng (FR → UC)

**Mục tiêu:** Xây dựng Mục 4.1 trong tài liệu US, đảm bảo 100% chức năng trong FR được phân định rõ ràng vai trò và liên kết use case.

## Quy trình lập ma trận

1. Liệt kê toàn bộ danh sách chức năng con `FR-Mxx-nn` đã trích xuất từ mục 4.4 của tài liệu FR ở Bước 1.
2. Ánh xạ từng mã `FR-Mxx-nn` vào cấu trúc phân rã Use Case đã thực hiện ở Bước 2 và Bước 4:
   - Thuộc **UC Chính** nào (`UC-C01`, `UC-C02`, ...).
   - Tương ứng với **UC con** nào (`UC-01.1`, `UC-02.3`, ...).
   - Định nghĩa **Vai trò quan hệ**:
     + `<<include>>`: Bắt buộc hoàn thành trong luồng UC Chính.
     + `<<extend>>`: Luồng nhánh, phương thức thay thế hoặc tùy chọn mở rộng.
     + `Tiến trình ngầm`: Chức năng do hệ thống tự động xử lý nền theo lịch trình (cron, batch job, background listener), không phải use case tương tác trực tiếp của người dùng. Để dấu gạch ngang `—` ở cột UC con.
3. Rà soát đảm bảo không có bất kỳ mã FR nào bị bỏ sót (100% Coverage).

## Cấu trúc bảng ma trận truy vết chuẩn (Mục 4.1)

```markdown
| Mã FR | Tên chức năng con | UC Chính liên quan | UC con tương ứng | Vai trò quan hệ |
|:---:|---|:---:|:---:|:---:|
| **FR-Mxx-01** | Đăng ký tài khoản... | UC-C01 | UC-01.1 | `<<include>>` (Bắt buộc) |
| **FR-Mxx-04** | Đăng ký qua OAuth... | UC-C01 | UC-01.4 | `<<extend>>` (Phương thức thay thế) |
| **FR-Mxx-12** | Tự động dọn dẹp... | UC-C04 | — | Tiến trình ngầm (Hệ thống tự thực thi) |
```

## Kiểm tra trước khi trình cổng

- [ ] Tổng số dòng trong bảng khớp chính xác 100% với số lượng mục trong danh sách chức năng FR (mục 4.4).
- [ ] Không có ô trống ở cột "UC Chính liên quan" và "Vai trò quan hệ".
- [ ] Các chức năng nền được đánh dấu chính xác là `Tiến trình ngầm`.

## Cổng xác nhận

Gửi tin nhắn theo mẫu trong SKILL.md và chờ.

