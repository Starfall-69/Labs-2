
МИНИСТЕРСТВО НАУКИ  И ВЫСШЕГО ОБРАЗОВАНИЯ РОССИЙСКОЙ ФЕДЕРАЦИИ  

Федеральное государственное автономное образовательное учреждение высшего образования  

"КРЫМСКИЙ ФЕДЕРАЛЬНЫЙ УНИВЕРСИТЕТ им. В. И. ВЕРНАДСКОГО"  

ФИЗИКО-ТЕХНИЧЕСКИЙ ИНСТИТУТ  

Кафедра компьютерной инженерии и моделирования
<br/></br>



### Отчет по лабораторной работе №2 </br> по дисциплине "Программирование"
<br/>

студента 1 курса группы ИВТ-б-о-191(1)  
Гринь Татьяны Станиславовны </br>
направления подготовки 09.03.01 " Информатика и вычислительная техника"  
<br/>

<table>
<tr><td>Научный руководитель<br/> старший преподаватель кафедры<br/> компьютерной инженерии и моделирования</td>
<td>(оценка)</td>
<td>Чабанов В.В.</td>
</tr>
</table>
<br/><br/>
​
Симферополь, 2019


__Цель:__

1) Овладеть практическими навыками разработки и программирования вычислительного процесса циклической структуры;
2) Сформировать навыков программирования алгоритмов разветвляющейся структуры;
3) Изучить операторы ветвления. Особенности использования полной и сокращенной формы оператора if и тернарного оператора.

__Ход работы:__

1) Для выполнения поставленной задачи напишем программу которая для функции *__f(x)__* на интервале __x ∈ [хнач; xкон]__:

* выводит в консоль значения функции *__f(x)__* с шагом __dx__;
* определяет максимальное и минимальное значение функции(__fmin__, __fmax__).

 Для начала реализуем ввод параметров __a__,__b__, начала и конца интервала __xn__, __xk__ и шага __dx__. 
 
 Формула которая нам дана изображена на 
(*рис.1*)
 
![](http://cpp.codelearn.ru/lab/lab2pic/pic1.png)</br>


  *рис.1 формула* 
 </br>
 
 Программа будет иметь следующий вид:
 ```
 
#include <iostream>
#include<cmath> 
using namespace std;

int main()
{
  double xn, xk, dx, fx,a,b;// параметры вводимые пользователем
  double fmin, fmax,  eps=pow(10,-15);// максимальное и минимальное значение функции

  cout << " a = "; // ввод параметра a
  cin >> a;
  cout << " b = ";// ввод параметра b
  cin >> b;
  cout << " xn = ";// ввод значения начала диапозона
  cin >> xn;
  cout << " xk = ";// ввод значения конца диапозона
  cin >> xk;
  cout << " dx = ";// ввод шага 
  cin >> dx;

  if (xk < xn) { // защита от дурака
    xk += xn;
    xn = xk - xn;
    xk = xk - xn;
  }

  while (xn<xk||abs(xn-xk)<eps) { // цикл для записи начального згачения fmin, fmax
    if (xn < a||abs(xn-a)<eps) {
      fmin = exp(xn) / (3 + sin(xn));
      fmax = fmin;
      break;
    }
    else if (a < xn && xn < b) {
      if (xn > 0) {
        fmin = log(xn) + xn * xn;
        fmax = fmin;
        break;
      }
    }
    else {
      fmin = 1 + sin(-xn);
      fmax = fmin;
      break;
    }
    xn += dx;
  }

  
  if (xn > xk) { // условие на проверку лежит ли диапозон в ОДЗ

    cout << " not exist\n\n"; 
  }
  else { 

    cout << "\n\n";

    while (xn < xk||abs(xn-xk)<eps) { // цикл вычисления значений функции с шагом dx
      if (xn < a||abs(xn-a)<eps) { 

        fx = exp(xn) / (3 + sin(xn));// вычисление по формуле
        if (fmin > fx) { fmin = fx; } // сравнение fmin и значения функции
        if (fmax < fx) { fmax = fx; } // сравнение fmax и значения функции
        cout << "  x =" << xn << "\n"; 
        cout << "  y =" << fx << "\n\n";
      }
      else if (a < xn && xn < b) {
        if (xn > 0) { // проверка на вхождение в ОДЗ

          fx = log(xn) + xn * xn;
          if (fmin > fx) { fmin = fx; }
          if (fmax < fx) { fmax = fx; }
          cout << "  x =" << xn << "\n";
          cout << "  y =" << fx << "\n\n";
        }
        else {
          cout << " not exist \n\n";
        }
      }
      else {
        fx = 1 + sin(-xn);
        if (fmin > fx) { fmin = fx; }
        if (fmax < fx) { fmax = fx; }
        cout << "  x =" << xn << "\n";
        cout << "  y =" << fx << "\n\n";
      }

      xn += dx;
    }
    cout << " fmin =" << fmin << "\n";
    cout << " fmax =" << fmax << "\n";
  }
  return 0;
}

 ```
 Результаты вычислений программы при __a__=0.7, __b__=1.2, начала и конца интервала __хнач__ = 0.5, __xкон__ = 1.5 и шага __dx__ = 0.05 представлены в таблице.
 <table>
 <tr>
  <td>№</td>
  <td><i>x</i></td>
  <td><i>f(x)</i></td>
 </tr>
 <tr>
  <td>1</td>
  <td><i>0.5</i></td>
  <td><i>0.473849</i></td>
 </tr>
 <tr>
  <td>2</td>
  <td><i>0.55</i></td>
  <td><i>0.492026</i></td>
 </tr>
 <tr>
  <td>3</td>
  <td><i>0.6</i></td>
  <td><i>0.511165</i></td>
 </tr>
 <tr>
  <td>4</td>
  <td><i>0.65</i></td>
  <td><i>0.531329</i></td>
 </tr>
 <tr>
  <td>5</td>
  <td><i>0.7</i></td>
  <td><i>0.552588</i></td>
 </tr><tr>
  <td>6</td>
  <td><i>0.75</i></td>
  <td><i>0.274818</i></td>
 </tr><tr>
  <td>7</td>
  <td><i>0.8</i></td>
  <td><i>0.416856</i></td>
 </tr>
  <tr>
  <td>8</td>
  <td><i>0.85</i></td>
  <td><i>0.559981</i></td>
 </tr>
  <tr>
  <td>9</td>
  <td><i>0.9</i></td>
  <td><i>0.704639</i></td>
 </tr>
  <tr>
  <td>10</td>
  <td><i>0.95</i></td>
  <td><i>0.851207</i></td>
 </tr><tr>
  <td>11</td>
  <td><i>1</i></td>
  <td><i>1</i></td>
 </tr>
 <tr>
  <td>12</td>
  <td><i>1.05</i></td>
  <td><i>1.15129</i></td>
 </tr>
 <tr>
  <td>13</td>
  <td><i>1.1</i></td>
  <td><i>1.30531</i></td>
 </tr>
 <tr>
  <td>14</td>
  <td><i>1.15</i></td>
  <td><i>1.46226</i></td>
 </tr>
 <tr>
  <td>15</td>
  <td><i>1.2</i></td>
  <td><i>0.0679609</i></td>
 </tr>
 <tr>
  <td>16</td>
  <td><i>1.25</i></td>
  <td><i>0.0510154</i></td>
 </tr>
 <tr>
  <td>17</td>
  <td><i>1.3</i></td>
  <td><i>0.0364418</i></td>
 </tr>
 <tr>
  <td>18</td>
  <td><i>1.35</i></td>
  <td><i>0.0242766</i></td>
 </tr>
  <tr>
  <td>19</td>
  <td><i>1.4</i></td>
  <td><i>0.0145503</i></td>
 </tr>
 <tr>
  <td>20</td>
  <td><i>1.45</i></td>
  <td><i>0.00728701</i></td>
 </tr>
 <tr>
  <td>21</td>
  <td><i>1.5</i></td>
  <td><i>0.00250501</i></td>
 </tr>
 <tr>
  <td></td>
  <td><i>fmin = 0.00250501</i></td>
  <td><i>fmax = 1.46226</i></td>
 </tr>
 </table> 
 </br>
 
 2) График представлен на рисунке *(рис.2)*</br>
![](https://raw.githubusercontent.com/Starfall-69/Labs-2/master/%D0%93%D0%A0%D0%90%D0%A4%D0%98%D0%9A.PNG)
 </br> 

*рис.2 График функций с точками min max.*
 
 На графике видно что точка максимума вычисленная с помощью программы не попадает в максимум функции это последствие того что шаг не попадает в эту точку чтобы ближе приблизиться к максимуму потребуеться выбрать шаг меньше.
 
 **Вывод:**
 В ходе работы я научился работать с циклом, обрела навыки программирования алгоритмов разветвляющейся структуры. 
 
 
 
 
 
 
 