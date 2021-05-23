## Практическая работа 0: Тестовый проект на React

## Начало работы

В рамках данной практической работы необходимо создать ToDo приложение.

Используемые технологии:

1. React (create-react-app)
2. CSS
3. axios
4. browser locale storage
5. react-router

## Создание базового приложения с помощью create-react-app

Для того чтобы создать приложение на react:

`npx create-react-app practice-0`\
`cd practice-0`\
`npm start`

Чтобы писать код используя React, необходимо знать некоторые базовые концепции из мира React:

1. [Привет, мир](https://ru.reactjs.org/docs/hello-world.html)
2. [Знакомство с JSX](https://ru.reactjs.org/docs/introducing-jsx.html)
3. [Рендеринг элементов](https://ru.reactjs.org/docs/rendering-elements.html)
4. [Компоненты и пропсы](https://ru.reactjs.org/docs/components-and-props.html)
5. [Обработка событий](https://ru.reactjs.org/docs/handling-events.html)
6. [Условный рендеринг](https://ru.reactjs.org/docs/conditional-rendering.html)
7. [Списки и ключи](https://ru.reactjs.org/docs/lists-and-keys.html)
8. [Формы](https://ru.reactjs.org/docs/forms.html)
9. [Подъём состояния](https://ru.reactjs.org/docs/lifting-state-up.html)
10. [Использование хука состояния](https://ru.reactjs.org/docs/hooks-state.html)
11. [Использование хука эффекта](https://ru.reactjs.org/docs/hooks-effect.html)

## Подключение Redux

Основная идея Redux предоставить глобальный store, к которому мы сможем получать доступ из любой части нашего приложения.

1. Необходимо установить Redux

```npm install react-redux```

2. Создать reducers, actions, action types, selectors

  - создать папку ```src/redux```, в которой будут храниться все необходимые для редакса конструкции

  - создать слудущие js файлы ```src/redux/actions.js```, ```src/redux/actionTypes.js```, ```src/redux/selectors.js```, ```src/redux/store.js```, ```src/redux/reducers.js```

Рассмотрим пример использования Redux. Добавим в Redux свойство user, которое будет хранить в себе объект с именем и фамилией пользователя. Имя и фамилия будут задаваться с помощью двух инпутов.

***src/redux/actionTypes.js***

```export const SET_USER = "SET_USER";```

***src/redux/actions.js***

```
import { SET_USER } from "./actionTypes";

export const setUser = userData => ({
  type: SET_USER,
  payload: {
    name: userData.name,
    surname: userData.surname,
  }
});
```

***src/redux/selectors.js***

```
export const getUser = store => store.user;
```

***src/redux/reducers.js***

```
import { SET_USER } from "./actionTypes";

const initialState = {
  user: {
    name: "",
    surname: "",
  }
};

export default function(state = initialState, action) {
  switch (action.type) {
    case SET_USER: {
      const { name, surname } = action.payload;
      return {
        ...state,
        user: {
          name,
          surname,
        }
      }
    }
    default: {
      return state;
    }
  }
}
```

***src/redux/store.js***

```
import { createStore } from "redux";
import rootReducer from "./reducers";

export default createStore(rootReducer);
```

3. Подключить Redux к приложению

index.js (файл, который генерируется автоматически, при создании приложения с помощью ```create-react-app```)

```
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

import { Provider } from 'react-redux';
import store from './redux/store';

const rootElement = document.getElementById('root')
ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  rootElement
)
```

4. Проверить результат с помощью Redux dev tools (https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd?hl)

- Подключить Redux dev tools в приложении

```
import { createStore } from "redux";
import rootReducer from "./reducers";

export default createStore(
  rootReducer,
  window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__(),
);
```

- Проверить результат

<!-- ![alt text]("./assets/Redux dev tools.png") -->
[logo]: ./assets/redux-dev-tools.png "Logo Title Text 2"