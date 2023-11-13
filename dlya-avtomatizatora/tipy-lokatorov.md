---
description: Локатор = или != Селектору?
---

# Типы локаторов

Что такое локатор?

Локатор это обычный текст, который идентифицирует себя как элемент DOM-a страницы. Другими словами, локатор это то, что позволяет найти тот или иной элемент на странице.

В случае css, локатор это набор уникальных атрибутов элемента, в случае xpath это путь по DOM-у, к элементу.

DOM (от англ. Document Object Model — «объектная модель документа») - это независящий от платформы и языка программный интерфейс, позволяющий получить доступ к содержимому HTML, XHTML, XML - документов, а так же изменять содержимое, структуру и оформление таких документов.&#x20;

или

DOM страницы - это HTML-код, написанный человеком или сгенерированный фреймворком, который преобразуется браузером в DOM. Те набор объектов, где каждый объект это html-тег.

Есть очень много видов локаторов, чаще всего используются вот эти:

* имя элемента
* id
* классы
* кастомные атрибуты
* родители и дети элементов
* ссылки



Состав элемента или html-тега

<figure><img src="../.gitbook/assets/Screenshot 2023-11-13 at 15.46.23.png" alt="" width="375"><figcaption></figcaption></figure>





Как найти локатор? Будет ли он уникальным? Почему может не подойти?

<figure><img src="../.gitbook/assets/Screenshot 2023-11-13 at 15.27.23.png" alt=""><figcaption><p><mark style="color:purple;">Отсюда можно взять уникальными id и name, title и placeholder кажутся сомнительными для использования как локатор.</mark></p></figcaption></figure>

<figure><img src="../.gitbook/assets/Screenshot 2023-11-13 at 15.29.09.png" alt=""><figcaption><p><mark style="color:purple;">Здесь ситуация другая, id кажется распространенным, а вот class - подходит, достаточно уникальный</mark></p></figcaption></figure>

Что же важно понять:

1\) локатор обязательно должен быть уникальным, иначе тест выберет первый подходящий, или просто упадет от обилия вариантов, такие как class, id, name(не факт, но надеюсь),

2\) локатор должен быть надежным, понятным, читаемым, поэтому не очень подходят:\
\- не стоит использовать title/subtitle/placeholder и другие элементы с текстом(не важно на каком языке), тексты часто меняются, а значит и тесты такие становятся не очень надежными,\
\- не стоит использовать type, потому что он не передает смысла локатора. \
Хороший пример, когда у нас есть поле для ввода пароля и ввода подтверждения пароля, у обоих локаторов будет type="password", и да, все символы заменятся на \*\*\*, но смысл теста останется непонятен.



А что по css?

В основном, будем использовать id и class. рассмотрим на примере&#x20;

```
class="btn-block btn btn-primary submit-button btn-block"
```

Как можно догадаться

* btn-block
* btn
* btn-primary
* submit-button
* btn-block

это все классы нашей кнопочки, и у каждого класса есть своя задача, размер кнопки, цвет кнопки, И так далее.&#x20;

Наличие более одного класса(в значении атрибута) внутри атрибута, говорит о том, что он комбинированный, бывают и комбинированные атрибуты, кроме классов. Значит, классы для одного элемента могут быть не уникальны. \
Например, класс кнопки регистрации выглядит вот так:

```
class="btn-block btn btn-primary registration-button btn-block"
```

те **registration-button** и **submit-button** различаются, остальное - идентично.



Читабельность локатора

```
[class=”btn-block btn btn-primary submit-button btn-block”]
или
btn-block.btn.btn-primary.submit-button.btn-block
```

для того, чтобы сократить еще, в питоне можно воспользоваться срезом и искать локатор в подстроке\[3]

<pre><code>[class*=”btn-block”]
[class*=”submit-button”]
[class*=”btn-block btn”]
[class*=”btn btn-primary”]
[class*=”primary submit”]
<strong>[class*=”submit”]
</strong>[class*=”sub”]
</code></pre>

можно попробовать варианты c сочетанием 2х классов и с .

```
.submit-button = [class*=”submit-button”]
.btn = [class*=”btn”]
.btn-block = [class*=”btn-block”]

button[class*=”submit-button”] = button.submit-button
button[class*=”btn”] = button.btn
button[class*=”btn”][class*=“submit-button”] = button.btn.submit-button
button[class*=”submit”]
```

Иногда, для понятности локатора, стоит комбинировать несколько локаторов.



Кастомные атрибуты - в некоторых компаниях разработчики фронтенда делают специальные кастомные атрибуты для автотестов с тегом qa. Это один из надежнейших способов, сохранить тесты в целости и сохранности.&#x20;



Поиск по XPath

XPath - это путь от элемента к элементу. Если вспомнить, что html страница это дерево \<div>-ов, \<span>-ов и прочих, или вспомнить про аналогию в виде дерева каталогов и использования cd и ls, то можно примерно представить, а что такое путь до папки, или в нашем случае путь до локатора.&#x20;

```
//div/div/button/span
//div//span
или
//*[@aria-label="Авторизация"]
//*[@type="submit"]
```

можно переходить от дочернего элемента к родителю, через "..", опять же вспоминаем cd ..,

```
//*[@href=”/doLogin”]/../..//*[@href=”/doReg”]
```



Немного про синтаксис:

1\) знаем название элемента - пишем span/button, не знаем, ставим - \*

```
//*[@href=”/doReg”] или //span[@href=”/doReg”]
//*[@name=”regButton”] или //button[@name=”regButton”]
```

2\) атрибуты всегда с собачкой -> @,

3\) использование **following-sibling** и **preceding-sibling,** или переходы по смежным осям\
ищем кнопку Войти чз кнопку Регистрации\
`//*[@name=”regButton”]/following-sibling::*[@name=”loginButton”]`

ищем кнопку Регистрации чз Войти\
`//*[@name=”loginButton”]/preceding-sibling::*[@name=”regButton”]`

4\) воспользуемся contains\
`//*[contains(@aria-label, "телефона")]`

5\) поиск по тексту на кнопке,\
в таком виде текст ищется по полному совпадению\
`//*[text()="или войти через"]`\
если же изменить на\
`//*[contains(text(),"войти")]`\
`то будет искать по совпадениям`



Гибкие локаторы - это сочетание xpath и css в локаторе. Например

```
//*[contains(text(), “Название издания”)]
/ancestor::*[contains(@data-component, "OfferCard")]
//*[contains(@data-component, "Purchase")]
```



Статья источник -> [https://habr.com/ru/companies/skyeng/articles/588282/](https://habr.com/ru/companies/skyeng/articles/588282/)

еще классная статья -> [https://testerslittlehelper.wordpress.com/2016/07/10/real-xpath/?utm\_content=id\&utm\_source=telegram\&utm\_campaign=smm\_posts\&utm\_term=\&utm\_medium=kuku](https://testerslittlehelper.wordpress.com/2016/07/10/real-xpath/?utm\_content=id\&utm\_source=telegram\&utm\_campaign=smm\_posts\&utm\_term=\&utm\_medium=kuku)

Книга по css селекторам -> [https://appletree.or.kr/quick\_reference\_cards/CSS/CSS%20selectors%20cheatsheet.pdf](https://appletree.or.kr/quick\_reference\_cards/CSS/CSS%20selectors%20cheatsheet.pdf)
