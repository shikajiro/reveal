## Kotlin で Extension

![](img/shikajiro.jpg)

@shikajiro

Android フリーランスプログラマー

---

## Extension(拡張関数)とは

既存クラスにメソッドを追加できる

```kotlin
val last = "shikajiro".lastChar()
```
---

### 文字列の最後を取得したい
```
val str = "shikajiro"
str.get(str.length - 1)
```
---

### static method 
```
class StringUtil{
  companion object {
    fun lastChar(str:String):Char{
      return str.get(str.length - 1)
    }
  }
}
StringUtil.lastChar(str)
```
---

### singleton
```
object StringUtil{
  fun lastChar(str:String):Char{
    return str.get(str.length - 1)
  }
}
StringUtil.lastChar(str)
```
---

### instance method
```kotlin
fun lastChar(str:String):Char{
  return str.get(str.length - 1)
}
lastChar(str)
```
---

### Extension(拡張関数)
```kotlin
fun String.lastChar():Char{
  return this.get(this.length - 1)
}
str.lastChar()
```
---

### Extension の書き方
```kotlin
fun レシーバ型.lastChar() = 
    レシーバオブジェクト.get(length -1)
```
---

### 省略
```kotlin
fun String.lastChar() = get(length -1)
```
---

### Extension
Java の Static Method とほぼ同等。書きやすく、読みやすく、呼びやすくしたもの。
可読性の良いStatic Method。

##### 拡張関数でできないこと
カプセル化はやぶれない
---

### 拡張プロパティ
```
val StringBuilder.lastChar: Char
    get() = get(length -1)
    set(value: Char) {
        setCharAt(length -1, value)
    }
val last = str.lastChar // shikajiro
str.lastChar = 'u' // shikajiru
```
---

### 拡張ラムダ
あとで
---

## DataBinding でやってみる
```xml
<layout>
<LinearLayout>
    <include 
        android:id="@+id/email" />
    <include 
        android:id="@+id/password"/>
</LinearLayout>
</layout>
```
---

```kotlin
var binding:ParentBinding
binding.email.emailView.setText("shikajiro@gmail.com")
binding.password.passwordView.setText("password")
//略
```
---

```kotlin
fun login(binding:ParentBinding) {
    binding.email.emailView.setText("shikajiro@gmail.com")
    binding.password.passwordView.setText("password")
}
login(binding)
```
---

```kotlin
fun ParentBinding.login() {
    email.emailView.setText("shikajiro@gmail.com")
    password.passwordView.setText("password")
}
binding.login()
```
---

```kotlin
binding.apply({ //this
  email.emailView.setText("shikajiro@gmail.com")
  password.passwordView.setText("password")
})
```
---

```kotlin
fun ParentBinding.login(block: ParentBinding.() -> Unit) {
    block()
}
binding.login{
  email.emailView.setText("shikajiro@gmail.com")
  password.passwordView.setText("password")
}
```
---

```kotlin
fun <T : ViewDataBinding> T.login(block: T.() -> Unit){
    block()
}
binding.login {
  email.login {
    emailView.setText("shikajiro@gmail.com")
  }
  password.login {
    passwordView.setText("password")
  }
}
```
---

```kotlin
operator fun <T : ViewDataBinding> T.invoke(block: T.() -> Unit){
    block()
}
binding {
  email {
    emailView.setText("shikajiro@gmail.com")
  }
  password {
    passwordView.setText("password")
  }
}
```
---

### DataBindingの入れ子にアクセスしやすくなったような気がする
---

## まとめ
### 拡張関数すごい

これを買おう

Have a Nice Kotlin

![](img/kotlininaction.jpg)
