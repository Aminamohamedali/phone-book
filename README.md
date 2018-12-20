# phone-book
///////main//////
#include <stdio.h>
#include <stdlib.h>
#include "phone-book.h"

int main()
{
    int j;
    File_Load();
    File_Modify();
    for(j=0; j<members; j++)
    {
        printf("last name:%s\n",(people+j)->lastname);
        printf("first name:%s\n",(people+j)->firstname);
        printf("Date of birth:%d/",(people+j)->date.day);
        printf("%d/",(people+j)->date.month);
        printf("%d\n",(people+j)->date.year);
        printf("Address:%s\n",(people+j)->address);
        printf("E-mail:%s\n",(people+j)->mail);
        printf("phone number:%d\n\n",(people+j)->number);
    }
    return 0;
}
////////header/////////
#include <string.h>

typedef struct
{
    int day;
    int month;
    int year;
} birthdate;
typedef struct
{
    char lastname[12];
    char firstname[12];
    birthdate date;
    char address[24];
    char mail[12];
    int number;
} data;
FILE*fpb;
data people[100];
int members=0;
void File_Load()
{
    fpb=fopen("phone-book.txt","r");
    while(!feof(fpb))
    {
        fscanf(fpb,"%[^,]%*c",(people+members)->lastname);
        fscanf(fpb,"%[^,]%*c",(people+members)->firstname);
        fscanf(fpb,"%d-%d-%d,",&(people+members)->date.day,&(people+members)->date.month,&(people+members)->date.year);
        fscanf(fpb,"%[^,]%*c",(people+members)->address);
        fscanf(fpb,"%[^,]%*c",(people+members)->mail);
        fscanf(fpb,"%d\n",&(people+members)->number);
        members++;
    }
    fclose(fpb);
}
void File_Add()
{
    printf("Enter last name:");
    scanf("%s",people[members].lastname);
    printf("Enter First name:");
    scanf("%s",people[members].firstname);
    printf("Enter Date of Birth\n");
    printf("Day:");
    scanf("%d",&people[members].date.day);
    printf("Month:");
    scanf("%d",&people[members].date.month);
    printf("Year:");
    scanf("%d",&people[members].date.year);
    printf("Enter Address:");
    getchar();
    gets(people[members].address);
    printf("Enter the email:");
    gets(people[members].mail);
    printf("Enter phone number:");
    scanf("%d",&people[members].number);
    members++;
}
void File_Search()
{
    char key[12];
    int result = 0;
    int i;
    printf("Enter last name for whom you search:");
    scanf("%s",key);
    for(i=0; i<members; i++)
    {
        if(strcasecmp(people[i].lastname,key)== 0)
        {
            printf("first name:%s\n",people[i].firstname);
            printf("Address:%s\n",people[i].address);
            printf("E-mail:%s\n",people[i].mail);
            printf("phone number:%d\n\n",people[i].number);
            result++;
        }
    }
    if(result == 0)
        printf("Sorry, couldn't find a match.\n");



}
void File_Delete()
{
    int check=members;
    char last[12],first[12];
    int i=0,j;
    printf("please enter last and first name to delete data\n");
    gets(last);
    gets(first);
    for(i=0; i<members; i++)
    {
        if(strcasecmp(people[i].lastname,last)==0 && strcasecmp(people[i].firstname,first)==0)
        {
            for(j=i; j<members; j++)
                people[j]=people[j+1];
            members--;
        }
    }
    if(check==members)
        printf("no data to delete\n");


}
void File_Modify()
{
    char key[12];
    data same[8];
    int result = 0;
    int i,j=0,n;
    printf("Enter last name:");
    scanf("%s",key);
    for(i=0; i<members; i++)
    {
        if(strcasecmp(people[i].lastname,key)== 0)
        {
            same[j++]=people[i];
            printf("%d.",j);
            printf("last name:%s\n",people[i].lastname);
            printf("first name:%s\n",people[i].firstname);
            printf("Address:%s\n",people[i].address);
            printf("Date of birth:%d/",people[i].date.day);
            printf("%d/",people[i].date.month);
            printf("%d\n",people[i].date.year);
            printf("E-mail:%s\n",people[i].mail);
            printf("phone number:%d\n\n",people[i].number);
            result++;
        }
    }
    if(result == 0)
    {
        printf("Sorry, couldn't find a match.\n");
        File_Modify();
    }

    printf("Which contact do you want to edit [");
    for(i=0; i<j; i++)
        printf("%d ",i+1);
    printf("]\n");
    scanf("%d",&n);
    printf("Which field do you want to edit\n");
    printf("1.last name:%s\n",same[--n].lastname);
    printf("2.first name:%s\n",same[n].firstname);
    printf("3.Address:%s\n",same[n].address);
    printf("4.Date of birth:%d/",same[n].date.day);
    printf("%d/",same[n].date.month);
    printf("%d\n",same[n].date.year);
    printf("5.E-mail:%s\n",same[n].mail);
    printf("6.phone number:%d\n\n",same[n].number);
    scanf("%d",&j);
    for(i=0; i<members; i++)
    {
        if(same[n].number==people[i].number)
            break;
    }
    switch(j)
    {
    case(1):
        printf("Enter the new last name:");
        scanf("%s",people[i].lastname);
        break;
    case(2):
        printf("Enter the new first name:");
        scanf("%s",people[i].firstname);
        break;
    case(3):
        printf("Enter the new Address:");
        getchar();
        gets(people[i].address);
    case(4):
        printf("Enter the new Date of birth:");
        printf("Day:");
        scanf("%d",&people[i].date.day);
        printf("Month:");
        scanf("%d",&people[i].date.month);
        printf("Year:");
        scanf("%d",&people[i].date.year);
        break;
    case(5):
        printf("Enter the new E-mail:");
        getchar();
        gets(people[i].mail);
        break;
    case(6):
        printf("Enter the new number:");
        scanf("%d",&people[i].number);
    }

}
//////////

