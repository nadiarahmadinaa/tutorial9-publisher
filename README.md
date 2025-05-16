# Reflection

## How much data your publisher program will send to the message broker in one run?
Publisher akan mengirim 5 messages dalam sekali run. Masing-masing message mengandung suatu UserCreatedEventMessage yang terdiri dari user_id string, dan user_name string. Satu messagenya memiliki besaran sekitar 30 bytes. Hal tersebut menghitung format serialisasi, size dari string, dan metadata lainnya. Sehingga total bytes dari sekali run sekitar 150 bytes.

## The URL "amqp://guest:guest@localhost:5672" is the same as in the subscriber program, what does it mean?
Dengan url koneksi ke AMQP yang sama antara publisher dan subscriber, berarti keduanya terhubung ke instance RabbitMQ yang sama. Hal ini penting untuk bisa mengirim message dari publisher ke subscriber dengan baik. Publisher mengirim pesan ke RabbitMQ dengan routing key "user_create". Kemudian RabbitMQ menyimpan message tersebut di dalam queue. Subscriber juga akan connect dan register handler untuk action "user_created". Kemudian RabbitMQ akan mengirim pesan ke subscriber jika available.

## Running RabbitMQ as message broker
![Running RabbitMQ as message broker](image/running.png)

## Sending and processing event
![Sending and processing event](image/console.png)
Gambar ini menunjukkan jalannya kedua program publisher dan subscriber pada console. Disini publisher akan push notification yang akan diterima pada sisi subscriber. Program subscriber aktif untuk listen terus menerus. Sedangkan program publisher hanya aktif ketika ingin mengirim notifikasi. Setiap run terdapat 5 messages yang terkirim ke subscriber dari publisher.