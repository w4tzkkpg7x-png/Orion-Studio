# Orion-Studio
Orion (Which stands for Ontological Rapid-Instruction Object-Network) is a unique project designed not to replace existing programming language from scratch, but rather to serve as a piece of art. Its core purpose is to simplify rigid programming language by infusing them with philosophical nuances, and similiar like C programming language.

===========================


# Orion - VerCode: Briar - VerNum: v2.0.0 - Creator: Mahad
## Spesifikasi formal untuk EBNF Orion
- = : definisi aturan
- , = konkatenasi
- | : pilihan (alternatif / OR)
- [...] : opsional (0 atau 1 kali)
- {...} : repetisi
- "..." : simbol terminal
- ; : akhir dari aturan EBNF

Console::Orion -> merupakan sebuah header dari Orion Standard Library
Console::println -> perintah untuk mencetak teks ke layar
Console::cherr -> perintah untuk menampilkan teks error ke layar
Console::string -> perintah memanggil string
Console::vector -> perintah memanggil vector

Akhiran sintaks harus memakai semicolon ("{}"). Tanpa itu, kode tidak akan bekerja.

module Main adalah perintah untuk memanggil atau menyertakan suatu perkakas ke dalam program kamu sebelum kodenya dijalankan. Dalam hal ini untuk memanggil perkakas/library bawaan Orion yang isinya perintah-perintah untuk menangani input dan output.

use Console::Orion adalah perintah untuk memberitahu sistem bahwa ia ditugaskan untuk menggunakan Bahasa Orion. Artinya, perintah ini menyediakan fasilitas untuk :
- menerima input dari keyboard
- menammpilkan output ke layar

tanpa module Main, compiler tidak tahu apa itu Console::Orion, Console::println, dan func.

tanpa module Main, compiler akan mengatakan kira-kira seperti:
'Console::println' was not declared
atau:
'println' is undefined
karena compiler belum diberi tahu definisi Console.

Intinya, module Main adakah preprocessor directive yang dijalankan sebelum prroses kompilasi.
Console::Orion adalah header dari Orion Standard Library.

## Contoh sintaks
Bahasa pemrograman Orion wajib menggunakan teks : "module Main" di awal-awal, dilanjut dengan "use Console::Orion" dibawahnya. Contoh sintaks untuk mencetak teks biasa yang benar :

module Main
use Console::Orion

entry main() {
    Console::println("Hello World");
}

ini adalah contoh sintaks untuk mencetak teks biasa yang salah :

Module Main

// kata "module" harus menggunakan huruf kecil di awal, dan kata "Main" dengan huruf kapital di awal

-------------------------------------------------------------------------------

### contoh sintaks Orion yang benar menggunakan Function

module Main
use Console::Orion

func greet(str nama) -> str {
    return("Salve, " + nama);
}

entry main() {
    let msg = greet("Cosmos");
    Console::println(msg);
}

### contoh sintaks Orion yang benar menggunakan void (fungsi tanpa return value):

module Main
use Console::Orion
use Console::String

func sapaSiswa(str nama) -> void {
    Console::println("Selamat siang, " nama "!");
}

entry main() {
    sapaSiswa("Raka");
}

------------------------------------------------------------------------------

### contoh sintaks Orion yang benar menggunakan constructed (const)

module Main
use Console::String
use Console::Orion

entry main() {
    let namaSiswa[5] = str{"Algani", "Rifki", "Firly", "Bayu", "Ambara"};
    let daftarSiswa = (inputUser) {
        if (inputUser == "siswa") {
            for (int i = 0; i < 5; i++) {
                Console::println(namaSiswa[i]);
            }
        }
    }
}

Menggunakan *->* sebelum blok kode *{...}* pada Lambda/Closure (*let daftarSiswa = (inputUser) ->*), *if*, hingga *for*. Ini membantu memperjelas bahwa sebuah ekspresi akann membuka blok eksekusi (scope baru). -- _Aturan ini kini dihilanglan, sehingga tidak ada *->*. Kecuali untuk void, class, dan lainnya. Aturan ini ditetapkan pada tanggal 26/10/2026._

------------------------------------------------------------------------------

### Array
module Main
use Console::Orion
use Console::String

entry main() {
    let namaSiswa[5] = str{"Algan", "Rifki", "Ahmad", "Saeful", "Ashrul"};
    let umurSiswa[5] = int{16, 18, 17, 18, 16};
    let daftarSiswa = (inputUser) {
        if (inputUser == "siswa") {
            for (int i = 0; i < 5; i++) {
                Console::println(namaSiswa[i]);
            }
        } else if (inputUser == "umur") {
            for (int i = 0; i < 5; i++) {
                Console::println("Umur siswa ke-" + i + " : " + umurSiswa[i]);
            }
        }
    }
}

Menggunakan deklarasi Array yang tegas & jelas, seperti pada *let namaSiswa[5] = str{...}*.

------------------------------------------------------------------

### Contoh penggunaan struct yang benar di bahasa Orion

module Main
use Console::Orion
use Console::String

func Siswa -> struct {
    str nama;
    int umur;
    float nilai;
};

entry main() {
    let s1 = Siswa{"Raka", 17, 98.5};

    Console::println("Nama : " s1.nama);
    Console::println("Umur : " s1.umur);
    Console::println("Nilai : " s1.nilai);
}

_Kini struct Orion berubah dari yang awalnya `struct Siswa` menjadi `func Siswa -> struct`. Dengan diakhiri semicolon di akhir kurawal struct. Aturan ini ditetapkan pada tanggal 26/10/2026._
--------------------------------------------------------------

### Contoh penggunaan struct dalam array & parameter fungsi

module Main
use Console::Orion

func Pelajar -> struct {
    str nama;
    int kelas;
};

func cetakInfo(Pelajar p) -> void {
    Console::println("Siswa : " +  p.nama + " | Kelas " + p.kelas);
};

entry main() {
    let daftar[2] = Pelajar{
        Pelajar{"Algani", 11}, Pelajar{"Firly", 11};
    }

    cetakInfo(daftar[0]);
}

_Kini Orion menggunakan keyword "+" agar memperjelas kode. Aturan ini ditetapkan pada tanggal 05/10/2026._
-----------------------------------------------------------------

### Contoh cara menggunakan sintaks input penggguna yang benar (ada dua variasi yang didukung)
- basic read
- prompt read

=================================================================

module Main
use Console::Orion

entry main() {
    // metode basic read
    Console::println("Masukkan nama Anda:");
    let nama = Console::read();

    // metode prompt read
    let kota = Console::read("Masukkan kota asal: ");
    Console::println("Halo " + nama + " dari " + kota + "!");
}

`Console::read()` disini mengembalikan `str`, maka kamu bisa menggunakan fungsi konversi eksplisit seperti `to_int()`, `to_float`, dan `to_str`. Contoh:

let inputTeks = Console::read("Masukkan umur: ");
let umur = to_int(inputTeks);
let tinggi = to_float("170.5");
let teksUmur = to_str(umur);

maka ini adalah contoh program utuh dari kalkulator umur sederhananya:

module Main
use Console::Orion
use Console::String

entry main() {
    Console::println("=== Program cek kelayakan SIM ===");

    let nama = Console::read("Masukkan nama: ");
    let inputUmur = Console::read("Masukkan umur anda: ");

    let umur = to_int(inputUmur);

    if (umur >= 17) {
        Console::println("Selamat " + nama + ", Anda sudah berhak memiliki SIM");
    } else {
        let sisaTahun = 17 - umur;
        Console::println("Maaf " + nama + ", Anda harus menunggu " + sisaTahun + " tahun lagi.");
    }
}

_Gaya sintaks input diatas sudah tidak lagi digunakan/telah diganti di Orion versi baru (Briar v2.0.0) pada tanggal 26/10/2026. File README.md ini adalah panduan Orion terbaru, Orion: Briar v2.0.0_
-------------------------------------------------------------

#### Lexical Block Scope ('{...}')
Aturan memori dan cakupan variabel / Memory & scope rules:
catatan: variabel di Orion menggunakan Lexical Scoping. Variabel yang dideklarasikan di dalam blok _{...}_ hanya hidup selama blok itu aktif. Setelah eksekusinya keluar dari _}_, memori lokal variabel itu akan otomatis dibersihkan / deallocated dari stack.

contoh yang benar:

entry main() {
    let x = 10;

    if (x > 5) {
        let y = 20;
        Console::println(x + y);
    }
}

#### Parameter Passing
pembuatan variabel dan pengiriman argumen fungsi di Orion bersifat pass-by-value. Tapi untuk struct atau array yang berukuran besar, atau ketika kamu ingin mengubah data asli dari dalam fungsi, kamu harus menyediakan kata kunci *ref*. Contoh penggunaan keywordnya :

module Main
use Console::Orion

func Player -> struct {
    str name;
    int hp;
};

func healPlayer(ref Player p, int amount) -> void {
    p.hp = p.hp + amount;
    Console::println(p.nama + " memulihkan " + amount + " HP");
};

entry main() {
    let p1 = Player{"Raka", 50};
    healPlayer(p1, 30);
    Console::println("HP Sekarang: " + p1.hp);
};

#### Konstanta
Contoh:

let skor = 100;
skor = 150;

const PI = 3.14159;

#### Loop control flow (break dan continue)
break : untuk menghentikan perulangan secara paksa dan keluar dari blok loop
continue : melewati sisa instruksi di iterasi saat ini dan langsung lompat ke iterasi berikutnya.

contoh:

for (int i == 0l i < 10; i++) {
    if (i == 3) {
        continue;
    }
    if (i == 7) {
        break;
    }
    Console::println("Angka: " + i);
}

-------------------------------------------------------

### Update baru

#### Contoh pemakaian kode menggunakan String, void, function, dan class.

module Main
use Console::Orion
use Console::String

// function
func greet(name: str) -> str {
	return "Salve, " + name;
};

// void
func sapaSiswa(str nama) -> void {
	Console::println("Selamat siang, " + nama + "!");
};

// class public
func Siswa() -> class {
public:
    str nama;
	int umur;
	char kelas;
	func intro() -> void {
		Console::println("Nama: " + nama + ", umur: " + umur + ", kelas: " + kelas);
	}
};

entry main() {
	let msg = greet("Cosmos");
	Console::println(msg);
	
	openClass::Siswa as siswa1;
	siswa1.nama = "Fitra";
	siswa1.umur = 17;
	siswa1.kelas = 'A';
	siswa.intro();
}

// class private
func Siswa() -> class {
private:
    str nama;
    int umur;
    char kelas;
}

(setiap akhiran wajib memakai semicolon, terutama pada akhiran kurawal func. Semicolon dibelakang kurawal berlaku untuk setiap func, maupun itu func-string, func-void, dan func-class)
(openClass::{namaClass}, adalah perintah untuk memanggil atau membawa Class kedalam entry Main().)
(untuk bagian function-string pada kode diatas, tidak ada update besar seperti tambahan atau perubahan, hanya penambahan semicolon di akhir.)
-----------------------------------------------------------------------------------------------------------------

#### contoh sintaks dengan kode yang sudah disempurnakan (disertai update)

module Main
use Console::Orion
use Console::String

entry main() {
    const let userBener = "admin";
    const let passBener = "kode123";
    let inputUser;
    let inputPass;

    Console::println("Masukkan username: ", Console::cin inputUser);
    Console::println("Masukkan kata sandi: ", Console::cin inputPass);

    if (inputUser == userBener && inputPass == passBener) {
        Console::println("Selamat, anda berhasil masuk.");
    } else {
        Console::println("Maaf, anda ditolak.");
    }
}

# Update: dukungan field `str` dan `char`
_24/10/2026_
Update ini melanjutkan milestone class sebelumnya yang hanya mendukung field `int`.

## Yang sudah ditambahkan

- Deklarasi field class dengan tipe `int`, `str`, dan `char`.
- Assignment string, misalnya `profil1.nama = "OrionOS";`.
- Assignment karakter, misalnya `profil1.inisial = 'O';`.
- Membaca kembali ketiga tipe field, misalnya `profil1.nama`, `profil1.umur`, dan `profil1.inisial`.
- `Console::println(...)` memilih format cetak berdasarkan tipe nilai: `%s` untuk string, `%d` untuk integer, dan `%c` untuk karakter.
- Literal karakter mendukung escape dasar: `\\n`, `\\t`, `\\r`, `\\\\`, `\\'`, dan `\\0`.
- String literal mendukung escape dasar: `\\n`, `\\t`, `\\r`, `\\\\`, dan `\\"`.
- Compiler memeriksa kesesuaian tipe ketika nilai di-assign ke field class.

# Update: sintaks input output (I/O) baru -- Yang saat ini digunakan oleh Orion: Briar v2.0.0
_26/10/2026_
module Main
use Console::Orion
use Console::String
use Console::IO

func Siswa() -> class {
    str nama;
    int umur;
    char kelas;
    func intro() -> void {
        Console::println("Halo, nama saya " + nama ", saya berumur " + )
    }
};

entry main() {
    const let userBenar = "admin";
    const let passBenar = "kode123";
    let inputUser = ?("Masukkan username anda: ");
    let inputPass = ?("Masukkan password anda: );

    if (inputUser == userBenar && inputPass == passBenar) {
        Console::println("Anda diterima");
        openClass::Siswa as siswa1 -> io {
            nama: ?("Masukkan nama siswa: ");
            umur: ?("Masukkan umur siswa: ");
            kelas: ?("Masukkan kelas siswa: ");
        };

        Console::println("=== Biodata siswa ===");
        siswa1.intro();
    } else {
        Console::println("Maaf, anda ditolak.");
    }
}
