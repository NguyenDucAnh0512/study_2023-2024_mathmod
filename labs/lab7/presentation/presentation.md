---
## Front matter
lang: ru-RU
title: Презентация по лабораторной работе №7
subtitle: модель рекламной компании (Вариант 12)
author:
  - Нгуен Дык Ань
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 24 февраля 2024

## i18n babel
babel-lang: russian
babel-otherlangs: english

## Formatting pdf
toc: false
toc-title: Содержание
slide_level: 2
aspectratio: 169
section-titles: true
theme: metropolis
header-includes:
 - \metroset{progressbar=frametitle,sectionpage=progressbar,numbering=fraction}
 - '\makeatletter'
 - '\beamer@ignorenonframefalse'
 - '\makeatother'
---

# Докладчик

:::::::::::::: {.columns align=center}
::: {.column width="70%"}

  * Нгуен Дык Ань
  * Студенческий билет: 1032215251
  * Группа: НКНбд-01-21
  * Российский университет дружбы народов
  * <https://github.com/NguyenDucAnh0512>

:::
::: {.column width="30%"}

![](https://drive.google.com/uc?id=11Y4Td4A-5Y6xtoE88lvJLn0uziw5GhbB)

:::
::::::::::::::

# Цель работы

Изучаем модель рекламной компании и построим график распространения рекламы с помощью Scilab.

# Задание

Постройте график распространения рекламы, математическая модель которой описывается следующим уравнением:

1. $\frac{dn}{dt}=(0.83+0.00013n(t))(N-n(t))$

2. $\frac{dn}{dt}=(0.000024+0.29n(t))(N-n(t))$

3. $\frac{dn}{dt}=(0.5*t+0.3*t*n(t))(N-n(t))$

# Задание

При этом объем аудитории $N=885$ , в начальный момент о товаре знает 3 человек. Для случая 2 определите в какой момент времени скорость распространения рекламы будет иметь максимальное значение.

# Выполнение задания
## 1. Введение теоремы

Модель рекламной кампании имеет вид:

$$
\frac{dn}{dt}=(\alpha _1 (t)+\alpha _2 (t)n(t))(N-n(t))
$$

* $\frac{dn}{dt}$ - скорость изменения со временем числа потребителей,
узнавших о товаре и готовых его купить.

* $t$ -  время, прошедшее с начала рекламной кампании.

* $n(t)$ - число уже информированных клиентов.

# Выполнение задания
## 1. Введение теоремы

* $N$ - общее число потенциальных платежеспособных покупателей.

* $\alpha _1(t)>0$ - характеризует интенсивность рекламной кампании (зависит от затрат на рекламу в данный момент времени).

* $\alpha _2(t)$ - функция, описывающая сарафанное радио

# Выполнение задания
## 2. Построии график распространения рекламы

Введём в Scilab:

* Начальные условия, соответствующие заданию:

``` Julia
t0=0;  //начальный момент времени
x0=3;  // количество людей, знающих о товаре в момент t0
N=885; // максимальное количество людей, которых может заинтересовать товар
t=0:0.1:30; // временной промежуток
```

# Выполнение задания
## 2. Построии график распространения рекламы

* Функция, отвечающая за платную рекламу и функция, описывающая сарафанное радио:

``` Julia
// Функция, отвечающая за платную рекламу
function g=k(t);
g=0.83;
endfunction
```

# Выполнение задания
## 2. Построии график распространения рекламы

``` Julia
// Функция, описывающая сарафанное радио:
function v=p(t);
v=0.00013;
endfunction
```

# Выполнение задания
## 2. Построии график распространения рекламы

* Уравнение, описывающее распространение рекламы:

``` Julia
function dx=f(t,x);
dx=(k(t)+p(t)*x)*(N-x);
endfunction
```

# Выполнение задания
## 2. Построии график распространения рекламы

* Решение и график решения:

``` Julia
x=ode(x0,t0,t,f);
plot(t,x);
```

# Выполнение задания
## $\frac{dn}{dt}=(0.83+0.00013n(t))(N-n(t))$

![](https://drive.google.com/uc?id=1vwB6Bbe0xQzdIyYo4MRE3poDPrCHeRlm)

# Выполнение задания
## $\frac{dn}{dt}=(0.000024+0.29n(t))(N-n(t))$

В результате указывается в момент $t=0.1$ скорость распространения рекламы будет иметь максимальное значение.

![](https://drive.google.com/uc?id=14msLEBWHBCokgboFdT7Iz0h_9JOC1sIR)

# Выполнение задания
## $\frac{dn}{dt}=(0.5*t+0.3*t*n(t))(N-n(t))$

![](https://drive.google.com/uc?id=1NWcXMmEKUgSvyik5kl-P0F6rKK882zlq)

# Вывод

После лабораторной работе я познакомился с моделью рекламной компании и получил навыки по построению график этой модели.
