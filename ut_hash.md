- [通用结构hash](#----hash)
  * [定义结构体](#-----)
  * [定义头节点](#-----)
  * [添加节点](#----)
  * [查找结点](#----)
  * [遍历节点](#----)
  * [删除节点](#----)
  * [删除整个hash表](#----hash-)
  * [获取hash表长度](#--hash---)

- 文档 http://troydhanson.github.io/uthash/userguide.html

# 通用结构hash
在uthash中，并不会对其所储存的值进行移动或者复制，也不会进行内存的释放。
## 定义结构体
```
typedef struct {
    UT_hash_handle handle; // handle,不用初始化
    long long key;         // key
    char data[100];        // data
} MyHash;  
```
## 定义头节点
- hash需要定义头节点，可以使用全局变量
```
MyHash *g_hashHead = NULL; // 头节点一定要初始化成空指针
```
## 添加节点
```
void AddNode(long long key, char *data)
{
    MyHash node = { 0 };
    node.key = key;
    memcpy(node.data, data, sizeof(char) * 100);
    HASH_ADD(handle, g_hashHead, key, sizeof(long long), &node);
}
```
|macro|arguments|
|:-:|:-:|
|HASH_ADD|(hh_name, head, keyfield_name, key_len, item_ptr)|

## 查找结点
```
MyHash *FindNode(long long key)
{
    MyHash *node;
    HASH_FIND(handle, g_hashHead, &key, sizeof(long long), node);
    return node;
}
```
查找不到key时，返回NULL
|macro|arguments|
|:-:|:-:|
|HASH_FIND|(hh_name, head, key_ptr, key_len, item_ptr)|
## 遍历节点
推荐该方式，也可以使用UT_hash_handle handle里的next, prev指针做类似双向链表的遍历。
```
VOID PrintNode()
{
    MyHash *currNode, *tmp;
    HASH_ITER(handle, g_hashHead, currNode, tmp) {
        printf("key:%lld, data:%s", currNode->key, currNode->data);
    }
}
```
|macro|arguments|
|:-:|:-:|
|HASH_ITER|(hh_name, head, item_ptr, tmp_item_ptr)|
## 删除节点
```
VOID DeleteNode(MyHash *nodeToDelete)
{
    HASH_DELETE(handle, g_hashHead, nodeToDelete);
}
```
|macro|arguments|
|:-:|:-:|
|HASH_DELETE|(hh_name, head, item_ptr)|
## 删除整个hash表
```
HASH_CLEAR(handle, g_hashHead)
```
|macro|arguments|
|:-:|:-:|
|HASH_CLEAR|(hh_name, head)|
## 获取hash表长度
```
HASH_CNT(handle, g_hashHead)
```
|macro|arguments|
|:-:|:-:|
|HASH_CNT|(hh_name, head)|
# int型key的简便hash表
## 定义结构体
```
typedef struct {
    UT_hash_handle handle; // handle,不用初始化
    int key;         // key
    char data[100];        // data
} MyIntHash;  
```
## 定义头节点
- hash需要定义头节点，可以使用全局变量
```
MyIntHash *g_intHashHead = NULL; // 头节点一定要初始化成空指针
```
## 添加节点
```
void AddNode(int key, char *data)
{
    MyHash node = { 0 };
    node.key = key;
    memcpy(node.data, data, sizeof(char) * 100);
    HASH_ADD_INT(g_intHashHead, key, &node);
}
```
|macro|arguments|
|:-:|:-:|
|HASH_ADD_INT|(head, keyfield_name, item_ptr)|
## 查找结点
```
MyHash *FindNode(int key)
{
    HASH_FIND_INT(g_intHashHead, &key, &node);
    return node;
}
```
查找不到key时，返回NULL
|macro|arguments|
|:-:|:-:|
|HASH_FIND_INT|(head, key_ptr, item_ptr)|
## 遍历节点
同通用hash的遍历方式
## 删除节点
同通用hash的删除方式
