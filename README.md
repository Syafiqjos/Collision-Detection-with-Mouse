# PesawatCollisionDetectionJava
Merupakan sebuah tugas dari mata kuliah Pemrograman Berbasis Objek, yaitu mengaplikasikan sebuah game dengan collision detection pada web http://zetcode.com/javagames/collision/.

# Pemrograman Berbasis Objek C
## Anggota Kelompok :
- Richard Asmarakandi - 05111940000017
- Ahmad Syafiq Aqil Wafi - 05111940000089
- Afifan Syafaqi Yahya - 05111940000234

Game ini adalah permainan tembak - tembakan pesawat. Pemain menjalankan SpaceShip yang memiliki misi atau objective untuk mengalahkan Alien - alien dengan cara menembak mereka dengan missile SpaceShip yang dimiliki Pemain. Apa bila Pemain dapat mengalahkan semua Alien dan selamat hingga akhir maka menang, sedangkan jika pemain terkena alien maka pemain akan kalah.

# Berikut adalah tampilan gameplay dari game ini.

## Tampilan Gameplay
![Image of Gameplay](/Images/gameplay.png)

## Tampilan Gameover
![Image of Gameover](/Images/gameover.png)

# Berikut adalah gambar dari diagram kelas pada game ini.
![Image of UML Diagram](/Images/uml1.png)
![Image of UML Diagram](/Images/uml2.png)

# Berikut penjelasan mengenai setiap Class nya :

## 1. Sprite

dalam class sprite, terdapat 6 variabel, yaitu
protected int x = yaitu posisi secara horizontal gambar yang akan di render
protected int y = yaitu posisi secara vertical gambar yang akan di render
protected int width = yaitu lebar gambar yang akan di render
protected int height = yaitu panjang gambar yang akan di render
protected boolean visible = yaitu flag untuk menandai gambar terlihat atau tidak
protected Image image = yaitu variable untuk menampung gambar

lalu terdapat beberapa fungsi,
yang pertama Constructornya public Sprite dengan parameter x dan y yang keduanya bertipe integer.
fungsi ini sebagai inisiasi/awal letak gambarnya, juga untuk mengatur gambar terlihat atau tidak.

yang kedua adalah protected void getImageDimensions tanpa parameter yang digunakan untuk mendapatkan
nilai panjang dan lebar dari gambarnya

yang ketiga void loadImage dengan parameter imageName dengan tipe data String. imageName
adalah variabel yang digunakan untuk mencatat nama dari gambar yang akan diload atau diproses
lalu fungsinya digunakan untuk meload image yang akan di render.

yang keempat Image getImage tanpa parameter. yang digunakan untuk mendapatkan image yang dipanggil

yang kelima sampai ke kedelapan mengandung getter untuk posisi x, posisi y, isVisible dan tambahan
setter untuk isVisible sehingga bisa diatur gambar nampak atau tidak.

yang terakhir terdapat fungsi dengan return Rectangle bernama getBounds untuk mendapatkan border
atau sebuah kotak yang merepresentasikan panjang dan lebar gambar

## 2. Missile

dalam class Missile yang merupakan child dari sprite atau gerenalization dari sprite mengandung 2
variabel yaitu :
private final int BOARD_WIDTH = yaitu variabel yang digunakan untuk menyimpan lebar window ketika
di run pada tampilan layar
private final int MISSILE_SPEED = yaitu variabel yang digunakan untuk menyimpan kecepatan missile
atau besarnya perpindahan pada misil yang akan diluncurkan pesawat.

lalu terdapat beberapa fungsi,
yang pertama adalah constructor itu sendiri dengan parameter x dan y dengan tipe data integer.
constructor ini memanggil constructor dari parentnya, yaitu sprite. maka dengan kata lain,
constructor pada missile.java ini mengatur letak dari sprite atau gambar yang akan di render
pada poin x,y. lalu terdapat tambahan selain memanggil constructor dari parent, adalah memanggil
fungsi initMissile yang terdapat dan akan dijelaskan pada fungsi yang kedua

yang kedua ini adalah fungsi initMissile dengan return tipe void dan tanpa parameter. fungsi ini
digunakan sebagai sebuah inisiasi saat missile hendak dilepaskan dari pesawat. lebih rincinya,
inisiasi ini memanggil fungsi untuk meload gambar yang akan dirender dan mendapatkan panjang dan
lebar dari gambar (yang disini adalah gambar misil/missile)

lalu yang terakhir terdapat fungsi move dengan return tipe void dan tanpa parameter. fungsi ini
digunakan ketika missile telah bergerak menjauhi pesawat atau dapat dibilang telah ditembakkan
dari pesawat. fungsi ini digunakan untuk menggerakkan misil ke kanan dengan cara mengubah posisi
misil pada bidang horizontal atau sumbu x secara konstan dengan perpindahan posisi sebesar 
MISSILE_SPEED, sehingga misil tampak bergerak. lalu dalam fungsi ini juga terdapat pengecekan,
jika posisi misil melebihi dari lebar layar window, maka gambar akan di set/atur tidak terlihat
sehingga seakan2 misil keluar dari layar window.

## 3. CollisionEx
dalam class CollisionEx yang memanfaatkan JFrame sebagai parent, tidak terdapat variabel lokal
pada class ini. terdapat tiga fungsi pada class ini

yang pertama adalah constructornya, yaitu memanggil fungsi yang bernama initUI yang terdapat juga
di dalam kelas ini dan akan dijelaskan pada fungsi berikutnya

fungsi kedua inilah yang bernama initUI. pada fungsi initUI ini, langkah pertama yang dilakukan
adalah add(new Board()) yaitu membuat sebuah objek yang akan menjadi basis dari sebuah
permainan, tempat berbagai macam objek diletakkan/dirender. atau analoginya seperti papan tulis 
yang digunakan sebagai media untuk menggambar. lalu kedua, fungsi ini mengeset agar window tidak
resizeable atau tidak dapat di resize. lalu terdapat pemanggilan fungsi pack() yang mengakibatkan
semua yang berada pada window sesuai atau lebih dari ukuran window yang telah ditetapkan. lalu 
terdapat pemanggilan fungsi setTitle dengan parameter "Collision" yang digunakan untuk menamai
judul/tulisan pada window. lalu ada pemanggilan fungsi/method setLocationRelativeTo dengan
parameter null yang berfungsi untuk meletakkan window defaultnya pada tengah2 layar sehingga
ketika program dijalankan, window akan berada pada tengah2 layar. terdapat juga pemanggilan
fungsi setDefaultCloseOperation dengan komponen parameter JFrame.EXIT_ON_CLOSE yang bertujuan 
ketika program diclose, akan menggunakan method exit dari sistem.

fungsi ketiga ini adalah fungsi main. dalam fungsi main ini, terdapat pemanggilan fungsi
EventQueue.invokeLater() yang bertujuan untuk memanggil fungsi yang dibutuhkan secara asinkronus.
dengan komponen parameter pembuatan objek baru dari class CollisionEx() dan mengatur objek
tersebut untuk terlihat pada layar(mengubah nilai setVisible ke true)

## 4. Alien
Class Alien merupakan child dari Class Sprite yang mengimplementasikan posisi x dan y nya.

menggunakan atribut integer final INITIAL_X = 400 menandakan merupakan titik spawn khusus berjarak (+)400 dari garis horizontal.

menggunakan Constructor dengan nama Class itu sendiri dengan parameter x dan y berupa integer. constructor ini memanggil constructor parentnnya yaitu Sprite. didalamnya juga terdapat fungsi initAlien() yang akan dijelaskan berikutnya

menggunakan fungsi void initAlien()  tanpa parameter. fungsi ini digunakan sebagai sebuah inisiasi saat Alien akan di spwan. fungsi yang menginisialisasi dan meng-load gambar lalu dengan fungsi getImageDimension() untuk merenser dan mendapatkan nilai bentuk panjang serta lebar dari gambar tersebut.

menggunakan fungsi void move() tanpa parameter sebagai pola aktivitas class Alien.
fungsi untuk memindahkan Alien dengan kecepatan x = -1 per frame. fungsi yang membuat gambar bergerak ke kiri sejauh 1 arah horizontal. pergerakan konstan ke kiri hingga x kurang dari 0. didalam fungsi tersebut terdapat if dengan parameter jika x kurang dar 0 maka object alien tersebut akan di set x nya kembali INITIAL_X = 400.

## 5. SpaceShip
SpaceShip merupakan child dari Class Sprite yang mengimplementasikan posisi x dan y nya

terdapat beberapa atribut pada class SpaceShip ini yaitu integer dx dan dy yang nantinya berguna sebagai nilai variable penggerak object. terus ada array namanya missiles dengan tipe List<Missile> sebagai array untuk menyimpen objek dari Class Missile.

mempunyai Constructor dengan parameter x dan y bertipe integer. isinya berupa inisialisasi menggunkan fungsi constructor parentnya berupa x dan y yang berupa integer. menggunukan fungsi initCraft() yang akan dijelaskan berikutnya.

menggunakan fungsi void initCraft() tanpa parameter yang isinya untuk menginisisalisasi objek SpaceShip  dan meng-load gambar lalu dengan fungsi getImageDimension() untuk merender dan mendapatkan nilai bentuk panjang serta lebar dari gambar tersebut. fungsi ini juga menginisialisasi array missile pada objek SpaceShip untuk dimasukannyaobjek missile tersebut.

menggunakan fungsi void move() tanpa parameter sebagai pola aktivitas objek tersebut. fungsi ini untuk memindahkan objek SpaceShip dengan perpindahan x sebagai horizontal dan y sebagai vertikal. terdapat 2 fungsi if untuk mencegah objek tersebut berpindah di luar dari screen.

menggunakan getMissiles() bertipe List<Missile> untuk mereturn missile yang akan dipilih unutk dihapus.

menggunakan fungsi void keyPressed dengan parameter KeyEvent yaitu ketika tombol di keyboard tertekan. terdapat sebuah variable key bertipe integer, dengan menggunakan fungsi getKeyCode() untuk mendapatkan code keyboard berupa nilai integer. 
SPACE untuk menjalankan fungsi fire()
LEFT untuk perpindahan minus x 1
RIGHT untuk perpindahan plus x 1
UP untuk perpindahan minus y 1
DOWN untuk perpindahan plus y 1

menggunakan fungsi fire() tanpa parameter yang berguna untuk ketika onjek menembakkan missile tersebut, maka ada objek bertipe jenis Missile baru yang dimasukkan pada array missiles. objek ini akan bertahan hingga objek ini terkena Alien atau keluar screen sebelum di hapus.

menggunakan fungsi void keyReleased dengan parameter KeyEvent yaitu ketika tombol di keyboard terlepas. fungsi didalamnyaakan membuat nilai dx dan nilai dy menjadi 0 sehingga membuat objek SpaceShip tidak bergerak lagi


## 6. Board
Board Class merupakan child dari class JPanel yang mengimplementasikan interface ActionListener. Board merupakan bidang dan semua dasar yang menjalankan game ini karena di dalamnya banyak fungsi yang mengatur window, level, musuh, alien dan player. Board memiliki beberapa property penting yaitu 
timer, spaceship, aliens, ingame, ICRAFT_X, ICRAFT_Y, B_WIDTH, B_HEIGHT, DELAY, dan POS.

- timer digunakan untuk mengatur delay senilai dengan variable DELAY dari setiap frame yang di gambar (draw) setiap cycle. Semakin besar DELAY maka draw akan semakin lama setiap cycle sehingga akan terdapat effect lagging, sedangkan semakin kecil DELAY maka cycle akan semakin cepat berlalu.
- spaceship merupakan variable untuk menyimpan variable Class SpaceShip yang merupakan player utama dari game.
- aliens merupakan kumpulan list musuh dari variable Class Alien.
- ingame merupakan property untuk menyimpan apakah game berjalan atau tidak.
- ICRAFT_X, ICRAFT_Y merupakan posisi pixel dari variable spaceship.
- B_WIDTH, B_HEIGHT merupakan ukuran pixel dari window JPanel atau bisa dibilang ukuran window game.
- DELAY merupakan variable untuk delay timer.
- POS merupakan kumpulan posisi untuk menggenerate letak masing - masing Alien. Alien yang dihasilkan dari POS disimpan pada List aliens.

Board Class memiliki fungsi utama untuk mengatur jalannya seluruh aplikasi dan fungsi. Fungsi yang dijalankan di constructor terdapat fungsi initBoard() yang digunakan untuk menginisialisasi beberapa fungsi yaitu :
- addKeyListener() dari interface ActionListener untuk mendeteksi event keyboard yang dibuat dari inner class TAdapter yang merupakan child dari KeyAdapter.
- terdapat setFocusable() agar window focus, lalu setBackground() untuk mengubah background window game.
- pengaktifan ingame yang diset true agar tahu bahwa game dimulai.
- pengaturan ukuran window game dengan setPreferredSize()
- inisialisasi player spaceship serta inisialisasi alien dengan fungsi initAliens().
- lalu terakhir ada timer yang mengatur Delay Refresh Rate atau Cycle Draw dari game.

Terdapat fungsi paintComponent yang menggambar object untuk gameplay dengan fungsi drawObjects() jika player belum kalah dan menggambar object untuk gameover dengan fungsi drawGameOver() jika player kalah.
Pada drawObjects() seluruh object seperti alien, spaceship dan missile diatur disini.

Kemudian terdapat fungsi actionPerformed() yang akan selalu di jalankan setiap kali user mengirim Event. Fungsi ini merefresh player spaceship, alien dan missile serta melakukan fungsi pengecheckan collision jika player menang atau kalah.

Ketika player spaceship terkena collisions dan aktif maka variable ingame akan diubah menjadi false sehingga akan menjalankan fungsi drawGameOver() pada fungsi paintComponent(). Jika gameover maka pemain harus exit game agar dapat memainkannya lagi.

# Terima Kasih