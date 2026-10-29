# QUY TẮC CHUYỂN ĐỔI ĐỀ THI 4 PHẦN SANG LATEX VÀ BIÊN DỊCH
Khi nhận yêu cầu chuyển đổi một file đề tổng hợp (PDF/Word/Ảnh) gồm các phần:

1. Đặt lại số thứ tự câu ở mỗi phần:
- Trước khi bắt đầu mỗi phần mới (Phần 1, Phần 2, Phần 3, Phần 4), bắt buộc phải thêm lệnh `\setcounter{ex}{0}` (và `\setcounter{bt}{0}` đối với phần tự luận) để số thứ tự câu luôn đếm lại từ Câu 1.

2. Phân loại cấu trúc chính xác theo từng phần:
- Phần 1 (Trắc nghiệm nhiều lựa chọn):
  + Đặt lệnh `\setcounter{ex}{0}` ở đầu phần.
  + Sử dụng môi trường `\begin{ex} ... \end{ex}` và lệnh `\choice`, đánh dấu đáp án đúng bằng `\True`.

- Phần 2 (Trắc nghiệm Đúng / Sai có khung bảng):
  + Đặt lệnh `\setcounter{ex}{0}` ở đầu phần.
  + Bắt buộc sử dụng lệnh `\choiceTFt` để tự động tạo khung bảng (Mệnh đề | Đúng | Sai)[cite: 6].
  + Đánh dấu mệnh đề đúng bằng `\True` ở đầu mệnh đề, mệnh đề sai giữ nguyên.
  + Phần lời giải bên trong `\loigiai{...}` bắt buộc sử dụng môi trường `\begin{itemchoice} ... \end{itemchoice}` và lệnh `\itemch` cho từng ý a, b, c, d.
  + Mẫu chuẩn bắt buộc:
    \begin{ex}
        Cho hình chóp $S.ABCD$ có $ABCD$ là hình bình hành tâm $O$. Gọi $M, N$ lần lượt nằm trên các cạnh $SA, SC$ sao cho $SM = 2MA$; $SN = 2NC$. Trong các mệnh đề sau, mệnh đề nào đúng, mệnh đề nào sai?
        \choiceTFt
        {\True $SO$ cắt $\text{mp}(BMN)$ tại điểm $I$ $(I = MN \cap SO)$}
        {\True Giao tuyến của $(SAD)$ và $(BMN)$ là $MK$ $(K = SD \cap BI)$}
        {$CD$ cắt $\text{mp}(BMN)$ tại điểm $F$ $(F = CD \cap BN)$}
        {Các điểm $E, B, F$ không thẳng hàng, với $E$ là giao điểm của $AD$ và $MK$}
        \loigiai{
            \begin{itemchoice}
                \itemch \textbf{Đúng.} Giải thích chi tiết ý a...
                \itemch \textbf{Đúng.} Giải thích chi tiết ý b...
                \itemch \textbf{Sai.} Giải thích chi tiết ý c...
                \itemch \textbf{Sai.} Giải thích chi tiết ý d...
            \end{itemchoice}
        }
    \end{ex}

- Phần 3 (Trả lời ngắn / Điền khuyết):
  + Đặt lệnh `\setcounter{ex}{0}` ở đầu phần.
  + Sử dụng môi trường `\begin{ex} ... \end{ex}` và đặt kết quả vào lệnh `\shortans{đáp_án}`.

- Phần 4 (Tự luận):
  + Đặt lệnh `\setcounter{ex}{0}` ở đầu phần.
  + Sử dụng môi trường `\begin{ex} ... \end{ex}`.

3. Quy chuẩn chung & Biên dịch:
- Không để dư dấu chấm ở cuối các phương án nếu không phải là câu hoàn chỉnh[cite: 1, 2].
- Phân số luôn dùng `\dfrac`, hệ phương trình dùng `\heva`, ngoặc vuông dùng `\hoac`.
- Tự động rà soát và sửa các lỗi chính tả tiếng Việt từ bản gốc PDF[cite: 1, 2].
- Sau khi tạo file `.tex`, tự động thêm `\input{...}` vào `main_TTL.tex` và chạy lệnh biên dịch `pdflatex -interaction=nonstopmode -output-directory=<tên_thư_mục> -jobname=<tên_thư_mục> main_TTL.tex` để lưu tất cả các file (`phanTN.tex`, `phanDS.tex`, `phanTLN.tex`, `phanTL.tex` và bản PDF có tên trùng với tên thư mục, ví dụ `DE_4_CUOI_KI/DE_4_CUOI_KI.pdf`) nằm gọn bên trong thư mục đề đó[cite: 1, 2, 4].
4. Quy tắc khi được yêu cầu "Tạo đề mới tương tự / Phát triển đề":
- Giữ nguyên cấu trúc phần, số lượng câu, chủ đề kiến thức và mức độ nhận thức (Nhận biết, Thông hiểu, Vận dụng) của từng câu tương ứng trong đề gốc.
- Thay đổi số liệu, hàm số, hình học không gian (ví dụ đổi từ chóp tứ giác sang chóp tam giác hoặc đổi tỉ lệ điểm) để tạo bài toán mới.
- BẮT BUỘC giải nháp ngược từ đáp án lên đề bài để đảm bảo số liệu chẵn đẹp, hàm số có nghiệm đẹp, không bị lỗi điều kiện xác định.
- Các phương án nhiễu (A, B, C, D) phải hợp lý, tính toán lại lời giải mới khớp 100% với số liệu vừa đổi.
- Nếu câu gốc có hình vẽ TikZ (bảng biến thiên, đồ thị, hình không gian), tự động cập nhật lại tọa độ/số liệu trong đoạn code TikZ cho khớp với hàm số mới.


# QUY TẮC TẠO ĐỀ LATEX & WORD TỰ ĐỘNG

1. KHI CÓ LỆNH "TẠO ĐỀ ...":
- Tự tạo thư mục `DE_<tên>` (VD: "Tạo đề 1" -> tạo thư mục `DE_1`).
- Tự tách thành 4 file riêng trong thư mục đó:
  + `phanTN.tex` : Trắc nghiệm 4 lựa chọn (`\begin{ex}`, `\choice`, `\True`)[cite: 1, 2].
  + `phanDS.tex` : Đúng/Sai kẻ bảng (`\begin{ex}`, `\choiceTFt`, `\True`)[cite: 6]. Lời giải dùng `\begin{itemchoice}` và `\itemch`.
  + `phanTLN.tex`: Trả lời ngắn (`\begin{ex}`, `\shortans{đáp_án}`).
  + `phanTL.tex` : Tự luận (`\begin{ex}`).
- Đầu mỗi file luôn có `\setcounter{ex}{0}`.
- Lời giải luôn đặt trong `\loigiai{...}`[cite: 1, 2]. Phân số dùng `\dfrac`, hệ dùng `\heva`, hoặc dùng `\hoac`.

2. KHI CÓ LỆNH "TẠO ĐỀ ... DỰA VÀO ĐỀ CÓ SẴN":
- Đọc các file trong thư mục đề gốc, tạo thư mục `DE_...` mới, đổi số liệu/hàm số tạo câu hỏi tương tự (đảm bảo số đẹp), giải lại chi tiết và cập nhật code TikZ nếu có.

3. CHẾ ĐỘ HIỂN THỊ LỜI GIẢI & BIÊN DỊCH LATEX:
- Mặc định khi tạo đề: Giữ chế độ hiện lời giải và tô màu đáp án (`solcolor` trong khai báo gói `ex_test`, ví dụ `\usepackage[solcolor]{ex_test}`).
- **KHI TÔI YÊU CẦU "LÀM ĐỀ KHÔNG CÓ LỜI GIẢI" (hoặc "ẩn lời giải", "xuất đề cho học sinh"):** Tự động mở `main.tex`, tìm tùy chọn `solcolor` (trong `\usepackage[...]{ex_test}`) và đổi thành `debai` (ví dụ `\usepackage[debai]{ex_test}`), sau đó biên dịch lại ra `main.pdf`[cite: 1, 2]. Khi nào tôi bảo "hiện lại lời giải" thì đổi ngược từ `debai` về `solcolor`.
- Tự thêm `\input{DE_.../phan...}` vào `main.tex`, chạy `xelatex` (hoặc `pdflatex`) xuất ra `main.pdf` và tự sửa nếu có lỗi[cite: 1, 2, 4].

4. KHI CÓ LỆNH "XUẤT RA WORD (.DOCX)":
- Xuất trực tiếp sang file Word `.docx` chuẩn OpenXML với toàn bộ công thức Toán ở định dạng **OMML Equation (`<m:oMath>`)** hiển thị sẵn và chỉnh sửa được ngay trong Word (tuyệt đối không để công thức dạng `$...$` hay bắt chạy MathType).
- Giữ nguyên bố cục của đề PDF: khung Header, bảng phương án trắc nghiệm, khung bảng 3 cột (Mệnh đề | Đúng | Sai) cho phần Đúng/Sai, và tự động render các hình vẽ TikZ ra ảnh độ phân giải cao (300 DPI) chèn vào đúng vị trí trong file `.docx`.
