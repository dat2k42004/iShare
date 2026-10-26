# Bước 4 — Phân rã Use Case con & Xác định Quan hệ

**Mục tiêu:** Với mỗi UC Chính, xác định các UC con, phân loại quan hệ `<<include>>` hoặc `<<extend>>`, và xây dựng Per-UC Diagram + Bảng quan hệ chi tiết cho Mục 3.

## Quy tắc phân loại quan hệ UML chuẩn

### 1. Quan hệ `<<include>>` (Bắt buộc / Tiên quyết)
- Dùng khi UC con là **bước bắt buộc phải thực hiện** để UC Chính hoàn thành.
- Nếu thiếu hoặc thất bại ở bước này, toàn bộ UC Chính bị dừng / không thể hoàn tất.
- Chiều mũi tên: `UC_Chính -.->|"<<include>>"| UC_Con`.

### 2. Quan hệ `<<extend>>` (Tùy chọn / Mở rộng / Rẽ nhánh)
- Dùng khi UC con là:
  + Phương thức thay thế (alternative path, ví dụ: đăng nhập OAuth thay vì mật khẩu).
  + Tính năng tùy chọn bổ sung (optional, ví dụ: điền thêm Bio/Avatar có thể bấm Bỏ qua).
  + Nhánh ngoại lệ hoặc điều kiện rẽ nhánh đặc thù (conditional branch, ví dụ: gửi lại mã khi hết hạn).
  + Màn hình thông báo / xử phạt phụ thuộc vào điều kiện kích hoạt.
- Chiều mũi tên: `UC_Con -.->|"<<extend>>"| UC_Chính`.

## Quy ước đặt mã Use Case con

- UC con của `UC-C01` $\to$ `UC-01.1`, `UC-01.2`, `UC-01.3`, ...
- UC con của `UC-C02` $\to$ `UC-02.1`, `UC-02.2`, ...
- Số đầu tiên tương ứng với số thứ tự của UC Chính.

## Quy trình thực hiện với từng UC Chính

1. Gom các chức năng con `FR-Mxx-nn` và các quy tắc nghiệp vụ `BR-Mxx-nn` thuộc phạm vi UC Chính này.
2. Tách thành các Use Case con có ranh giới rõ ràng.
3. Vẽ sơ đồ phân rã (`flowchart TB`) riêng cho từng UC:
   - Thể hiện Actor liên quan.
   - Thể hiện UC Chính và các UC con trong một subgraph.
   - Các cạnh `<<include>>` và `<<extend>>` có nhãn đặt trong chuỗi nháy kép: `|"<<include>>"|` và `|"<<extend>>"|`.
   - Node styling: Include dùng `fill:#e8f5e9,stroke:#2e7d32` (xanh lá); Extend dùng `fill:#fffde7,stroke:#f57f17,stroke-dasharray: 4 4` (vàng đứt đoạn).
4. Lập bảng quan hệ chi tiết ngay dưới sơ đồ:
   - Cột: `Mã Use Case con | Tên Use Case con | Căn cứ FR/BR | Quan hệ | Điều kiện kích hoạt & Lý do nghiệp vụ`.
   - Lý do nghiệp vụ phải nêu rõ: vì sao bắt buộc (với include) hoặc điều kiện nào kích hoạt (với extend).

## Kiểm tra trước khi trình cổng

- [ ] Phân định rõ ràng `<<include>>` và `<<extend>>`, không có Use Case con nào bị gán lẫn lộn cả hai.
- [ ] Mũi tên Mermaid đúng chiều chuẩn UML (Include từ Chính sang Con; Extend từ Con về Chính).
- [ ] Nhãn mũi tên và node Mermaid bọc ngoặc kép đầy đủ, không gây lỗi cú pháp parser.
- [ ] Bảng quan hệ có căn cứ FR/BR chính xác.

## Cổng xác nhận

Gửi tin nhắn theo mẫu trong SKILL.md và chờ.

