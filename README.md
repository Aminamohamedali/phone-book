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

