# Bank-Management C++
Error Password 
#include <stdlib.h>
#include<iostream>
#include<fstream>
#include<cctype>
#include<iomanip>
#include <conio.h>
#include <string.h>

using namespace std;


class TaiKhoan
{
	public:
	int ID;
	char Ten[50];
	int TienGui;
	char LoaiTaiKhoan;
public:
	void TaoTaiKhoan();	
	void HienThiTaiKhoan() const;	
	void SuaTaiKhoan();	
	void GuiTien(int);	
	void RutTien(int);	
	void BaoCao() const;	
	int NhapLaiID() const;	
	int NhapLaiTienGui() const;	
	char NhapLaiLoaiTaiKhoan() const;	

	void DangNhap()
{
    char c=0,x[20];
    int i = 0;
    cout << "PASS:";
    
    while(1) {
	    c = getch();
        if (c == 13) {
            break;
        } else {
            x[i++] = c;
            cout << "*" ;
        }
    }
    
   x[i] = '\0';
int mk = atoi(x);
	if ( mk != 00 )
	{
		cout<<"Sai Mat Khau."<<endl;
		cout<<"Nhap Lai."<<endl;
		DangNhap();
	}	

getch();
}

};         

void TaiKhoan::TaoTaiKhoan()
{
	cout<<"\nNhap So Tai Khoan :";
	cin>>ID;
	cout<<"\n\nNhap Ten Tai Khoan : ";
	cin.ignore();
	cin.getline(Ten,50);
	cout<<"\nNhap Loai Tai Khoan (T/V) : ";
	cin>>LoaiTaiKhoan;
	cout<<"\nNhap So Tien Gui : ";
	cin>>TienGui;
	cout<<"\n\n\nDang Tao Tai Khoan ...";
}

void TaiKhoan::HienThiTaiKhoan() const
{
	cout<<"\nSo Tai Khoan : "<<ID;
	cout<<"\nTen Tai Khoan : ";
	cout<<Ten;
	cout<<"\nLoai Tai Khoan : "<<LoaiTaiKhoan;
	cout<<"\nSo Du Tai Khoan : "<<TienGui;
}


void TaiKhoan::SuaTaiKhoan()
{
	cout<<"\nNhap So Tai Khoan : "<<ID;
	cout<<"\nNhap Ten Tai Khoan Moi : ";
	cin.ignore();
	cin.getline(Ten,50);
	cout<<"\nNhap Loai Tai Khoan Moi : ";
	cin>>LoaiTaiKhoan;
	LoaiTaiKhoan=toupper(LoaiTaiKhoan);
	cout<<"\nNhap So Tien Gui Moi : ";
	cin>>TienGui;
}

	
void TaiKhoan::GuiTien(int x)
{
	TienGui+=x;
}
	
void TaiKhoan::RutTien(int x)
{
	TienGui-=x;
}
	
void TaiKhoan::BaoCao() const
{
	cout<<ID<<setw(10)<<" "<<Ten<<setw(10)<<" "<<LoaiTaiKhoan<<setw(15)<<TienGui<<endl;
}

	
int TaiKhoan::NhapLaiID() const
{
	return ID;
}

int TaiKhoan::NhapLaiTienGui() const
{
	return TienGui;
}

char TaiKhoan::NhapLaiLoaiTaiKhoan() const
{
	return LoaiTaiKhoan;
}


void GhiTaiKhoan();	
void HienThiSoDu(int);	
void SuaTaiKhoan(int);	
void XoaTaiKhoan(int);	
void DanhSachTaiKhoan();		
void TienGui_TienRut(int, int); 
void ManHinhChinh();	



int main()
{
	TaiKhoan dn ;
	dn.DangNhap();
	char ch;
	int num;
		ManHinhChinh();
	do
	{
		system("cls");
		cout<<"\n\n\n\t Thao Tac:";
		cout<<"\n\n\t1. Tao Tai Khoan";
		cout<<"\n\n\t2. Gui Tien";
		cout<<"\n\n\t3. Rut Tien";
		cout<<"\n\n\t4. Kiem Tra So Du";
		cout<<"\n\n\t5. Danh Sach Tai Khoan";
		cout<<"\n\n\t6. Dong Tai Khoan";
		cout<<"\n\n\t7. Sua Tai Khoan";
		cout<<"\n\n\t8. Thoat";
		cout<<"\n\n\tNhap Lua Chon (1-8) ";
		cin>>ch;
		system("cls");
		switch(ch)
		{
		case '1':
			GhiTaiKhoan();
			break;
		case '2':
			cout<<"\n\n\tNhap So Tai Khoan : "; cin>>num;
			TienGui_TienRut(num, 1);
			break;
		case '3':
			cout<<"\n\n\tNhap So Tai Khoan : "; cin>>num;
			TienGui_TienRut(num, 2);
			break;
		case '4': 
			cout<<"\n\n\tNhap So Tai Khoan : "; cin>>num;
			HienThiSoDu(num);
			break;
		case '5':
			DanhSachTaiKhoan();
			break;
		case '6':
			cout<<"\n\n\tNhap So Tai Khoan : "; cin>>num;
			XoaTaiKhoan(num);
			break;
		 case '7':
			cout<<"\n\n\tNhap So Tai Khoan : "; cin>>num;
			SuaTaiKhoan(num);
			break;
		 case '8':
			cout<<"\n\n\tTran Thanh Cam On";
			break;
		 default :cout<<"\a";
		}
		cin.ignore();
		cin.get();
	}while(ch!='8');
	
	return 0;
}




void GhiTaiKhoan()
{
	TaiKhoan ac;
	ofstream outFile;
	outFile.open("TaiKhoan.dat",ios::binary|ios::app);
	ac.TaoTaiKhoan();
	outFile.write(reinterpret_cast<char *> (&ac), sizeof(TaiKhoan));
	outFile.close();
}


void HienThiSoDu(int n)
{
	TaiKhoan ac;
	bool flag=false;
	ifstream inFile;
	inFile.open("TaiKhoan.dat",ios::binary);
	if(!inFile)
	{
		cout<<"Khong The Thuc Hien !! Quay Lai...";
		return;
	}
	cout<<"\nChi Tiet\n";

    	while(inFile.read(reinterpret_cast<char *> (&ac), sizeof(TaiKhoan)))
	{
		if(ac.NhapLaiID()==n)
		{
			ac.HienThiTaiKhoan();
			flag=true;
		}
	}
	inFile.close();
	if(flag==false)
		cout<<"\n\nSo Tai Khoan Khong Ton Tai";
}



void SuaTaiKhoan(int n)
{
	bool found=false;
	TaiKhoan ac;
	fstream File;
	File.open("TaiKhoan.dat",ios::binary|ios::in|ios::out);
	if(!File)
	{
		cout<<"Khong The Thuc Hien !! Quay Lai...";
		return;
	}
	while(!File.eof() && found==false)
	{
		File.read(reinterpret_cast<char *> (&ac), sizeof(TaiKhoan));
		if(ac.NhapLaiID()==n)
		{
			ac.HienThiTaiKhoan();
			cout<<"\n\nNhap Thong Tin Moi Ve Tai Khoan"<<endl;
			ac.SuaTaiKhoan();
			int pos=(-1)*static_cast<int>(sizeof(TaiKhoan));
			File.seekp(pos,ios::cur);
			File.write(reinterpret_cast<char *> (&ac), sizeof(TaiKhoan));
			cout<<"\n\n\t Chinh Sua Thanh Cong";
			found=true;
		  }
	}
	File.close();
	if(found==false)
		cout<<"\n\n Khong Ton Tai ";
}



void XoaTaiKhoan(int n)
{
	TaiKhoan ac;
	ifstream inFile;
	ofstream outFile;
	inFile.open("TaiKhoan.dat",ios::binary);
	if(!inFile)
	{
		cout<<"Khong The Thuc Hien !! Quay Lai...";
		return;
	}
	outFile.open("Temp.dat",ios::binary);
	inFile.seekg(0,ios::beg);
	while(inFile.read(reinterpret_cast<char *> (&ac), sizeof(TaiKhoan)))
	{
		if(ac.NhapLaiID()!=n)
		{
			outFile.write(reinterpret_cast<char *> (&ac), sizeof(TaiKhoan));
		}
	}
	inFile.close();
	outFile.close();
	remove("TaiKhoan.dat");
	rename("Temp.dat","TaiKhoan.dat");
	cout<<"\n\n\tDa Xoa Ban Ghi ..";
}


void DanhSachTaiKhoan()
{
	TaiKhoan ac;
	ifstream inFile;
	inFile.open("TaiKhoan.dat",ios::binary);
	if(!inFile)
	{
		cout<<"Khong The Thuc Hien !! Quay Lai...";
		return;
	}
	cout<<"\n\n\t\tDanh Sach Tai Khoan\n\n";
	cout<<"====================================================\n";
	cout<<"So ID      Ten           Loai 		Tai Khoan\n";
	cout<<"====================================================\n";
	while(inFile.read(reinterpret_cast<char *> (&ac),sizeof(TaiKhoan)))
	{
		ac.BaoCao();
	}
	inFile.close();
}


void TienGui_TienRut(int n, int option)
{
	int amt;
	bool found=false;
	TaiKhoan ac;
	fstream File;
	File.open("TaiKhoan.dat", ios::binary|ios::in|ios::out);
	if(!File)
	{
		cout<<"Khong Ton Tai !! Quay Lai...";
		return;
	}
	while(!File.eof() && found==false)
	{
		File.read(reinterpret_cast<char *> (&ac), sizeof(TaiKhoan));
		if(ac.NhapLaiID()==n)
		{
			ac.HienThiTaiKhoan();
			if(option==1)
			{
				cout<<"\n\n\tGui Tien ";
				cout<<"\n\nNhap So Tien Gui";
				cin>>amt;
				ac.GuiTien(amt);
			}
			if(option==2)
			{
				cout<<"\n\n\tRut Tien ";
				cout<<"\n\nNhap Vao So Tien Rut";
				cin>>amt;
				int bal=ac.NhapLaiTienGui()-amt;
				if((bal<500 && ac.NhapLaiLoaiTaiKhoan()=='S') || (bal<1000 && ac.NhapLaiLoaiTaiKhoan()=='C'))
					cout<<"So Du Khong Du";
				else
					ac.RutTien(amt);
			}
			int pos=(-1)*static_cast<int>(sizeof(ac));
			File.seekp(pos,ios::cur);
			File.write(reinterpret_cast<char *> (&ac), sizeof(TaiKhoan));
			cout<<"\n\n\t Thanh Cong";
			found=true;
	       }
         }
	File.close();
	if(found==false)
		cout<<"\n\n Ban Ghi Khong Ton Tai ";
}




void ManHinhChinh()
{
	cout<<"\n\n\t  Ten Ngan Hang: Nhom 3 Bank";
	cout<<"\n\n\tHe Thong Quan Ly Ngan Hang";
	cout<<"\n\n\tThuc Hien : Nhom 3";
	cout<<"\n\n\tTruong : HUBT";
	cin.get();
}

