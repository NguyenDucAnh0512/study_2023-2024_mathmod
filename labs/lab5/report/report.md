---
## Front matter
title: "Отчёт по лабораторной работе №5"
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

Изучаем модель хищник-жертра и построим график модели с помощью Scilab.

# II. Задание

Для модели «хищник-жертва»:

$$
\begin{cases} \frac{dx}{dt}=-0.24x(t)+0.044x(t)y(t)\\ \frac{dy}{dt}=0.44y(t)-0.024x(t)y(t) \end{cases}
$$

Постройте график зависимости численности хищников от численности жертв,
а также графики изменения численности хищников и численности жертв при
следующих начальных условиях: $x_0=4; y_0=10$ Найдите стационарное
состояние системы.

# III. Выполнение задания

## 1. С помощью Scilab построим график модели «хищник-жертва»

В Scilab мы задаём коеффициенты, соответствующие с заданием:

``` Julia
a= 0.24; // коэффициент естественной смертности хищников
b= 0.44; // коэффициент естественного прироста жертв
c= 0.044; // коэффициент увеличения числа хищников
d= 0.024; // коэффициент смертности жертв
```

Затем задаём функцию модели:

``` Julia
function dx=syst2(t, x)
dx(1) = -a*x(1) + c*x(1)*x(2);
dx(2) = b*x(2) - d*x(1)*x(2);
endfunction
```

После этого задаём начальные условия модели, и интервал с шагом:

``` Julia
t0 = 0;
x0=[4;10]; //начальное значение x и у (популяция хищников и популяция жертв)
t = [0: 0.1: 400];
```

Решаем дифференциальные уравнеия:

``` Julia
y = ode(x0, t0, t, syst2);
n = size(y, "c");
for i = 1: n
y2(i) = y(2, i);
y1(i) = y(1, i);
```
И построим график модели с помощью кодами:

* Построение графика колебаний изменения числа популяции хищников:

``` Julia
plot(t,y1);
```
Результат:

![График колебаний изменения числа популяции хищников](https://drive.google.com/uc?id=1skJVHcm4rb_B7l5yp--00bhOKI0V4pXm)

* Построение графика колебаний изменения числа популяции жертра:

``` Julia
plot(t,y2);
```
Результат:

![График колебаний изменения числа популяции жертра](https://drive.google.com/uc?id=1t-RfZ2Wv6eLSBia-u2Gu7qAsYzJxWe3w)

* Построение графика зависимости изменения числености хищников от изменения числености жертра:

``` Julia
plot(y1,y2);
```
Результат:

![График зависимости изменения числености хищников от изменения числености жертра](https://drive.google.com/uc?id=10_zMW82sN2_cmkljDIKYCJ5wrOixxDT1)

## 2. Наидём стационарное состояние системы

$$
\begin{cases} \frac{dx}{dt}=-0.24x(t)+0.044x(t)y(t)\\ \frac{dy}{dt}=0.44y(t)-0.024x(t)y(t) \end{cases}
$$

С этой системы мы получим коеффициенты: $a=0.24;b=0.044;c=0.44;d=0.024$

Стационарное состояние системы будет в точке:

$$
\begin{cases} x_0=\frac{0.24}{0.044} \approx 5.45\\ y_0=\frac{0.44}{0.024} \approx 18.33 \end{cases}
$$

# IV. Вывод

После лабораторной работы я познакомился с моделей хищник-жертва и получил навыки по построению графика модели.