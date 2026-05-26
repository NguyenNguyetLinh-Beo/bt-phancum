# bt-phancum
---

## 🎥 Video demo
[https://youtu.be/4h85vv_rx7U](https://youtu.be/Vi1N104zPds)

# 📊 PHÂN CỤM SINH VIÊN K58KTP BẰNG K-MEANS

## 🎯 Giới thiệu
Dự án này thực hiện phân tích dữ liệu điểm sinh viên lớp K58KTP và áp dụng thuật toán K-Means Clustering để nhóm sinh viên có mức học tập tương tự nhau.

Ý tưởng chính là thay vì nhìn thủ công từng bảng điểm rất dài, ta dùng Machine Learning để tự động tìm ra các nhóm sinh viên có đặc điểm học tập gần giống nhau, từ đó hỗ trợ việc đánh giá tổng quan chất lượng học tập của lớp.

**Sinh viên thực hiện:** Nguyễn Nguyệt Linh  
**Lớp:** 58KTPM  
**Môn học:** Phát triển ứng dụng với mã nguồn mở - TEE0421 

---

## 📁 Dữ liệu sử dụng
File dữ liệu:
TỔNG HỢP ĐIỂM K58KTP.xlsx

Trong dữ liệu gồm:
- Mã số sinh viên (MSSV)
- Họ tên sinh viên
- Điểm các môn học

Sau khi xử lý và làm sạch:
- 71 sinh viên
- 52 môn học

Dữ liệu ban đầu là dạng bảng thô nên cần phải xử lý lại để phù hợp với mô hình học máy.

---

## 🛠️ Công nghệ sử dụng
- Python 3
- Pandas (xử lý dữ liệu)
- NumPy (tính toán số học)
- Scikit-learn (KMeans, StandardScaler, Imputer)
- Matplotlib (trực quan hóa)
- OpenPyXL (đọc file Excel)

---

## 📦 Cài đặt thư viện
Để chạy chương trình, cài đặt các thư viện sau:

pip install pandas numpy scikit-learn matplotlib openpyxl

---

## 🔄 Các bước thực hiện

### 1. Đọc dữ liệu
Sử dụng Pandas để đọc file Excel chứa bảng điểm sinh viên. Vì dữ liệu ban đầu chưa sạch nên phải đọc ở dạng thô để xử lý tiếp.

---

### 2. Làm sạch dữ liệu
Trong bước này, dữ liệu được xử lý để:
- Chuyển các giá trị về dạng số
- Xử lý lỗi Excel (có trường hợp điểm bị đọc thành ngày tháng)
- Thay thế các giá trị thiếu

Mục tiêu là đảm bảo dữ liệu đầu vào cho mô hình không bị sai lệch.

---

### 3. Chuẩn hóa dữ liệu
Sử dụng StandardScaler để đưa tất cả các môn học về cùng một thang đo.

Điều này rất quan trọng vì K-Means dựa trên khoảng cách, nếu dữ liệu không cùng scale thì kết quả sẽ bị sai.

---

### 4. Áp dụng K-Means
Thuật toán K-Means được sử dụng với k = 3 để phân nhóm sinh viên thành 3 cụm.

Mỗi cụm đại diện cho một nhóm sinh viên có mức độ học tập tương tự nhau dựa trên dữ liệu điểm.

---

### 5. Đánh giá mô hình
Sử dụng Silhouette Score để kiểm tra chất lượng phân cụm.

Kết quả:
Silhouette Score ≈ 0.0922

Điều này cho thấy các nhóm chưa tách biệt quá rõ, nhưng vẫn có cấu trúc phân nhóm trong dữ liệu.

---

### 6. Phân loại học lực
Sau khi có kết quả phân cụm, tiến hành tính điểm trung bình và gán nhãn học lực cho sinh viên:

- Cần cải thiện
- Trung bình
- Học tốt

Ngoài ra cũng có thể dựa vào cluster để gán nhãn theo mức điểm trung bình của từng nhóm.

---

## 📊 Kết quả đạt được
- Phân cụm sinh viên thành 3 nhóm
- Tính được điểm trung bình từng sinh viên
- Thống kê điểm theo từng nhóm
- Trực quan hóa dữ liệu
- Xuất file Excel kết quả cuối

---

## 📈 Nhận xét
Kết quả cho thấy nhóm “Trung bình” chiếm đa số, tiếp theo là nhóm “Cần cải thiện”, và nhóm “Học tốt” chiếm ít hơn. Điều này phản ánh đúng thực tế học tập của lớp, nơi phần lớn sinh viên đang ở mức trung bình.

---

## ⚠️ Hạn chế
- Silhouette Score còn thấp nên độ phân tách chưa cao
- Kết quả phụ thuộc vào việc chọn số cụm k
- K-Means nhạy với dữ liệu nhiễu và ngoại lệ

---

## 🚀 Hướng phát triển
- Sử dụng Elbow Method để chọn k tối ưu hơn
- Thử các thuật toán khác như DBSCAN hoặc Hierarchical Clustering
- Cải thiện feature (điểm môn quan trọng hơn có thể được weighting)

---

## ❓ Câu hỏi thảo luận + Trả lời

### 1. Vì sao cần chuẩn hóa dữ liệu trước khi dùng K-Means?
👉 Vì K-Means dựa trên khoảng cách giữa các điểm dữ liệu. Nếu không chuẩn hóa, các môn có thang điểm lớn sẽ chi phối kết quả, làm sai lệch phân cụm. Chuẩn hóa giúp tất cả đặc trưng có cùng thang đo.

---

### 2. Nếu thay đổi số cụm (k) thì kết quả có thay đổi không?
👉 Có. Khi tăng hoặc giảm k, cách phân nhóm sinh viên sẽ thay đổi. Nếu k quá nhỏ thì nhóm bị gộp, nếu k quá lớn thì bị chia quá chi tiết. Vì vậy cần chọn k hợp lý.

---

### 3. Silhouette Score = 0.0922 nói lên điều gì?
👉 Giá trị này khá thấp, cho thấy các cụm chưa tách biệt rõ ràng. Điều đó nghĩa là dữ liệu có sự chồng lấn giữa các nhóm học lực.

---

### 4. Ngoài K-Means có thể dùng thuật toán nào khác?
👉 Có thể dùng DBSCAN hoặc Hierarchical Clustering. Các thuật toán này có thể xử lý dữ liệu phức tạp hơn và không cần chọn k cố định như K-Means.

---
### 5. Phân loại học lực bằng clustering có hoàn toàn chính xác không?
👉 Không hoàn toàn chính xác, vì clustering chỉ dựa trên dữ liệu mà không có nhãn thật. Nó chỉ mang tính tham khảo để phân tích xu hướng, không thay thế được đánh giá chính thức.

---

## 🧠 Nhận xét cá nhân

Qua bài thực hành này, em hiểu rõ hơn cách áp dụng Machine Learning vào một bài toán thực tế như phân tích dữ liệu sinh viên. Việc sử dụng thuật toán K-Means giúp em thấy được cách máy tính có thể tự động nhóm dữ liệu dựa trên mức độ tương đồng mà không cần gán nhãn trước.

Trong quá trình làm bài, em gặp khá nhiều vấn đề như dữ liệu bị thiếu, lỗi định dạng từ Excel, hoặc kết quả phân cụm chưa rõ ràng. Tuy nhiên, qua việc xử lý và thử nghiệm nhiều bước như làm sạch dữ liệu, chuẩn hóa và đánh giá mô hình, em đã hiểu hơn về quy trình xây dựng một bài toán Machine Learning hoàn chỉnh.

Bài tập cũng giúp em nhận ra rằng K-Means không phải lúc nào cũng cho kết quả hoàn hảo, đặc biệt khi dữ liệu có sự chồng lấn giữa các nhóm. Vì vậy, việc chọn số cụm và xử lý dữ liệu đầu vào đóng vai trò rất quan trọng.

Tổng kết lại, bài thực hành này giúp em củng cố kiến thức về Python, xử lý dữ liệu và thuật toán K-Means, đồng thời hiểu rõ hơn cách phân tích dữ liệu trong thực tế.

