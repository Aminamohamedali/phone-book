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
   fscanf(pb,"%[^,]%*c",(people+i)->lastname);
   i++;
}
for(i=0;i<6;i++)
   printf("%s\n",(people+i)->lastname);
   fclose(pb);

    return 0;
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



