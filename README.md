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
		
## ********************************************************************************************************* ##
## ********************** *** preparing project *** ****************************** (look up) ##
## ********************************************************************************************************* ##

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
				  
## ********************************************************************************************************* ##
## ********************** *** completion of project preparation *** ****************************** (look up) ## 
## ********************************************************************************************************* ##	
	
## **************************************************************************************************** ##
					*** Handling Authentication with React (with REDUX) ***
## **************************************************************************************************** ##
	15. Set up an OAuth confirmation screen
		## console.developers.google.com - change Project - credentials (учетные данные) -  
		## OAuth confirmation (настроить окно запроса доступа) - credentials (учетные данные) - 
		## OAuth ClientID (Идентификатор клиента OAuth)
		## web application:
			- http://localhost:3000
			- http://rudenkopavel.com
		
		Идентификатор клиента: `47661926609-9ekpajmdn1p8p4146r88vae5q14cdu64.apps.googleusercontent.com`
		Секретный код клиента: `wFJ1K9w_-vgkvqkTb6Hb2ukG`

	16. Wiring Up the Google API Library
		- Edit `public/index.html`
		<head>
		...
			<script src="https://apis.google.com/js/api.js"></script>
		...
		</head>
	
	17. Create `src/components/GoogleAuth.js`:
		import React from "react";
		class GoogleAuth extends React.Component {
			render() {
				return <div>GoogleAuth</div>;
			}
		}
		export default GoogleAuth;
	
	18. Edit `src/components/Header.js`:
		## import:
		import GoogleAuth from "./GoogleAuth";	
	
	19. Edit `src/components/Header.js`:
		## Create an instanse of GoogleAuth
		...
		<Link to="/" className="item">All streams</Link>
        <GoogleAuth />
		...	
	
	20. Для использования REDUX, необходимо его добавть в проект
		console: 
			npm i --save redux react-redux
			npm i --save redux-thunk
	
	21. Create `src/actions/index.js`:
		## добавляем `actions`
		export const signIn = () => {
			return {
				type: "SIGN_IN"
			};
		};

		export const signOut = () => {
			return {
				type: "SIGN_OUT"
			};
		};	
	
	22. Create `src/reducers/index.js`
		## если нет данных для передачи, мы все-равно должны что-то передавать.
		## Поэтому или убираем `import reducers from './reducers';` или добавлем `dummy reducers`:
		import { combineReducers } from 'redux';
		export default combineReducers({
			dummyKey: 'replaceMe'
		});
		
	23. Edit `src/index.js`:
		import { Provider } from 'react-redux';
		import { createStore, applyMiddleware } from 'redux';
		import reducers from './reducers';
		import thunk from 'redux-thunk';

		const store = createStore(reducers, applyMiddleware(thunk));

		ReactDOM.render(
			<Provider store={store}>
				<App />
			</Provider>, 
			document.querySelector("#root")
		);
		
	24. Create `src/reducers/authReducer.js`:
		## `src/reducers/authReducer`:
		## `isSignedIn` - look at `src/components GoogkeAuth.js -> state`
		const INITIAL_STATE = {
			isSignedIn: null
		};

		export default (state = INITIAL_STATE, action) => {
			switch (action.type) {
				// see to `src/actions/index.js`
				case "SIGN_IN":
					return { ...state, isSignedIn: true };
				case "SIGN_OUT":
					return { ...state, isSignedIn: false };
				default:
					return state;
			}
		};	

	25. Edit `src/reducers/index.js`:
		## добавляем `reducers`
		import authReducer from "./authReducer";
		...
		export default combineReducers({
			auth: authReducer
		});

	## РАБОТА С `src/components/GoogleAuth.js`
	
	26. Edit `src/components/GoogleAuth.js`:
		import { connect } from "react-redux";
		import { signIn, signOut } from "../actions";
		...
		## поскольку у нас еще нет функции `mapStateToProps`, первым параметром передаем `null`
		export default connect(null,{ signIn, signOut})(GoogleAuth);
		
	
	27. Edit `src/components/GoogleAuth.js`:
		## Callback-функция `onAuthChange` возвращает bool-значение: true/false
		## Передаем в функцию аргумент и в зависимости от значения - будем вызывать различные `reducers`
		onAuthChange = (isSignedIn) => {
			if (isSignedIn){
				this.props.signIn();
			} else{
				this.props.signOut();
			}
		};

	28. Edit `src/components/GoogleAuth.js`:
		## инициализируем данные при первом отображении Компонента
		componentDidMount() {
			window.gapi.load('client:auth2');
		}
		
	29. Edit `src/components/GoogleAuth.js`:
		## добавляем в функцию второй аргумент - функцию, которая вызывается после того, как первый аргумент
		## был успешно загружен. Эта функция возвращает объект с данными `scope`, используя наш `ClientID` (п.33)
		componentDidMount() {
			window.gapi.load("client:auth2", () => {
				window.gapi.client.init({
					clientId:
					"47661926609-9ekpajmdn1p8p4146r88vae5q14cdu64.apps.googleusercontent.com",
					scope: "email"
				});
			});
		}
		
	30. Edit `src/components/GoogleAuth.js`
		## Продолжаем разрабатывать наш класс.
		## Какие-либо действия с полученным объектом, мы сможем делать только после того как его получим:
		window.gapi.client.init({
			clientId:
			"47661926609-9ekpajmdn1p8p4146r88vae5q14cdu64.apps.googleusercontent.com",
			scope: "email"
		}).then (() =>{	});
		
	31. Edit `src/components/GoogleAuth.js`
		## Определяем статус юзера (LogIn/ LogOut):
		.then(() => {
          this.auth = window.gapi.auth2.getAuthInstance();
        });	
		
	32. Edit `src/components/GoogleAuth.js`
		## выводим на экран статус:
		## для этого вводим переменную `isSignedIn`
		state = { isSignedIn: null };
		...
		.then(() => {
          this.auth = window.gapi.auth2.getAuthInstance();
          this.setState({ isSignedIn: this.auth.isSignedIn.get() });
        });		
		
	33. Edit `src/components/GoogleAuth.js`:
		## отображаем текст `Log In/ Log Out` в зависимости от `state.isSignedIn`
		## для этого вводим вспомогательную функцию:
		renderAuthButton() {
			if (this.state.isSignedIn === null) {
				return <div>I don&apos;t khow if you are signed in</div>;
			}
			if (this.state.isSignedIn) {
				return <div>You are signed</div>;
			}
			if (!this.state.isSignedIn) {
				return <div>You are not signed</div>;
			}
		}
		...
		  render() {
			return <div>{this.renderAuthButton()}</div>;
		}		
		
	34. Edit `src/components/GoogleAuth.js`:
		## Updating Auth State
		## функция `onAuthChange()` следит за состоянием переменной `isSignedIn`
		## отображаем `state.isSignedIn` на лету
        .then(() => {
          this.auth = window.gapi.auth2.getAuthInstance();
          this.setState({ isSignedIn: this.auth.isSignedIn.get() });
          this.auth.isSignedIn.listen(this.onAuthChange);
        });
		...
		onAuthChange = () => {
			this.setState({ isSignedIn: this.auth.isSignedIn.get() });
		};

		## для изменения состояния из консоли: 
		## gapi.auth2.getAuthInstance().signOut()
		## gapi.auth2.getAuthInstance().signIn()		
		
	35. Edit `src/components/GoogleAuth.js`:
		## Отображаем кнопку `Log In/ Log Out`
		if (this.state.isSignedIn) {
		return (
			<button className="ui red google button">
			<i className="google icon" />
			Sign Out
			</button>
		);
		}
		if (!this.state.isSignedIn) {
		return (
			<button className="ui green google button">
			<i className="google icon" />
			Sign In
			</button>
		);

	36. Edit `src/components/GoogleAuth.js`:
		## навешивание действий на кнопки:
		onSignInClick = () => {
			this.auth.signIn();
		};

		onSignOutClick = () => {
			this.auth.signOut();
		};
		...
		if (this.state.isSignedIn) {
			return (
				// eslint-disable-next-line react/button-has-type
				<button onClick={this.onSignOutClick} className="ui red google button">
				<i className="google icon" />
				Sign Out
				</button>
			);
		}
		if (!this.state.isSignedIn) {
			return (
				// eslint-disable-next-line react/button-has-type
				<button onClick={this.onSignInClick} className="ui green google button">
				<i className="google icon" />
				Sign In
				</button>
		);

	
	37. Handling Auth Status Through Redux (Обработка статуса аутентификации через Redux):
		## Edit `src/components/GoogleAuth.js`:
		## add `mapStateToProps()`
		const mapStateToProps = (state) => {
			return { isSignedIn : state.auth.isSignedIn };
		};
		
	38. ## Edit `src/components/GoogleAuth.js`:
		## delete
		//state = { isSignedIn: null };
		...
		## old code:
		    .then(() => {
				this.auth = window.gapi.auth2.getAuthInstance();
				this.setState({ isSignedIn: this.auth.isSignedIn.get() });
				this.auth.isSignedIn.listen(this.onAuthChange);
			});
		## new code:
		    .then(() => {
				this.auth = window.gapi.auth2.getAuthInstance();
				this.onAuthChange(this.auth.isSignedIn.get());
				this.auth.isSignedIn.listen(this.onAuthChange);
			});
		
	39. ## Edit `src/components/GoogleAuth.js`:
		## renderAuthButton()
			`this.state.isSignedIn`
		change on 
			`this.props.isSignedIn`
		...
		export default connect(mapStateToProps, { signIn, signOut })(GoogleAuth);
		
		
	## ----------------------------------------
	40. Fixed Action Types:
		## для того, чтобы не было случайных ошибок в написании, 
		## выносим значения TYPE в отдельный файл
		Create `src/actions/types.js`:
		## здесь будут храниться все константы, которые мы используем 
		## в наших `action creators` & `reducers`:
		export const SIGN_IN = "SIGN_IN";
		export const SIGN_OUT = "SIGN_OUT";
		
	41. Edit `src/actions/index.js`:
		## import
		import { SIGN_IN, SIGN_OUT } from "./types";
		...
		change `"SIGN_IN"` on `SIGN_IN`
		
	42.  Edit `src/actions/authReducer.js`:
		import { SIGN_IN, SIGN_OUT } from "../actions/types";
		...
		change `"SIGN_IN"` on `SIGN_IN`
		
	53. Recording the User's ID
		## Edit `src/components/GoogleAuth.js`:
		if (isSignedIn) {
			this.props.signIn(this.auth.currentUser.get().getId());
		}	