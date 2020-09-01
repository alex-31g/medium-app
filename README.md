project/series/angular-i-ngrx-pishem-realnyj-proekt-s-nulya

# 1. Подготавливаем проект

Проверить установлен ли *nodejs* и *npm* и узнать их версии:
`node -v`
`npm -v`

Описание, как удалить старую версию *nodejs* и *npm*:
https://stackoverflow.com/questions/20711240/how-to-completely-remove-node-js-from-windows

Установка/обновление *angular*:
`npm install -g @angular/cli`

Узнать версию *angular*:
`ng --version`

Создание нового проекта с флагами, которые добавят роутинг, scss и уберут тесты https://angular.io/cli/new:
`ng new medium-app --routing=true --style=scss --skipTests=true`

Запуск проекта: 
`npm start` 

Так как нам нужен абсолютно чистый проект, то:
- удаляем весь существующий код из *app.component.html*
- удаляем существующую переменную *title* из *app.component.ts*

# 2. Почему нам нужен NgRx?

**Redux** — js-библиотека, предназначенная для управления состоянием приложения. 
Чаще всего используется в связке с *React* или *Angular* для разработки клиентской части. 
Содержит ряд инструментов, позволяющих значительно упростить передачу данных хранилища через контекст.

**NgRx** (https://ngrx.io/docs) - js-библиотека, реализует принцип работы *Redux* для *Angular*. 
Главная цель *NgRx* - централизовать и сделать максимально понятным управление всеми состояниями приложения.
Цель достигается благодаря заложенным в библиотеке принципам:
-	Наличие единственного источника данных о состоянии - хранилища (store);
-	Доступность состояния только для чтения;
-	Изменение состояние осуществляется только через действия (actions), которые обрабатываются редюсерами (reducer), представляющими собой чистые функции.

# 3. Планируем структуру проекта

Каждая отдельная страница - это отдельный модуль, который хранится в *src/app*.
Например, имеем 2 страницы *article* и *auth* - это значит, что создаем 2 директории *article* и *auth*:

```js
/src
	/app
		app.component.html
		app.component.scss
		app.component.ts
		app.module.ts

		/article
			article.module.ts

		/auth
			auth.module.ts
```

Внутри каждого модуля, создаем директорию *components*, в которой будут храниться компоненты в отдельных директориях.
Например, модуль *article* имеет директорию *components*, которая в свою очередь имеет вложенные директории, которые и являются компонентами:
- *article* - главный компонент модуля article, поэтому именуем так же как и модуль
- *comments*

```js
/src
	/app

		/article
			article.module.ts

			/components
				/article
					article.component.html
					article.component.scss
					article.component.ts
				/comments
					comments.component.html
					comments.component.scss
					comments.component.ts

		/auth
			auth.module.ts
```

Далее внутри каждого модуля необходимо создать:
- директорию *services* - для хранения сервисов, которые относятся к данному модулю. Главный сервис именуется как так же, как модуль
- директорию store - куда мы будем помещать все, что относится к NgRx
- директорию types - для хранения типов и интерфейсов модуля

```js
/src
	/app

		/article
			article.module.ts
			/components

			/services
				article.service.ts

			/store

			/types
				article.interface.ts
```

Теперь поговорим о вещах, которые мы хотим переиспользовать в разных местах (shareble). 
Сперва возьмем **компоненту**, которую мы хотим сделать shareble. 
Так просто поместить её в папку *shared* нельзя, поскольку компоненты не могут существовать сами по себе, они должны быть зарегистрированы в каком-то модуле. 
Поэтому shareble-компоненты должны быть модулями и мы помещаем их в директорию *shared --> modules*.
Например у нас есть shareble-модуль *feed*, который нужно использовать на двух страницах одновременно. Он имеет точно такую же структуру, как и любой другой модуль-страница:

```js
/src
	/app

		/article

		/shared
			/modules
				/feed
					/components
					/services
					/store
					/types
					feed.module.ts
```

**Сервисы** и **типы** не регистрируем ни на каком модуле. Мы просто кладем их в папку *shared*, а регистрируем их в том модуле, где хотим использовать.
Например, если мы используем сервис на двух страницах, то его нужно поместить в *shared --> services*:

```js
/src
	/app

		/article

		/shared
			/modules
				/feed

			/services
			
			/types
```



		  