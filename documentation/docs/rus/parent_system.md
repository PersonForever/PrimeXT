---
sidebar_position: 6
---

# Парент-система

В PrimeXT имеется система родительских привязок (parent system), которая аналогично своему прототипу из Half-Life 2 позволяет прикреплять друг к другу неограниченное число объектов. Основной упор при этом делается на кинематические объекты, такие как двери, кнопки, поезда, лифты и прочие. Из уникальных возможностей присутствует переход иерархии сквозь уровни без потери функциональности и «разваливания» системы, что, например, имеет место в Half-Life 2, а также возможность форсированного прикрепления объекта средствами клиента (без учёта физики). Вторая особенность даёт мапперу возможность прикреплять непосредстенно к аттачментам NPC различные точечные объекты: спрайты, источники света, лазерные лучи, а в отдельно оговоренных случаях — модели.

Также система позволяет динамически отсоединять одни объекты из группы (с сохранением иерархии, разумеется), и присоединять их к другим, произвольным объектам. Прикрепление объектов достигается при помощи особого поля parent, где левел-дизайнеру следует указать targetname родителя. Точка с числом сразу после имени провоцируют игру на включение клиентской parent system, где число является номером аттачмента у родительской модели.

Клиентская parent system работает только для studio-моделей. Это означает что в качестве родителя могут выступать только такие модели, но не брашевые и не спрайтовые. В целях облегчения портирования карт из-под тулкита Spirit of Half-Life у поля parent есть псевдоним movewith, который выполняет те же самые действия.

## Ограничения системы

- Не все объекты могут быть корректно прилинкованы при помощи данной системы. Так, например, нежелательно прикреплять NPC с её помощью, поскольку это может вызывать проблемы с интерполяцией и в конечном итоге будет работать не так, как того ожидал левел-дизайнер. 
- Прикрепление игрока также недоступно, однако вы можете крепить какие-либо объекты к самому игроку через trigger_changeparent, указав в поле **New Parent** одно из двух: 
  - Ключевое слово `*locus` при условии, что trigger_changeparent был активирован при помощи trigger_once, trigger_multiple или trigger_inout, которые задел игрок (т. е. выступил в роли активатора) 
  - Ключевое слово `*player`
- Напрямую вписывать слово `*player` в поле parent нельзя, так как игрок заходит на сервер самым последним, когда все объекты уже скреплены между собой. 
- Статический свет (предрассчитанный компиляторами), не даёт эффекта при скреплении. Но вы можете использовать динамический свет, который будет передвигаться вместе с вашими объектами. 
- Некоторые объекты, которые имеют эффект только на клиенте, точно так же не смогут правильно работать. Это env_bubbles, env_rain, env_static, env_funnel и, возможно, func_mortar_field. 
