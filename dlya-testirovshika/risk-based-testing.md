---
description: или тестирование на основе рисков
---

# Risk Based Testing



здесь очень много расплывчато написанных статей, постараюсь сделать краткую выжимку на основе своего опыта.&#x20;

Какие бывают риски:

1. риски инфраструктурные(функциональные), например, когда какой-то из модулей внешней системы интегрирован в нашу систему, и он может отказать, тут нужно не забыть о безопасности(инъекциях, скриптах, И так далее),
2. риски основанные на бизнес требованиях, например, пользовательский сценарий выглядит очень запутанным/непрозрачным/долгим или просто непонятно, как по нему идти,
3. от себя добавлю - коммерческие риски, например, не работающая система оплаты товара, может принести очень большие потери бизнесу, а так же атомный взрыв в поддержке,

Это важно, но нужно переформулировать:\
Перед тем, как идти со списком рисков к другим участникам команды, нужно понять, проблема характерна для тестовой среды или для продакшена. Потому что проблемы тестовой среды нужно решать силами тестировщиков, или может быть привлечь девопса.

Теперь, со списком рисков, которые есть на продакшионе -> идем определять их приоритеты с командой, продактом, др заинтересованным лицом.&#x20;

Далее, в зависимости от приоритетов, и того, где находится место подверженное рискам мы решаем каким именно тестированием его покрыть(юнит/интеграционное/приемочное). И покрываем, и обязательно следим, чтобы этот тест проверялся ПРИ КАЖДЫХ ИЗМЕНЕНИЯХ КОДА.&#x20;

Если не всегда удается избежать рисков, стоит хотя бы подумать о заглушке, о срабатывании которой нас оповестит мониторинг. Те, если платежная система все-таки не работает, тк апи у банка отвалилось, стоит предусмотреть заглушку "у нас возникла проблема, мы скоро ее починим", таким образом мы уменьшим волну негатива и обращений в службу поддержки, и благодаря алерту узнаем о проблеме.&#x20;


