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
{   int result = 0;
    int line=0;
    while(str[line]!='\0'){
    if(strcmp(str->lastname,s)== 0){
      printf("%s\n",str->firstname);
      printf("%s\n",str->adress);
      printf("%s\n",str->city);
      printf("%d\n",str->number);
			result++;
			str++;
			line ++;

}

	if(result == 0) {
		printf("Sorry, couldn't find a match.\n");
	}
   	return(0);
}

Sami,Ahmed,10-06-1989,26 Elhoreya Street,Alexandria,4876321
Sara,Khaled,11-08-1999,211 el max street,Alexandria,598327
Maram,attia,22-12-1998,23 zezenia street,Alexandria,5303596
Amina,selim,27-7-1999,21 Riad street,Alexandria,5789362
Khadija,assem,23-09-1999,75 al rondi street,Alexandria,5982067
Ali,Mohamed,22-05-2007,28 gleem street,Alexandria,5960357
Ahmed,omar,12-03-1989,35 al moez street,cairo,7852964
Ibrahim,ali,30-09-1978,66 zahran street,Aswan,986327
Mai,ali,15-03-2009,20 nasir street,Alexandria,5910637
Omar,ahamed,09-07-2001,19 talaat,Alexandria,9304587
Shaima,ali,16-07-2000,21 loran,Alexandria,9632845
Habiba,Ibrahim,16-03-2009,20 roushdy,Alexandria,5396217
Mirna,ali,15-03-2002,18 syria street,Alexandria,9638514


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
   fscanf(pb,"%[^-]%*d",(people+i)->date.day);
   fscanf(pb,"%[^-]%*d",(people+i)->date.month);
   fscanf(pb,"%[^,]%*d",(people+i)->date.year);
   fscanf(pb,"%[^,]%*c",(people+i)->adress);
   fscanf(pb,"%[^,]%*c",(people+i)->city);
   fscanf(pb,"%[^,]%*d",(people+i)->number);
   fscanf(pb,"\n");
   i++;
}
for(i=0;i<100;i++)
   {
   printf("%s\n",(people+i)->lastname);
   printf("%s\n",(people+i)->firstname);
   printf("%d\n",(people+i)->date.day);
   printf("%d\n",(people+i)->date.month);
   printf("%d\n",(people+i)->date.year);
   printf("%s\n",(people+i)->adress);
   printf("%s\n",(people+i)->city);
   printf("%d\n",(people+i)->number);
   }
   fclose(pb);

    return 0;
}
