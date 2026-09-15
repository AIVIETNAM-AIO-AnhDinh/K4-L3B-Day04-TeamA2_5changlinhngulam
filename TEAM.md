# TEAM — Day04, K4-L3B

**Làm nhóm.** Mỗi người tự viết và commit phần INDIVIDUAL của mình.

## Thông tin bài nộp

- Tên nhóm: 5changlinhngulam
- Người đại diện / MSSV: Đinh Lệnh Tiến Anh 2A202602928
- Tên repo: `K4-L3B-Day04-TeamA2_5changlinhngulam`
- URL repo, nhánh nộp, commit chốt: https://github.com/AIVIETNAM-AIO-AnhDinh/K4-L3B-Day04-TeamA2_5changlinhngulam
- Deadline áp dụng và link thông báo đổi hạn nếu có: 23:59 ngày 15/09/2026

## Thành viên

| Họ và tên | MSSV | GitHub | Vai trò và công việc | File/commit/PR |
|---|---|---|---|---|
| Đinh Lệnh Tiến Anh | 02928 | /AIVIETNAM-AIO-AnhDinh | Sửa tools và chạy v2 | "TienAnh tool, v2" |
| Nguyễn Đức Triệu | 02978 | /ductrieunguyen897-code | Sửa prompt và chạy v1 | "Trieu: prompt, v1" |
| Nguyễn Hoàng Nam | 02485 | /namchip2003-beep | Giao diện, test | "feat: lam giao dien" |
| Vũ Hải Minh | 02452 | /dtc-z | Merge và thêm test,... để chạy v3 | "Add v3 evaluation evidence" |

## Nhận xét chung

- **Kết quả và bằng chứng**: 
  - Nhóm đã hoàn thành đầy đủ các vòng thử nghiệm từ `v0` đến `v3` trên 30 case base, 10 case nhóm (`eval_group.json`) và 12 case an toàn (`eval_adversarial.json`). 
  - Bằng chứng lưu tại [version_log.csv](starter_v0/artifacts/version_log.csv) và [REPORT.md](starter_v0/artifacts/REPORT.md).
  - Kết quả đo lường chính xác: Baseline `v0` đạt `70.0%` ([v0_B_base.json](starter_v0/runs/v0_B_base_openai_20260915T184504437109.json)), bản `v1` (Triệu) cải tiến prompt đạt **`83.33%`** ([v1_B_base.json](starter_v0/runs/v1_B_base_openai_20260915T191249685924.json)), bản `v2` (Tiến Anh) sửa `tools.yaml` đạt `73.33%` ([v2_B_base.json](starter_v0/runs/v2_B_base_openai_20260915T193131381056.json)), và bản `v3` tích hợp chạy bộ an toàn & nhóm ([v3_adversarial.json](starter_v0/runs/v3_B_adversarial_openai_20260915T201014488672.json), [v3_group.json](starter_v0/runs/v3_B_group_openai_20260915T201123482250.json)).

- **Thay đổi hiệu quả nhất**: 
  - Việc chỉnh sửa [system_prompt.md](starter_v0/artifacts/system_prompt.md) ở phiên bản `v1` đạt hiệu quả cao nhất. Việc bổ sung quy tắc phân biệt mã `EMP-xxxx` (chỉ dùng `lookup_user`) và `AST-xxxx` (dùng `inspect_device`), cùng việc ép chỉ định tham số `check` chính xác (`check="vpn"`, `check="network"`) đã làm giảm lỗi `wrong_tool` từ 3 xuống 1 case, nâng `case_accuracy` từ `70.0%` lên **`83.33%`**.

- **Giới hạn còn lại**: 
  - Một số case ranh giới xác nhận phức tạp khi người dùng thay đổi payload sau xác nhận cũ (case `M09_confirmation_invalidated`) hoặc các bài test `adversarial` vẫn còn tỷ lệ `wrong_boundary` do mô hình LLM có lúc dùng lại xác nhận cũ. Cần tiếp tục siết chặt quy trình vòng lặp `clarify` ở các phiên bản tiếp theo.

- **Cách phân công và tích hợp**: 
  - Nhóm phân công độc lập theo mốc công việc: M1 (Triệu - System Prompt v1), M2 (Tiến Anh - Tools Declaration v2), M3 (Minh - System Integration & Safety/Group v3), M4 (Nam - Giao diện Chat UI Streamlit `app.py`).
  - Tích hợp code thông qua quy trình Git Feature Branch (`Trieu_branch`, `Anh_branch`,...) và tạo các Pull Request (PR #1, PR #2) gộp về nhánh `main` minh bạch trên GitHub.

## INDIVIDUAL

### Đinh Lệnh Tiến Anh — 02928

- Phần việc và file/commit/PR: Phụ trách Tools & Schema Engineer (M2). Đã tối ưu hóa file `starter_v0/artifacts/tools.yaml`, tinh chỉnh mô tả và schema tham số cho 9 công cụ hỗ trợ IT, thực hiện run `v2` với commit "TienAnh tool, v2" và khởi tạo PR #1.
- Quyết định, khó khăn và cách xử lý: Phải làm rõ ranh giới giữa các tool trong description mà không sửa code python bên dưới. Đã xử lý bằng cách siết chặt enum giá trị (như `environment`, `category`, `check`) và mô tả rõ các ranh giới khi nào không được tự ý gọi `create_ticket`.
- Điều đã học: Hiểu cách LLM phân tích Tool Declarations/JSON Schema để ra quyết định Tool Calling.
- AI/công cụ đã dùng và cách kiểm tra: Sử dụng Antigravity AI để hỗ trợ kiểm tra tính tương thích của YAML schema.
- Thời điểm đã tự nộp URL repo chung trên VLearn: Đúng hạn buổi học.

### Nguyễn Đức Triệu — 02978

- Phần việc và file/commit/PR: Phụ trách Agent & Prompt Engineer (M1). Đã chỉnh sửa `starter_v0/artifacts/system_prompt.md`, chạy thử nghiệm `v0` và `v1`, bổ sung [version_log.csv](starter_v0/artifacts/version_log.csv) và cập nhật [REPORT.md](starter_v0/artifacts/REPORT.md). Commit "Trieu: prompt, v1" trên PR #2.
- Quyết định, khó khăn và cách xử lý: Khó khăn ở v0 là Agent hay gọi thừa tool `inspect_device` khi gặp mã nhân viên `EMP-xxxx`. Đã giải quyết bằng cách thiết lập quy tắc Routing phân biệt rõ mã `EMP` và `AST` trong prompt, giúp nâng độ chính xác từ 70% lên 83.33%.
- Điều đã học: Hiểu sâu sắc cơ chế Prompt Engineering cho Tool Calling, cách thiết lập giả thuyết và đo lường thực nghiệm qua từng phiên bản v0-v3.
- AI/công cụ đã dùng và cách kiểm tra: Dùng Antigravity AI Assistant hỗ trợ phân tích log lỗi JSON v0 và rà soát kết quả đo lường accuracy.
- Thời điểm đã tự nộp URL repo chung trên VLearn: Đúng hạn buổi học.

### Nguyễn Hoàng Nam — 02485

- Phần việc và file/commit/PR: Phụ trách UI & Transcript Engineer (M4). Xây dựng ứng dụng giao diện Chat UI (`starter_v0/app.py` / `chat.py`) cho phép người dùng tương tác trực tiếp với Agent, hiển thị rõ ràng Tool calls, Arguments, Result/Error và Version. Commit "feat: lam giao dien".
- Quyết định, khó khăn và cách xử lý: Khó khăn trong việc bắt sự kiện Tool execution và render định dạng JSON trên UI. Đã xử lý bằng cách tích hợp trực tiếp vào agent loop để lấy dữ liệu thực runtime.
- Điều đã học: Nắm vững cách xây dựng ứng dụng Trợ lý AI có giao diện tương tác minh bạch luồng Tool Calling.
- AI/công cụ đã dùng và cách kiểm tra: Dùng Streamlit framework và AI trợ giúp format giao diện.
- Thời điểm đã tự nộp URL repo chung trên VLearn: Đúng hạn buổi học.

### Vũ Hải Minh — 02452

- Phần việc và file/commit/PR: Phụ trách Integration & Safety/Eval Engineer (M3). Biên soạn bộ 10 test case của nhóm (`data/eval_group.json`), thực hiện tích hợp code từ các nhánh, chạy thử nghiệm `v3` trên bộ `adversarial` và `group`, bổ sung bằng chứng vào REPORT.md. Commit "Add v3 evaluation evidence".
- Quyết định, khó khăn và cách xử lý: Khó khăn khi kiểm thử ranh giới an toàn cho 12 case adversarial. Đã xử lý bằng cách rà soát kỹ `tool_results` để đảm bảo Agent từ chối các câu lệnh độc hại và không phát tán thông tin nhạy cảm.
- Điều đã học: Hiểu cách đánh giá Red-Teaming / Adversarial cho AI Agent và quy trình merge/integration bằng Git Pull Request.
- AI/công cụ đã dùng và cách kiểm tra: Dùng Antigravity AI để kiểm tra cấu trúc case JSON.
- Thời điểm đã tự nộp URL repo chung trên VLearn: Đúng hạn buổi học.
