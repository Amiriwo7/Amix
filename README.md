# Amix
#include <stdio.h>
#include <windows.h>
#include <time.h>
#include <conio.h>
#include <stdlib.h>
#include <math.h>
#include <string.h>

int a[20][3];
void cm();
void randloc();
void drivercode();
void gotoxy(int x, int y);
void setTextColor(int textColor,int backColor);
void sort();
void check();
void set();
void animation();
int cl(int x,int y);

struct person{
	
	char phone[15];
	char name[30];
	
};

struct car{

	int x,y;
	
	char Tpname[10];
	
	int Tpcoe; 
		
}carlist [18];

int main()
{
	
	char c;
	drivercode();
	randloc();
	while(1)
	{
		animation();
		if (_kbhit())
		{
			c = getch();
			if(c=='l')
			{
				gotoxy(0,25);
				system("pause");
			}
				
		}
		system("cls");
	}
	
		
}

void randloc()
{
	
	int i,j,x,y,z,t,temp;
	
	srand(time(0));	
	
	for(i=0;i<18;i++)
	{	
		x = rand()% 20;
		y = rand()% 8;
		a[i][0] = x;
		a[i][1] = y;
		a[i][2] = carlist[i].Tpcoe;		
		carlist[i].x = x;
		carlist[i].y = y;
	}
		
	sort();
	check();
//	set();
	
	
	
}
void drivercode()
{
	int i;
	for(i=0;i<18;i++)
	{
		carlist[i].Tpcoe = i+1;
	}
}

void cm()
{
	int i=0,j=0,k=0;
	
	for(i=0;i<20;i++)
	{
		printf(" __");	
	}
	printf(" \n");
	
	for(i=1;i<=16;i++)
	{
		if(i%2==0)
		{
			for(j=1;j<=20;j++)
			{
				printf("|__");
			}
			printf("|\n");
		}
		else
		{
			for(j=1;j<=2;j++)
			{
				for(k=1;k<=20;k++)
				{
					printf("|  ");
				}
				printf("|\n");
			}	
		}
	}	
	
}
void gotoxy(int x, int y)
{
	HANDLE consoleHandle = GetStdHandle(STD_OUTPUT_HANDLE);
	COORD cursorCoord;
	cursorCoord.X=x;
	cursorCoord.Y=y;
	SetConsoleCursorPosition(consoleHandle, cursorCoord);
}

void setTextColor(int textColor,int backColor)
{
	HANDLE consoleHandle = GetStdHandle(STD_OUTPUT_HANDLE);
	int colorAttribute = backColor << 4 | textColor;
	SetConsoleTextAttribute(consoleHandle, colorAttribute);
}

void sort()
{
	int i,j,temp;
	for(i=0;i<18;i++)
	{
		for(j=0;j<18-i-1;j++)
		{
			if(a[j+1][0]<a[j][0])
			{
				temp = a[j][0];
				a[j][0] = a[j+1][0];
				a[j+1][0] = temp;
				
				temp = a[j][1];
				a[j][1] = a[j+1][1];
				a[j+1][1] = temp;
				
				temp = a[j][2];
				a[j][2] = a[j+1][2];
				a[j+1][2] = temp;
			}
			
			else if(a[j+1][0]==a[j][0] && a[j+1][1]<a[j][1])
			{
				temp = a[j][0];
				a[j][0] = a[j+1][0];
				a[j+1][0] = temp;
				
				temp = a[j][1];
				a[j][1] = a[j+1][1];
				a[j+1][1] = temp;
				
				temp = a[j][2];
				a[j][2] = a[j+1][2];
				a[j+1][2] = temp;
			}
			
		}
	}
}

void check()
{
	int i,x,y,z;
	for(i=0;i<17;i++)
	{
		if(a[i][0]==a[i+1][0] && a[i][1]==a[i+1][1])
		{
				x = rand()%20;
				y = rand()%8;
				a[i][0] = x;
				a[i][1] = y;
				z = a[i][2];
				carlist[z-1].x = x;
				carlist[z-1].y = y;
				sort();
				check();
		}
	}
}

void set()
{
	int i,t;
	for(i=0;i<18;i++)
	{
		gotoxy((carlist[i].x*3)+1,(carlist[i].y*3)+2);
		t = carlist[i].Tpcoe;
		printf("%d",t);
	}
}


void animation()
{
	
	int i,temp,x;
	
	for(i=0;i<18;i++)
	{
		while(1)
		{
		
			x=rand()%4;
			
			if(x==0 && 0<=(carlist[i].y-1))
			{
				temp = cl(carlist[i].x,carlist[i].y-1);
				
				if(temp==1)
					i--;
					
				else if(temp==0)
				{
					carlist[i].y-=1;
					break;
				}
				break;//////////////
			}
			
			else if(x==1 && (carlist[i].x+1)<19)
			{	
				temp = cl(carlist[i].x+1,carlist[i].y);
				
				if(temp==1)
					i--;
					
				else if(temp==0)
				{
					carlist[i].x+=1;
					break;
				}
				break;//////////
			}
			
			else if(x==2 && (carlist[i].y+1)<8)
			{
				temp = cl(carlist[i].x,carlist[i].y+1);
				
				if(temp==1)
					i--;
					
				else if(temp==0)
				{
					carlist[i].y+=1;
					break;
				}
				break;///////////
			}
			
			else if(x==3 && 0<=(carlist[i].x-1))
			{
				temp = cl(carlist[i].x-1,carlist[i].y);
				
				if(temp==1)
					i--;
					
				else if(temp==0)
				{
					carlist[i].x-=1;
					break;
				}
				break;/////////////
				
			}
			
		}
		
	}
	setTextColor(7,0);
	cm();
	setTextColor(10,0);
	set();
	Sleep(800);
//	system("cls");	
}
int cl(int x,int y)
{
	int i;
	for(i=0;i<18;i++)
	{
		if(x==carlist[i].x && carlist[i].y==y)	
			return 1;
	}
	return 0;
}

