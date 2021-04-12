#include<stdio.h>
#include<stdlib.h>
#include<time.h>
#define p printf
#define s scanf
#define and &&
#define or ||
#define equ ==
#define not_equ !=
#define greater >
#define less <
#define great_equ >=
#define less_equ <=

typedef struct ToDo todo;

struct ToDo{
    int count;
    char data[50];
    todo *next;
};

todo *start= NULL;

void main(){
    int choice;
    system("pause");
    wlcScreen();
    while(1){
        system("color f0");
        system("cls");
        p("\n\n\n\n\n\n\n\n");
        p("\n\t\t\t\t\t\t 1. See your ToDo List. \n");
        p("\n\t\t\t\t\t\t 2. Create your ToDo List. \n");
        p("\n\t\t\t\t\t\t 3. Delete your ToDo List. \n");
        p("\n\t\t\t\t\t\t 4. Update your ToDo List. \n");
        p("\n\t\t\t\t\t\t 5. Exit ");
        p("\n\t\t\t\t\t\t");
        p("\n\t\t\t\t\t\t");
        p("\n\t\t\t\t\t\t Enter your choice \n\t\t\t\t\t\t --> ");
        s("%d",&choice);

        switch(choice){
        case 1:
            seeTodo();
            break;
        case 2:
            CreateTodo();
            break;
        case 3:
            DeleteTodo();
            break;
        case 4:
            updateTodo();
            break;
        case 5:
            exit(0);
        }

    }
}

void delay(int number_of_seconds){
    // Converting time into milli_seconds
    int milli_seconds = 1000 * number_of_seconds;

    // Storing start time
    clock_t start_time = clock();

    // looping till required time is not achieved
    while (clock() < start_time + milli_seconds)
        ;
}

void wlcScreen(){
    system("color f0");
    char c;
    system("cls");
    p("\n\n\n\n      ");

    c=215;
    p("\n\t\t\t\t\t         / ----- %c%c%c%c%c ----- \\",c,c,c,c,c);
    p("\n\t\t\t\t\t        /                     \\");
    p("\n\t\t\t\t\t       /                       \\");
    p("\n\t\t\t\t\t      /                         \\");
    p("\n\n");


    // first line
    p("\t\t\t\t\t%c%c%c%c%c%c",c=176,c=176,c=177,c=177,c=178,c=178);
    p("\t\t\t\t %c%c%c%c%c%c",c=178,c=178,c=177,c=177,c=176,c=176);
    p("\n\n\t       ");


    // second line
    // diamonds
    c=4;
    for(int i=0; i<10; i++){
        p("-%c",c);
    }
    // heart
    c=3;
    for(int i=0; i<5; i++){
        p("--%c",c);
    }

    p("    %cl %c  l l %c    ",c=195,c=137,c=153);




    // heart
    c=3;
    for(int i=0; i<4; i++){
        p("%c--",c);
    }

    p("%c-",c);
   // diamonds
    c=4;
    for(int i=0; i<10; i++){
        p("-%c",c);
    }
    p("-\n");

    // third line
    c=157;
    p("\n\t\t\t   ------ %c ------\t\t\t\t    ------ %c ------",c,c);


    // fourth line
    c=153;
    p("\n\t\t\t\t\t\t\t   %c",c);


    // fifth line
    c=240;
    p("\n\t\t\t\t\t\t\t ");
    for(int i=0; i<5; i++){
        p("%c",c);
    }

    // sixth line
    c=194;
    p("\n\t\t\t\t\t\t\t   %c",c);

    // seventh line
    p("\n\t\t\t\t\t\t\t   |");

    // eighth line
    p("\n\t\t\t\t\t\t\t   |");

    // ninth line
    p("\n\t\t\t\t\t\t\t   |");

    // tenth line
    p("\n\t\t\t\t\t\t\t   |");


    while(1){
        int i=0;
        system("color f1");
        delay(1);
        system("color f2");
        delay(1);
        system("color f4");
        delay(1);
        system("color f0");
        delay(1);
        i++;
        if(i equ 1){
            break;
        }

    }



    //p("\n\n\n\n\n");
    p("\n\n\n\t\t\t\t\t      ");
    system("pause");
}

void seeTodo(){
    system("cls");
    todo *temp;
    temp = start;
    if(start equ NULL)
    {
        p("\n\t\t\t\t\t\t Empty list");
    }
    else
    {
        while(temp not_equ NULL)
        {
            p("\n\t\t\t\t\t\t %d . ",temp->count);
            puts(temp->data);
            fflush(stdin);
            temp= temp->next;
        }
    }
    p("\n\t\t\t\t\t\t");
    system("pause");

}

void CreateTodo(){

    char a;
    todo *ptr , *ptr2;
    system("cls");
    while(1){
        p("\n\t\t\t\t\t\t Want to add? y/n \n\t\t\t\t\t\t -->");
        fflush(stdin);
        s("%c",&a);
        if(a equ 'n')
        {
            break;
        }
        else
        {
            if(start equ NULL)
            {
                ptr = (todo *)calloc(1,sizeof(todo));
                start = ptr;
                p("\n\t\t\t\t\t\t Write 1st list here \n\t\t\t\t\t\t --> ");
                fflush(stdin);
                gets(ptr->data);
                ptr->count = 1;
                start->next = NULL;
            }
            else
            {
                ptr2 = (todo *)calloc(1, sizeof(todo));
                p("\n\t\t\t\t\t\t Write another list here \n\t\t\t\t\t\t --> ");
                fflush(stdin);
                gets(ptr2->data);

                ptr2->next=NULL;
                ptr->next = ptr2;
                ptr = ptr->next; //just like i++ for increment
            }
            fixcount();
        }
    }


}

void fixcount(){
    todo *ptr;
    int i=1;
    ptr = start;
    while(ptr not_equ NULL)
    {
        ptr->count = i;
        i++;
        ptr= ptr->next;
    }
}

void DeleteTodo(){
    system("cls");
    int a;
    todo *ptr,*ptr1;   // points to starting list
     // points to next list for tracing
    p("\n\t\t\t\t\t\t Enter the number you want to delete \n\t\t\t\t\t\t --> ");
    s("%d",&a);

    ptr = start;
    ptr1 = start->next;
    while(1)
    {
        // first condition
        // if we want to delete fist node
        if(ptr->count equ a)
        {
            start=start->next;
            free(ptr);
            fixcount();
            break;
        }
        // second condition
        // if we want to delete other node
        if(ptr1->count equ a)
        {
            ptr->next=ptr1->next;
            free(ptr1);
            fixcount();
            break;
        }
        else
        {
            ptr = ptr1;
            ptr1 = ptr1->next;
        }

    }
    //system("pause");
}

void updateTodo(){
    system("cls");
    todo *ptr, *ptr1;
    char a;
    while(1)
    {
        p("\n\t\t\t\t\t\t Want to add ? y/n \n\t\t\t\t\t\t --> ");
        fflush(stdin);
        s("%c",&a);
        if(a equ 'n')
        {
            break;
        }
        p("\n\t\t\t\t\t\t Write here \n\t\t\t\t\t\t -->");
        ptr = (todo *)calloc(1, sizeof(todo));
        fflush(stdin);
        gets(ptr->data);
        ptr->next = NULL;
        ptr1 = start;
        while(ptr1->next not_equ NULL)
        {
            ptr1=ptr1->next;
        }
        ptr1->next=ptr;
        fixcount();
    }
    p("\n\t\t\t\t\t\t");
    //system("pause");
}



































