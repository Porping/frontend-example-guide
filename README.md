# React for Frontend development CAPSTONE

Today we will learn how to create the frontend that connects to the backend. In this case, I will create the to-do for the demo.

## What is Frontend 🖥

Frontend refers to the part of a software application or website that users interact with directly. It is the user interface and user experience (UI/UX) layer of the application that is visible to the users.

## Outline

- [Prerequisite](#prerequisite)
- [Installation](#installation)
- [Let's start implementing the Todo website](#lets-start-implementing-todo-website)
  - [About frontend project](#about-frontend-project)
  - [Setup Todo website](#setup-todo-web-application)
  - [Create addTodo feature on the Todo website](#create-addtodo-feature-into-todo-web-application)
  - [Add more Todo features on the Todo website](#add-more-feature-into-todo-web-application)
  - [Add TailwindCss on Todo website](#add-tailwindcss-to-your-project)
  - [Connect frontend and backend](#connect-frontend-and-backend)
  
## Prerequisite

- [NodeJS](https://nodejs.org/)
- [Docker](https://www.docker.com/)
- Any HTTP client, ex: [Postman](https://www.postman.com/), [Insomnia](https://insomnia.rest/), some vs code extension. In this lab, I will use Postman for example.

## Installation

The easiest way to install Go, NodeJS, etc is by using the package manager

- for windows, you can use [scoop](https://scoop.sh/), [winget](https://github.com/microsoft/winget-cli), or [chocolatey](https://chocolatey.org/)
- for macOS, you can use [brew](https://brew.sh/)

### NodeJS

install via scoop

```sh
scoop install main/nodejs
```

install via winget

```sh
winget install -e --id OpenJS.NodeJS
```

install via brew

```sh
brew install node
```

Finally, you need to check if NodeJs is installed correctly you can copy this command and paste it into your terminal.

```sh
node -v
  ```

This command will check your NodeJS versions but we recommend you to use pnpm instead.

```sh
corepack enable pnpm
```

read more about [pnpm](https://pnpm.io/).

## Let's start implementing Todo website

In this project, I will separate it into 4 steps as follows.

1. About the frontend project.
2. Setup todo web application.
3. Create addTodo feature into the Todo web application.
4. Add more features to Todo web application.
5. Add tailwindCSS in the project.
6. Connect frontend and backend.

### About frontend project

In this project I will explain about frontend by using React and building the Todo website for the first section I will focus on only frontend and the final section will be connected to the backend and database.

#### What is React

React is an open-source JavaScript library for building user interfaces or Web applications. You can create your components and these components will work independently and can reused this component. [read more](https://react.dev/)

![image](./assets/react.png)

#### Why did we choose Vite

Vite is a build tool that is designed to enhance the development experience for modern web projects. It can be used with various front-end frameworks and libraries. The feature that is outstanding in Vite is HMR (Hot Module Replacement). HMR helps you to development without refreshing your bowser and Vite has a build tool bundle you can use to build your React application and deploy it to the server.
[read more](https://vitejs.dev/)

![image](./assets/vite.jpg)

#### What alternative way if we don't use Vite

The main point that we use Vite is to build the React application and [hot reload](https://www.linkedin.com/advice/0/how-do-you-use-hot-reload-restart-speed-up) the website so this is another way you want to use another library to build your React application:

1. [webpack](https://webpack.js.org/)
2. [esbuild](https://esbuild.github.io/)
3. [parcel](https://parceljs.org/)
4. [rollupjs](https://rollupjs.org/)

### Setup Todo web application.

in this step, I will explain and give you an example of implementing a todo app. What you need to know

1. Basic HTML, CSS, Typescript [read more](https://developer.mozilla.org/en-US/)
2. Basic React such as React hook [read more](https://legacy.reactjs.org/docs/hooks-intro.html)

Next, install React typescript by [Vite](https://vitejs.dev/guide/) and you can choose by the steps below

```sh
pnpm create vite
  ```

1. Your project name is up to you.
2. Choose React.
3. Choose Typescript + SWC.
4. After finish installing you can copy and paste the command below to check it install correctly.

```sh
  cd your_project_name
  pnpm install
  pnpm run dev
  ```

If you install it correctly your screen will look like me

![image](/assets/vite_dev.png)

#### Let's see the project structure

```text
/my-react-vite-ts-swc-app
  ├── /node_modules      # Dependencies installed by npm or yarn
  ├── /public            # Static assets and the root HTML file
  │   ├── vite.ico       # Favicon
  │   └── ...
  ├── /src               # Source code of the React application
  │   ├── /components    # Reusable React components
  │   │   └── ...
  │   │
  │   ├── App.tsx        # Main component or entry point
  │   ├── main.ts        # Entry point for ReactDOM
  │   ├── index.css      # CSS or SCSS files
  │   └── ...
  ├── /tests             # Test files
  ├── .gitignore         # Git ignore file
  ├── package.json       # Project dependencies and scripts
  ├── vite.config.ts     # Vite configuration file
  ├── tsconfig.json      # TypeScript configuration file
  ├── swcrc.js           # SWC configuration file
  ├── README.md          # Project documentation
  ├── .eslintrc.js       # ESLint configuration
  ├── .prettierrc        # Prettier configuration
  └── ...

```

You will use the components folder to implement the todo component and display it on your website.

First, you need to create a file named Todo.tsx in your component folder

```text
/my-react-vite-ts-swc-app
  ├── /node_modules    
  ├── /public            
  │   ├── vite.ico       
  │   └── ...
  ├── /src              
  │   ├── /components   
  │       ├── Todo.tsx       
  │       
  └── ...
```

In Todo.tsx you can copy the code below and paste it into your file.
I will explain it below the code.

<h5 a><strong><code>Todo.tsx</code></strong></h5>

```tsx
import { useState } from "react";

const mockTodoData: TodoType[] = [
  {
    id: 1,
    title: "Learn React",
    completed: false,
  },
  {
    id: 2,
    title: "Learn React 2",
    completed: false,
  },
];

export type TodoType = {
  id: number;
  title: string;
  completed: boolean;
};

export const Todo = () => {
  const [todoData, setTodoData] = useState<TodoType[]>(mockTodos);

  return (
    <>
      {todoData.map((todo) => (
        <div key={todo.id}>{todo.title}</div>
      ))}
    </>
  );
};
```

#### Explanation step 2

First, in the section, I declared the Todo type for use in useState to identify the type I want to store in the todoData variable.

```tsx
export type TodoType = {
  id: number;
  title: string;
  completed: boolean;
};
```

Next, I create mockTodoData which is the Array type of TodoType for setting the default value in useState.

```tsx
const mockTodoData: TodoType[] = [
  {
    id: 1,
    title: "Learn React",
    completed: false,
  },
  {
    id: 2,
    title: "Learn React 2",
    completed: false,
  },
];
```

Next, I built the render section of this component I named it TodoList and I made useState that name todoData and set default value to mockTodoData that I created. In the return section, I display the data in the array of todoList.

```tsx
export const Todo= () => {
  const [todoData, setTodoData] = useState<TodoType[]>(mockTodoData);

  return (
    <>
      {todoData.map((todo) => (
        <div key={todo.id}>{todo.title}</div>
      ))}
    </>
  );
};
```

Your website will not show anything related to Todo yet because You haven't imported this TodoList into App.tsx

let's import it into App.tsx

<h5 a><strong><code>App.tsx</code></strong></h5>

```tsx
import { Todo } from "./components/Todo";

const App = () => {
  return <>{Todo}</>;
};

export default App;
```

After import into App.tsx your website will look like this.

![image](/assets/ex_1.png)

Nice 😁 now you can show your mockData Todo on your website.

#### The concept of step 2

1. **Type declaration**
    - **Basic Types**
      - number: Represents numeric values.
      - string: Represents textual data.
      - boolean: Represents true or false values.
      - any: Represents a dynamic or unknown type.
      - void: Represents the absence of a value.
      - null and undefined: Represent null and undefined values, respectively.
      - object: Represents any non-primitive type.
    - **Arrays and Tuples**
      - Array\<T>: Represents an array of elements of type T.
      - T[]: An alternative syntax for representing arrays.
    - **Functions**
      - (parameter: Type) => ReturnType: Represents a function type.
    - **Objects**
      - { key: Type }: Represents an object with a specific key and value type.
    - [read more an example](https://www.typescriptlang.org/docs/handbook/basic-types.html)

2. **The useState hook** is part of the React Hooks API. It provides a way to declare state variables in functional components. Here's a basic example of counting a number:

if you declare the count variable as var or let that set default value is 0 and create a button and if you click it will plus count variable by one like this

```tsx
import React, { useState } from 'react';

function ExampleComponent() {
  let count = 0;

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => {
        count = count + 1;
        console.log(count);
      }}>
        Click me
      </button>
    </div>
  );
}

```

On the website you won't see count number change but if you open the console log in to your browser count number will be changed normally if you click a button. So let's change it by useState.

```tsx
import React, { useState } from 'react';

function ExampleComponent() {
  // Declare a state variable named "count" with an initial value of 0
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}

```

In this example
**count** is a state variable
**setCount** is a function provided by the useState hook to update the value of count.

When the button is clicked, the setCount function is called to increment the value of count, triggering a re-render of the component with the updated state.

If you still don't understand, you can watch this [video clip](https://www.youtube.com/watch?v=O6P86uwfdR0&t=635s&ab_channel=WebDevSimplified) from when I started learning React. This clip helped me a lot 😁.

### Create addTodo feature into Todo web application.

In the first step, we only display the data in our mocked todoData. In this step, we will add more features such as addTodo editTodo deleteTodo and toggleTodo. Let's do an easy one addTodo.

<h5 a><strong><code>Todo.tsx</code></strong></h5>

```tsx
import { useState } from "react";

export type TodoType = {
  id: number;
  title: string;
  completed: boolean;
};

export const Todo = () => {
  const [todoData, setTodoData] = useState<TodoType[]>([]);
  const [text, setText] = useState<string>("");

  const addTodo = (title: string) => {
    setTodoData((prevTodos) => [
      ...prevTodos,
      { id: prevTodos.length + 1, title, completed: false },
    ]);
  };

  return (
    <>
      <input
        type="text"
        value={text}
        onChange={(e) => setText(e.target.value)}
      />
      <button onClick={() => addTodo(text)}>Add</button>

      {todoData.map((todo) => (
        <div key={todo.id}>{todo.title}</div>
      ))}
    </>
  );
};
```

#### Explanation step 2

First I add more useState variable name text to receive the text that the user type in the input box.

```tsx
const [text, setText] = useState<string>("");
```

Next, I create addTodo function that has one string parameter as the title for todo. This function will set a new value by using setTodoData without affecting any value in todoData. You can learn more about spreading operators in this [link](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)

```tsx
const addTodo = (title: string) => {
    setTodoData((prevTodos) => [
      ...prevTodos,
      { id: prevTodos.length + 1, title, completed: false },
    ]);
  };
```

Finally, I created an input box that has an onChange function which receives a value of that input when you type in the input box and store it in text value by using the setText function and create a button that when I click it will trigged addTodo function that passes text parameter into the function.

```tsx
      <input
        type="text"
        value={text}
        onChange={(e) => setText(e.target.value)}
      />
      <button onClick={() => addTodo(text)}>Add</button>
```

Now in your website you can add a new Todo 😁.

![image](/assets/ex_2.png)

### Add more feature into Todo web application.

In this step, I will create the remaining functions in the Todo website including edit Todo delete Todo, and toggle Todo in order. First, let's add the editTodo function.

<h5 a><strong><code>Todo.tsx</code></strong></h5>

```tsx
import { useState } from "react";

export type TodoType = {
  id: number;
  title: string;
  completed: boolean;
};

export const Todo = () => {
  const [todoData, setTodoData] = useState<TodoType[]>([]);
  const [text, setText] = useState<string>("");

  const addTodo = (title: string) => {
    setTodoData((prevTodos) => [
      ...prevTodos,
      { id: prevTodos.length + 1, title, completed: false },
    ]);
  };

  const editTodo = (id: number, newText: string) => {
    setTodoData((prevTodos) =>
      prevTodos.map((todo) =>
        todo.id === id ? { ...todo, title: newText } : todo
      )
    );
  };

  return (
    <>
      <input
        type="text"
        value={text}
        onChange={(e) => setText(e.target.value)}
      />
      <button onClick={() => addTodo(text)}>Add</button>

       <>
      <input
        type="text"
        value={text}
        onChange={(e) => setText(e.target.value)}
      />
      <button onClick={() => addTodo(text)}>Add</button>
      {todoData.map((todo) => (
        <div key={todo.id}>{todo.title}</div>
      ))}
    </>
    </>
  );
};
```

As you see we want to change the title of Todo. We need to send the id and new title into the editTodo function. So we will create components that receive todoData and editTodo function.

#### Explanation step 4

At the end of the code let's create a new component named TodoList for display title, edit button, and delete button.

```tsx
export const TodoList= () => {
  return (
    <div></div>
  );
};
```

Next, we need to create TodoList type to identify what we need to send into these components.

```tsx
type TodoListType = {
  todo: TodoType;
  onEdit: (id: number, title: string, completed: boolean) => void;
};
export const TodoList= ({
  todo,
  onEdit,
}) => {
  return (
    <div></div>
  );
};
```

Next, we will add an edit button and title todo in the return section in this case you can decorate with CSS if you want.

```tsx
type TodoListType = {
  todo: TodoType;
  onEdit: (id: number, title: string, completed: boolean) => void;
};
export const TodoList:React.FC<TodoListType> = ({
  todo,
  onEdit,
}) => {
  const [isEditing, setEditing] = useState(false);
  const [newTitle, setNewTitle] = useState(todo.title);

  const handleEdit = () => {
    setEditing(true);
  };

  const handleSave = () => {
    onEdit(todo.id, newTitle, todo.completed);
    setEditing(false);
  };

  return (
      <div >
      {isEditing ? (
        <div >
          <input
            type="text"
            value={newTitle}
            onChange={(e) => setNewText(e.target.value)}
          />
          <button onClick={handleSave}>
            Save
          </button>
        </div>
      ) : (
        <div >
            {todo.title}
          <button onClick={handleEdit} >
            Edit
          </button>
        </div>
      )}
    </div>
  );
};
```

Let me explain the logic of this component as simple. this component will show the title and edit button. When you click the edit button the title text will change to an input box that allows you change the title Todo what ever you want and when you finish changing you can click the save button to save the new title.

Let's see, in detail first I create new two useState variables named Editing and new Title:
**isEditing** is a boolean type that will check whether it now editing or not if isEditiing is true it will show an input box instead Todo title.
**newTitle** is a string type that will receive the string value that the user types in the input box by using the setNewTitle function. it sets the default value to the title of Todo value which makes the user easier to use.

```tsx
const [isEditing, setEditing] = useState(false);
const [newTitle, setNewTitle] = useState(todo.title);
```

Next, create new function named handleEdit and handleSave:
**handleEdit**: this function is triggered when the user click on the edit button. It will change the isEditing value from false to true.

```tsx
const handleEdit = () => {
    setEditing(true);
  };
```

**handleSave**: this function is triggered when the user clicks on the save button. It will use the onEdit function that I passed into this component to change the title of Todo after that I set the isEditing value to false.

In the return section I make a condition is if isEditing is true it will return the text box and save button and if isEditing is false then show the title of Todo instead.

```tsx
return (
      <div >
      {isEditing ? (
        <div >
          <input
            type="text"
            value={newTitle}
            onChange={(e) => setNewText(e.target.value)}
          />
          <button onClick={handleSave}>
            Save
          </button>
        </div>
      ) : (
        <div >
            {todo.title}
          <button onClick={handleEdit} >
            Edit
          </button>
        </div>
      )}
    </div>
  );
  ```

Now you need to replace the return of todoData.map to the TodoList component your final code will look like this.

<h5 a><strong><code>Todo.tsx</code></strong></h5>

```tsx
import { useState } from "react";

export type TodoType = {
  id: number;
  title: string;
  completed: boolean;
};

export const Todo = () => {
  const [todoData, setTodoData] = useState<TodoType[]>([]);
  const [text, setText] = useState<string>("");

  const addTodo = (title: string) => {
    setTodoData((prevTodos) => [
      ...prevTodos,
      { id: prevTodos.length + 1, title, completed: false },
    ]);
  };

  const editTodo = (id: number, newText: string) => {
    setTodoData((prevTodos) =>
      prevTodos.map((todo) =>
        todo.id === id ? { ...todo, title: newText } : todo
      )
    );
  };

  return (
    <>
      <input
        type="text"
        value={text}
        onChange={(e) => setText(e.target.value)}
      />
      <button onClick={() => addTodo(text)}>Add</button>
      {todoData.map((todo) => (
        <TodoList
            key={todo.id}
            todo={todo}
            onEdit={editTodo}
          />
      ))}
    </>
  );
};

type TodoListType = {
  todo: TodoType;
  onEdit: (id: number, title: string, completed: boolean) => void;
};
export const TodoList:React.FC<TodoListType> = ({
  todo,
  onEdit,
}) => {
  const [isEditing, setEditing] = useState(false);
  const [newTitle, setNewTitle] = useState(todo.title);

  const handleEdit = () => {
    setEditing(true);
  };

  const handleSave = () => {
    onEdit(todo.id, newTitle, todo.completed);
    setEditing(false);
  };

  return (
      <div >
      {isEditing ? (
        <div >
          <input
            type="text"
            value={newTitle}
            onChange={(e) => setNewTitle(e.target.value)}
          />
          <button onClick={handleSave}>
            Save
          </button>
        </div>
      ) : (
        <div >
            {todo.title}
          <button onClick={handleEdit} >
            Edit
          </button>
        </div>
      )}
    </div>
  );
};
```

Your website will look like this:

![image](/assets/ex_3.png)

Next, I will add remain functions of Todo including deleteTodo and toggleTodo but I am not going to explain the code because I have explained the concept already.

<h5 a><strong><code>Todo.tsx</code></strong></h5>

```tsx
import { useState } from "react";

export type TodoType = {
  id: number;
  title: string;
  completed: boolean;
};

export const Todo = () => {
  const [todoData, setTodoData] = useState<TodoType[]>([]);
  const [text, setText] = useState<string>("");

  const addTodo = (title: string) => {
    setTodoData((prevTodos) => [
      ...prevTodos,
      { id: prevTodos.length + 1, title, completed: false },
    ]);
  };

  const editTodo = (id: number, newText: string) => {
    setTodoData((prevTodos) =>
      prevTodos.map((todo) =>
        todo.id === id ? { ...todo, title: newText } : todo
      )
    );
  };

  const deleteTodo = (id: number) => {
    setTodoData((prevTodos) => prevTodos.filter((todo) => todo.id !== id));
  };

  const toggleTodo = (id: number) => {
    setTodoData((prevTodos) =>
      prevTodos.map((todo) =>
        todo.id === id ? { ...todo, completed: !todo.completed } : todo
      )
    );
  };

  return (
    <>
      <input
        type="text"
        value={text}
        onChange={(e) => setText(e.target.value)}
      />
      <button onClick={() => addTodo(text)}>Add</button>

      <div>
        {todoData.map((todo) => (
          <TodoList
            key={todo.id}
            todo={todo}
            onToggle={toggleTodo}
            onEdit={editTodo}
            onDelete={deleteTodo}
          />
        ))}
      </div>
    </>
  );
};

export type TodoListType= {
  todo: TodoType;
  onToggle: (id: number, title: string, completed: boolean) => void;
  onEdit: (id: number, title: string, completed: boolean) => void;
  onDelete: (id: number) => void;
};

export const TodoList: React.FC<TodoListType> = ({
  todo,
  onToggle,
  onEdit,
  onDelete,
}) => {
  const [isEditing, setEditing] = useState(false);
  const [newText, setNewText] = useState(todo.title);

  const handleEdit = () => {
    setEditing(true);
  };

  const handleSave = () => {
    onEdit(todo.id, newText, todo.completed);
    setEditing(false);
  };

  return (
    <>
      {isEditing ? (
        <div >
          <input
            type="text"
            value={newText}
            onChange={(e) => setNewText(e.target.value)}
          />
          <button onClick={handleSave}>Save</button>
        </div>
      ) : (
        <div >
          <div
            onClick={() => onToggle(todo.id, todo.title, todo.completed)}
          >
            {todo.title}
          </div>
          <button onClick={handleEdit}>Edit</button>
          <button onClick={() => onDelete(todo.id)}>Delete</button>
        </div>
      )}
    </>
  );
};
```

Now your website will look like this:
![image](/assets/ex_4.png)

😣 Does it look not friendly to use right? In the next step, I will show you how to install Tailwind CSS and decorate the website with it.

### Add TailwindCSS to your project

#### What is CSS

CSS (Cascading Style Sheets) It is the language used to describe the shape and characteristics of. HTML file. Simply put, it is a file used to decorate your website pages to look beautiful.

In the past, we had to create a .css file and reference it to our HTML file, whether using a class or an id, as in the example below.

```css
/* refer by class */
.box{
  background-color: black;
}

/* refer by id */
#container{
  width: 100%;
}
```

But in React we highly recommend using [tailwindCSS](https://tailwindcss.com/) or [styled component](https://styled-components.com/) for development because it easy to understand and comprehend.

this is an example of using styled component

```tsx
import styled from 'styled-components';

const Button = styled.button`
  background-color: white;
  color: blue;
  border: 2px solid blue;
`;

render() {
  return <Button>Normal Button</Button>;
}
```

this is an example of using tailwind CSS

```tsx


render() {
  return <button className="p-2 bg-red-500 w-10 h-auto">
          Normal Button
         </button>;
}
```

#### Why we use tailwindCss

According to the example above. TailwindCSS can create CSS in HTML elements without importing any file. it's easy to use and easy to understand. In the next step, I will install tailwindCSS and integrate it with the Todo website.

#### Install TailwindCSS

In this installation I following by Tailwind document you can go to this [link](https://tailwindcss.com/docs/guides/create-react-app) and look around by yourself or follow me step-by step

First please make sure now you are in the project directory copy this command and run it in your terminal.

```sh
pnpm install -D tailwindcss
npx tailwindcss init
```

You will have the tailwind.config.js file in your project directory. Click that file copy the code below and paste it into your tailwind.config.js file.

<h5 a><strong><code>tailwind.config.js</code></strong></h5>

```ts
/** @type {import('tailwindcss').Config} */
export default {
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

Next, add the Tailwind directives to your CSS
in your index.css which path [[./src/index.css]]

<h5 a><strong><code>index.css</code></strong></h5>

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

Finally, You can play around for yourself. Change the style of a button or input box you can read it in this [link](https://tailwindcss.com/docs/installation) or you can copy my code and look around it by yourself.

<h5 a><strong><code>Todo.tsx</code></strong></h5>

```tsx
import React, { useState } from "react";
export type TodoType = {
  id: number;
  title: string;
  completed: boolean;
};

export const Todo = () => {
  const [todoData, setTodoData] = useState<TodoType[]>([]);
  const [text, setText] = useState<string>("");

  const addTodo = (title: string) => {
    setTodoData((prevTodos) => [
      ...prevTodos,
      { id: prevTodos.length + 1, title, completed: false },
    ]);
  };

  const editTodo = (id: number, newText: string) => {
    setTodoData((prevTodos) =>
      prevTodos.map((todo) =>
        todo.id === id ? { ...todo, title: newText } : todo
      )
    );
  };

  const deleteTodo = (id: number) => {
    setTodoData((prevTodos) => prevTodos.filter((todo) => todo.id !== id));
  };

  const toggleTodo = (id: number) => {
    setTodoData((prevTodos) =>
      prevTodos.map((todo) =>
        todo.id === id ? { ...todo, completed: !todo.completed } : todo
      )
    );
  };

  return (
    <div className="max-w-md mx-auto mt-8 p-4 shadow-lg shadow-[#E8D8C4] bg-[#E8D8C4] ">
      <h1 className="text-2xl font-bold mb-4 text-[#6D2932]">Todo App</h1>
      <div className="mb-4 flex space-x-3">
        <input
          type="text"
          value={text}
          placeholder="Add new todo"
          className="border border-[#6D2932] bg-[#C7B7A3] text-[#6D2932] placeholder:text-[#6D2932] p-2 w-full"
          onChange={(e) => setText(e.target.value)}
        />
        <button className="p-2 bg-[#C7B7A3]" onClick={() => addTodo(text)}>
          Add
        </button>
      </div>
      {todoData == null ? (
        <p className=" text-center text-lg font-semibold animate-pulse">
          No todo{" "}
        </p>
      ) : (
        <>
          {todoData.map((todo) => (
            <TodoList
              key={todo.id}
              todo={todo}
              onToggle={toggleTodo}
              onEdit={editTodo}
              onDelete={deleteTodo}
            />
          ))}
        </>
      )}
    </div>
  );
};

type TodoListType = {
  todo: TodoType;
  onToggle: (id: number, title: string, completed: boolean) => void;
  onEdit: (id: number, title: string, completed: boolean) => void;
  onDelete: (id: number) => void;
};

export const TodoList: React.FC<TodoListType> = ({
  todo,
  onToggle,
  onEdit,
  onDelete,
}) => {
  const [isEditing, setEditing] = useState(false);
  const [newTitle, setNewTitle] = useState(todo.title);

  const handleEdit = () => {
    setEditing(true);
  };

  const handleSave = () => {
    onEdit(todo.id, newTitle, todo.completed);
    setEditing(false);
  };

  return (
    <div className="flex items-center justify-between p-2 border-b border-[#6D2932]">
      {isEditing ? (
        <div className="flex items-center">
          <input
            type="text"
            value={newTitle}
            onChange={(e) => setNewTitle(e.target.value)}
            className="border-b border-[#6D2932] bg-[#C7B7A3] text-[#6D2932] placeholder:text-[#6D2932] focus:outline-none  px-2 py-1 mr-2"
          />
          <button onClick={handleSave} className="text-blue-500">
            Save
          </button>
        </div>
      ) : (
        <div className="flex items-center">
          <span
            className={`cursor-pointer ${
              todo.completed ? "line-through text-gray-400" : "text-black"
            }`}
            onClick={() => onToggle(todo.id, todo.title, todo.completed)}
          >
            {todo.title}
          </span>
          <button onClick={handleEdit} className="ml-2 text-blue-500">
            Edit
          </button>
          <button
            onClick={() => onDelete(todo.id)}
            className="ml-2 text-red-500"
          >
            Delete
          </button>
        </div>
      )}
    </div>
  );
};
```

Now your website looks better.
![image](/assets/ex_5.png)

### Connect frontend and backend

This is the final step you build the Todo website. In this step you will learn about fetch API and new React hooks called useEffect.

#### You need to creat backend before following this step

Before you continue this step please create your backend and database first. So you can read it by this [link](https://github.com/XiaoXuxxxx/backend-example-guide?tab=readme-ov-file#what-is-backend).

#### What is API

You can read about API at this [link](https://github.com/XiaoXuxxxx/backend-example-guide?tab=readme-ov-file#what-is-api) in the backend In this project I will use Axois for fetch or send API from the backend or you can use normal fetch instead. This is an example of using fetch in react.

```tsx
 const fetchTodos = async () => {
    const res = fetch("http://localhost:3000/todo", {
      method: "GET",
    });
    if (res.data.isSuccess) {
      setTodoData(res.data.data);
    }
  };

```

You can read more about fetch at this [link](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch).

#### What is Axios

Axios is a JavaScript library that is used to make HTTP requests from web browsers or Node.js environments. Let's install Axios in the project.

```sh
pnpm i axios
```

#### Used Axios with fetchTodo function

In the Todo component, I will make a fetchTodo to get Todo data from the database.

<h5 a><strong><code>Todo.tsx</code></strong></h5>

```tsx
useEffect(() => {
    fetchTodos();
  }, []);

const fetchTodos = async () => {
    const res = await axios.get("http://localhost:3000/todo");
    if (res.data.isSuccess) {
      setTodoData(res.data.data);
    }
  };
```

As you see in the fetchTodos function has Axios that receive data by get method with "http://localhost:3000/todo" and store it in res variable and I make a condition if the value of res.data.isSucccess that response by backend is true it will store value in the todoData by setTodoData function.

NOTE: In default javascript behavior is asynchronous so we need to fetch data before rendering the website. So we need to add await before the function that we need to finish first. read more about async await at this [link](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function).

#### The concept of step 6

 **useEffect** is a React hook that manages side effects in the life cycle component. It is normally used to fetch data or change something in the component that has a state. You can manage when you want to trigger useEffect by adding some parameter in an array if you use an empty array it will trigger once the website finishes load. read more about useEffect in this [link](https://legacy.reactjs.org/docs/hooks-effect.html).

After you run the website press F12 to see in the network tab if you don't see anything please reload the web browser. You will see this data the same as in picture below.

(add image)

##### Integrate Axios with addTodo

It is the same as fetchTodos but changes the method to post and send the title to the backend. You can see behavior in the network tab in your browser.

```tsx
const addTodo = async (text: string) => {
    const res = await axios.post("http://localhost:3000/todo", {
      title: text,
    });

    if (res.data.isSuccess) {
      fetchTodos();
    }
  };
```

After sending data successfully to the backend I will fetch data again to render new data that we add.

##### Let's integrate Axios with remain feature

In this section I won't explain the code because it is the same concept please look around and play it with yourself good luck 😀

```tsx
import React, { useEffect, useState } from "react";
import axios from "axios";

export type TodoType = {
  id: number;
  title: string;
  completed: boolean;
};

export const Todo = () => {
  const [todoData, setTodoData] = useState<TodoType[]>([]);

  useEffect(() => {
    fetchTodos();
  }, []);

  const addTodo = async (text: string) => {
    const res = await axios.post("http://localhost:3000/todo", {
      title: text,
    });

    if (res.data.isSuccess) {
      fetchTodos();
    }
  };

  const toggleTodo = async (id: number, title: string, completed: boolean) => {
    const res = await axios.patch(`http://localhost:3000/todo/${id}`, {
      title: title,
      completed: !completed,
    });

    if (res.data.isSuccess) {
      fetchTodos();
    }
  };

  const editTodo = async (id: number, title: string, completed: boolean) => {
    const res = await axios.patch(`http://localhost:3000/todo/${id}`, {
      title: title,
      completed: completed,
    });

    if (res.data.isSuccess) {
      fetchTodos();
    }
  };

  const deleteTodo = async (id: number) => {
    const res = await axios.delete(`http://localhost:3000/todo/${id}`);

    if (res.data.isSuccess) {
      fetchTodos();
    }
  };

  const fetchTodos = async () => {
    const res = await axios.get("http://localhost:3000/todo");
    if (res.data.isSuccess) {
      setTodoData(res.data.data);
    }
  };

  return (
    <div className="max-w-md mx-auto mt-8 p-4 shadow-lg shadow-[#E8D8C4] bg-[#E8D8C4] ">
      <h1 className="text-2xl font-bold mb-4 text-[#6D2932]">Todo App</h1>
       <div className="mb-4 flex space-x-3">
        <input
          type="text"
          value={text}
          placeholder="Add new todo"
          className="border border-[#6D2932] bg-[#C7B7A3] text-[#6D2932] placeholder:text-[#6D2932] p-2 w-full"
          onChange={(e) => setText(e.target.value)}
        />
        <button className="p-2 bg-[#C7B7A3]" onClick={() => addTodo(text)}>
          Add
        </button>
      </div>
      {todoData == null ? (
        <p className=" text-center text-lg font-semibold animate-pulse">
          No todo{" "}
        </p>
      ) : (
        <>
          {todoData.map((todo) => (
            <TodoList
              key={todo.id}
              todo={todo}
              onToggle={toggleTodo}
              onEdit={editTodo}
              onDelete={deleteTodo}
            />
          ))}
        </>
      )}
    </div>
  );
};

type TodoListType = {
  todo: TodoType;
  onToggle: (id: number, title: string, completed: boolean) => void;
  onEdit: (id: number, title: string, completed: boolean) => void;
  onDelete: (id: number) => void;
};

export const TodoList: React.FC<TodoListType> = ({
  todo,
  onToggle,
  onEdit,
  onDelete,
}) => {
  const [isEditing, setEditing] = useState(false);
  const [newTitle, setNewTitle] = useState(todo.title);

  const handleEdit = () => {
    setEditing(true);
  };

  const handleSave = () => {
    onEdit(todo.id, newTitle, todo.completed);
    setEditing(false);
  };

  return (
    <div className="flex items-center justify-between p-2 border-b border-[#6D2932]">
      {isEditing ? (
        <div className="flex items-center">
          <input
            type="text"
            value={newTitle}
            onChange={(e) => setNewTitle(e.target.value)}
            className="border-b border-[#6D2932] bg-[#C7B7A3] text-[#6D2932] placeholder:text-[#6D2932] focus:outline-none  px-2 py-1 mr-2"
          />
          <button onClick={handleSave} className="text-blue-500">
            Save
          </button>
        </div>
      ) : (
        <div className="flex items-center">
          <span
            className={`cursor-pointer ${
              todo.completed ? "line-through text-gray-400" : "text-black"
            }`}
            onClick={() => onToggle(todo.id, todo.title, todo.completed)}
          >
            {todo.title}
          </span>
          <button onClick={handleEdit} className="ml-2 text-blue-500">
            Edit
          </button>
          <button
            onClick={() => onDelete(todo.id)}
            className="ml-2 text-red-500"
          >
            Delete
          </button>
        </div>
      )}
    </div>
  );
};
```

Thank you for reading this blog. I hope it helps you in some way to understand React. If there are any mistakes, sorry and good luck with your project😄.
