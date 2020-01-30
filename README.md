# react
project: REACT-streams 

## ## ## ## lesson from www.udemy.com (chapter 16: Navigation with React Router)
	## получаем стримы с https://www.twitch.tv/ 
	## `RTMP` - Real Time Messaging Protocol Server 
	
	## Проект будет состоять из трех частей
		- клиентская часть (`CLIENT PORTION`)
		- 
		-
	## Задачи приложения:
		- (`point #1`) нужно иметь навигацию между страницами
		- нужно дать возможность юзеру логиниться/разлогиниваться (`Google log/off`)
		- нужно обрабатывать формы в Redux
		- необходимо освоить операции CRUD в REACT / REDUX.
				## `CRUD` - Creates Read Update Destroy
		- ошибки скорее всего произойдут! Нужна хорошая обработка ошибок.



## ## ## Instruction

# STEP 1 (`CLIENT PORTION`):
## preparation of project (Подготовка проекта)  
	1. console
		## создаем проект
		create-react-app client
		cd client
		npm start

	2. delete all files from `client/src`

# `point #1` - work with navigation
	3. Create `src/index.js`:
		import React from 'react';
		import ReactDOM from 'react-dom';
		import App from './components/App';
		ReactDOM.render( <App />, document.querySelector('#root'));

	4. Create `src/components/App.js`:
		import React from 'react';
		const App = () =>{
			return(<div>App</div>)
		}
		export default App;

	5. Add some css: 		// optional
		## console
			npm i --save semantic-ui-css
			npm i --save sass node-sass
		## Create files `src/index.scss`, `src/components/App.scss`
		## import `css`  
		5.1. Edit `src/index.js`:
			import 'semantic-ui-css/semantic.min.css';
			import './index.scss'; 
		5.2. Edit `src/components/App.js`:
			import './App.scss'; 
			return(<div className="ui container">App</div>)

	6. console
		## добавляем библиотеку в зависимости:
		npm install --save react-router-dom

	7. 	### *** Extend ESLint configuration ***
		npm i eslint eslint-config-airbnb eslint-config-prettier eslint-plugin-jsx-a11y eslint-plugin-prettier eslint-plugin-react eslint-plugin-react-hooks eslint-plugin-simple-import-sort prettier --save-dev

		Edit `package.json`:
    	  "scripts": {
				"start": "react-scripts start",
				"build": "react-scripts build",
				"test": "react-scripts test",
				"eject": "react-scripts eject",
				"lint": "eslint . && flow"
			}

		add file `.eslintrc` to root directory
		npm run lint

## ********************** Extend ESLint configuration ****************************** (look up) ##










	7. Edit `src/components/App.js`:
		## import
		import { HashRouter, Route } from 'react-router-dom';
		...
		return(
			<div className="ui container">
				<HashRouter>
					<div>
						<Route path="/" exact  component={} /> 		// шаблон. Пока без ссылок
						<Route path="/" component={} />
					</div>
				</HashRouter>
			</div>
		)


