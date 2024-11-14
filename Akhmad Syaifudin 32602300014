#include <iostream>
#include <vector>
#include <algorithm>
#include <string>
using namespace std;

class Buku {
public:
    string Judul;
    string Pengarang;
    int TahunTerbit;
    string ISBN;
    bool Status;

    Buku(string Judul, string Pengarang, int TahunTerbit, string ISBN, bool Status)
        : Judul(Judul), Pengarang(Pengarang), TahunTerbit(TahunTerbit), ISBN(ISBN), Status(Status) {}

    void displayBukuInfo() {
        cout << "Judul Buku: " << Judul << endl;
        cout << "Pengarang: " << Pengarang << endl;
        cout << "Tahun Terbit: " << TahunTerbit << endl;
        cout << "ISBN: " << ISBN << endl;
        cout << "Status: " << (Status ? "Tersedia" : "Dipinjam") << endl;
    }

    string getISBN() const { return ISBN; }

    void displayISBN() const {
        cout << "ISBN: " << ISBN << endl;
    }
};

class Anggota {
public:
    string Nama;
    vector<Buku*> BukuDipinjam;

    Anggota(string Nama) : Nama(Nama) {}

    void PinjamBuku(Buku* buku) {
        BukuDipinjam.push_back(buku);
        buku->Status = false; 
    }
    
    void KembalikanBuku(Buku* buku) {
        auto it = find(BukuDipinjam.begin(), BukuDipinjam.end(), buku);
        if (it != BukuDipinjam.end()) {
            BukuDipinjam.erase(it); 
            buku->Status = true;  
        } else {
            cout << "Buku tidak ditemukan dalam daftar peminjaman!" << endl;
        }
    }

    void displayAnggotaInfo() {
        cout << "Nama Anggota: " << Nama << endl;
        cout << "Daftar Buku yang Dipinjam: " << endl;
        if (BukuDipinjam.empty()) {
            cout << "Tidak ada buku yang dipinjam." << endl;
        } else {
            for (Buku* buku : BukuDipinjam) {
                buku->displayBukuInfo();
            }
        }
    }
};

int main() {
    vector<Buku> daftarBuku;  
    vector<Anggota> daftarAnggota;  

    int pilihan;
    do {
        cout << "\n===== Menu Perpustakaan =====\n";
        cout << "1. Tambah Buku\n";
        cout << "2. Tambah Anggota \n";
        cout << "3. Pinjam Buku\n";
        cout << "4. Kembalikan Buku\n";
        cout << "5. Tampilkan Daftar Buku\n";
        cout << "6. Tampilkan Daftar Anggota dan Buku yang Dipinjam\n";
        cout << "0. Keluar\n";
        cout << "Pilih menu: ";
        cin >> pilihan;
        cin.ignore();  

        switch (pilihan) {
            case 1: {
                string judul, pengarang, isbn;
                int tahunTerbit;
                cout << "Masukkan judul buku: ";
                getline(cin, judul);
                cout << "Masukkan pengarang buku: ";
                getline(cin, pengarang);
                cout << "Masukkan tahun terbit: ";
                cin >> tahunTerbit;
                cin.ignore();  
                cout << "Masukkan ISBN buku: ";
                getline(cin, isbn);
                daftarBuku.push_back(Buku(judul, pengarang, tahunTerbit, isbn, true));
                cout << "Buku " << judul << " telah ditambahkan ke perpustakaan.\n";
                break;
            }        
            case 2: {
                string nama;
                cout << "Masukkan nama anggota: ";
                getline(cin, nama);
                daftarAnggota.push_back(Anggota(nama));
                cout << "Anggota " << nama << " telah ditambahkan.\n";
                break;
            }

            case 3: {
                string nama, isbn;
                cout << "Masukkan nama anggota: ";
                getline(cin, nama);
                cout << "Masukkan ISBN buku yang ingin dipinjam: ";
                getline(cin, isbn);

                Anggota* anggota = nullptr;
                for (auto& a : daftarAnggota) {
                    if (a.Nama == nama) {
                        anggota = &a;
                        break;
                    }
                }

                if (anggota) {
                    Buku* buku = nullptr;
                    for (auto& b : daftarBuku) {
                        if (b.ISBN == isbn && b.Status == true) {
                            buku = &b;
                            break;
                        }
                    }

                    if (buku) {
                        anggota->PinjamBuku(buku);
                        cout << "Buku " << buku->Judul << " berhasil dipinjam oleh " << anggota->Nama << ".\n";
                    } else {
                        cout << "Buku dengan ISBN " << isbn << " tidak tersedia.\n";
                    }
                } else {
                    cout << "Anggota dengan nama " << nama << " tidak ditemukan.\n";
                }
                break;
            }
            case 4: {
                string nama, isbn;
                cout << "Masukkan nama anggota: ";
                getline(cin, nama);
                cout << "Masukkan ISBN buku yang ingin dikembalikan: ";
                getline(cin, isbn);

                Anggota* anggota = nullptr;
                for (auto& a : daftarAnggota) {
                    if (a.Nama == nama) {
                        anggota = &a;
                        break;
                    }
                }

                if (anggota) {
                    Buku* buku = nullptr;
                    for (auto& b : daftarBuku) {
                        if (b.ISBN == isbn && b.Status == false) {
                            buku = &b;
                            break;
                        }
                    }

                    if (buku) {
                        anggota->KembalikanBuku(buku);
                        cout << "Buku " << buku->Judul << " berhasil dikembalikan oleh " << anggota->Nama << ".\n";
                    } else {
                        cout << "Buku dengan ISBN " << isbn << " tidak ditemukan atau tidak dipinjam.\n";
                    }
                } else {
                    cout << "Anggota dengan nama " << nama << " tidak ditemukan.\n";
                }
                break;
            }
            case 5: {
                cout << "\n===== Daftar Buku =====\n";
                for (auto& buku : daftarBuku) {
                    buku.displayBukuInfo();
                    cout << endl;
                }
                break;
            }
            case 6: {
                cout << "\n===== Daftar Anggota dan Buku yang Dipinjam =====\n";
                for (auto& anggota : daftarAnggota) {
                    anggota.displayAnggotaInfo();
                    cout << endl;
                }
                break;
            }
            case 0:
                cout << "Keluar dari aplikasi.\n";
                break;
            default:
                cout << "Pilihan tidak valid! Silakan pilih lagi.\n";
                break;
        }
    } while (pilihan != 0);

    return 0;
}
