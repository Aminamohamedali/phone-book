#include <stdio.h>
#include <stdlib.h>
#include "phone-book.h"

int main()
{
    int x=0,y=0;
    char temp[4];
    File_Load();
    printf("Welcome to your phone book\n   what do you want to do?\n ");
    while(1)
    {
        if(x!=0)
            printf("What do you want to do Next?\n ");
        printf("1.Search for a contact\n 2.Add new contact\n 3.Delete existing contact\n 4.Modify existing contact\n 5.Print the entire dictionary\n ");
        if(x!=0)
            printf("6.Save modification\n 7.Exit\n");
        scanf("%d",&x);
        switch(x)
        {
        case(1):
            File_Search();
            break;
        case(2):
            File_Add();
            y=2;
            break;
        case(3):
            File_Delete();
            y=3;
            break;
        case(4):
            File_Modify();
            y=4;
            break;
        case(5):
            File_Print();
            break;
        case(6):
            File_Save();
            exit(1);
        case(7):
            if(y==2||y==3||y==4)
            {
                printf(" WARNING \"All your changes would be discarded Are you sure you want to exit\"[yes no]\n");
                scanf("%s",temp);
                if(strcasecmp(temp,"no")==0)
                {
                    printf("Do you want to save?[yes no]\n");
                    scanf("%s",temp);
                    if(strcasecmp(temp,"yes")==0)
                        File_Save();
                    exit(1);
                }
            }
            exit(1);

        }
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

void File_sort()
{

    int sorted;
    data temp;
    int i;
    while(1)
    {
        sorted=0;
        for(i=0; i<members-1; i++)
        {
            if(strcasecmp(people[i].lastname,people[i+1].lastname)>0)
            {
                temp=people[i];
                people[i]=people[i+1];
                people[i+1]=temp;
                sorted=1;
            }
            else if(strcasecmp(people[i].lastname,people[i+1].lastname)==0&&strcasecmp(people[i].firstname,people[i+1].firstname)>0)
            {
                temp=people[i];
                people[i]=people[i+1];
                people[i+1]=temp;
                sorted=1;
            }
            else if(strcasecmp(people[i].lastname,people[i+1].lastname)==0&&strcasecmp(people[i].firstname,people[i+1].firstname)==0&&people[i].number>people[i+1].number)
            {
                temp=people[i];
                people[i]=people[i+1];
                people[i+1]=temp;
                sorted=1;
            }
        }
        if(sorted==0)
            break;
    }
}

void File_Print()
{
    File_Sort();
    int j;
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

}
void File_Save()
{
    int i=members-10;
    File_Sort();
    fpb=fopen("phone-book2.txt","w");
    for(i=0; i<members; i++)
    {
        fprintf(fpb,"%s",people[i].lastname);
        fprintf(fpb,",");
        fprintf(fpb,"%s",people[i].firstname);
        fprintf(fpb,",");
        fprintf(fpb,"%d",people[i].date.day);
        fprintf(fpb,"-");
        fprintf(fpb,"%d",people[i].date.month);
        fprintf(fpb,"-");
        fprintf(fpb,"%d",people[i].date.year);
        fprintf(fpb,",");
        fprintf(fpb,"%s",people[i].address);
        fprintf(fpb,",");
        fprintf(fpb,"%s",people[i].mail);
        fprintf(fpb,",");
        fprintf(fpb,"%d",people[i].number);
        fprintf(fpb,"\n");
    }
    fclose(fpb);
}
//////////



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
Sami,Ahmed,10-06-1989,26 Elhoreya Street,Alexandria,5986267
Ahmed,ayman,12-03-1989,35 al moez street,cairo,7596324



