- [通用结构hash](#----hash)
  * [定义结构体](#-----)

- 文档 http://troydhanson.github.io/uthash/userguide.html

# 通用结构hash
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
void addNode(long long key, char *data)
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
MyHash *addNode(long long key)
{
  MyHash *node;
  HASH_FIND(handle, g_hashHead, &key, sizeof(long long), node);
  return node;
}
```
查找不到key时，返回NULL

