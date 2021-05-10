# Bai Tap Lon
#include<stdio.h>
#include<conio.h>     
#include<stdlib.h>   //tim kiem . xep thu tu, cap phat bo nho ....
#include<windows.h> ///xoa man hinh , gotoxy , kich thuoc  
#include<string.h> ////ddieu chinh nhieu loai day ky tu
void gotoxy(int ,int ); 
void menu();
void add();
void xem();
void timkiem();
void suadoi();
void xoa();
struct sinhvien
{
    char ten[20];
    char sdt[10];
    int msv;
    char khoahoc[20];
    char chinhanh[20];
};
int main()
{
    gotoxy(15,8); //tac dung di chuyen con tro den toa do nao do
    printf("                          <--:HE THONG QUAN LY SINH VIEN:-->              ");
    gotoxy(19,15);
    printf("                         Nhan phim bat ki de tiep tuc                    ");
    getch();
    menu();
    return 0;
}
void menu()
{
    int luachon;
    system("cls");
    gotoxy(10,3);
    printf("<--:MENU:-->");
    gotoxy(10,5);
    printf("Nhap so thich hop de thuc hien tac vu sau.");
    gotoxy(10,7);
    printf("1 : Them ban ghi.");
    gotoxy(10,8);
    printf("2 : Xem ban ghi.");
    gotoxy(10,9);
    printf("3 : Tim kiem ban ghi.");
    gotoxy(10,10);
    printf("4 : Sua ban ghi.");
    gotoxy(10,11);
    printf("5 : Xoa.");
    gotoxy(10,12);
    printf("6 : Thoat.");
    gotoxy(10,15);
    printf("Nhap lua chon cua ban: ");
    scanf("%d",&luachon);
    switch(luachon)   // switch case re nhanh , dieu khien , de viet de doc va hieu nang tot hon so voi if else
    {
    case 1:
        add();
        break;

    case 2:
        xem();
        break;

    case 3:
        timkiem();
        break;

    case 4:
        suadoi();
        break;

    case 5:
        xoa();
        break;

    case 6:
        exit(1);
        break;

    default: // xu li case ngoai le khi ko thoa man case nao
        gotoxy(10,17);
        printf("Lua chon khong hop le.");
    }
}
void add()
{
    FILE *fp; // doc va ghi file
    struct sinhvien std; // nhap tat ca ten vao khong gian ten chung
    char another ='y';
    system("cls"); //ham dung de xoa man hinh

    fp = fopen("record.txt","ab+"); //doc file trong C
    if(fp == NULL){ // xu ly file 
        gotoxy(10,5);
        printf("Loi khi mo tep");
        exit(1);
    }
    fflush(stdin); // xoa di bo nho tam thoi cua chuong trinh de ko ton tai gia tri rac 
    while(another == 'y')
    {
        gotoxy(10,3);
        printf("<--:Them ghi:-->");
        gotoxy(10,5);
        printf("Nhap thong tin sinh vien.");
        gotoxy(10,7);
        printf("Nhap ten : ");
        gets(std.ten);
        gotoxy(10,8);
        printf("Nhap so dien thoai : ");
        gets(std.sdt);
        gotoxy(10,9);
        printf("Nhap msv : ");
        scanf("%d",&std.msv);
        fflush(stdin);
        gotoxy(10,10);
        printf("Nhap khoa hoc : ");
        gets(std.khoahoc);
        gotoxy(10,11);
        printf("Nhap chi nhanh : ");
        gets(std.chinhanh);
        fwrite(&std,sizeof(std),1,fp);
        gotoxy(10,15);
        printf("  Nhan 'y' de them ban ghi khac  hoac 'n' de thoat .");
        fflush(stdin);

        another = getch();
        system("cls");
        fflush(stdin);
    }
    fclose(fp);
    gotoxy(10,18);
    printf("Nhan phim bat ki de tiep tuc.");
    getch();
    menu();
}
void xem()
{
    FILE *fp;
    int i=1,j;
    struct sinhvien std;
    system("cls");
    gotoxy(10,3);
    printf("<--:Xem ghi:-->");
    gotoxy(10,5);
    printf("STT      Ten sinh vien      So dien thoai       MSV         Khoa hoc          Chi nhanh");
    gotoxy(10,6);
    printf("------------------------------------------------------------------------------------------");
    fp = fopen("record.txt","rb+");
    if(fp == NULL){
        gotoxy(10,8);
        printf("Loi khi mo tep.");
        exit(1);
    }
    j=8;
    while(fread(&std,sizeof(std),1,fp) == 1){
        gotoxy(10,j);
        printf("%-9d%-20s%-16s%-16d%-15s%-15s",i,std.ten,std.sdt,std.msv,std.khoahoc,std.chinhanh);
        i++;
        j++;
    }
    fclose(fp);
    gotoxy(10,j+3);
    printf("Nhan phim bat ki de tiep tuc.");
    getch();
    menu();
}
void timkiem()
{
    FILE *fp;
    struct sinhvien std;
    char stten[20];
    system("cls");
    gotoxy(10,3);
    printf("<--:Ban ghi tim kiem:-->");
    gotoxy(10,5);
    printf("Nhap ten sinh vien : ");
    fflush(stdin);
    gets(stten);
    fp = fopen("record.txt","rb+");
    if(fp == NULL){
        gotoxy(10,6);
        printf("Loi khi mo tep");
        exit(1);                         ///////exit la ham dung de thoat chuong trinh khi duoc goi 
    }
    while(fread(&std,sizeof(std),1,fp ) == 1){
        if(strcmp(stten,std.ten) == 0){
            gotoxy(10,8);
            printf("Ten : %s",std.ten);
            gotoxy(10,9);
            printf("So dien thoai : %s",std.sdt);
            gotoxy(10,10);
            printf("MSV : %d",std.msv);
            gotoxy(10,11);
            printf("Khoa hoc : %s",std.khoahoc);
            gotoxy(10,12);
            printf("Chi nhanh : %s",std.chinhanh);
        }
    }
    fclose(fp);
    gotoxy(10,16);
    printf("Nhan phim bat ki de tiep tuc.");
    getch();
    menu();
}
void suadoi()
{
    char stten[20];
    FILE *fp;
    struct sinhvien std;
    system("cls");
    gotoxy(10,3);
    printf("<--:Ban ghi sua doi:-->");
    gotoxy(10,5);
    printf("Nhap ten sinh vien can sua: ");
    fflush(stdin);
    gets(stten);
    fp = fopen("record.txt","rb+");
    if(fp == NULL){
        gotoxy(10,6);
        printf("Loi khi mo tep");
        exit(1);
    }
    rewind(fp);
    fflush(stdin);
    while(fread(&std,sizeof(std),1,fp) == 1)
    {
        if(strcmp(stten,std.ten) == 0){
            gotoxy(10,7);
            printf("Nhap ten: ");
            gets(std.ten);
            gotoxy(10,8);
            printf("Nhap so dien thoai : ");
            gets(std.sdt);
            gotoxy(10,9);
            printf("Nhap MSV : ");
            scanf("%d",&std.msv);
            gotoxy(10,10);
            printf("Nhap khoa hoc : ");
            fflush(stdin);
            gets(std.khoahoc);
            gotoxy(10,11);
            printf("Nhap chi nhanh : ");
            fflush(stdin);
            gets(std.chinhanh);
            fseek(fp ,-sizeof(std),SEEK_CUR); //vi tri hien tai cua con tro File 
            fwrite(&std,sizeof(std),1,fp);
            break;
        }
    }
    fclose(fp);
    gotoxy(10,16);
    printf("Nhan bat ki de tiep tuc.");
    getch();
    menu();
}
void xoa()
{
    char stten[20];
    FILE *fp,*ft;
    struct sinhvien std;
    system("cls");
    gotoxy(10,3);
    printf("<--:Xoa ban ghi:-->");
    gotoxy(10,5);
    printf("Nhap ten sinh vien can xoa : ");
    fflush(stdin);
    gets(stten);
    fp = fopen("record.txt","rb+");
    if(fp == NULL){
        gotoxy(10,6);
        printf("Loi khi mo tep");
        exit(1);
    }
    ft = fopen("temp.txt","wb+");
    if(ft == NULL){
        gotoxy(10,6);
        printf("Loi khi mo tep");
        exit(1);
    }
    while(fread(&std,sizeof(std),1,fp) == 1){
        if(strcmp(stten,std.ten)!=0)
            fwrite(&std,sizeof(std),1,ft);
    }
    fclose(fp);
    fclose(ft);
    remove("record.txt");
    rename("temp.txt","record.txt");
    gotoxy(10,10);
    printf("Nhan bat ki de tiep tuc.");
    getch();
    menu();
}
void gotoxy(int x,int y)
{
        COORD c; // tao cau truc coord va dien vao cac thanh vien cua no . chi dinh vi tri moi cua con tro ma chung ta dat
        c.X=x; // hang
        c.Y=y;// cot
        SetConsoleCursorPosition(GetStdHandle(STD_OUTPUT_HANDLE),c); // lay 1 xu ly vao bo dem chuong trinh console . goi ham de dong no lai , Di chuyen con tro trong bang dieu khien 
}
