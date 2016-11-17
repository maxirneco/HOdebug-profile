add_array_segfault.c

#include <stdio.h>
//#include <stdlib.h>// agregamos porque faltaba declarar abs (warning: implicit declaration of function ‘abs’ [-Wimplicit-function-declaration]
     sum += abs(a[i]))

int add_array(int *a, int *b, int n){
  int sum = 0;
  int i = 0;
  for (i = 0; i <= n + 1; i++) {
    sum += abs(a[i]);
    sum += abs(b[i]);
  };
  return sum;
}

int main(int argc, char **argv) {
  int *a, *b;
  int n = 3;

// a = malloc(sizeof(int) * 3);
  b = malloc(sizeof(int) * 3);//Agregamos esta parte para que se le asigne lugar de memoria a a y b (segmetation fault)

  int i, sum;
  for (i = 0; i < n; i++) {
    a[i] = i;
    b[i] = i;
  }
  sum = add_array(a, b, 3);
  printf("The addition is %d\n", sum);
  return 0;
}


add_array_dynamic.c

#include <stdio.h>
#include <stdlib.h>

int add_array(int *a, int *b, int n){
  int sum = 0;
  int i = 0;
  for (i = 0; i <= n + 1; i++)-------> lo correcto seria i<n pues los vectores estan definidos para dimension n.
    sum += abs(a[i]);
    sum += abs(b[i]);
  };
  return sum;
}

int main(int argc, char **argv) {
  int *a, *b;
  int n = 3;
  int i, sum;
  a = malloc(sizeof(int) * 3);
  b = malloc(sizeof(int) * 3);
  for (i = 0; i < n; i++) {
    a[i] = i;
    b[i] = i;
  }
  sum = add_array(a, b, 3);
  printf("The addition is %d\n", sum);
  return 0;
}


add_array_static.c

#include <stdio.h>

//warning: implicit declaration of function ‘abs’ [-Wimplicit-function-declaration]
     sum += abs(a[i]);// pues no esta agregado el header que accede a la biblioteca donde se declara abs


int add_array(int *a, int *b, int n){
  int sum = 0;
  int i = 0;
  for (i = 0; i <= n + 1; i++) {//gabi@gabi-W240HU-W250HUQ ~/HOdebug-profile/debug/bugs $ ./static.e
The addition is 92771190// el problema es que suma hasta n+1 cuando deberia hacerlo hasta n-1

    sum += abs(a[i]);
    sum += abs(b[i]);
  };
  return sum;
}

int main(int argc, char **argv) {
  int a[3], b[3];
  int n = 3;
  int i, sum;
  for (i = 0; i < n; i++) {
    a[i] = i;
    b[i] = i;
  }
  sum = add_array(a, b, 3);
  printf("The addition is %d\n", sum);
  return 0;
}




