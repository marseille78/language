# (REACT) 1. Модуль 1 Компоненти та колекції. Стилізація

## Links

- [Умовний рендеринг](https://react.dev/learn/conditional-rendering)
- [All the Conditional Renderings in React](https://www.robinwieruch.de/conditional-rendering-react/)
- [Списки і ключі](https://react.dev/learn/rendering-lists)

### Додані користувачами

- [По лекции react_40 Норец Максим](https://github.com/Karlsoninit/online_react_40)
- [Настройка pre-commit хуков](https://github.com/goitacademy/react-lint-staged-workshop)
- [Репозиторій з кодом заняття 01.08.2022](https://github.com/luxplanjay/react-48/tree/01-components/src)
- [Theme Specification](https://theme-ui.com/theme-spec)
- [Знакомство с MPA/SPA, SSR/CSR - отличия, недостатки](https://www.youtube.com/watch?v=0zQPQztuWto)

### Платформи

- [Next.js](https://nextjs.org/)
- [React Native](https://reactnative.dev/)
- [Electron](https://www.electronjs.org/)

### React DevTools

- [Devtools в Chrome Web Store](https://chromewebstore.google.com/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en)
- [Introducing the New React DevTools](https://legacy.reactjs.org/blog/2019/08/15/new-react-devtools.html)

### Пакети

- [prop-types](https://www.npmjs.com/package/prop-types)
- [PostCSS Normalize](https://github.com/csstools/postcss-normalize)
- [clsx](https://www.npmjs.com/package/clsx)

## JSX

- [Знайомство з JSX](https://react.dev/learn/writing-markup-with-jsx)

```jsx
import ReactDOM from "react-dom/client";


const imageUrl =
  "https://images.pexels.com/photos/461198/pexels-photo-461198.jpeg?dpr=2&h=480&w=640";
const productPrice = 10.99;


const product = (
  <div>
    <img src={imageUrl} alt="Tacos With Lime" width="640" />
    <h2>Tacos With Lime</h2>
    <p>Price: {productPrice}$</p>
    <button type="button">Add to cart</button>
  </div>
);


ReactDOM.createRoot(document.getElementById("root")).render(product);
```
```jsx
/* Рендер за умовою. if за допомогою логічного оператора && */

const Mailbox = ({ unreadMessages }) => {
  return (
    <div>
      <h1>Hello!</h1>
      {unreadMessages.length > 0 && (
        <p>You have {unreadMessages.length} unread messages.</p>
      )}
    </div>
  );
};
```
```jsx
/* Рендер за умовою. if...else за допомогою тернарного оператора */

const Mailbox = ({ username, unreadMessages }) => {
  return (
    <div>
      <h1>Hello {username}</h1>
      {unreadMessages.length > 0 ? (
        <p>You have {unreadMessages.length} unread messages.</p>
      ) : (
        <p>No unread messages.</p>
      )}
    </div>
  );
};
```
```jsx
/* Ключ (key) — це спеціальний рядковий проп, який потрібно задати під час створення елементів колекції. */

const favouriteBooks = [
  { id: "id-1", name: "JS for beginners" },
  { id: "id-2", name: "React basics" },
  { id: "id-3", name: "React Router overview" },
  { id: "id-4", name: "Redux in depth" },
];

const BookList = ({ books }) => (
  <ul>
    {books.map(book => (
      <li key={book.id}>{book.name}</li>
    ))}
  </ul>
);
```
```jsx
/* Вбудовані стилі */

const App = () => {
  return (
    <p
      style={{
        margin: 8,
        padding: "12px 16px",
        borderRadius: 4,
        backgroundColor: "gray",
        color: "white",
      }}
    >
      Please update your email!
    </p>
  );
};

/* ==================================== */

const alertStyles = {
  margin: 8,
  padding: "12px 16px",
  borderRadius: 4,
  backgroundColor: "gray",
  color: "white",
};


export const Alert = ({ children }) => {
  return <p style={alertStyles}>{children}</p>;
};
```

### Бібліотека `clsx`

```jsx
import clsx from "clsx";


const className = clsx(
  "first",
  10,
  undefined && "second",
  true && "third",
  false ? "fourth" : "fifth"
);
console.log(className); // "first 10 third fifth"
```
```jsx
import clsx from "clsx";
import css from "./Alert.module.css";


const Alert = ({ variant, outlined, elevated, children }) => {
  return (
    <p
      className={clsx(css[variant], {
        [css.isOutlined]: outlined,
        [css.isElevated]: elevated,
      })}
    >
      {children}
    </p>
  );
};
```

## CSS-модулі

```css
/* Властивість composes - Композиція селекторів це одна з ключових можливостей CSS-модулів, яка дозволяє створювати клас, наслідуючи стилі іншого класу, але не дублюючи їх. */

.alert {
  margin: 8px;
  padding: 12px 16px;
  border-radius: 4px;
  background-color: gray;
  color: white;
}


.info {
  composes: alert;
  background-color: blue;
}


.success {
  composes: alert;
  background-color: green;
}


.error {
  composes: alert;
  background-color: red;
}


.warning {
  composes: alert;
  background-color: orange;
}
```

## Нормалізація стилів

```jsx
@import-normalize;


/* Решта стилів файлів */
```

## PropTypes

```bash
npm install --save-dev prop-types
```
```jsx
import PropTypes from "prop-types";

const Product = ({
  imgUrl = "<https://dummyimage.com/640x480/2a2a2a/ffffff&text=Product+image+placeholder>",
  name,
  price,
}) => (
  <div>
    <img src={imgUrl} alt={name} width="640" />
    <h2>{name}</h2>
    <p>Price: {price}$</p>
    <button type="button">Add to cart</button>
  </div>
);

Product.propTypes = {
  imgUrl: PropTypes.string,
  name: PropTypes.string.isRequired,
  price: PropTypes.number.isRequired,
};
```