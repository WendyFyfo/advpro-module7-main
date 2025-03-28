# BambangShop Publisher App
Tutorial and Example for Advanced Programming 2024 - Faculty of Computer Science, Universitas Indonesia

---

## About this Project
In this repository, we have provided you a REST (REpresentational State Transfer) API project using Rocket web framework.

This project consists of four modules:
1.  `controller`: this module contains handler functions used to receive request and send responses.
    In Model-View-Controller (MVC) pattern, this is the Controller part.
2.  `model`: this module contains structs that serve as data containers.
    In MVC pattern, this is the Model part.
3.  `service`: this module contains structs with business logic methods.
    In MVC pattern, this is also the Model part.
4.  `repository`: this module contains structs that serve as databases and methods to access the databases.
    You can use methods of the struct to get list of objects, or operating an object (create, read, update, delete).

This repository provides a basic functionality that makes BambangShop work: ability to create, read, and delete `Product`s.
This repository already contains a functioning `Product` model, repository, service, and controllers that you can try right away.

As this is an Observer Design Pattern tutorial repository, you need to implement another feature: `Notification`.
This feature will notify creation, promotion, and deletion of a product, to external subscribers that are interested of a certain product type.
The subscribers are another Rocket instances, so the notification will be sent using HTTP POST request to each subscriber's `receive notification` address.

## API Documentations

You can download the Postman Collection JSON here: https://ristek.link/AdvProgWeek7Postman

After you download the Postman Collection, you can try the endpoints inside "BambangShop Publisher" folder.
This Postman collection also contains endpoints that you need to implement later on (the `Notification` feature).

Postman is an installable client that you can use to test web endpoints using HTTP request.
You can also make automated functional testing scripts for REST API projects using this client.
You can install Postman via this website: https://www.postman.com/downloads/

## How to Run in Development Environment
1.  Set up environment variables first by creating `.env` file.
    Here is the example of `.env` file:
    ```bash
    APP_INSTANCE_ROOT_URL="http://localhost:8000"
    ```
    Here are the details of each environment variable:
    | variable              | type   | description                                                |
    |-----------------------|--------|------------------------------------------------------------|
    | APP_INSTANCE_ROOT_URL | string | URL address where this publisher instance can be accessed. |
2.  Use `cargo run` to run this app.
    (You might want to use `cargo check` if you only need to verify your work without running the app.)

## Mandatory Checklists (Publisher)
-   [x] Clone https://gitlab.com/ichlaffterlalu/bambangshop to a new repository.
-   **STAGE 1: Implement models and repositories**
    -   [x] Commit: `Create Subscriber model struct.`
    -   [x] Commit: `Create Notification model struct.`
    -   [x] Commit: `Create Subscriber database and Subscriber repository struct skeleton.`
    -   [x] Commit: `Implement add function in Subscriber repository.`
    -   [x] Commit: `Implement list_all function in Subscriber repository.`
    -   [x] Commit: `Implement delete function in Subscriber repository.`
    -   [x] Write answers of your learning module's "Reflection Publisher-1" questions in this README.
-   **STAGE 2: Implement services and controllers**
    -   [x] Commit: `Create Notification service struct skeleton.`
    -   [x] Commit: `Implement subscribe function in Notification service.`
    -   [x] Commit: `Implement subscribe function in Notification controller.`
    -   [x] Commit: `Implement unsubscribe function in Notification service.`
    -   [x] Commit: `Implement unsubscribe function in Notification controller.`
    -   [x] Write answers of your learning module's "Reflection Publisher-2" questions in this README.
-   **STAGE 3: Implement notification mechanism**
    -   [x] Commit: `Implement update method in Subscriber model to send notification HTTP requests.`
    -   [x] Commit: `Implement notify function in Notification service to notify each Subscriber.`
    -   [x] Commit: `Implement publish function in Program service and Program controller.`
    -   [x] Commit: `Edit Product service methods to call notify after create/delete.`
    -   [ ] Write answers of your learning module's "Reflection Publisher-3" questions in this README.

## Your Reflections
This is the place for you to write reflections:

### Mandatory (Publisher) Reflections

#### Reflection Publisher-1
1. Jika hanya ada satu jenis Subscriber, cukup menggunakan satu struct tanpa perlu trait, tetapi jika ada berbagai jenis subscriber dengan perilaku berbeda, maka trait tetap diperlukan agar lebih fleksibel dalam menerapkan pola Observer.
2. Vec bisa digunakan jika jumlah subscriber kecil dan diakses dengan iterasi yang sederhana, tetapi kalau perlu pencarian cepat berdasarkan ID, DashMap lebih efisien karena memiliki waktu akses yang lebih cepat dibandingkan Vec.
3. DashMap juga lebih praktis dibandingkan pola Singleton karena langsung menangani thread-safety, sementara Singleton (misalnya dengan lazy_static) hanya memastikan satu instance tanpa menangani akses bersamaan. tetapi keduanya bisa digunakan bersama, contohnya Singleton mencegah instansiasi ganda, dan DashMap memastikan operasi tetap aman dalam multi-threading.

#### Reflection Publisher-2
1. Memisahkan Service dan Repository dari Model mengikuti prinsip Separation of Concerns dan Single Responsibility Principle (SRP). Repository bertanggung jawab atas akses data, seperti mengambil dan menyimpan informasi ke database, sementara Service menangani business logic tanpa bergantung langsung pada cara data disimpan. Dengan tugas yang dipisah, perubahan pada penyimpanan data tidak memengaruhi business logic, dan sebaliknya business logic dapat diuji tanpa harus berurusan dengan database. Hal ini juga membuat kode lebih modular dan lebih mudah dimaintain.

2. Jika hanya menggunakan model, setiap model harus menangani akses data dan business logic, membuat kode lebih kompleks dan sulit dimaintain. Program, Subscriber, dan Notification akan saling berinteraksi langsung, menyebabkan banyak ketergantungan antar model. Perubahan pada satu model bisa berdampak ke model lain, meningkatkan risiko bug dan duplikasi kode. Dengan memisahkan Service dan Repository, interaksi antar model lebih rapi, sehingga kode lebih modular dan mudah dimaintain.

3. Postman membantu saya menguji API yang saya buat. Dengan Postman, saya dapat mengirim request dengan mudah tanpa perlu membuat frontend.  Fitur seperti Collections memungkinkan saya menyimpan dan mengelola berbagai request API. Selain itu, fitur Automated Testing dan Mock Server juga menarik karena dapat membantu saya menguji respons API tanpa tergantung pada backend yang sudah sepenuhnya terimplementasi, yang berguna untuk tugas kelompok. 
#### Reflection Publisher-3
