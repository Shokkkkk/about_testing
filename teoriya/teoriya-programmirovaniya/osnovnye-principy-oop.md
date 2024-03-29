# Основные принципы ООП

**Инкапсуляция** - вся информация, которая нужна для работы с конкретным объектом должна хранится внутри этого объекта.

Методы обновления этого объекта, тоже должны хранится внутри этого объекта. Для работы внешних объектов с выбранным объектом доступны только публичные методы и атрибуты.

!!! Этот принцип обеспечивает безопасность и целостность данных внутри класса из вне. Так же, помогает избежать случайных зависимостей, когда из-за изменений одного объекта, ломается что-то в другом.&#x20;



**Наследование** - каждый дочерний элемент класса, наследует методы и атрибуты родителя. Он может использовать их все, только часть, или вообще никакие.

Например, класс млекопитающие имеет\
\- атрибуты: рост, вес, волосатость,\
\- методы: есть, пить, спать,\
Класс хищники, отнаследованный от класса млекопитающие имеет\
\- атрибуты: рост, вес, волосатость, тип поедаемого мяса,\
\- методы: есть, пить, спать, охотится.



**Полиморфизм** - как полиамория, только полиморфизм, один и тот же метод, может работать по разному, в зависимости от того, какие параметры ему передали, и над каким объектом совершается действие.

Например, метод удаления можно вызвать для удаления Гиены 1 и удалится объект, а можно вызвать для класса Хищники и удалятся все хищники.
