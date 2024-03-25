# IPC

## Definisi

IPC (Inter-Process Communication) adalah media agar process yang berbeda dapat saling berkomunikasi

## Operasi IPC

- Send
- Receive

## Race Condition

Race Condition adalah kondisi ketika 2 atau lebih process mencoba melakukan operasi read/write pada **shared data** yang sama. Untuk mengatasi masalah Race Condition maka menggunakan **Critical Region**

### Solution

- Tidak boleh lebih dari 1 process mengakses critical region secara bersamaan

- Asumsi tidak boleh dibuat untuk kecepatan dan jumlah CPU

- Process yang berada di luar critical region tidak boleh melakukan block

- Tidak ada process yang harus menunggu selamanya sebelum masuk ke critical region

### Mutex

Mutex (Mutual Exclusion) adalah metode untuk menciptakan critical region **hanya untuk 1 thread** saja. Berikut merupakan langkah penggunaan mutex:

1. Deklarasi `pthread_mutex_t lock` sebagai global variabel.

2. Deklarasi `pthread_mutex_init(&lock, NULL)` pada **awal** main process. Mengembalikan 0 jika berhasil.

3. Deklarasi `pthread_mutex_lock(&lock)` pada **awal** Critical Region

4. Deklarasi `pthread_mutex_unlock(&lock)` pada **akhir** Critical Region

5. Deklarasi `pthread_mutex_destroy(&lock)` pada **akhir** main process.

### Semaphore

Semaphore adalah metode untuk menciptakan critical region untuk **lebih dari 1 thread**. Berikut merupakan langkah untuk menggunakan Semaphore:

1. Deklarasi `sem_t semaphore` sebagai variabel global.

2. Deklarasi `sem_init(&semaphore, 0, SEM_NUM)` pada **awal** main process.

3. Deklarasi `sem_wait(&semaphore)` pada **awal** Critical Region.

4. Deklarasi `sem_post(&semaphore)` pada **akhir** Critical Region.

5. Deklarasi `sem_destroy(&semaphore)` pada  **akhir** Main Process.

### Perbedaan Mutex dan Semaphore

- Mutex memastikan hanya 1 thread yang akses Critical Region, sedangkan Semaphore memperbolehkan lebih dari 1 thread untuk mengakses Critical Region

- Mutex menggunakan operasi lock dan unlock, sedangkan Semaphore menggunakan operasi wait (P) dan signal (V).

- Mutex lebih mudah untuk diimplementasikan, sedangkan Semaphore perlu penggunaan yang hati-hati

## Unnamed Pipes

Menggunakan file decriptor sebagai pipe, sehingga pipe akan hilang ketika process berakhir. Langkah menggunakan unnamed pipes adalah sebagai berikut:

1. Inisialisasi file decriptor. `fd[0]` digunakan untuk **read**, sedangkan `fd[1]` digunakan untuk **write**.

```c
int fd[2];
```

2. Untuk Process yang ingin melakukan operasi **write**, maka gunakan `fd[1]`

```c
close(fd[0]);
write(fd[1], &var, sizeof(var_type));
close(fd[1]);
```

3. Untuk Process yang ingin melakukan operasi **read**, maka gunakan `fd[0]`

```c
close(fd[1]);
read(fd[0], &var, sizeof(var_type));
close(fd[0]);
```

## Named Pipes

Menggunakan file FIFO sebagai pipe, sehingga pipe tetap ada meskipun process berakhir. Berikut merupakan langkah untuk menggunakan Named Pipes:

1. Inisialisasi file decriptor dan buat FIFO file path

```c
int fd;
char *myfifo = "/tmp/myfifo";
```

2. Buat file  FIFO pada path tersebut

```c
mkfifo(myfifo, 0666);
```

3. Untuk Process yang melakukan operasi **write**, maka gunakan kode berikut:

```c
fd = open(myfifo, 0_WRONLY);
write(fd, &var, sizeof(var_type));
close(fd);
```

4. Untuk Process yang melakukan operasi **read**, maka gunakan kode berikut:

```c
fd = open(myfifo, O_RDONLY);
read(fd, &var, sizeof(var));
close(fd);
```

5. Isi dari pipe dapat dilihat menggunakan command berikut

```bash
cat /tmp/myfifo
```

## Shared Memory

IPC yang tidak menggunakan pipes, tetapi menggunakan sebuah bagian dalam memori yang dapat digunakan oleh process yang terlibat. Hal ini memungkinkan untuk **lebih dari 2** Process saling berkomunikasi sekaligus. Berikut merupakan langkah untuk menggunakan Shared Memory:

1. Menghasilkan sebuah key untuk shared memory

```c
key_t key = ftok("/temp", 65);
```

2. Simpan alamat dari shared memory berdasarkan key yang diberikan

```c
int shmid = shmget(key, 1024, 0666|IPC_CREAT);
```

3. Attach alamat tersebut dengan sebuah variabel

```c
char *str = (char*)shmat(shmid, (void*)0, 0);
```

4. Detach variabel dari alamat shared memory

```c
shmdt(str);
```

5. Hapus Shared Memory

```c
shmctl(shmid, IPC_RMID, NULL);
```

