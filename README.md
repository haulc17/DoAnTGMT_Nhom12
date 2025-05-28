# Nhóm 12: Đề tài nhận diện chữ viết tay
Thành Viên:
## 1 Đào Xuân Hậu - 0072767
## 2 Hoàng Khắc Anh Nhật -0203767
## 3 Nguyễn Đăng Tú - 0109367
## 4 Trần Đoàn Quang Vũ - 0088667
# I: Giới thiệu 
Trong thời đại số hóa hiện nay, khối lượng tài liệu cần xử lý ngày càng lớn, bao gồm cả văn bản đánh máy và chữ viết tay. Việc hai hình thức chữ này đồng thời xuất hiện trong cùng một tập tài liệu – chẳng hạn như thư tay, email in ra, đơn từ, hay biểu mẫu khảo sát – có thể gây khó khăn trong việc đọc hiểu và trích xuất thông tin, đặc biệt khi chữ viết tay có sự khác biệt lớn giữa các cá nhân. Điều này dẫn đến nhu cầu cấp thiết về các hệ thống tự động nhận diện chữ viết tay, nhằm hỗ trợ người dùng đọc nhanh hơn, chính xác hơn và dễ dàng hơn. Bên cạnh đó, việc chuyển đổi chữ viết tay thành văn bản số hóa còn góp phần quan trọng trong việc lưu trữ, tìm kiếm, phân tích dữ liệu và nâng cao hiệu quả làm việc trong nhiều lĩnh vực như giáo dục, hành chính, y tế và tài chính. Do vậy, nghiên cứu và phát triển các phương pháp nhận diện chữ viết tay đang ngày càng trở thành một hướng đi tiềm năng và có giá trị thực tiễn cao trong lĩnh vực trí tuệ nhân tạo và xử lý ảnh.
# II: Tổng quan về đề tài
 Nhận diện chữ viết tay là một lĩnh vực quan trọng trong trí tuệ nhân tạo và xử lý hình ảnh , tập trung vào việc phát triển các hệ thống có khả năng tự đông nhận dạng và chuyển đổi chữ viết tay thành văn bản kỹ thuật số. Với sự phát triển của các mô hình công nghệ như : mạng nơ-ron tích chập (CNN) và mạng nơ-ron hồi quy (RNN),…. Đã đạt được những kết quả ấn tượng trong việc xử lý các mẫu viết tay đa dạng , như nhận dạng chữ viết tay tiếng việt .Đề tài này không chỉ có ý nghĩa trong việc số hoá tài liệu , mà còn hỗ trợ các ứng dụng thực tiễn như nhận diện chữ viết trên thiết bị di động , hỗ trợ người khiếm thị ,…Tuy nhiên , thách thức lớn nhất là sự đa dạng trong phong cách viết , chất lượng hình ảnh 
# III Cơ sở lý thuyết
## 1 Tiền xử  lý ảnh
### A Chuyển đổi sang ảnh xám 
Mỗi pixel trong ảnh màu RGB được biểu diễn bằng ba giá trị (Red, Green, Blue).
Để chuyển sang ảnh xám, giá trị RGB của mỗi pixel được thay bằng một giá trị cường độ sáng duy nhất (grayscale intensity). 
Giá trị xám thường được tính bằng công thức trung bình có trọng số của các kênh màu, dựa trên độ nhạy của mắt người với các màu:
                                   I = 0.299R + 0.587G + 0.114B          
                                   
![Picture1](https://github.com/user-attachments/assets/cd9fbc15-cc15-4091-831e-94d7845c3525)

![Picture2](https://github.com/user-attachments/assets/078d9aac-b89d-4c63-acd7-422654cfc6c7)

### B Giảm nhiễu
Giảm nhiễu mục đích là loại bỏ hoặc giảm nhiễu để cải thiện chất lượng ảnh do bị tác động do cảm biến , điều kiện môi trường , do đường truyền tải dữ liệu
**Các phương pháp phổ biến:**
**1. Lọc không gian (Spatial Filtering):**
  + **Lọc trung bình (Mean Filter):** Thay giá trị pixel bằng trung bình của vùng lân cận, làm mờ nhiễu nhưng có thể làm mất chi tiết.
  + **Lọc trung vị (Median Filter):** Thay giá trị pixel bằng trung vị của vùng lân cận, hiệu quả với nhiễu muối-tiêu (salt-and-pepper).
  + **Lọc Gaussian:** Dùng hàm Gaussian để làm mịn, giữ chi tiết tốt hơn lọc trung bình.
**2. Lọc tần số (Frequency Domain Filtering):**
  + Chuyển tín hiệu sang miền tần số (dùng biến đổi Fourier).
  + Loại bỏ tần số cao (thường liên quan đến nhiễu) bằng bộ lọc thông thấp.
**3. Phương pháp nâng cao:**
  + **Wavelet Denoising:** Phân tích tín hiệu ở các mức độ chi tiết khác nhau, loại bỏ nhiễu trong các băng tần cụ thể.
  + **Non-Local Means:** So sánh các vùng tương tự trong ảnh để bảo toàn cấu trúc và giảm nhiễu.
  + **Học sâu (Deep Learning):** Sử dụng mạng nơ-ron để học cách khôi phục tín hiệu gốc từ dữ liệu nhiễu.
### C Cải thiện độ tương phản
Nhằm tăng cường sự khác biệt giữa các mức sáng tối , giúp chi tiết ảnh rõ ràng và nhận biết hơn
**Phương pháp phổ biến:**
**1. Điều chỉnh tuyến tính (Linear Contrast Stretching):**
- Kéo dãn phạm vi giá trị pixel để sử dụng toàn bộ thang giá trị (thường từ 0 đến 255 trong ảnh 8-bit).
- Công thức   : I_out=(I_in-min/max-min)x255                          
**2. Cân bằng biểu đồ (Histogram Equalization):**
- Phân bố lại giá trị pixel dựa trên biểu đồ (histogram) để tăng cường độ tương phản toàn cục.
- Hiệu quả với ảnh có phân bố giá trị pixel tập trung trong một khoảng hẹp.
**3. Cải thiện cục bộ (Local Contrast Enhancement):** 
- Áp dụng các kỹ thuật như lọc CLAHE (Contrast Limited Adaptive Histogram Equalization) để tăng tương phản trong từng vùng nhỏ, bảo toàn chi tiết.
## 2: Tách dòng ( Object detection) 
- Phát hiện đối tượng (object detection): Là nhiệm vụ khó khăn hơn và là sự kết hợp của cả hai nhiệm vụ trên: Vẽ một bounding box xung quanh từng đối tượng quan tâm trong ảnh và gán cho chúng một nhãn. Kết hợp cùng nhau, tất cả các vấn đề này được gọi là object recognition hoặc object detection.
- Một vài thư viện có thể được dùng trong object detection: OpenCV (Open Source Computer Vision Library), TensorFlow Object Detection API, KerasCV, …..
- Phát hiện đối tượng: Xác định vị trí hiện diện của các đối tượng trong bounding box và nhãn của các đối tượng nằm trong một hình ảnh.
	+ Input: Một hình ảnh có một hoặc nhiều đối tượng, chẳng hạn như một bức ảnh.
	+ Output: Một hoặc nhiều bounding box và nhãn cho mỗi bounding box.
3 Mô hình thị giác máy tính
3.1: CNN
mô hình CNN để training và kiểm tra, mỗi hình ảnh đầu vào sẽ chuyển nó qua 1 loạt các lớp tích chập với các bộ lọc (Kernals), tổng hợp lại các lớp được kết nối đầy đủ (Full Connected) và áp dụng hàm Softmax để phân loại đối tượng có giá trị xác suất giữa 0 và 1. Hình dưới đây là toàn bộ luồng CNN để xử lý hình ảnh đầu vào và phân loại các đối tượng dựa trên giá trị.

![Picture3](https://github.com/user-attachments/assets/639007e8-ea9b-4af6-a747-51777d173ba5)

**A Lớp tích chập - Convolution Layer**
Tích chập là lớp đầu tiên để trích xuất các tính năng từ hình ảnh đầu vào. Tích chập duy trì mối quan hệ giữa các pixel bằng cách tìm hiểu các tính năng hình ảnh bằng cách sử dụng các ô vương nhỏ của dữ liệu đầu vào. Nó là 1 phép toán có 2 đầu vào như ma trận hình ảnh và 1 bộ lọc hoặc hạt nhân.

![Picture4](https://github.com/user-attachments/assets/524cb682-b186-4696-b686-f71a732ce144)

 
Sự kết hợp của 1 hình ảnh với các bộ lọc khác nhau có thể thực hiện các hoạt động như phát hiện cạnh, làm mờ và làm sắc nét bằng cách áp dụng các bộ lọc. Ví dụ dưới đây cho thấy hình ảnh tích chập khác nhau sau khi áp dụng các Kernel khác nhau.

![Picture5](https://github.com/user-attachments/assets/e619a33a-a93d-44fa-848a-e3945e1bf7f3)
                   
**B Bước nhảy - Stride**
Stride là số pixel thay đổi trên ma trận đầu vào. Khi stride là 1 thì ta di chuyển các kernel 1 pixel. Khi stride là 2 thì ta di chuyển các kernel đi 2 pixel và tiếp tục như vậy. Hình dưới là lớp tích chập hoạt động với stride là 2.

![Picture6](https://github.com/user-attachments/assets/2e092bb7-dd33-4f0b-904c-3dfb89f42c6f)

**C Đường viền - Padding**
+ Đôi khi kernel không phù hợp với hình ảnh đầu vào. Ta có 2 lựa chọn:
+ Chèn thêm các số 0 vào 4 đường biên của hình ảnh (padding).
+ Cắt bớt hình ảnh tại những điểm không phù hợp với kernel.

**D  Hàm phi tuyến - ReLU**
+ ReLU viết tắt của Rectified Linear Unit, là 1 hàm phi tuyến. Với đầu ra là: ƒ(x) = max(0, x).
+ Tại sao ReLU lại quan trọng: ReLU giới thiệu tính phi tuyến trong ConvNet. Vì dữ liệu trong thế giới mà chúng ta tìm hiểu là các giá trị tuyến tính không âm.

![Picture7](https://github.com/user-attachments/assets/374a0b5d-a570-4b20-86ed-4dfe1d076b16)

**E Lớp gộp - Pooling Layer**
+ Lớp pooling sẽ giảm bớt số lượng tham số khi hình ảnh quá lớn. Không gian pooling còn được gọi là lấy mẫu con hoặc lấy mẫu xuống làm giảm kích thước của mỗi map nhưng vẫn giữ lại thông tin quan trọng. Các pooling có thể có nhiều loại khác nhau:
+ Max Pooling
+ Average Pooling
+ Sum Pooling
+ Max pooling lấy phần tử lớn nhất từ ma trận đối tượng, hoặc lấy tổng trung bình. Tổng tất cả các phần tử trong map gọi là sum pooling

![Picture8](https://github.com/user-attachments/assets/de4febd9-2142-48b5-991c-884d8b97f91c)

3.2 TransformerOCR
**3.2.1 TranformerOCR là gì?**
  TransformerOCR là một kiến trúc mô  hình học sâu dựa trên cơ chế self-attention, cho phép mô hình này hiểu được mỗi quan hệ giữa các từ trong một câu mà không cần đến kiến trúc tuần tự truyền thống như RNN hay LSTM . Transformer có khả năng xử lý toàn bộ câu cùng một lúc , điều này giúp tăng tốc huấn luyện và cải thiện hiệu quả xử lý
**3.2.2 Đặc điểm nổi bật**
**Các điểm nổi bật chính của Transformer là:** 
+ Xử lý song song: Transformer xử lý đầu vào theo từng khối, không tuần tự. Điều này cho phép việc huấn luyện mô hình được thực hiện song song, giảm đáng kể thời gian cần thiết để huấn luyện mô hình.
+ Self-Attention: Cơ chế này giúp Transformer xác định được mối quan hệ giữa tất cả các từ trong một câu, bất kể khoảng cách giữa chúng trong văn bản, giải quyết vấn đề về phụ thuộc dài hạn.
+ Hiệu suất và mở rộng: Với khả năng xử lý đồng thời, Transformer tận dụng tối đa sức mạnh của phần cứng hiện đại, như GPU và TPU, để xử lý các tác vụ NLP một cách hiệu quả.
3.2.3 **Tranformer hoạt động như thế nào?**
Cốt lõi của transformer là attension mechanism (cơ chế tập trung), giúp mô hình tập trung vào các phần quan trọng của văn bản để đưa ra dự đoán chính xác hơn.
Transformer được cấu trúc thành hai phần chính là encoder và decoder.
  + Encoder: Encoder xử lý dữ liệu đầu vào (gọi là "Source") và nén dữ liệu vào vùng nhớ hoặc context mà Decoder có thể sử dụng sau đó.
  + Decoder: Decoder nhận đầu vào từ đầu ra của Encoder (gọi là "Encoded input") kết hợp với một chuỗi đầu vào khác (gọi là "Target") để tạo ra chuỗi đầu ra cuối cùng.
  + Mỗi encoder và decoder đều bao gồm nhiều lớp, mỗi lớp chứa các thành phần self-attention và feed-forward neural networks.
Về cơ bản, quy trình hoạt động của Tranformer gồm các bước sau :

<img width="404" alt="Picture9" src="https://github.com/user-attachments/assets/9e72e3bf-6d7b-4ea5-9b15-535834d2ca0d" />

**Bước 1: Preprocessing (tiền xử lý).**
	- Tokenization: Dữ liệu đầu vào được biến đổi thành token. Ví dụ, câu      "ChatGPT là gì?" sẽ được mã hoá thành 4 token ["ChatGPT, "là", "gì", "?"].
	- Embedding: Biến token thành vector. Mỗi token được chuyển thành một vector
	- Positional Encoding: Vì Transformer không xử lý tuần tự nên cần một cách để hiểu vị trí của từng từ trong câu. Điều này được thực hiện thông qua positional encodings, được cộng trực tiếp vào input embeddings. Các positional encodings có thể dùng các hàm sin và cos với bước sóng khác nhau để mỗi vị trí có một encoding duy nhất
**Bước 2: Encoder.**
Encoder bao gồm nhiều layer (lớp) xếp chồng lên nhau (stack). Mỗi layer có 2 sublayer là Multi-Head Attention và Positionwise Feed-forward Neural Network (FNN). Output của 2 sublayer sẽ đi qua một lớp gọi là Add & Norm.

 <img width="185" alt="Picture10" src="https://github.com/user-attachments/assets/58d7b07b-83c0-4643-91e0-9f54c5b0a68d" />

	- Multi-Head Attention: Dữ liệu đầu vào được truyền vào nhiều head để tạo một tập các vector đầu ra. Multi-head attention được thiết kế để cho phép mô hình xử lý thông tin đồng thời ở các không gian không gian (subspaces) khác nhau. Thay vì có một module attention duy nhất, mô hình có nhiều "heads", mỗi head có thể tập trung vào các phần khác nhau của đầu vào.
	- Positionwise Feed-forward Neural Network (FNN): Các vector đầu ra của attention head được truyền qua positionwise feed-forward neural network (mạng thần kinh chuyển tiếp theo vị trí). Mỗi head trong khối có một mạng FNN riêng, cho phép mô hình học được các biểu diễn dựa trên nhiều không gian không gian (subspaces) khác nhau của dữ liệu. Mục tiêu là tạo một lớp biểu diễn phi tuyến tính (non-linear representation) của dữ liệu đầu vào, giúp mô hình có khả năng học được các mối quan hệ phức tạp và phi tuyến tính của dữ liệu.
	- Add & Norm: Bao gồm hai bước Add và Norm. Bước Add thêm residual connection (kết nối dư) nhằm giảm vấn đề vanishing gradient (mất độ dốc) trong các deep network (mạng sâu). Ngay sau đó, bước Norm thực hiện layer normalization (chuẩn hoá lớp) giúp ổn định quá trình huấn luyện và giảm số lượng giai đoạn cần thiết để huấn luyện.

<img width="353" alt="Picture11" src="https://github.com/user-attachments/assets/5d32e162-fd4a-43d1-9e09-371983054a1c" />

**Bước 3: Decoder.**
Tương tự Encoder, Decoder cũng có 2 sublayer và có thêm 1 sublayer ở nằm giữa 2 sublayer tên là Encode-decode Attention   

<img width="179" alt="Picture12" src="https://github.com/user-attachments/assets/2ebb711e-c9f2-4230-a40b-f990d2e07d18" />
                  
- **Masked Multi-Head Attention:** Là một biến thể của Multi-Head Attention, hoạt động tương tự Multi-Head Attention nhưng có "mask" để đảm bảo rằng các vị trí trong output chỉ có thể tập trung vào các từ trước đó mà không "nhìn thấy" các từ tiếp theo (điều này quan trọng cho quá trình dự đoán từ tiếp theo).
- **Multi-Head Attention:** Hoạt động giống với bước Encoder.
- **Encode-decode Attention:** Trong Encode-decode Attention, truy vấn tới từ đầu ra của lớp con Attention, còn key và value tới từ đầu ra của Encoder.
- **Positionwise Feed-forward Neural Network (FNN):** Hoạt động giống với bước Encoder.
- **Add & Norm:** Hoạt động giống với bước Encoder.
Đầu ra của Decoder thường là một chuỗi các vector. Mỗi vector tương ứng với một từ trong chuỗi đầu ra. Các vector này sau đó được chuyển qua một lớp tuyến tính (linear layer) và một hàm softmax để tạo ra một phân phối xác suất trên tất cả các từ trong từ điển. Sau cùng, từ có xác suất cao nhất được chọn làm từ dự đoán tiếp theo trong chuỗi. Quy trình này lặp lại cho mỗi từ trong chuỗi đầu ra, cho tới khi mô hình dự đoán ra ký tự kết thúc câu hoặc đạt độ dài tối đa cho phép.
IV : Phương pháp đề xuất

![Picture13](https://github.com/user-attachments/assets/db9d8159-41f8-4f45-8f4e-1d65fb23b8f7)

1: Chuẩn bị tập dữ liệu 
**Chuẩn bị dữ liệu** là quá trình xử lý và biến đổi dữ liệu thô thành định dạng phù hợp để huấn luyện mô hình học máy hoặc học sâu. Đây là bước rất quan trọng vì dữ liệu chất lượng kém sẽ dẫn đến mô hình không chính xác, dễ bị overfitting hoặc underfitting.
**1.1. Các bước chuẩn bị dữ liệu phổ biến**
**1.1.1 Thu thập dữ liệu (Data Collection)**
	- Thu thập dữ liệu từ nhiều nguồn như: cảm biến, cơ sở dữ liệu, API, website, v.v.
	- Có thể là dữ liệu dạng có nhãn (supervised) hoặc không có nhãn (unsupervised).
**1.1.2 Làm sạch dữ liệu (Data Cleaning)**
	- Xử lý các giá trị thiếu (missing values): xóa hoặc thay thế bằng trung bình, trung vị...
	- Loại bỏ dữ liệu nhiễu hoặc không hợp lệ.
	- Chuẩn hóa định dạng, loại bỏ trùng lặp.
**1.1.3 Gán nhãn dữ liệu (Labeling)**
	- Với các bài toán học có giám sát, cần gán nhãn cho từng dữ liệu (ví dụ: ảnh + nhãn "con mèo").
	- Có thể thực hiện thủ công hoặc bán tự động.
**1.1.4 Tiền xử lý dữ liệu (Preprocessing)**
	- Mã hóa dữ liệu phân loại: one-hot encoding, label encoding...
	- Chuẩn hóa dữ liệu số: min-max scaling, z-score standardization...
	- Chuyển đổi định dạng dữ liệu: ảnh → ma trận, văn bản → chuỗi token, v.v.
**1.1.5 Phân chia dữ liệu (Splitting Data)**
	- Training set: dùng để huấn luyện mô hình (~70–80%)
	- Validation set: điều chỉnh tham số mô hình (~10–15%)
	- Test set: đánh giá độ chính xác mô hình (~10–15%)
2 : Object detection( tách dòng)
**Thành phần chính của Object Detection**
	1. **Feature Extraction (Trích xuất đặc trưng)**
	Từ ảnh đầu vào, hệ thống cần hiểu nội dung bằng cách trích ra các đặc trưng (edges, textures, shapes...).
	2. **Bounding Box Regression (Dự đoán hộp giới hạn)**
	Xác định vị trí của mỗi đối tượng thông qua tọa độ hộp chữ nhật: (x, y, width, height).
	3. **Classification (Phân loại)**
	Gán nhãn cho từng đối tượng được phát hiện (như người, xe, mèo...).
	4. **Post-processing**
	Xử lý sau như Non-Maximum Suppression (NMS) để loại bỏ các hộp chồng lặp
Trong đoạn code:
Bước 1: Tiền xử lý ảnh (Preprocessing)

![Picture14](https://github.com/user-attachments/assets/548ca073-cfe4-486d-ac07-75189266dc0c)

	Chuyển ảnh về grayscale.
	Làm mờ để giảm nhiễu (Gaussian blur).
	Nhị phân hóa ảnh (threshold) để dễ phát hiện vật thể.
________________________________________
Bước 2: Giãn ảnh (Dilation) 

![Picture15](https://github.com/user-attachments/assets/ca608d57-255b-4aee-87ba-ebb1edb28203)

	Dùng morphological dilation để kết nối các ký tự thành dòng bằng cách giãn theo chiều ngang.
	Đây là thủ thuật cực kỳ phổ biến trong object detection thủ công để cải thiện shape.
________________________________________
Bước 3: Tìm contour

![Picture16](https://github.com/user-attachments/assets/e4095a94-703f-4d3a-b232-459491606b5f)

 Phát hiện biên của vật thể (dòng chữ).
	Mỗi contour là một object được phát hiện.
________________________________________
Bước 4: Tạo Bounding Box (tọa độ khung giới hạn)

![Picture17](https://github.com/user-attachments/assets/5fecd108-38ac-464c-bdd4-7bc1716b60a2)

 Mỗi contour được chuyển thành (x, y, w, h) → đại diện cho bounding box.
	Sắp xếp các box theo tọa độ Y để có thứ tự từ trên xuống dưới.
________________________________________
Bước 5: Lọc và trích xuất vùng dòng chữ

![Picture18](https://github.com/user-attachments/assets/867e676f-e74c-4924-87e5-5e8fe576b539)

 Lọc bỏ vùng quá nhỏ (nhiễu).
	Cắt vùng ảnh dòng chữ từ ảnh gốc → coi như object cropped from bounding box

![Picture19](https://github.com/user-attachments/assets/88d01af9-db99-43e7-abcd-325d5a766552)

![Picture20](https://github.com/user-attachments/assets/19e41e29-3d4e-4c19-8b34-2e6d6e6dc697)
 
3 Tiền xử lý 
Trong đề tài hôm nay , nhóm bọn em sử dụng các kỹ thuật như :
	Chuyển đổi sang ảnh xám 
	Thay đổi kích thước 
	Giảm nhiễu
	Cải thiện độ tương phản 
	Tăng độ nét
	Chuẩn hoá giá trị pixel và chuyển đổi sang tensor

Việc dùng các kỹ thuật trên cho việc tiền xử lý nhằm giúp:
	Loại bỏ nhiễu và yếu tố không cần thiết : Như màu sắc , nhiễu hạt , hoặc ánh sáng không đồng đều và định dạng 1 độ dài nhất định cố định cho ảnh
	Tăng cường đặc trưng : Làm nổi bật đường nét chữ , cải thiện độ tương phản 
	Chuẩn hoá dữ liệu : Đảm bảo đầu vào phù hợp với yêu cầu của mô hình
Ảnh nguyên gốc

![Picture21](https://github.com/user-attachments/assets/eb7f952e-00cb-43be-aeb0-ef9ea8f3ef03)

         
                   Ảnh sau khi qua tiền xử lý

![Picture22](https://github.com/user-attachments/assets/802d7ac7-266a-4d41-8ddb-c4be488527bd)

3 CNN
Trong phần CNN ta chủ yếu sử dùng mô hình để thực hiện các nhiệm vụ :
	Trích xuất đặc trưng cục bộ từ ảnh bằng các lớp Convolution (CNN): nét mảnh , nét đậm , đường cong , dấu câu , hình dạng chữ ,…..
	Giảm chiều (height) và giữ lại chiều width qua câu lệnh sau :( MaxPool2d(kernel_size=(2,1))) :Việc ta giảm chiều cao và giữ chiều ngang tránh không bị mất thông tin
	Biến đổi tensor về dạng chuỗi đặc trưng phù hợp để đưa vào Transformer (dạng (seq_len, batch_size, embed_dim)).:  

![Picture23](https://github.com/user-attachments/assets/11e7b3d7-7067-43ea-8b5b-c396481449e3)

4 Mô hình : TransformerOCR
	Sau khi ảnh đầu vào được xử lý qua các bước tiền xử lý và trích xuất đặc trưng bằng mạng CNN, ta thu được biểu diễn đặc trưng không gian của nội dung ảnh. Những đặc trưng này đóng vai trò như đầu vào cho các thành phần tiếp theo của mô hình TransformerOCR, bao gồm Encoder, Attention và Decoder, nhằm thực hiện nhiệm vụ giải mã chuỗi ký tự tương ứng với nội dung trong ảnh
	Attention:

![Picture24](https://github.com/user-attachments/assets/9cd413e0-ca3f-46f9-8461-7be676924b9f)

Encoder

![Picture25](https://github.com/user-attachments/assets/7cfe3d8c-4bc9-4004-9fb1-04246714f4cf)

Decoder

![Picture26](https://github.com/user-attachments/assets/b143fdda-7476-42ba-b6bb-c839d6015ee3)

5 Train model
Trong giai đoạn này, tôi tiến hành huấn luyện mô hình TransformerOCR trên tập dữ liệu huấn luyện. Sau mỗi epoch, mô hình được đánh giá trên tập validation để theo dõi quá trình học và điều chỉnh siêu tham số nếu cần thiết. Trọng số của mô hình tại epoch có hiệu suất tốt nhất sẽ được lưu lại để sử dụng ở bước dự đoán sau cùng.
Bộ từ vựng (vocabulary – vocab) được định nghĩa là tập hợp tất cả các ký tự mà mô hình có thể dự đoán, bao gồm chữ cái, chữ số, ký tự đặc biệt và các token đặc biệt như <sos> (start of sequence), <eos> (end of sequence), và <pad>. Việc xây dựng vocab rõ ràng là bước quan trọng để mô hình có thể học cách ánh xạ các đặc trưng đầu vào thành chuỗi ký tự đầu ra hợp lệ. Nói cách khác, vocab chính là không gian tìm kiếm mà mô hình sử dụng để dự đoán từng ký tự trong quá trình giải mã.
	Định nghĩa bộ từ vựng 
```python
special_tokens = ["<PAD>", "<SOS>", "<EOS>"]
alphabet = "aAàÀảẢãÃáÁạẠăĂằẰẳẲẵẴắẮặẶâÂầẦẩẨẫẪấẤậẬbBcCdDđĐeEèÈẻẺẽẼéÉẹẸêÊềỀểỂễỄếẾệỆfFgGhHiIìÌỉỈĩĨíÍịỊjJkKlLmMnNoOòÒỏỎõÕóÓọỌôÔồỒổỔỗỖốỐộỘơƠờỜởỞỡỠớỚợỢpPqQrRsStTuUùÙủỦũŨúÚụỤưƯừỪửỬữỮứỨựỰvVwWxXyYỳỲỷỶỹỸýÝỵỴzZ0123456789!#$%&\'()*+,-./:;<=>?@[\\]^_`{|}~ "
characters = special_tokens + list(alphabet)
vocab = {char: idx for idx, char in enumerate(characters)}
vocab_size = len(vocab)
```
Khởi tạo epoch và batch_size 
  ```python
	BATCH_SIZE = 32
	EPOCHS = 25
  ```
Train model 
  ```python
	def train_model(label_file, model_name):
	    dataset = OCRDataset(IMG_DIR, label_file, transform)
	    dataloader = DataLoader(dataset, batch_size=BATCH_SIZE, shuffle=True, collate_fn=collate_fn)
	
	    model = TransformerOCR(vocab_size).to(device)
	    criterion = nn.CrossEntropyLoss(ignore_index=vocab["<PAD>"])
	    optimizer = optim.Adam(model.parameters(), lr=1e-4)
	
	    train_losses = []
	    val_losses = []
	
	    for epoch in range(EPOCHS):
	        model.train()
	        total_loss = 0
	
	        for images, labels in dataloader:
	            images, labels = images.to(device), labels.to(device)
	            tgt_input = labels[:, :-1].long()
	            tgt_output = labels[:, 1:].long()
	            optimizer.zero_grad()
	            output = model(tgt_input, tgt_input)
	            loss = criterion(output.reshape(-1, vocab_size), tgt_output.reshape(-1))
	            loss.backward()
	            optimizer.step()
	            total_loss += loss.item()
	
	        avg_train_loss = total_loss / len(dataloader)
	        train_losses.append(avg_train_loss)
	        print(f"{model_name} - Epoch [{epoch + 1}/{EPOCHS}], Train Loss: {avg_train_loss:.4f}")
  ```
6 Dự đoán
Ở giai đoạn suy luận (inference), tôi sử dụng mô hình VietOCR đã được tiền huấn luyện trên tập dữ liệu tiếng Việt để thực hiện nhận dạng văn bản từ ảnh. VietOCR là một mô hình OCR hiện đại kết hợp giữa CNN Encoder và Transformer Decoder, được huấn luyện với cơ chế Attention và hàm mất mát Cross-Entropy nhằm sinh ra chuỗi ký tự chính xác từ ảnh văn bản đầu vào.
Trước khi đưa ảnh vào mô hình, dữ liệu được tiền xử lý qua các bước như chuyển ảnh về thang xám, thay đổi kích thước và chuẩn hóa để đảm bảo tương thích với định dạng đầu vào của mô hình. Sau đó, ảnh được đưa vào mô hình VietOCR để tạo ra chuỗi văn bản đầu ra thông qua cơ chế giải mã tự động.
Việc sử dụng mô hình pretrained giúp tận dụng các trọng số đã học trên tập dữ liệu lớn, từ đó cải thiện hiệu suất nhận dạng và giảm thời gian huấn luyện lại trên tập dữ liệu mới.

![Picture27](https://github.com/user-attachments/assets/4036a1f9-1774-426a-ab0e-29c8c219e923)

 
V Thực nghiệm và đánh giá 
1 mô tả dữ liệu và cách chia dữ liệu 
Để đảm bảo mô hình được huấn luyện và đánh giá một cách hiệu quả,  dữ liệu ban đầu gồm có 1 folder chứa ảnh và 1 file (.txt) chứa nhãn từng ảnh tương ứng. Trong file (.txt)  được chia thành ba tập riêng biệt: tập huấn luyện (train), tập kiểm định (validation) và tập kiểm tra (test). Cụ thể, dữ liệu được đọc từ một tệp gốc chứa toàn bộ thông tin (ví dụ: label.txt), sau đó được chia ngẫu nhiên theo tỷ lệ ngẫu nhiêu do người dùng mong muốn 
Quá trình chia dữ liệu được thực hiện bằng cách xáo trộn toàn bộ các dòng dữ liệu, sau đó phân chia theo tỷ lệ . Mỗi phần dữ liệu sau khi chia được lưu vào các tệp riêng biệt: train.txt, val.txt và test.txt. Việc chia dữ liệu như vậy giúp đảm bảo rằng mô hình không bị overfitting và có thể đánh giá được khả năng tổng quát hoá trên các dữ liệu chưa từng thấy trong quá trình huấn luyện

![Picture28](https://github.com/user-attachments/assets/23ec1580-0e9d-492d-aef4-358dc705ba97)

![Picture29](https://github.com/user-attachments/assets/354336a6-1756-4ca5-ba35-b0742049dc86)

![Picture30](https://github.com/user-attachments/assets/5a9cb393-148b-4d87-9fd0-eb7887d4a87b)

![Picture31](https://github.com/user-attachments/assets/ca9f81b5-197d-4423-a477-bb7cd9e74452)

![Picture32](https://github.com/user-attachments/assets/9638a46f-2c25-48a1-882f-6f1141e54aa5)


  

        

   

2 Đánh giá kết quả học của mô hình 
Để đánh giá chất lượng học của mô hình, ta theo dõi và so sánh xu hướng thay đổi của hàm mất mát (loss) trên hai tập dữ liệu: huấn luyện (train) và kiểm định (validation) qua từng epoch
Trường hợp lỗi: Thiếu ký tự trong bộ từ vựng (vocab)
Trong quá trình huấn luyện mô hình, bộ từ vựng (vocab) được định nghĩa để mô hình học các đặc trưng ký tự cần thiết cho việc sinh ra chuỗi đầu ra. Tuy nhiên, nếu vocab không được xây dựng đầy đủ – tức là thiếu các ký tự thực tế có trong dữ liệu nhãn – mô hình sẽ không thể học cách sinh ra những ký tự này. Điều này dẫn đến việc mô hình bị giới hạn khả năng dự đoán, đặc biệt khi gặp phải các mẫu chứa ký tự ngoài vocab (out-of-vocabulary – OOV).
Hệ quả là hàm mất mát (loss) trên tập huấn luyện có thể tiếp tục giảm do mô hình chỉ học tốt các ký tự nằm trong vocab, trong khi loss trên tập kiểm định (validation) lại không cải thiện hoặc thậm chí tăng dần. Hiện tượng này phản ánh tình trạng overfitting, khi mô hình học quá khớp với các mẫu trong train set nhưng không có khả năng tổng quát hoá với dữ liệu thực tế chứa các ký tự mà nó chưa từng thấy trong quá trình huấn luyện

![Picture33](https://github.com/user-attachments/assets/a460a627-172c-4a9d-bee9-9ec4302793fd)

	Cách sửa lỗi : Để khắc phục lỗi do thiếu ký tự trong bộ từ vựng, ta cần kiểm tra lại toàn bộ tập dữ liệu nhãn (ground truth) nhằm đảm bảo rằng tất cả các ký tự có khả năng xuất hiện đều đã được đưa vào vocab. Việc bổ sung đầy đủ vocab giúp mô hình học được toàn diện hơn và có khả năng tổng quát hóa tốt hơn khi dự đoán chuỗi văn bản mới

![Picture34](https://github.com/user-attachments/assets/07a02487-6e74-495d-9208-1c65b2c86b17)

3 Dự đoán  và đánh giá các chỉ số 
      Các chỉ số đánh giá :
          Accuracy: tính theo tỷ lệ chuỗi chính xác hoàn toàn
                              Accuracy=(Số lượng từ dự đoán trùng khớp với nhãn)/(tổng số từ)
       WER( Word Error Rate) : tính toán số lượng từ ( ký tự sai ) so với nhãn
                            WER =(edit_distance(words))/(len(reference_words))
	Dự đoán ảnh riêng lẻ

![Picture35](https://github.com/user-attachments/assets/94f4962c-a4b8-4821-b0d3-ffb99a7e1a0b)

	 Ta test trên 1 tập ảnh gồm n ảnh và nhãn tương ứng:  

![Picture36](https://github.com/user-attachments/assets/9f736f77-ef45-45c0-b76e-35db2c468caa)

	
4 Giao diện ứng dụng 
Ta thiết lập màn hình giao diện nhỏ để hiện thị kết quả khi tải ảnh cần dịch:
 

![Picture37](https://github.com/user-attachments/assets/b641385b-4cfd-4002-b940-f846f84d3fe8)

VI:Kết luận và hướng phát triển
Tổng kết những gì đã đạt được
Trong khuôn khổ đề tài, chúng tôi đã nghiên cứu và xây dựng một hệ thống nhận diện chữ viết tay dựa trên các phương pháp học sâu hiện đại. Hệ thống được thiết kế theo hướng end-to-end, bao gồm các bước tiền xử lý ảnh, trích xuất đặc trưng bằng mạng CNN, mô hình hóa chuỗi ký tự bằng RNN hoặc Transformer, và sử dụng hàm mất mát CTC để huấn luyện. Thông qua các thực nghiệm trên tập dữ liệu mẫu, mô hình cho thấy khả năng nhận diện chữ viết tay ở mức độ chấp nhận được, với độ chính xác khá cao trên các trường hợp viết rõ ràng và thống nhất.
Hạn chế của hệ thống
Mặc dù hệ thống đã đạt được một số kết quả khả quan, vẫn còn tồn tại nhiều hạn chế cần được khắc phục. Trước hết, mô hình chưa xử lý hiệu quả các trường hợp chữ viết tay phức tạp, mờ nhòe hoặc có đặc điểm khó nhận diện. Bên cạnh đó, khi tập dữ liệu huấn luyện còn hạn chế về số lượng và đa dạng, mô hình gặp khó khăn trong việc nhận dạng chính xác các mẫu mới. Ngoài ra, quá trình tiền xử lý ảnh chưa được tối ưu hoàn toàn, dẫn đến chất lượng dữ liệu đầu vào chưa đạt mức tốt nhất, ảnh hưởng trực tiếp đến kết quả dự đoán của mô hình. Cuối cùng, do hạn chế về nguồn dữ liệu lớn cùng với giới hạn tài nguyên tính toán, mô hình chưa được huấn luyện trên tập dữ liệu đủ phong phú và đa dạng để đảm bảo khả năng tổng quát hóa cao khi áp dụng trên dữ liệu thực tế.Chưa tối ưu hoá và ràng buộc được các điều kiện việc tách từng dòng cho phù hợp(bởi vì phong cách viết và trình bày của mỗi người là khác nhau)
Định hướng tương lai
Trong các bước tiếp theo, chúng tôi định hướng phát triển hệ thống theo các hướng sau:
	Tích hợp mô hình ngôn ngữ Việt (Language Model) để cải thiện khả năng hiệu chỉnh lỗi và tăng tính logic của kết quả đầu ra.
	Ứng dụng các kiến trúc mới như Vision Transformer (ViT) để nâng cao hiệu suất mô hình.
	Thu thập và mở rộng tập dữ liệu, đa dạng về phong cách viết và chất lượng ảnh, giúp mô hình học tốt hơn trên các tình huống thực tế.

