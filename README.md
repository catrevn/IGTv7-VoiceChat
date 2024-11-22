# IGTv7-Neural-Network-for-AI
A complete Neural-Network system for AI.
## Chuẩn bị :
# 1. Tải mô hình + mô hình phân tích cảm xúc = IGTv6; IGTv7
IGTv6J là một mô hình ngôn ngữ mạnh mẽ, có thể tạo ra phản hồi tự động từ ngữ cảnh hội thoại.

# 2. Tải mô hình IGTv6J + IGTv7 sẽ là mô hình thông tin 1 và cảm xúc = IGTv6-2B7 ; IGTv7-2B70; IGTv7-2B90; IGTv6J
IGTv6 và IGTv7 sẽ là một mô hình thông tin nhỏ và cảm xúc. Có 2 loại, 1 là 7B+, 2 là 70B+, loại mạnh nhất là 90B+ parameters

# 3. Wikipedia sẽ là kho thông tin 2
Wikipedia sẽ là 1 kho thông tin lớn.

# 4 Haystack sẽ là công cụ kết hợp cả 3 thứ lại để roll ra best answer
Haystack : kết hợp  IGTv6-7 wikipedia lại với nhau, chọn ra tất cả các kết quả tốt nhất trong  IGTv6-7, wikipedia, sau đó kết hợp lại 1 cách hợp lý và trả lời câu hỏi cho người dùng.

# 5 Vosk sẽ là nhận dạng giọng nói
Vosk (cho nhận dạng giọng nói) cho nhiều ngôn ngữ

# 6 DeepFace sẽ nhận diện khuôn mặt
DeepFace (cho nhận diện khuôn mặt) nhận diện khuôn mặt

## Các bước để tạo ra 1 mạng lưới Neural Network (7B -> 90B)
1. Cấu hình thiết bị
Kiểm tra xem máy tính có GPU hỗ trợ CUDA không. Nếu có, mô hình sẽ sử dụng GPU để tăng tốc độ tính toán.

device = torch.device('cuda' if torch.cuda.is_available() else 'cpu')

3. Tải các mô hình và  IGTv6J
IGTv6-7: Sinh văn bản hội thoại.
BERT: Dùng cho phân loại (Sequence Classification).
DistilBERT: Phiên bản nhẹ hơn của BERT để sinh văn bản.


3. FAISS index
Mục đích: FAISS là thư viện giúp tìm kiếm vector nhanh chóng.
IndexFlatL2: Loại chỉ mục tìm kiếm dựa trên khoảng cách Euclidean (L2)

faiss_index = faiss.IndexFlatL2(embedding_dim)

4. Bộ nhớ ngữ cảnh
context_memory = []

5. Mô hình Neural Network đánh giá phản hồi
Mục đích: Neural Network đơn giản đánh giá độ phù hợp của phản hồi dựa trên đầu vào là vector embedding.
Kiến trúc:
Fully Connected Layers (fc1 và fc2) và hàm kích hoạt ReLU.
Output là một số điểm (similarity score).


6. Hàm phân tích cảm xúc và ý định
Mục đích: Phân tích loại ý định (intention) của người dùng.
Sử dụng SentenceTransformer để mã hóa câu thành vector embedding.
Mô hình intention_model dự đoán loại ý định dựa trên vector đó.



7. Tích hợp Wikipedia API
Mục đích: Lấy tóm tắt từ Wikipedia để trả lời các câu hỏi của người dùng.

9. Sinh phản hồi từ nhiều mô hình
Tạo văn bản từ  IGTv6-7, BERT và DistilBERT.
Mã hóa các phản hồi thành vector.
Chọn phản hồi tốt nhất bằng hàm select_best_response.


9. Chọn phản hồi tốt nhất
Mục đích: Chọn phản hồi phù hợp nhất dựa trên độ tương đồng giữa query và các phản hồi.
FAISS giúp tìm kiếm vector tương tự nhanh chóng.
Neural Network evaluator_model đánh giá độ phù hợp.


10. Phản hồi cá nhân hóa
Mục đích: Thêm sắc thái cá nhân vào phản hồi dựa trên loại ý định.
Ví dụ: Nếu ý định là câu hỏi, chatbot trả lời chi tiết hơn.


11. Giao diện Tkinter
Giao diện

Đoạn mã này là một hệ thống chatbot đa năng, kết hợp nhiều công nghệ tiên tiến:

Tích hợp nhiều mô hình NLP để tạo và đánh giá phản hồi.
Sử dụng FAISS cho tìm kiếm embedding hiệu quả.
Tích hợp API Wikipedia để cung cấp thông tin thực tế.
Phân tích ý định để tăng tính cá nhân hóa.
Xây dựng giao diện người dùng thân thiện với Tkinter.

####





















































