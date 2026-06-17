Chatbot Bantuan Hukum Masyarakat Awam Berbasis RAG, LangChain, dan LangGraph
Deskripsi Proyek

Proyek ini merupakan implementasi chatbot bantuan hukum yang dikembangkan untuk membantu masyarakat memperoleh informasi hukum secara lebih mudah dan cepat. Sistem memanfaatkan pendekatan Retrieval-Augmented Generation (RAG) sehingga jawaban yang diberikan tidak hanya berasal dari kemampuan model bahasa, tetapi juga didukung oleh dokumen hukum yang telah diproses sebelumnya.

Pada proyek ini digunakan dua sumber dokumen hukum, yaitu Undang-Undang Ketenagakerjaan dan Undang-Undang Perlindungan Konsumen. Pengguna dapat mengajukan pertanyaan menggunakan bahasa alami, kemudian sistem akan mencari bagian dokumen yang relevan sebelum menghasilkan jawaban.

Proyek dikembangkan menggunakan LangChain untuk membangun pipeline RAG, LangGraph untuk mengatur alur kerja chatbot, ChromaDB sebagai vector database, serta LangSmith untuk melakukan monitoring dan evaluasi proses yang berjalan.

Identitas Mahasiswa
Keterangan	Isi
Nama	Ferdinand Tobing
NPM	233510397
Mata Kuliah	Natural Language Processing
Platform	Google Colab
Latar Belakang

Informasi hukum sering kali sulit dipahami oleh masyarakat karena menggunakan istilah dan bahasa yang formal. Di sisi lain, tidak semua orang memiliki akses untuk berkonsultasi langsung dengan praktisi hukum ketika menghadapi suatu permasalahan.

Melalui proyek ini dibangun sebuah chatbot yang dapat membantu pengguna memperoleh informasi awal mengenai hak dan kewajiban mereka berdasarkan dokumen hukum yang tersedia. Sistem tidak ditujukan untuk menggantikan konsultasi hukum profesional, tetapi sebagai media informasi yang lebih mudah diakses.

Tujuan

Tujuan pengembangan proyek ini adalah:

Menerapkan konsep Retrieval-Augmented Generation (RAG).
Mengintegrasikan LangChain dengan LangGraph dalam sebuah sistem chatbot.
Memanfaatkan vector database untuk pencarian dokumen berbasis semantic search.
Menghasilkan jawaban yang mengacu pada sumber dokumen hukum yang relevan.
Melakukan evaluasi dan monitoring proses menggunakan LangSmith.
Dokumen Hukum yang Digunakan
Dokumen	Topik Utama
UU No. 13 Tahun 2003 tentang Ketenagakerjaan	PHK, pesangon, kontrak kerja, hak pekerja
UU No. 8 Tahun 1999 tentang Perlindungan Konsumen	Garansi, refund, hak konsumen, tanggung jawab pelaku usaha
Arsitektur Sistem
Pengguna
    │
    ▼
Pertanyaan Hukum
    │
    ▼
Clarify Context
    │
    ▼
Retrieve Documents
    │
    ▼
Analyze and Answer
    │
    ▼
Recommend Action
    │
    ▼
Jawaban Akhir
Teknologi yang Digunakan
Teknologi	Fungsi
Python	Bahasa pemrograman utama
LangChain	Membangun pipeline RAG
LangGraph	Mengatur workflow chatbot
ChromaDB	Penyimpanan embedding dokumen
OpenAI	Model bahasa untuk menghasilkan jawaban
LangSmith	Monitoring dan evaluasi pipeline
Pandas	Pengolahan data
Matplotlib	Visualisasi hasil
PyPDF	Membaca dokumen PDF
Alur Kerja Sistem
1. Persiapan Dokumen

Dokumen hukum dalam format PDF diunggah dan diverifikasi sebelum diproses lebih lanjut.

Screenshot

images/upload-dokumen.png

2. Pembentukan Vector Store

Dokumen dipecah menjadi beberapa bagian (chunk), kemudian setiap chunk diubah menjadi embedding dan disimpan ke dalam ChromaDB.

Hasil pemrosesan:

Domain	Jumlah Chunk
Ketenagakerjaan	229
Konsumen	81
Total	310

Screenshot

images/vector-store.png

3. Semantic Search

Ketika pengguna mengajukan pertanyaan, sistem melakukan pencarian dokumen berdasarkan kemiripan makna (semantic similarity), bukan sekadar pencocokan kata.

Screenshot

images/semantic-search.png

4. Workflow LangGraph

Alur kerja chatbot dibangun menggunakan empat node utama:

Clarify Context
Retrieve Documents
Analyze and Answer
Recommend Action

Screenshot

images/langgraph-workflow.png

5. Proses Retrieval

Node retrieval bertugas mengambil dokumen yang paling relevan dari ChromaDB berdasarkan pertanyaan pengguna.

Screenshot

images/retrieve-documents.png

6. Analisis dan Pembentukan Jawaban

Informasi yang ditemukan kemudian dikirim ke model bahasa untuk menghasilkan jawaban yang lebih mudah dipahami.

Screenshot

images/analyze-answer.png

7. Rekomendasi Tindakan

Selain memberikan penjelasan hukum, sistem juga memberikan rekomendasi langkah yang dapat dilakukan pengguna.

Screenshot

images/recommend-action.png

Hasil Pengujian

Pengujian dilakukan menggunakan beberapa pertanyaan dari domain ketenagakerjaan dan perlindungan konsumen.

Contoh pertanyaan:

Berapa pesangon yang saya dapatkan jika di-PHK setelah bekerja 6 tahun?
Apakah kontrak kerja lisan memiliki kekuatan hukum?
Toko online tidak mau refund padahal produk yang dikirim rusak.
Saya membeli barang tetapi tidak sesuai deskripsi.

Screenshot

images/demo-chatbot.png

Visualisasi Data
Distribusi Chunk Dokumen

Visualisasi menunjukkan jumlah chunk yang dihasilkan dari masing-masing dokumen hukum.

Screenshot

images/distribusi-chunk.png

Visualisasi Embedding

Embedding dokumen divisualisasikan menggunakan Principal Component Analysis (PCA) dua dimensi untuk melihat persebaran data.

Screenshot

images/pca-embedding.png

Evaluasi Sistem

Evaluasi dilakukan untuk menguji kemampuan sistem dalam mengidentifikasi domain pertanyaan.

Hasil evaluasi menunjukkan:

Metrik	Hasil
Jumlah Query Uji	6
Prediksi Benar	6
Akurasi Domain	100%

Screenshot

images/evaluasi.png

Monitoring dengan LangSmith

LangSmith digunakan untuk memantau proses eksekusi setiap node, mengukur latency, serta membantu proses debugging selama pengembangan sistem.

Screenshot

images/langsmith.png

Cara Menjalankan Program
Clone Repository
git clone https://github.com/username/chatbot-hukum.git
cd chatbot-hukum
Install Dependensi
pip install langchain
pip install langgraph
pip install chromadb
pip install openai
pip install langsmith
pip install pandas
pip install matplotlib
Konfigurasi API Key
OPENAI_API_KEY="YOUR_API_KEY"
LANGSMITH_API_KEY="YOUR_API_KEY"
Menjalankan Notebook

Buka file:

UAS_PRATIKUM_NLP_Chatbot_Hukum.ipynb

Kemudian jalankan seluruh cell secara berurutan dari awal hingga akhir.

Kesimpulan

Berdasarkan hasil implementasi dan pengujian, sistem chatbot bantuan hukum berhasil dibangun menggunakan pendekatan Retrieval-Augmented Generation (RAG). Integrasi LangChain, LangGraph, ChromaDB, dan OpenAI memungkinkan sistem memberikan jawaban yang relevan dengan dokumen hukum yang tersedia. Selain itu, penggunaan LangSmith membantu proses evaluasi dan pemantauan kinerja sistem selama pengembangan.

Referensi
LangChain Documentation
LangGraph Documentation
ChromaDB Documentation
OpenAI Documentation
Undang-Undang Nomor 13 Tahun 2003 tentang Ketenagakerjaan
Undang-Undang Nomor 8 Tahun 1999 tentang Perlindungan Konsumen
