# Bước 4 — Phân rã Use Case con & Xác định Quan hệ

**Mục tiêu:** Với mỗi UC Chính, xác định các UC con, phân loại theo 3 quan hệ chuẩn UML (`<<include>>`, `<<extend>>`, `Generalization`), và xây dựng Per-UC Diagram + Bảng quan hệ chi tiết cho Mục 3.

## Quy tắc phân loại 3 quan hệ UML chuẩn (Visual Paradigm / UML Standard)

### 1. Quan hệ `<<include>>` (Bao hàm Bắt buộc / Tiên quyết)
- Dùng khi UC con là **bước bắt buộc phải thực hiện** để UC Chính hoàn thành.
- Nếu thiếu hoặc thất bại ở bước này, toàn bộ UC Chính bị dừng / không thể hoàn tất.
- Chiều mũi tên: Nét đứt từ UC Chính sang UC Con:
  `UC_Chính -.->|"<<include>>"| UC_Con`
- Node styling: `classDef incStyle fill:#e8f5e9,stroke:#2e7d32,stroke-width:1.5px;` (xanh lá).

### 2. Quan hệ `<<extend>>` (Tùy chọn / Mở rộng / Rẽ nhánh / Ngoại lệ)
- Dùng khi UC con thuộc một trong các tình huống nghiệp vụ sau:
  + **Tính năng tùy chọn (Optional):** Bước người dùng có thể làm hoặc bỏ qua mà quy trình chính vẫn hoàn thành (ví dụ: điền Bio, Avatar, Khối lớp ở Bước 3 thiết lập).
  + **Nhánh ngoại lệ / Điều kiện rẽ nhánh (Conditional / Exception):** Chỉ kích hoạt khi thỏa mãn điều kiện nhất định (ví dụ: gửi lại Magic Link khi link cũ hết hạn; màn hình khóa khi tài khoản `BANNED`; yêu cầu Re-consent khi chính sách đổi).
  + **Tương tác mở rộng ngữ cảnh:** Chức năng bổ trợ gắn liền với màn hình nhưng không bắt buộc (ví dụ: nút Nhắn tin 1-1 từ hồ sơ người khác, nút xem chi tiết danh sách follower).
- Chiều mũi tên: Nét đứt từ UC Con sang UC Chính:
  `UC_Con -.->|"<<extend>>"| UC_Chính`
- Node styling: `classDef extStyle fill:#fffde7,stroke:#f57f17,stroke-width:1.5px,stroke-dasharray: 4 4;` (vàng viền đứt).

### 3. Quan hệ `Generalization` (Khái quát hóa / Kế thừa / Quan hệ Cha - Con)
- **Bản chất nghiệp vụ:** Thể hiện quan hệ "là-một-dạng-của" (*is-a-kind-of*). Use Case con là một dạng chuyên biệt hóa (specialization) cụ thể của một Use Case cha tổng quát (generalization).
- **Cơ chế kế thừa:** Use Case con kế thừa toàn bộ mục tiêu của cha, vai trò của Actor, các ràng buộc và quan hệ chung, nhưng cụ thể hóa quy trình nghiệp vụ hoặc cơ chế kỹ thuật thực thi. Khi người dùng thực hiện một trong các Use Case con, họ đồng thời hoàn thành mục tiêu của Use Case cha.
- **Khi nào áp dụng:**
  + Khi một mục tiêu nghiệp vụ có nhiều phương thức thực hiện hoàn toàn khác nhau về luồng xử lý hoặc nguồn xác thực, nhưng cùng mang lại một kết quả cuối cùng.
  + *Ví dụ kinh điển trong Visual Paradigm:*
    - **Cha:** `Đăng nhập hệ thống (User Authentication)`
      + **Con 1:** `Đăng nhập bằng Email & Mật khẩu (Login via Credentials)`
      + **Con 2:** `Đăng nhập bằng Google OAuth (Login via Google OAuth)`
    - **Cha:** `Đăng ký tài khoản mới (User Registration)`
      + **Con 1:** `Đăng ký bằng Email truyền thống (Register via Email Flow)`
      + **Con 2:** `Đăng ký nhanh qua Google OAuth (Register via Google OAuth)`
    - **Cha:** `Tìm kiếm nội dung (Search System)`
      + **Con 1:** `Tìm kiếm bài viết (Search Posts)`
      + **Con 2:** `Tìm kiếm người dùng (Search Users)`
- **Phân biệt rành mạch giữa 3 quan hệ:**
  + `<<include>>`: Con là một *mảnh ghép/bước bắt buộc* bên trong Cha (Cha chứa Con).
  + `<<extend>>`: Con là một *phần mở rộng tùy chọn/ngoại lệ* của Cha (Cha chạy độc lập được mà không cần Con).
  + `Generalization`: Cha là một *khái niệm trừu tượng*, Cha không tự thực thi độc lập được mà bắt buộc phải chạy thông qua một trong các Con chuyên biệt (Con thay thế cho Cha tại thời điểm chạy).
- **Chiều mũi tên:** Mũi tên nét liền trỏ từ Use Case Con (chuyên biệt hóa) về Use Case Cha (tổng quát):
  `UC_Con -->|"<<generalization>>"| UC_Cha`
- **Node styling:** `classDef genStyle fill:#f3e5f5,stroke:#7b1fa2,stroke-width:1.5px;` (màu tím nhạt, nét liền).

---

## Quy ước đặt mã Use Case con

- UC con của `UC-C01` $\to$ `UC-01.1`, `UC-01.2`, `UC-01.3`, ...
- UC con của `UC-C02` $\to$ `UC-02.1`, `UC-02.2`, ...
- Số đầu tiên tương ứng với số thứ tự của UC Chính.

## Xử lý quan hệ giữa mã FR và Use Case con

1. **Một mã FR có thể sinh ra nhiều Use Case con:**
   - Khi một mục trong tài liệu FR mô tả nhiều hành vi (vừa có phần bắt buộc, vừa có phần tùy chọn hoặc xử lý ngoại lệ), hãy tách thành các UC con riêng rẽ với các quan hệ độc lập (`<<include>>`, `<<extend>>`, hoặc `Generalization`).
   - *Ví dụ:* `FR-M01-03` tách thành `UC-01.3: Thiết lập username/display_name` (`<<include>>`) và `UC-01.5: Bổ sung Bio, Avatar` (`<<extend>>`). `FR-M01-05` tách thành 4 UC con.
2. **Một mã FR có thể tham gia vào nhiều UC Chính:**
   - *Ví dụ:* `FR-M01-04` (Google OAuth) vừa là phương thức đăng ký chuyên biệt trong `UC-C01`, vừa là phương thức đăng nhập chuyên biệt trong `UC-C02`.
3. **Chức năng không tạo UC con:**
   - Các chức năng được xác định là `*(Tiến trình ngầm)*` (cron job dọn dẹp, token refresh) hoặc `*(Tầng hiển thị)*` (logic ẩn/hiện nội dung tài khoản bị khóa/xóa) **KHÔNG** tạo Use Case con ở bước này. Chúng sẽ được định danh trực tiếp trong ma trận truy vết ở Bước 5.

## Quy trình thực hiện với từng UC Chính

1. Gom các chức năng con `FR-Mxx-nn` và các quy tắc nghiệp vụ `BR-Mxx-nn` thuộc phạm vi UC Chính này.
2. Tách thành các Use Case con có ranh giới rõ ràng.
3. Xác định đúng quan hệ của từng Use Case con: `<<include>>`, `<<extend>>`, hay `Generalization`.
4. Vẽ sơ đồ phân rã (`flowchart TB`) riêng cho từng UC:
   - Thể hiện Actor liên quan.
   - Thể hiện UC Chính và các UC con trong một subgraph.
   - Đường nối đúng cú pháp:
     + Include: `UC_Chính -.->|"<<include>>"| UC_Con`
     + Extend: `UC_Con -.->|"<<extend>>"| UC_Chính`
     + Generalization: `UC_Con -->|"<<generalization>>"| UC_Chính`
   - Áp dụng đúng classDef màu sắc: `incStyle` (xanh lá), `extStyle` (vàng đứt), `genStyle` (tím liền).
5. Lập bảng quan hệ chi tiết ngay dưới sơ đồ:
   - Cột: `Mã Use Case con | Tên Use Case con | Căn cứ FR/BR | Quan hệ | Điều kiện kích hoạt & Lý do nghiệp vụ`.
   - Cột "Quan hệ" ghi rõ: `<<include>>`, `<<extend>>`, hoặc `Generalization (Kế thừa)`.

## Kiểm tra trước khi trình cổng

- [ ] Phân định rõ ràng giữa `<<include>>`, `<<extend>>`, và `Generalization`, không có sự lẫn lộn.
- [ ] Mũi tên Mermaid đúng chiều chuẩn UML:
  + Include: từ Chính sang Con.
  + Extend: từ Con sang Chính.
  + Generalization: nét liền từ Con chuyên biệt về Cha tổng quát.
- [ ] Nhãn mũi tên và node Mermaid bọc ngoặc kép đầy đủ, không gây lỗi cú pháp parser.
- [ ] Bảng quan hệ có căn cứ FR/BR chính xác.

## Cổng xác nhận

Gửi tin nhắn theo mẫu trong SKILL.md và chờ.
