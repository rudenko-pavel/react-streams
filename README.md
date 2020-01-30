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

## ********************** *** preparing project *** ****************************** (look up) ##

	8. Create Components:
		- `src/components/streams/StreamList`
		- `src/components/streams/StreamCreate`
		- `src/components/streams/StreamEdit`
		- `src/components/streams/StreamShow`
		- `src/components/streams/StreamDelete`
			import React from "react";
			const StreamCreate = () => {
			  return <div>StreamCreate</div>;
			};
			export default StreamCreate;
	
	9. 	Edit `src/components/App.js`:
		##import Components:
		import StreamCreate from "./streams/StreamCreate";
		import StreamDelete from "./streams/StreamDelete";
		import StreamEdit from "./streams/StreamEdit";
		import StreamList from "./streams/StreamList";
		import StreamShow from "./streams/StreamShow";
	
	10. Edit `src/components/App.js`:
		##Create paths to Components
		import { HashRouter, Route } from 'react-router-dom';
		...
		  return (
			<div className="ui container">
			  <HashRouter>
				<div>
				  <Route path="/" exact component={StreamList} />
				  <Route path="/streams/new" exact component={StreamCreate} />
				  <Route path="/streams/edit" exact component={StreamEdit} />
				  <Route path="/streams/delete" exact component={StreamDelete} />
				  <Route path="/streams/show" exact component={StreamShow} />
				</div>
			  </HashRouter>
			</div>
		  );
		  
	11. Create always visible Components
		## Component is not listed inside HashComponent - 100% is visible always
		`src/components/Header`:
		import React from "react";
		const Header = () => {
		  return (
			<div className="ui secondary pointing menu">
			  <div className="right menu">Header</div>
			</div>
		  );
		};
		export default Header;

	12. Edit `src/components/App.js`:
		##import Components:
		import Header from "./Header";
		...
		  return (
			<div className="ui container">
			  <Header />
			  <HashRouter>
			  ...
			  
	13. Edit `src/components/Header`:
		## add links to menu
		import { Link } from "react-router-dom";
		...
		<Link to="/" className="item">Streamer</Link>
		<div className="right menu">
			<Link to="/" className="item">All streams</Link>
		</div>

	14. You should not use <Link> outside a <Router>
		## как использовать <Link> снаружи <Router> ?
		Edit `src/components/App.js`:
		## переносим все внутрь <Router>
		  return (
			<div className="ui container">
			  <HashRouter>
				<div>
				  <Header />
				  
	



