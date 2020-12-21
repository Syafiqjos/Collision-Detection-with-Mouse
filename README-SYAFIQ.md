## Penambahan Batasan Border untuk Move Spaceship yang dijalankan oleh Mouse Motion
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

## Memberi Event MouseClick untuk Menembak dengan menggunakan Left Mouse Button
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

## Menambah Fungsi baru mouseMovement untuk memperbaiki Bug Conflict dari MouseListener dan MouseMotionListener
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