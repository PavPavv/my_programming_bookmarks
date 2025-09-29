# TypeScript

## Basics

### Модификаторы доступа

Модификаторы доступа позволяют сокрыть состояние объекта от внешнего доступа и управлять доступом к этому состоянию. В TypeScript три модификатора: **public, protected и private**.

#### Private

Если же к свойствам и методам применяется модификатор **private**, то к ним нельзя будет обратиться извне при создании объекта данного класса. (Можно обратиться только внутри самого класса в котором объявлены)

#### Protected

Модификатор **protected** определяет поля и методы, которые из вне класса видны только в классах-наследниках. (Можно обратиться только внутри самого класса в котором объявлены или только внутри класса -наследника). Снаружи нигде нельзя!

#### Public

Можно обращаться везде!

Если к свойствам и функциям классов не применяется модификатор, то такие свойства и функции расцениваются как будто они определены с модификатором **public**.

```typescript
class Super {
    private _hello: string = 'hello!';

    constructor() {}

    protected foo(): void {
        console.log('foo!');
    }

    private bar(): void {
        console.log('bar!');
    }

    public test(): void {
        console.log('test!');
    }

    print(): void {
        console.log(this._hello);
    }
}

class Nice extends Super {
    constructor() {
        super();
    }

    getBar(): void {
        return this.bar();
    }

    getFoo(): void {
        return this.foo();
    }

}

const s = new Super();
console.log(s.bar()); // error
console.log(s._hello); // error

const n = new Nice();
console.log(n.bar()); // error
console.log(n.foo()); // error
console.log(n.getFoo());
console.log(n.test());
```

Чтобы обращаться к свойствам и методам родительского класса в конструкторе дочернего класса должен быть вызван глобавльный метод конструктра **super()**;

## Main

- 🧾 [Official docs](https://www.typescriptlang.org/docs/)
- 📋 [TS-total](https://github.com/harryheman/React-Total/blob/main/md/ts.md)
- 📋 [Brief explanation](https://2ality.com/2018/04/type-notation-typescript.html)
- 📋 [Handbook RU](https://typescript-handbook.ru/docs/ts-1/)

## Linter

- 🧾 [TSLint](https://palantir.github.io/tslint/)

## Parts

- 📋 [Static Properties, Abstract Classes, and Constructor Functions in TS](https://betterprogramming.pub/introduction-to-typescript-classes-static-properties-abstract-classes-and-more-869f1eaa4835)

## Record type

- 📋 [Record](https://stackoverflow.com/questions/51936369/what-is-the-record-type-in-typescript)

## React with TS

- 📋 [ReactTS cheatsheet](https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-started/basic_type_example/)
