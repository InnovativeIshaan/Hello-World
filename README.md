# Hello-World(A SIMPLE GAME IN C)

#include<stdio.h>
#include<conio.h>//keys
#include<windows.h>//cursor

void gotoxy(short col,short row)//function to position cursor
{
    HANDLE hStdout = GetStdHandle(STD_OUTPUT_HANDLE);
    COORD position = {col,row};
    SetConsoleCursorPosition(hStdout,position);
}


void boxes();
void display();
int getkey();
void check();

 int arr[4][4] =   {
                            {1,4,15,7},
                            {8,10,2,11},
                            {14,3,6,13},
                            {12,9,5,0}

                      };

int main()
{
    int row=3,col=3,t,ch;

    boxes();//function to draw boxes
    display();//function to display numbers

    while(1)
    {
        ch = getkey();//returns the scancode of the key that has been hit
        
        switch(ch)
        {
            case 80 ://down arrow
            if(row==0)//why if is used and function of "\a"
            {
                printf("\a");
                break;
            }

            t = arr[row][col];
            arr[col][row] = arr[row-1][col];
            arr[row-1][col] = t;
            row--;
            display();
            break;

            case 77 ://right arrow
            if(col==0)//why if is used and function of "\a" = alarm sound
            {
                printf("\a");
                break;
            }
            
            t = arr[row][col];
            arr[row][col] = arr[row][col-1];
            arr[row][col-1] = t;
            col--;
            display();
            break;

            case 72 ://up arrow
            if(row==3)//why if is used?
            {
                printf("\a");//PRODUCES BEEP SOUND
                break;
            }
            t = arr[row][col];
            arr[row][col] = arr[row+1][col];
            arr[row+1][col] = t;
            row++;
            display();
            break;

            case 75 ://left arrow
            if(col==3)//why if is used?
            {
                printf("\a");
                break;
            }

            t = arr[row][col];
            arr[col][row] = arr[row][col+1];
            arr[row][col+1] = t;
            display();
            break;

            case 27 : //escape key
            exit(0);
        }
        check();
    }
    return 0;
   
}

void check()
{
    static int move = 0;
    int k=1,i,j;

    move++;//?
    gotoxy(30,24);

    printf("\n number of moves  = %d",move);

    for(i=0;i<=3;i++)
    {
        for(j=0;j<=3;j++)
        {
            if(arr[i][j] == 0)// at origin
            continue;
            
            else if(arr[i][j] == k)
            k++;
            
            else
            {
                return;
            }
            
            
        }
    }
    exit(0);//brings out of void function
}


void boxes()//to draw boxes
{
    int r,c;//rows & coloumns

    for(c=30;c<=42;c++)
    {
        for(r=8;r<=16;r+=2)
        {
            gotoxy(c,r);
            printf("%c",196);//ascii value for drawing -
        }
    }


    for(r=8;r<=16;r++)
    {
        for(c=30;c<=42;c++)
        {
            gotoxy(c,r);
            printf("%c",179);//ascii value for drawing |
        }
    }


    

    for(c=33;c<=39;c += 3)
    {
        gotoxy(30,r);
        printf("%c",194);// drawing T

        gotoxy(c,16);
        printf("%c",193);//  drawing inverse T
    }


    for(r=10;r<=14;r+=2)
    {
        gotoxy(30,r);
        printf("%c",195);// drawing |-

        gotoxy(42,r);
        printf("%c",180);// drawing -|
    }

    for(r=10;r<=14;r+=2)
    {
        for(c=33;c<=39;c+=3)
        {
            gotoxy(c,r);
            printf("%c",197);//drawing CHRIST CROSS
        }
    }

    gotoxy(30,8);
    printf("%c",218);//box drawing character

    gotoxy(42,8);
    printf("%c",191);//box drawing character

    gotoxy(30,16);
    printf("%c",192);//box drawing

    gotoxy(42,16);
    printf("%c",217);//box drawing


}

void display() //display numbers in the boxes
{
    int r=9,c=31,i,j;

    for(i=0;i<=3;i++)
    {
        for(j=0;j<=3;j++)
        {
            if(arr[i][j] == 0)//why this condition is used?
            {
                gotoxy(c,r);
                printf(" ");
            }

            else
            {
                gotoxy(c,r);
                printf("%d",arr[i][j]);//print number
            }

            c = c + 3;
            
        }
        r = r + 2;
        c = 31;//why again c = 31 meintioned here?
    }
}

//RETURNS SCAN CODE OF THE KEY THAT HAS BEEN HIT,27 IF ESCAPE
int getkey()
{
    int ch;
    ch = getch();
    if(ch == 0)
    {
        ch = getch();
        return ch;
    }
}
