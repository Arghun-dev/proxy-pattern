# proxy-pattern

Tradeoffs

`Advantages`: 

  proxies make it easy to add functionality when interacting with a certain object, such as validaion, logging, formatting, notifications, debuggin ...
  

`Disadvantage`:

  Long handler execution


Example: 


```js
const person = {
  name: "arghun",
  age: 20
};

const personProxy = new Proxy(person, {
  get: (target, prop) => {
    return `The value for ${prop} is ${target[prop]}`;
  },

  set: (target, prop, value) => {
    if (prop === "name") {
      if (value.length < 3) {
        throw new Error("please add valid name");
      }
    }

    if (prop === "age") {
      if (value < 15) {
        throw new Error("age should be higher than 15");
      }
    }

    return Reflect.set(target, prop, value);
  }
});

personProxy.name = "afh";
```
