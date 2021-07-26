# Berkenalan dengan Void Linux

Pada kesempatan ini kita saya mencoba menginstall linux yang agak berbeda dari biasanya yang saya gunakan. Emangnya apa bedanya? Linux yang akan kita coba adalah void linux, sebuah distro independen dan rolling release yang menggunakan init sistem `runit`. Pada umumnya sekarang distro yang beredar kebanyakan menggunakan init sistem `systemd`. Nah tahu gak kalo init sistem ini pernah jadi perdebatan saaat itu, karena dikalaim nggak sesuai sama filosofi unix. Bahkan dulu pelopor kernel linux sempat menolaknya. Heheh malah jadi cerita kontoversi systemd, yuk kembali ke laptop. Unit sistem runit ini ternyata berjalan lebih sederhana, lebih cepat dan lebih efisien dalam menjalankan proses(nggak sama ya dengan namanya, *run(m)it*). 

Penasaran banget kan sama distro yang satu ini? sama aku juga... ayolah langsung kita tes aja yuk untuk makenya.

Untuk mendownload file iso-nya kalian bisa cek di website official dari void linux itu sendiri([ini](https://voidlinux.org/download/))

![Gambar-1](images/gambar-1.png)

Tersedia beberapa pilihan file iso untuk didownload. Dimana ada pilihan dengan basenya saja dan ada yang disertakan langsung dengan desktop environment. Dan juga ada pilihan untuk library C-nya, yakni glibc dan juga musl. Untuk musl yang merupakan library yang lebih modern tidak support untuk mesin 32-bit, sedangkan glibc merupakan library yang mungkin lebih dan support mesin 32-bit.

Disini kita akan menggunakan file iso yang base-nya aja dengan C library glibc. 

Mari kita buatkan virtual machine terlebih dahulu. Disini saya tidak akan tunjukkan caranya, karena kalian sendiri pasti tahu dan kalian bisa bebas menggunakan aplikasi virtualization yang kalian suka. Disini saya akan menggunakan virtualbox, dengan spek seperti berikut ini

![Gambar-2](images/gambar-2.png)

Selanjutnya jalankan virtual machine, dan kita akan diminta untuk login, gunakan username **root** dengan password **voidlinux**

![Gambar-3](images/gambar-3.png)

Nah setelah itu gunakan command `void-installer` untuk melakukan tahap instalasi. Maka tampil seperti gambar dibawah ini untuk menyambut kita. Lalu kita tekan saja enter untuk menlanjut ke tahap berikutnya.

![Gambar-4](images/gambar-4.png)

oh iya lupa bilang kalau untuk tahap instalasi kita akan dibantu dengan `ncurses`. Maka kita akan dihadapkan tampilan seperti gambar dibawah. Mari kita mulai dengan secara berurutan yaa.

![Gambar-5](images/gambar-5.png)

Untuk sistem keyboard kita gunakan US.

![Gambar-6](images/gambar-6.png)

Berikutnya kita atur networknya, pilih network interface yang anda inginkan. Disini saya hanya punya satu saja, jadi ya saya cuma bisa pilih itu hehe.

![Gambar-7](images/gambar-7.png)

Lalu untuk pengalokasian IP-address kita gunakan DHCP.

![Gambar-8](images/gambar-8.png)

Jika berjalan dengan lancar maka akan tampil output seperti ini 

![Gambar-9](images/gambar-9.png)

Kemudian untuk installation source kita pilih saja yang local yaitu dari file iso yang tadi kita download atau kita buat di virtual machine. 

![Gambar-10](images/gambar-10.png)

Lalu masukkan hostname sesuai keinginan kalian.

![Gambar-11](images/gambar-11.png)

Berikutnya untuk system locale kita bisa pilih `en_US.UTF-8`

![Gambar-12](images/gambar-12.png)

Lalu set timezone, disini saya memakai timezone Asia/Jakarta

![Gambar-13](images/gambar-13.png)

Masukkan password untuk user root(ga usah dibikin gambar ya hahah, gampang kok bikinnya :) )

Kemudian kita akan buatkan user baru serta passwordnya. Ini juga untuk nambahin user ga dibikin gambar yaa. Tapi disini saya menambahkan user tadi ke group root.

![Gambar-14](images/gambar-14.png)

Lalu kita select bootloadernya, Kalian bisa pilih menggunakan graphical interface untuk bootloadernya.

![Gambar-15](images/gambar-15.png)

Nah lalu kita ke bagian yang cukup tricky, yaitu partisi. Pilih disk yang akan digunakan. Disini saya hanya punya satu.

![Gambar-16](images/gambar-16.png)

Nah kemudiakan kita disediakan dua pilihan untuk melakukan partisi, yakni cfdisk dan fdisk. Disini saya akan menggunakan fdisk. 

![Gambar-17](images/gambar-17.png)

Seperti ini tampilan fdisk

![Gambar-18](images/gambar-18.png)

Partisi pertama kita akan buat dengan ukuran 512M dengan tipe primary.

![Gambar-19](images/gambar-19.png)

Lalu tekan t untuk memilih typenya, jika ingin melihat listnya bisa ketikkan L. Disini ketikkan EF untuk membuatnya sebagai UEFI 

![Gambar-20](images/gambar-20.png)

Selanjutnya buatkan lagi partisi baru dengan ukuran 1G

![Gambar-21](images/gambar-21.png)

Lalu kita buatkan partisi tersebut untuk swap. 

![Gambar-22](images/gambar-22.png)

Lalu kita buatkan satu lagi partisi dimana ini akan menjadi partisi terakhir yang akan menjadi partisi untuk folder root dan home kita. Alokasikan saja semua sisa disk ke partisi tersebut. 

![Gambar-23](images/gambar-23.png)

Partisi sudah selesai, untuk memastikan bisa kita ketikkan p lalu enter

![Gambar-24](images/gambar-24.png)

lalu tekan w untuk menyimpan semua konfigurasi tadi 

Lalu kita akan menset mountpoint partisi yang telah kita buat tadi dan menset file system-nya.

![Gambar-25](images/gambar-25.png)

Untuk partisi pertama kita akan moun di `/boot/efi` dengan file system FAT32

![Gambar-26](images/gambar-26.png)

![Gambar-27](images/gambar-27.png)

Untuk partisi kedua kita set sebagai swap,

![Gambar-28](images/gambar-28.png)

Lalu partisi terakhir kita set dengan file system ext4 di mount di `/`

![Gambar-29](images/gambar-29.png)

![Gambar-30](images/gambar-30.png)

Jika sudah selesai arahkan ke button `done` menggunakan tombol arrow lalu enter.

![Gambar-31](images/gambar-31.png)

Lalu pilih ke pilihan install, maka kita akan ditanyakan untuk melanjutkan tahap instalasi. Pilih saja Yes

![Gambar-32](images/gambar-32.png)

Kita tinggal tunggu saja instalasi selesai. Minum kopi aja dulu heheh.

![Gambar-33](images/gambar-33.png)

Ketika instalasisudah selesai maka kita akan dihadapkan pilihan untuk melakukan reboot. Kita pilih saja Yes.

![Gambar-34](images/gambar-34.png)

Karena kita belum mencabut atau meremove file iso, kita akan kembali pada tahap instalasi. Jadi cabut atau remove dulu file isonya.

Lalu nyalakan kembali virtual machine. Dan walahh kita sudah berhasil menginstall void linux dan kini kita bisa login.

![Gambar-35](images/gambar-35.png)

Udah dulu mungkin yaa, kapan-kapan kita akan coba review distro ini dan kita akan coba memasang DE dll. Makasih banyak semuanya udah baca..