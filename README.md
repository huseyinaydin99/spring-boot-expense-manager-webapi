### Harcama yöneticisi WebAPI uygulaması.

### Açıklama
```
Spring Boot + Security + Data JPA + JWT + MySQL + Postman teknolojileri kullanılmıştır.
Çok katmanlı mimariye sahiptir.
SOLID ve DRY prensipleri kullanılmıştır.
ORM + IoC + DI + Strategy Desing Pattern + Repository Desing Pattern teknikleri kullanılmıştır.
Harcama yöneticisi WebAPI projesidir.
Kullanıcı register olduktan sonra login olmak için postman üzerinden email ve şifresini girer.
Sonrasında ise bir JSON Web Token elde eder. Bu token onun erişim anahtarıdır(jeton).
Bu jeton'nun içerisinde kullanıcının kimlik bilgileri, yetkileri ve geçerlilik süresi vardır.
Belirlenen geçerlilik süresinde bu jeton ile sisteme erişim sağlar.
Yapmış olduğu harcamaları CRUD operasyonları ile yönetir.
Kendi profilini güncelleyebilir ve deactive edebilir.
Deactive işlemi aslında kullanıcıyı komple veritabanından silmektedir. 
```

### Register ve Login API 

```
Kayıt olmak için Postman ile aşağıdaki endpoint'e POST metodu ile Body / Raw / JSON kısmına
localhost:8080/api/v1/register
{
    "name": "Huseyin",
    "email": "huseyinaydin99@gmail.com",
    "password": "123Aa*"
}
girilir ve send butonu ile API'e POST edilir. Artık kullanıcı kaydı oluşmuştur.

Login olmak için Postman ile aşağıdaki endpoint'e POST metodu ile Body / Raw / JSON kısmına
localhost:8080/api/v1/login
{
    "email": "hasanaydin99@gmail.com",
    "password": "123Aa*"
}
girilir ve send butonu ile API'e POST edilir. Artık kullanıcı login olmuştur ve JSON Web Token gelir.

İlgili JSON Web Token kopyalanır. Postman'in ilgili Authorization kısmından OAuth2 seçilir ve Token kısmına
kopyalanılan JSON Web Token yapıştırılır.
```

### Expense API

```
Yeni bir harcama girerken aşağıdaki adrese POST metodu ile Body / RAW / JSON kısmına
localhost:8080/api/v1/expense
{
    "name": "Elektrik Faturası",
    "description": "Elektrik faturası çok gelmiş",
    "amount": 250,
    "category": "Ev",
    "date": "2019-04-28T14:45:15"
}
ilgili JSON verisi girilir. Bu veri bir elektrik faturası kaydının JSON halidir. Send butonu ile API'ye gönderilerekten kaydettirilir. Geriye 201 Created döner.

İlgili endpoint'e GET isteği gönderilerekten sistemde ne kadar kayıtlı harcama varsa alınır.
localhost:8080/api/v1/expenses GET

İlgili endpoint'in sonuna ilgili harcamanın ID numarası eklenilerekten GET isteği gönderilirse o ID'e sahip kayıt döner. Bir nevi ID'ye göre arama işlemidir.
localhost:8080/api/v1/expense/1

Harcama kaydı güncelleneceği zaman aşağıdaki adrese PUT metodu ile Body / RAW / JSON kısmına sonunada ID eklenerekten
localhost:8080/api/v1/expense/1
{
    "name": "Elektrik Faturası",
    "description": "Elektrik faturası çok gelmiş",
    "amount": 300,
    "category": "Ev",
    "date": "2019-04-28T14:45:15"
}
ilgili JSON verisi girilir. Bu veri bir elektrik faturası kaydının JSON halidir. Send butonu ile API'ye gönderilerekten güncelleme yapılır. Geriye 201 Created döner.

localhost:8080/api/v1/expenses/?category=Ev GET -> Ev kategorisine ait harcama kayıtlarını döner.
localhost:8080/api/v1/expenses/?date=2019-04-28T14:45:15 GET -> tarihe göre harcama kayıtlarını döner.
localhost:8080/api/v1/expenses/?name=Elektrik Faturası -> Harcama kaydının adına göre harcama kayıtlarını döner.
localhost:8080/api/v1/expense/?expenseId=1 DELETE -> 1 ID'li harcama kaydını siler.
```

### USER API
```
localhost:8080/api/v1/profile GET --> login olan kullanıcının kaydını geriye döndürür.
localhost:8080/api/v1/profile PUT --> adresi girilir.
{
    "name": "hasan",
    "email": "hasanaydin99@gmail.com",
    "password": "123Aa**"
}
ilgili kullanıcının JSON verisi girilerekten güncellemesi yapılır.

localhost:8080/api/v1/deactivate DELETE adresi girilir ve send butonuna basınca ilgili kullanıcı kaydı silinir.
```

### Görseller
![270783024-6db29f49-00a5-41b5-83f3-a56e831da59c](https://github.com/user-attachments/assets/4369f912-d140-48a6-bf4f-3c7ce7c7e0ef)
![270782968-1b4d7c82-aa29-409e-8bce-f66467f4e6a6](https://github.com/user-attachments/assets/2bd1ff91-dfbe-4b4e-b7a3-590845d58e07)
![270782637-7ea26abe-8b9e-45f7-9f3b-0279ac0b471f](https://github.com/user-attachments/assets/8809c7e8-a7da-468a-ade2-772cde6c7916)
![270782489-e8b56ff7-a370-40d0-8b06-80b07f3dc7c3](https://github.com/user-attachments/assets/0c4f3630-f228-4f14-9074-cb780e77b4c4)
