# dsa
#include <stdio.h>
#include <stdlib.h>


struct Node
{
	int data;
	struct Node* next;
};


void printList(struct Node* head)
{
	struct Node* ptr = head;
	while (ptr)
	{
		printf("%d —> ", ptr->data);
		ptr = ptr->next;
	}

	printf("NULL");
}


void push(struct Node** head, int data)
{
	struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
	newNode->data = data;
	newNode->next = *head;
	*head = newNode;
}


int findLength(struct Node* head)
{
	int count = 0;
	struct Node* current = head;
	while (current != NULL)
	{
		count++;
		current=current->next;
	}
	return count;
}


void frontBackSplit(struct Node* source, struct Node** frontRef, struct Node** backRef)
{
	int len = findLength(source);
	if (len < 2)
	{
		*frontRef = source;
		*backRef = NULL;
		return;
	}

	struct Node* current = source;
int i;
	int hopCount = (len - 1) / 2;	

	for (i = 0; i < hopCount; i++) {
		current = current->next;
	}


	*frontRef = source;
	*backRef = current->next;
	current->next = NULL;
}

int main(void)
{

	int keys[] = {2,3,5,7,11};
	int n = sizeof(keys)/sizeof(keys[0]);
if(n<2)
{ printf("the list cannot be broken");
}
else{
	
	struct Node* head = NULL;

	
	for (int i = n-1; i >= 0; i--) {
		push(&head, keys[i]);
	}

	struct Node *a = NULL, *b = NULL;
	frontBackSplit(head, &a, &b);

	
	printf("1st List is: ");
	printList(a);

	printf("\n2nd List is: ");
	printList(b);

	return 0;
}
}
