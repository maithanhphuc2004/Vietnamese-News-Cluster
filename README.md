# 📰 Vietnamese-News-Cluster

## 🔖 Model Badges  
*(Các mô hình sử dụng trong nghiên cứu)*

![TFIDF](https://img.shields.io/badge/Embedding-TF--IDF-blue?style=flat-square)
![PhoBERT-base](https://img.shields.io/badge/Embedding-PhoBERT--base-green?style=flat-square)
![PhoBERT-large](https://img.shields.io/badge/Embedding-PhoBERT--large-purple?style=flat-square)
![UMAP](https://img.shields.io/badge/Dimensionality%20Reduction-UMAP-orange?style=flat-square)

![KMeans](https://img.shields.io/badge/Clustering-KMeans-red?style=flat-square)
![Hierarchical](https://img.shields.io/badge/Clustering-Hierarchical--Ward-brown?style=flat-square)
![DBSCAN](https://img.shields.io/badge/Clustering-DBSCAN-yellow?style=flat-square)
![HDBSCAN](https://img.shields.io/badge/Clustering-HDBSCAN-lightgrey?style=flat-square)
![Spectral](https://img.shields.io/badge/Clustering-Spectral-blueviolet?style=flat-square)

![Python](https://img.shields.io/badge/Python-3.10+-blue?style=flat-square&logo=python)
![Status](https://img.shields.io/badge/Status-Active-brightgreen?style=flat-square)
![Dataset](https://img.shields.io/badge/Dataset-7.278%20articles-orange?style=flat-square)

---

# 📌 Overview  
*(Tổng quan)*  

This project focuses on clustering electronic news articles using modern NLP techniques and multiple clustering algorithms.  
*(Dự án tập trung phân cụm nội dung bài báo điện tử bằng các kỹ thuật NLP hiện đại và nhiều thuật toán phân cụm khác nhau.)*

The workflow includes:  
- Text preprocessing  
- Embedding with TF-IDF and PhoBERT variants  
- Dimensionality reduction via UMAP  
- Clustering using 5 algorithms  
- Evaluation with Silhouette, Davies–Bouldin, and Calinski–Harabasz metrics  

---

# 📂 Dataset  
*(Tập dữ liệu)*  

- Collected from **electronic news articles**  
- Total samples: **7,000+ documents**  
- Preprocessing steps include tokenization, normalization, stopword removal, embedding generation  

---

# 🧠 Embedding Methods  
*(Các phương pháp biểu diễn văn bản)*  

### **1. TF-IDF**  
*(Chuẩn hóa tần suất–nghịch đảo tần suất)*  
- Sparse representation  
- Effective for lexical similarity  
- Used as baseline

### **2. PhoBERT-base**  
*(Mô hình ngôn ngữ tiếng Việt – phiên bản base)*  
- Transformer-based  
- Pretrained on large Vietnamese corpus  
- Captures contextual meaning

### **3. PhoBERT-large**  
*(Phiên bản large – mạnh hơn và chính xác hơn)*  
- Better semantic representation  
- Improved clustering separability

### **4. UMAP (Uniform Manifold Approximation and Projection)**  
*(Giảm chiều dữ liệu)*  
- Reduces embedding from 768D → 2/3D  
- Preserves neighborhood structure  
- Makes clustering easier and more accurate

---

# 🔍 Clustering Algorithms  
*(Các thuật toán phân cụm)*

## **1. K-Means**  
*(Phân cụm K-Means)*  
- Simple and widely used  
- Works best for spherical clusters  
- K chosen using Elbow + Silhouette  
- Applied to TF-IDF and PhoBERT embeddings

## **2. Hierarchical Clustering (Ward linkage)**  
*(Phân cụm phân cấp – Ward)*  
- Builds dendrogram to visualize cluster hierarchy  
- Does not require choosing K initially  
- Ward linkage minimizes variance  
- Used after UMAP reduction

## **3. DBSCAN**  
*(Phân cụm dựa trên mật độ)*  
- Automatically detects noise points  
- No need to specify K  
- Good for arbitrary-shaped clusters  
- Applied on UMAP-embedded space

## **4. HDBSCAN**  
*(Phiên bản nâng cấp của DBSCAN)*  
- Density hierarchy  
- Automatically determines cluster count  
- More stable than DBSCAN  
- Handles variable-density regions

## **5. Spectral Clustering**  
*(Phân cụm phổ)*  
- Uses graph Laplacian  
- Extracts eigenvectors → then runs K-Means  
- Good for complex, non-linear cluster structures  

---

# 📊 Algorithm Comparison  
*(Bảng so sánh thuật toán)*

### **📌 Comparison based on Silhouette, Davies–Bouldin, Calinski–Harabasz across embeddings**
*(So sánh dựa trên ba chỉ số đánh giá trên các embedding khác nhau)*

| Algorithm | Embedding | K | Silhouette ↑ | Davies–Bouldin ↓ | Calinski–Harabasz ↑ |
|----------|-----------|---|--------------|-------------------|----------------------|
| Spectral | TF-IDF (UMAP) | 15 | **0.3120** | 0.8360 | 2259.86 |
| Spectral | PhoBERT-base (UMAP) | 19 | 0.2581 | 0.9197 | 1861.72 |
| Spectral | PhoBERT-large (UMAP) | 8 | **0.3466** | **0.7688** | **2416.71** |
| HDBSCAN | TF-IDF / PhoBERT | — | Auto | Auto | — |
| DBSCAN | TF-IDF / PhoBERT | — | Medium | Medium | — |
| K-Means | All embeddings | Varied | Moderate | Medium | Medium |
| Hierarchical (Ward) | All embeddings | Varied | Moderate | Medium | Medium |

(*↑ Higher is better, ↓ Lower is better*)  
*(↑ Cao hơn là tốt hơn, ↓ Thấp hơn là tốt hơn)*

---

# 📈 Key Findings  
*(Kết luận chính)*  

- **PhoBERT-large + Spectral Clustering performs best**, with the highest Silhouette and CH score.  
*(PhoBERT-large + Spectral cho kết quả tốt nhất.)*

- **DBSCAN and HDBSCAN effectively detect natural clusters**, especially with noise handling.  
*(DBSCAN và HDBSCAN phát hiện cụm tự nhiên tốt và xử lý nhiễu.)*

- **TF-IDF works surprisingly well**, especially after UMAP reduction.  
*(TF-IDF vẫn hoạt động tốt sau khi giảm chiều bằng UMAP.)*

- **Hierarchical Clustering + Ward linkage** provides clean dendrogram visualization.  
*(Phân cấp Ward tạo dendrogram rõ ràng.)*

---

# 🛠 Installation  
*(Cài đặt)*  

```bash
pip install -r requirements.txt
```
python src/preprocess.py
python src/embedding.py
python src/clustering.py
python src/evaluate.py

## 👨‍💻 Authors (Tác giả)

Mai Thanh Phúc
Hoàng Thị Yến Nhi
Trần Trọng Thành
Supervisor: Lê Nhật Tùng (GVHD)

##📚 Citation (Trích dẫn)

Mai Thanh Phúc, Hoàng Thị Yến Nhi, Trần Trọng Thành, Lê Nhật Tùng. 
Clustering Electronic News Articles using NLP and Machine Learning.
HUTECH University.
