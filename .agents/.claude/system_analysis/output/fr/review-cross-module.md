# Rà soát chéo FR-M01 … FR-M16

| Mục | Nội dung |
|---|---|
| Ngày | 2026-10-24 |
| Phạm vi | 16 tệp FR đã chốt trong `output/fr/` |
| Mốc register | DEC-269, QA-475, ISS-413, OPEN-012 |
| Trạng thái | Xong pha A–D (kết quả ở mục 6) |

Báo cáo chỉ nêu chỗ lệch **giữa** các module. Không phân tích lại từng module. Chưa sửa FR hay register nào.

## 1. Cách làm

1. **Tool (pha A).** Sinh lại index một lần (1301 mục nguồn) và lineage cho toàn register (326 cạnh, `.work/lineage-all.json`).
   Chạy `lint_fr.py --final` và `trace_check.py --lineage --others` trên cả 16 FR: ERROR=0. Kết quả thô ở `.work/xreview/`.
   Để biết WARN nào mới, lint được chạy hai lần, một lần với lineage riêng của từng module, một lần với lineage toàn register.
   TR-08 "mới" là cảnh báo chỉ hiện ở lần chạy thứ hai, tức do DEC ra đời sau khi module đó chốt.
2. **Tham chiếu chéo.** Script tạm `.work/xreview/xref.py` lấy mọi mã `FR-/BR-/TBD-Mxx-…` một FR trích từ FR khác.
   Có 68 tham chiếu như vậy. Mọi mã đều tồn tại, không mã nào trỏ tới yêu cầu đã bỏ. Từng tham chiếu đã được đọc lại cùng ngữ cảnh để kiểm đúng nghĩa.
3. **Giao tiếp module.** Trích bảng "Giao tiếp với module khác" của 16 FR (`.work/xreview/iface.txt`), rồi đối chiếu từng cặp Cung cấp ↔ Dùng.
4. **DEC sinh muộn.** Đọc nguyên văn các DEC mà TR-08 "mới" chỉ ra: DEC-185, DEC-203 đến DEC-269.
   Với mỗi DEC, kiểm FR làm trước nó đã phản ánh đúng hay chưa.
5. **Thống nhất.** Kiểm tên trạng thái, nhãn hiển thị và các con số giữa các FR, với glossary và register.
   Các con số gồm thời hạn, giới hạn, ngưỡng, trọng số, kích thước tệp, số từ, giới hạn tần suất.

## 2. Bảng phát hiện

Cột "Xử lý": **sửa thẳng** là chỗ suy ra được từ draft hoặc register. **Cần hỏi** là mâu thuẫn từ mức Trung bình trở lên mà nguồn không cho kết luận.

| CR | Mức | FR liên quan | Mô tả | Nguồn | Xử lý |
|---|---|---|---|---|---|
| CR-01 | Trung bình | FR-M11, FR-M03, FR-M15 (kéo theo M02, M05, M14) | Bài "Bị gỡ khỏi nhóm" chưa có trạng thái đăng thống nhất. Bảng chuyển trạng thái của M11 ghi "Đã đăng → Bị gỡ khỏi nhóm" như một trạng thái. Mục dữ liệu của M11 lại ghi đây là thuộc tính "bị gỡ khỏi nhóm (xóa mềm)" của bài. M03, module sở hữu trạng thái đăng, không có trạng thái này và cũng không xếp nó vào "Đã xóa", vì tác giả không khôi phục được. M15 đếm bài theo 6 trạng thái đăng (DEC-268) và không nói bài bị gỡ khỏi nhóm thuộc nhóm nào. | DEC-231, DEC-239, DEC-268, DEC-269 | cần hỏi |
| CR-02 | Trung bình | FR-M09, FR-M11 | Bài nhóm bị AI tự từ chối, khiếu nại được chấp nhận: chưa rõ có đi qua cổng duyệt của nhóm không. Theo BR-M09-24, bài sang Đã đăng ngay, không quét lại. FR-M11-13.12 chỉ nói "khiếu nại qua M09 như bài không thuộc nhóm". Không nguồn nào nói bài có qua cổng duyệt của nhóm nữa không khi nhóm bật công tắc duyệt trước. | DEC-198, DEC-237 (L11), DEC-104, DEC-230 | cần hỏi |
| CR-03 | Trung bình | FR-M03 (FR-M03-07.01), FR-M14 | Điều kiện hiển thị chưa đủ ngoại lệ. FR-M03-07.01 viết "phải hiển thị bài cho mọi người khi Đã đăng và Bình thường, trừ nhóm Private". Câu này chưa trừ các trường hợp module khác ẩn bài: tác giả DEACTIVATED hoặc DELETED (FR-M01-13.01), nhóm Bị ẩn (BR-M11-27, BR-M08-50), bài bị gỡ khỏi nhóm (FR-M11-14), người ngoài nhóm sau khi nhóm chuyển Private (DEC-234). M14 dùng FR-M03-07.01 làm điều kiện "bài đủ điều kiện hiển thị", nên hai tài liệu đọc riêng thì mâu thuẫn. | DEC-019, DEC-156, DEC-194, DEC-231, DEC-234 | sửa thẳng: thêm vế "trừ khi bài bị module khác ẩn (M01, M08, M11)" kèm các mã yêu cầu; không thêm hành vi |
| CR-04 | Trung bình | FR-M03, FR-M11, FR-M07, FR-M13 | Bài đăng hay bị từ chối qua cổng duyệt của nhóm chưa được báo cho M07, M13. M03 có liệt kê sự kiện cho hai module này: "bài được đăng, bị từ chối, bài mới cho người theo dõi" cho M07, và "mốc Đã đăng theo mọi đường" để M13 tạo embedding. Nhưng danh sách chỉ có đường của M03, thiếu các đường đăng của M11: nhóm chấp nhận (FR-M11-13.05), đăng thẳng khi tắt duyệt trước (FR-M11-12.05, 12.06), bài của Owner (FR-M11-12.19); và thiếu việc nhóm từ chối bài (FR-M11-13.06). Dòng "Cung cấp M07" của M11 cũng không có các sự kiện này. DEC-065 ("post published/rejected") và DEC-215 áp cho mọi bài. | DEC-065, DEC-215, DEC-205, DEC-237 (L11) | sửa thẳng: dòng Cung cấp M07, M13 của M03 ghi "kể cả bài nhóm qua cổng duyệt của nhóm (M11)"; M11 thêm dòng tương ứng |
| CR-05 | Trung bình | FR-M03 | Bảng trạng thái kiểm duyệt của M03, module sở hữu, thiếu dòng "Bình thường → Bị Mod ẩn khi Mod, Admin ẩn bài lúc xử lý vụ" (FR-M08-06.01). M08 và M09 đều có dòng này. Hai dòng "Mod xét…" ghi "Mod", trong khi FR-M08-07.01 và 07.02 ghi "Mod hoặc Admin". | DEC-032, DEC-190 | sửa thẳng |
| CR-06 | Thấp | FR-M12, FR-M08, FR-M09 | Tên trạng thái kiểm duyệt của bài chưa thống nhất. M03 và M15 dùng "Bị Mod ẩn"; M08, M09, M12 dùng "Bị ẩn" (M08, M09 đã có ghi chú đây là bí danh). Riêng thuật ngữ "Gỡ vì vi phạm" của M12 còn dùng mã kỹ thuật "HIDDEN". | DEC-032 | sửa thẳng: M12 đổi thành "Bị Mod ẩn (M03)" và thêm ghi chú bí danh như M08 |
| CR-07 | Thấp | FR-M09 (BR-M09-02, FR-M09-01.15) | Danh sách không khiếu nại được có "giáng cấp Mod" nhưng chưa có "thu hồi vai trò Admin". DEC-221 nói rõ việc thu hồi không có khiếu nại, và dòng "Cung cấp M09" của M10 đã ghi. | DEC-221 | sửa thẳng |
| CR-08 | Thấp | FR-M08 (BR-M08-50, FR-M08-18.05), FR-M11 (BR-M11-28) | Hai module cùng liệt kê thao tác bị chặn khi nhóm Bị khóa. M08 chỉ có danh sách của DEC-194, thiếu các thao tác quản lý của Owner, Group Mod (DEC-235). Hai bên không mâu thuẫn, nhưng hành vi bị định nghĩa ở hai nơi. | DEC-194, DEC-235 | sửa thẳng: M08 giữ quyết định khóa; danh sách chi tiết trỏ sang BR-M11-28 |
| CR-09 | Thấp | FR-M04 | Thuật ngữ "Khóa bình luận, Khóa toàn bộ" và dòng "Dùng M03" của M04 chỉ nói chặn bình luận mới. Theo DEC-246, Khóa toàn bộ còn chặn upvote và rút upvote trên bình luận của bài (đã có ở FR-M03-14.06, BR-M12-04). | DEC-246 | sửa thẳng |
| CR-10 | Thấp | FR-M07, FR-M02 | Khi cờ Chat tắt, biểu tượng Tin nhắn cùng số chưa đọc (M07) và nút "Nhắn tin" trên hồ sơ (M02) vẫn hiện (DEC-256). M02, M07 chưa ghi điều này. M02 đã ghi tương tự cho cờ Group (DEC-236). | DEC-256 | sửa thẳng: ghi ở dòng "Dùng M16" (M16 sở hữu) |
| CR-11 | Thấp | FR-M03, FR-M04 | Ghi chú C.1 còn nói tới "theo dõi bài": M03 ở dòng DEC-156 và QA-319, M04 ở dòng QA-043. DEC-215 đã bỏ việc theo dõi bài. | DEC-215 | sửa thẳng |
| CR-12 | Thấp | FR-M09 | TBD-M09-01 đã đóng bởi DEC-201 nhưng dòng bị xóa khỏi B.2. Các FR khác giữ dòng "(Đã đóng …)". | DEC-201 | sửa thẳng: khôi phục dòng ở trạng thái đã đóng |
| CR-13 | Thấp | FR-M15 | BR-M15-09 định nghĩa lại cách tính tỷ lệ Topic gợi ý được giữ lại, mà BR-M13-29 đã định nghĩa (M13 sở hữu). Câu hỏi Q-11 trích BR-M01-24 (quy tắc cho DELETED) cho cả trường hợp vô hiệu hóa; quy tắc đúng là FR-M01-13.01. | DEC-203, DEC-019 | sửa thẳng: BR-M15-09 trỏ BR-M13-29, giữ ví dụ; sửa trích dẫn ở Q-11 |
| CR-14 | Thấp | FR-M09 | Bảng "Trạng thái đăng (phần M09)" ghi "(bắt đầu) → Chờ duyệt", còn M03 ghi "Nháp → Chờ duyệt". | DEC-031 | sửa thẳng |
| CR-15 | Thấp | FR-M01–M05, M07–M10, M12, M13, M15 | Khoảng 100 cặp TR-08 "mới": một DEC sinh muộn sửa hoặc làm rõ một phần nguồn mà FR trích, nhưng chưa có ở Phụ lục A hay C.2. Đã đọc nguyên văn từng DEC. Ngoài các CR ở trên, không cặp nào làm đổi yêu cầu. Danh sách theo FR ở mục 4. | xem mục 4 | sửa thẳng: thêm dòng C.2 "Không đổi hành vi Mxx", ghi chú C.1 |
| CR-16 | Thấp | FR-M12 | C2-02: MR-M12 sửa DEC-079 và được trích ở Phụ lục A, nhưng chưa có trong C.2. | MR-M12, DEC-079 | sửa thẳng |
| CR-17 | Thấp | FR-M01, FR-M13 | COV-10: TBD-M01-01 ghi dùng OPEN-008 và TBD-M13-01 ghi dùng OPEN-001, nhưng Phụ lục A chưa trích hai OPEN đó. | OPEN-008, OPEN-001 | sửa thẳng |
| CR-18 | Thấp | glossary.md | Một số mục glossary lỗi thời so với DEC và chưa gắn dấu sửa. Các FR đã ghi nhận chỗ lỗi thời ở C.1, nên chỉ register cần sửa. Comment: "accepted as an answer" (DEC-169). Reputation: Accepted Answers (DEC-169). Leaderboard: có kỳ Yearly (QA-038, DEC-242: chỉ tuần, tháng, toàn thời gian). GroupMember: thiếu Group Mod (DEC-107). Lớp/Khối: "personalize feed" (DEC-125). Summarization: tóm tắt luồng bình luận (DEC-206). Feedback / Evaluation Loop: precision, recall, F1 (DEC-203). | DEC-107, DEC-125, DEC-169, DEC-203, DEC-206, DEC-242 | sửa thẳng: gắn `[Amended 2026-10-24 — DEC-nnn: …]`, không xóa |
| CR-19 | Thấp | 13 FR | `moc_nguon` của 13 FR lùi so với register (DEC-269), lùi xa nhất là M09 (DEC-202), M13 (DEC-207), M06 (DEC-213). Riêng M06 đã xử lý tới DEC-263 (bản 1.5) nhưng chưa cập nhật mốc này. | — | sửa thẳng: cập nhật `moc_nguon` ở mọi FR được nâng phiên bản trong pha D |

**Không phải lỗi, ghi lại để khỏi rà lại:**
- STATE-02 ở M03, M08, M09, M10, M11, M12: các dòng này trỏ tới yêu cầu của module khác (ví dụ "FR-M09-08.12") hoặc ghi tên module ("M01"). Tool chỉ nhận mã của chính module nên báo thiếu. Nội dung đúng.
- COV-03: các dòng C.1 được thêm sau bước 1 nên không có trong scan cũ. Không thiếu nguồn.
- REQ-01 ở M07, M09, M10, M14: các dòng "(Đã bỏ …)", đúng quy ước không đánh lại mã.
- REQ-02 ở FR-M12-08.01, 08.08 và FR-M16-06.04, 15.01: một câu có hai chữ "phải" nhưng chỉ mô tả một hành vi. Đã giữ lại khi chốt.
- Các con số trùng khớp giữa mọi FR. Đã so: ngưỡng 0,5 và 0,9; thời gian chờ 5 và 10 giây, thử lại một lần sau 2 giây; giới hạn 10 lần trong 60 giây (gợi ý Topic); giới hạn 30/10 (Guest) và 45/20 (người đã đăng nhập) trong 60 giây (tìm kiếm); 20 từ; 6.000 từ và 150 ký tự (bài); 1.000 từ (bình luận, tin nhắn); 5 MB × 10 ảnh và 20 MB × 3 tài liệu; avatar 5 MB; bio 155 ký tự; vô hiệu hóa 14 ngày; email cảnh báo trước 24 giờ; ban 30, 90 ngày, vĩnh viễn; hạn khiếu nại (thời gian thử thách, thời hạn ban, 90 ngày, 30 ngày); thời gian thử thách 7, 10, 15 ngày; khôi phục bài 7 ngày; trọng số Trending; trọng số điểm 2:1; mốc huy hiệu; đề xuất có hạn 7 ngày.
- Nhãn hiển thị trùng khớp: "[Người dùng đã xóa]", "Tài khoản tạm thời vô hiệu hoá", "Tài khoản đã bị khóa", "Hệ thống đang bận, vui lòng thử lại sau", "Nội dung không tồn tại". "[Tài khoản đã xóa]" chỉ còn trong câu hỏi lịch sử của M12 (Q-09) và chuỗi C.2, không có trong yêu cầu.
- Cấu hình (M10): mọi FR dùng đúng tên công tắc (AI tổng; Moderation, Search, Topic suggestion), đúng ba cờ tính năng (Group, Gamification, Chat), và đều coi ngưỡng, thời hạn là hằng số không chỉnh qua giao diện.
- Nhật ký: thao tác Tag, Topic của Admin được ghi cả ở nhật ký thao tác Admin (M10) và nhật ký kiểm duyệt (M08), theo BR-M10-24. M05, M08, M10 khớp nhau.

## 3. TBD còn mở và TBD đã được giải quyết

| TBD | Trạng thái trong FR | Đã giải quyết bởi | Ghi chú |
|---|---|---|---|
| TBD-M01-01 | Mở (Thấp) | — | OPEN-008 còn mở phần email liên hệ và bản sao dữ liệu |
| TBD-M03-01, TBD-M05-02, TBD-M15-02 | Mở (Thấp) | — | OPEN-005 còn mở; ba FR ghi cùng một lý do |
| TBD-M03-02, TBD-M05-01, TBD-M06-01, TBD-M14-02 | Mở (Thấp) | — | OPEN-006 còn mở; bốn FR ghi cùng một lý do |
| TBD-M04-01, TBD-M08-03 | Đã đóng | DEC-201 | Khớp |
| TBD-M08-01, TBD-M16-01 | Mở (Thấp) | — | OPEN-003 còn mở |
| TBD-M08-02, TBD-M16-02 | Đã đóng | DEC-239 (M11), DEC-248 (M16) | Khớp; OPEN-011 đã đóng |
| TBD-M08-04 | Mở (Trung bình) | — | Ngưỡng tốc độ trả lời để kích hoạt quét luồng. Chưa DEC nào chốt; C.2 của M04 cũng ghi "chưa chốt". Để ngỏ có chủ đích (DEC-077) |
| TBD-M08-05 | Mở (Thấp) | — | Ngưỡng 0,9 và 0,5 là giá trị tạm. Khớp BR-M13-14 (hằng số, chỉ đổi qua triển khai) |
| TBD-M09-01 | Đã đóng, nhưng dòng bị xóa | DEC-201 | CR-12 |
| TBD-M10-01 | Đã đóng | DEC-236, DEC-245, DEC-256 | Khớp |
| TBD-M11-01 | Đã đóng | DEC-239 | Khớp |
| TBD-M13-01 | Mở (Thấp) | — | OPEN-001 còn mở |
| TBD-M14-01 | Đã đóng | DEC-259 | Khớp; OPEN-009 đã đóng |
| TBD-M15-01 | Mở (Thấp) | — | OPEN-004 còn mở |

Không có TBD nào đang mở mà thực ra đã được một DEC hay một module sau giải quyết.

## 4. TR-08 "mới" theo FR (cho CR-15)

Ký hiệu: X←Y nghĩa là nguồn X bị Y sửa hoặc làm rõ một phần. Mọi cặp dưới đây đã được đọc nguyên văn. Cặp nào làm đổi yêu cầu thì đã tách thành CR riêng, ghi ở cột cuối.

| FR | Cặp | Kết luận |
|---|---|---|
| M01 | DEC-065←231, 237; DEC-129←248 | Không đổi hành vi M01 |
| M02 | DEC-038←184; DEC-079←188, 211; DEC-122←246; DEC-167←246; QA-011←206, 208; QA-018←246; QA-127←215 | Không đổi hành vi M02 |
| M03 | DEC-065←221, 231, 237; DEC-104←230, 233 | Không đổi hành vi M03; nội dung DEC-230/231/240 đã vào bản 1.6 |
| M04 | DEC-167←246; DEC-195←240; QA-227←260 | DEC-246 → CR-09; còn lại không đổi |
| M05 | DEC-081←224; DEC-090←224; DEC-129←248; DEC-159←215 | Không đổi hành vi M05 |
| M07 | DEC-067←254; DEC-125←258, 260; DEC-129←248; DEC-194←235; DEC-212←263; DEC-237←240 | Không đổi hành vi M07 |
| M08 | DEC-065←231, 237, 246; DEC-104←230, 233, 240; DEC-108←234; DEC-118←242, 246; DEC-167←246; DEC-194←235; DEC-195←240; QA-018←246 | DEC-235 → CR-08; còn lại không đổi |
| M09 | DEC-065←215, 218, 221, 231, 237, 246; DEC-079←211; DEC-081←224; DEC-090←224; DEC-091←220, 221, 222, 223; DEC-109←237; DEC-113←231, 241; DEC-129←248; DEC-133←207; DEC-194←235; DEC-195←240 | DEC-221 → CR-07; DEC-237 → CR-02; còn lại không đổi |
| M10 | DEC-129←248; DEC-195←240; DEC-225←236, 245, 256 | Không đổi hành vi M10; TBD-M10-01 đã ghi ba DEC này nhưng C.2 chưa ghi |
| M12 | DEC-225←256 | Không đổi hành vi M12 |
| M13 | DEC-090←224; DEC-092←225, 226, 228; DEC-104←230, 233, 240; DEC-129←248; DEC-159←215; DEC-195←240 | Không đổi hành vi M13 |
| M15 | DEC-161←185 | Không đổi hành vi M15 |

## 5. Dự kiến pha D (khi được duyệt)

| FR | CR |
|---|---|
| FR-M01 | CR-15, CR-17 |
| FR-M02 | CR-10, CR-15 |
| FR-M03 | CR-01 (theo câu trả lời), CR-03, CR-04, CR-05, CR-11, CR-15 |
| FR-M04 | CR-09, CR-11, CR-15 |
| FR-M05 | CR-15 |
| FR-M07 | CR-04, CR-10, CR-15 |
| FR-M08 | CR-08, CR-15 |
| FR-M09 | CR-02 (theo câu trả lời), CR-07, CR-12, CR-14, CR-15 |
| FR-M10 | CR-15 |
| FR-M11 | CR-01, CR-02 (theo câu trả lời), CR-04 |
| FR-M12 | CR-06, CR-15, CR-16 |
| FR-M13 | CR-04, CR-15, CR-17 |
| FR-M14 | CR-03 (chỉ khi câu chữ ở M14 cần đổi theo FR-M03-07.01 mới) |
| FR-M15 | CR-01 (theo câu trả lời), CR-13, CR-15 |
| glossary.md | CR-18 |

FR-M06 và FR-M16 không có thay đổi. Mọi FR được nâng phiên bản đều cập nhật `moc_nguon` (CR-19).

## 6. Kết quả pha C, D (2026-10-24)

**Câu trả lời của stakeholder:** CR-01 chọn A, ghi thành DEC-270 (QA-476, ISS-414). CR-02 chọn B, ghi thành DEC-271 (QA-477, ISS-415).

**Register:**
- Thêm mục "Cross-module review — 2026-10-24" vào issue-queue, qa-log và decisions.
- Gắn dấu lên các mục cũ, không xóa nội dung: DEC-198 nhận `[Amended — DEC-271]`; DEC-231, DEC-268 nhận `[Clarified — DEC-270]`; DEC-237 nhận `[Clarified — DEC-271]`.
- Glossary: gắn dấu Amended cho 7 mục (CR-18).

**FR đã nâng phiên bản:**

| FR | Phiên bản | Ghi chú |
|---|---|---|
| FR-M01 | 1.9 → 1.10 | |
| FR-M02 | 1.5 → 1.6 | |
| FR-M03 | 1.9 → 1.10 | |
| FR-M04 | 1.3 → 1.4 | |
| FR-M05 | 1.6 → 1.7 | |
| FR-M07 | 1.4 → 1.5 | |
| FR-M08 | 1.6 → 1.7 | |
| FR-M09 | 1.1 → 1.2 | Thêm FR-M09-08.18 |
| FR-M10 | 1.3 → 1.4 | |
| FR-M11 | 1.2 → 1.3 | Thêm FR-M11-13.14 |
| FR-M12 | 1.0 → 1.1 | |
| FR-M13 | 1.2 → 1.3 | FR-M13-03.01 thêm đường đăng qua cổng duyệt của nhóm; phát hiện khi chạy lại XMOD |
| FR-M14 | 1.0 → 1.1 | Chỉ thêm C.2 cho DEC-271 |
| FR-M15 | 1.0 → 1.1 | |

FR-M06 và FR-M16 không đổi.

**Hai mục không sửa như dự kiến:**
- CR-14: giữ "(bắt đầu)" ở bảng trạng thái đăng (phần M09). Bảng này chỉ trích lại luồng của M03; đổi thành "Nháp" sẽ sinh STATE-01 vì trong bảng trích không có đường vào trạng thái Nháp.
- CR-17: giữ WARN COV-10. TBD không có dòng ở Phụ lục A nên không trích OPEN được; đây là giới hạn của tool, đã có từ lúc chốt.

**Tool sau khi sửa:** 16/16 FR có ERROR=0. Các WARN mới chỉ gồm:
- COV-03 cho các nguồn mới thêm vào C.1 (scan bước 1 là bản cũ).
- Một STATE-02 ở dòng "Bình thường → Bị Mod ẩn" của M03, vì dòng này trỏ tới FR-M08-06.01 (tool chỉ nhận mã của chính module).
- C2-02 của M12 vẫn còn: dòng C.2 "DEC-079 → MR-M12" đã thêm nhưng tool không nhận dạng mã `MR-Mxx` trong C.2.
