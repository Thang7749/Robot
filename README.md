#include <iostream>
#include <cstdlib>
#include <ctype.h>
#include <iomanip>
#include <fstream>
#include <windows.h>
using namespace std;
int dem;
int m, n;
struct robot{
    int c;
    int h;
    int bot[50];
};
void nhap_file(int A[][10]){
    fstream nhap;
    nhap.open("input.txt");
    // kiem tra co mo file duoc khong

    if (nhap.is_open())
        // nhap file
        nhap >> m >> n;

    for (int i = 0; i < m; i++){
        for (int j = 0; j < n; j++)
        	nhap >> A[i][j];
    }
    nhap.close();
}

// B?NG COPY
void bang_copy(int bangchinh[][10], int bangcopy[][10], int hang, int cot){
    for (int i = 0; i < hang; i++){
        for (int j = 0; j < cot; j++){
            bangcopy[i + 1][j + 1] = bangchinh[i][j];
        }
    }
}
//  T?O VI?N
void taovien(int bang[][10], int hang, int cot){
    for (int i = 0; i < (hang + 2); i++){
        for (int j = 0; j < (cot + 2); j++){
            if (i < 1)
                bang[i][j] = 0;
            if (i > hang)
                bang[i][j] = 0;
            if (j < 1)
                bang[i][j] = 0;
            if (j > cot)
                bang[i][j] = 0;
        }
    }
}
void ctm(int bot[], int bang[][10], int hang, int cot, int buoc, int bot1[], int bang1[][10], int hang1, int cot1){
    bot[buoc] = bang[hang][cot];
    bang[hang][cot] = 0;
    bot1[buoc] = bang1[hang1][cot1];
    bang1[hang1][cot1] = 0;
    buoc++;
    ///////////////////////////////////////
    int mx = 0;
    if (bang[hang][cot - 1] > mx)
        mx = bang[hang][cot - 1];
    if (bang[hang - 1][cot] > mx)
        mx = bang[hang - 1][cot];
    if (bang[hang][cot + 1] > mx)
        mx = bang[hang][cot + 1];
    if (bang[hang + 1][cot] > mx)
        mx = bang[hang + 1][cot];
    ///////////////////////////////////////
    if (bang[hang + 1][cot] == mx)
        hang++;
    if (bang[hang - 1][cot] == mx)
        hang--;
    if (bang[hang][cot + 1] == mx)
        cot++;
    if (bang[hang][cot - 1] == mx)
        cot--;
    ///////////////////////////////////////
    int mx1 = 0;
    if (bang1[hang1][cot1 - 1] > mx1)
        mx1 = bang1[hang1][cot1 - 1];
    if (bang1[hang1 - 1][cot1] > mx1)
        mx1 = bang1[hang1 - 1][cot1];
    if (bang1[hang1][cot1 + 1] > mx1)
        mx1 = bang1[hang1][cot1 + 1];
    if (bang1[hang1 + 1][cot1] > mx1)
        mx1 = bang1[hang1 + 1][cot1];
    ///////////////////////////////////////
    if (bang1[hang1 + 1][cot1] == mx1)
        hang1++;
    if (bang1[hang1 - 1][cot1] == mx1)
        hang1--;
    if (bang1[hang1][cot1 + 1] == mx1)
        cot1++;
    if (bang1[hang1][cot1 - 1] == mx1)
        cot1--;
    if (mx == 0){
        if (mx1 == 0){
            bot[buoc]=0;
            bot1[buoc]=0;
            return;
        }
        else
            ctm(bot, bang, hang, cot, buoc, bot1, bang1, hang1, cot1);
    }
    else
        ctm(bot, bang, hang, cot, buoc, bot1, bang1, hang1, cot1);
}
void in_day_so(int bot[], int i){
    if (bot[i] == 0)
        return;
    else{
        Sleep (50);
        cout << " " << bot[i];
        i++;dem=i;
        in_day_so(bot, i);
    }
}
void FindTrung(int arr1[], int size1, int arr2[], int size2, int*& arr3, int& size3) {
    size3 = 0;
    for (int i = 0; i < size1; ++i) {
        for (int j = 0; j < size2; ++j) {
            if (arr1[i] == arr2[j]) {
                int* temp = new int[size3 + 1];
                for (int k = 0; k < size3; ++k) {
                    temp[k] = arr3[k];
                }
                temp[size3++] = arr1[i];
                delete[] arr3;
                arr3 = temp;
                break;
            }
        }
    }
}
void In(int arr[], int size) {
    for (int i = 0; i < size; ++i) { Sleep(50);
        cout << arr[i] << " ";
    }
    cout << "\n";
}
int main(){

    int A[10][10];
    int bot,bot1;
    robot p1;
    robot p2;
    int bangbot[10][10];
    int bangbot2[10][10];
    int bangbot1[10][10];
    int ln=0,chedo = 0;
    nhap_file(A);
    bang_copy(A, bangbot1, m, n);
    taovien(bangbot1, m, n);
    fstream xuat;
    xuat.open("output.txt");
    Sleep(100);
    do{
        cout<< "     ROWS: " << m << " and "
            << "COLS: " << n << endl;Sleep(100);
        cout << "  ==========TABLE==========\n";Sleep(100);
        for (int i = 0; i < (m + 2); i++){
            for (int j = 0; j < (n + 2); j++){
                if (bangbot1[i][j] > 0){
                    cout << setw(4) << bangbot1[i][j];Sleep(70);
                }else{
                    cout << setw(4) << " * ";
                }
            }
            cout << endl;
    	} Sleep(100);
            bang_copy(A, bangbot, m, n);
            taovien(bangbot, m, n);
            bang_copy(A, bangbot2, m, n);
            taovien(bangbot2, m, n);
            cout << "  =========================\n";Sleep(50);
            cout << "  ......................" << endl;Sleep(50);
            cout << "  .  ----- MENU -----  ." << endl;Sleep(50);
            cout << "  .    1.BOT PATH      ." << endl;Sleep(60);
            cout << "  .    2.ROBO TURN     ." << endl;Sleep(60);
            cout << "  .    3.OVERLAP       ." << endl;Sleep(60);
            cout << "  .    4.EXIT          ." << endl;Sleep(60);
            cout << "  .      - o0o -       ." << endl;Sleep(60);
            cout << "  ......................" << endl;Sleep(50);
            cout << "SELECT MODE: ";
            cin >> chedo;

            if (chedo == 4){cout <<"Tat ca ket qua duoc luu tai output.txt";
                    xuat.close();
                return 0;
            }
            system("cls")  ;
            ln++;
            xuat<<"lan thu: "<<ln<<endl;
            int tr;
           Sleep(40);
            switch (chedo){
	            case 1:
	                {tr=0 ;
	                do{
                    cout << "ROBOT A" << endl;
                    cout << "toa do x:";
	                cin >> p1.c;
                    cout << "toa do y:";
	                cin >> p1.h;
	                if (p1.c<n&&p1.h<m) tr=1;
	                else{system("cls");
                        cout <<"SAI TOA DO, YEU CAU NHAP LAI !\n";}
                    Sleep(100);
	                }while(tr==0);}
	                ctm(p1.bot, bangbot, p1.h + 1, p1.c + 1, 0, p2.bot, bangbot2, 0, 0);
	                cout << "Duong di cua robot :";
	                in_day_so(p1.bot, 0);
	                xuat<<"che do 1:\n";
	                xuat << "Duong di cua robot :";
	                for (int i=0;i<dem;i++)
                    xuat<<" " <<p1.bot[i];
                    xuat<<endl;
	                cout << endl;
	                break;
	            case 2:
                    {tr=0;
                    do{
	                cout << "ROBOT A" << endl;
	                cout << "toa do x:";
	                cin >> p1.c;
	                cout << "toa do y:";
	                cin >> p1.h;
	                cout << "ROBOT B" << endl;
	                cout << "toa do x:";
	                cin >> p2.c;
	                cout << "toa do y:";
	                cin >> p2.h;
	                if (p1.c<n&&p1.h<m)
                    if (p2.c<n&&p2.h<m)tr=1;
                    if (tr==0){system("cls");
                        cout <<"SAI TOA DO, YEU CAU NHAP LAI !\n";};Sleep(100);
                   }while(tr==0);}
	                ctm(p1.bot, bangbot, p1.h + 1, p1.c + 1, 0, p2.bot, bangbot, p2.h + 1, p2.c + 1);
	                cout << "Duong di cua robot 1:";
	                in_day_so(p1.bot, 0);
	                xuat<<"che do 2:\n";
	                xuat << "Duong di cua robot 1:";
	                for (int i=0;i<dem;i++)
                    xuat<<" " <<p1.bot[i];
                    xuat<<endl;
	                cout << endl;
	                cout << "Duong di cua robot 2:";
	                in_day_so(p2.bot, 0);
	                xuat << "Duong di cua robot 2:";
	                for (int i=0;i<dem;i++)
                    xuat<<" " <<p2.bot[i];
                    xuat<<endl;
	                cout << endl;

	                break;
	            case 3:
	                {tr=0;
                    do{
	                cout << "ROBOT A" << endl;
	                cout << "toa do x:";
	                cin >> p1.c;
	                cout << "toa do y:";
	                cin >> p1.h;
	                cout << "ROBOT B" << endl;
	                cout << "toa do x:";
	                cin >> p2.c;
	                cout << "toa do y:";
	                cin >> p2.h;
	                if (p1.c<n&&p1.h<m)
                    if (p2.c<n&&p2.h<m)tr=1;
                    if (tr==0){system("cls");
                        cout <<"SAI TOA DO, YEU CAU NHAP LAI !\n";};Sleep(100);
                   }while(tr==0);}
	                ctm(p1.bot, bangbot, p1.h + 1, p1.c + 1, 0, p2.bot, bangbot2, p2.h + 1, p2.c + 1);
	                cout << "Duong di cua robot 1:";
	                in_day_so(p1.bot, 0);
	                xuat<<"che do 3:\n";
	                xuat << "Duong di cua robot 1:";
	                for (int i=0;i<dem;i++)
                    xuat<<" " <<p1.bot[i];
                    xuat<<endl;
                    int size1=dem;
	                cout << endl;
	                cout << "Duong di cua robot 2:";
	                in_day_so(p2.bot, 0);
	                xuat << "Duong di cua robot 1:";
	                for (int i=0;i<dem;i++)
                    xuat<<" " <<p1.bot[i];
                    xuat<<endl;
                    int size2=dem;
                    int* arr3 = NULL;
                    int size3 = 0;
                    FindTrung(p1.bot,size1,p2.bot,size2,arr3, size3);
                    cout<<endl;
                    cout<<"\nCac diem di chuyen trung nhau cua ROBOT A va ROBOT B\n";
                    xuat<<"\nCac diem di chuyen trung nhau cua ROBOT A va ROBOT B\n";
                    In(arr3, size3);
                    for (int i = 0; i < size3; ++i) {
                    xuat<< arr3[i] << " ";}
                    xuat<< "\n";
	                cout << endl;
	                break;
            }
            char next;Sleep(50);
            cout << " << 1.NEXT >>";
            cin >> next;Sleep(70);
            system("cls");
        } while (chedo != 4);
}
