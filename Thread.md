# Thread

## Definisi

Beberapa program yang dapat dieksekusi pada proses yang sama

## Context Switching
Context Switching adalah proses ketika CPU berpindah mengerjakan thread lainnya pada proses yang **sama**

## Sumber Daya Thread

1. Program Counter
>Masing-masing thread memiliki program counter tersendiri
2. Register
>Register digunakan oleh Thread untuk menyimpan data variabel
3. Stack
>Stack digunakan oleh Thread untuk menyimpan lokasi return sebuah procedure
4. Process
>Seluruh Thread pada Process yang sama akan menggunakan sumber daya yang sama juga

## State
1. Running
2. Blocked
3. Ready
4. Terminated

## POSIX Threads Command

- `int pthread_create(pthread_t *thread, const pthread_attr_t * attr, void * (*start_routine)(void *), void *arg)`

Membuat thread baru. Mengembalikan 0 jika berhasil.

- `void pthread_exit(void *retval)`

Mengakhiri sebuah thread

- `int pthread_join(pthread_t th, void **thread_return)`

Menunggu **sebuah** thread selesai sebelum lanjut. Mengembalikan 0 jika berhasil.

- `pthread_t pthread_self(void)`

Mendapatkan id dari thread yang menjalankan memanggil function tersebut

- `int pthread_equal(pthread_t t1, pthread_t t2)`

Membandingkan 2 thread (t1 dan t2). Mengembalikan 0 apabila beda.

- `int pthread_cancel(pthread_t thread)`

Digunakan untuk mengirim *cancelation request` pada sebuah thread. Mengembalikan 0 apabila gagal.

- `int pthread_detach(pthread_t thread)`

Membuat sebuah thread menjadi `detach`. Thread yang detached tidak akan mengembalikan sumber daya yang digunakan ketika selesai. Selebihnya, thread detached juga tidak akan mengaktifkan `thread_join` apabila berakhir. Mengembalikan 0 jika berhasil.

- `int pthread_yield(void)`

Memberikan sumber daya CPU saat ini ke thread lainnya. Mengembalikan 0 jika berhasil.

