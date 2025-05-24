# University Library API

Üniversitenin çevrim içi kütüphane sistemi için hazırlanmış OpenAPI 3.1 standardına uygun **RESTful API** tanımı.

---

## İçindekiler

1. [Özellikler](#özellikler)
2. [Dizin Yapısı](#dizin-yapısı)
3. [Başlarken](#başlarken)

   * [Kurulum](#kurulum)
4. [Kullanım](#kullanım)

   * [Sunucular](#sunucular)
   * [Endpoint’ler](#endpointler)
   * [Örnek İstek/Cevap](#örnek-istekcevap)
5. [Yetkilendirme](#yetkilendirme)

---

## Özellikler

* Tam kapsamlı **CRUD** operasyonları:

  * `/books` → kitap yönetimi
  * `/students` → öğrenci yönetimi
  * `/loans` → ödünç ve iade işlemleri
* **Sayfalama** desteği (`page`, `size` query parametreleri\`)
* Hata yönetimi için standart `400`, `404`, `500` cevapları
* Örnek istek/cevap blokları ile kolay entegrasyon
* **ApiKey** tabanlı basit güvenlik şeması (opsiyonel)

---

## Dizin Yapısı

```
/
├── openapi.yaml        # OpenAPI 3.1 tanımı
├── README.md           # Proje açıklaması ve kullanım talimatları
└── DELIVERY.md         # Google Classroom’a yüklenecek teslim dosyası
```

---

## Başlarken

### Kurulum

1. Depoyu klonlayın:

   ```bash
   git clone https://github.com/FatihErenD/OpenAPI-Design.git
   cd OpenAPI-Design
   ```
2. `openapi.yaml` dosyasını favori OpenAPI editörünüze (Swagger Editor, Redocly vb.) yükleyin.

---

## Kullanım

### Sunucular

| Ortam      | URL                                     |
| ---------- | --------------------------------------- |
| Production | `https://api.marmarauniversity.edu/v1`  |


### Endpoint’ler

* **Kitaplar (`/books`)**

  * `GET /books` – Kitap listesini sayfalı getir
  * `GET /books/{id}` – Tek kitap detayı
  * `POST /books` – Yeni kitap ekle
  * `PUT /books/{id}` – Kitap güncelle
  * `DELETE /books/{id}` – Kitap sil

* **Öğrenciler (`/students`)**

  * `GET /students` – Öğrenci listesini getir
  * `GET /students/{id}` – Tek öğrenci detayı
  * `POST /students` – Yeni öğrenci ekle
  * `PUT /students/{id}` – Öğrenci güncelle
  * `DELETE /students/{id}` – Öğrenci sil

* **Ödünç İşlemleri (`/loans`)**

  * `GET /loans` – Ödünç kayıtlarını getir
  * `GET /loans/{id}` – Tek kayıt detayı
  * `POST /loans` – Yeni ödünç kaydı oluştur
  * `PATCH /loans/{id}/return` – Kaydı iade olarak işaretle

### Örnek Istek/Cevap

```http
POST /books HTTP/1.1
Host: sandbox.university.edu
Content-Type: application/json
X-API-Key: your_api_key_here

{
  "title": "Introduction to Algorithms",
  "author": "Cormen, Leiserson, Rivest, Stein",
  "isbn": "9780262033848",
  "publisher": "MIT Press",
  "pageCount": 1312,
  "stock": 5
}
```

```json
HTTP/1.1 201 Created
Content-Type: application/json

{
  "id": "7f9f8c2e-d4c9-4c0b-8e3a-1a2b3c4d5e6f",
  "title": "Introduction to Algorithms",
  "author": "Cormen, Leiserson, Rivest, Stein",
  "isbn": "9780262033848",
  "publisher": "MIT Press",
  "pageCount": 1312,
  "stock": 5
}
```

---

## Yetkilendirme

* Tüm **production** isteklerinde `X-API-Key` header’ı zorunludur.
