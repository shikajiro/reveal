## はじめてのKotlin

![](img/shikajiro.jpg)

@shikajiro

Android フリーランスプログラマー

---

![](img/kotlin.jpg)

イマドキ系JVM言語

- Java互換
- Javaと同じコンパイル速度
- Javaより安全
- Javaより簡潔

---

## Javaと比べたKotlinの特徴
- 型推論
- 関数型プログラミング
- Null 安全
- プロパティ
- 拡張関数
- イミュータブル
- 名前付き・デフォルト引数
- デリゲート
- 演算子オーバーロード
- とか
---


## 型推論
java
```java
String dogName = "もなか";
```
kotlin
```kotlin
val dogName :String = "もなか"
val dogName = "もなか"
```

---

## 暗黙の型チェック
java
```java
if(dog instanceof Dog){
    Dog d = (Dog)dog;
    d.walking();
}
```
kotlin
```kotlin
if(dog is Dog){
    dog.walking()
}
```

---

## 関数型プログラミング

kotlin
```kotlin
fun createDog(name:String):Dog{/**/}

fun postDog(createDogFun : (name:String)->Dog){/**/}

//関数を渡す場合
postDog(::createDog)
//ラムダを渡す場合
postDog { name -> 
  Dog()
}  
```

---

## イミュータブル

kotlin
```kotlin
val dog = Dog() // Immutable 不可変
dog = Dog() //コンパイルエラー

var dog2 = Dog() // Mutable 可変
dog2 = Dog() //OK
```

---

## プロパティ

java
```java
class Dog{
    private String name;
    public String getName(){
        return name;
    }
    public void setName(String name){
        this.name = name;
    }
}
```

kotlin
```kotlin
class Dog{
    var name : String
}
```

---

## プロパティ

kotlin
```kotlin
class Dog{
    var name : String
        get() {
            return field // バッキングフィールドと呼ぶ
        }
        set(value) {
            field = value
        }
}
```

---

## if, when (switch) は式
java
```java
String text;
if(dogName.equal("もなか")){
    text = "かわいい";
}else{
    text = ""
}
```
kotlin
```kotlin
val text = if (dogName == "もなか") "かわいい" else ""
```

---

java
```java
String text;
switch(dogName){
    case "もなか":
        text = "かわいい"
        break;
    default:
        text = ""
        break;
}
```
kotlin
```kotlin
val text = when (dogName) {
  "もなか" -> "かわいい"
  else -> ""
}
```
```kotlin
val text = when {
  dogName == "もなか" -> "かわいい"
  dogAge > 5 -> "やっぱりかわいい"
  else -> ""
}
```

---

## Utilクラスの脱却
```java
class DateUtil{
    public static String format(Date date){/***/}
}
DateUtil.format(new Date());
```

#### トップレベル関数にできる
```kotlin
fun format(date:Date):String{/**/}

format(Date())
```

#### 拡張関数にできる
```kotlin
fun Date.format():String{/**/}

Date().format()
```

---

## 名前付き引数、デフォルト引数
java
```java
public void createDog(String name, String address, String type, int color, 
                                       int age, int gender){/***/}
public void createDog(String name, String address, String type, int color, 
                                       int age){
    createUser(name, address, type, color, age, 0)
}
```

kotlin
```kotlin
fun createDog(name:String, address:String, type:String, color:Int, age:Int, 
              gender:Int = 0)

createDog(address="住所", name=name, color=0xFFFFFF, age=3, 
    type="corgi")
```

---

## Null Safety 1
java
```java
public void hug(Dog dog){
    // もし dog == null なら NullPointerException が起きる 
    String name = dog.getName(); 
}
```
kotlin
```kotlin
fun hug(dog : Dog){
    val name = dog.name
    //...
}
val dog : Dog? = /***/
hug(dog)// この時点でnullの可能性があるdogインスタンスを渡すとコンパイルエラー
```

---

## Null Safety 2
kotlin
```kotlin
fun hug(dog : Dog?){ //nullかもしれないdogを受け取ることが可能になる
    val name1 = dog.name // dogはnullかもしれないのでコンパイルエラー
    val name2 : String? = dog?.name // name2には文字列かnullが代入される
    
    // dog または name が null なら return
    val name3 : String = dog?.name ?: return
}
```

---

## Null Safety 3
kotlin
```kotlin
val dog : Dog? = /***/
if(dog != null){
    dog.walking() //null check をしたのでコンパイルエラーにはならない
}
```

```kotlin
dog?.let { it.walking() }
```

---

## Null Safety まとめ

kotlinを使えばnullぽが起きないわけじゃない。

kotlinを正しく使えば意図しないnullぽは起きない！（願望）


---

## スコープ関数
`apply()` を使えば　builder pattern みたいになる。名前付き引数でメソッドを呼んでる感覚。

```java
Dog dog = new Dog();
dog.setName("");
dog.setAddress("");
dog.setGender(1);
```

```kotlin
val dog = Dog().apply {
    name = ""
    address = ""
    gender = 1
}

```

---

## 文字列

```kotlin
val str1 = "${dog.name} は かわいい！"
val str2 = """
#{dog.name}は
かわいい
"""
```

---

## データオブジェクト
java
```java
class Dog{
    private String name;
    private String address;
    public String getName(){ return name; }
    public String setName(String name){this.name = name;}
    public String getAddress(){ return address; }
    public String setAddress(String name){this.address = address;}
    override public String toString(){/***/}
    override public equals(){/***/}
    override public hashCode(){/***/}
    public Dog copy(){/***/}
}

```
kotlin
```kotlin
data class Dog(val name:String, val address:String)
```

---

## まとめ

これを読もう。

![](img/kotlin_start.jpg)
