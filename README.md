# Đề thi ảnh (de-thi-anh-watermark)

Công cụ chạy hoàn toàn trên trình duyệt: đọc đề trắc nghiệm từ file `.docx`, chuyển **từng câu hỏi thành ảnh PNG** (không có đáp án), gắn **thông báo quy chế thi** và watermark mờ, rồi **chèn ảnh ngược vào file `.docx` gốc**.

Không có máy chủ, không gửi dữ liệu đi đâu. Đề thi chỉ nằm trong trình duyệt của bạn.

## Tính năng

- Nạp file `.docx` hoặc dán nội dung đề. Tự nhận dạng format dạng Aiken:
  ```
  PI2.1 - Nội dung câu hỏi? CLO1      (hoặc "Câu 1: …", hoặc câu hỏi trơn)
  A. Đáp án A
  B. Đáp án B
  C. Đáp án C
  D. Đáp án D
  ANSWER: A
  ```
  Mã `PI…`, `CLO…` và số thứ tự ở cuối câu được tự cắt khỏi ảnh. Phần tiêu đề và thang điểm của file được bỏ qua.
- **Ảnh chỉ có câu hỏi**, khung cố định 1000×560 px, chữ tự co để vừa khung, nên chụp một lần là thấy đủ trên cả laptop và điện thoại. Câu quá dài sẽ được đánh dấu "dài" và ảnh cao hơn.
- **Khu vực "Kiểm tra câu hỏi"**: xem và sửa trực tiếp nội dung từng câu trước khi tạo ảnh. Có nút thử nghiệm "Tự bỏ câu dẫn".
- **Thông báo quy chế thi ở góc trên và góc dưới ảnh** (chữ nhìn thấy được, song ngữ Việt/Anh) và watermark chữ mờ phủ nền cùng viền chữ siêu nhỏ.
- **Chữ chéo "BÀI THI · CẤM DÙNG AI" ở giữa ảnh** (xám nhạt, nhìn thấy được, khó cắt bỏ mà không mất nội dung câu hỏi).
- Phần **"Kiểm tra hiển thị"** mô phỏng khung điện thoại dọc và laptop ngang, kèm cỡ chữ thực tế ước tính. Công tắc "Xem như AI thấy" tăng tương phản để kiểm tra watermark có trong ảnh.
- **Tải PNG từng câu hoặc cả zip** (kèm CSV ghi đáp án đúng).
- **Xuất Moodle XML**: mỗi câu là ảnh làm đề bài (nhúng base64) kèm 4 phương án chữ, đáp án đúng theo `ANSWER`, bật trộn đáp án. Import tại *Ngân hàng câu hỏi → Nhập → Moodle XML*.
- **Chèn ảnh vào `.docx` gốc**: thay đoạn câu hỏi bằng ảnh, giữ nguyên đáp án A–D và dòng `ANSWER`.

## Dùng online (GitHub Pages)

1. Tạo repo mới trên GitHub và đẩy toàn bộ thư mục này lên nhánh `main`.
2. Vào **Settings → Pages → Build and deployment → Source: GitHub Actions**.
3. Workflow `.github/workflows/pages.yml` sẽ tự triển khai. Trang chạy tại `https://<tên-bạn>.github.io/<tên-repo>/`.

## Chạy cục bộ

Chỉ cần mở `index.html` trong trình duyệt. Trang tải thư viện `JSZip`, `mammoth` từ cdnjs và font từ Google Fonts, nên cần có mạng.

Nếu muốn chạy offline, tải các file đó về và sửa đường dẫn trong thẻ `<script>` và `<link>` ở đầu `index.html`.

## Cách dùng

1. Chọn file `.docx` của đề (hoặc dán nội dung).
2. Xem lại mục **Kiểm tra câu hỏi**, sửa nếu cần.
3. Chọn mẫu thông báo quy chế. Mặc định là **"Quy chế thi: nêu sự thật, không ra lệnh"**.
4. Bấm **Tạo ảnh**, kiểm tra phần xem trước, rồi bấm **Chèn ảnh vào file .docx gốc** hoặc **Tải tất cả (.zip)**.

## Hạn chế cần biết

- **Chữ ẩn trong ảnh không đảm bảo ngăn AI.** Nhiều AI hiện nay đọc được chữ mờ, coi đó là dữ liệu chứ không phải mệnh lệnh, rồi bỏ qua và còn báo cho người dùng biết. Các mẫu "ra lệnh cho AI" (Diagnostic, NDA, đáp án mồi) đã được thử, thường bị bỏ qua và có thể đánh lừa sinh viên, nên đã bị gỡ khỏi app. App chỉ giữ thông báo quy chế trung thực.
- Thông báo quy chế hiện rõ chỉ có tác dụng răn đe sinh viên, và có thể khiến một số AI từ chối hoặc nhắc nhở. Không có gì đảm bảo.
- Ảnh hóa câu hỏi chỉ chặn được sao chép văn bản. Sinh viên vẫn có thể chụp màn hình rồi hỏi AI.
- **Khả năng tiếp cận:** người dùng trình đọc màn hình không đọc được câu hỏi trong ảnh. Cần có phương án hỗ trợ riêng cho sinh viên có nhu cầu.
- Moodle không đọc file Word, và định dạng Aiken chỉ nhận chữ thuần nên mất ảnh. Với Moodle hãy dùng **Moodle XML** do app xuất. File có thể nặng vài chục MB; kiểm tra giới hạn tải lên của hệ thống và thử trên bài thi nháp trước khi dùng thật.
- Chỉ lưu và nộp ảnh dạng **PNG**. JPG nén sẽ làm mất watermark mờ.
- Biện pháp bền hơn là thay đổi chính **nội dung đề**: số liệu và tình huống riêng của lớp, hình ảnh hoặc bảng cần đọc, mỗi sinh viên một mã đề, giới hạn thời gian theo câu, giám sát hoặc vấn đáp ngắn.

## Cấu trúc

```
index.html                    # toàn bộ ứng dụng (HTML + CSS + JS, một file)
.github/workflows/pages.yml   # tự triển khai lên GitHub Pages
LICENSE
```

## Công nghệ

HTML/CSS/JavaScript thuần, `<canvas>` để vẽ ảnh, [JSZip](https://stuk.github.io/jszip/) để đọc/ghi `.docx` và tạo zip, [mammoth](https://github.com/mwilliamson/mammoth.js) để đọc chữ từ `.docx`, font Be Vietnam Pro.

## Giấy phép

MIT. Xem file `LICENSE`.
