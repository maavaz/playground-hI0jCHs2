C has a type of variable which can store address or memory location. This type of variable is called a pointer. Essentially a pointer holds address of a variable. To declare a variable as a pointer, `*` is used before the variable name as seen in the example below:

```C runnable
#include <stdio.h>

int main()
{
	int a = 55;
	int *pa = &a;

	printf("The address of a  is %p\n", &a);
	printf("The content of a  is %d\n", a);
	printf("The content of pa is %p\n", pa);
	printf("The address of pa is %p\n", &pa);

	return 0;
}
```

A pointer is also called _reference type_ variable in generic way. `int *pa = &a;` can be stated like `pa` is a pointer to an integer. `pa` points to `a`. Just like `a` has a content (55), `pa` has a content (that's the address of `a`). As `pa` itself is a variable, it has an address too.

The content of `a` can be obtained using `pa`. This is called **dereferencing** a pointer. Dereferencing a pointer can be performed by a `*` character before the pointer variable name as seen in the example below:

```C runnable
#include <stdio.h>

int main()
{
	int a = 55;
	int *pa = &a;

	printf("The address of a             is %p\n", &a);
	printf("The content of a             is %d\n", a);
	printf("The content of pa            is %p\n", pa);
	printf("The address of pa            is %p\n", &pa);
	printf("The content of content of pa is %d\n", *pa); /* Dereference */
	printf("The content of address of a  is %d\n", *(&a)); /* Dereference */

	return 0;
}
```

As you can see, `*pa == a`. Because `pa == &a`, we can also write `*(&a)` to get the content of `a`.

The declaration and assignment of a pointer can take place in different statements:

```C
int *pa;
pa = &a;
```

It will produce the same result as the example before it.

**Warning:** It is dangerous to leave a pointer without pointing anything. This kind of pointer is called **dangling pointer**. Reading or dereferencing a dangling pointer results in **undefined behaviour**:

```C
int *pa;

/* Fatal: reading uninitialized variable - undefined behaviour */
/* printf("The content of pa is %p\n", pa); */

/* Fatal: dereferencing dangling pointer - undefined behaviour */
/* printf("The dereferenced value of pa is %d\n", *pa); */
```

An undefined behaviour means that when a compiler encounters anything that triggers undefined behaviour, it is allowed to do anything it seems appropriate. For maximum portability of your program, make sure to avoid any undefined behaviour.

Since pointers are themselves variables, there can be pointer which points to another pointer! Run and observe the output of the following example:

```C runnable
#include <stdio.h>

int main()
{
	int a = 55;			/* An integer */
	int *pa = &a;		/* A pointer to an integer */
	int **ppa = &pa;	/* A pointer to a pointer to an integer */

    printf("The content of a              is %d\n", a);
	printf("The address of a              is %p\n", &a);

	printf("The content of pa             is %p\n", pa);
	printf("The address of pa             is %p\n", &pa);
	printf("The dereferenced value of pa  is %d\n", *pa);

	printf("The content of ppa            is %p\n", ppa);
	printf("The address of ppa            is %p\n", &ppa);
	printf("The dereferenced value of ppa is %p\n", *ppa);
	printf("The content of a through ppa  is %d\n", **ppa);

	return 0;
}
```

In words:

**Referencing/pointing**

```
address of a  == content of pa
address of pa == content of ppa
```

**Dereferencing**

```
dereferenced value of ppa   == content of pa
dereferenced value of pa    == content of a
double dereferencing of ppa == content of a
```

