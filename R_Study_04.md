### 데이터 전처리
```r
library(dplyr)
exam <- read.csv("./Data/csv_exam.csv")
head(exam, 10)
```

- %>% : 파이프 연산자(pipe operator)로 함수들을 연결하는 기능
- filter(조건) : 행 추출
  - & : and
  - | : or
  - %in% : 포함
```r
exam %>% filter(class == 1)
exam %>% filter(class == 2)
exam %>% filter(class != 1)
exam %>% filter(english <= 80)
exam %>% filter(class == 1 & math >= 50)
exam %>% filter(english >= 90 | math >= 90)
exam %>% filter(class %in% c(1, 3, 5)) 
class1 <- exam %>%
  filter(class == 1) # class == 1인 것 class1에 할당
mean(class1$math)
```

- 연산자
  - ^, ** : 제곱
  - %/% : 몫
  - %% : 나머지

- select(열 이름) : 열(변수) 추출
```r
exam %>%
  select(class, math) # 여러 변수 추출
exam %>%
  select(-math) # '-'기호를 통해 변수를 제외
```

- dplyr 함수 조합
```r
exam %>%
  filter(class == 1) %>%
  select(english)
exam %>%
  filter(class == 2) %>%
  select(math)

exam %>%
  select(id, math) %>%
  head
```

- arrange(열 이름) : 열 정렬
```r
exam %>% arrange(math) # 오름차순 정렬
exam %>% arrange(desc(math)) # 내림차순 정렬

head(mpg %>%
       filter(manufacturer == "audi") %>%
       arrange(desc(hwy)), 5)
mpg %>%
  filter(manufacturer == "audi") %>%
  arrange(desc(hwy)) %>% head(5)
```

- mutate(새로운 열 = 조건) : 새로운 열 추가
```r
exam %>% mutate(total = math + english + science) %>% head
exam %>% mutate(sum = math + english + science, mean = sum / 3) %>% arrange(sum)
exam %>% mutate(test = ifelse(science >= 60, "pass", "fail")) %>% head
```

- summarise(조건) : 집단별로 요약
- summarise 함수
  - n() : 빈도수
  - mean() : 평균
  - var() : 분산
  - sd() : 표준편차
  - sum() : 합계
  - max() : 최대값
  - min() : 최소값
  - median() : 중위값
  - IQR() : 4분위값
  - mad() : 중위절대편차
```r
exam %>% summarise(mean_math = mean(math))
```

```r
exam %>% group_by(class) %>% summarise(mean_math = mean(math))
exam %>% group_by(class) %>% summarise(
  mean_math = mean(math),
  sum_math = sum(math),
  median_math = median(math),
  n = n()
)
```

```r
mpg %>%
  group_by(manufacturer, drv) %>%
  summarise(mean_cty = mean(cty)) %>%
  head(10)
```

```r
mpg %>%
  group_by(manufacturer) %>%
  filter(class == "suv") %>%
  mutate(sum = hwy + cty) %>%
  summarise(mean = mean(sum)) %>%
  arrange(desc(mean)) %>%
  head(5)
```

- left_join : 가로로 데이터 프레임 합치기
- bind_rows : 세로로 데이터 프레임 합치기
  - 세로로 합칠 변수명이 다를 경우 rename()을 통해 변수를 통일

```r
test1 <-
  data.frame(id = c(1, 2, 3, 4, 5),
             midterm = c(60, 80, 70, 90, 85))
test2 <-
  data.frame(id = c(1, 2, 3, 4, 5),
             final = c(70, 83, 65, 95, 80))
test3 <-
  data.frame(id = c(6, 7, 8, 9, 10),
             midterm = c(60, 80, 70, 90, 85))
```

```r
total <- left_join(test1, test2, by = "id") # 가로로 합치기
total

name <- data.frame(id = c(1, 2, 3, 4, 5),
                   teacher = c("kim", "choi", "park", "jung", "lee"))
total <- left_join(total, name, by = "id")
total
```

```r
total2 <- bind_rows(test1, test3) # 세로로 합치기
total2
```