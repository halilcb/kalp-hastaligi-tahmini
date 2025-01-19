# Kalp Hastalığı Tahmin Projesi

Bu proje, **UCI Heart Disease Data** veri seti kullanılarak bireylerde kalp hastalığı derecesini tahmin etmek için çeşitli makine öğrenimi tekniklerini uygulamaktadır.
Proje, veri ön işleme, keşfedici veri analizi (EDA), eksik değer yönetimi, model eğitimi, topluluk (ensemble) öğrenme yöntemleri ve değerlendirme aşamalarını kapsamaktadır.



## Veri Seti

Bu projede kullanılan veri seti, **Kaggle** platformunda paylaşılan **Heart Disease Data** veri setidir.
Veri seti, bireylerin çeşitli klinik ve demografik özelliklerini içerir ve bu özelliklere dayanarak kalp hastalığı derecesini belirten bir hedef değişken barındırır.
Veri seti 76 özelliğe sahiptir, ancak çalışmalar genellikle bu özelliklerden 14'ü üzerinde yapılmaktadır.  

### Özellikler:
- **id**: Her hasta için benzersiz kimlik
- **age**: Hastanın yaşı
- **origin**: Çalışmanın yapıldığı yer
- **sex**: Hastanın cinsiyeti (1: Erkek, 0: Kadın)
- **cp**: Göğüs ağrısı tipi (4 kategorik değer)
- **trestbps**: İstirahat halindeki kan basıncı (mm Hg)
- **chol**: Serum kolesterolü (mg/dl)
- **fbs**: Açlık kan şekeri > 120 mg/dl (1: Doğru, 0: Yanlış)
- **restecg**: İstirahat EKG sonuçları (0, 1, 2)
- **thalach**: Maksimum kalp hızı
- **exang**: Egzersiz ile oluşan anjina (1: Evet, 0: Hayır)
- **oldpeak**: ST depresyonu (istirahat ve egzersiz arasındaki fark)
- **slope**: Egzersiz sırasında ST segmentinin eğimi
- **ca**: Floroskopi ile görülen majör damar sayısı (0-3)
- **thal**: Talasemi (3: Normal, 6: Sabit kusur, 7: Tersine çevrilebilir kusur)
- **num**: Tahmin edilen özellik:
  - `0`: Kalp hastalığı yok
  - `1, 2, 3, 4`: Kalp hastalığı dereceleri

**Veri seti bağlantısı**: [Heart Disease Data on Kaggle](https://www.kaggle.com/datasets/redwankarimsony/heart-disease-data)



## Proje Aşamaları

### 1. Veri Keşfi ve Görselleştirme
- Veri seti yüklenerek sütunların yapısı ve istatistiksel bilgileri incelenmiştir (`info()`, `describe()`).
- Sayısal özellikler arasındaki ilişkiler, bir `pairplot` kullanılarak analiz edilmiştir.
- Hedef değişkenin sınıf dağılımı `countplot` ile görselleştirilmiştir.

### 2. Eksik Değer Yönetimi
- Eksik değerler kontrol edilmiştir (`isnull().sum()`).
- Bazı sütunlar çok fazla eksik değer içerdiği için kaldırılmıştır (örneğin, `ca` sütunu).
- Eksik değerler sütunlara göre uygun şekilde doldurulmuştur:
  - Sayısal sütunlar: **Ortanca (median)** değeri ile doldurulmuştur.
  - Kategorik sütunlar: **Mod (en sık tekrar eden değer)** ile doldurulmuştur.

### 3. Veri Ayrımı ve Standardizasyon
- Veri, hedef değişken (`num`) ve özellikler (`X`) olarak ayrılmıştır.
- Eğitim ve test kümelerine `train_test_split` ile bölünmüştür (%75 eğitim, %25 test).
- Sayısal özellikler **StandardScaler** kullanılarak standardize edilmiştir.
- Kategorik özellikler **OneHotEncoder** kullanılarak kodlanmıştır.

### 4. Model Eğitimi ve Değerlendirme
- İki model kullanılmıştır:
  - **Random Forest Classifier**
  - **K-Nearest Neighbors (KNN)**
- Modeller, bir **VotingClassifier** (Soft Voting) ile birleştirilmiştir.
- Eğitim verileri ile model eğitilmiş, test verileri ile modelin doğruluğu (`accuracy`), karmaşıklık matrisi (`confusion_matrix`) ve sınıflandırma raporu (`classification_report`) hesaplanmıştır.

### 5. Performans Görselleştirme
- Karmaşıklık matrisi, bir ısı haritası (heatmap) ile görselleştirilmiştir.
