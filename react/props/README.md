# React

### Introdução aos Hooks - Parte 1

O objetivo é escrever uma variável sem precisar do processo de criação de uma classe. A primeira é o useState(), que serve para lembrar uma informação, então, por exemplo,  em um formulário é possível utilizar o useState() para armazenar um valor colocado pelo usuário. Também é possível utilizar em imagens, principalmente no seu carregamento.

```jsx
function ImageGallery() {
	const [index, setIndex] = useState(0);
}
```

Outro Hook que pode ser usado é o de contexto, mas é necessário entender Props. Props são fatores que são passados de um componente para outro, portanto, é uma forma de comunicação entre componentes. 

### Props

Como programação orientada a objetos, os atributos passados são realizados de uma camada acima da atual. Portanto, se houver a função:

```jsx
import React from 'react'

function Avatar(){
	return (
		<img className="" src="" width={} height={} />
	);
}

export default Avatar;
```

E:

```jsx
import React from 'react'

function Profile(){
	return(
		<Avatar />
	);
}

export default Profile;
```

A sua modularidade é ruim visto que é válido para um único tipo de Avatar. Para reverter essa situação, pode-se passar por parâmetro todas as informações que limitam a função Avatar, de modo que o novo código se torne:

```jsx
import { getImageUrl } from './utils.js';

function Avatar({ person, size }) {
  return (
    <img
      className="avatar"
      src={getImageUrl(person)}
      alt={person.name}
      width={size}
      height={size}
    />
  );
}

export default function Profile() {
  return (
    <div>
      <Avatar
        size={100}
        person={{ 
          name: 'Katsuko Saruhashi', 
          imageId: 'YfeOqp2'
        }}
      />
      <Avatar
        size={80}
        person={{
          name: 'Aklilu Lemma', 
          imageId: 'OKS67lh'
        }}
      />
      <Avatar
        size={50}
        person={{ 
          name: 'Lin Lanying',
          imageId: '1bX5QH6'
        }}
      />
    </div>
  );
}
```

Person e size são passados como parâmetros e tornou-se possível repetir a tag Avatar ao invés de criar outros 3 componentes.

A utilização de Props faz com que pensemos que pai e filho são independentes. Se fizermos:

```jsx
function Avatar(props){
	let person = props.person;
	let size = props.size;
}
```

Props conterá todos os parâmetros passados para a função.

Da mesma forma que os parâmetros em linguagens que utilizam funções, tal como python, os parâmetros podem ter valores previamente definidos para caso haja a falta de um, o valor definido seja utilizado. Para que não fique igual as outras linguagens, existe a sintaxe de spread. 

```jsx
function Profile({ person, size, isSepia, thickBorder }) {
  return (
    <div className="card">
      <Avatar
        person={person}
        size={size}
        isSepia={isSepia}
        thickBorder={thickBorder}
      />
    </div>
  );
}
```

Prefiro o que está acima 😊, mas para que não fique repetitivo é possível realizar:

```jsx
function Profile(props) {
  return (
    <div className="card">
      <Avatar {...props} />
    </div>
  );
}
```

Além de passar parâmetros, é possível passar objetos ou JSX como children. As vezes se faz necessário o seguinte processo.

```jsx
<Card>
  <Avatar />
</Card>
```

A função Card deverá receber como parâmetro um children já que este armazena a função Avatar.

```jsx
import Avatar from './Avatar.js';

function Card({ children }) {
  return (
    <div className="card">
      {children}
    </div>
  );
}

export default function Profile() {
  return (
    <Card>
      <Avatar
        size={100}
        person={{ 
          name: 'Katsuko Saruhashi',
          imageId: 'YfeOqp2'
        }}
      />
    </Card>
  );
}
```