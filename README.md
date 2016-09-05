#include<stdio.h>
#include<malloc.h>
struct node
{
    void* data;
    struct node* next;
};
typedef struct node node;
node *new_node(void* data)
{
    node* p=(node*)malloc(sizeof(node));
    p->data=data;
    p->next=NULL;
    return p;
}
void insertbeg(node **head,node **last,void *data)
{
   node *temp1=*head;

   node *temp2=*last;
   if(temp1==NULL)
   {
        node*temp=new_node(data);
        temp->next=temp;
        *head=temp;
        *last=temp;
   }
   else if(temp1!=NULL)
   {
          node*temp=new_node(data);
          temp->next=*head;
          *head=temp;
          temp2->next=temp;
          *last=temp2;
   }

}
void deleteChar(node **a,node **b ,int *j)
{
    node *temp=*a;
    node *prev=*b;
    prev->next=temp->next;
    free(temp);
    temp=NULL;
    j=0;
}
void kill(node **head,node **last,int value)
{
    node *temp=*head;
    node *temp2=*head;
    node*temp3;
    node *temp1=*last;
    int i=0;int j=1;
    node *prev;
    while(temp->next!=temp&&i<value)
    {
        if(i==value-1)
        {   printf("Killing soldier %c",temp->data);

            deleteChar(&temp,&prev,&j);
            i=0;
            printf("\nThe value of i is %d",i);
            temp=temp3;
            printf("\nThe new value of temp is %c\n",temp->data);
        }
        prev=temp;
        temp=temp->next;
        temp3=prev;
        i++;

    }

    printf("The soldier escaping is %c",temp->data);

}

void disp(node **head,node **last)
{
    node *temp=*head;
    node *temp2=*last;
        while(temp->next!=temp2->next)
    {
        printf("%c",temp->data);
        printf("\n The address is %d",temp);
        printf("\n The next is %d\n",temp->next);
        temp=temp->next;
    }
    printf("%c",temp->data);
    printf("\n The address is %d",temp);
    printf("\n The next is %d\n",temp->next);
}
int main()
{
    node *head=NULL;
    node *last=NULL;
    int m,i,n;
    char x;
    printf("Enter the number of soldiers:");
    scanf(" %d",&m);
    printf("Enter the number sequence:");
    scanf(" %d",&n);
    printf("Enter the name of the soldiers:");
    for(i=0;i<m;i++)
    {
        scanf(" %c",&x);
        insertbeg(&head,&last,x);
    }
    disp(&head,&last);
    kill(&head,&last,n);
}
