# REACT 시작하기

## 예전에 사용중이던 돔 활용 방식
```js
 const root = document.querySelector('#root');
    const btn_plue = document.querySelector('#btn_plus');

    let i = 0;

    root.innerHTML = '<p>init : 0</p>'

    btn_plue.addEventListener('click', () => {
      root.innerHTML = `<p>init : ${++i}</p>`;
    })
```

## component 의 데이터를 변경 시키는 방식
```js
const component = {
      message: 'init',
      count: 0,
      render() {
        return `<p>${this.message} : ${this.count}</p>`;
      }
    };

    function render(rootElement, component) {
      rootElement.innerHTML = component.render();
    }
    //초기화
    render(document.querySelector('#root'), component);

    document.querySelector('#btn_plus').addEventListener('click', () => {
      component.message = 'update';
      component.count = component.count +1;

      render(document.querySelector('#root'), component)
    })
```

## React의 가상의 돔을 사용한 방식
```js
const Component = props => {
      return React.createElement('p', null, `${props.message} : ${props.count}`)  //가상의 돔 생성
    }

    ReactDOM.render(
      React.createElement(Component, {message: 'init', count: 0}, null),
      document.querySelector('#root')
      //가상의 돔의 값과 id 입력
    );    

    document.querySelector('#btn_plus').addEventListener('click', () => {
      ReactDOM.render(
      React.createElement(Component, {message: 'update', count: 10}, null),
      document.querySelector('#root')
      //가상의 돔의 이벤트와 값과 id 입력
    );  
    })
```
