# qcc1
#include <stdio.h>
#include <stdlib.h>
typedef int E;
struct list {
    E  *arr;
    int Long;
    int size;
};
typedef struct list * node;

_Bool initList(node list) {
    list->arr= malloc(sizeof (int)*10);
    list->Long=10;
    list->size=0;
    if (list->arr==NULL)return 0;
    return 1;
}


int  inputList(node list){
    printf("输入你数据的个数:");
    int n;
    scanf("\n%d",&n);
    while(list->Long<n){
        int newLong=list->Long+(list->Long>>1);
        int * newArr= realloc(list->arr, newLong * sizeof(E));
        list->arr=newArr;
        list->Long=newLong;
    }
    for (int i = list->size; i < list->Long; ++i) {
        printf("输入你的数据，第%d个:",i+1);
        scanf("%d",&list->arr[i]);
        list->size++;
        if(list->size==n)break;
    }
    return 1;
}

_Bool insertList(node list){
    int index,element;
    printf("输入你想插入的位数:");
    scanf("%d",&index);
    printf("输入你想插入的数据:");
    scanf("%d",&element);
    if(index<1||index>list->size+1){
        printf("输入错误");
        return 0;
    }
    if(list->size==list->Long){
        int newLong=list->Long+(list->Long>>1);
        int * newArr= realloc(list->arr, newLong * sizeof(E));
        list->arr=newArr;
        list->Long=newLong;
    }
    for (int i = list->size; i >index ; --i) {
        list->arr[i+1]=list->arr[i];
    }
    list->arr[index-1]=element;
    list->size++;
    return 1;
}
_Bool findList (node list){
    printf("输入你想寻找的数字:");
    int n;
    scanf("%d",&n);
    for (int i = 0; i <list->size ; ++i) {
        if (list->arr[i] == n) {
            printf("yes\n");
            return 1;
        }
        else printf("No\n");
    }
    return 0;
}
_Bool  deleteList(node list){
    int index;
    printf("输入你想删除的位数:");
    scanf("%d",&index);
    if(index<1||index>list->size){
        printf("输入错误");
        return 0;
    }
    for (int i = index-1; i < list->size; ++i) {
        list->arr[i]=list->arr[i+1];
    }
    list->size--;
    return 1;
}
_Bool getList(node list){
    printf("输入你想查询的位数: ");
    int a;
    scanf("%d",&a);
    printf("%d\n",list->arr[a-1]);
    return 1;
}

_Bool printList (node list) {
    for (int i = 0; i <list->size ; ++i) {
        printf("%d  ",list->arr[i]);
    }
    printf("\n链表数据大小为%d\n",list->size);
    printf("链表现在长度为%d\n",list->Long);
    return 1;
    }
void qidong(node list){
    int a;
    printf("1.输入数字\n2.插入数字\n3.删除数字\n4.寻找数字\n5.查询位数\n6.输出链表数据\n0.退出程序\n");
    scanf("%d",&a);

    switch (a) {
        case 1:
            inputList(list);
            return qidong(list);
        case 2:
            insertList(list);
            return qidong(list);
        case 3:
            deleteList(list);
            return qidong(list);
        case 4:
            findList(list);
            return qidong(list);
        case 5:
            getList(list);
            return qidong(list);
        case 6:
            printList(list);
            return qidong(list);
        case 0:
            return ;
    }
}
int main(){
struct list list;
    if (initList(&list)){
        qidong(&list);
    }
    printf("谢谢使用");

}
