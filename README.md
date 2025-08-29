# README

## Tổng quan

Workspace này gồm hai notebook chính phục vụ cho bài toán phát hiện Hallucination trong phản hồi của mô hình ngôn ngữ:

- [`HalluDetect.ipynb`](Code/HalluDetect.ipynb): Pipeline xử lý dữ liệu, tạo embedding và huấn luyện mô hình phân loại truyền thống (MLP/Attention).
- [`pre-trained.ipynb`](Code/pre-trained.ipynb): Fine-tune mô hình Transformer (PhoBERT/XLM-R) cho bài toán phân loại.

---

## 1. [`HalluDetect.ipynb`](Code/HalluDetect.ipynb)

### Các bước xử lý:

1. **Tiền xử lý dữ liệu**  
   - Đọc dữ liệu từ file CSV.
   - Làm sạch văn bản (`clean_text`): loại bỏ ký tự đặc biệt, link, chuẩn hóa chữ thường.
   - Tách tập train/val/test và lưu ra file.

2. **Sinh embedding**  
   - Sử dụng mô hình [`SentenceTransformer`](https://huggingface.co/sentence-transformers/paraphrase-multilingual-MiniLM-L12-v2) để tạo embedding cho từng mẫu (kết hợp context, prompt, response).
   - Lưu embedding và label ra file `.npy`.

3. **Huấn luyện mô hình phân loại**  
   - Đọc embedding và label.
   - Encode label về số.
   - Huấn luyện MLP hoặc Attention Classifier bằng PyTorch.
   - Đánh giá trên tập test, in classification report.

### Model sử dụng:
- SentenceTransformer để sinh embedding.
- MLP hoặc Attention Classifier (PyTorch).

---

## 2. [`pre-trained.ipynb`](Code/pre-trained.ipynb)

### Các bước xử lý:

1. **Tiền xử lý dữ liệu**  
   - Đọc dữ liệu từ các file CSV (train/val/test).
   - Chuyển dữ liệu sang định dạng HuggingFace Dataset.

2. **Tokenization**  
   - Sử dụng tokenizer của PhoBERT hoặc XLM-R để mã hóa dữ liệu đầu vào.

3. **Fine-tune mô hình Transformer**  
   - Sử dụng [`AutoModelForSequenceClassification`](https://huggingface.co/docs/transformers/main/en/model_doc/auto#transformers.AutoModelForSequenceClassification) để huấn luyện trên tập dữ liệu đã mã hóa.
   - Đánh giá mô hình trên tập test, in các chỉ số: accuracy, precision, recall, f1.

### Model sử dụng:
- PhoBERT hoặc XLM-R (transformers).
- Trainer của HuggingFace.

---

## Kết quả

- Cả hai pipeline đều cho phép đánh giá mô hình trên tập test với các chỉ số phân loại chuẩn.
- Có thể so sánh hiệu quả giữa mô hình embedding + MLP/Attention và mô hình Transformer fine-tune.

---

## Hướng dẫn chạy

1. Cài đặt các package cần thiết (có lệnh pip ở đầu mỗi notebook).
2. Chạy lần lượt các cell trong notebook để thực hiện pipeline.

---

## Liên hệ

Nếu có thắc mắc về workspace hoặc các bước xử lý, vui lòng liên hệ qua email hoặc github.
