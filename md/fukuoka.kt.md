## はじめてのKotlin

@shikajiro

![](img/shikajiro.jpg)

---

## Javaと比べたKotlinの特徴
- 関数型プログラミング
- Nullable, NotNull
- Property
- Extension
- Immutable
- default param
- object
- delegate

---

## 関数型プログラミング

```java
class User{
    private String name;
    public String getName(){
        return name;
    }
    public void setName(String name){
        this.name = name;
    }
}
```

```kotlin
class User{
    var name : String
}
```