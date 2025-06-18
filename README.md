# doublelinklist
#include<stdio.h>
#include<stdlib.h>
void append();
void display();
int length();
void insert_at_begain();
void insert_at_any_position();
void delet_at_begain();
void delet_at_any_position();
void delet_at_end();
struct node
{
	struct node* leftlink;
	int data;
	struct node* rightlink;
};
struct node* root=NULL;
int main()
{
	int n;
	while(1)
	{
		printf("Press 1 to Append:\n");
		printf("Press 2 to Display:\n");
		printf("Press 3 to Length:\n");
		printf("Press 4 to Exit:\n");
		printf("Press 5 to Insert_at_begain:\n");
		printf("Press 6 to Insert_at_any_position:\n");
		printf("Press 7 to Delet_at_begain:\n");
		printf("press 8 to Delet_at_any_position:\n");
		printf("Press 9 to Delet_at_end:\n");
		scanf("%d",&n);
		switch(n)
		{
			case 1:
				append();
				break;
			case 2:
				display();
				break;
			case 3:
				printf("Lenght:%d\n",length());
				break;
			case 4:
				exit(0);
			case 5:
				insert_at_begain();
				break;
			case 6:
				insert_at_any_position();
				break;
			case 7:
				delet_at_begain();
				break;
			case 8:
				delet_at_any_position();
				break;
			case 9:
				delet_at_end();
				break;
			default:
				printf("Enter a valid position:\n");
		}
	}
	return 0;
}
void append()
{
	int a;
	struct node* temp=NULL,*p=root;
	temp=(struct node*)malloc(sizeof(struct node));
	printf("\n Enter a number:");
	scanf("%d",&a);
	temp->leftlink=NULL;
	temp->data=a;
	temp->rightlink=NULL;
	if(root==NULL)
	{
		root=temp;
	}
	else
	{
		while(p->rightlink != NULL)
		{
			p=p->rightlink;
		}
		p->rightlink=temp;
		temp->leftlink=p;
	}
}
void display()
{
	struct node* d=root;
	if(root==NULL)
	{
		printf("Linked is empty:\n");
	}
	else{
		while(d->rightlink != NULL)
		{
			printf("%d ",d->data);
			d=d->rightlink;
		}
		printf("%d ",d->data);
	}
	printf("\n");
}
int length()
{
	int count=0;
	struct node *p=root;
	if(p==NULL)
	printf("Length not count/n");
	else{
		while(p!=NULL)
		{
			count++;
			p=p->rightlink;
		}
		return count;
	}
}
void insert_at_begain()
{
	int a;
	struct node* temp=NULL;
	temp=(struct node*)malloc(sizeof(struct node));
	printf("Insert a number:");
	scanf("%d ",&a);
	temp->data=a;
	temp->rightlink=root;
	root->leftlink=temp;
	root=temp;
	printf("\n");
}
void insert_at_any_position()
{
	int pos,n,i;
	struct node* p=root;
	struct node* temp=NULL;
	temp=(struct node*)malloc(sizeof(struct node));
	printf("Insert a number:");
	scanf("%d ",&n);
	temp->leftlink=NULL;
	temp->data=n;
	temp->rightlink=NULL;
	printf("\nEnter insert position number:");
	scanf("%d ",&pos);
	if(pos>=1&&pos<=length())
	{
		i=1;
		while(i<pos-1)
		{
			p=p->rightlink;
			i++;
		}
		temp->rightlink=p->rightlink;
		temp->leftlink=p->leftlink;
		p->rightlink=temp;
	}
}
void delet_at_begain()
{
	struct node* p=root;
	root=p->rightlink;
	p->rightlink->leftlink=NULL;
	p->rightlink=NULL;
	free(p);
}
void delet_at_any_position()
{
	int pos,i=1;
	struct node* p=root;
	struct node* q=root;
	printf("Enter delet position:");
	scanf("%d",&pos);
	if(pos>=1&&pos<=length())
	{
		while(i<pos)
		{
			p=q;
			q=q->rightlink;
			i++;
		}
		p->rightlink=q->rightlink;
		q->rightlink->leftlink=q->leftlink;
		q->rightlink=NULL;
		q->leftlink=NULL;
		free(q);
	}
}
void delet_at_end()
{
	struct node* p=root;
	struct node* q=root;
	if(p->rightlink!=NULL)
	{
		q=p;
		p=p->rightlink;
	}
	p->leftlink=NULL;
	q->rightlink=NULL;
	free(p);
}
