# OpenAPI Tasarımı Ödevi Teslim Raporu

## 👤 Öğrenci Bilgileri
- **Ad Soyad**: Fatih Eren Durmuş
- **Öğrenci Numarası**: 171422006
- **Teslim Tarihi**: 24.05.2025

---

## 📂 OpenAPI YAML Dosyası

- **openapi.yaml** dosyasını projenizin GitHub reposuna yükledim.
- Swagger Editor ile doğrulama ve testlerini tamamladım.

### 🔗 GitHub Repo Linki
[https://github.com/FatihErenD/OpenAPI-Design](https://github.com/FatihErenD/OpenAPI-Design)

---

## 📝 API Açıklaması

- **Varlıklar (Entities):**  
  - **Book**: `id`, `title`, `author`, `isbn`, `publisher`, `pageCount`, `stock`  
  - **Student**: `id`, `name`, `studentNumber`, `email`, `isActive`  
  - **Loan**: `id`, `studentId`, `bookId`, `loanDate`, `returnDate`, `status` (enum: ongoing, returned, late)  

- **CRUD İşlemleri ve Endpoint’ler:**  
  - **Books**  
    - `GET /books` (sayfalama: `page`, `size`)  
    - `GET /books/{id}`  
    - `POST /books`  
    - `PUT /books/{id}`  
    - `DELETE /books/{id}`  
  - **Students**  
    - `GET /students`  
    - `GET /students/{id}`  
    - `POST /students`  
    - `PUT /students/{id}`  
    - `DELETE /students/{id}`  
  - **Loans**  
    - `GET /loans`  
    - `GET /loans/{id}`  
    - `POST /loans`  
    - `PATCH /loans/{id}/return`  

- **components/schemas, parameters, responses Kullanımı:**  
  - `components/schemas` içerisinde tüm veri modellerini (`Book`, `BookCreate`, `Student`, `StudentCreate`, `Loan`, `LoanCreate`, `BookList`, `ErrorResponse`) tanımladım.  
  - `components/parameters` altında `page`, `size`, `id` parametrelerini belirttim.  
  - `components/responses` ile `BadRequest (400)`, `NotFound (404)`, `InternalError (500)` şablonlarını oluşturdum.  

- **Sayfalama ve Hata Durumları:**  
  - `GET /books` endpoint’inde `page` ve `size` query parametreleriyle sayfalama yaptım.  
  - Hatalı isteklerde (eksik/yanlış parametre) `400`, bulunamayan kaynakta `404`, sunucu hatasında `500` dönülüyor.  

---

## 🧪 Test Notları (Opsiyonel)

- **`GET /books`**  
  - **İstek:** `GET https://marmarauniversity.edu/v1/books?page=1&size=5`  
  - **Dönen:**  
    ```json
    {
      "totalItems": 125,
      "page": 1,
      "size": 5,
      "items": [ /* Book dizisi */ ]
    }
    ```

- **`POST /students`**  
  - **İstek Gövdesi:**
    ```json
    {
      "name": "Jane Doe",
      "studentNumber": "202312345",
      "email": "jane.doe@example.com",
      "isActive": true
    }
    ```
  - **Başarılı Cevap (201):** Yeni oluşturulan `Student` kaydı JSON olarak döner.

- **Hatalı İstek Örneği (400):**
  - Eksik `email` alanı ile:
    ```json
    {
      "code": 400,
      "message": "Invalid request parameters."
    }
    ```
