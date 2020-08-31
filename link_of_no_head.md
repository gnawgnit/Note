## 链表基本操作（无头节点且排序）

### 1. 插入

```c
/*
**链表的插入
*/
int insert(register Node **linkp, int new_value)
{
	register Node *current;
	register Node *new;
	
	current = *linkp;
	while(current != NULL && current->value < new_value)
	{
		linkp = &current->link;
		current = *linkp;
	}
	
	new = (Node *)malloc(sizeof(Node));
	if(new == NULL)
		return false;
	new->value = new_value;
	
	new->link = current;
	*linkp = new;//
	
	return ture;
}
```

### 2.删除

```c
/*
**删除链表（删除链表尾部）
*/
int delete(Node **linkp, int value)
{
	Node *current;
	Node *precious = NULL;
	//找到链表尾部或找到删除值
	current = *linkp;
	
	while(current->link != NULL && current->value != value)
	{
		precious = current;
		current = current->link;
	}
	//没有找到
	if(current->link == NULL && current->value != value)
		printf("end but not find the value!");
	//特殊情况：删除首链
	else if(current->value == value && precious == NULL)
	{
		*linkp = current->link;
	}
	else
	{
		precious->link = current->link;
	}
	
	return ture;
}
```

### 3.反序

```c
//反序
int reserve(Node **linkp)
{
	Node *tem = NULL;
	Node *pre = NULL;
	
	if(linkp == NULL)
		return false;
	if(*linkp == NULL)
		return false;
	
	tem = *linkp;
	
	while(tem->link != NULL)
	{
		pre = tem->link;
		tem->link = pre->link;
		pre->link = *linkp;
		*linkp = pre;
	}
	
	return ture;
	
	
}

```

### 4.查找

```c
/*
**查找链表成员
*/
Node* find(Node **linkp, int value)
{
	Node *current;
	current = *linkp;
	
	while(current->link != NULL && current->value != value)
	{
		current = current->link;
	}
	if(current->value == value)
	{
		return current;
	}
	else
	{		
		printf("end of the link and not find!");
		return NULL;
	}
}
```



