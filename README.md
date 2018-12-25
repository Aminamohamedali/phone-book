#include <stdio.h>
#include <stdlib.h>
#include "phone-book.h"

int main()
{
    int x=0,y=0;
    File_Load();
    printf("Welcome to your phone book\n   what do you want to do?\n ");
    while(1)
    {
        if(x!=0)
            printf("What do you want to do Next?\n ");
        printf("1.Search for a contact\n 2.Add new contact\n 3.Delete existing contact\n 4.Modify existing contact\n 5.Print the entire dictionary\n ");
        if(x!=0)
            printf("6.Save modification\n 7.Quit\n");
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
            File_Quit(y);

        }


    }

    return 0;
}



////////header1 validation.h/////////

typedef struct
{
    char day[4];
    char month[4];
    char year[8];
} birthdate;
typedef struct
{
    char lastname[12];
    char firstname[12];
    birthdate date;
    char address[24];
    char mail[32];
    char number[8];
} data;
FILE*fpb;
data people[100];
int members=0;


int NameValidation(char x[])
{
    int i;
    for(i=0; i<strlen(x); i++)
    {
        if(x[i]>48&&x[i]<57)
            return 0;
    }
    return 1;
}
int DayValidation(char x[])
{
    if (strlen(x)>2||((strlen(x)==2)&&x[0]>51)||(x[0]==51&&x[1]>49))
        return 0;
    return 1;
}
int MonthValidation(char x[])
{
    if (strlen(x)>2||((strlen(x)==2)&&x[0]>49)||(x[0]==49&&x[1]>50))
        return 0;
    return 1;
}
int yearValidation(char x[])
{
    if (strlen(x)!=4||x[0]>50||(x[0]==49&&x[1]<57)||(x[0]==50&&(x[1]>48||x[2]>49||x[3]>56)))
        return 0;
    return 1;
}
int NumberValidation(char x[])
{
    int i;
    if (strlen(x)!=7)
        return 0;
    for(i=0; i<7; i++)
    {
        if(x[i]<48||x[i]>57)
            return 0;
    }
    return 1;
}
int Emailvalidation(char x[])
{
    int i,len,j,flag,m;
    int check;
    j=m=flag=check=0;
    len=strlen(x);
    char b[35];
    if(strstr(x," ")!=NULL)
        return 0;
    for(i=0; i<len; i++)
    {
        if(x[i]=='@')
        {
            for(; i<len; i++)
            {
                b[j]=x[i+1];
                j++;
            }
            check++;}
    }
    if(check==1)
    {
        for(i=0; i<j; i++)
        {
            if(b[i]=='.')
            {
                for(; i<j-1; i++)
                {
                    if(b[i+1]!='.')
                    {
                        m++;
                    }
                    else if(b[i+1]=='.')
                    {

                        return 0;
                        flag =1;
                        break;
                    }
                }
            }
        }
        if(m<3&&flag==0)
            return 0;
        else
            return 1;
    }
    else
    return 0;
}
void Print_data(int j)
{
        printf("last name:%s\n",(people+j)->lastname);
        printf("first name:%s\n",(people+j)->firstname);
        printf("Date of birth:%s/",(people+j)->date.day);
        printf("%s/",(people+j)->date.month);
        printf("%s\n",(people+j)->date.year);
        printf("Address:%s\n",(people+j)->address);
        printf("E-mail:%s\n",(people+j)->mail);
        printf("phone number:%s\n\n",(people+j)->number);
}



////////header2 phone-book.h/////////
#include <string.h>
#include "validation.h"

void File_Load()
{
    fpb=fopen("phone-book.txt","r");
    while(!feof(fpb))
    {
        fscanf(fpb,"%[^,],",people[members].lastname);
        fscanf(fpb,"%[^,],",people[members].firstname);
        fscanf(fpb,"%[^-]-",people[members].date.day);
        fscanf(fpb,"%[^-]-",people[members].date.month);
        fscanf(fpb,"%[^,],",people[members].date.year);
        fscanf(fpb,"%[^,],",people[members].address);
        fscanf(fpb,"%[^,],",people[members].mail);
        fscanf(fpb,"%s\n",people[members].number);
        members++;
    }
    fclose(fpb);

}
void File_Add()
{
    int temp=0;
    printf("Enter last name:");
    while(1)
    {
        scanf("%s",people[members].lastname);
        temp=NameValidation(people[members].lastname);
        if(!temp)
            printf("Not valid \nplease enter correct Name\n");
        else
            break;
    }
    printf("Enter First name:");
    while(1)
    {
        scanf("%s",people[members].firstname);
        temp=NameValidation(people[members].firstname);
        if(!temp)
            printf("Not valid \nplease enter correct Name\n");
        else
            break;
    }

    printf("Enter Date of Birth\n");
    printf("Day:");
    while(1)
    {
        scanf("%s",people[members].date.day);
        temp=DayValidation(people[members].date.day);
        if(!temp)
            printf("Not valid \nplease enter correct day between[1~31]\n ");
        else
            break;
    }
    printf("Month:");
    while(1)
    {
        scanf("%s",people[members].date.month);
        temp=MonthValidation(people[members].date.month);
        if(!temp)
            printf("Not valid \nplease enter correct month between[1~12]\n ");
        else
            break;
    }
    printf("Year:");
    while(1)
    {
        scanf("%s",people[members].date.year);
        temp=yearValidation(people[members].date.year);
        if(!temp)
            printf("Not valid \nplease enter correct year between[1900~2018]\n ");
        else
            break;
    }
    printf("Enter Address:");
    getchar();
    gets(people[members].address);
    printf("Enter the email:");
    while(1)
    {
        gets(people[members].mail);
        temp=Emailvalidation(people[members].mail);
        if(!temp)
            printf("Not valid \nplease enter correct E-mail format\n ");
        else
            break;
    }
    printf("Enter phone number:");
    while(1)
    {
        scanf("%s",people[members].number);
        temp=NumberValidation(people[members].number);
        if(!temp)
            printf("Not valid \nplease enter correct number\n");
        else
            break;
    }
    members++;
}
void File_Search()
{
    char key1[12],key2[4],key3[4],key4[8],key5[12],key6[12],key7[12],key8[12];
    int result = 0;
    int i;
    getchar();
    printf("1.Lastname:");
    gets(key1);
    printf("2.Firstname:");
    gets(key2);
    printf("3.Date of birth:\n");
    printf("Day:");
    gets(key3);
    printf("Month:");
    gets(key4);
    printf("year:");
    gets(key5);
    printf("4.Address:");
    gets(key6);
    printf("5.E-mail:");
    gets(key7);
    printf("6.Number:");
    gets(key8);
    printf("\n");
    for(i=0; i<members; i++)
    {
        if((strcmp(key1,"")==0)||strcasecmp(people[i].lastname,key1)== 0)
        {
            if((strcmp(key2,"")==0)||(strcasecmp(people[i].firstname,key2)== 0))
            {
                if((strcmp(key3,"")==0)||(strcasecmp(people[i].date.day,key3)== 0))
                {
                    if((strcmp(key4,"")==0)||(strcasecmp(people[i].date.month,key4)== 0))
                    {
                        if((strcmp(key5,"")==0)||((strcasecmp(people[i].date.year,key5)== 0)))
                        {
                            if((strcmp(key6,"")==0)||(strstr(people[i].address,key6)!=NULL))
                            {
                                if((strcmp(key7,"")==0)||(strcasecmp(people[i].mail,key7)== 0))
                                {
                                    if((strcmp(key8,"")==0)||(strcasecmp(people[i].number,key8)== 0))
                                    {
                                        Print_data(i);
                                        result++;
                                    }
                                }
                            }
                        }
                    }
                }
            }
        }
    }
    if(result==0)
        printf("Sorry couldn't find a match\n\n");
}

void File_Delete()
{
    int check=members;
    char last[12],first[12];
    int i=0,j;
    printf("please enter last and first name to delete data\n");
    getchar();
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
        printf("no data to delete\n\n");


}
void File_Modify()
{
    char key[12];
    data same[8];
    int result = 0;
    int i,j=0,n,temp=0;
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
            printf("Date of birth:%s/",people[i].date.day);
            printf("%s/",people[i].date.month);
            printf("%s\n",people[i].date.year);
            printf("E-mail:%s\n",people[i].mail);
            printf("phone number:%s\n\n",people[i].number);
            result++;
        }
    }
    if(result == 0)
    {
        printf("Sorry, couldn't find a match.\n\n");
        File_Modify();
    }

    if(j>1)
    {
        printf("Which contact do you want to edit [");
        for(i=0; i<j; i++)
            printf("%d ",i+1);
        printf("]\n");
        scanf("%d",&n);
    }
    else
        n=1;
    printf("Which field do you want to edit\n");
    printf("1.last name:%s\n",same[--n].lastname);
    printf("2.first name:%s\n",same[n].firstname);
    printf("3.Address:%s\n",same[n].address);
    printf("4.Date of birth:%s/",same[n].date.day);
    printf("%s/",same[n].date.month);
    printf("%s\n",same[n].date.year);
    printf("5.E-mail:%s\n",same[n].mail);
    printf("6.phone number:%s\n\n",same[n].number);
    scanf("%d",&j);
    for(i=0; i<members; i++)
    {
        if(strcmp(same[n].number,people[i].number)==0)
            break;
    }
    switch(j)
    {
    case(1):
        printf("Enter the new last name:");
        while(1)
        {
            scanf("%s",people[i].lastname);
            temp=NameValidation(people[i].lastname);
            if(!temp)
                printf("Not valid \nplease enter correct Name\n");
            else
                break;
        }
        break;
    case(2):
        printf("Enter the new first name:");
        while(1)
        {
            scanf("%s",people[i].firstname);
            temp=NameValidation(people[i].firstname);
            if(!temp)
                printf("Not valid \nplease enter correct Name\n");
            else
                break;
        }
        break;
    case(3):
        printf("Enter the new Address:");
        getchar();
        gets(people[i].address);
        break;
    case(4):
        printf("Enter the new Date of birth:");
        printf("Day:");
        while(1)
        {
            scanf("%s",people[i].date.day);
            temp=DayValidation(people[i].date.day);
            if(!temp)
                printf("Not valid \nplease enter correct day between[1~31]\n ");
            else
                break;
        }
        printf("Month:");
        while(1)
        {
            scanf("%s",people[i].date.month);
            temp=MonthValidation(people[i].date.month);
            if(!temp)
                printf("Not valid \nplease enter correct month between[1~12]\n ");
            else
                break;
        }
        printf("Year:");
        while(1)
        {
            scanf("%s",people[i].date.year);
            temp=yearValidation(people[i].date.year);
            if(!temp)
                printf("Not valid \nplease enter correct year between[1900~2018]\n ");
            else
                break;
        }
        break;
    case(5):
        printf("Enter the new E-mail:");
        getchar();
        gets(people[i].mail);
        break;
    case(6):
        printf("Enter the new number:");
        while(1)
        {
            scanf("%s",people[i].number);
            temp=NumberValidation(people[i].number);
            if(!temp)
                printf("Not valid \nplease enter correct number\n");
            else
                break;
        }

    }

}
void File_Sort()
{
    int x;
    printf("Do you want to sort by\n 1.last name\n 2.date of birth\n ");
    scanf("%d",&x);
    int sorted;
    data temp;
    int i;
    if(x==1)
    {
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
                else if(strcasecmp(people[i].lastname,people[i+1].lastname)==0&&strcasecmp(people[i].firstname,people[i+1].firstname)==0&&strcasecmp(people[i].number,people[i+1].number)>0)
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
    else if(x==2)
    {
        while(1)
        {
            sorted=0;
            for(i=0; i<members-1; i++)
            {
                if(strcasecmp(people[i].date.year,people[i+1].date.year)>0)
                {
                    temp=people[i];
                    people[i]=people[i+1];
                    people[i+1]=temp;
                    sorted=1;
                }
                else if(strcasecmp(people[i].date.year,people[i+1].date.year)==0&&(strcasecmp(people[i].date.month,people[i+1].date.month)>0))
                {
                    temp=people[i];
                    people[i]=people[i+1];
                    people[i+1]=temp;
                    sorted=1;
                }
                else if(strcasecmp(people[i].date.year,people[i+1].date.year)==0&&(strcasecmp(people[i].date.month,people[i+1].date.month)==0)&&(strcasecmp(people[i].date.day,people[i+1].date.day)>0))
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
}
void File_Print()
{
    File_Sort();
    int j;
    for(j=0; j<members; j++)
    {
        printf("last name:%s\n",(people+j)->lastname);
        printf("first name:%s\n",(people+j)->firstname);
        printf("Date of birth:%s/",(people+j)->date.day);
        printf("%s/",(people+j)->date.month);
        printf("%s\n",(people+j)->date.year);
        printf("Address:%s\n",(people+j)->address);
        printf("E-mail:%s\n",(people+j)->mail);
        printf("phone number:%s\n\n",(people+j)->number);
    }

}
void File_Save()
{
    int i;
    File_Sort();
    fpb=fopen("phone-book2.txt","w");
    for(i=0; i<members; i++)
    {
        fprintf(fpb,"%s,",people[i].lastname);
        fprintf(fpb,"%s,",people[i].firstname);
        fprintf(fpb,"%s-",people[i].date.day);
        fprintf(fpb,"%s-",people[i].date.month);
        fprintf(fpb,"%s,",people[i].date.year);
        fprintf(fpb,"%s,",people[i].address);
        fprintf(fpb,"%s,",people[i].mail);
        fprintf(fpb,"%s\n",people[i].number);

    }
    fclose(fpb);
}
void File_Quit(int y)
{
    char temp[4];
    if(y==2||y==3||y==4)
    {
        printf(" WARNING \"All your changes would be discarded Are you sure you want to Quit\"[yes no]\n");
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

/////////
phone-book.txt

Sami,Ahmed,10-06-1989,26 elhoreya street-Alexandria,ahmed_sami45@yahoo.com,4876321
Khaled,Sara,11-08-1999,211 el max street-Alexandria,sara.khaled99@yahoo.com,598327
attia,Maram,22-12-1998,23 zezenia street-Alexandria,maram.ali.attia@gmail.com,5303596
selim,Amina,27-07-1999,21 riad street-Alexandria,Amina.mohamed.ali@gmail.com,5789362
assem,khadija,23-09-1999,75 al rondi street-Alexandria,khadija_Assem99@gmail.com,5982067
Ali,Mohamed,22-05-2007,28 gleem street-Cairo,mohamed.ali35@alexu.edu,5960357
Ahmed,omar,12-03-1989,35 al moez street-Cairo,omar.ahmed1989@hotmail.com,7852964
Ibrahim,ali,30-09-1978,66 zahran street-Aswan,ibrahim.ali78@gmail.com,986327
ali,Mai,15-03-2009,20 nasir street-Alexandria,mai-ali20@yahoo.com,5910637
Omar,ahmed,09-07-2001,19 talaat-Alexandria,,ahmed.omar@ieee.org,9304587
ali,shimaa,16-07-2000,21 loran-Alexandria,shimaa_Ahmed2000@gmail.com,9632845
Habiba,Ibrahim,16-03-2009,20 roushdy-Alexandria,habibaIbrahim@yahoo.com,5396217
Ziad,Mirna,15-03-2002,18 syria street-Alexandria,mirna-ziad02@gmail.com,9638514
Sami,Ahmed,06-10-1999,26 elhoreya street-Alexandria,Ahmed.sami99@gmail.com,5986267
Ahmed,ayman,12-03-1989,35 al moez street-cairo,ayman_ahmed89@gmail.com,7596324

//////phone-book2.txt




