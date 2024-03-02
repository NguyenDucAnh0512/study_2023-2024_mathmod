---
## Front matter
title: "Отчёт по лабораторной работе №4"
subtitle: "Вариант 12"
author: "Нгуен Дык Ань"

## Generic otions
lang: ru-RU
toc-title: "Содержание"

## Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

## Pdf output format
toc: true # Table of contents
toc-depth: 2
lof: false # List of figures
lot: false # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt
## I18n polyglossia
polyglossia-lang:
  name: russian
  options:
	- spelling=modern
	- babelshorthands=true
polyglossia-otherlangs:
  name: english
## I18n babel
babel-lang: russian
babel-otherlangs: english
## Fonts
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase,Scale=0.9
## Biblatex
biblatex: true
biblio-style: "gost-numeric"
biblatexoptions:
  - parentracker=true
  - backend=biber
  - hyperref=auto
  - language=auto
  - autolang=other*
  - citestyle=gost-numeric
## Pandoc-crossref LaTeX customization
figureTitle: "Рис."
tableTitle: "Таблица"
listingTitle: "Листинг"
lofTitle: "Список иллюстраций"
lotTitle: "Список таблиц"
lolTitle: "Листинги"
## Misc options
indent: true
header-includes:
  - \usepackage[T2B]{fontenc}
  - \usepackage{indentfirst}
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# I.Цель работы

Изучаем модель гармонических колебаний, решаем уравнения гармонического осциллятора и построим фазовый портрет с помощью Scilab

# II.Задание

Постройте фазовый портрет гармонического осциллятора и решение уравнения гармонического осциллятора для следующих случаев.

1. Колебания гармонического осциллятора без затуханий и без действий внешней силы $\ddot{x}+4x=0$

2. Колебания гармонического осциллятора c затуханием и без действий внешней силы $\ddot{x}+4\dot{x}+8x=0$

3. Колебания гармонического осциллятора c затуханием и под действием внешней силы $\ddot{x}+3\dot{x}+4x=5sin(2t)$

На интервале $t=[0;55]$ (шаг 0.05) с начальными условиями $x_{0}=0, y_{0}=-2$

# III. Выполнение задания

## 1. Колебания гармонического осциллятора без затуханий и без действий внешней силы $\ddot{x}+4x=0$

* Решать уравнеие $\ddot{x}+4x=0$

Характерическое уравнеие: $k^{2}+4=0$, решаем его, мы получим решения:

$$
\begin{cases} k_{1}=2i\\ k_{2}=-2i \end{cases}
$$

Поэтому мы получим общее решение: $x=(C_{1}cos(2t)+C_{2}sin(2t))$ (1)

Дифференцируем (1), получим: $\dot{x}=-C_{1}sin(2t)+C_{2}cos(2t)$

С помощью начальных условии $x_{0}=0, y_{0}=-2$, мы создаём систему уравнении, чтобы найти $C_{1}$ и $C_{2}$:

$$
\begin{cases} x(0)=0\\ \dot{x}(0)=-2 \end{cases} \Rightarrow \begin{cases} C_{1}*cos(0)+C_{2}sin(0)=0\\ -C_{1}sin(0)+C_{2}cos(0)=-2 \end{cases} \Rightarrow \begin{cases} C_{1}=0\\ C_{2}=-2 \end{cases}
$$

Таким образом, мы получим общее решение: $x=-2sin(2t)$ (2)

* Построить фазовый портрет гармонического осциллятора с помощью Scilab

Введём следующий код:
```c++
//x'' + w^2* x = 0
w2 = 4; //w - частота (w2 - это w^2)
g = 0; //g - затухание

// Введём функцию для решения
function dx=y(t, x)
dx(1) = x(2);
dx(2) = -w2 * x(1);
endfunction

//Точка, в которой заданы начальные условия
t0 = 0;
//Вектор начальных условий
x0 = [0; -2];
//Интервал на котором будет решаться задача
t = [0: 0.05: 55];

//Решаем дифференциальные уравнения и записываем решение в матрицу x
x = ode(x0, t0, t, y);
//Количество столбцов в матрице
n = size(x, "c"); //Переписываем отдельно
//x в y1, x' в y2
for i = 1: n
y1(i) = x(1, i);
y2(i) = x(2, i);
end
//Рисуем фазовый портрет: зависимость x(x')
plot(y1, y2);
//plot(t,y1); -фазовый портрет: зависимость x(t)
xgrid()
```
И мы получим результат:

![Фазовый портрет гармонического осциллятора первого случая в зависимость x(x')](https://drive.google.com/uc?id=18gic8pS-vxdxkrv_VZQOnnVKETBA8Tsc)

![Фазовый портрет гармонического осциллятора первого случая в зависимость x(t)](https://drive.google.com/uc?id=1zddyHVOTvWAaFXal9lhQtEYxZEI9g7Vb)

## 2. Колебания гармонического осциллятора c затуханием и без действий внешней силы $\ddot{x}+4\dot{x}+8x=0$

* Решать уравнеие $\ddot{x}+4\dot{x}+8x=0$

Характерическое уравнеие: $k^{2}+4k+8=0$, решаем его, мы получим решения:

$$
\begin{cases} k_{1}=-2+2i\\ k_{2}=-2-2i \end{cases}
$$

Поэтому мы получим общее решение: $x=e^{-2t}(C_{1}cos(2t)+C_{2}sin(2t))$ (3)

Дифференцируем (3), получим:

$\dot{x}=(e^{-2t}C_{1}cos(2t))'+(e^{-2t}C_{2}sin(2t))'$

$\dot{x}=-2e^{-2t}C_{1}cos(2t)-2e^{-2t}C_{1}sin(2t)-2e^{-2t}C_{2}sin(2t)+2e^{-2t}C_{2}cos(2t)$

$\dot{x}=-2e^{-2t}[(C_{1}-C_{2})cos(2t)+(C_{1}+C_{2})sin(2t)]$ (4)

С начальными условиями получим систему уравнении:

$$
\begin{cases} x(0)=0\\ \dot{x}(0)=-2 \end{cases} \Leftrightarrow \begin{cases} e^{-2*0}(C_{1}cos(2*0)+C_{2}sin(2*0))=0\\ -2e^{-2*0}[(C_{1}-C_{2})cos(2*0)+(C_{1}+C_{2})sin(2*0)] \end{cases}
$$

$$
\Leftrightarrow \begin{cases} C_{1}=0\\ -2(C_{1}-C_{2})=-2 \end{cases} \Leftrightarrow \begin{cases} C_{1}=0\\ C_{2}=-1 \end{cases}
$$

И мы получим решение: $x=-e^{-2t}sin(2t)$

* Построить фазовый портрет гармонического осциллятора с помощью Scilab

Введём следующий код:
```c++
//x'' + g* x' + w^2* x = 0
w2 = 8; 
g = 4;

// Введём функцию для решения
function dx=y(t, x)
dx(1) = x(2);
dx(2) = -w2 * x(1) - g * x(2);
endfunction

//Точка, в которой заданы начальные условия
t0 = 0;
//Вектор начальных условий
x0 = [0; -2];
//Интервал на котором будет решаться задача
t = [0: 0.05: 55];

//Решаем дифференциальные уравнения и записываем решение в матрицу x
x = ode(x0, t0, t, y);
//Количество столбцов в матрице
n = size(x, "c");//Переписываем отдельно
//x в y1, x' в y2
for i = 1: n
y1(i) = x(1, i);
y2(i) = x(2, i);
end
//Рисуем фазовый портрет: зависимость x(x')
plot(y1, y2);
//plot(t,y1); -фазовый портрет: зависимость x(t)
xgrid();
```

И мы получим результат:

![Фазовый портрет гармонического осциллятора второго случая в зависимость x(x')](https://drive.google.com/uc?id=1jq2NTKRjZatC9U0hFmRA0_baYT34gsoF)

![Фазовый портрет гармонического осциллятора второго случая в зависимость x(t)](https://drive.google.com/uc?id=1A21yICveFEEKvyr5gi4toz0HhLQX4v5W)

## 3. Колебания гармонического осциллятора c затуханием и под действием внешней силы $\ddot{x}+3\dot{x}+4x=5sin(2t)$

* Решать уравнеие $\ddot{x}+3\dot{x}+4x=5sin(2t)$

Сначала нам нужно решать однородные линейные дифференцирующие уравнения $\ddot{x}+3\dot{x}+4x=0$, чтобы найти общее решение однородного уравнения:

Характерическое уравнеие: $k^{2}+3k+4=0$, решаем его, мы получим решения:

$$
\begin{cases} k_{1}=\frac{-3+\sqrt{7}i}{2}\\ k_{2}=\frac{-3-\sqrt{7}i}{2} \end{cases}
$$

Мы получим общее решение однородного уравнения: 

$x=e^{-\frac{3}{2}t}(C_{1}cos(\frac{\sqrt{7}}{2}t)+C_{2}sin(\frac{\sqrt{7}}{2}t))$ (5)

Затем мы наидём частное решение неоднородного уравнения.

Видно, что $m=0, n=2, m \ne \alpha, n \ne \beta \Rightarrow$ решение имеет вид: 

$x=e^{mx}(Acos(nt)+Bsin(nt))$ (6)

Поставим $m=0 , n=2$ в (6), получим $x=Acos(2t)+Bsin(2t)$. Дифференцируем этот уравнение, получим:

$\dot{x}=-2Asin(2t)+2Bcos(2t)$

$\ddot{x}=-4Acos(2t)-4Bsin(2t)$

Поставим $\dot{x}$ и $\ddot{x}$ в уравнеие $\ddot{x}+3\dot{x}+4x=5sin(2t)$, получим:

$(-4Acos(2t)-4Bsin(2t))+3(-2Asin(2t)+2Bcos(2t))+4(Acos(2t)+Bsin(2t))=5sin(2t)$

$\Leftrightarrow 6Bcos(2t)-6Asin(2t) = 5sin(2t) \Leftrightarrow \begin{cases} A=-\frac{5}{6}\\ B=0 \end{cases}$

Так мы получим частное решение неоднородного уравнения: $x=-\frac{5}{6}cos(2t)$

Таким образом, общее решение неоднородного уравнения равно сумме общего решения однородного уравнения и частного решения неоднородного уравнения:

$x=e^{-\frac{3}{2}t}(C_{1}cos(\frac{\sqrt{7}}{2}t)+C_{2}sin(\frac{\sqrt{7}}{2}t))-\frac{5}{6}cos(2t)$ (7)

Чтобы найти конкретное значение $C_{1}$ и $C_{2}$, мы дифференцируем (7) и с начальными условиями, получим:

$\dot{x}=-\frac{e^{-\frac{3t}{2}}((9C_{2}+3\sqrt{7}C_{1})sin(\frac{\sqrt{7}t}{2})+(9C_{1}-3\sqrt{7}C_{2})cos(\frac{\sqrt{7}t}{2})-10e^{\frac{3t}{2}}sin(2t))}{6}$ (8)

От (7), (8) мы создаём систему уравнении:

$$
\begin{cases} x(0)=0\\ \dot{x}(0)=-2 \end{cases} \Leftrightarrow \begin{cases} C_{1}-\frac{5}{6}=0\\ 9C_{1}-3\sqrt{7}C_{2}=-2 \end{cases} \Leftrightarrow \begin{cases} C_{1}=\frac{5}{6}\\ C_{2}=\frac{19\sqrt{7}}{42} \end{cases}
$$

Общее решение неоднородного уравнения:

$x=e^{-\frac{3}{2}t}(\frac{5}{6}cos(\frac{\sqrt{7}}{2}t)+\frac{19\sqrt{7}}{42}sin(\frac{\sqrt{7}}{2}t))-\frac{5}{6}cos(2t)$

* Построить фазовый портрет гармонического осциллятора с помощью Scilab

Введём следующий код:
```c++
//x'' + g* x' + w^2* x = f(t)
w2 = 4;
g = 3;
//Правая часть уравнения f(t)
function f=f(t)
f = 5*sin(2*t);
endfunction

// Введём функцию для решения
function dx=y(t, x)
dx(1) = x(2);
dx(2) = -w2 * x(1) - g * x(2) - f(t);
endfunction

//Точка, в которой заданы начальные условия
t0 = 0;
//Вектор начальных условий
x0 = [0; -2];
//Интервал на котором будет решаться задача
t = [0: 0.05: 55];

//Решаем дифференциальные уравнения и записываем решение в матрицу x
x = ode(x0, t0, t, y);
//Количество столбцов в матрице
n = size(x, "c");//Переписываем отдельно
//x в y1, x' в y2
for i = 1: n
y1(i) = x(1, i);
y2(i) = x(2, i);
end
//Рисуем фазовый портрет: зависимость x(x')
plot(y1, y2);
//plot(t,y1); -фазовый портрет: зависимость x(t)
xgrid();
```
И мы получим результат:

![Фазовый портрет гармонического осциллятора третьего случая в зависимость x(x')](https://drive.google.com/uc?id=1CIkkURPDIpzl388VqbILvmuDFu46vfst)

![Фазовый портрет гармонического осциллятора третьего случая в зависимость x(t)](https://drive.google.com/uc?id=1LxUOISo7qbc3TA4317edLOAAhAUnBKs5)

# IV. Вывод

После лабораторной работы, я познакомился с моделей гармонических колебаний, получил навыки по решению уравнения гармонического осциллятора и приобрел построить фазовый портрет с помощью Scilab.