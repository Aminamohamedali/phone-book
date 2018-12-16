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
