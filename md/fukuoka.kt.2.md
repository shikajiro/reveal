## Kotlin で Test

![](img/shikajiro.jpg)

@shikajiro

Android フリーランスプログラマー

---

## 今日紹介するもの
### kotlintest
### spek

---

## Java
```java
public class CalculatorTest {
    @Test
    public void testSum() throws Exception {
        Calculator calculator = new Calculator();
        assertEquals(300, calculator.sum(200, 10));
    }
}
```

---

### Kotlin
```kotlin
class CalculatorTest {
    @Test
    fun testSum() {
        val calculator = Calculator()
        assertEquals(300, calculator.sum(200, 100))
    }
}
```

---

## KotlinTest

Scalatest 風 便利テストライブラリ

---

## KotlinTest
```kotlin
class SimpleKotlinTest : StringSpec() {
    init {
        "Calculator.sum should return all total value" {
            val calculator = Calculator()
            calculator.sum(200, 100) shouldBe 300
        }
    }
}
```

---

### Property Testing

1000回テストをする
```kotlin
"Calculator.sum random test" {
    forAll { i: Int, j: Int ->
        Calculator().sum(i, j) == i + j
    }
}
```

---

```kotlin
"Calculator.sum table test" {
    val table = table(
            headers("a", "b", "result"),
            row(1, 2, 3),
            row(1, 1, 2)
    )
    forAll(table) { a, b, result ->
        Calculator().sum(a, b) shouldBe result
    }
}
```

---

## Spek

RSpec風な読みやすいテストライブラリ

---


```kotlin
class SimpleSpek : Spek(
    {
        given("一般的な計算を行うクラス") {
            val calculator = Calculator()
            on("合計値を計算する") {
                val value = calculator.sum(200, 10)
                it("300になる") {
                    assertEquals(300, value)
                }
            }
        }
    })
```

---

<img src="img/spek1.png" width=1200px>

---

### style

|||
|:---|:---|
|given, on, it|基本|
|describe, it|Jasmine, Mocha|

---

```kotlin
given("コンテキスト") {
    val calculator = Calculator()
    on("処理") {
        val value = calculator.sum(200, 100)
        it("検証") {
            assertEquals(300, value)
        }
    }
}
```

---

```kotlin
describe("コンテキスト"){
    val calculator = Calculator()
    it("処理と検証"){
        val value = calculator.sum(200, 100)
        assertEquals(300, value)
    }
}
```

---

### assertion

|||
|:---|:---|
|kotlin-test|assertEquals(a, b)|
|HamKrest|assert.that(a, b)|
|Expekt|a.should.equal(b)|
|Kluent|a shouldEqual b|

---

### Fixtures

```kotlin
describe("a group") {
    beforeGroup { /* 1 */ }
    beforeEachTest { /* 2, 6 */ }
    context("a nested group") {
        beforeEachTest { /* 3 */ }
        it("should work") { /* 4 */ }
    }
    it("do something") { /* 7 */ }
    afterEachTest { /* 5, 8 */ }
    afterGroup { /* 9 */ }
}
```