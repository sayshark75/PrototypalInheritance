Cart Item Hierarchy

![image](https://user-images.githubusercontent.com/112304655/203323896-44ee4a13-5c99-40d2-8f6f-5b206eb0062f.png)

Cart items Chart

![image](https://user-images.githubusercontent.com/112304655/203326765-08197b63-5eba-4395-bd8e-8e125cee5a47.png)


App Component
```
import "./styles.css";
import React from "react";
import CartItem from "./Components/CartItem.jsx";
import Total from "./Components/Total";
const myData = [
  { id: 1, title: "chicken tikka", amount: 200, price: 200, quantity: 1 },
  { id: 2, title: "Biryani", amount: 190, price: 190, quantity: 1 },
  { id: 3, title: "Chai Chapati", amount: 40, price: 40, quantity: 1 },
  { id: 4, title: "Dal Chawal", amount: 80, price: 80, quantity: 1 }
];
export default function App() {
  const [data, setData] = React.useState(myData);
  const changePrice = (id, q, p) => {
    setData(
      data.map((elem) =>
        elem.id === id
          ? { ...elem, quantity: elem.quantity + q, price: elem.price + p }
          : elem
      )
    );
  };
  return (
    <div className="App">
      <h1>Cart Items</h1>
      <div>
        {data.map((elem) => (
          <CartItem key={elem.id} {...elem} changePrice={changePrice} />
        ))}
      </div>
      <Total price={data.reduce((acc, elem) => acc + elem.price, 0)} />
    </div>
  );
}
```
CartItem Component
```
import Button from "./Button";

const CartItem = ({ id, title, amount, price, quantity, changePrice }) => {
  return (
    <div
      style={{
        border: "1px solid red",
        display: "flex",
        alignItems: "center",
        justifyContent: "space-around"
      }}
    >
      <h4>{title}</h4>
      <h4>{price}</h4>
      <Button
        id={id}
        price={price}
        quantity={quantity}
        changePrice={changePrice}
        amount={amount}
      />
    </div>
  );
};
export default CartItem;
```
Button Component
```
const Button = ({ id, amount, price, quantity, changePrice }) => {
  return (
    <div
      style={{
        border: "1px solid red",
        display: "flex",
        alignItems: "center",
        gap: "10px",
        justifyContent: "space-around"
      }}
    >
      <button
        disabled={quantity <= 0 ? true : false}
        onClick={() => {
          changePrice(id, -1, -amount);
        }}
      >
        -
      </button>
      <h4>{quantity}</h4>
      <button
        disabled={quantity >= 10 ? true : false}
        onClick={() => {
          changePrice(id, +1, amount);
        }}
      >
        +
      </button>
    </div>
  );
};

export default Button;
```
Total Component
```
const Total = ({ price }) => {
  console.log(price);
  return (
    <div>
      <h4>Total: {price}</h4>
    </div>
  );
};
export default Total;
```
