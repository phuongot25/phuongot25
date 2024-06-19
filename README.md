#include <iostream>
#include <string>
using namespace std;

const int MAXbenhnhan = 100;

class Benhnhan {
    string ten;
    long masobenhnhan;
    int tuoi;
    string diachi;

public:
    Benhnhan(string ten, long masobenhnhan, int tuoi, string diachi = "") {
        this->ten = ten;
        this->tuoi = tuoi;
        this->masobenhnhan = masobenhnhan;
        this->diachi = diachi;
    }

    string getten() {
        return this->ten;
    }
    void setten(string ten) {
        this->ten = ten;
    }
    long getmasobenhnhan() {
        return this->masobenhnhan;
    }
    void setmasobenhnhan(long masobenhnhan) {
        this->masobenhnhan = masobenhnhan;
    }
    int gettuoi() {
        return this->tuoi;
    }
    void settuoi(int tuoi) {
        this->tuoi = tuoi;
    }
    string getdiachi() {
        return this->diachi;
    }

    void setdiachi(string diachi) {
        this->diachi = diachi;
    }
    void hienthi() {
        cout << "Ho ten benh nhan: " << ten << "\n";
        cout << "Ma so benh nhan: " << masobenhnhan << "\n";
        cout << "Tuoi: " << tuoi << "\n";
        cout << "Dia chi: " << diachi << "\n";
    }
    ~Benhnhan() {}
};

class Hosobenhnhan : public Benhnhan {
    string ngaykham;
    string ketquakham;

public:
    Hosobenhnhan(string ten, long masobenhnhan, int tuoi, string diachi, string ngaykham, string ketquakham)
        : Benhnhan(ten, masobenhnhan, tuoi, diachi) {
        this->ngaykham = ngaykham;
        this->ketquakham = ketquakham;
    }

    string getngaykham() {
        return this->ngaykham;
    }
    void setngaykham(string ngaykham) {
        this->ngaykham = ngaykham;
        
    }
    string getketquakham(){
    	return this->ketquakham; 
	} 
	void setketquakham(string ketquakham){
		this->ketquakham=ketquakham; 
	} 
    void Hienthihoso() {
        Benhnhan::hienthi();
        cout << "Ngay kham: " << ngaykham << "\n";
        cout << "Ket qua kham: " << ketquakham << "\n";
    }
};

Benhnhan *dsbenhnhan[MAXbenhnhan];
int soluongbenhnhan = 0;

// Cac ham quan li danh sach benh nhan
void ThemHoSoBenhNhan();
void SuaThongTinBenhNhan();
void XoaBenhNhan();
void TimKiemBenhNhan();
void SapXepBenhNhanTheoTen();
void HienThiDanhSachHoSo();

void ThemHoSoBenhNhan() {
    string ten, diachi, ngaykham, ketquakham;
    long masobenhnhan;
    int tuoi;
    cin.ignore();
    cout << "Nhap ten benh nhan: ";
    getline(cin, ten);
    cout << "Nhap ma so benh nhan: ";
    cin >> masobenhnhan;
    cout << "Nhap tuoi: ";
    cin >> tuoi;
    cin.ignore();
    cout << "Nhap dia chi: ";
    getline(cin, diachi);
    cout << "Nhap ngay kham: ";
    getline(cin, ngaykham);
    cout << "Nhap ket qua kham: ";
    getline(cin, ketquakham);

    if (soluongbenhnhan < MAXbenhnhan) {
        dsbenhnhan[soluongbenhnhan] = new Hosobenhnhan(ten, masobenhnhan, tuoi, diachi, ngaykham, ketquakham);
        ++soluongbenhnhan;
        cout << "Them moi ho so benh nhan thanh cong.\n";
    } else {
        cout << "Danh sach benh nhan da day, khong the them moi ho so benh nhan.\n";
    }
}

void HienThiDanhSachHoSo() {
    cout << "\nDanh sach ho so benh nhan:\n";
    for (int i = 0; i < soluongbenhnhan; ++i) {
        Hosobenhnhan *hosobenhnhan = static_cast<Hosobenhnhan *>(dsbenhnhan[i]);
        if (hosobenhnhan) {
            hosobenhnhan->Hienthihoso();
            cout << "\n";
        }
    }
}

void SuaThongTinBenhNhan() {
    long masobenhnhan;
    cout << "\nNhap ma so benh nhan can sua: ";
    cin >> masobenhnhan;
    bool timthay = false;
    for (int i = 0; i < soluongbenhnhan; i++) {
        if (dsbenhnhan[i]->getmasobenhnhan() == masobenhnhan) {
            cin.ignore();
            string ten, diachi, ngaykham, ketquakham;
            int tuoi;
            cout << "\nDang sua thong tin benh nhan co ma so " << masobenhnhan << "\n";
            dsbenhnhan[i]->hienthi();
            cout << "Nhap ten moi: ";
            getline(cin, ten);
            cout << "Nhap tuoi moi: ";
            cin >> tuoi;
            cin.ignore();
            cout << "Nhap dia chi moi: ";
            getline(cin, diachi);
            if (static_cast<Hosobenhnhan *>(dsbenhnhan[i])) {
                Hosobenhnhan *hosobenhnhan = static_cast<Hosobenhnhan *>(dsbenhnhan[i]);
                cout << "Nhap ngay kham moi: ";
                getline(cin, ngaykham);
                cout << "Nhap ket qua kham moi: ";
                getline(cin, ketquakham);
                hosobenhnhan->setten(ten);
                hosobenhnhan->settuoi(tuoi);
                hosobenhnhan->setdiachi(diachi);
                hosobenhnhan->setngaykham(ngaykham);
                hosobenhnhan->setketquakham(ketquakham);
            } else {
                dsbenhnhan[i]->setten(ten);
                dsbenhnhan[i]->settuoi(tuoi);
                dsbenhnhan[i]->setdiachi(diachi);
            }
            cout << "Cap nhat thong tin benh nhan thanh cong.\n";
            timthay = true;
            break;
        }
    }

    if (!timthay) {
        cout << "Khong tim thay benh nhan voi ma so " << masobenhnhan << ".\n";
    }
}

void XoaBenhNhan() {
    long masobenhnhan;
    cout << "\nNhap ma so benh nhan can xoa: ";
    cin >> masobenhnhan;
    bool timthay = false;
    for (int i = 0; i < soluongbenhnhan; i++) {
        if (dsbenhnhan[i]->getmasobenhnhan() == masobenhnhan) {
            delete dsbenhnhan[i];
            for (int j = i; j < soluongbenhnhan - 1; j++) {
                dsbenhnhan[j] = dsbenhnhan[j + 1];
            }
            --soluongbenhnhan;
            cout << "Xoa benh nhan thanh cong.\n";
            timthay = true;
            break;
        }
    }

    if (!timthay) {
        cout << "Khong tim thay benh nhan voi ma so " << masobenhnhan << ".\n";
    }
}

void TimKiemBenhNhan() {
    string ten;
    cout << "\nNhap ten benh nhan can tim: ";
    cin.ignore(); // Xóa b? nh? ð?m ð? tránh l?i nh?p
    getline(cin, ten);

    bool timthay = false;
    for (int i = 0; i < soluongbenhnhan; ++i) {
        if (dsbenhnhan[i]->getten() == ten) {
            dsbenhnhan[i]->hienthi();
            timthay = true;
        }
    }

    if (!timthay) {
        cout << "Khong tim thay benh nhan voi ten " << ten << ".\n";
    }
}

void SapXepBenhNhanTheoTen() {
    for (int i = 0; i < soluongbenhnhan - 1; ++i) {
        int min = i;
        for (int j = i + 1; j < soluongbenhnhan; ++j) {
            if (dsbenhnhan[j]->getten() < dsbenhnhan[min]->getten()) {
                min = j;
            }
        }
        if (min != i) {
            Benhnhan *temp = dsbenhnhan[i];
            dsbenhnhan[i] = dsbenhnhan[min];
            dsbenhnhan[min] = temp;
        }
    }

    cout << "Da sap xep danh sach benh nhan theo ten.\n";
}
int main() {
    int lua_chon;

    while (true) {
        cout << "\n HE THONG QUAN LY BENH NHAN VA HO SO BENH NHAN \n";
        cout << "1. Them moi ho so benh nhan\n";
        cout << "2. Sua thong tin benh nhan\n";
        cout << "3. Xoa benh nhan\n";
        cout << "4. Tim kiem benh nhan\n";
        cout << "5. Sap xep benh nhan theo ten\n";
        cout << "6. Hien thi danh sach ho so benh nhan\n";
        cout << "7. Thoat\n";
        cout << "Nhap lua chon cua ban: ";
        cin >> lua_chon;

        switch (lua_chon) {
            case 1:
                ThemHoSoBenhNhan();
                break;
            case 2:
                SuaThongTinBenhNhan();
                break;
            case 3:
                XoaBenhNhan();
                break;
            case 4:
                TimKiemBenhNhan();
                break;
            case 5:
                SapXepBenhNhanTheoTen();
                break;
            case 6:
                HienThiDanhSachHoSo();
                break;
            case 7:
                cout << "Dang thoat chuong trinh...\n";
                for (int i = 0; i < soluongbenhnhan; ++i) {
                    delete dsbenhnhan[i];
                }
                return 0;
            default:
                cout << "Lua chon khong hop le! Vui long nhap so tu 1 den 7.\n";
                break;
        }
    }

    return 0;
}
