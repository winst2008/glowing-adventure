// tratata.cpp: определяет точку входа для консольного приложения.
//

#include "stdafx.h"
#include <conio.h>
#include <iostream>
#include <fstream>

void bubbleSort(char a[100][100],int i);
void straightSelectionSort(char b[100][100], int col);
void saveFile(char a[100][100],char b[100][100],int col);


int main()
{
  setlocale(LC_ALL, "Russian");
	l:
	system("cls");
	std::ifstream f;
	char a[100][100];
	char b[100][100];
	int i=0,j=0;
	
	char* fnamein = new char[50];
	std::cout << "Введите имя файла" << std::endl;
	std::cin >> fnamein;

	f.open(fnamein);
		while(f.good())
		{
		f >> a[i][j+1];
		j++;
		if (f.peek()=='\n')
			{
				i++;
				j=0;
			}
		if (f.eof())
			i++;
		}
		f.close();
		for (int ii=0; ii<i; ii++)
			{
				for (int jj=1; jj<j+1; jj++)
				std::cout << a[ii][jj] << '\t';
				std::cout << '\n';
			}

		for (int ii=0; ii<i; ii++)
			{
				for (int jj=1; jj<j+1; jj++)
				{
					b[ii][jj] = a[ii][jj];
				}
			}

		std::cout << std::endl << "i = "<< i <<" j = "<< j << std::endl;

		if (i!=j)
			{
			std::cout << "Error! Incorrect matrix!" << std::endl;
			_getch();
			goto l;
			}
		if (i=j)
			{
			std::cout << "Good matrix." << std::endl;
			_getch();
			}


		bubbleSort(a,i);

		std::cout << std::endl << "BubbleSort matrix: " << std::endl;
		for (int ii=0; ii<i; ii++)
			{
				for (int jj=1; jj<j+1; jj++)
				std::cout << a[ii][jj] << '\t';
				std::cout << std::endl;
			}
		_getch();
		
		straightSelectionSort(b,i);

		std::cout << std::endl << "SelectionSort matrix: " << std::endl;
		for (int ii=0; ii<i; ii++)
			{
				for (int jj=1; jj<j+1; jj++)
				std::cout << b[ii][jj] << '\t';
				std::cout << std::endl;
			}
		
		_getch();

		saveFile(a,b,i);
		 
	return 0;
}

void bubbleSort(char a[100][100], int col)
{                   
	
	int &&d1 = 0;
	int &&d2 = 0;
	int temp=0;

	for(int p=0; p<=col; p++)
	{
		for (int i=0;  i<=col  ;  i++)
			{            
				for (int j=1;  j<col-i;  j++)
				{     
					d1++;
					if (a[p][j]<a[p][j+1])
						{   
							d2++;
							temp=a[p][j];           
							a[p][j]=a[p][j+1];    
							a[p][j+1]=temp;
							
						}
				}
			}
	}
	
	std::cout  << "\n\nСортировка пузырьком\n" << d1 << " сравнений и " << d2 << " присваиваний" << "\n";
}
void straightSelectionSort(char b[100][100], int col)
{
	int c;
	int h1=0;
	int h2=0;
	char t;
	int exchange = 0;
	for(int k=0;k<col;k++)
	{
		for(int i = 0; i < col; i++)
		{
			exchange = 0;
			c = i;
			t = b[k][i];
			for(int j = i+1; j < col+1; j++)
			{
				h1++;
				if(b[k][j] < t)
				{
					
					c = j;
					t = b[k][j];
					exchange = 1;
				}
			}   
			if(exchange)
			{
				h2++;
				b[k][c] = b[k][i];
				b[k][i] = t;
			}
		} 
		
	 
	for(int i=1;i<=((col)/2);i++)
		{
		char t=b[k][i];
		b[k][i] = b[k][col-i+1];
		b[k][col-i+1] = t;
		}
	}
	std::cout << "\n\nСортировка выбором\n" << h1 << " сравнений " << h2 << " присвоений " << std::endl;
}
void saveFile(char a[100][100],char b[100][100], int col)
{
		
		char* fnameout = new char[50];
		std::cout << "Введите имя файла для сохранения"<< std::endl;
		std::cin >> fnameout;
		std::ofstream g(fnameout);
		
		g << "Матрица отсортированная обменом(пузырьком)";
		g << std::endl;

		for (int i=0; i<col; i++)
			{
				for (int j=1; j<col; j++)
				g << a[i][j] << '\t';
				g << std::endl;

			}

		g << "Матрица отсортированная выбором";
		g << std::endl;

		for (int i=0; i<col; i++)
			{
				for (int j=1; j<col; j++)
				g << b[i][j] << '\t';
				g << std::endl;

			}
}
				
