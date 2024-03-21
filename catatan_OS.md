# Catatan Operating System

## C Basic

### CLI Arguments

1. int argc
    >Variabel Integer yang digunakan untuk menyimpan jumlah argument yang ingin di-passing ke main. Argc minimal bernilai 1 untuk memanggil nama program itu sendiri, dan minimal bernilai 2 jika ingin mem-passing sebuah argumen dari CLI.
2. char *argv[]
    >Array of String yang berguna untuk menyimpan argument yang di-passing melalui CLI. Argv[0] adalah nama program. Argv[1] adalah argumen pertama yang diberikan. Argv[argc] adalah null pointer.
3. Command

    `./exe_file arg1 arg2 ... argN`


## Process

### Task Struct

Setiap process pada linux dapat direpresentasikan menggunakan struktur data **task_struct**.

### Task Vector

Task Vector berisikan maksimum 512 elemen, yang dimana masing-masing elemen tersebut adalah pointer terhadap sebuah task_struct.

### PCB

Process Control Blocks berisikan semua informasi yang dibutuhkan agar sebuah Process dapat berjalan dengan semestinya.

### Process Pointer

1. p_pptr
    >Pointer yang menunjuk Parent Process
2. p_cptr
    >Pointer yang menunjuk Child Process paling muda
3. p_osptr
    >Pointer yang menunjuk Sibling Process lebih tua
4. p_ysptr
    >Pointer yang menunjuk Sibling Process lebih muda

### Process Function

1. pid_t getpid(void)
    >Digunakan untuk mendapatkan Process ID sebuah Child Process
2. pid_t getppid (void)
    >Digunakan untuk mendapatkan Process ID Parent Process
3. pid_t fork(void)
    >Digunakan untuk membuat sebuah Child Process

### PID

1. Child Process mengembalikan Process ID = 0.
2. Parent Process mengembalikan Process ID = Child PID.

## Thread

### Sumber Daya Thread

1. Program Counter
>Masing-masing thread memiliki program counter tersendiri
2. Register
>Register digunakan oleh Thread untuk menyimpan data variabel
3. Stack
>Stack digunakan oleh Thread untuk menyimpan lokasi return sebuah procedure
4. Process
>Seluruh Thread pada Process yang sama akan menggunakan sumber daya yang sama juga

### State
1. Running
2. Blocked
3. Ready
4. Terminated

### Syscall
1. thread_create
2. thread_exit
3. thread_join
4. thread_yield

### POSIX Threads Command
1. Pthread_create
    >Membuat thread baru
2. Pthread_exit
    >Mengakhiri sebuah thread
3. Pthread_join
    >Menunggu **sebuah** thread selesai sebelum lanjut
4. Pthread_yield
    >Memberikan sumber daya CPU saat ini ke thread lainnya

### Process Switching
Process Switching adalah proses ketika CPU mem-block sebuah process untuk berpindah mengerjakan process lainnya. Cost dari Process Switching cukup besar.

### Context Switching
Context Switching adalah proses ketika CPU berpindah mengerjakan thread lainnya pada proses yang **sama**

### Pseudo Paralelism
Mengeksekusi program secara paralel hanya pada 1 CPU

