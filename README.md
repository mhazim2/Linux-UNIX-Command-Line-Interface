# Linux-UNIX-Command-Line-Interface
Copy Materi

% Linux/UNIX Command Line Interface
% Auriza Akbar
% 2015

# Perintah Dasar

`echo`
:   Menampilkan satu baris teks.

    ```bash
    echo [OPTION] [STRING]
    ```

    - `-n`: tanpa *newline* di akhir
    - `-e`: mengaktifkan interpretasi *backslash escape*


`hostname`
:   Menampilkan nama *host* sistem.

    ```bash
    hostname [OPTION]
    ```
    - `-I`: menampilkan semua alamat IP pada *host*


`uname`
:   Menampilkan informasi kernel sistem.

    ```bash
    uname [OPTION]
    ```
    - `-a`: menampilkan semua informasi


`uptime`
:   Menampilkan berapa lama sistem sudah berjalan.

    ```bash
    uptime
    ```


`whoami`
:   Menampilkan nama *user* yang sedang dipakai.

    ```bash
    whoami
    ```


`who`
:   Menampilkan siapa saja yang sedang *log on*.

    ```bash
    who [OPTION]
    ```
    - `-b`: waktu *booting* sistem terakhir


`date`
:   Mencetak (atau mengeset) tanggal dan waktu sistem.

    ```bash
    date
    ```

`cal`
:   Menampilkan kalender.

    ```bash
    cal [[MONTH] YEAR]
    ```

`last`
:   Menampilkan daftar kapan *user* terakhir kali *log in*.

    ```bash
    last
    ```

`logout`
:   Keluar dari sistem.

    ```bash
    logout
    ```

`poweroff`
:   Mematikan (*shut down*) sistem.

    ```bash
    poweroff
    ```

Tombol panah `Up` dan `Down`
:   Mengakses *history* perintah yang pernah dimasukkan.


Tombol `Tab`
:   Mengaktifkan fitur *auto-completion*

# File dan direktori

`pwd`
:   Mencetak nama direktori saat ini.

    ```bash
    pwd
    ```

`cd`
:   Mengganti direktori.

    ```bash
    cd [DIRECTORY]
    ```
    Jika tanpa parameter `DIRECTORY`, maka `cd` akan mengganti ke directori *home* (`~`).

`ls`
:   Menampilkan daftar isi direktori.

    ```bash
    ls [OPTION] [FILE]
    ```

    - `-a`: tampilkan juga *dotfile*
    - `-h`: mencetak ukuran dalam format yang mudah dibaca
    - `-i`: cetak nomor indeks setiap *file*
    - `-l`: gunakan format panjang
    - `-r`: balik urutan *sorting*
    - `-S`: *sorting* berdasarkan ukuran

`touch`
:   Meng-*update* waktu akses dan modifikasi suatu `FILE`.

    ```bash
    touch FILE
    ```
     Jika `FILE` belum ada, maka `touch` akan membuat `FILE` kosong.

`mkdir`
:   Membuat direktori.

    ```bash
    mkdir [OPTION] DIRECTORY
    ```

    - `-p`: buar direktori *parent* jika diperlukan

`cp`
:   Menyalin *file* dan direktori.

    ```bash
    cp [OPTION] SOURCE DEST
    cp [OPTION] SOURCE... DIRECTORY
    ```
    - `-f`: tanpa konfirmasi jika terjadi *overwrite*
    - `-i`: meminta konfirmasi sebelum *overwrite*
    - `-r`: salin direktori secara rekursif


`mv`
:   Memindahkan (mengganti nama)  *file*.

    ```bash
    mv [OPTION] SOURCE DEST
    mv [OPTION] SOURCE... DIRECTORY
    ```
    - `-f`: tanpa konfirmasi jika terjadi *overwrite*
    - `-i`: meminta konfirmasi sebelum *overwrite*

`rm`
:   Menghapus *file* atau direktori.

    ```bash
    rm [OPTION] FILE...
    ```

    - `-f`: tanpa konfirmasi, abaikan jika *file* tidak ada
    - `-i`: meminta konfirmasi setiap kali menghapus
    - `-r`: hapus direktori dan isinya secara rekursif

`rmdir`
:   Menghapus direktori kosong.

    ```bash
    rmdir [OPTION] DIRECTORY...
    ```

    - `-p`: hapus `DIRECTORY` dan pendahulunya; misal: '`rmdir -p a/b/c`{.bash}' sama dengan '`rmdir a/b/c a/b a`{.bash}'

*Dotfile*
:   *File* yang namanya diawali dengan tanda titik. Secara umum, *dotfile* tidak akan terlihat (*hidden*). Biasanya digunakan untuk menyimpan konfigurasi program.

`~`
:   Simbol untuk direktori `home`.

`.`
:   Simbol untuk direktori saat ini.

`..`
:   Simbol untuk direktori *parent* dari direktori saat ini.

`/`
:   Simbol untuk direktori *root*, yaitu direktori paling atas.

*Absolute path*
:   *Path* yang diawali dari direktori *root*; contoh: '`/etc`'.

*Relative path*
:   *Path* yang tidak diawali dari direktori *root*; contoh: '`../etc`'.


# *Ownership* dan *Permission*

Setiap *file* memiliki atribut pemilik (*user* dan *group*). Hanya *superuser* yang dapat mengubah kepemilikan suatu *file*.

Tiap *file* juga memiliki atribut *permission* untuk mengatur siapa saja yang dapat mengakses *file* tersebut.
Terdapat tiga macam *permission*:

:   Jenis *permission* dan artinya

*Permission*    *File*      *Directory*
------------    ---------   ---------------------
`r`             *read*      *list files*
`w`             *write*     *add or remove files*
`x`             *execute*   *enter the directory*

yang diasosiasikan ke tiga jenis *user* yang mungkin mengakses *file*:

- *user owner* (`u`)
- *group owner* (`g`)
- *others* (`o`)


`su`
:   Mengganti ID *user* atau menjadi *superuser*.

    ```bash
    su [OPTION] [USERNAME]
    ```
    - `-c COMMAND`: menspesifikasikan perintah yang akan dijalankan oleh *shell*
    - `-l`: menyediakan *environment* yang sama seperti jika *user* *log in* secara langsung


`chown`
:   Mengganti *owner* dan grup suatu *file*.

    ```bash
    chown [OPTION] [OWNER][:GROUP] FILE
    ```
    - `-R`: rekursif

`chmod`
:   Mengganti mode *permission* suatu *file*.

    ```bash
    chmod [OPTION] MODE[,MODE]... FILE...
    chmod [OPTION] OCTAL-MODE FILE...
    ```
    - `-R`: rekursif

    Format mode simbolis adalah `[ugoa][+-=][rwxX]`. Sedangkan, format mode numerik adalah tiga digit oktal (0-7), yang didapatkan dari penambahan bit bernilai 4 (*read*), 2 (*write*), dan 1 (*execute*).

    Catatan: opsi *permission* `X` hanya akan mengeset bit *execute* untuk direktori saja, sangat berguna saat dipakai secara rekursif.

    Contoh:

    - Mode: `r--r--r--` (444)
        - `chmod a=r FILE`{.bash}
        - `chmod 444 FILE`{.bash}
    - Mode: `rw-rw----` (660)
        - `chmod ug=rw,o= FILE`{.bash}
        - `chmod 660 FILE`{.bash}
    - Mode: `rwxr-xr-x` (755)
        - `chmod a=rx,u+w FILE`{.bash}
        - `chmod 755 FILE`{.bash}


# Link

*Link* berguna untuk membuat semacam *shortcut*. Terdapat dua macam *link*:

- *hard link*: mengacu pada nomor indeks *file* sehingga lebih *robust* terhadap perubahan nama *file*, namun hanya bisa dalam satu partisi
- *symbolic link*: mengacu pada nama *file*, bisa lintas partisi, bisa *link* ke direktori, namun jika *file* asli berubah namanya akan mengakibatkan *broken link*

`ln`
:   Membuat *link* antar-*file*.

    ```bash
    ln [OPTION] TARGET LINK-NAME
    ```
    - `-s`: membuat *symbolic link*

# *Stream*, *Pipe*, dan *Redirect*


## *Stream* Standar

Setiap proses yang berjalan memiliki tiga *stream* standar I/O:

0. *standard input* (`stdin`)
1. *standard output* (`stdout`)
2. *standard error* (`stderr`)

```
               +------------+
               |            |
stdin  +-----> |   PROSES   | ------>  stdout
               |            |
               +------+-----+
                      |
                      |
                      v
                    stderr

```

## *Pipe*

*Pipe* (karakter `|`) menyalurkan `stdout` dari suatu proses menjadi `stdin` dari proses berikutnya. *Pipe* berguna untuk membuat *pipeline*, yaitu gabungan beberapa perintah untuk mengerjakan suatu tugas.

    COMMAND1 | COMMAND2

```
                     pipe
+------------+         +        +------------+
|            |         |        |            |
|  PROCESS1  +---------|------->|  PROCESS2  |
|            | stdout  |  stdin |            |
+------------+         +        +------------+
```

Contoh:

- `echo "halo" | rev`{.bash}
- `echo "2 + 5" | bc`{.bash}
- `who | wc -l`{.bash}


## *Redirect*

*Redirect* mengarahkan *stream* standar proses ke suatu *file* yang ditentukan oleh pengguna.

: Jenis *redirect*

Karakter    *Redirect*
--------    ----------
`<`         `stdin`
`>`         `stdout`
`>>`        `stdout` (*append*)
`2>`        `stderr`

Contoh:

```bash
date > now.txt 2> err.txt
rev < now.txt
rev < now.txt > rev.txt
```


# Pencarian

`man`
:   Mencari halaman manual suatu program, fungsi, dan sebagainya.

    ```bash
    man [SECTION] PAGE
    ```
    - `q`: keluar
    - `/PATTERN`: pencarian kata
    - `n`: lanjutkan pencarian kata
    - `N`: lanjutkan pencarian kata (mundur)

`which`
:   Mencari lokasi *file* program.

    ```bash
    which FILENAME
    ```

`locate`
:   Mencari *file* berdasarkan nama.

    ```bash
    locate [OPTION] PATTERN
    ```
    - `-c`: cetak jumlah *file* yang ditemukan
    - `-i`: abaikan perbedaan huruf kecil/kapital (*case insensitive*)


`find`
:   Mencari *file* pada sebuah hierarki direktori.

    ```bash
    find [PATH] [TEST]...
    ```

    - `-name PATTERN    `: pencarian berdasarkan pola nama *file*
    - `-iname PATTERN   `: sama seperti `-name` tetapi *case insensitive*
    - `-size [+-]N[kMG] `: ukuran *file* sebesar *N* unit
    - `-atime [+-]N     `: *file* terakhir diakses *N* hari yang lalu
    - `-mtime [+-]N     `: *file* terakhir dimodifikasi *N* hari yang lalu
    - `-empty           `: *file* kosong
    - `-type [df]       `: jenis *file* (direktori atau *file* biasa)

`grep`
:   Mencetak baris *file* yang cocok dengan suatu pola.

    ```bash
    grep [OPTION] PATTERN FILE
    ```
    - `-c`: cetak jumlah baris yang cocok
    - `-i`: abaikan perbedaan huruf kecil/kapital (*case insensitive*)
    - `-v`: invers pencocokan, untuk menampilkan baris yang tidak cocok dengan pola
    - `-r`: rekursif

`xargs`
:   Mengubah tiap baris masukan menjadi argumen untuk suatu perintah.

    ```bash
    xargs [OPTION] COMMAND
    ```
    - `-l[N]`: gunakan *N* baris argumen untuk sekali perintah (*default* 1)

    - Contoh:

        - `find . -name "*.bak" | xargs -l rm`{.bash}
        - `seq 1 10 | xargs echo`{.bash}



# Pemrosesan Teks

`editor`
:   Membuat dan mengedit *file* teks.

    ```bash
    editor [OPTION] FILE
    ```

    - `-i`: indentasi otomatis, berguna untuk mengedit kode program
    - `-u`: mengaktifkan fitur *undo* (`Alt+U`)
    - `-w`: mematikan fitur *wrapping* untuk baris yang panjang
    - `Ctrl+O`: menyimpan *file*
    - `Ctrl+X`: keluar dari `editor`


`pager` (`less`)
:   Menampilkan *file* teks yang panjang per halaman.

    ```bash
    pager FILE
    ```
    - `q`: keluar
    - `/PATTERN`: pencarian kata
    - `n`: lanjutkan pencarian kata
    - `N`: lanjutkan pencarian kata (mundur)


`cat`
:   Menggabungkan sejumlah *file* dan menampilkannya ke *standard output*.

    ```bash
    cat [OPTION] [FILE]...
    ```
    - `-n`: berikan nomor baris
    - `-b`: berikan nomor baris yang ada isinya saja
    - `-s`: hilangkan baris kosong yang berulang


`split`
:   Memecah *file* menjadi beberapa bagian.

    ```bash
    split [OPTION] FILE
    ```
    - `-b SIZE`: pecah per *SIZE* *byte*
    - `-l N`: pecah per *N* baris


`sort`
:   Mengurutkan tiap baris pada *file* teks

    ```bash
    sort [OPTION] FILE
    ```
    - `-n`: (*numeric*) urutkan secara numerik
    - `-r`: (*reverse*) urutkan terbalik

`uniq`
:   Menampilkan baris yang unik saja

    ```bash
    uniq [OPTION] FILE
    ```
    - `-c`: (*count*) tambahkan jumlah kemunculan di awal baris
    - `-d`: (*duplicate*) hanya cetak baris yang berulang
    - `-i`: (*ignore-case*) abaikan perbedaan huruf kecil/kapital
    - `-u`: (*unique*) hanya cetak baris yang tidak berulang

`head`
:   Menampilkan bagian awal *file*.

    ```bash
    head [OPTION] FILE
    ```
    - `-b K`: tampilkan *K* *byte* pertama
    - `-n K`: tampilkan *K* baris pertama

`tail`
:   Menampilkan bagian akhir *file*.

    ```bash
    tail [OPTION] FILE
    ```
    - `-b K`: tampilkan K *byte* terakhir
    - `-n K`: tampilkan K baris terakhir

`tr`
:   Translasi dari karakter set pertama ke karakter set kedua.
    ```bash
    tr [OPTION] SET1 [SET2]
    ```

    - `-d`: (*delete*) menghapus karakter yang terdapat pada `SET1`
    - `-s`: (*squeeze*) memampatkan karakter yang berulang dari `SET1` menjadi satu karakter

`sed`
:   *Stream editor*, mengganti *string* menggunakan ekspresi reguler.
    ```bash
    sed [OPTION] 's/REGEXP/REPLACEMENT/' [FILE]
    ```

    - `-e`: (*execute*) menambahkan perintah untuk dieksekusi
    - `-i`: (*in-place*) mengedit *file* secara langsung


`cut`
:   Mengambil sebagian karakter/kolom dari sebaris teks.
    ```bash
    cut OPTION [FILE]
    ```

    - `-c LIST`: (*characters*) pilih hanya karakter berikut
    - `-f LIST`: (*fields*) pilih hanya kolom berikut
    - `-d DELIM`: (*delimiter*) gunakan karakter `DELIM` (selain TAB) sebagai pemisah antarkolom

`paste`
:   Menggabungkan baris-baris tiap *file*.
    ```bash
    paste [OPTION] [FILE]
    ```

    - `-d`: (*delimiter*) menambahkan perintah untuk dieksekusi
    - `-i`: (*in-place*) mengedit *file* secara langsung


Latihan:

- [HackerRank text processing challenges](https://www.hackerrank.com/domains/shell/textpro)
- Buat satu *shell script* untuk membaca sebuah *file* teks,
    - menentukan *n* kata yang paling banyak muncul, dan
    - mencetak kata-kata tersebut beserta frekuensinya dengan urutan menurun


<!--

# Ekspresi Reguler

## Ekspansi String

```bash
echo n{1,2,3}
echo n{1..10}
echo n{1..10..2}
```

-->

# Manajemen Proses

Lihat modul [Linux System Adminsitration](http://cs.ipb.ac.id/~auriza/so/book/LinuxSystemAdministration.pdf) bab 8--10.

# Instalasi Aplikasi

## *Repository*

`apt-get`
:   Aplikasi untuk manajemen paket *software*

    ```bash
    apt-get update
    apt-get upgrade
    apt-get install PKG...
    apt-get remove PKG...
    ```

    - `update`: meng-*update* daftar paket aplikasi
    - `upgrade`: meng-*upgrade* paket aplikasi yang sudah terinstal dengan versi yang lebih baru
    - `install`: menginstal paket aplikasi
    - `remove`: meng-*uninstall* paket aplikasi

## *Source code*

```bash
tar -xvzf PKG.tar.gz
cd PKG
./configure
make
make install
```


<!--
Edit text files on the command line
Manipulate text files from the command line
Archive and compress files and directories
Assemble partitions as LVM devices
Configure swap partitions
File attributes
Find files on the filesystem
Format filesystems
Mount filesystems automatically at boot time
Mount networked filesystems
Partition storage devices
Troubleshoot filesystem issues
Create backups
Create local user groups
Manage file permissions
Manage fstab entries
Manage local users accounts
Manage the startup process and related services
Manage user accounts
Manage user account attributes
Manage user processes
Restore backed up data
Set file permissions and ownership
Access the root account
Use sudo to manage access to the root account
Write basic bash shell scripts
Install software packages
-->
