### 변수 선언

```r
a <- 2
b <- 3
a + b # 5
```

### 숫자 관련 함수 및 연산

-   c() : 여러 개의 값을 넣는 것
-   seq() : 연속된 값 생성

```r
var1 <- c(1, 2, 3)
var2 <- c(6, 7, 8)

var3 <- seq(1, 5) # 1,2,3,4,5
var4 <- seq(1, 10, 2) # 1,3,5,7,9

var1 + var2 # 각 위치 값끼리 연산
var3 + 2 # 각 요소마다 연산

mean(var1) # 2
max(var1) # 3
min(var1) # 1
```

### 문자열 관련 함수 및 연산

```r
str1 <- "Hello "
str2 <- "World!"
# 문자열끼리 이항 연산자(str1 + 1) 사용 불가능
paste(str1, str2) # Hello World
str3 <- c("Hello", "World", "Laeti")
# !을 구분자로 단어들 연결
paste(str3, collapse = "!") # Hello!World!Laeti
str_arr1 <- c("DongHun", "Park") # Hello World
paste(str_arr1, collapse = "-") # DongHun-Park
```
