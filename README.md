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
#iclude <string.h>
fsearch(char*str,char*s)
{   FILE*pb;
    int line_num = 1;
	int find_result = 0;
    while(!feof(pb)){
    if(strstr(str,s)!= NUll){
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
