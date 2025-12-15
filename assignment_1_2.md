# Assignment No: 1.2

## Title
Write a program to construct and verify a magic square of order 'n' (for both even & odd) such that all rows, columns, and diagonals sum to the same value.

## Code

```cpp
#include<iostream.h>
#include<conio.h>

int isMagicMatrix(int arr[50][50],int n) {
    int msum=0;
    int i, j;
    int dsum1=0,dsum2=0;

    for(i=0;i<n;i++) {
        msum+=arr[0][i];
    }
    
    for(i=0;i<n;i++) {
        int rsum=0,csum=0;
        for(j=0;j<n;j++) {
            rsum+=arr[i][j];
            csum+=arr[j][i];
        }
        if(rsum!=msum || csum!=msum) {
            return 0;
        }
        dsum1+=arr[i][i];
        dsum2+=arr[i][n-i-1];
    }
    if(dsum1!=msum || dsum2!=msum) {
        return 0;
    }
    cout<<"Magic sum: "<<msum<<endl;
    return 1;
}

int main() {
    int n, i, j;
    int arr[50][50];
    clrscr();

    cout<<"Enter the value of n: ";
    cin>>n;
    
    for(i=0;i<n;i++) {
        for(j=0;j<n;j++) {
            cout<<"Enter the element at position "<<i<<","<<j<<": ";
            cin>>arr[i][j];
        }
    }
    if(isMagicMatrix(arr,n)) {
        cout<<"It is the magic matrix";
    }
    else {
        cout<<"It is not the magic matrix";
    }
    getch();
    return 0;
}

```

## Output

```text
Enter the value of n: 3
Enter the element at position 0,0: 8
Enter the element at position 0,1: 1
Enter the element at position 0,2: 6
Enter the element at position 1,0: 3
Enter the element at position 1,1: 5
Enter the element at position 1,2: 7
Enter the element at position 2,0: 4
Enter the element at position 2,1: 9
Enter the element at position 2,2: 2

Magic sum: 15
It is the magic matrix
```
