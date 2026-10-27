# Bước 6 — Xây dựng Sơ đồ Use Case Chi tiết Toàn Module

**Mục tiêu:** Tổng hợp toàn bộ các Actor, UC Chính và UC con của module thành một sơ đồ Mermaid duy nhất hoàn chỉnh và trực quan cho Mục 4.2.

## Quy tắc kỹ thuật Mermaid (Bắt buộc tuân thủ 100%)

1. Dùng `flowchart TB` để các nhóm chức năng được bố trí mạch lạc theo chiều dọc từ trên xuống dưới.
2. Mỗi Use Case Chính tạo thành một `subgraph` độc lập:
   - Đặt tên subgraph rõ ràng: `subgraph UCC01 ["UC-C01: Tên UC Chính"]`.
   - Thiết lập `direction TB` bên trong subgraph.
   - Bên trong chứa: Node UC Chính, các Node UC con Include, Extend và Generalization tương ứng.
3. **Quy tắc định danh Node ID:**
   - Phải là **DUY NHẤT (Unique)** trong toàn bộ sơ đồ.
   - Đặt prefix theo mã UC và loại quan hệ để tránh xung đột, ví dụ:
     + `INC_C01_1`, `INC_C01_2` (Include)
     + `EXT_C01_1`, `EXT_C01_2` (Extend)
     + `GEN_C01_1`, `GEN_C01_2` (Generalization)
     + `INC_C02_1`, `EXT_C02_1`, `GEN_C02_1`
4. **Quy tắc nhãn và chuỗi ký tự (Tuyệt đối không gây lỗi parse):**
   - Mọi nhãn mũi tên chứa ký tự đặc biệt như `<`, `>` PHẢI được bọc trong cặp dấu nháy kép:
     + Include: `UC_C01 -.->|"<<include>>"| INC_C01_1`
     + Extend: `EXT_C01_1 -.->|"<<extend>>"| UC_C01`
     + Generalization: `GEN_C01_1 -->|"<<generalization>>"| UC_C01` (mũi tên nét liền trỏ từ con về cha)
   - Node label có chứa dấu ngoặc đơn `()`, dấu phẩy, khoảng trắng hoặc ký tự xuống dòng PHẢI được bọc trong chuỗi kép:
     `INC_C01_1(["UC-01.1: Nhập thông tin & Cam kết<br/>[FR-Mxx-01]"])`
   - Tuyệt đối **KHÔNG** dùng ký tự `\n` trong nhãn mũi tên hay label node. Thay vào đó, dùng thẻ `<br/>` bên trong label node.
   - Tuyệt đối **KHÔNG** dùng thẻ HTML in đậm `<b>` hay `<i>` trong label node để tránh xung đột parser Mermaid.
   - Tuyệt đối **KHÔNG** dùng dấu ngoặc nhọn kép `{{` hoặc `}}` làm placeholder bên trong code block Mermaid vì parser Mermaid nhận diện đó là toán tử tạo hình Hexagon/Diamond (`DIAMOND_START`). Khi cần placeholder trong sơ đồ, chỉ dùng định danh hợp lệ như `Actor1`, `Mxx_Core`.
5. **Class định kiểu chuẩn:**
   ```mermaid
   classDef actorStyle fill:#ffffff,stroke:#333333,stroke-width:2px;
   classDef coreUC fill:#e1f5fe,stroke:#0288d1,stroke-width:2px,font-weight:bold;
   classDef incStyle fill:#e8f5e9,stroke:#2e7d32,stroke-width:1.5px;
   classDef extStyle fill:#fffde7,stroke:#f57f17,stroke-width:1.5px,stroke-dasharray: 4 4;
   classDef genStyle fill:#f3e5f5,stroke:#7b1fa2,stroke-width:1.5px;
   ```

## Kiểm tra trước khi trình cổng

- [ ] Toàn bộ các Actor liên quan đều được khai báo và liên kết đến các UC Chính.
- [ ] Không có node nào bị trùng Node ID.
- [ ] Mọi nhãn mũi tên `<<include>>`, `<<extend>>`, `<<generalization>>` đều được bọc trong chuỗi nháy kép `|"<<...>>"|`.
- [ ] Render thử cú pháp để chắc chắn 100% không phát sinh lỗi parse.

## Cổng xác nhận

Gửi tin nhắn theo mẫu trong SKILL.md và chờ.
