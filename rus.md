# Использование свойства pointer-events с медиа-запросами

Все мы знаем, что медиа-запросы позволяют нам управлять положением элементов,
мы даже можем [анимировать изменение значений свойств при выполнении условий
медиа-запросов][1]. Чуть менее стандартное применение медиа-запросов — это
использование их вместе со свойством [pointer-events][5]. Используя CSS-
свойство `pointer-events`, мы можем изменять функциональность приложения,
основываясь на выполнении условий медиа-запроса.

Пример можно увидеть в текущем варианте MDN. Слева вы видите содержимое
статьи, справа вы видите оглавление:

![Новая версия дизайна MDN для браузеров настольных компьютеров][2]

При выполнении условий медиа-запроса для планшетов оглавление должно
переместиться вверх и оказаться над статьей:

![Новая версия дизайна MDN для планшетов][3]

В браузерах настольных компьютеров при клике на заголовке оглавления ничего
происходить не должно. На планшете или другом мобильном устройстве оглавление
должно сворачиваться вверх при клике на заголовке, чтобы освободить критически
важное место и предотвратить (по возможности) необходимость постоянной
прокрутки статьи. Мне не хотелось использовать JavaScript для включения и
отключения этого функционала, потому что... ну... это было бы неэффективным
решением. Вместо этого я включил свойство `pointer-events` в медиа-запрос для
планшетов:

    /* по умолчанию обработка событий отключена */
    #toc .heading {
    	pointer-events: none;
    }
    #toc i {
    	display: none;
    }

    /* включаем этот функционал для планшетов! */
    @media only screen and (max-width: 760px) {
    	#toc .heading {
    		pointer-events: auto;
    	}
    	#toc i {
    		display: block;
    	}
    }

Я просто обожаю свойство `pointer-events`, потому что кроме всего прочего оно
предотвращает срабатывание события клика, поэтому фрагмент JavaScript-кода,
который я использовал для [сворачивания и разворачивания][4], не выполняется. Я
бы не сказал, что я сделал что-то заумное, я просто хочу показать, что с
помощью медиа-запросов вы можете менять не только расположение элементов. Ну
и, конечно, то, что `pointer-events` — это очень круто!

[1]: http://davidwalsh.name/animate-media-queries
[2]: img/mdn-redesign-desktop.jpg "Новая версия дизайна MDN для браузеров настольных компьютеров"
[3]: img/mdn-redesign-tablet.jpg "Новая версия дизайна MDN для планшетов"
[4]: http://davidwalsh.name/css-slide
[5]: http://davidwalsh.name/pointer-events
