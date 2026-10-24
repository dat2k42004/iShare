---
module: M13
ten_module: AI Layer
ma_tai_lieu: FR-M13
phien_ban: 1.2
trang_thai: Đã chốt
ngay: 2026-10-24
tac_gia: Phạm Văn Đức
moc_nguon: DEC-207, QA-392, ISS-332, OPEN-012
steps_completed: [1, 2, 3, 4, 5, 6, 7]
---
# Tài liệu yêu cầu chức năng — M13 AI Layer

| Mã tài liệu | FR-M13 |
|---|---|
| Dự án | iShare |
| Module | M13 — AI Layer |
| Trạng thái | Đã chốt |
| Phiên bản | 1.2 |
| Ngày | 2026-10-24 |
| Tác giả | Phạm Văn Đức |

<!-- Quy ước chung cho mọi bảng dưới đây:
     - Thân tài liệu không ghi nguồn. Nguồn của mọi ID nằm ở Phụ lục A.
     - Ô không có nội dung ghi "—". Không xóa cột.
     - Mục chưa tới bước làm thì để dòng "(Chưa làm — bước N)". -->

## 1. Tổng quan

### 1.1 Mục đích

M13 là lớp AI hỗ trợ dùng chung của iShare: gọi dịch vụ AI của bên thứ ba để chấm điểm kiểm duyệt bài viết và
bình luận, tạo embedding cho tìm kiếm ngữ nghĩa, lấy gợi ý Topic và tóm tắt bài viết dài khi người dùng yêu cầu;
ghi lại quyết định của AI và đo chất lượng gợi ý Topic theo thời gian. AI chỉ hỗ trợ: con người quyết định cuối cùng
với trường hợp không ở khoảng điểm cao, và phần lõi vẫn hoạt động khi AI bị tắt hoặc gặp lỗi.

### 1.2 Phạm vi

**Trong phạm vi:**

- Gọi dịch vụ AI cho các module khác: công tắc, thời gian chờ, một lần thử lại, phân biệt AI bị tắt chủ đích với AI
  lỗi tạm thời.
- Chấm điểm kiểm duyệt bài viết (tiêu đề, nội dung chữ, bình chọn, ảnh) và bình luận theo bốn nhóm vi phạm; cặp
  ngưỡng dùng chung 0,9 / 0,5 (giá trị tạm) cho hai nhánh cổng nội dung và cảnh cáo.
- Embedding bài viết: tạo khi bài Đã đăng, tạo lại khi tiêu đề hoặc nội dung chữ thay đổi, tạo bù cho bài còn
  thiếu; embedding truy vấn cho tìm kiếm ngữ nghĩa. Chỉ cho bài, không cho bình luận.
- Thực hiện lời gọi AI cho gợi ý Topic.
- Tóm tắt bài viết từ 300 từ khi người dùng đã đăng nhập yêu cầu; kết quả giữ tạm 24 giờ, dùng chung.
- Nhật ký quyết định AI: một bản ghi cho mỗi lời gọi chấm điểm, embedding bài, gợi ý Topic, kể cả lời gọi thất bại;
  giữ vĩnh viễn, không sửa; Mod, Admin xem khi xét khiếu nại.
- Đánh giá chất lượng gợi ý Topic: tỷ lệ Topic gợi ý được giữ lại, cung cấp cho trang thống kê của Admin.
- Nguyên tắc chung của lớp AI: chỉ hỗ trợ; chạy thật với mỗi thao tác mới; phần lõi không phụ thuộc cứng vào AI.

**Ngoài phạm vi:**

- Công tắc AI tổng và công tắc riêng cho Search, Moderation, Topic suggestion — M10 Admin Panel.
- Khi nào quét nội dung (quét trước khi đăng, quét lại khi sửa, khi hiện lại bài tự ẩn) và hệ quả với bài viết
  theo điểm quét — M03 Post & Content.
- Quét luồng bình luận theo tốc độ trả lời, hệ quả với bình luận, cảnh cáo do AI, hàng chờ vụ do AI tạo —
  M08 Moderation (hiển thị bình luận bị ẩn — M04 Comment).
- Bài trong nhóm qua AI rồi tới cổng duyệt của nhóm — M11 Group.
- Gợi ý Topic phía người dùng: nút gợi ý, tối đa 3 Topic, ngưỡng 20 từ, đối chiếu danh mục Topic, giới hạn
  10 lần / 60 giây, ghi phản hồi gợi ý — M05 Topic & Tag.
- Tìm kiếm ngữ nghĩa, xếp hạng kết quả, tìm full-text khi tắt AI hoặc khi AI lỗi — M06 Search.
- Trang thống kê hiển thị chỉ số chất lượng gợi ý Topic — M15 Analytics & Stats.
- Trang chính sách công bố nội dung được nhà cung cấp dịch vụ AI xử lý — M01 Authentication & Account.
- Xét khiếu nại dựa trên nhật ký quyết định AI — M09 Appeal.
- Đã quyết là không làm: đánh giá chất lượng AI kiểm duyệt và thao tác đánh dấu dự đoán AI đúng, sai; tra cứu nhật
  ký AI ngoài lúc xét khiếu nại; tóm tắt tự động, lưu tóm tắt lâu dài, tóm tắt luồng bình luận, tóm tắt cho Guest;
  gửi tài liệu đính kèm cho AI; AI gợi ý Tag; AI quét tin nhắn chat; AI tự viết bài, bình luận; AI tự quyết điểm,
  badge, Accepted Answer; AI tự ban; chatbot, RAG phức tạp, multi-agent; train, fine-tune mô hình riêng; Related
  Posts; feed cá nhân hóa bằng AI; embedding cho bình luận; hệ thống giới hạn tần suất riêng cho AI.

## 2. Thuật ngữ và viết tắt

### 2.1 Thuật ngữ

| Thuật ngữ | Định nghĩa |
|---|---|
| Lớp AI (AI Layer) | Tập năm năng lực AI bắt buộc của iShare, gọi dịch vụ AI của bên thứ ba để hỗ trợ chứ không thay quyết định của con người. |
| Dịch vụ AI | Dịch vụ của nhà cung cấp AI bên ngoài mà iShare gửi nội dung tới và nhận kết quả về (chấm điểm kiểm duyệt, embedding, gợi ý Topic, tóm tắt). |
| Lời gọi AI | Một yêu cầu của một module tới dịch vụ AI, gồm lần thử đầu và lần thử lại nếu có. |
| Lần thử | Một lần gửi yêu cầu tới dịch vụ AI trong một lời gọi AI. Một lời gọi có tối đa hai lần thử. |
| Thời gian chờ | Thời gian tối đa, tính bằng giây, từ lúc một lần thử được gửi tới lúc có kết quả. Hết thời gian chờ mà chưa có kết quả thì lần thử đó bị tính là lỗi. |
| Công tắc AI tổng | Công tắc ở cấu hình hệ thống (M10) bật hoặc tắt toàn bộ lớp AI. |
| Công tắc AI riêng | Ba công tắc ở cấu hình hệ thống (M10): Search, Moderation, Topic suggestion. Chỉ có tác dụng khi công tắc tổng bật. Tóm tắt không có công tắc riêng. |
| AI tắt | Tình trạng do Admin chủ động tắt công tắc tổng hoặc công tắc riêng; module dùng cách làm thay thế đã định. |
| AI lỗi tạm thời | Lời gọi AI không có kết quả (lỗi hoặc hết thời gian chờ ở cả hai lần thử) trong lúc AI đang bật. Chỉ ảnh hưởng yêu cầu đó, không làm AI chuyển sang tắt. |
| Nhóm vi phạm | Một trong bốn nhóm AI kiểm duyệt chấm điểm, theo thứ tự: Quấy rối, Ngôn từ thù ghét, Nội dung người lớn, Bạo lực. |
| Điểm quét | Điểm cao nhất trong bốn điểm nhóm vi phạm của một bài viết hoặc bình luận, từ 0 đến 1. |
| Khoảng điểm | Ba khoảng theo cặp ngưỡng: cao (≥ 0,9), nghi ngờ (0,5 đến < 0,9), sạch (< 0,5). |
| Embedding | Biểu diễn ý nghĩa nội dung của một bài viết hoặc một truy vấn, dùng để tìm bài theo ngữ nghĩa (M06). |
| Gửi bài, Đã đăng | Theo FR-M03: "gửi" là lúc tác giả nộp bài để đăng; "Đã đăng" là lúc bài qua bước quét, được Mod duyệt, hoặc được đăng thẳng (AI tắt, bài của Admin). |
| Hàng chờ tạo bù embedding | Danh sách các bài Đã đăng đang thiếu embedding theo nội dung hiện tại (do công tắc tắt hoặc lời gọi thất bại), chờ được tạo embedding khi AI dùng được trở lại. |
| Từ | Như M05: một cụm ký tự cách nhau bởi khoảng trắng; mỗi âm tiết tiếng Việt là một từ. Số từ của bài tính trên tiêu đề cộng nội dung chữ. |
| Tóm tắt | Bản tóm lược ngắn hoặc các ý chính của một bài viết, do AI tạo khi người dùng đã đăng nhập yêu cầu. |
| Kết quả tóm tắt đang giữ | Tóm tắt của một bài được giữ tạm 24 giờ kể từ lúc tạo, dùng chung cho mọi người yêu cầu bài đó; bị bỏ khi hết hạn, khi tiêu đề hoặc nội dung chữ thay đổi, hoặc khi bài còn dưới 300 từ. |
| 24 giờ | Đủ 24 × 60 phút kể từ thời điểm tạo, không theo ngày lịch. |
| Nhật ký quyết định AI | Bản ghi của một lời gọi AI (chấm điểm kiểm duyệt, embedding bài, gợi ý Topic): loại lời gọi, thành công hay thất bại, đầu ra thô; gắn với bài viết hoặc bình luận liên quan; tách khỏi nhật ký hành động của Mod, Admin. |
| Đầu ra thô | Kết quả dịch vụ AI trả về, giữ nguyên chưa qua xử lý của iShare (ví dụ bốn điểm nhóm vi phạm, danh sách Topic gợi ý). |
| Phản hồi gợi ý Topic | Bản ghi của M05 gồm các Topic AI gợi ý và các Topic tác giả chọn cuối cùng; chỉ ghi khi gợi ý chưa lỗi thời (FR-M05). |
| Tỷ lệ Topic gợi ý được giữ lại | Số Topic AI gợi ý mà tác giả giữ lại chia cho tổng số Topic AI gợi ý, trên các phản hồi gợi ý Topic trong khoảng thời gian chọn. |

### 2.2 Viết tắt

| Viết tắt | Đầy đủ |
|---|---|
| FR | Functional Requirement — yêu cầu chức năng |
| AI | Trí tuệ nhân tạo; trong tài liệu này là dịch vụ AI của bên thứ ba mà iShare gọi tới |
| MS1 | Milestone 1 — mốc demo của đồ án |

## 3. Thông tin đầu vào

### 3.1 Tài liệu đầu vào

| Tài liệu | Phiên bản / mốc |
|---|---|
| Draft: docs/_temp/iShare_modules.md, iShare_specs_general.md | Theo ngày sửa tệp |
| Register: decisions, qa-log, issue-queue, open-issues, glossary, module-registry | DEC-207, QA-392, ISS-332, OPEN-012 (khớp `moc_nguon`) |

### 3.2 Tài liệu liên quan

| Module | Liên quan ở điểm nào |
|---|---|
| M01 Authentication & Account | Trang chính sách công bố việc xử lý nội dung bởi nhà cung cấp dịch vụ AI; nhật ký AI và phản hồi gợi ý Topic của tài khoản đã xóa được giữ lại. |
| M03 Post & Content | Quét bài trước khi đăng, quét lại khi sửa; hệ quả theo điểm quét và khi AI lỗi; bài của Admin không quét; mốc Đã đăng để tạo embedding; nút tóm tắt trên bài. |
| M04 Comment | Bình luận bị AI tự ẩn; bình luận của Admin không quét. |
| M05 Topic & Tag | Gợi ý Topic do M13 thực hiện lời gọi; phản hồi gợi ý là dữ liệu đánh giá chất lượng gợi ý Topic. |
| M06 Search | Tìm kiếm ngữ nghĩa dùng embedding của M13; tìm full-text khi tắt AI hoặc AI lỗi. |
| M08 Moderation | Quét luồng bình luận, cảnh cáo do AI, vụ do AI tạo dùng điểm và ngưỡng của M13. |
| M09 Appeal | Nhật ký quyết định AI làm căn cứ khi xét khiếu nại bài bị AI tự từ chối. |
| M10 Admin Panel | Công tắc AI tổng và riêng; ngưỡng là hằng số chính sách, không chỉnh qua giao diện. |
| M11 Group | Bài trong nhóm dùng cùng ngưỡng AI trước cổng duyệt của nhóm. |
| M14 Feed & Discovery | Không còn phụ thuộc M13 (không có feed cá nhân hóa bằng AI). |
| M15 Analytics & Stats | Hiển thị tỷ lệ Topic gợi ý được giữ lại cho Admin ở bảng thống kê Nội dung; định nghĩa các khoảng thời gian và cách hiện khi không có dữ liệu. |
| M16 Chat & Messaging | Không có AI kiểm duyệt tin nhắn. |

## 4. Tổng quan chức năng

### 4.1 Luật, tiêu chuẩn liên quan

Không có.

### 4.2 Vai trò

| Vai trò | Mô tả trong module này |
|---|---|
| Guest | Người chưa đăng nhập. Thấy nút tóm tắt trên bài nhưng không dùng được (được nhắc đăng nhập); không tìm bài theo ngữ nghĩa. |
| User | Người dùng đã đăng nhập. Yêu cầu tóm tắt bài viết từ 300 từ; tìm bài theo ngữ nghĩa. Nội dung của User được AI chấm điểm, tạo embedding, gợi ý Topic qua các module gọi tới M13. |
| Mod | Có quyền của User. Xem nhật ký quyết định AI khi xét khiếu nại bài bị AI tự từ chối. |
| Admin | Có các quyền của Mod. Bật, tắt công tắc AI ở M10; xem tỷ lệ Topic gợi ý được giữ lại ở M15; nội dung của Admin không qua quét AI. |
| Hệ thống | Lớp AI: gọi dịch vụ AI (kiểm tra công tắc, thời gian chờ, thử lại), chấm điểm kiểm duyệt, tạo và tạo bù embedding, lấy gợi ý Topic, tạo và giữ tạm tóm tắt, ghi nhật ký quyết định AI, tính chất lượng gợi ý Topic. |

### 4.3 Ma trận quyền

| Hành động | Guest | User | Mod | Admin | Yêu cầu |
|---|---|---|---|---|---|
| Yêu cầu và xem tóm tắt AI của bài viết từ 300 từ | ✗ | ✓ | ✓ | ✓ | FR-M13-07.01, FR-M13-07.03 |
| Tìm bài viết theo ngữ nghĩa (tạo embedding cho truy vấn) | ✗ | ✓ | ✓ | ✓ | FR-M13-04.01, FR-M13-04.04 |
| Xem nhật ký quyết định AI khi xét khiếu nại bài bị AI tự từ chối | ✗ | ✗ | ✓ | ✓ | FR-M13-09.01, FR-M13-09.02 |
| Tra cứu nhật ký quyết định AI ngoài lúc xét khiếu nại | ✗ | ✗ | ✗ | ✗ | FR-M13-09.04 |
| Xem tỷ lệ Topic gợi ý được giữ lại | ✗ | ✗ | ✗ | ✓ | FR-M13-10.04 |
| Đánh dấu dự đoán của AI là đúng hay sai | ✗ | ✗ | ✗ | ✗ | FR-M13-10.05 |

<!-- Ô nói thẳng: hàng 1 (QA-389: chỉ người đã đăng nhập; Guest được nhắc đăng nhập); hàng 2 cột Guest (QA-011 "Semantic
     Search: Không"; luồng tìm thuộc M06); hàng 3 cột Mod, Admin (DEC-198, DEC-207); hàng 4 (QA-391, DEC-207); hàng 5
     (QA-385, DEC-203: Admin xem ở M15, M15 chỉ cho Admin — QA-241); hàng 6 (QA-384, DEC-203).
     Ô suy ra: hàng 2 cột User, Mod, Admin (DEC-053 tìm bài theo ngữ nghĩa, chỉ Guest bị loại); hàng 3 cột Guest, User
     (DEC-207: chỉ Mod, Admin xét khiếu nại xem nhật ký). -->

### 4.4 Danh sách chức năng

| ID | Chức năng | Tác nhân chính | Kích hoạt |
|---|---|---|---|
| FR-M13-01 | Gọi dịch vụ AI | Hệ thống | Một module cần kết quả AI: chấm điểm kiểm duyệt, tạo embedding, gợi ý Topic hoặc tóm tắt |
| FR-M13-02 | Chấm điểm kiểm duyệt bài viết, bình luận | Hệ thống | M03 gửi bài để quét (bài mới gửi, bài đã đăng được sửa, bài tự ẩn đã sửa được hiện lại); M08 kích hoạt quét một luồng bình luận |
| FR-M13-03 | Tạo embedding cho bài viết | Hệ thống | Bài chuyển sang Đã đăng; tiêu đề hoặc nội dung chữ của bài Đã đăng thay đổi; bài trong hàng chờ tạo bù khi AI dùng được trở lại |
| FR-M13-04 | Tạo embedding cho truy vấn tìm kiếm | Hệ thống | M06 nhận một truy vấn tìm bài viết của người dùng đã đăng nhập |
| FR-M13-05 | Lấy gợi ý Topic từ AI | Hệ thống | M05 chuyển yêu cầu gợi ý Topic hợp lệ của tác giả |
| FR-M13-06 | Tạo và giữ tạm tóm tắt bài viết | Hệ thống | Có yêu cầu tóm tắt một bài mà bài đó chưa có kết quả tóm tắt đang giữ |
| FR-M13-07 | Yêu cầu xem tóm tắt bài viết | User, Mod, Admin | Người dùng bấm "Tóm tắt" trên một bài viết từ 300 từ |
| FR-M13-08 | Ghi nhật ký quyết định AI | Hệ thống | Một lời gọi chấm điểm kiểm duyệt, embedding bài hoặc gợi ý Topic kết thúc |
| FR-M13-09 | Xem nhật ký quyết định AI | Mod, Admin | Mod hoặc Admin xét khiếu nại bài bị AI tự từ chối (M09) |
| FR-M13-10 | Đánh giá chất lượng gợi ý Topic | Hệ thống | Admin mở bảng thống kê Nội dung của M15 hoặc đổi khoảng thời gian |

### 4.5 Mốc và ưu tiên

Toàn bộ yêu cầu của module thuộc MS1, ưu tiên **Must** (bảng MoSCoW Summary của module-registry: Must gồm M01–M10, M13;
cột MoSCoW ở dòng M13 của bảng Module List bị lệch nên không dùng). Không có yêu cầu ngoại lệ về ưu tiên.

## 5. Yêu cầu chức năng

### 5.1 FR-M13-01 Gọi dịch vụ AI

**Yêu cầu cấp trên:** Hệ thống phải gửi yêu cầu AI của các module tới dịch vụ AI của bên thứ ba khi AI đang bật, giới hạn thời gian chờ, thử lại một lần khi lỗi, và báo kết quả hoặc thất bại cho module gọi.

**Lý do:** Hệ thống phải hoạt động độc lập khi AI tắt; công tắc AI cho phép bật, tắt linh hoạt mà không cần triển khai lại. AI lỗi tạm thời được xử lý như một lần giảm cấp cho riêng yêu cầu đó, không phải một lần đổi trạng thái. M13 là hạ tầng dùng chung cho M05, M06, M08 nên được thiết kế như một lớp riêng ngay từ đầu, để phần lõi không phụ thuộc cứng vào AI và nhà cung cấp AI có thể thay đổi.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M13-01.01 | Ở nơi công tắc AI tổng bật, khi một module yêu cầu kết quả AI, hệ thống phải gửi yêu cầu tới dịch vụ AI của bên thứ ba (BR-M13-03, BR-M13-05). |
| FR-M13-01.02 | Trong khi công tắc AI tổng tắt, hệ thống phải không gửi lời gọi AI nào và báo cho module gọi rằng AI đang tắt (BR-M13-06). |
| FR-M13-01.03 | Trong khi công tắc AI tổng bật và công tắc riêng của loại yêu cầu tắt (Moderation với chấm điểm kiểm duyệt; Search với embedding bài và embedding truy vấn; Topic suggestion với gợi ý Topic), hệ thống phải không gửi lời gọi đó và báo cho module gọi rằng AI đang tắt (BR-M13-06). |
| FR-M13-01.04 | Hệ thống phải tính một lần thử là lỗi khi dịch vụ AI báo lỗi hoặc chưa có kết quả sau thời gian chờ: 5 giây với chấm điểm kiểm duyệt và embedding, 10 giây với gợi ý Topic và tóm tắt (BR-M13-08). |
| FR-M13-01.05 | Nếu lần thử đầu lỗi, hệ thống phải đợi 2 giây rồi thử lại đúng một lần, không gửi hai lần thử cùng lúc (BR-M13-09). |
| FR-M13-01.06 | Nếu cả hai lần thử đều lỗi, hệ thống phải báo lời gọi thất bại cho module gọi để module đó xử lý theo cách đã định (BR-M13-10). |
| FR-M13-01.07 | Khi một lời gọi thất bại, hệ thống phải giữ nguyên các công tắc AI và tiếp tục xử lý các lời gọi AI khác như bình thường (BR-M13-07). |
| FR-M13-01.08 | Hệ thống phải không áp giới hạn tần suất riêng cho lời gọi AI, ngoài giới hạn tìm kiếm của M06 và giới hạn gợi ý Topic của M05 (BR-M13-19). |
| FR-M13-01.09 | Khi Admin đổi một công tắc AI (M10), hệ thống phải áp dụng trạng thái mới cho các lời gọi AI sau đó mà không cần triển khai lại. |
| FR-M13-01.10 | Hệ thống phải cung cấp qua lớp AI năm năng lực: chấm điểm kiểm duyệt (FR-M13-02), embedding cho tìm kiếm ngữ nghĩa (FR-M13-03, FR-M13-04), gợi ý Topic (FR-M13-05), tóm tắt bài viết (FR-M13-06, FR-M13-07) và đánh giá chất lượng gợi ý Topic (FR-M13-10) (BR-M13-04). |
| FR-M13-01.11 | Hệ thống phải không tự xây, train hay fine-tune mô hình AI riêng, và không có chatbot, RAG phức tạp, multi-agent (BR-M13-03). |
| FR-M13-01.12 | Hệ thống phải không để AI ban tài khoản, tự cộng hoặc trừ điểm, tự trao badge, hay tự viết bài, bình luận (BR-M13-02). |

### 5.2 FR-M13-02 Chấm điểm kiểm duyệt bài viết, bình luận

**Yêu cầu cấp trên:** Hệ thống phải chấm điểm nội dung bài viết, bình luận mà M03, M08 gửi tới theo bốn nhóm vi phạm, rồi trả điểm quét, nhóm vi phạm và khoảng điểm để module gọi quyết hệ quả.

**Lý do:** Nền tảng phục vụ học sinh nên cần quét để kiểm soát nội dung. Bốn nhóm AI chấm khớp thẳng với các lý do báo cáo; các vi phạm khác không có cách phát hiện bằng AI nên dựa hoàn toàn vào báo cáo. Một lần gọi dùng cho cả cổng nội dung và cảnh cáo. AI không phải là quyết định duy nhất với trường hợp nhạy cảm, vì chất lượng AI không đoán trước được và niềm tin cần có người giám sát. Cặp ngưỡng là giá trị tạm, chờ dữ liệu sử dụng thật để chỉnh.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M13-02.01 | Khi M03 gửi một bài viết để quét (bài mới gửi, bài đã đăng được sửa, bài tự ẩn đã sửa được hiện lại), hệ thống phải gửi tiêu đề, nội dung chữ, bình chọn (câu hỏi và các lựa chọn) và ảnh đính kèm của bài tới AI kiểm duyệt qua FR-M13-01 (BR-M13-25). |
| FR-M13-02.02 | Hệ thống phải không gửi tài liệu đính kèm của bài (PDF, DOCX, XLSX, PPTX) tới AI kiểm duyệt (BR-M13-25). |
| FR-M13-02.03 | Khi M08 kích hoạt quét một luồng bình luận, hệ thống phải gửi nội dung chữ của từng bình luận M08 chuyển tới để AI kiểm duyệt chấm điểm qua FR-M13-01 (BR-M13-25). |
| FR-M13-02.04 | Khi dịch vụ AI trả kết quả, hệ thống phải lấy điểm của bốn nhóm vi phạm: Quấy rối, Ngôn từ thù ghét, Nội dung người lớn, Bạo lực (BR-M13-11). |
| FR-M13-02.05 | Hệ thống phải lấy điểm quét là điểm cao nhất trong bốn nhóm, và nhóm có điểm đó là nhóm vi phạm (BR-M13-12). |
| FR-M13-02.06 | Nếu hai nhóm trở lên cùng có điểm cao nhất, hệ thống phải lấy nhóm đứng trước theo thứ tự Quấy rối, Ngôn từ thù ghét, Nội dung người lớn, Bạo lực làm nhóm vi phạm (BR-M13-12). |
| FR-M13-02.07 | Hệ thống phải xếp điểm quét vào khoảng cao (từ 0,9), nghi ngờ (từ 0,5 đến dưới 0,9) hoặc sạch (dưới 0,5) theo cùng một cặp ngưỡng cho bài viết, bình luận và mọi tác giả (BR-M13-13). |
| FR-M13-02.08 | Khi chấm xong, hệ thống phải trả điểm quét, nhóm vi phạm và khoảng điểm cho module gọi, để M03, M04, M08, M11 quyết hệ quả cho cổng nội dung và cảnh cáo (BR-M13-15). |
| FR-M13-02.09 | Hệ thống phải chỉ cho module gọi tự xử lý nội dung không qua người (tự từ chối bài mới, tự ẩn bình luận, tự cảnh cáo) khi điểm quét ở khoảng cao; ở khoảng nghi ngờ, Mod hoặc Admin quyết (BR-M13-01). |
| FR-M13-02.10 | Hệ thống phải để Spam/Quảng cáo, Đạo văn/Vi phạm bản quyền, Nội dung sai/gây hiểu nhầm chỉ được phát hiện qua báo cáo (M08), không qua AI (BR-M13-11). |
| FR-M13-02.11 | Hệ thống phải không chấm điểm kiểm duyệt nội dung của tài khoản Admin (BR-M13-16). |
| FR-M13-02.12 | Hệ thống phải không chấm điểm kiểm duyệt tin nhắn chat (BR-M13-16). |
| FR-M13-02.13 | Trong khi công tắc AI tổng hoặc công tắc Moderation tắt, hệ thống phải không chấm điểm kiểm duyệt (BR-M13-06). |
| FR-M13-02.14 | Hệ thống phải chỉ đổi cặp ngưỡng 0,9 và 0,5 qua một lần triển khai mới, không qua giao diện quản trị (BR-M13-14). |
| FR-M13-02.15 | Nếu lời gọi chấm điểm thất bại sau hai lần thử, hệ thống phải báo thất bại cho M03 hoặc M08 để module đó xử lý theo cách đã định (BR-M13-10). |

### 5.3 FR-M13-03 Tạo embedding cho bài viết

**Yêu cầu cấp trên:** Hệ thống phải tạo một embedding cho mỗi bài viết khi bài Đã đăng, tạo lại khi tiêu đề hoặc nội dung chữ thay đổi, và tạo bù cho bài còn thiếu, để M06 tìm bài theo ngữ nghĩa.

**Lý do:** Tìm kiếm bài viết của M06 theo ngữ nghĩa nên cần embedding của bài; bài thiếu embedding sẽ không bao giờ xuất hiện khi tìm theo ngữ nghĩa, nên bài thiếu được tạo bù. Khác với quét kiểm duyệt (không quét bù), tạo bù embedding không làm đổi điều người dùng đang thấy. Bình luận không có embedding vì chi phí duy trì không đáng ở quy mô đồ án.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M13-03.01 | Khi một bài viết chuyển sang Đã đăng (qua bước quét, được Mod duyệt, đăng thẳng khi AI tắt, hoặc là bài của Admin), hệ thống phải tạo embedding cho bài qua FR-M13-01 (BR-M13-18). |
| FR-M13-03.02 | Khi tiêu đề hoặc nội dung chữ của một bài Đã đăng thay đổi, hệ thống phải tạo lại embedding của bài (BR-M13-18). |
| FR-M13-03.03 | Hệ thống phải giữ đúng một embedding cho mỗi bài viết; embedding tạo lại thay embedding cũ (BR-M13-17). |
| FR-M13-03.04 | Khi chỉ Tag, Topic, ảnh hoặc tài liệu đính kèm của bài thay đổi, hệ thống phải không tạo lại embedding (BR-M13-18). |
| FR-M13-03.05 | Hệ thống phải không tạo embedding cho bài chưa Đã đăng: bài nháp, bài đang chờ, bài bị từ chối (BR-M13-18). |
| FR-M13-03.06 | Hệ thống phải không tạo embedding cho bình luận (BR-M13-17). |
| FR-M13-03.07 | Hệ thống phải cung cấp embedding của bài cho M06 để tìm bài theo ngữ nghĩa. |
| FR-M13-03.08 | Nếu công tắc AI tổng hoặc công tắc Search đang tắt khi một bài cần tạo embedding, hệ thống phải không gọi AI và đưa bài vào hàng chờ tạo bù embedding (BR-M13-26). |
| FR-M13-03.09 | Nếu tạo embedding cho một bài thất bại sau hai lần thử, hệ thống phải đưa bài vào hàng chờ tạo bù embedding (BR-M13-26). |
| FR-M13-03.10 | Ở nơi công tắc AI tổng và công tắc Search đều bật, hệ thống phải tạo embedding theo nội dung hiện tại cho các bài trong hàng chờ tạo bù khi AI trả lời được, rồi đưa bài ra khỏi hàng chờ (BR-M13-26). |

### 5.4 FR-M13-04 Tạo embedding cho truy vấn tìm kiếm

**Yêu cầu cấp trên:** Hệ thống phải tạo embedding cho truy vấn tìm bài viết mà M06 chuyển tới, để M06 so với embedding của các bài.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M13-04.01 | Ở nơi công tắc AI tổng và công tắc Search đều bật, khi M06 nhận một truy vấn tìm bài viết của người dùng đã đăng nhập, hệ thống phải tạo embedding cho truy vấn qua FR-M13-01 và trả cho M06. |
| FR-M13-04.02 | Trong khi công tắc AI tổng hoặc công tắc Search tắt, hệ thống phải không tạo embedding cho truy vấn, để M06 tìm full-text (BR-M13-06). |
| FR-M13-04.03 | Nếu tạo embedding cho truy vấn thất bại sau hai lần thử, hệ thống phải báo thất bại cho M06 để M06 tìm full-text cho riêng truy vấn đó (BR-M13-10). |
| FR-M13-04.04 | Nếu truy vấn đến từ Guest, hệ thống phải không tạo embedding cho truy vấn. |

### 5.5 FR-M13-05 Lấy gợi ý Topic từ AI

**Yêu cầu cấp trên:** Hệ thống phải gửi tiêu đề và nội dung chữ của bài mà M05 chuyển tới cho AI để lấy các Topic gợi ý, rồi trả đầu ra cho M05.

**Lý do:** AI chỉ gợi ý Topic, không tự gán; tác giả xem và chọn lại nếu cần, và lựa chọn cuối cùng của tác giả là phản hồi cho AI.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M13-05.01 | Ở nơi công tắc AI tổng và công tắc Topic suggestion đều bật, khi M05 chuyển một yêu cầu gợi ý Topic, hệ thống phải gửi tiêu đề và nội dung chữ của bài, không gồm tệp đính kèm, tới AI gợi ý Topic qua FR-M13-01. |
| FR-M13-05.02 | Khi AI trả kết quả, hệ thống phải chuyển các Topic AI trả về cho M05 để M05 đối chiếu với danh mục Topic và hiển thị cho tác giả. |
| FR-M13-05.03 | Nếu lời gọi gợi ý Topic thất bại sau hai lần thử, hệ thống phải báo thất bại cho M05 để M05 hiện lỗi không chặn và tác giả tự chọn Topic (BR-M13-10). |
| FR-M13-05.04 | Trong khi công tắc AI tổng hoặc công tắc Topic suggestion tắt, hệ thống phải không lấy gợi ý Topic (BR-M13-06). |
| FR-M13-05.05 | Hệ thống phải không lấy gợi ý Tag từ AI. |

### 5.6 FR-M13-06 Tạo và giữ tạm tóm tắt bài viết

**Yêu cầu cấp trên:** Hệ thống phải tạo tóm tắt bằng AI cho bài viết khi có yêu cầu, giữ tạm kết quả 24 giờ để mọi người yêu cầu dùng chung, và bỏ kết quả khi hết hạn hoặc bài thay đổi.

**Lý do:** Giữ tạm kết quả "vừa giảm tải khi nhiều user yêu cầu, vừa hạn chế 1 người spam tóm tắt", nên không cần giới hạn tần suất riêng. Tóm tắt không cần lưu lâu dài: mỗi lần có yêu cầu thì nhận kết quả từ AI và hiện cho người dùng.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M13-06.01 | Khi có yêu cầu tóm tắt một bài viết mà bài chưa có kết quả tóm tắt đang giữ, hệ thống phải gửi tiêu đề và nội dung chữ của bài tới AI qua FR-M13-01, không gửi tệp đính kèm và bình chọn (BR-M13-28). |
| FR-M13-06.02 | Khi AI trả kết quả tóm tắt, hệ thống phải giữ tạm kết quả đó cho bài trong 24 giờ kể từ lúc tạo (BR-M13-27). |
| FR-M13-06.03 | Khi có yêu cầu tóm tắt một bài đang có kết quả tóm tắt đang giữ, hệ thống phải trả kết quả đó mà không gọi AI, bất kể người yêu cầu là ai (BR-M13-27). |
| FR-M13-06.04 | Khi kết quả tóm tắt đang giữ đủ 24 giờ, hệ thống phải bỏ kết quả đó (BR-M13-27). |
| FR-M13-06.05 | Khi tiêu đề hoặc nội dung chữ của bài thay đổi, hệ thống phải bỏ kết quả tóm tắt đang giữ của bài (BR-M13-27). |
| FR-M13-06.06 | Hệ thống phải dùng thời gian chờ 10 giây cho mỗi lần thử tóm tắt, và chỉ đổi con số này qua một lần triển khai mới (BR-M13-08). |
| FR-M13-06.07 | Nếu lời gọi tóm tắt thất bại sau hai lần thử, hệ thống phải không giữ kết quả nào và báo thất bại cho FR-M13-07 (BR-M13-10). |
| FR-M13-06.08 | Hệ thống phải không tạo tóm tắt tự động và không giữ tóm tắt quá thời gian giữ tạm (BR-M13-20). |
| FR-M13-06.09 | Hệ thống phải không tạo tóm tắt cho luồng bình luận (BR-M13-20). |
| FR-M13-06.10 | Hệ thống phải không áp giới hạn tần suất riêng cho yêu cầu tóm tắt (BR-M13-19). |
| FR-M13-06.11 | Hệ thống phải không đưa bài vào hàng chờ tạo bù cho tóm tắt (BR-M13-26). |

### 5.7 FR-M13-07 Yêu cầu xem tóm tắt bài viết

**Yêu cầu cấp trên:** Hệ thống phải cho người dùng đã đăng nhập yêu cầu và xem tóm tắt AI của bài viết từ 300 từ mà họ xem được.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M13-07.01 | Ở nơi công tắc AI tổng bật, khi một người dùng đã đăng nhập bấm "Tóm tắt" trên một bài viết mà họ xem được, hệ thống phải hiển thị tóm tắt của bài lấy từ FR-M13-06 (BR-M13-20). |
| FR-M13-07.02 | Hệ thống phải chỉ hiển thị nút "Tóm tắt" trên bài viết có tiêu đề cộng nội dung chữ từ 300 từ trở lên (BR-M13-20). |
| FR-M13-07.03 | Nếu Guest bấm "Tóm tắt", hệ thống phải không tạo tóm tắt và hiển thị thông báo yêu cầu đăng nhập để sử dụng tính năng. |
| FR-M13-07.04 | Khi hiển thị tóm tắt, hệ thống phải hiển thị kèm ghi chú "Tóm tắt chưa bao gồm nội dung tệp đính kèm" (BR-M13-28). |
| FR-M13-07.05 | Nếu lời gọi tóm tắt thất bại, hệ thống phải hiển thị thông báo hệ thống đang bận, vui lòng thử lại sau, và vẫn cho đọc bài bình thường (BR-M13-10). |
| FR-M13-07.06 | Trong khi công tắc AI tổng tắt, hệ thống phải vẫn hiển thị nút "Tóm tắt" trên bài viết từ 300 từ. |
| FR-M13-07.07 | Khi người dùng bấm "Tóm tắt" trong lúc công tắc AI tổng tắt, hệ thống phải hiển thị ngay thông báo hệ thống đang bận mà không gọi AI (BR-M13-06). |
| FR-M13-07.08 | Hệ thống phải hiển thị bài viết đầy đủ dù tóm tắt chưa được yêu cầu, đang chờ AI hay thất bại. |

### 5.8 FR-M13-08 Ghi nhật ký quyết định AI

**Yêu cầu cấp trên:** Hệ thống phải ghi một bản ghi nhật ký quyết định AI cho mỗi lời gọi chấm điểm kiểm duyệt, embedding bài và gợi ý Topic, kể cả lời gọi thất bại, gắn với bài viết hoặc bình luận liên quan, và giữ vĩnh viễn.

**Lý do:** Nhật ký cho dữ liệu sử dụng thật để chỉnh cặp ngưỡng tạm 0,9/0,5 thay vì đoán, và là căn cứ cho Mod, Admin khi xét khiếu nại của người dùng phản đối việc AI xử lý mình. Nhật ký này ghi quyết định do AI đưa ra, khác với nhật ký hành động của Mod, Admin. Nhật ký là loại dữ liệu thường không bao giờ bị xóa vì giá trị minh bạch và truy vết.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M13-08.01 | Khi một lời gọi chấm điểm kiểm duyệt, tạo embedding bài hoặc lấy gợi ý Topic kết thúc, kể cả khi thất bại, hệ thống phải ghi đúng một bản ghi nhật ký quyết định AI cho lời gọi đó (BR-M13-21). |
| FR-M13-08.02 | Hệ thống phải ghi trong mỗi bản ghi loại lời gọi, lời gọi thành công hay thất bại, và đầu ra thô khi có (BR-M13-21). |
| FR-M13-08.03 | Hệ thống phải gắn mỗi bản ghi nhật ký quyết định AI với bài viết hoặc bình luận liên quan (BR-M13-21). |
| FR-M13-08.04 | Khi quét một luồng bình luận, hệ thống phải ghi một bản ghi riêng cho mỗi bình luận được chấm điểm (BR-M13-21). |
| FR-M13-08.05 | Hệ thống phải không ghi lời gọi tóm tắt và lời gọi tạo embedding cho truy vấn vào nhật ký quyết định AI (BR-M13-21). |
| FR-M13-08.06 | Hệ thống phải ghi nhật ký quyết định AI tách khỏi nhật ký kiểm duyệt của Mod, Admin (BR-M13-21). |
| FR-M13-08.07 | Hệ thống phải giữ nhật ký quyết định AI vĩnh viễn, không sửa và không xóa bản ghi (BR-M13-22). |
| FR-M13-08.08 | Khi tài khoản của tác giả chuyển sang DELETED, hệ thống phải giữ nhật ký quyết định AI liên quan và vẫn gắn với tài khoản qua username giữ lại (BR-M13-22). |
| FR-M13-08.09 | Khi quét một bình luận thất bại sau hai lần thử, hệ thống phải ghi bản ghi thất bại của bình luận đó làm bản ghi lỗi cho Admin (BR-M13-21). |

### 5.9 FR-M13-09 Xem nhật ký quyết định AI

**Yêu cầu cấp trên:** Hệ thống phải cho Mod, Admin xem nhật ký quyết định AI của bài viết làm căn cứ khi xét khiếu nại bài bị AI tự từ chối, và chỉ trong ngữ cảnh đó.

**Lý do:** Khi người dùng khiếu nại vì cho rằng AI xử lý oan, Mod, Admin cần xem lại AI đã chấm gì để quyết. Không có bản chụp nội dung lúc xử lý ở MS1, nên người xét dựa vào lý do kết luận, bằng chứng, lịch sử sửa bài và nhật ký AI. Việc chỉnh ngưỡng do đội phát triển đọc dữ liệu và đổi qua triển khai, nên không cần màn hình tra cứu riêng.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M13-09.01 | Khi Mod hoặc Admin xét khiếu nại một bài viết bị AI tự từ chối (M09), hệ thống phải hiển thị nhật ký quyết định AI của bài. |
| FR-M13-09.02 | Nếu người yêu cầu xem nhật ký quyết định AI là Guest hoặc User, hệ thống phải từ chối. |
| FR-M13-09.03 | Hệ thống phải cho Mod, Admin xem nhật ký quyết định AI của nội dung thuộc tài khoản đã xóa qua username giữ lại. |
| FR-M13-09.04 | Hệ thống phải không cung cấp chỗ tra cứu nhật ký quyết định AI nào khác ngoài lúc xét khiếu nại bài bị AI tự từ chối. |

### 5.10 FR-M13-10 Đánh giá chất lượng gợi ý Topic

**Yêu cầu cấp trên:** Hệ thống phải tính tỷ lệ Topic gợi ý được giữ lại từ các phản hồi gợi ý Topic theo khoảng thời gian, để Admin theo dõi chất lượng gợi ý Topic ở trang thống kê.

**Lý do:** Đo chất lượng việc tích hợp dịch vụ AI theo thời gian để biết có cần chỉnh hay không, không phải để train lại mô hình. Chỉ đo gợi ý Topic vì dữ liệu phản hồi đã có sẵn trong luồng gợi ý, không cần giao diện riêng; việc đo nội bộ không gửi phản hồi ngược cho AI.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M13-10.01 | Hệ thống phải tính tỷ lệ Topic gợi ý được giữ lại bằng số Topic AI gợi ý mà tác giả giữ lại chia cho tổng số Topic AI gợi ý, trên các phản hồi gợi ý Topic của M05, kể cả phản hồi của tài khoản đã xóa (BR-M13-29, BR-M13-23). |
| FR-M13-10.02 | Hệ thống phải tính tỷ lệ cho khoảng thời gian Admin chọn trong bộ lọc của M15 (Hôm nay, 7 ngày, 30 ngày, Toàn thời gian), xếp mỗi phản hồi theo lúc nó được ghi, theo giờ Việt Nam (BR-M13-29). |
| FR-M13-10.03 | Nếu khoảng thời gian chọn không có phản hồi gợi ý Topic nào, hệ thống phải báo không có dữ liệu thay vì một tỷ lệ (BR-M13-29). |
| FR-M13-10.04 | Hệ thống phải cung cấp tỷ lệ cho bảng thống kê Nội dung của M15, nơi chỉ Admin xem được. |
| FR-M13-10.05 | Hệ thống phải không có thao tác đánh dấu dự đoán của AI là đúng hay sai (BR-M13-24). |
| FR-M13-10.06 | Hệ thống phải không tính chỉ số chất lượng cho AI kiểm duyệt (BR-M13-24). |
| FR-M13-10.07 | Hệ thống phải không gửi kết quả đánh giá cho dịch vụ AI và không dùng kết quả để train lại mô hình (BR-M13-24). |

### 5.11 Quy tắc nghiệp vụ

| ID | Loại | Quy tắc | Ví dụ |
|---|---|---|---|
| BR-M13-01 | Sự kiện | AI chỉ là lớp hỗ trợ. AI chỉ tự xử lý (tự từ chối bài mới, tự ẩn bình luận, tự cảnh cáo) khi điểm quét ở khoảng cao; mọi trường hợp khác do người quyết. Người bị AI xử lý khiếu nại được (M09). | — |
| BR-M13-02 | Ràng buộc | AI không bao giờ ban, không tự cộng, trừ điểm, không tự trao badge, không tự viết bài hoặc bình luận. | — |
| BR-M13-03 | Ràng buộc | Lớp AI chỉ dùng dịch vụ AI của bên thứ ba; không xây, train hay fine-tune mô hình riêng; không có chatbot, RAG phức tạp, multi-agent. | — |
| BR-M13-04 | Sự kiện | Năm năng lực AI bắt buộc: kiểm duyệt nội dung, gợi ý Topic, tìm kiếm ngữ nghĩa, tóm tắt bài viết, đánh giá chất lượng gợi ý Topic. | — |
| BR-M13-05 | Sự kiện | AI chạy thật với mỗi thao tác mới; không dùng kết quả AI dựng sẵn. Phần lõi không phụ thuộc cứng vào AI: khi AI tắt hoặc lỗi, các module vẫn hoạt động bằng cách làm thay thế đã định. | Dữ liệu demo được nạp sẵn, nhưng một bài mới gửi trong buổi demo vẫn được gửi tới dịch vụ AI để chấm điểm. |
| BR-M13-06 | Ràng buộc | Công tắc tổng tắt thì không có lời gọi AI nào. Công tắc tổng bật thì: Moderation tắt → không chấm điểm kiểm duyệt; Search tắt → không tạo embedding cho bài và cho truy vấn; Topic suggestion tắt → không lấy gợi ý Topic. Tóm tắt không có công tắc riêng, chỉ theo công tắc tổng. | Tổng bật, Moderation tắt, Search bật: bài mới không được chấm điểm, tìm kiếm vẫn theo ngữ nghĩa. Tổng bật, Search tắt: bài mới Đã đăng vào hàng chờ tạo bù, tìm kiếm full-text, tóm tắt vẫn dùng được. Tổng tắt: không chấm điểm, không embedding, bấm "Tóm tắt" thì báo bận ngay. |
| BR-M13-07 | Sự kiện | AI tắt là trạng thái do Admin đặt. AI lỗi tạm thời chỉ ảnh hưởng yêu cầu bị lỗi, không đổi công tắc, không ảnh hưởng yêu cầu khác. | Truy vấn của A bị lỗi lúc 10:00:00 → chỉ truy vấn đó tìm full-text; truy vấn của B lúc 10:00:01 vẫn gọi AI. |
| BR-M13-08 | Ràng buộc | Thời gian chờ mỗi lần thử: chấm điểm kiểm duyệt và embedding 5 giây; gợi ý Topic và tóm tắt 10 giây. Thời gian chờ của tóm tắt là hằng số, chỉ đổi qua một lần triển khai mới. | Chấm điểm có kết quả ở giây 4,8 → dùng kết quả. Có kết quả ở giây 5,3 → lần thử đó lỗi. Tóm tắt có kết quả ở giây 9 → dùng. |
| BR-M13-09 | Kích hoạt | Lần thử đầu lỗi hoặc hết thời gian chờ thì đợi 2 giây rồi thử lại đúng một lần. Không thử hai lần song song. | Chấm điểm: lần 1 hết giờ ở giây 5, lần 2 gửi ở giây 7, hết giờ ở giây 12 → lời gọi thất bại; tối đa 12 giây. Gợi ý Topic, tóm tắt: 10 + 2 + 10 = tối đa 22 giây. Lần 1 lỗi ngay ở giây 0,5 → lần 2 gửi ở giây 2,5. |
| BR-M13-10 | Suy diễn | Lời gọi thất bại sau hai lần thử thì báo thất bại cho module gọi; module đó xử lý theo cách đã định: tìm kiếm → full-text cho riêng truy vấn đó (M06); gợi ý Topic → báo lỗi không chặn, tác giả tự chọn (M05); quét bài mới gửi → chờ Mod xét, không tự đăng (M03); quét lại bài đã đăng sau khi sửa → giữ nguyên, bài vẫn hiện (M03); quét luồng bình luận → giữ nguyên, ghi bản ghi lỗi cho Admin (M08); embedding bài → vào hàng chờ tạo bù (FR-M13-03); tóm tắt → báo hệ thống đang bận, không giữ kết quả (FR-M13-07). | Bài mới gửi, cả hai lần chấm điểm hết giờ → bài ở lại chờ Mod xét. Bài Q Đã đăng, embedding lỗi cả hai lần → Q vẫn hiển thị, vào hàng chờ tạo bù. |
| BR-M13-11 | Sự kiện | AI kiểm duyệt chỉ chấm bốn nhóm vi phạm: Quấy rối, Ngôn từ thù ghét, Nội dung người lớn, Bạo lực. Spam/Quảng cáo, Đạo văn/Vi phạm bản quyền, Nội dung sai/gây hiểu nhầm không do AI phát hiện, chỉ qua báo cáo (M08). | — |
| BR-M13-12 | Tính toán | Điểm quét = điểm cao nhất trong bốn điểm nhóm vi phạm; nhóm có điểm đó là nhóm vi phạm được ghi làm lý do. Nhiều nhóm cùng điểm cao nhất thì lấy nhóm đứng trước theo thứ tự Quấy rối, Ngôn từ thù ghét, Nội dung người lớn, Bạo lực. | Quấy rối 0,92, Bạo lực 0,10 → 0,92, nhóm Quấy rối. Người lớn 0,55, Thù ghét 0,40 → 0,55, nhóm Người lớn. Quấy rối 0,92, Bạo lực 0,92 → 0,92, nhóm Quấy rối. Người lớn 0,7, Bạo lực 0,7 → 0,7, nhóm Người lớn. |
| BR-M13-13 | Ràng buộc | Một cặp ngưỡng 0,9 / 0,5 chia điểm quét thành ba khoảng: cao (≥ 0,9), nghi ngờ (0,5 đến < 0,9), sạch (< 0,5). Dùng chung cho bài viết và bình luận, cho cả cổng nội dung và cảnh cáo, cho mọi tác giả bất kể mức cảnh cáo. Giá trị là tạm thời, sẽ chỉnh theo dữ liệu thật. | 0,90 → cao. 0,8999 → nghi ngờ. 0,50 → nghi ngờ. 0,4999 → sạch. Tác giả đang ở mức HEAVY, điểm 0,6 → vẫn là nghi ngờ. |
| BR-M13-14 | Ràng buộc | Ngưỡng là hằng số chính sách: không chỉnh được qua giao diện quản trị, chỉ đổi qua một lần triển khai mới. Việc chỉnh do đội phát triển đọc nhật ký quyết định AI. | — |
| BR-M13-15 | Sự kiện | Một lần chấm điểm phục vụ cả hai nhánh: cổng nội dung và cảnh cáo. Hệ quả của từng khoảng do module gọi quyết: bài viết (M03), bình luận (M04, M08), cảnh cáo (M08), bài trong nhóm (M11). | — |
| BR-M13-16 | Ràng buộc | Không chấm điểm kiểm duyệt nội dung của Admin và tin nhắn chat. | Bài mới của Admin đăng thẳng, không có lời gọi AI kiểm duyệt. |
| BR-M13-17 | Ràng buộc | Embedding chỉ tạo cho bài viết, mỗi bài một embedding; bình luận không có embedding. | — |
| BR-M13-18 | Kích hoạt | Embedding của bài được tạo khi bài chuyển sang Đã đăng, qua bất kỳ đường nào (quét sạch, Mod duyệt, đăng thẳng khi AI tắt, bài của Admin), và tạo lại mỗi lần tiêu đề hoặc nội dung chữ thay đổi. Bài nháp, đang chờ, bị từ chối không có embedding. Chỉ đổi Tag, Topic, ảnh, tài liệu thì không tạo lại. | Bài Y gửi 10:00, chờ Mod, được duyệt 12:00 → tạo lúc 12:00. Bài X bị AI tự từ chối → không có. Bài của Admin đăng 9:00 → tạo lúc 9:00. Sửa một lỗi chính tả trong nội dung → tạo lại. Chỉ thêm một Tag → không tạo lại. |
| BR-M13-19 | Ràng buộc | Lớp AI không có hệ thống giới hạn tần suất riêng. Lời gọi do hệ thống kích hoạt (chấm điểm, embedding bài) và yêu cầu tóm tắt không bị giới hạn. Tìm kiếm dùng giới hạn của M06; gợi ý Topic tối đa 10 yêu cầu trong 60 giây gần nhất cho mỗi người dùng (M05). | — |
| BR-M13-20 | Ràng buộc | Tóm tắt chỉ tạo khi người dùng đã đăng nhập yêu cầu, cho bài viết có tiêu đề cộng nội dung chữ từ 300 từ trở lên; không tóm tắt tự động, không lưu lâu dài, không tóm tắt luồng bình luận. | Bài 250 từ → không có nút "Tóm tắt". Bài 300 từ → có nút. Bài 2.000 từ → có nút. Bài 320 từ sửa còn 250 từ → mất nút. |
| BR-M13-21 | Sự kiện | Mỗi lời gọi chấm điểm kiểm duyệt, embedding bài, gợi ý Topic, kể cả lời gọi thất bại, có đúng một bản ghi nhật ký quyết định AI gồm loại lời gọi, thành công hay thất bại, đầu ra thô; bản ghi gắn với bài viết hoặc bình luận. Quét một luồng bình luận ghi mỗi bình luận một bản ghi. Tóm tắt và embedding truy vấn không được ghi. Nhật ký này tách khỏi nhật ký kiểm duyệt. | Quét một luồng gồm 1 bình luận gốc và 11 trả lời → 12 bản ghi. Chấm điểm một bài lỗi ở lần thử 1, thành công ở lần 2 → 1 bản ghi thành công. Cả hai lần lỗi → 1 bản ghi thất bại. |
| BR-M13-22 | Ràng buộc | Nhật ký quyết định AI được giữ vĩnh viễn, không sửa, không xóa. Khi tài khoản chuyển DELETED, nhật ký vẫn gắn với tài khoản qua username giữ lại để Mod, Admin tra cứu khi xét khiếu nại. | Tài khoản "an.nguyen" bị xóa ngày 10/10: nhật ký AI các bài cũ của tài khoản vẫn còn, hiện theo username "an.nguyen". |
| BR-M13-23 | Sự kiện | Dữ liệu đánh giá chất lượng gợi ý Topic là các phản hồi gợi ý Topic của M05 (Topic gợi ý so với Topic tác giả chọn cuối), kể cả của tài khoản đã xóa (không còn danh tính). | Gợi ý {Toán, Vật lý}, tác giả chọn {Toán, Hóa}: là một phản hồi. |
| BR-M13-24 | Ràng buộc | Chỉ gợi ý Topic được đánh giá chất lượng. AI kiểm duyệt không được đánh giá bằng chỉ số và không có thao tác đánh dấu dự đoán đúng, sai. Kết quả đánh giá không gửi cho dịch vụ AI, không dùng để train lại mô hình. | — |
| BR-M13-25 | Ràng buộc | Nội dung gửi cho AI kiểm duyệt: với bài viết là tiêu đề, nội dung chữ, bình chọn (câu hỏi và các lựa chọn) và ảnh đính kèm, không gồm tài liệu đính kèm; với bình luận là nội dung chữ. | Bài có 3 ảnh, 1 tệp PDF và một bình chọn: gửi tiêu đề, nội dung chữ, bình chọn và 3 ảnh; không gửi tệp PDF. |
| BR-M13-26 | Kích hoạt | Bài Đã đăng chưa có embedding theo nội dung hiện tại vì công tắc tổng hoặc Search đang tắt, hoặc vì lời gọi thất bại, được đưa vào hàng chờ tạo bù embedding. Khi cả hai công tắc bật và AI trả lời được, embedding được tạo theo nội dung hiện tại và bài ra khỏi hàng chờ. Tóm tắt không có tạo bù. | 9:00 Admin tắt công tắc tổng; 9:30 bài P Đã đăng → P vào hàng chờ; 10:00 bật lại → tạo embedding cho P, P ra khỏi hàng chờ. Bài Q lỗi cả hai lần thử → Q vào hàng chờ. P bị sửa lúc 9:45 khi còn trong hàng chờ → embedding tạo theo nội dung đã sửa. |
| BR-M13-27 | Ràng buộc | Kết quả tóm tắt đầu tiên của một bài được giữ tạm 24 giờ kể từ lúc tạo và dùng chung cho mọi người yêu cầu bài đó. Kết quả bị bỏ khi đủ 24 giờ, khi tiêu đề hoặc nội dung chữ thay đổi, hoặc khi bài còn dưới 300 từ. Kết quả thất bại không được giữ. | An yêu cầu lúc 20:00 ngày 10/10 → kết quả giữ tới trước 20:00 ngày 11/10. Bình yêu cầu lúc 20:05 → nhận kết quả của An, không gọi AI. An bấm lại 20 lần → không gọi AI. Tác giả sửa nội dung lúc 21:00 → kết quả bị bỏ; Bình yêu cầu lúc 21:10 → gọi AI lại. Chi yêu cầu lúc 20:30 ngày 11/10 (kết quả 21:10 còn hạn) → dùng kết quả 21:10. |
| BR-M13-28 | Ràng buộc | Nội dung gửi cho AI tóm tắt là tiêu đề và nội dung chữ của bài; không gồm tệp đính kèm và bình chọn. Tóm tắt luôn hiển thị kèm ghi chú "Tóm tắt chưa bao gồm nội dung tệp đính kèm". | — |
| BR-M13-29 | Tính toán | Tỷ lệ Topic gợi ý được giữ lại = tổng số Topic AI gợi ý mà tác giả giữ lại ÷ tổng số Topic AI gợi ý, trên các phản hồi gợi ý Topic được ghi trong khoảng thời gian chọn (Hôm nay, 7 ngày, 30 ngày, Toàn thời gian; giờ Việt Nam). Khoảng không có phản hồi nào thì không có tỷ lệ. | Ba phản hồi: {Toán, Vật lý, Hóa} → chọn {Toán, Hóa} (giữ 2/3); {Ngữ văn} → {Ngữ văn, Lịch sử} (giữ 1/1); {Tin học, Toán} → {Tin học, Toán} (giữ 2/2): tỷ lệ = 5/6 ≈ 83,3%. Phản hồi ghi lúc 23:30 ngày 10/10 giờ Việt Nam thuộc "Hôm nay" khi xem trong ngày 10/10. Khoảng "Hôm nay" chưa có phản hồi → không có dữ liệu. |

### 5.12 Dữ liệu nghiệp vụ

| Thực thể | Thuộc tính nguồn đã nêu | Quan hệ |
|---|---|---|
| Nhật ký quyết định AI | Loại lời gọi (chấm điểm kiểm duyệt, embedding bài, gợi ý Topic); thành công hay thất bại; đầu ra thô | Gắn với một bài viết hoặc một bình luận; qua đó với tài khoản tác giả (tra cứu theo username kể cả khi DELETED) |
| Embedding bài viết | (Biểu diễn tiêu đề, nội dung chữ của bài; không có thuộc tính nghiệp vụ khác) | Thuộc một bài viết Đã đăng (M03); mỗi bài một embedding |
| Hàng chờ tạo bù embedding | Các bài Đã đăng đang thiếu embedding theo nội dung hiện tại | Mỗi mục là một bài viết (M03) |
| Kết quả tóm tắt đang giữ | Nội dung tóm tắt; thời điểm tạo | Thuộc một bài viết từ 300 từ (M03); mỗi bài tối đa một kết quả đang giữ |
| Tỷ lệ Topic gợi ý được giữ lại | Giá trị tỷ lệ theo khoảng thời gian | Tính từ phản hồi gợi ý Topic (M05); hiển thị ở M15 |
| Phản hồi gợi ý Topic (M05) | Các Topic AI gợi ý, các Topic tác giả chọn cuối, thời điểm ghi | Thuộc một lượt gợi ý Topic của một bài (M05) |
| Công tắc AI (M10) | Công tắc tổng; công tắc riêng Search, Moderation, Topic suggestion; bật hoặc tắt | Thuộc cấu hình hệ thống (M10) |

**Ma trận CRUD:**

| Thực thể | Tạo | Đọc | Sửa | Xóa |
|---|---|---|---|---|
| Nhật ký quyết định AI | FR-M13-08.01, FR-M13-08.04 | FR-M13-09.01, FR-M13-09.03, M09 | Không có (FR-M13-08.07, BR-M13-22) | Không có (FR-M13-08.07, BR-M13-22) |
| Embedding bài viết | FR-M13-03.01, FR-M13-03.10 | FR-M13-03.07, M06 | FR-M13-03.02, FR-M13-03.03 | Không có (bài viết chỉ xóa mềm, giữ toàn bộ dữ liệu — M03) |
| Hàng chờ tạo bù embedding | FR-M13-03.08, FR-M13-03.09 | FR-M13-03.10 | Không có (mục chỉ được thêm vào hoặc lấy ra) | FR-M13-03.10 |
| Kết quả tóm tắt đang giữ | FR-M13-06.02 | FR-M13-06.03, FR-M13-07.01 | Không có (bỏ rồi tạo mới, BR-M13-27) | FR-M13-06.04, FR-M13-06.05 |
| Tỷ lệ Topic gợi ý được giữ lại | FR-M13-10.01, FR-M13-10.02 | FR-M13-10.04, M15 | Không có (tính lại từ dữ liệu) | Không có (tính lại từ dữ liệu) |
| Phản hồi gợi ý Topic (M05) | M05 | FR-M13-10.01 | Không có (FR-M05) | Không có (FR-M05; giữ cả khi tài khoản bị xóa) |
| Công tắc AI (M10) | M10 | FR-M13-01.02, FR-M13-01.03, FR-M13-01.09 | M10 | M10 |

### 5.13 Chuyển trạng thái

Nguồn không nêu trạng thái cho thực thể nào của M13. Bật, tắt của công tắc AI thuộc M10. AI lỗi tạm thời không phải
một trạng thái (BR-M13-07). Hàng chờ tạo bù embedding và kết quả tóm tắt đang giữ chỉ có thêm vào và bỏ đi, không có
trạng thái riêng (xem CRUD).

### 5.14 Giao tiếp với module khác

| Hướng | Module | Nội dung ở mức nghiệp vụ | Yêu cầu |
|---|---|---|---|
| Dùng | M01 | Username giữ lại của tài khoản DELETED để nhật ký AI vẫn tra cứu được; trang chính sách công bố nội dung được nhà cung cấp dịch vụ AI xử lý | FR-M13-08.08, FR-M13-09.03 |
| Cung cấp | M03 | Điểm quét, nhóm vi phạm, khoảng điểm của bài; báo AI tắt hoặc lời gọi thất bại; nút và nội dung tóm tắt trên bài | FR-M13-02.08, FR-M13-01.02, FR-M13-01.06, FR-M13-07.01, FR-M13-07.02 |
| Dùng | M03 | Bài viết cần quét (tiêu đề, nội dung chữ, bình chọn, ảnh); mốc Đã đăng và các lần sửa tiêu đề, nội dung chữ; vai trò tác giả (Admin không quét) | FR-M13-02.01, FR-M13-02.11, FR-M13-03.01, FR-M13-03.02, FR-M13-06.05 |
| Cung cấp | M04 | Điểm quét bình luận để M04, M08 hiển thị, ẩn bình luận | FR-M13-02.08 |
| Cung cấp | M05 | Các Topic AI gợi ý; báo AI tắt hoặc lời gọi thất bại | FR-M13-05.02, FR-M13-05.03, FR-M13-05.04 |
| Dùng | M05 | Yêu cầu gợi ý Topic hợp lệ (đã qua giới hạn 10 lần / 60 giây và ngưỡng 20 từ); phản hồi gợi ý Topic để đánh giá chất lượng | FR-M13-05.01, FR-M13-10.01 |
| Cung cấp | M06 | Embedding của bài và của truy vấn; báo AI tắt hoặc lời gọi thất bại để M06 tìm full-text | FR-M13-03.07, FR-M13-04.01, FR-M13-04.02, FR-M13-04.03 |
| Dùng | M06 | Truy vấn tìm bài của người dùng đã đăng nhập; giới hạn tần suất tìm kiếm | FR-M13-04.01, FR-M13-01.08 |
| Cung cấp | M08 | Điểm quét, nhóm vi phạm, khoảng điểm cho nhánh cảnh cáo và mục do AI tạo; bản ghi thất bại khi quét bình luận lỗi ("ghi lỗi cho Admin") | FR-M13-02.05, FR-M13-02.06, FR-M13-02.08, FR-M13-08.09 |
| Dùng | M08 | Kích hoạt quét luồng bình luận theo tốc độ trả lời | FR-M13-02.03 |
| Cung cấp | M09 | Nhật ký quyết định AI của bài bị AI tự từ chối cho người xét khiếu nại | FR-M13-09.01 |
| Dùng | M10 | Công tắc AI tổng và công tắc Search, Moderation, Topic suggestion; ngưỡng là hằng số, không chỉnh qua giao diện | FR-M13-01.02, FR-M13-01.03, FR-M13-01.09, FR-M13-02.14 |
| Cung cấp | M11 | Điểm quét của bài trong nhóm, dùng cùng ngưỡng trước cổng duyệt của nhóm | FR-M13-02.08 |
| Cung cấp | M15 | Tỷ lệ Topic gợi ý được giữ lại theo khoảng thời gian M15 định nghĩa (Hôm nay; 7 ngày, 30 ngày theo ngày lịch; Toàn thời gian), không có giá trị khi khoảng không có phản hồi, cho bảng thống kê Nội dung (chỉ Admin); cách hiển thị thuộc M15 | FR-M13-10.02, FR-M13-10.03, FR-M13-10.04 |
| Cung cấp | M16 | Không chấm điểm tin nhắn chat | FR-M13-02.12 |

### 5.15 AI hỗ trợ và hành vi khi tắt AI

- Cả module là lớp AI. Năm năng lực: chấm điểm kiểm duyệt (FR-M13-02), embedding cho tìm kiếm ngữ nghĩa (FR-M13-03,
  FR-M13-04), gợi ý Topic (FR-M13-05), tóm tắt bài theo yêu cầu (FR-M13-06, FR-M13-07), đánh giá chất lượng gợi ý
  Topic (FR-M13-10) (FR-M13-01.10). AI chỉ tự xử lý ở khoảng điểm cao; không ban, không cộng trừ điểm, không trao badge,
  không tự viết nội dung (FR-M13-02.09, FR-M13-01.12).
- Khi AI tắt: công tắc tổng tắt thì không có lời gọi AI nào; công tắc riêng tắt thì không có lời gọi loại đó; module gọi
  được báo AI đang tắt để dùng cách thay thế của mình (FR-M13-01.02, FR-M13-01.03, FR-M13-02.13, FR-M13-04.02,
  FR-M13-05.04). Bài Đã đăng lúc tắt vào hàng chờ tạo bù embedding (FR-M13-03.08). Nút "Tóm tắt" vẫn hiện, bấm thì báo
  bận ngay (FR-M13-07.06, FR-M13-07.07). Đổi công tắc có hiệu lực ngay, không cần triển khai lại (FR-M13-01.09).
- Khi AI lỗi tạm thời: thời gian chờ 5 giây (kiểm duyệt, embedding), 10 giây (gợi ý Topic, tóm tắt); thử lại một lần sau
  2 giây; thất bại thì báo module gọi, không đổi công tắc (FR-M13-01.04 đến FR-M13-01.07). Embedding bài lỗi vào hàng chờ
  tạo bù (FR-M13-03.09); tóm tắt lỗi báo bận, không giữ kết quả (FR-M13-06.07, FR-M13-07.05).
- Lời gọi chấm điểm, embedding bài, gợi ý Topic, kể cả lời gọi thất bại, được ghi vào nhật ký quyết định AI (FR-M13-08.01).

### 5.16 Yêu cầu HMI

Chưa có — chờ giai đoạn thiết kế.

### 5.17 Chuyển màn hình

Chưa có — chờ giai đoạn thiết kế.

## 6. Lịch sử sửa đổi

| Phiên bản | Ngày | Nội dung | Người sửa |
|---|---|---|---|
| 0.1 | 2026-10-18 | Tạo mới | Phạm Văn Đức |
| 1.0 | 2026-10-19 | Chốt sau 7 bước; câu trả lời ghi vào register (DEC-203–207) | Phạm Văn Đức |
| 1.1 | 2026-10-20 | Đối chiếu với FR-M06: FR-M13-04.04 khớp DEC-208; ghi chuỗi DEC-208–213 ở C.2; không đổi yêu cầu. Chốt bản 1.1 | Phạm Văn Đức |
| 1.2 | 2026-10-24 | Đối chiếu với FR-M15: dòng Cung cấp M15 nêu rõ M13 tính tỷ lệ theo khoảng thời gian M15 định nghĩa và không có giá trị khi khoảng không có phản hồi; cách hiển thị thuộc M15; sửa mục 3.2; không đổi yêu cầu. Chốt bản 1.2 | Phạm Văn Đức |

## Phụ lục A. Truy vết

| ID | Nguồn | Căn cứ | Ghi chú |
|---|---|---|---|
| FR-M13-01 | DEC-099, DEC-008, DEC-093, DG-6, DG-7, DM-x04, QA-002, QA-024, MR-M13 | Nói thẳng | — |
| FR-M13-01.01 | DG-6, DG-7, DEC-008, QA-002 | Nói thẳng | — |
| FR-M13-01.02 | DEC-093, DEC-008, DEC-099 | Suy ra | DEC-093: công tắc tổng "overrides everything OFF"; DEC-099: khi tắt mỗi module dùng cách thay thế của mình ⇒ module gọi phải biết AI đang tắt |
| FR-M13-01.03 | DEC-093, DEC-205, DEC-099 | Nói thẳng | — |
| FR-M13-01.04 | DEC-099, DEC-206 | Nói thẳng | — |
| FR-M13-01.05 | DEC-099, DEC-206 | Nói thẳng | — |
| FR-M13-01.06 | DEC-099, DEC-161, DEC-205, DEC-206 | Nói thẳng | — |
| FR-M13-01.07 | DEC-099 | Nói thẳng | — |
| FR-M13-01.08 | DEC-100, DEC-144, DEC-063, DEC-206 | Nói thẳng | — |
| FR-M13-01.09 | DEC-008, DEC-092 | Nói thẳng | — |
| FR-M13-01.10 | DEC-006, DG-6, DM-x02, QA-024, DEC-203 | Nói thẳng | — |
| FR-M13-01.11 | DG-8, DM-x03, DM-11 | Nói thẳng | — |
| FR-M13-01.12 | DM-11, DG-8, DM-x03, DEC-078 | Nói thẳng | — |
| FR-M13-02 | DEC-097, DEC-098, DEC-186, DEC-204, DM-11.1, QA-017, DEC-013, DEC-161, DEC-185, DEC-077, DEC-195, MR-M13 | Nói thẳng | — |
| FR-M13-02.01 | DEC-013, DEC-161, DEC-185, DEC-204, DM-11.1, QA-017 | Nói thẳng | — |
| FR-M13-02.02 | DEC-204, DEC-160 | Nói thẳng | — |
| FR-M13-02.03 | DEC-077, DEC-204, QA-017, DM-11.1 | Nói thẳng | — |
| FR-M13-02.04 | DEC-097 | Nói thẳng | — |
| FR-M13-02.05 | DEC-186 | Nói thẳng | — |
| FR-M13-02.06 | DEC-204 | Nói thẳng | — |
| FR-M13-02.07 | DEC-098, DEC-186 | Nói thẳng | — |
| FR-M13-02.08 | DEC-098, DEC-104 | Nói thẳng | — |
| FR-M13-02.09 | DEC-005, DM-11, DG-5, DEC-098, DEC-078 | Nói thẳng | — |
| FR-M13-02.10 | DEC-097 | Nói thẳng | — |
| FR-M13-02.11 | DEC-195 | Nói thẳng | — |
| FR-M13-02.12 | QA-217 | Nói thẳng | — |
| FR-M13-02.13 | DEC-093, DEC-185, DEC-013 | Nói thẳng | — |
| FR-M13-02.14 | DEC-090 | Nói thẳng | — |
| FR-M13-02.15 | DEC-099, DEC-161 | Nói thẳng | — |
| FR-M13-03 | DEC-095, DEC-205, QA-037, DEC-053 | Nói thẳng | — |
| FR-M13-03.01 | DEC-205, DEC-095 | Nói thẳng | — |
| FR-M13-03.02 | DEC-205, DEC-095 | Nói thẳng | — |
| FR-M13-03.03 | DEC-095 | Suy ra | DEC-095: "computed once at publish", "recomputed if content edited" ⇒ mỗi bài một embedding, bản tính lại thay bản cũ |
| FR-M13-03.04 | DEC-205 | Nói thẳng | — |
| FR-M13-03.05 | DEC-205 | Nói thẳng | — |
| FR-M13-03.06 | QA-037, DEC-053 | Nói thẳng | — |
| FR-M13-03.07 | DEC-053, DEC-055 | Nói thẳng | — |
| FR-M13-03.08 | DEC-205, DEC-093 | Nói thẳng | — |
| FR-M13-03.09 | DEC-205, DEC-099 | Nói thẳng | — |
| FR-M13-03.10 | DEC-205 | Nói thẳng | — |
| FR-M13-04 | DM-11.3, DEC-053, DEC-099 | Suy ra | DM-11.3 nêu luồng "Query → Embedding API → Vector Search"; DEC-099 nêu thời gian chờ của embedding và tìm full-text cho riêng truy vấn bị lỗi ⇒ M13 tạo embedding cho truy vấn, M06 tìm và xếp hạng |
| FR-M13-04.01 | DM-11.3, DEC-053, DEC-093, DEC-205 | Suy ra | DM-11.3 nêu luồng "Query → Embedding API → Vector Search"; DEC-099 nêu thời gian chờ embedding và tìm full-text cho riêng truy vấn bị lỗi ⇒ M13 tạo embedding cho truy vấn, M06 tìm và xếp hạng |
| FR-M13-04.02 | DEC-093, DEC-099, DEC-053, MR-FB-M06 | Nói thẳng | — |
| FR-M13-04.03 | DEC-099 | Nói thẳng | — |
| FR-M13-04.04 | QA-011 | Nói thẳng | QA-011: Guest "Semantic Search: Không". Đã đối chiếu với FR-M06: khớp DEC-208 (Guest tìm bài bằng full-text, FR-M06-02.23) |
| FR-M13-05 | DEC-096, DEC-099, DEC-050, DEC-132, DEC-144, DM-11.2 | Nói thẳng | Phía người dùng của gợi ý Topic thuộc M05 |
| FR-M13-05.01 | DEC-050, DEC-093, DM-11.2 | Nói thẳng | — |
| FR-M13-05.02 | DEC-132, DEC-144, DEC-050 | Nói thẳng | — |
| FR-M13-05.03 | DEC-099, MR-FB-M05 | Nói thẳng | — |
| FR-M13-05.04 | DEC-093, DEC-008 | Nói thẳng | — |
| FR-M13-05.05 | DEC-140 | Nói thẳng | — |
| FR-M13-06 | DEC-206, DM-11.4, QA-007, DG-6, DM-x02, GL:Summarization | Nói thẳng | — |
| FR-M13-06.01 | DEC-206 | Nói thẳng | — |
| FR-M13-06.02 | DEC-206 | Nói thẳng | — |
| FR-M13-06.03 | DEC-206 | Nói thẳng | — |
| FR-M13-06.04 | DEC-206 | Nói thẳng | — |
| FR-M13-06.05 | DEC-206 | Nói thẳng | — |
| FR-M13-06.06 | DEC-206 | Nói thẳng | — |
| FR-M13-06.07 | DEC-206 | Nói thẳng | — |
| FR-M13-06.08 | DEC-206, DM-11.4 | Nói thẳng | — |
| FR-M13-06.09 | QA-007 | Nói thẳng | — |
| FR-M13-06.10 | DEC-206 | Nói thẳng | — |
| FR-M13-06.11 | DEC-206 | Nói thẳng | — |
| FR-M13-07 | DEC-206, QA-011, DM-11.4 | Nói thẳng | — |
| FR-M13-07.01 | DEC-206, GL:Summarization, DM-11.4 | Nói thẳng | — |
| FR-M13-07.02 | DEC-206 | Nói thẳng | — |
| FR-M13-07.03 | DEC-206, QA-011 | Nói thẳng | — |
| FR-M13-07.04 | DEC-206 | Nói thẳng | — |
| FR-M13-07.05 | DEC-206 | Nói thẳng | Câu chữ cụ thể chốt khi thiết kế |
| FR-M13-07.06 | DEC-206 | Nói thẳng | — |
| FR-M13-07.07 | DEC-206 | Nói thẳng | — |
| FR-M13-07.08 | DM-x04, DEC-206 | Suy ra | Phần lõi không phụ thuộc cứng vào AI (DM-x04) và tóm tắt chỉ có khi được yêu cầu (DEC-206) ⇒ việc đọc bài không phụ thuộc tóm tắt |
| FR-M13-08 | DEC-133, DEC-207, DEC-156, DEC-129 | Nói thẳng | — |
| FR-M13-08.01 | DEC-133, DEC-207 | Nói thẳng | — |
| FR-M13-08.02 | DEC-133, DEC-207 | Nói thẳng | — |
| FR-M13-08.03 | DEC-133 | Nói thẳng | — |
| FR-M13-08.04 | DEC-207 | Nói thẳng | — |
| FR-M13-08.05 | DEC-207, DEC-206 | Nói thẳng | — |
| FR-M13-08.06 | DEC-133 | Nói thẳng | — |
| FR-M13-08.07 | DEC-207, DEC-129, OPEN-008 | Nói thẳng | — |
| FR-M13-08.08 | DEC-156 | Nói thẳng | — |
| FR-M13-08.09 | DEC-207, DEC-099 | Nói thẳng | — |
| FR-M13-09 | DEC-133, DEC-156, DEC-198, DEC-207 | Nói thẳng | — |
| FR-M13-09.01 | DEC-198, DEC-133, DEC-207 | Nói thẳng | — |
| FR-M13-09.02 | DEC-133, DEC-156, DEC-207 | Suy ra | Nguồn chỉ nêu Mod, Admin dùng nhật ký (DEC-133, DEC-156) và chỉ khi xét khiếu nại (DEC-207); tác giả bài bị từ chối chỉ thấy nhóm vi phạm (DEC-166) ⇒ Guest, User bị từ chối |
| FR-M13-09.03 | DEC-156 | Nói thẳng | — |
| FR-M13-09.04 | DEC-207 | Nói thẳng | — |
| FR-M13-10 | DEC-203, DM-11.5, GL:Feedback / Evaluation Loop, DG-6, DG-7, QA-017, DEC-050, DEC-159 | Nói thẳng | — |
| FR-M13-10.01 | DEC-203, DEC-159, QA-017, DEC-050, DEC-142 | Nói thẳng | — |
| FR-M13-10.02 | DEC-203, DEC-127 | Nói thẳng | — |
| FR-M13-10.03 | DEC-203 | Suy ra | Tỷ lệ chia cho tổng số Topic gợi ý; tổng bằng 0 thì tỷ lệ không xác định ⇒ không có giá trị để hiển thị. Cách hiển thị thuộc M15 |
| FR-M13-10.04 | DEC-203 | Nói thẳng | — |
| FR-M13-10.05 | DEC-203 | Nói thẳng | — |
| FR-M13-10.06 | DEC-203 | Nói thẳng | — |
| FR-M13-10.07 | DM-11.5, GL:Feedback / Evaluation Loop, DEC-203 | Nói thẳng | — |
| BR-M13-01 | DEC-005, DM-11, DG-5, DEC-098, DEC-078 | Nói thẳng | — |
| BR-M13-02 | DM-11, DG-8, DM-x03, DEC-078 | Nói thẳng | — |
| BR-M13-03 | DG-6, DG-8, DM-x03, DM-11 | Nói thẳng | — |
| BR-M13-04 | DEC-006, DG-6, DM-x02, QA-007, DEC-203 | Nói thẳng | — |
| BR-M13-05 | QA-002, QA-007, DM-x04, DEC-008, QA-024 | Nói thẳng | — |
| BR-M13-06 | DEC-093, DEC-205, DEC-206, DEC-008, DEC-185, DEC-013, DEC-099 | Nói thẳng | — |
| BR-M13-07 | DEC-099 | Nói thẳng | — |
| BR-M13-08 | DEC-099, DEC-206 | Suy ra | Nguồn ghi "timeout 5s/10s"; "chưa có kết quả khi hết thời gian chờ thì lần thử lỗi" là cách hiểu timeout |
| BR-M13-09 | DEC-099, DEC-206 | Nói thẳng | — |
| BR-M13-10 | DEC-099, DEC-161, DEC-205, DEC-206, DEC-207, MR-FB-M06, MR-FB-M05 | Nói thẳng | — |
| BR-M13-11 | DEC-097 | Nói thẳng | — |
| BR-M13-12 | DEC-186, DEC-204 | Nói thẳng | — |
| BR-M13-13 | DEC-098, DEC-186 | Nói thẳng | — |
| BR-M13-14 | DEC-090, DEC-203 | Nói thẳng | — |
| BR-M13-15 | DEC-098, DEC-104 | Nói thẳng | — |
| BR-M13-16 | DEC-195, QA-217 | Nói thẳng | — |
| BR-M13-17 | DEC-095, QA-037 | Nói thẳng | — |
| BR-M13-18 | DEC-095, DEC-205 | Nói thẳng | — |
| BR-M13-19 | DEC-100, DEC-144, DEC-063, DEC-206 | Nói thẳng | — |
| BR-M13-20 | DEC-206, QA-007, DM-11.4 | Nói thẳng | — |
| BR-M13-21 | DEC-133, DEC-207 | Nói thẳng | — |
| BR-M13-22 | DEC-129, DEC-156, DEC-207, OPEN-008 | Nói thẳng | — |
| BR-M13-23 | DEC-050, DEC-159, QA-017, DEC-203 | Nói thẳng | — |
| BR-M13-24 | DEC-203, DM-11.5, GL:Feedback / Evaluation Loop | Nói thẳng | — |
| BR-M13-25 | DEC-204, DEC-160 | Nói thẳng | — |
| BR-M13-26 | DEC-205, DEC-206 | Nói thẳng | — |
| BR-M13-27 | DEC-206 | Nói thẳng | — |
| BR-M13-28 | DEC-206 | Nói thẳng | — |
| BR-M13-29 | DEC-203, DEC-127 | Nói thẳng | — |

## Phụ lục B. Câu hỏi, giả định và TBD

### B.1 Câu hỏi đã hỏi

| Mã | Loại | Câu hỏi | Trả lời | Ghi vào register |
|---|---|---|---|---|
| Q-01 | Mâu thuẫn | Vòng phản hồi đánh giá AI gồm những gì: chỉ phản hồi ngầm từ gợi ý Topic (QA-017: "không cần UI riêng"), hay cả đánh giá dự đoán của AI kiểm duyệt (DM-11.5: Mod / Trusted User đánh dấu đúng/sai; DEC-133: nhật ký AI để chỉnh ngưỡng 0,9/0,5)? Đề xuất A: cả hai, đều ngầm — Topic từ lựa chọn cuối của tác giả, kiểm duyệt từ kết luận Mod đã ra trên nội dung AI xử lý; không thêm thao tác đánh dấu đúng/sai. | Chỉ đánh giá gợi ý Topic, từ phản hồi gợi ý của M05. Không đánh giá AI kiểm duyệt, không có thao tác đánh dấu đúng/sai, không có "Trusted User". Chỉnh ngưỡng do đội phát triển đọc nhật ký AI. Stakeholder lúc đầu muốn bỏ hẳn, sau khi xem hệ quả: "giữ cho phần phản hồi topic". | QA-384, DEC-203 |
| Q-02 | Thiếu chi tiết | Tóm tắt bài viết được tạo khi nào: tự động khi bài "đủ dài", hay khi có người yêu cầu ("hoặc user yêu cầu", DM-11.4)? Nếu có yêu cầu thì vai trò nào được yêu cầu (Guest xem được tóm tắt theo QA-011)? Bổ sung ở bước 4: bài "đủ dài" là bao nhiêu (đếm theo đơn vị nào); bài đã có tóm tắt được sửa thì tóm tắt có tạo lại không; bài bị xóa thì tóm tắt xử lý thế nào. | Tóm tắt theo yêu cầu, không lưu lâu dài: chỉ người đã đăng nhập; Guest bấm thì được nhắc đăng nhập; bài từ 300 từ; kết quả giữ tạm dùng chung 24 giờ, bỏ khi tiêu đề, nội dung chữ thay đổi; không giới hạn tần suất riêng. | QA-389, DEC-206 |
| Q-03 | Cần cân nhắc | Mở rộng phạm vi: Ngoài lúc xét khiếu nại bài bị AI từ chối (DEC-198), Mod, Admin có tra cứu nhật ký quyết định AI ở chỗ khác không (DEC-156: "so MOD/ADMIN can investigate")? Lỗi khi quét bình luận "log error for admin" (DEC-099) được Admin xem ở đâu? | Không có chỗ tra cứu nào ngoài lúc xét khiếu nại (câu mở rộng phạm vi — không chấp nhận). Lỗi quét bình luận "ghi cho Admin" là bản ghi thất bại trong nhật ký AI. | QA-391, QA-392, DEC-207 |
| Q-04 | Thiếu chi tiết | Ai xem các chỉ số chất lượng AI (Accuracy, Precision, Recall, F1, dương tính giả, âm tính giả — DM-11.5) và xem ở đâu (trong M13, hay trong trang thống kê của M15)? | Admin xem ở bảng thống kê Nội dung của M15, dùng bộ lọc thời gian của M15. | QA-385, DEC-203 |
| Q-05 | Thiếu chi tiết | Công tắc Search (DEC-093) có điều khiển cả việc tạo embedding khi bài được đăng không; tóm tắt theo công tắc nào (DEC-093 không có công tắc riêng cho tóm tắt)? Bài đăng trong lúc AI tắt không có embedding, tóm tắt: khi bật lại có tạo bù không (DEC-013 chỉ nói không quét bù kiểm duyệt)? | Embedding bài và truy vấn theo công tắc tổng và Search; tóm tắt chỉ theo công tắc tổng. Bài thiếu embedding vào hàng chờ tạo bù. Tóm tắt không lưu nên không tạo bù. | QA-388, QA-389, DEC-205, DEC-206 |
| Q-06 | Thiếu chi tiết | DEC-099 chưa nêu thời gian chờ của tóm tắt, và chưa nêu cách xử lý khi tạo embedding bài hoặc tóm tắt thất bại sau hai lần thử (bài vẫn đăng nhưng không tìm được theo ngữ nghĩa? có thử lại sau không?). | Tóm tắt: 10 giây mỗi lần thử, thử lại một lần, hằng số đổi qua triển khai; thất bại báo "hệ thống đang bận", không giữ kết quả. Embedding bài thất bại → hàng chờ tạo bù. | QA-388, QA-390, DEC-205, DEC-206 |
| Q-07 | Mơ hồ | Hai nhóm vi phạm cùng có điểm cao nhất (ví dụ Quấy rối 0,92 và Bạo lực 0,92) thì nhóm nào được ghi làm lý do (DEC-186 chỉ nói "that category")? | Lấy nhóm đứng trước theo thứ tự Quấy rối → Thù ghét → Người lớn → Bạo lực. | QA-392, DEC-204 |
| Q-08 | Mơ hồ | Embedding được tạo ở mốc nào: lúc gửi bài, cùng với quét trước (bài có thể bị từ chối sau đó), hay lúc bài Đã đăng (DEC-095: "at publish time (or alongside pre-scan)")? "Sửa nhiều" (recomputed if content edited significantly) là thế nào — mọi lần sửa tiêu đề, nội dung như cờ "gợi ý cũ" của M05, hay một mức thay đổi nào đó? Embedding của bài bị xóa hẳn xử lý thế nào? Bài của Admin (không qua quét trước, DEC-195) có embedding không? | Tạo khi bài chuyển sang Đã đăng (mọi đường, gồm bài của Admin); tạo lại mỗi lần tiêu đề hoặc nội dung chữ thay đổi. Bài bị xóa vẫn giữ toàn bộ dữ liệu (FR-M03), không cần hỏi. | QA-387, DEC-205 |
| Q-09 | Thiếu chi tiết | Phạm vi nhật ký quyết định AI (DEC-133 liệt kê kiểm duyệt, embedding, gợi ý Topic): có ghi lời gọi tóm tắt và embedding truy vấn (không gắn bài nào) không; ghi mỗi lời gọi hay mỗi lần thử, có ghi lời gọi thất bại không; một lần quét luồng bình luận ghi một bản ghi hay mỗi bình luận một bản ghi; bản ghi có được sửa không? | Ghi chấm điểm kiểm duyệt, embedding bài, gợi ý Topic; không ghi tóm tắt, embedding truy vấn. Mỗi lời gọi một bản ghi kể cả thất bại; quét luồng: mỗi bình luận một bản ghi; không sửa, không xóa. | QA-392, DEC-207 |
| Q-10 | Mơ hồ | Accuracy, Precision, Recall, F1 (DM-11.5) tính thế nào và theo khoảng thời gian nào? Ví dụ gợi ý {Toán, Vật lý}, tác giả chọn {Toán, Hóa}: tính theo từng Topic (1 đúng, 1 gợi ý thừa, 1 bỏ sót) hay theo cả lượt gợi ý (đúng/sai)? Với kiểm duyệt, lấy kết luận nào làm "đúng" (phụ thuộc Q-01)? | Một chỉ số: tỷ lệ Topic gợi ý được giữ lại; theo bộ lọc M15, xếp theo lúc ghi phản hồi, giờ Việt Nam. Không tính Precision, Recall, F1, Accuracy. | QA-385, QA-392, DEC-203 |
| Q-11 | Thiếu chi tiết | Phần nào của bài viết được gửi tới AI kiểm duyệt: tiêu đề, nội dung chữ, ảnh, tệp đính kèm? (Gợi ý Topic chỉ gửi tiêu đề và nội dung chữ, không gồm tệp đính kèm — DEC-050; nguồn chưa nói với kiểm duyệt.) | Tiêu đề, nội dung chữ, bình chọn và ảnh đính kèm; không gửi tài liệu đính kèm. | QA-386, DEC-204 |

### B.2 TBD

| ID | Nội dung | Ảnh hưởng | Lý do chưa chốt |
|---|---|---|---|
| TBD-M13-01 | Ngân sách AI cho MS1 (ước tính dưới 0,01 USD cho quy mô demo, đề xuất nạp 5 USD) | Thấp | OPEN-001 hoãn có chủ đích |

### B.3 Cần cân nhắc (ngoài dữ liệu hiện có)

| Mã | Điểm cần cân nhắc | Vì sao cần | Quyết định |
|---|---|---|---|

## Phụ lục C. Sổ nguồn

**Owner keywords:** M13, AI Layer, lớp AI, AI Assistance, AI provider, AI Provider API, nhà cung cấp dịch vụ AI, AI service provider, OpenAI, embedding, embeddings, Embedding API, text-embedding-3-small, pgvector, HNSW, vector, GPT-4o-mini, LLM, Moderation API, confidence, confidence threshold, threshold, thresholds, ngưỡng, Content Gate, timeout, timeouts, retry, transient failure, AI failure, AI-off, AI off, AI_ENABLED, AI master, master toggle, per-module toggle, AI toggle, fallback, fallbacks, ai_decision_log, raw output, raw response, hallucination, whitelist, Summarization, AI Summary, summarize, tóm tắt, Feedback, Evaluation, Evaluation Loop, accuracy, precision, recall, F1, F1-score, False Positive, False Negative, asynchronous, bất đồng bộ, fine-tune, chatbot, RAG, Related Posts, AI budget, AI cost, AI decision log, AI decision logs, nhật ký AI, nhật ký quyết định AI, Human-in-the-loop, AI features, AI Classification, AI Moderation, master AI, Moderation switch, scan failure, AI lỗi, re-enable, Full-text keyword search, Manual moderation queue only, không có gợi ý AI, AI-scanned, quét AI
**Dependency keywords:** post, bài viết, comment, bình luận, search, tìm kiếm, semantic search, topic, chủ đề, Topic Suggestion, Topic Suggest, gợi ý, pre-scan, auto-scan, post-scan, velocity, auto-warn, auto-reject, auto-hide, warning, cảnh cáo, moderation queue, mod review, report, báo cáo, appeal, khiếu nại, Content Deletion Appeal, admin, system config, audit log, Privacy Policy, ToS, is_stale, rate limit, AI, timezone, notification, PENDING, FLAGGED
**Mục draft của module:** DM-11 (gồm DM-11.1–11.5), DM-13, DG-6, DG-7
**Loại khỏi bảng nguồn (khớp nhầm):** DEC-069, ISS-102, QA-131 (thử lại khi đẩy thông báo, M07); DEC-088, ISS-105, DEC-115 (hết thời gian nhận vụ, M08, M09); DEC-114, ISS-143, QA-192, QA-195, QA-040, QA-047, GL:Badge (ngưỡng điểm của badge, M12); DEC-120 ("fraud vector" — gian lận bình chọn, M12); DEC-130, ISS-192, QA-251 (danh sách định dạng tệp được tải lên); ISS-175, QA-235 (ngưỡng vào Trending, M14); QA-012 (ngưỡng uy tín để làm Mod); DG-x01 ("bản tóm tắt" là tài liệu, không phải tóm tắt bằng AI)

### C.1 Bảng nguồn

| Nguồn | Nhãn | Trạng thái | Dùng ở | Ghi chú |
|---|---|---|---|---|
| DEC-095 | Sở hữu | Sửa một phần bởi DEC-205 | BR-M13-17, BR-M13-18, FR-M13-03.01, FR-M13-03.02, FR-M13-03.03 | Nhóm A. Embedding bài viết: tính một lần khi đăng (cùng lúc quét trước), tính lại khi nội dung sửa nhiều. Tên mô hình, cách lưu là chi tiết công nghệ, không đưa vào FR. DEC-205: tạo khi Đã đăng, tạo lại mỗi lần tiêu đề, nội dung chữ đổi; hàng chờ tạo bù |
| DEC-096 | Nhắc tới | Hiện hành | FR-M13-05 | Nhóm A. Chỉ chọn mô hình cho gợi ý Topic (chi tiết công nghệ) |
| DEC-097 | Sở hữu | Sửa một phần bởi DEC-204 | BR-M13-11, FR-M13-02.04, FR-M13-02.10 | Nhóm A. AI kiểm duyệt chỉ phát hiện 4 nhóm (Quấy rối, Thù ghét, Người lớn, Bạo lực); Spam, đạo văn, sai lệch chỉ qua báo cáo. DEC-204: nội dung gửi kiểm duyệt; thứ tự nhóm khi cùng điểm |
| DEC-098 | Sở hữu | Sửa một phần bởi DEC-161, DEC-166, DEC-186, DEC-195 | BR-M13-01, BR-M13-13, BR-M13-15, FR-M13-02.07, FR-M13-02.08, FR-M13-02.09 | Nhóm A. Một lần quét cho hai nhánh (cổng nội dung, cảnh cáo), cặp ngưỡng 0,9/0,5 dùng chung, giá trị tạm. Hệ quả từng nhánh thuộc M03, M04, M08. FR-M08 đã ghi Sở hữu cho DEC-098 — ranh giới cần xác nhận. DEC-161: quét lại bài đã sửa ≥ 0,5 → Bị gắn cờ, không tự từ chối; DEC-166: bài bị từ chối (M03); DEC-186: điểm = cao nhất 4 nhóm, không theo mức cảnh cáo, AI không tự cảnh cáo Mod/Admin; DEC-195: nội dung Admin không quét |
| DEC-099 | Sở hữu | Sửa một phần bởi DEC-205, DEC-206, DEC-207 | BR-M13-06, BR-M13-07, BR-M13-08, BR-M13-09, BR-M13-10, FR-M13-01.02, FR-M13-01.03, FR-M13-01.04, FR-M13-01.05, FR-M13-01.06, FR-M13-01.07, FR-M13-02.15, FR-M13-03.09, FR-M13-04.02, FR-M13-04.03, FR-M13-05.03, FR-M13-08.09 | Nhóm A. Phân biệt AI tắt chủ đích và AI lỗi tạm thời; thời gian chờ 5 giây / 10 giây; đúng 1 lần thử lại sau 2 giây. Xử lý khi hết lượt thử thuộc từng module (M03, M05, M06, M08). Thêm xử lý lỗi embedding bài, tóm tắt; "log error for admin" = bản ghi thất bại |
| DEC-100 | Sở hữu | Sửa một phần bởi DEC-144 | BR-M13-19, FR-M13-01.08 | Nhóm A. Không có hệ thống giới hạn tần suất riêng cho AI; quét do hệ thống kích hoạt không cần giới hạn. Giới hạn nút gợi ý Topic thuộc M05 |
| DG-6 | Sở hữu | Sửa một phần bởi DEC-097, DEC-140, QA-007, DEC-203, DEC-206 | BR-M13-03, BR-M13-04, FR-M13-01.01, FR-M13-01.10, FR-M13-06, FR-M13-10 | Nhóm A. Draft: 5 năng lực AI bắt buộc; API bên thứ ba, lớp tách riêng, bất đồng bộ, có fallback; vòng phản hồi chỉnh ngưỡng, không train lại. Spam không do AI phát hiện; AI không gợi ý Tag, không có Mod duyệt; tóm tắt chỉ cho bài (sửa không có dấu) |
| DG-7 | Sở hữu | Hiện hành | FR-M13-01.01, FR-M13-10 | Nhóm A. Draft: AI Layer gọi API bên thứ ba, bất đồng bộ, fallback khi lỗi hoặc hết thời gian chờ, vòng phản hồi đo độ chính xác |
| DM-11 | Sở hữu | Sửa một phần bởi DEC-098 | BR-M13-01, BR-M13-02, BR-M13-03, FR-M13-01.11, FR-M13-01.12, FR-M13-02.09 | Nhóm A. Draft: AI chỉ là lớp hỗ trợ; không tự quyết tuyệt đối với case nhạy cảm, không chọn Accepted Answer, không cộng/trừ điểm; không xây hay fine-tune model. Như DEC-005. DEC-169 (ngoài bảng nguồn): không có Accepted Answer ở MS1 |
| DM-11.1 | Sở hữu | Sửa một phần bởi DEC-077, DEC-097, DEC-098, DEC-204 | FR-M13-02.01, FR-M13-02.03 | Nhóm A. Draft: gọi AI kiểm duyệt bài, bình luận, trả dự đoán + độ tin cậy. Quyết định đăng/xét/từ chối thuộc M03, M04, M08. Spam, quảng cáo không do AI phát hiện; bình luận quét theo tốc độ trả lời (sửa không có dấu) |
| DM-11.2 | Phụ thuộc | Sửa một phần bởi DEC-050, DEC-140 | FR-M13-05.01 | Nhóm A. Draft: gợi ý Topic/Tag thuộc M05 (phần Tag đã bị DEC-140 bỏ); M13 thực hiện lời gọi AI. AI không gợi ý Tag, không có Mod duyệt |
| DM-11.3 | Phụ thuộc | Hiện hành | FR-M13-04.01 | Nhóm A. Draft: tìm kiếm ngữ nghĩa thuộc M06; M13 tạo embedding cho câu truy vấn và bài viết |
| DM-11.4 | Sở hữu | Sửa một phần bởi QA-007, DEC-206 | BR-M13-20, FR-M13-06.08, FR-M13-07.01 | Nhóm A. Draft: tóm tắt bài dài và luồng bình luận dài, chỉ khi đủ dài hoặc người dùng yêu cầu. QA-007 nói chỉ cho bài (đối chiếu ở bước 2). Tóm tắt luồng bình luận bị bỏ (QA > draft). Tóm tắt theo yêu cầu, bài từ 300 từ |
| DM-11.5 | Sở hữu | Sửa một phần bởi DEC-203 | BR-M13-24, FR-M13-10.07 | Nhóm A. Draft: vòng phản hồi — Mod/người dùng tin cậy đánh giá đúng/sai; đo Accuracy, Precision, Recall, F1, FP, FN; Related Posts ngoài phạm vi. Q-01. Bỏ Mod / Trusted User đánh dấu đúng/sai và các chỉ số; chỉ còn tỷ lệ Topic gợi ý được giữ lại |
| DM-13 | Nhắc tới | Hiện hành | Không áp dụng: Sơ đồ kiến trúc: AI Layer gồm Moderation, Classification, Embedding, Summarization, Feedback gọi AI Provider API; không quy định hành vi | Nhóm A. Sơ đồ kiến trúc: AI Layer gồm Moderation, Classification, Embedding, Summarization, Feedback gọi AI Provider API; không quy định hành vi |
| ISS-124 | Nhắc tới | Trùng với DEC-095 | — | Nhóm A. Câu hỏi đã có DEC-095 trả lời |
| ISS-125 | Nhắc tới | Trùng với DEC-096 | — | Nhóm A. Câu hỏi đã có DEC-096 trả lời |
| ISS-126 | Nhắc tới | Trùng với DEC-097 | — | Nhóm A. Câu hỏi đã có DEC-097 trả lời |
| ISS-127 | Nhắc tới | Trùng với DEC-098 | — | Nhóm A. Câu hỏi đã có DEC-098 trả lời |
| ISS-128 | Nhắc tới | Trùng với DEC-099 | — | Nhóm A. Câu hỏi đã có DEC-099 trả lời |
| ISS-129 | Nhắc tới | Trùng với DEC-100 | — | Nhóm A. Câu hỏi đã có DEC-100 trả lời |
| QA-167 | Nhắc tới | Trùng với DEC-095 | — | Nhóm A. Chọn mô hình embedding (chi tiết công nghệ) |
| QA-168 | Nhắc tới | Trùng với DEC-095 | — | Nhóm A. Nơi lưu embedding (chi tiết công nghệ) |
| QA-169 | Nhắc tới | Trùng với DEC-096 | — | Nhóm A. Chọn mô hình gợi ý Topic (chi tiết công nghệ) |
| QA-170 | Sở hữu | Trùng với DEC-097 | — | Nhóm A. AI kiểm duyệt không phủ mọi lý do báo cáo |
| QA-171 | Sở hữu | Trùng với DEC-098 | — | Nhóm A. Điểm ≥ 0,9: AI tự từ chối bài / tự ẩn bình luận, không qua Mod |
| QA-172 | Sở hữu | Trùng với DEC-098 | — | Nhóm A. Cổng nội dung và cảnh cáo dùng chung ngưỡng 0,9/0,5 |
| QA-173 | Sở hữu | Trùng với DEC-098 | — | Nhóm A. Ngưỡng là giá trị tạm, cần chỉnh theo dữ liệu thật |
| QA-174 | Sở hữu | Trùng với DEC-099 | — | Nhóm A. AI tắt dùng fallback của module; AI lỗi là giảm cấp theo từng yêu cầu, có thử lại |
| QA-175 | Sở hữu | Trùng với DEC-099 | — | Nhóm A. Thời gian chờ: kiểm duyệt, embedding 5 giây; gợi ý Topic 10 giây |
| QA-176 | Sở hữu | Trùng với DEC-099 | — | Nhóm A. Đúng 1 lần thử lại, tuần tự, chờ 2 giây |
| QA-177 | Phụ thuộc | Trùng với DEC-099 | — | Nhóm A. M03: quét trước khi đăng lỗi → giữ chờ Mod xét, không tự đăng |
| QA-178 | Sở hữu | Trùng với DEC-100 | — | Nhóm A. Không có hệ thống giới hạn riêng cho AI; giới hạn mới chỉ cho nút gợi ý Topic (M05) |
| MR-M13 | Sở hữu | Sửa một phần bởi DEC-205, DEC-206 | FR-M13-01, FR-M13-02 | Nhóm A. Dòng module: 4 nhóm kiểm duyệt, ngưỡng 0,9/0,5 hai nhánh, thời gian chờ 5s/10s + 1 lần thử lại, AI tắt khác AI lỗi, fallback theo module. Cột MoSCoW lệch (đọc từ MoSCoW Summary) |
| DEC-005 | Sở hữu | Sửa một phần bởi DEC-098 | BR-M13-01, FR-M13-02.09 | Nhóm B. AI chỉ là lớp hỗ trợ, có người trong vòng quyết định; không tự quyết với case nhạy cảm. DEC-098 cho AI tự từ chối bài, tự ẩn bình luận, tự cảnh cáo khi điểm ≥ 0,9 mà không qua Mod (sửa không có dấu) |
| DEC-006 | Sở hữu | Hiện hành | BR-M13-04, FR-M13-01.10 | Nhóm B. Cả 5 năng lực AI là bắt buộc |
| DEC-008 | Sở hữu | Sửa một phần bởi DEC-093, DEC-099 | BR-M13-05, BR-M13-06, FR-M13-01.01, FR-M13-01.02, FR-M13-01.09, FR-M13-05.04 | Nhóm B. Công tắc AI toàn cục; mỗi module có fallback khi AI tắt (fallback cụ thể thuộc M05, M06, M08); nơi đổi công tắc thuộc M10 (DEC-092/093). DEC-093: hai tầng công tắc ở M10; DEC-099: Moderation tắt thì nội dung đăng thẳng, chỉ dựa vào báo cáo |
| DEC-013 | Phụ thuộc | Sửa một phần bởi DEC-161, DEC-195 | BR-M13-06, FR-M13-02.01, FR-M13-02.13 | Nhóm B. M03: AI tắt thì bỏ quét, bài đăng ngay; không quét bù khi bật lại AI |
| DEC-050 | Phụ thuộc | Sửa một phần bởi DEC-142, DEC-144 | BR-M13-23, FR-M13-05.01, FR-M13-05.02, FR-M13-10.01 | Nhóm B. M05: phản hồi (gợi ý so với lựa chọn cuối) chỉ ghi khi gợi ý chưa cũ — đầu vào đánh giá AI |
| DEC-053 | Phụ thuộc | Hiện hành | FR-M13-03.06, FR-M13-03.07, FR-M13-04.01, FR-M13-04.02 | Nhóm B. M06: tìm bài bằng embedding; full-text khi tắt AI |
| DEC-055 | Phụ thuộc | Hiện hành | FR-M13-03.07 | Nhóm B. M06: xếp hạng dùng độ tương đồng embedding |
| DEC-057 | Nhắc tới | Hiện hành | Không áp dụng: M06: kỹ thuật tìm full-text dự phòng | Nhóm B. M06: kỹ thuật tìm full-text dự phòng |
| DEC-077 | Phụ thuộc | Sửa một phần bởi DEC-186, DEC-195 | FR-M13-02.03 | Nhóm B. M08: điều kiện kích hoạt quét AI luồng bình luận. DEC-180, DEC-190 (ngoài bảng nguồn) chỉ sửa phần hiển thị bình luận ẩn và vụ chờ xét |
| DEC-078 | Phụ thuộc | Sửa một phần bởi DEC-186 | BR-M13-01, BR-M13-02, FR-M13-01.12, FR-M13-02.09 | Nhóm B. M08: AI tự cảnh cáo khi tin cậy cao; AI không bao giờ ban |
| DEC-090 | Phụ thuộc | Hiện hành | BR-M13-14, FR-M13-02.14 | Nhóm B. M10: ngưỡng là hằng số chính sách, không chỉnh qua giao diện, đổi qua triển khai. DEC-141 (ngoài bảng nguồn) chỉ sửa phần Topic |
| DEC-092 | Phụ thuộc | Hiện hành | FR-M13-01.09 | Nhóm B. M10: cấu hình hệ thống có công tắc AI. DEC-152 (ngoài bảng nguồn) chỉ sửa phần bảo trì, đăng ký |
| DEC-093 | Phụ thuộc | Sửa một phần bởi DEC-205 | BR-M13-06, FR-M13-01.02, FR-M13-01.03, FR-M13-02.13, FR-M13-03.08, FR-M13-04.01, FR-M13-04.02, FR-M13-05.01, FR-M13-05.04 | Nhóm B. M10: công tắc tổng + công tắc riêng cho Search, Moderation, Topic suggestion (không có công tắc riêng cho tóm tắt). DEC-205: Search điều khiển cả embedding bài; tóm tắt không có công tắc riêng |
| DEC-104 | Phụ thuộc | Hiện hành | BR-M13-15, FR-M13-02.08 | Nhóm B. M11: bài trong nhóm dùng cùng ngưỡng 0,9/0,5 với cổng duyệt nhóm |
| DEC-125 | Nhắc tới | Hiện hành | Không áp dụng: M14 bỏ phụ thuộc M13; không có feed cá nhân hóa bằng AI | Nhóm B. M14 bỏ phụ thuộc M13; không có feed cá nhân hóa bằng AI |
| DEC-131 | Phụ thuộc | Sửa một phần bởi DEC-154 | Chuyển M01 | Nhóm B. Chuyển M01: trang chính sách công bố nội dung được dịch vụ AI xử lý. DEC-146 (ngoài bảng nguồn) thêm công bố gợi ý Topic |
| DEC-132 | Phụ thuộc | Sửa một phần bởi DEC-144 | FR-M13-05.02 | Nhóm B. M05: kết quả gợi ý ngoài danh mục Topic coi như gợi ý thất bại (FR-M05 đã ghi Sở hữu). DEC-141 (ngoài bảng nguồn) đối chiếu danh mục Topic hiện tại |
| DEC-133 | Sở hữu | Sửa một phần bởi DEC-156, DEC-198, DEC-207 | BR-M13-21, FR-M13-08.01, FR-M13-08.02, FR-M13-08.03, FR-M13-08.06, FR-M13-09.01, FR-M13-09.02 | Nhóm B. Nhật ký quyết định AI: ghi đầu ra thô mỗi lần gọi (kiểm duyệt, embedding, gợi ý Topic), gắn bài/bình luận; để chỉnh ngưỡng và làm căn cứ khiếu nại. DEC-156: giữ khi tài khoản DELETED, gắn qua username; DEC-198: khiếu nại bài bị AI từ chối là loại "bài", người xét xem nhật ký AI (sửa không có dấu). DEC-207: đơn vị ghi, phạm vi, bất biến, chỉ xem khi khiếu nại |
| DEC-134 | Nhắc tới | Hiện hành | Không áp dụng: Công nghệ backend/frontend | Nhóm B. Công nghệ backend/frontend |
| DEC-137 | Nhắc tới | Hiện hành | Không áp dụng: Công nghệ đã chốt, gồm nhà cung cấp AI (không đưa vào FR) | Nhóm B. Công nghệ đã chốt, gồm nhà cung cấp AI (không đưa vào FR) |
| DEC-140 | Phụ thuộc | Hiện hành | FR-M13-05.05 | Nhóm B. M05: AI chỉ gợi ý Topic, không gợi ý Tag; không có Mod duyệt kết quả gợi ý |
| DEC-142 | Phụ thuộc | Hiện hành | FR-M13-10.01 | Nhóm B. M05: gợi ý khi sửa bài đã gửi, cùng quy tắc ghi phản hồi |
| DEC-154 | Phụ thuộc | Hiện hành | Chuyển M01 | Nhóm B. M01: trang chính sách ghi "nhà cung cấp dịch vụ AI", không nêu tên |
| DEC-156 | Phụ thuộc | Sửa một phần bởi DEC-159 | BR-M13-22, FR-M13-08.08, FR-M13-09.02, FR-M13-09.03 | Nhóm B. M01: nhật ký quyết định AI giữ lại khi tài khoản DELETED, gắn qua username để Mod/Admin tra cứu |
| DEC-159 | Phụ thuộc | Hiện hành | BR-M13-23, FR-M13-10.01 | Nhóm B. M01/M05: phản hồi gợi ý Topic giữ lại để M13 đánh giá chất lượng AI, không còn danh tính |
| DEC-161 | Phụ thuộc | Sửa một phần bởi DEC-185 | BR-M13-10, FR-M13-01.06, FR-M13-02.01, FR-M13-02.15 | Nhóm B. M03: quét lại khi sửa bài đã đăng; AI lỗi thì giữ nguyên, bài vẫn hiện |
| DEC-185 | Phụ thuộc | Hiện hành | BR-M13-06, FR-M13-02.01, FR-M13-02.13 | Nhóm B. M03: không quét khi công tắc AI tổng hoặc Moderation tắt |
| DEC-186 | Phụ thuộc | Sửa một phần bởi DEC-195, DEC-204 | BR-M13-12, BR-M13-13, FR-M13-02.05, FR-M13-02.07 | Nhóm B. M08: điểm quét = điểm cao nhất trong 4 nhóm; một cặp ngưỡng cho mọi người. Định nghĩa điểm quét nằm giữa M08 và M13 — ranh giới cần xác nhận. DEC-204: hai nhóm cùng điểm cao nhất. Cạnh lineage DEC-097 → DEC-186 là khớp nhầm (DEC-097 chỉ được nhắc tên trong dấu sửa của DEC-204) |
| DEC-195 | Phụ thuộc | Hiện hành | BR-M13-16, FR-M13-02.11 | Nhóm B. M03/M04/M08: bài, bình luận của Admin không qua quét AI |
| DEC-198 | Phụ thuộc | Hiện hành | FR-M13-09.01 | Nhóm B. M09: người xét khiếu nại bài bị AI từ chối xem nhật ký quyết định AI |
| DG-1 | Nhắc tới | Hiện hành | Không áp dụng: Giới thiệu dự án có lớp AI hỗ trợ | Nhóm B. Giới thiệu dự án có lớp AI hỗ trợ |
| DG-4 | Nhắc tới | Hiện hành | Không áp dụng: Bản đồ module | Nhóm B. Bản đồ module |
| DG-5 | Phụ thuộc | Sửa một phần bởi DEC-098 | BR-M13-01, FR-M13-02.09 | Nhóm B. Nguyên tắc chung: con người quyết định cuối, AI chỉ gợi ý; AI kiểm duyệt không tự quyết tuyệt đối với case nhạy cảm. Như DEC-005. DEC-169 (ngoài bảng nguồn): không có Accepted Answer ở MS1 |
| DG-8 | Sở hữu | Hiện hành | BR-M13-02, BR-M13-03, FR-M13-01.11, FR-M13-01.12 | Nhóm B. Không làm: AI tự viết bài/bình luận, tự quyết điểm/badge/Accepted Answer, chatbot/RAG, multi-agent, train/fine-tune |
| DM-5.3 | Nhắc tới | Hiện hành | Không áp dụng: M11: nhóm dùng chung AI Moderation của Forum | Nhóm B. M11: nhóm dùng chung AI Moderation của Forum |
| DM-x02 | Sở hữu | Sửa một phần bởi QA-007, DEC-125, DEC-206 | BR-M13-04, FR-M13-01.10, FR-M13-06 | Nhóm B. Draft phạm vi: AI Content Moderation, Classification, Semantic Search, Summarization (Post + Comment-thread), Feedback/Evaluation Loop. Tóm tắt chỉ cho bài; feed không cá nhân hóa bằng AI |
| DM-x03 | Sở hữu | Hiện hành | BR-M13-02, BR-M13-03, FR-M13-01.11, FR-M13-01.12 | Nhóm B. Draft ngoài phạm vi: Related Posts, AI tự viết, AI tự quyết điểm/badge/Accepted Answer, chatbot/RAG, train/fine-tune |
| DM-x04 | Sở hữu | Hiện hành | BR-M13-05, FR-M13-01, FR-M13-07.08 | Nhóm B. Draft nguyên tắc kiến trúc: core không phụ thuộc cứng AI; nhà cung cấp AI thay được; fallback khi lỗi; tác vụ chậm chạy bất đồng bộ |
| GL:AI Assistance Layer | Sở hữu | Hiện hành | Không áp dụng: thuật ngữ ở mục 2.1 | Nhóm B. Thuật ngữ: 5 năng lực AI bắt buộc, hỗ trợ chứ không thay quyết định của người |
| GL:AI Classification | Phụ thuộc | Sửa một phần bởi DEC-140 | Chuyển M05 | Nhóm B. Thuật ngữ M05 (đã sửa bởi DEC-140) |
| GL:AI Moderation | Phụ thuộc | Sửa một phần bởi DEC-097, DEC-204 | Chuyển M08 | Nhóm B. Thuật ngữ M08: trả dự đoán + độ tin cậy. Spam không do AI phát hiện |
| GL:Feedback / Evaluation Loop | Sở hữu | Sửa một phần bởi DEC-203 | BR-M13-24, FR-M13-10.07 | Nhóm B. Thuật ngữ: theo dõi độ chính xác AI theo thời gian để chỉnh ngưỡng, không train lại. Chỉ đánh giá gợi ý Topic; không chỉnh ngưỡng kiểm duyệt bằng chỉ số |
| GL:Semantic Search | Phụ thuộc | Hiện hành | Chuyển M06 | Nhóm B. Thuật ngữ M06 |
| GL:Summarization | Sở hữu | Sửa một phần bởi QA-007, DEC-206 | FR-M13-06, FR-M13-07.01 | Nhóm B. Thuật ngữ: tóm tắt bài dài hoặc luồng bình luận dài. Tóm tắt luồng bình luận bị bỏ |
| GL:iShare | Nhắc tới | Hiện hành | Không áp dụng: Tên nền tảng | Nhóm B. Tên nền tảng |
| GL:pgvector | Nhắc tới | Hiện hành | Không áp dụng: Thuật ngữ công nghệ | Nhóm B. Thuật ngữ công nghệ |
| ISS-026 | Nhắc tới | Hiện hành | Không áp dụng: Câu hỏi ngân sách AI → QA-007, OPEN-001 | Nhóm B. Câu hỏi ngân sách AI → QA-007, OPEN-001. Register vẫn ghi Open; xem OPEN-001 |
| ISS-042 | Nhắc tới | Trùng với QA-024 | — | Nhóm B. Câu hỏi MoSCoW M13 → QA-024 |
| ISS-089 | Nhắc tới | Trùng với DEC-057 | — | Nhóm B. M06: full-text dự phòng |
| ISS-107 | Nhắc tới | Trùng với DEC-077 | — | Nhóm B. M08: quét bình luận, đã có DEC-077 |
| ISS-108 | Nhắc tới | Trùng với DEC-078 | — | Nhóm B. M08: cảnh cáo AI, đã có DEC-078 |
| ISS-121 | Nhắc tới | Trùng với DEC-092 | — | Nhóm B. M10: danh sách cấu hình, đã có DEC-092 |
| ISS-122 | Nhắc tới | Trùng với DEC-093 | — | Nhóm B. M10: mức chi tiết công tắc AI, đã có DEC-093 |
| ISS-159 | Phụ thuộc | Trùng với QA-217 | — | Nhóm B. M16: không có AI kiểm duyệt cho tin nhắn chat |
| ISS-160 | Nhắc tới | Hiện hành | Không áp dụng: M16: quấy rối qua tin nhắn khi không có AI kiểm duyệt | Nhóm B. M16: quấy rối qua tin nhắn khi không có AI kiểm duyệt |
| ISS-170 | Nhắc tới | Hiện hành | Không áp dụng: M14: không còn feed cá nhân hóa cần AI | Nhóm B. M14: không còn feed cá nhân hóa cần AI |
| ISS-186 | Nhắc tới | Trùng với DEC-125 | — | Nhóm B. M14 bỏ phụ thuộc M13 |
| ISS-193 | Nhắc tới | Trùng với DEC-131 | — | Nhóm B. Câu hỏi đã có DEC-131 trả lời |
| ISS-194 | Nhắc tới | Trùng với DEC-132 | — | Nhóm B. Câu hỏi đã có DEC-132 trả lời |
| ISS-195 | Nhắc tới | Trùng với DEC-133 | — | Nhóm B. Câu hỏi đã có DEC-133 trả lời |
| ISS-200 | Nhắc tới | Trùng với DEC-008 | — | Nhóm B. Nơi lưu cờ AI, đã giải quyết bởi DEC-092/093 |
| ISS-203 | Nhắc tới | Trùng với DEC-137 | — | Nhóm B. Xác nhận công nghệ |
| ISS-207 | Nhắc tới | Trùng với DEC-140 | — | Nhóm B. M05: AI có gợi ý Tag không → DEC-140 |
| ISS-221 | Nhắc tới | Trùng với DEC-144 | — | Nhóm B. M05: ngưỡng 20 từ của gợi ý Topic → DEC-144 |
| ISS-263 | Nhắc tới | Trùng với DEC-161 | — | Nhóm B. M03: quét lại khi sửa và khi AI lỗi → DEC-161 |
| ISS-285 | Nhắc tới | Hiện hành | Không áp dụng: M04: bình luận bị ẩn, quét AI giữ như cũ → DEC-180 | Nhóm B. M04: bình luận bị ẩn, quét AI giữ như cũ → DEC-180 |
| ISS-292 | Nhắc tới | Trùng với DEC-186 | — | Nhóm B. M08: ngưỡng AI theo mức cảnh cáo → DEC-186 |
| ISS-306 | Nhắc tới | Trùng với DEC-186 | — | Nhóm B. M08: điểm quét, ngưỡng tốc độ → DEC-186, DEC-188 |
| ISS-311 | Nhắc tới | Trùng với DEC-195 | — | Nhóm B. M09: nội dung Admin không quét AI → DEC-195 |
| ISS-ADMN-01 | Nhắc tới | Hiện hành | Không áp dụng: M08 đã giải quyết bằng DEC-080, DEC-187 | Nhóm B. M08 backlog: ngưỡng số cảnh cáo để AI chuyển lên Mod (register còn Open; đối chiếu ở bước 2). Đã được M08 giải quyết bằng DEC-080, DEC-187 (ngoài bảng nguồn); không quy định hành vi M13 |
| ISS-AI-01 | Sở hữu | Bị thay bởi DEC-098 | — | Nhóm B. Hiệu chỉnh ngưỡng độ tin cậy AI kiểm duyệt (register còn Open, Blocker; DEC-098 đặt giá trị tạm — đối chiếu ở bước 2). DEC-098 đặt ngưỡng tạm; việc chỉnh theo dữ liệu thật thuộc vòng đánh giá AI |
| OPEN-001 | Sở hữu | Hiện hành | TBD-M13-01 | Nhóm B. Ngân sách AI chưa chốt (hoãn có chủ đích) → TBD. TBD-M13-01 |
| OPEN-002 | Nhắc tới | Hiện hành | Không áp dụng: Tech stack, đã đóng (DEC-137) | Nhóm B. Tech stack, đã đóng (DEC-137) |
| OPEN-008 | Sở hữu | Sửa một phần bởi DEC-154, DEC-156 | BR-M13-22, FR-M13-08.07 | Nhóm B. Privacy: quan hệ giữa giữ nhật ký AI vĩnh viễn và xóa PII; đã chốt phần lớn bởi DEC-154–157, còn email liên hệ và bản sao dữ liệu. Phần liên quan M13 (giữ nhật ký AI khi xóa tài khoản) đã chốt bởi DEC-156; phần còn mở (email liên hệ, nhận bản sao dữ liệu) thuộc M01, không tạo TBD cho M13 |
| QA-001 | Nhắc tới | Hiện hành | Không áp dụng: Timeline MS1 gồm cả AI layer | Nhóm B. Timeline MS1 gồm cả AI layer |
| QA-002 | Sở hữu | Hiện hành | BR-M13-05, FR-M13-01.01 | Nhóm B. AI layer phải chạy live, xử lý thời gian thực với thao tác mới (dữ liệu demo có thể seed) |
| QA-004 | Nhắc tới | Hiện hành | Không áp dụng: Bối cảnh: học sinh hay hỏi AI; AI hỗ trợ, không thay cộng đồng | Nhóm B. Bối cảnh: học sinh hay hỏi AI; AI hỗ trợ, không thay cộng đồng |
| QA-007 | Sở hữu | Sửa một phần bởi DEC-206 | BR-M13-04, BR-M13-05, BR-M13-20, FR-M13-06.09 | Nhóm B. Tóm tắt chỉ cho bài, không cho luồng bình luận; AI chạy live; ước tính chi phí; ngân sách chưa chốt. Thắng draft về tóm tắt luồng bình luận (QA > draft); phần ngân sách → OPEN-001. Tóm tắt theo yêu cầu, không mỗi bài một tóm tắt |
| QA-008 | Nhắc tới | Hiện hành | Không áp dụng: Ghi chú: tích hợp AI cần xử lý lỗi, fallback khi AI không khả dụng | Nhóm B. Ghi chú: tích hợp AI cần xử lý lỗi, fallback khi AI không khả dụng |
| QA-011 | Sở hữu | Sửa một phần bởi DEC-206 | FR-M13-04.04, FR-M13-07.03 | Nhóm B. Guest xem được AI Summary và kết quả phân loại trên bài; Guest không dùng tìm kiếm ngữ nghĩa (M06). DEC-171 (ngoài bảng nguồn) chỉ sửa quyền Guest xem hồ sơ. Tóm tắt chỉ cho người đã đăng nhập |
| QA-016 | Phụ thuộc | Sửa một phần bởi DEC-104 | Chuyển M11 | Nhóm B. M11: bài trong nhóm qua AI kiểm duyệt trước, rồi tới hàng chờ Group Mod |
| QA-017 | Sở hữu | Sửa một phần bởi DEC-050, DEC-077, DEC-203 | BR-M13-23, FR-M13-02.01, FR-M13-02.03, FR-M13-10.01 | Nhóm B. Tác nhân hệ thống AI Moderation Worker, AI Classification Worker; vòng phản hồi chạy ngầm qua lựa chọn Topic cuối, không cần giao diện riêng. Q-01. Ngoài ra bị DEC-050 (gợi ý khi bấm nút) và DEC-077 (bình luận quét theo tốc độ) sửa một phần. Q-01 đã trả lời: DEC-203 chọn chỉ đánh giá gợi ý Topic |
| QA-019 | Phụ thuộc | Sửa một phần bởi DEC-078, DEC-186 | Chuyển M08 | Nhóm B. M08: AI được cảnh cáo, không ban, chuyển lên Mod khi đủ ngưỡng cảnh cáo. DEC-187, DEC-189 (ngoài bảng nguồn) sửa phần ban (M08) |
| QA-020 | Phụ thuộc | Sửa một phần bởi DEC-186 | Chuyển M08 | Nhóm B. M08: phác thảo ngưỡng AI theo mức cảnh cáo (DEC-186 đã bỏ — đối chiếu ở bước 2). Bỏ ngưỡng AI theo mức cảnh cáo. DEC-188 (ngoài bảng nguồn) sửa phần mức cảnh cáo (M08) |
| QA-022 | Phụ thuộc | Sửa một phần bởi DEC-053 | Chuyển M06 | Nhóm B. M06: tìm kiếm ngữ nghĩa cho bài, full-text khi tắt AI; M06 phụ thuộc M13 |
| QA-024 | Sở hữu | Hiện hành | BR-M13-05, FR-M13-01.10 | Nhóm B. M13 là Must, là lớp riêng, hạ tầng dùng chung cho M05, M06, M08; công tắc toàn cục bảo đảm giảm cấp khi tắt AI |
| QA-031 | Phụ thuộc | Hiện hành | Chuyển M03 | Nhóm B. M03: không quét bù khi bật lại AI; Admin cần được báo rõ khi bật lại |
| QA-035 | Nhắc tới | Sửa một phần bởi DEC-053 | Không áp dụng: M06: các chiến lược tìm kiếm | Nhóm B. M06: các chiến lược tìm kiếm. Nhóm, bình luận khác DEC-053 |
| QA-037 | Sở hữu | Sửa một phần bởi DEC-053 | BR-M13-17, FR-M13-03.06 | Nhóm B. Bình luận không có embedding, chỉ tìm full-text. Phần bình luận tìm full-text bị thay (bình luận không được tìm kiếm); không embedding bình luận còn hiệu lực |
| QA-104 | Phụ thuộc | Trùng với DEC-050 | — | Nhóm B. M05: phản hồi chỉ ghi khi gợi ý chưa cũ |
| QA-110 | Nhắc tới | Hiện hành | Không áp dụng: M06: tìm người dùng không dùng embedding | Nhóm B. M06: tìm người dùng không dùng embedding |
| QA-114 | Nhắc tới | Trùng với DEC-057 | — | Nhóm B. M06: kỹ thuật full-text dự phòng |
| QA-144 | Nhắc tới | Trùng với DEC-078 | — | Nhóm B. M08: AI tự cảnh cáo, trùng DEC-078 |
| QA-164 | Nhắc tới | Trùng với DEC-092 | — | Nhóm B. M10: danh sách cấu hình |
| QA-165 | Nhắc tới | Trùng với DEC-093 | — | Nhóm B. M10: công tắc tổng + riêng |
| QA-217 | Phụ thuộc | Hiện hành | BR-M13-16, FR-M13-02.12 | Nhóm B. M16: không có AI kiểm duyệt quét tin nhắn chat |
| QA-218 | Nhắc tới | Hiện hành | Không áp dụng: M16: câu hỏi quấy rối qua tin nhắn | Nhóm B. M16: câu hỏi quấy rối qua tin nhắn |
| QA-240 | Nhắc tới | Trùng với DEC-125 | — | Nhóm B. M14 bỏ phụ thuộc M13 |
| QA-252 | Nhắc tới | Trùng với DEC-131 | — | Nhóm B. Trả lời ISS-193 → DEC-131 (M01) |
| QA-253 | Nhắc tới | Trùng với DEC-132 | — | Nhóm B. Trả lời ISS-194 → DEC-132 (M05) |
| QA-254 | Sở hữu | Trùng với DEC-133 | — | Nhóm B. Nhật ký quyết định AI: mỗi lần gọi lưu đầu ra thô, tách khỏi nhật ký hành động của Mod/Admin |
| QA-259 | Nhắc tới | Trùng với DEC-008 | — | Nhóm B. Nơi lưu cờ AI: Admin Panel (M10) |
| QA-263 | Nhắc tới | Trùng với DEC-137 | — | Nhóm B. Xác nhận công nghệ |
| QA-267 | Nhắc tới | Trùng với DEC-140 | — | Nhóm B. M05: AI không gợi ý Tag |
| QA-281 | Nhắc tới | Trùng với DEC-144 | — | Nhóm B. M05: đếm 20 từ |
| QA-312 | Phụ thuộc | Trùng với DEC-156 | — | Nhóm B. M01: nhật ký AI của tài khoản đã xóa vẫn gắn qua username |
| QA-313 | Nhắc tới | Trùng với DEC-154 | — | Nhóm B. M01: cách ghi "nhà cung cấp dịch vụ AI" |
| QA-320 | Phụ thuộc | Trùng với DEC-159 | — | Nhóm B. M01/M05: phản hồi gợi ý của tài khoản đã xóa giữ lại như nhật ký AI, không còn danh tính |
| QA-323 | Phụ thuộc | Trùng với DEC-161 | — | Nhóm B. M03: quét lại khi sửa; AI lỗi thì bài vẫn hiện |
| QA-345 | Nhắc tới | Hiện hành | Không áp dụng: M04: giữ cách quét AI bình luận như cũ | Nhóm B. M04: giữ cách quét AI bình luận như cũ |
| QA-352 | Phụ thuộc | Trùng với DEC-186 | — | Nhóm B. M08: một cặp ngưỡng 0,9/0,5 cho mọi người |
| QA-366 | Phụ thuộc | Trùng với DEC-186 | — | Nhóm B. M08: điểm quét = điểm cao nhất trong 4 nhóm |
| QA-371 | Phụ thuộc | Trùng với DEC-195 | — | Nhóm B. M09: nội dung của Admin không qua quét AI |
| QA-376 | Phụ thuộc | Trùng với DEC-198 | — | Nhóm B. M09: người xét khiếu nại dựa vào nhật ký AI |
| MR-A02 | Nhắc tới | Trùng với DEC-125 | — | Nhóm B. Đợt sửa M14: bỏ phụ thuộc M13 |
| MR-A03 | Nhắc tới | Hiện hành | Không áp dụng: Đợt sửa M15; không quy định hành vi AI | Nhóm B. Đợt sửa M15; không quy định hành vi AI |
| MR-A04 | Nhắc tới | Hiện hành | Không áp dụng: Đợt sửa Phase 6: tóm tắt DEC-131–133 | Nhóm B. Đợt sửa Phase 6: tóm tắt DEC-131–133 |
| MR-A05 | Nhắc tới | Hiện hành | Không áp dụng: Đợt sửa tech stack | Nhóm B. Đợt sửa tech stack |
| MR-FB-M05 | Phụ thuộc | Hiện hành | BR-M13-10, FR-M13-05.03 | Nhóm B. Bảng fallback: M05 tự chọn Topic, không có gợi ý |
| MR-FB-M06 | Phụ thuộc | Hiện hành | BR-M13-10, FR-M13-04.02 | Nhóm B. Bảng fallback: M06 tìm full-text |
| MR-FB-M08 | Phụ thuộc | Sửa một phần bởi DEC-099 | Chuyển M08 | Nhóm B. Bảng fallback: M08 chỉ còn hàng chờ thủ công. "Hàng chờ thủ công" = nội dung đăng thẳng, chỉ dựa vào báo cáo |
| MR-M06 | Nhắc tới | Hiện hành | Không áp dụng: Dòng module M06 | Nhóm B. Dòng module M06 |
| MR-M10 | Phụ thuộc | Hiện hành | Chuyển M10 | Nhóm B. Dòng module M10: công tắc AI tổng + riêng |
| MR-M11 | Nhắc tới | Hiện hành | Không áp dụng: Dòng module M11 ghi phụ thuộc M13 | Nhóm B. Dòng module M11 ghi phụ thuộc M13 |
| MR-M14 | Nhắc tới | Hiện hành | Không áp dụng: Dòng module M14: bỏ phụ thuộc M13 | Nhóm B. Dòng module M14: bỏ phụ thuộc M13 |
| DEC-063 | Nhắc tới | Hiện hành | BR-M13-19, FR-M13-01.08 | Nhóm C. M06: giới hạn tần suất tìm kiếm mà DEC-100 dùng lại |
| DEC-144 | Phụ thuộc | Hiện hành | BR-M13-19, FR-M13-01.08, FR-M13-05.02 | Nhóm C. M05: giới hạn 10 lần / 60 giây; bỏ Topic ngoài danh mục, giữ Topic hợp lệ |
| DEC-166 | Phụ thuộc | Sửa một phần bởi DEC-198 | Chuyển M03 | Nhóm C. M03: bài bị AI tự từ chối — tác giả thấy nhóm vi phạm, gửi lại không giới hạn |
| DEC-127 | Phụ thuộc | Hiện hành | BR-M13-29, FR-M13-10.02 | Nhóm D. Dùng chung: múi giờ Asia/Ho_Chi_Minh cho mọi tính toán theo thời gian |
| DEC-128 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M13 | Nhóm D. Dùng chung; không quy định hành vi M13 |
| DEC-129 | Phụ thuộc | Sửa một phần bởi DEC-156 | BR-M13-22, FR-M13-08.07 | Nhóm D. Dùng chung: nhật ký giữ vĩnh viễn, không xóa cứng (OPEN-008 nêu gồm cả nhật ký AI) |
| DEC-135 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M13 | Nhóm D. Dùng chung; không quy định hành vi M13 |
| DEC-136 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M13 | Nhóm D. Dùng chung; không quy định hành vi M13 |
| DEC-138 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung (M01); không quy định hành vi M13 | Nhóm D. Dùng chung (M01); không quy định hành vi M13. DEC-155, DEC-157 (ngoài bảng nguồn) chỉ sửa phần đồng ý chính sách (M01) |
| ISS-189 | Nhắc tới | Trùng với DEC-127 | — | Nhóm D. Câu hỏi đã có DEC-127 trả lời |
| ISS-190 | Nhắc tới | Trùng với DEC-128 | — | Nhóm D. Câu hỏi đã có DEC-128 trả lời |
| ISS-191 | Nhắc tới | Trùng với DEC-129 | — | Nhóm D. Câu hỏi đã có DEC-129 trả lời |
| ISS-196 | Nhắc tới | Trùng với QA-255 | — | Nhóm D. Câu hỏi → OPEN-005 |
| ISS-197 | Nhắc tới | Trùng với DEC-134 | — | Nhóm D. Dùng chung; không quy định hành vi M13 |
| ISS-198 | Nhắc tới | Trùng với DEC-135 | — | Nhóm D. Dùng chung; ghi chú AI là request/response |
| ISS-199 | Nhắc tới | Trùng với DEC-136 | — | Nhóm D. Dùng chung; không quy định hành vi M13 |
| ISS-201 | Nhắc tới | Trùng với QA-260 | — | Nhóm D. Dùng chung; không quy định hành vi M13 |
| ISS-202 | Nhắc tới | Trùng với QA-261 | — | Nhóm D. Dùng chung; không quy định hành vi M13 |
| ISS-204 | Nhắc tới | Trùng với DEC-138 | — | Nhóm D. Dùng chung (M01); không quy định hành vi M13 |
| QA-248 | Phụ thuộc | Trùng với DEC-127 | — | Nhóm D. Dùng chung: múi giờ (trùng DEC-127) |
| QA-249 | Nhắc tới | Trùng với DEC-128 | — | Nhóm D. Dùng chung; không quy định hành vi M13 |
| QA-250 | Phụ thuộc | Trùng với DEC-129 | — | Nhóm D. Dùng chung: giữ nhật ký vĩnh viễn (trùng DEC-129) |
| QA-255 | Phụ thuộc | Hiện hành | Không áp dụng: không tạo yêu cầu riêng; xem lại khi chốt Q-10 | Nhóm D. Dùng chung: không có hạ tầng theo dõi sự kiện (OPEN-005) — đánh giá AI chỉ dựa trên dữ liệu đã có |
| QA-256 | Nhắc tới | Trùng với DEC-134 | — | Nhóm D. Dùng chung; không quy định hành vi M13 |
| QA-257 | Nhắc tới | Trùng với DEC-135 | — | Nhóm D. Dùng chung; ghi chú AI là request/response |
| QA-258 | Nhắc tới | Trùng với DEC-136 | — | Nhóm D. Dùng chung; không quy định hành vi M13 |
| QA-260 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M13 | Nhóm D. Dùng chung; không quy định hành vi M13 |
| QA-261 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M13 | Nhóm D. Dùng chung; không quy định hành vi M13 |
| QA-262 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M13 | Nhóm D. Dùng chung; không quy định hành vi M13 |
| QA-264 | Nhắc tới | Trùng với DEC-138 | — | Nhóm D. Dùng chung (M01); không quy định hành vi M13 |
| DEC-203 | Sở hữu | Hiện hành | BR-M13-04, BR-M13-14, BR-M13-23, BR-M13-24, BR-M13-29, FR-M13-01.10, FR-M13-10.01, FR-M13-10.02, FR-M13-10.03, FR-M13-10.04, FR-M13-10.05, FR-M13-10.06, FR-M13-10.07 | Nhóm A. Đánh giá chất lượng chỉ cho gợi ý Topic; một chỉ số; Admin xem ở M15 |
| DEC-204 | Sở hữu | Hiện hành | BR-M13-12, BR-M13-25, FR-M13-02.01, FR-M13-02.02, FR-M13-02.03, FR-M13-02.06 | Nhóm A. Nội dung gửi kiểm duyệt; hai nhóm cùng điểm cao nhất |
| DEC-205 | Sở hữu | Hiện hành | BR-M13-06, BR-M13-10, BR-M13-18, BR-M13-26, FR-M13-01.03, FR-M13-01.06, FR-M13-03.01, FR-M13-03.02, FR-M13-03.04, FR-M13-03.05, FR-M13-03.08, FR-M13-03.09, FR-M13-03.10, FR-M13-04.01 | Nhóm A. Embedding bài: mốc tạo, tạo lại, công tắc, hàng chờ tạo bù |
| DEC-206 | Sở hữu | Hiện hành | BR-M13-06, BR-M13-08, BR-M13-09, BR-M13-10, BR-M13-19, BR-M13-20, BR-M13-26, BR-M13-27, BR-M13-28, FR-M13-01.04, FR-M13-01.05, FR-M13-01.06, FR-M13-01.08, FR-M13-06.01, FR-M13-06.02, FR-M13-06.03, FR-M13-06.04, FR-M13-06.05, FR-M13-06.06, FR-M13-06.07, FR-M13-06.08, FR-M13-06.10, FR-M13-06.11, FR-M13-07.01, FR-M13-07.02, FR-M13-07.03, FR-M13-07.04, FR-M13-07.05, FR-M13-07.06, FR-M13-07.07, FR-M13-07.08, FR-M13-08.05 | Nhóm A. Tóm tắt theo yêu cầu, giữ tạm 24 giờ, người đã đăng nhập, bài từ 300 từ |
| DEC-207 | Sở hữu | Hiện hành | BR-M13-10, BR-M13-21, BR-M13-22, FR-M13-08.01, FR-M13-08.02, FR-M13-08.04, FR-M13-08.05, FR-M13-08.07, FR-M13-08.09, FR-M13-09.01, FR-M13-09.02, FR-M13-09.04 | Nhóm A. Nhật ký AI: phạm vi, đơn vị ghi, bất biến, ai xem |
| ISS-324 | Nhắc tới | Trùng với QA-384 | — | Nhóm A |
| ISS-325 | Nhắc tới | Trùng với QA-385 | — | Nhóm A |
| ISS-326 | Nhắc tới | Trùng với QA-386 | — | Nhóm A |
| ISS-327 | Nhắc tới | Trùng với QA-387 | — | Nhóm A |
| ISS-328 | Nhắc tới | Trùng với QA-388 | — | Nhóm A |
| ISS-329 | Nhắc tới | Trùng với QA-389 | — | Nhóm A |
| ISS-330 | Nhắc tới | Trùng với QA-390 | — | Nhóm A |
| ISS-331 | Nhắc tới | Trùng với QA-391 | — | Nhóm A |
| ISS-332 | Nhắc tới | Trùng với QA-392 | — | Nhóm A |
| QA-384 | Sở hữu | Trùng với DEC-203 | — | Nhóm A. Trả lời Q-01 |
| QA-385 | Sở hữu | Trùng với DEC-203 | — | Nhóm A. Trả lời Q-04 |
| QA-386 | Sở hữu | Trùng với DEC-204 | — | Nhóm A. Trả lời Q-11 |
| QA-387 | Sở hữu | Trùng với DEC-205 | — | Nhóm A. Trả lời Q-08 |
| QA-388 | Sở hữu | Trùng với DEC-205 | — | Nhóm A. Trả lời Q-05; phần tóm tắt bị DEC-206 thay |
| QA-389 | Sở hữu | Trùng với DEC-206 | — | Nhóm A. Trả lời Q-02 |
| QA-390 | Sở hữu | Trùng với DEC-206 | — | Nhóm A. Trả lời Q-06 |
| QA-391 | Sở hữu | Trùng với DEC-207 | — | Nhóm A. Trả lời Q-03 (mở rộng phạm vi, không chấp nhận) |
| QA-392 | Sở hữu | Trùng với DEC-207 | — | Nhóm A. Danh sách xác nhận; phần nhóm cùng điểm ở DEC-204, chỉ số ở DEC-203 |
| DEC-160 | Phụ thuộc | Hiện hành | BR-M13-25, FR-M13-02.02 | Nhóm C. M03: tài liệu đính kèm giữ, không quét mã độc; DEC-204 không gửi tài liệu cho AI |
| QA-243 | Phụ thuộc | Sửa một phần bởi DEC-203 | Chuyển M15 | Nhóm C. M15: chỉ số của bảng Nội dung; DEC-203 thêm tỷ lệ Topic gợi ý được giữ lại |
| MR-M15 | Phụ thuộc | Sửa một phần bởi DEC-203 | Chuyển M15 | Nhóm C. Dòng module M15: chỉ Admin, 3 bảng, bộ lọc thời gian có sẵn |

### C.2 Chuỗi quyết định

| Chuỗi | Nội dung hiện hành |
|---|---|
| DEC-005, DM-11, DG-5 → DEC-098, DEC-078 → DEC-186 | AI chỉ là lớp hỗ trợ. AI được tự từ chối bài mới, tự ẩn bình luận và tự cảnh cáo khi điểm ≥ 0,9, không qua Mod; người bị xử lý khiếu nại được (M09). AI không bao giờ ban, không tự cảnh cáo Mod (Admin quyết) và Admin. Ý "không tự chọn Accepted Answer" không còn đối tượng ở MS1 (DEC-169, ngoài bảng nguồn). |
| DEC-006, DG-6, DM-x02 → DEC-097, DEC-140, QA-007, DEC-125, DEC-203, DEC-206 | Năm năng lực AI bắt buộc: kiểm duyệt, phân loại (gợi ý Topic), tìm kiếm ngữ nghĩa, tóm tắt bài, đánh giá chất lượng gợi ý Topic. Kiểm duyệt không phát hiện Spam; phân loại chỉ gợi ý Topic, không gợi ý Tag, không có Mod duyệt; tóm tắt chỉ cho bài, theo yêu cầu; đánh giá chỉ cho gợi ý Topic; feed không cá nhân hóa bằng AI. |
| DM-11.1, GL:AI Moderation, QA-170 → DEC-097 → DEC-204 | AI kiểm duyệt chấm bốn nhóm: Quấy rối, Ngôn từ thù ghét, Nội dung người lớn, Bạo lực; Spam, quảng cáo, đạo văn/bản quyền, nội dung sai lệch chỉ qua báo cáo. Bài gửi tiêu đề, nội dung chữ, bình chọn và ảnh; không gửi tài liệu; bình luận gửi nội dung chữ. |
| ISS-AI-01, QA-020, QA-171–173 → DEC-098 → DEC-161, DEC-166, DEC-186, DEC-195, DEC-204; DEC-104 | Một lần quét cho hai nhánh. Điểm quét là điểm cao nhất trong bốn nhóm; nhiều nhóm cùng điểm cao nhất thì lấy theo thứ tự Quấy rối, Thù ghét, Người lớn, Bạo lực. Một cặp ngưỡng tạm 0,9 / 0,5 cho bài, bình luận và mọi tác giả (bỏ ngưỡng theo mức cảnh cáo); chỉnh do đội phát triển, qua triển khai. Cổng nội dung: bài mới ≥ 0,9 tự từ chối, 0,5–< 0,9 chờ Mod, < 0,5 đăng; bình luận ≥ 0,9 tự ẩn, 0,5–< 0,9 ẩn và chờ Mod; bài đã đăng sửa rồi quét lại ≥ 0,5 thì Bị gắn cờ, không tự từ chối. Cảnh cáo: ≥ 0,9 AI tự cảnh cáo mỗi nội dung một lần, 0,5–< 0,9 Mod quyết khi xét. Nội dung của Admin không quét. Bài trong nhóm dùng cùng ngưỡng, < 0,5 thì theo cổng duyệt của nhóm. |
| DEC-008, MR-FB-M05/M06/M08 → DEC-092 → DEC-152; DEC-093, DEC-099 → DEC-205, DEC-206; DEC-013, DEC-185 | Công tắc tổng (M10) tắt mọi AI; công tắc riêng Search, Moderation, Topic suggestion chỉ có tác dụng khi công tắc tổng bật; đổi lúc đang chạy. Search điều khiển cả embedding bài và embedding truy vấn; tóm tắt chỉ theo công tắc tổng. Khi tắt: tìm full-text (M06); tự chọn Topic, không có gợi ý (M05); không quét, nội dung đăng thẳng, chỉ dựa vào báo cáo (M03, M08); bài Đã đăng vào hàng chờ tạo bù embedding; nút tóm tắt vẫn hiện, bấm thì báo bận ngay. Bật lại không quét bù kiểm duyệt nhưng có tạo bù embedding. DEC-152 (ngoài bảng nguồn) chỉ sửa phần bảo trì, tạm dừng đăng ký của DEC-092, không chạm M13. |
| DEC-099, QA-174–177 → DEC-161, DEC-185, DEC-205, DEC-206, DEC-207 | AI lỗi tạm thời là giảm cấp theo từng yêu cầu, không đổi trạng thái AI. Thời gian chờ 5 giây (kiểm duyệt, embedding), 10 giây (gợi ý Topic, tóm tắt); thử lại đúng một lần, tuần tự, sau 2 giây. Hết lượt: tìm full-text cho truy vấn đó; gợi ý Topic báo lỗi không chặn; quét trước khi đăng → chờ Mod, không tự đăng; quét lại bài đã sửa → giữ nguyên, bài vẫn hiện; quét bình luận → giữ nguyên, bản ghi thất bại trong nhật ký AI là "lỗi ghi cho Admin"; embedding bài → hàng chờ tạo bù; tóm tắt → báo hệ thống đang bận, không giữ kết quả. |
| DEC-100, QA-178 → DEC-144; DEC-063; DEC-206 | Không có hệ thống giới hạn tần suất riêng cho AI. Quét, embedding bài do hệ thống kích hoạt không giới hạn; tóm tắt không giới hạn (kết quả giữ tạm dùng chung thay cho giới hạn); tìm kiếm dùng giới hạn của M06; nút gợi ý Topic tối đa 10 lần trong 60 giây gần nhất cho mỗi người dùng (M05). |
| DEC-095, QA-167, QA-168, QA-037 → DEC-053, DEC-205; DEC-055 | Mỗi bài Đã đăng có một embedding, tạo khi bài chuyển sang Đã đăng (mọi đường, gồm bài của Admin), tạo lại mỗi lần tiêu đề hoặc nội dung chữ thay đổi; bài nháp, đang chờ, bị từ chối không có. Bài thiếu embedding (tắt hoặc lỗi) được tạo bù qua hàng chờ. Bình luận không có embedding và không được tìm kiếm. M06 tìm bài bằng embedding và xếp hạng theo độ liên quan và tương tác. |
| DEC-133, QA-254 → DEC-156, DEC-198, DEC-207; DEC-129 | Mỗi lời gọi chấm điểm kiểm duyệt, embedding bài, gợi ý Topic có đúng một bản ghi nhật ký quyết định AI, kể cả lời gọi thất bại (ghi thành công hay thất bại, đầu ra thô), gắn với bài hoặc bình luận; quét luồng bình luận ghi mỗi bình luận một bản ghi; tóm tắt và embedding truy vấn không ghi. Tách khỏi nhật ký Mod/Admin. Giữ vĩnh viễn, không sửa, không xóa; tài khoản bị xóa vẫn gắn qua username. Chỉ Mod, Admin xem khi xét khiếu nại bài bị AI từ chối; không có chỗ tra cứu khác. |
| DM-11.4, GL:Summarization → QA-007 → DEC-206; QA-011 → DEC-171, DEC-206 | Tóm tắt chỉ cho bài viết, không cho luồng bình luận; không tự động, không lưu lâu dài. Người dùng đã đăng nhập yêu cầu trên bài từ 300 từ; Guest bấm thì được nhắc đăng nhập (sửa QA-011). AI nhận tiêu đề và nội dung chữ, không nhận tệp đính kèm, bình chọn; tóm tắt hiện kèm ghi chú "chưa bao gồm nội dung tệp đính kèm". Kết quả giữ tạm dùng chung 24 giờ, bỏ khi sửa tiêu đề, nội dung chữ hoặc còn dưới 300 từ. DEC-171 (ngoài bảng nguồn) chỉ thêm quyền Guest xem hồ sơ, không chạm M13. |
| DM-11.5, GL:Feedback / Evaluation Loop, QA-017 → DEC-050, DEC-142, DEC-159 → DEC-203 | Chỉ đánh giá gợi ý Topic. Dữ liệu là phản hồi gợi ý Topic của M05 (Topic gợi ý so với Topic tác giả chọn cuối), chỉ ghi khi gợi ý chưa lỗi thời, kể cả khi sửa bài; giữ khi tài khoản bị xóa, không còn danh tính. Một chỉ số: tỷ lệ Topic gợi ý được giữ lại, theo bộ lọc thời gian của M15, Admin xem ở bảng Nội dung. Bỏ phần Mod / Trusted User đánh dấu đúng/sai và các chỉ số Precision, Recall, F1, Accuracy của draft. Không gửi gì cho AI, không train lại. |
| QA-243 → DEC-203; MR-M15 | M15 (bảng Nội dung) có thêm tỷ lệ Topic gợi ý được giữ lại. |
| DM-11.2, GL:AI Classification → DEC-050 → DEC-140; DEC-132 → DEC-141, DEC-144 | Thuộc M05: AI chỉ gợi ý Topic khi tác giả bấm nút, dựa trên danh mục Topic hiện tại; Topic ngoài danh mục bị bỏ, chỉ thất bại khi không còn Topic hợp lệ (DEC-141 ngoài bảng nguồn). |
| QA-022, QA-035 → DEC-053 | Thuộc M06: bài tìm theo ngữ nghĩa, người dùng/Tag/Topic/nhóm tìm theo khớp chính xác hoặc tiền tố; bình luận không tìm; full-text khi tắt AI. |
| DEC-131 → DEC-154 | Thuộc M01: trang chính sách ghi nội dung được "nhà cung cấp dịch vụ AI" xử lý, không nêu tên (DEC-146, ngoài bảng nguồn, thêm gợi ý Topic). |
| DEC-129 → DEC-156 → DEC-159; OPEN-008 → DEC-154, DEC-156 | Nhật ký giữ vĩnh viễn, chỉ xóa cứng khi an toàn. Phần OPEN-008 chạm M13 (nhật ký AI khi xóa tài khoản) đã chốt; phần còn mở thuộc M01. |
| DEC-077, QA-019 → DEC-078 → DEC-180, DEC-186, DEC-190, DEC-195 | Thuộc M08: bình luận quét cả luồng khi số trả lời đạt ngưỡng tốc độ; bình luận của Admin không quét. DEC-180, DEC-190 (ngoài bảng nguồn) chỉ sửa phần hiển thị bình luận ẩn và vụ chờ xét, không chạm M13. |
| QA-016 → DEC-104 | Thuộc M11: bài trong nhóm qua AI trước cổng duyệt của nhóm; Mod hệ thống vẫn can thiệp được. |
| QA-217, ISS-159 | Thuộc M16: không có AI kiểm duyệt tin nhắn chat. |
| DEC-053 → DEC-209, DEC-210; DEC-055 → DEC-211; DEC-063 → DEC-213; QA-011 → DEC-208 (M06) | Chỉ sửa hành vi tìm kiếm của M06: cách khớp tên, nhóm Private, chi tiết xếp hạng, cách đếm giới hạn tần suất. M13 không đổi: Guest không có embedding truy vấn (FR-M13-04.04) khớp DEC-208 — Guest tìm bài bằng full-text, bấm "Tìm kiếm thông minh" thì được nhắc đăng nhập, không gọi AI; giới hạn tần suất tìm kiếm vẫn là của M06. |
