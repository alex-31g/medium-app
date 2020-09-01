project/series/angular-i-ngrx-pishem-realnyj-proekt-s-nulya

# 1. Подготавливаем проект

Проверить установлен ли *nodejs* и *npm* и узнать их версии:
` 
	node -v
	npm -v
`

Описание, как удалить старую версию node и npm:
https://stackoverflow.com/questions/20711240/how-to-completely-remove-node-js-from-windows

Установка/обновление angular:
` 
	npm install -g @angular/cli
	ng --version
`

Создание нового проекта с флагами, которые добавят роутинг и scss + уберут тесты https://angular.io/cli/new:
`ng new medium-app --routing=true --style=scss --skipTests=true`

Запуск проекта: 
`npm start` 

Так как нам нужен абсолютно чистый проект, то:
- удаляем весь существующий код из app.component.html
- удаляем существующую переменную title из app.component.ts

