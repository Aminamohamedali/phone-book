# phone-book
typedef struct{
    int day;
    int month;
    int year;
}birthdate;


typedef struct{
    char lastname[50];
    char firstname[50];
    birthdate date;
    char adress[100];
    char city[50];
    int number;
}data;

#include <stdio.h>
#include <stdlib.h>
#include "phone-book.h"
int main()
{
   FILE*pb;
   data people[6];
   int i=0;
   pb=fopen("phone-book.txt","r");
   while(!feof(pb)){
    fscanf(pb,"%[^,]",*(people+i)->lastname);
    i++;
   }
   fclose(pb);
   printf("%s",people->lastname);

    return 0;
}
#include <string.h>
int fsearch(char*str,char*s)
{   FILE*pb;
    int line_num = 1;
	int find_result = 0;
    while(!feof(pb)){
    if(strstr(str,s)!= NULL){
      printf("A match found on line: %d\n", line_num);
			find_result++;
			str++;
		}
		line_num++;
}

	if(find_result == 0) {
		printf("\nSorry, couldn't find a match.\n");
	}

	if(pb) {
		fclose(pb);
	}
   	return(0);
}

Sami,Ahmed,10-06-1989,26 Elhoreya Street,Alexandria,4876321
khaled,sara,11-08-1999,211 el max street,Alexandria,598327
attia,maram,22-12-1998,23 zezenia street,Alexandria,5303596
selim,amina,27-7-1999,21 Riad street,Alexandria,5789362
assem,Khadija,23-09-1999,75 al rondi street,Alexandria,5982067
Ali,Mohamed,22-05-2007,28 gleem street,Alexandria,5960357
Ahmed,omar,12-03-1989,35 al moez street,cairo,7852964
Ibrahim,ali,30-09-1978,66 zahran street,Aswan,986327
ali,mai,15-03-2009,20 nasir street,Alexandria,5910637
Omar,ahamed,09-07-2001,19 talaat,Alexandria,9304587
ali,Shaima,16-07-2000,21 loran,Alexandria,9632845
ibrahim,Habiba,16-03-2009,20 roushdy,Alexandria,5396217
ali,mirna,15-03-2002,18 syria street,Alexandria,9638514
#include <stdio.h>
#include <stdlib.h>
#include "phone-book.h"
int main()
{
   FILE*pb;
   data people[100];
   int i=0;
   pb=fopen("phone-book.txt","r");
while(!feof(pb)){
   fscanf(pb,"%[^,]%*c",(people+i)->lastname);
   fscanf(pb,"%[^,]%*c",(people+i)->firstname);
   fscanf(pb,"%[^-]%*c",(people+i)->date.day);
   fscanf(pb,"%[^-]%*c",(people+i)->date.month);
   fscanf(pb,"%[^,]%*c",(people+i)->date.year);
   fscanf(pb,"%[^,]%*c",(people+i)->adress);
   fscanf(pb,"%[^,]%*c",(people+i)->city);
   fscanf(pb,"%[^,]%*c",(people+i)->number);
   fscanf(pb,"\n");
   i++;
}
for(i=0;i<100;i++)
   {fscanf(pb,"%s",(people+i)->lastname);
   fscanf(pb,"%s",(people+i)->firstname);
   fscanf(pb,"%d",(people+i)->date.day);
   fscanf(pb,"%d",(people+i)->date.month);
   fscanf(pb,"%d",(people+i)->date.year);
   fscanf(pb,"%s",(people+i)->adress);
   fscanf(pb,"%s",(people+i)->city);
   fscanf(pb,"%d",(people+i)->number);}
   fclose(pb);

    return 0;
}
