# phone-book
////////header
#include <string.h>
typedef struct
{
    int day;
    int month;
    int year;
} birthdate;


typedef struct
{
    char lastname[50];
    char firstname[50];
    birthdate date;
    char adress[100];
    char city[50];
    int number;
} data;
int File_Load(FILE*fp,data people[])
{
    int i=0;
    fp=fopen("phone-book.txt","r");
    while(!feof(fp))
    {
        fscanf(fp,"%[^,]%*c",(people+i)->lastname);
        fscanf(fp,"%[^,]%*c",(people+i)->firstname);
        fscanf(fp,"%d-%d-%d,",&(people+i)->date.day,&(people+i)->date.month,&(people+i)->date.year);
        fscanf(fp,"%[^,]%*c",(people+i)->adress);
        fscanf(fp,"%[^,]%*c",(people+i)->city);
        fscanf(fp,"%d\n",&(people+i)->number);
        i++;
    }
    fclose(fp);
    return i;
}
void File_Add(FILE*fp)
{
    char temp[100];
    fp=fopen("phone-book.txt","a");
    printf("Enter last name:");
    scanf("%s",temp);
    fprintf(fp,temp);
    fprintf(fp,",");
    printf("Enter First name:");
    scanf("%s",temp);
    fprintf(fp,temp);
    fprintf(fp,",");
    printf("Enter Date of Birth\n");
    printf("Day:");
    scanf("%s",temp);
    fprintf(fp,temp);
    fprintf(fp,"-");
    printf("Month:");
    scanf("%s",temp);
    fprintf(fp,temp);
    fprintf(fp,"-");
    printf("Year:");
    scanf("%s",temp);
    getchar();
    fprintf(fp,temp);
    fprintf(fp,",");
    printf("Enter Address:");
    gets(temp);
    fprintf(fp,temp);
    fprintf(fp,",");
    printf("Enter phone number:");
    scanf("%s",temp);
    fprintf(fp,temp);
    fprintf(fp,"\n");

}
//////////

#include <stdio.h>
#include <stdlib.h>
#include "phone-book.h"
int main()
{
    FILE*pb;
    data people[100];
    int members,j;
    members=File_Load(pb,people);
    for(j=0; j<members; j++)
    {
        printf("last name:%s\n",(people+j)->lastname);
        printf("first name:%s\n",(people+j)->firstname);
        printf("Date of birth:%d/",(people+j)->date.day);
        printf("%d/",(people+j)->date.month);
        printf("%d\n",(people+j)->date.year);
        printf("Address:%s\n",(people+j)->adress);
        printf("City:%s\n",(people+j)->city);
        printf("phone number:%d\n\n",(people+j)->number);
    }
    File_Add(pb);
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


void file_delete(data people[],int l){
    char last[50],first[50];
    int i=0;
    printf("please enter last and first name to delete data\n");
    gets(last);
    gets(first);
    for(i=0;i<l;i++){
          if(strcmp(people[i].lastname,last)==0 && strcmp(people[i].firstname,first)==0){
                    break;}
          }
          if(i==l)
            printf("no data to delete\n");
        for(;i<l;i++)
            people[i]=people[i+1];


}
