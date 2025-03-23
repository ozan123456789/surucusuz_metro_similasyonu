# Sürücüsüz Metro Simülasyonu

Bu proje, bir metro ağı üzerinde iki istasyon arasındaki en az aktarmalı ve en hızlı rotaları bulan bir simülasyon uygulamasıdır. Proje, farklı metro hatları arasında aktarma yapabilme özelliğini de dikkate alarak, kullanıcılara optimal rota seçenekleri sunmaktadır.

## Kullanılan Teknolojiler ve Kütüphaneler

- **Python 3.x**
- **collections**: 
  - `defaultdict`: Farklı metro hatlarındaki istasyonları gruplamak için kullanılmıştır
  - `deque`: BFS (Breadth-First Search) algoritması için kuyruk veri yapısı olarak kullanılmıştır
- **heapq**: A* algoritması için öncelik kuyruğu (priority queue) implementasyonu için kullanılmıştır
- **typing**: Tip güvenliği için kullanılan type hints özelliklerini sağlar

## Algoritmaların Çalışma Mantığı

### BFS (Breadth-First Search) Algoritması

BFS algoritması, en az aktarmalı rotayı bulmak için kullanılmıştır. Algoritmanın çalışma mantığı:

1. Başlangıç istasyonundan başlayarak, tüm komşu istasyonları aynı seviyede (breadth) ziyaret eder
2. Her adımda, ziyaret edilmemiş komşu istasyonları kuyruğa ekler
3. Hedef istasyona ulaşıldığında, ilk bulunan rota en az aktarmalı rotadır

BFS'i seçmemizin nedeni:
- En az aktarma sayısını garanti eder
- Basit ve anlaşılır bir algoritmadır
- Aktarma sayısını optimize etmek için ideal bir çözümdür

### A* Algoritması

A* algoritması, en hızlı rotayı bulmak için kullanılmıştır. Algoritmanın çalışma mantığı:

1. Her istasyon için toplam maliyeti (g + h) hesaplar:
   - g: Başlangıçtan mevcut istasyona kadar olan gerçek maliyet
   - h: Mevcut istasyondan hedef istasyona olan tahmini maliyet
2. Öncelik kuyruğu kullanarak en düşük maliyetli rotaları önceliklendirir
3. Her adımda, daha düşük maliyetli rotaları keşfeder ve günceller

A*'ı seçmemizin nedeni:
- En kısa süreyi garanti eder
- Öncelik kuyruğu sayesinde en optimal rotayı bulur
- Farklı metro hatları arasındaki geçişleri de dikkate alır

## Örnek Kullanım ve Test Sonuçları

Proje üç farklı test senaryosu içermektedir:

1. **AŞTİ'den OSB'ye:**
   - En az aktarmalı rota: AŞTİ -> Kızılay -> Ulus -> Demetevler -> OSB
   - En hızlı rota: AŞTİ -> Kızılay -> Ulus -> Demetevler -> OSB (Toplam süre: 23 dakika)

2. **Batıkent'ten Keçiören'e:**
   - En az aktarmalı rota: Batıkent -> Demetevler -> Gar -> Keçiören
   - En hızlı rota: Batıkent -> Demetevler -> Gar -> Keçiören (Toplam süre: 21 dakika)

3. **Keçiören'den AŞTİ'ye:**
   - En az aktarmalı rota: Keçiören -> Gar -> Sıhhiye -> Kızılay -> AŞTİ
   - En hızlı rota: Keçiören -> Gar -> Sıhhiye -> Kızılay -> AŞTİ (Toplam süre: 17 dakika)

## Projeyi Geliştirme Fikirleri

1. **Görsel Arayüz Eklenmesi:**
   - Metro haritasının interaktif olarak görüntülenmesi
   - Rotaların harita üzerinde animasyonlu gösterimi
   - Kullanıcı dostu bir arayüz ile rota planlaması

2. **Web API Geliştirmesi:**
   - RESTful API tasarımı ve implementasyonu
   - Swagger/OpenAPI dokümantasyonu
   - Endpoint'ler:
     - `/api/rota/en-az-aktarma`: En az aktarmalı rota hesaplama
     - `/api/rota/en-hizli`: En hızlı rota hesaplama
     - `/api/istasyonlar`: Tüm istasyonların listesi
     - `/api/hatlar`: Metro hatlarının listesi
     - `/api/istasyon/{id}`: Belirli bir istasyonun detayları
   - API Güvenliği:
     - JWT tabanlı kimlik doğrulama
     - Rate limiting
     - API key yönetimi
   - Performans İyileştirmeleri:
     - Redis önbelleği
     - API response compression
     - Asenkron işlem desteği

3. **Gerçek Zamanlı Özellikler:**
   - Metro trenlerinin gerçek zamanlı konumlarının takibi
   - Yoğunluk bilgisi ve alternatif rota önerileri
   - Bekleme sürelerinin hesaplanması

4. **Veri Yönetimi İyileştirmeleri:**
   - JSON veya XML formatında metro ağı verilerinin saklanması
   - Farklı şehirler için metro ağı verilerinin eklenmesi
   - Veritabanı entegrasyonu

5. **Algoritma İyileştirmeleri:**
   - Paralel rota hesaplama desteği
   - Daha karmaşık maliyet fonksiyonları (enerji tüketimi, çevresel etki vb.)
   - Çoklu hedef noktası desteği

6. **Kullanıcı Deneyimi İyileştirmeleri:**
   - Mobil uygulama desteği
   - Offline çalışma modu
   - Rota geçmişi ve favori rotalar
   - Farklı dil desteği 