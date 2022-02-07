# 快速开始

## 例1 解析Json(不可变)

```javascript
{
	"person": {
		"name": "Tom",
		"age": 18,
		"height": 1.88
	}
}
```
例如, 我们想要拿到这个Json内的`person`对象, 并且拿到`person`对象内的所有属性
```Java
String jsonStr = "{\n" +
                "\t\"person\": {\n" +
                "\t\t\"name\": \"Tom\",\n" +
                "\t\t\"age\": 36,\n" +
                "\t\t\"height\": 1.88,\n" +
                "\t}\n" +
                "}";

/* 创建一个不可变Json实例 */
Json root = new Json(jsonStr);

/* 通过Json指针拿到person对象 */
var person = root.getPointer("/person").asPointerObject();

/* Tom */
String name = person.getString("name");

/* 36 */
int age = person.getInt("age");

/* 1.88 */
double height = person.getDouble("height");

/* 释放资源 */
root.close();
```

## 例2 创建Json(可变)
例如我们想要创建一个如上一模一样的Json
```Java
/* 创建一个可变JSON(根节点为对象) */
JsonMut mut = JsonMut.buildObject();

/* 获取根节点(因为上面创建的是根节点为对象的Json, 所以强转到JsonMutObject类型) */
var root = (JsonMut.JsonMutObject) mut.getRoot();

/* 在根节点内创建一个person对象 */
var person = root.createJsonMutObject("person");

/* 在person对象中添加值(K-V) */
person.addStr("name", "Lisa")
		.addInt("age", 18)
		.addDouble("height", 1.7);

/* 获得Json字符串, 并输出 */
System.out.println(mut.getJsonStr());

/* 释放资源 */
mut.close();
```
输出结果:
```
	{
		"person": {
			"name": "Lisa",
			"age": 18,
			"height": 1.7
		}
	}
```