# Collision Detection with Mouse
Merupakan sebuah tugas dari mata kuliah Pemrograman Berbasis Objek, yaitu mengaplikasikan sebuah game dengan collision detection pada web http://zetcode.com/javagames/collision/.

# Pemrograman Berbasis Objek C
## Anggota Kelompok :
- Richard Asmarakandi - 05111940000017 - [@soraasmarakandi](http://github.com/soraasmarakandi)
- Ahmad Syafiq Aqil Wafi - 05111940000089 - [@Syafiqjos](http://github.com/Syafiqjos)
- Afifan Syafaqi Yahya - 05111940000234 - [@anakpayah](http://github.com/anakpayah)

Game ini adalah permainan tembak - tembakan pesawat. Pemain menjalankan SpaceShip yang memiliki misi atau objective untuk mengalahkan Alien - alien dengan cara menembak mereka dengan missile SpaceShip yang dimiliki Pemain. Apa bila Pemain dapat mengalahkan semua Alien dan selamat hingga akhir maka menang, sedangkan jika pemain terkena alien maka pemain akan kalah.
Pada proyek ini terdapat updates atau perubahan antara lain adalah, pergerakan SpaceShip menggunakan Mouse, penambahan batas pergerakan SpaceShip, penambahan tembak missile dengan mouse dan juga terdapat demo video youtube yang ada.

# Berikut adalah tampilan gameplay dari game ini.

Video Gameplay : [LINK Gameplay](https://www.youtube.com/watch?v=QKgxuCMY25M).

## Tampilan Gameplay Update
![Image of Gameplay](/Images/gameplay.png)

# Berikut adalah gambar dari diagram kelas pada game yang telah diupdate ini.
![Image of UML Diagram](/Images/uml3.png)
![Image of UML Diagram](/Images/uml4.png)

# Berikut penjelasan mengenai updates pada game ini :

## 1. Perubahan KeyEvent menjadi MouseMotionEvent
Untuk mengubah controller pada spaceship dengan mouse, kami memodifikasi 2 class yang telah dibuat. Class tersebut adalah `board.java` dan `spaceship.java`.
Pada `board.java`, kita menambah class untuk mouse control bernama `MouseHandler`. Pada class  tersebut, segala aksi yang dilakukan oleh mouse akan dicatat dan dijadikan fungsi agar terdapat reaksi pada program ketika mouse melakukan suatu aksi, seperti `mouseMove`, `mouseClick` dan lainnya. karena kami ingin object spaceship mengikuti mouse, maka kami masukkan fungsi `spaceship.move` kedalam fungsi `mouseMoved` dengan komponen parameter `tempX` dan `tempY` yang menandakan koordinat mouse. Hal itu yang akan membatasi pergerakan spaceship agar tidak keluar layar.
Lalu pada fungsi `spaceship.move`, diatur posisi spaceship, yaitu pada variabel `x` dan `y` diatur agar sama dengan posisi mouse yang telah dicatat oleh `tempX` dan `tempY` pada mousemoved.

## 2. Penambahan Batasan Border untuk Move Spaceship yang dijalankan oleh Mouse Motion
Untuk mencegah Spaceship kita keluar dari window dan selalu berada didalam game window, kita harus memberikan batas untuk pencegahan tersebut. Untuk mempermudah abstraksi, kami mengubah parameter fungsi `move` dari Class `SpaceShip` dari `MouseEvent e` menjadi `int posX` dan `int posY`. Sehingga kami dapat mencegah border pada Class `Board` dan pada bagian Inner Class `MouseHandler`.

```
spaceship.move(tempX, tempY);
```

Untuk MouseHandler sendiri kami menambahkan constanta `POS_X_MAX` dan `POS_Y_MAX` yang merupakan batas maksimal koordinal pixel dari border. Kami tidak memberikan batas minimal karena batas minimal koordinat pixel telah diketahui bernilai 0. Kami juga memodifikasi Constructor untuk memasang nilai Constanta tersebut.

```
private final int POS_X_MAX;
private final int POS_Y_MAX;
```
Nilai Constanta MouseHandler di set menjadi berikut.

```
MouseHandler tempHandler = new MouseHandler(B_WIDTH - ICRAFT_X / 2,B_HEIGHT - ICRAFT_Y / 2);
```

Nilai tersebut dipilih karena memberikan hasil yang diinginkan.

Lalu untuk pencegahan border, kami mengubah nilai `e.getX()` dan `e.getY()` sebelum dikirimkan ke fungsi `move` pada Class `SpaceShip`.

```
int tempX = e.getX();
int tempY = e.getY();

if (tempX <= 0) {
	tempX = 0;
} else if (tempX >= POS_X_MAX) {
	tempX = POS_X_MAX;
}

if (tempY <= 0) {
	tempY = 0;
} else if (tempY >= POS_Y_MAX) {
	tempY = POS_Y_MAX;
}
```

## 3. Memberi Event MouseClick untuk Menembak dengan menggunakan Left Mouse Button
Agar mempermudah permainan dan agar lebih cocok dimainkan dengan mouse, kami berinisiatif untuk menambahkan Event MouseClick untuk menembak missile Spaceship.

Untuk melakukan hal tersebut, kami menambahkan interface baru yaitu `MouseListener` pada Class `MouseHandler`.

```
private class MouseHandler implements MouseMotionListener, MouseListener
```

Lalu kami memasukkan semua abstraksi dari interface tersebut. Setelah itu kita hanya membutuhkan fungsi `mousePressed` agar missile dapat ditembakkan dari spaceship saat mouse di klik.

```
@Override
public void mousePressed(MouseEvent e) {
	// TODO Auto-generated method stub
	spaceship.fire();
}
```

Kemudian, agar dapat berfungsi dengan baik, kami menambahkan listener pada fungsi `InitBoard()`

```
addMouseListener(tempHandler);
```

## 4. Menambah Fungsi baru mouseMovement untuk memperbaiki Bug Conflict dari MouseListener dan MouseMotionListener
Terdapat bug yang aneh dan tidak diketahui perbaikan yang paling efektif. Meskipun begitu kami berhasil mengatasinya dengan cara berikut.

Bug ini terjadi ketika Player menekan tombol click pada mouse, lalu didrag, spaceship tidak dapat bergerak. Sedangkan jika mouse hanya digerakkan tanpa menekan tombol, maka spaceship dapat bergerak.
Diketahui hal ini terjadi karena listener tidak membaca fungsi `mouseMove` melainkan `mouseDrag` saat proses drag.
Jadi kami membuat fungsi baru `mouseMovement` yang memiliki parameter sama dengan `mouseMove`.
Lalu kami menjalankan fungsi `mouseMovement` pada `mouseMove` dan `mouseDrag`.

```
private void mouseMovement(MouseEvent e) {
	int tempX = e.getX();
	int tempY = e.getY();
	
	if (tempX <= 0) {
		tempX = 0;
	} else if (tempX >= POS_X_MAX) {
		tempX = POS_X_MAX;
	}
	
	if (tempY <= 0) {
		tempY = 0;
	} else if (tempY >= POS_Y_MAX) {
		tempY = POS_Y_MAX;
	}
	
	spaceship.move(tempX, tempY);
}

@Override
public void mouseDragged(MouseEvent e) {
	mouseMovement(e);
}

@Override
public void mouseMoved(MouseEvent e) {
	mouseMovement(e);
}
```

Dengan cara ini, bug conflict ini dapat diperbaiki dengan baik.

# Terima Kasih