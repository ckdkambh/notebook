- [通用key结构hash](#通用key结构hash)
  * [定义结构体](#定义结构体)
  * [定义头节点](#定义头节点)
  * [添加节点](#添加节点)
  * [查找结点](#查找结点)
  * [遍历节点](#遍历节点)
  * [删除节点](#删除节点)
  * [删除整个hash表](#删除整个hash表)
  * [获取hash表长度](#获取hash表长度)
- [int型key的简便hash表](#int型key的简便hash表)
  * [定义结构体](#定义结构体-1)
  * [定义头节点](#定义头节点-1)
  * [添加节点](#添加节点-1)
  * [查找结点](#查找结点-1)
  * [遍历节点](#遍历节点-1)
  * [删除节点](#删除节点-1)
- [字符串型key的简便hash](#字符串型key的简便hash)
  * [定义结构体](#定义结构体-2)
  * [定义头节点](#定义头节点-2)
  * [添加节点](#添加节点-2)
  * [查找结点](#查找结点-2)
  * [遍历节点](#遍历节点-2)
  * [删除节点](#删除节点-2)
- [指针型key的简便hash](#指针型key的简便hash)
  * [定义结构体](#定义结构体-3)
  * [定义头节点](#定义头节点-3)
  * [添加节点](#添加节点-3)
  * [查找结点](#查找结点-3)
  * [遍历节点](#遍历节点-3)
  * [删除节点](#删除节点-3)
- [其他函数](#其他函数)
- [leetcode例题](#leetcode例题)

- 文档 http://troydhanson.github.io/uthash/userguide.html  https://blog.csdn.net/JT_Notes/article/details/81330023

# 通用key结构hash
在uthash中，并不会对其所储存的值进行移动或者复制，也不会进行内存的释放。每个节点的内存都要自己__malloc__，不能使用局部变量，否则可能异常。
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
    MyHash *node = malloc(sizeof(MyHash));
    node->key = key;
    memcpy(node.data, data, sizeof(char) * 100);
    HASH_ADD(handle, g_hashHead, key, sizeof(long long), node);
}
```
|名称|参数|
|:-:|:-:|
|HASH_ADD|(hh_name, head, keyfield_name, key_len, item_ptr)|

## 查找结点
```
void FindNode(long long key)
{
    MyHash *node;
    HASH_FIND(handle, g_hashHead, &key, sizeof(long long), node);
    printf("%lld, %s", node->key, node->data);
}
```
查找不到key时，返回NULL
|名称|参数|
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
|名称|参数|
|:-:|:-:|
|HASH_ITER|(hh_name, head, item_ptr, tmp_item_ptr)|
## 删除节点
```
VOID DeleteNode(MyHash *nodeToDelete)
{
    HASH_DELETE(handle, g_hashHead, nodeToDelete);
}
```
|名称|参数|
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
|名称|参数|
|:-:|:-:|
|HASH_CNT|(hh_name, head)|
# int型key的简便hash表
## 定义结构体
```
typedef struct {
    UT_hash_handle handle; // handle,不用初始化
    int key;               // key
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
    MyIntHash *node = malloc(sizeof(MyIntHash));
    node->key = key;
    memcpy(node->data, data, sizeof(char) * 100);
    HASH_ADD_INT(g_intHashHead, key, node);
}
```
|名称|参数|
|:-:|:-:|
|HASH_ADD_INT|(head, keyfield_name, item_ptr)|
## 查找结点
```
void FindNode(int key)
{
    MyIntHash *node;
    HASH_FIND_INT(g_intHashHead, &key, node);
    printf("%d, %s", node->key, node->data);
}
```
查找不到key时，返回NULL
|名称|参数|
|:-:|:-:|
|HASH_FIND_INT|(head, key_ptr, item_ptr)|
## 遍历节点
同通用hash的遍历方式 [遍历节点](#遍历节点)
## 删除节点
同通用hash的删除方式 [删除节点](#删除节点)
# 字符串型key的简便hash
## 定义结构体
```
typedef struct {
    UT_hash_handle handle; // handle,不用初始化
    char key[20];          // key
    char data[100];        // data
} MyStrHash;  
```
## 定义头节点
- hash需要定义头节点，可以使用全局变量
```
MyStrHash *g_strHashHead = NULL; // 头节点一定要初始化成空指针
```
## 添加节点
```
void AddNode(char *key, char *data)
{
    MyStrHash *node = malloc(sizeof(MyStrHash));
    strcpy(node->key, key);
    memcpy(node->data, data, sizeof(char) * 100);
    HASH_ADD_STR(g_strHashHead, key, node);
}
```
|名称|参数|
|:-:|:-:|
|HASH_ADD_STR|(head, keyfield_name, item_ptr)|
## 查找结点
```
void FindNode(char *key)
{
    MyStrHash *node;
    HASH_FIND_STR(g_strHashHead, key, node);
    printf("%s, %s", node->key, node->data);
}
```
查找不到key时，返回NULL
|名称|参数|
|:-:|:-:|
|HASH_FIND_STR|(head, key_ptr, item_ptr)|
## 遍历节点
同通用hash的遍历方式 [遍历节点](#遍历节点)
## 删除节点
同通用hash的删除方式 [删除节点](#删除节点)

# 指针型key的简便hash
## 定义结构体
```
typedef struct {
    UT_hash_handle handle; // handle,不用初始化
    void *key;             // key
    char data[100];        // data
} MyPointHash;  
```
## 定义头节点
- hash需要定义头节点，可以使用全局变量
```
MyPointHash *g_pointHashHead = NULL; // 头节点一定要初始化成空指针
```
## 添加节点
```
void AddNode(void *key, char *data)
{
    MyPointHash *node = malloc(sizeof(MyPointHash));
    node.key = key;
    memcpy(node.data, data, sizeof(char) * 100);
    HASH_ADD_PTR(g_strHashHead, key, node);
}
```
|名称|参数|
|:-:|:-:|
|HASH_ADD_PTR|(head, keyfield_name, item_ptr)|
## 查找结点
```
void FindNode(void *key)
{
    MyStrHash *node;
    HASH_FIND_PTR(g_strHashHead, &key, node);
    printf("%p, %s", node->key, node->data);
}
```
查找不到key时，返回NULL
|名称|参数|
|:-:|:-:|
|HASH_FIND_PTR|(head, key_ptr, item_ptr)|
## 遍历节点
同通用hash的遍历方式 [遍历节点](#遍历节点)
## 删除节点
同通用hash的删除方式 [删除节点](#删除节点)
# 其他函数
|名称|参数|功能|
|:-:|:-:|
|HASH_DEL|(head, item_ptr)|基于HASH_DELETE的宏|
|HASH_SORT|(head, cmp)|基于HASH_SRT的宏|
|HASH_COUNT|(head)|将源hash表中复合条件的元素添加到目标hash表|
|HASH_SELECT|(dst_hh_name, dst_head, src_hh_name, src_head, condition)|基于HASH_CNT的宏|
|HASH_OVERHEAD|(hh_name, head)|统计hash表内部结构消耗的内存|
# leetcode例题
int型key和字符串型key hash:https://leetcode-cn.com/problems/design-underground-system/
