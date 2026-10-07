# Hybrid Information Retrieval & Semantic Search Pipeline (RAG System)

Bu proje, akademik metinler (ArXiv veri seti) üzerinde yüksek doğruluklu arama ve getirme (retrieval) süreçleri yürütmek amacıyla tasarlanmış uçtan uca bir **Hibrit Bilgi Getirimi (Hybrid Information Retrieval)** ve **Semantik Arama** boru hattıdır. Modern RAG (Retrieval-Augmented Generation) mimarilerinin veri getirme katmanını optimize etmeye odaklanır.

---

## 📌 Temel Özellikler

- **Hibrit Arama (Hybrid Retrieval):** 
  - Kelime tabanlı (Lexical) arama için **BM25** algoritması.
  - Anlamsal (Dense/Semantic) temsil için `sentence-transformers/all-mpnet-base-v2` Bi-Encoder modeli.
- **Yeniden Sıralama (Re-ranking):** 
  - Getirilen aday belgelerin alaka düzeyini artırmak için `cross-encoder/ms-marco-MiniLM-L-6-v2` modeli.
- **Vektör Depolama & İndeksleme:** 
  - Hızlı ve ölçeklenebilir gömme (embedding) saklama ve benzerlik araması için **ChromaDB**.
- **Modüler Yapı:** RAG ve LLM boru hatlarına doğrudan entegre edilebilir Python modülleri.

---

## 🏗️ Mimari ve Çalışma Mantığı

1. **Veri Ön İşleme:** Metinler temizlenir, parçalara (chunks) ayrılır ve metadata bilgileri yapılandırılır.
2. **Çift Yönlü Getirme (First-Stage Retrieval):**
   - Kullanıcı sorgusu hem BM25 (anahtar kelime uyumu) hem de ChromaDB (vektör benzerliği) üzerinden taranır.
   - Sonuçlar birleştirilerek en alakalı ilk 3 aday doküman belirlenir.
3. **Yeniden Sıralama (Second-Stage Re-ranking):**
   - Aday dokümanlar Cross-Encoder üzerinden geçirilerek sorgu-metin bağlamsal ilişkisine göre nihai puanlama yapılır.
4. **Çıktı / LLM Bağlamı:** En yüksek puanlı bağlamlar kullanıcıya veya LLM üretici katmanına sunulur.

---

## 🛠️ Kullanılan Teknolojiler

- **Programlama Dili:** Python 3.10+
- **Vektör Veri Tabanı:** ChromaDB
- **Makine Öğrenmesi & NLP:** PyTorch, Sentence-Transformers, Hugging Face Hub, Scikit-learn
- **Leksikal Arama:** `rank_bm25`
- **Veri Manipülasyonu:** Pandas, NumPy

---

## 🚀 Kurulum ve Çalıştırma

### 1. Projeyi Klonlayın
```bash
git clone [https://github.com/GamzeDuru/repo-adin.git](https://github.com/GamzeDuru/repo-adin.git)
cd repo-adin
