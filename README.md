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
   data people[100];
   int j=0,i=0;
   pb=fopen("phone-book.txt","r");
while(!feof(pb)){
   fscanf(pb,"%[^,]%*c",(people+i)->lastname);
   fscanf(pb,"%[^,]%*c",(people+i)->firstname);
   fscanf(pb,"%d-%d-%d,",&(people+i)->date.day,&(people+i)->date.month,&(people+i)->date.year);
   fscanf(pb,"%[^,]%*c",(people+i)->adress);
   fscanf(pb,"%[^,]%*c",(people+i)->city);
   fscanf(pb,"%d\n",&(people+i)->number);
   i++;
}
fclose(pb);
for(j=0;j<i;j++)
   {
   printf("%s\n",(people+j)->lastname);
   printf("%s\n",(people+j)->firstname);
   printf("%d\n",(people+j)->date.day);
   printf("%d\n",(people+j)->date.month);
   printf("%d\n",(people+j)->date.year);
   printf("%s\n",(people+j)->adress);
   printf("%s\n",(people+j)->city);
   printf("%d\n\n",(people+j)->number);
   }


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

