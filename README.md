# ¿QUÉ ES UN PATRÓN DE DISEÑO? 🔍

Los patrones de diseño son soluciones predefinidas para problemas comunes en el diseño de software. Funcionan como plantillas adaptables que se pueden personalizar para abordar problemas recurrentes en el código.

## PATRONES CREACIONALES 🛠️

Estos patrones proporcionan mecanismos de creación de objetos que incrementan la flexibilidad y la reutilización del código existente.

| Patrón           | Descripción                                                                                         |
|------------------|-----------------------------------------------------------------------------------------------------|
| **Singleton**       | Garantiza que una clase tenga una sola instancia y proporciona un punto de acceso global a esa instancia. 🔒 |
| **Builder**         | Permite la construcción paso a paso de objetos complejos. Con este patrón, es posible producir diferentes tipos y representaciones de un objeto utilizando el mismo proceso de construcción. 🏗️ |
| **Prototype**       | Permite la creación de copias de objetos existentes sin que el código dependa de sus clases. 📑     |
| **Factory Method**  | Define una interfaz para la creación de objetos en una clase base, permitiendo que las subclases alteren el tipo de objetos que se crearán. 🏭|
| **Abstract Factory** | Facilita la creación de familias de objetos relacionados sin necesidad de especificar sus clases concretas. 🏭|


## ¿CUÁNDO USARLOS?

Los patrones creacionales se utilizan cuando necesitas crear objetos de manera flexible y desacoplada, evitando acoplar el código a clases concretas. 


## Singleton: 🕵️
### Cuando necesitas asegurar que una clase tenga solo una instancia en toda la aplicación:

```ts
class Singleton {
  private static instance: Singleton | null = null;

  private constructor() {}

  static getInstance(): Singleton {
    return this.instance || (this.instance = new Singleton());
  }
}

// Uso del Singleton
const instance1 = Singleton.getInstance();
const instance2 = Singleton.getInstance();
console.log(instance1 === instance2); // Output: true

```

## Builder: 🛠️ 
### Cuando necesitas construir objetos complejos paso a paso:

```ts
class Product {
  constructor(
    public property1: string,
    public property2: number,
    public property3: boolean
  ) {}
}

class ProductBuilder {
  constructor(
    private property1: string = "",
    private property2: number = 0,
    private property3: boolean = false
  ) {}

  build(): Product {
    return new Product(this.property1, this.property2, this.property3);
  }
}

// Uso del Builder
const product = new ProductBuilder("Value 1", 42, true).build();

console.log(product); // Output: Product {property1: "Value 1",property2: 42,property3: true}
```

## Prototype: 🔄
### Cuando necesitas crear objetos basados en prototipos existentes:

```ts
// Interfaz para el prototipo
interface Prototype {
    clone(): Prototype;
}

// Implementación concreta del prototipo
class ConcretePrototype implements Prototype {
    clone(): Prototype {
        return new ConcretePrototype();
    }
}

// Uso del prototipo
const original = new ConcretePrototype();
const clone = original.clone();

// ConcretePrototype {}
```

## Factory Method: 🏭
### Cuando quieres desacoplar la creación de objetos de su uso:

```ts
interface Product {
  name: string;
}

class ConcreteProduct implements Product {
  constructor(public name: string) {}
}

abstract class Creator {
  abstract factoryMethod(): Product;
}

class ConcreteCreator extends Creator {
  factoryMethod(): Product {
    return new ConcreteProduct("Product");
  }
}

// Uso del Factory Method
const creator = new ConcreteCreator();
const product = creator.factoryMethod();
console.log(product); // Output: ConcreteProduct { name: 'Product' }
```

## Abstract Factory: 🏭
### Cuando necesitas crear familias de objetos relacionados sin especificar sus clases concretas:

```ts
// Definición de productos y sus métodos
interface Product {
  operation(): void;
}

class ConcreteProductA implements Product {
  operation(): void {
    console.log('Operación de Producto A');
  }
}

class ConcreteProductB implements Product {
  operation(): void {
    console.log('Operación de Producto B');
  }
}

// Definición de la fábrica abstracta
interface Factory {
  createProductA(): Product;
  createProductB(): Product;
}

// Implementación de la fábrica concreta
class ConcreteFactory implements Factory {
  createProductA(): Product {
    return new ConcreteProductA();
  }

  createProductB(): Product {
    return new ConcreteProductB();
  }
}

// Uso de la fábrica
const factory: Factory = new ConcreteFactory();
const productA = factory.createProductA();
const productB = factory.createProductB();

productA.operation(); // Output: Operación de Producto A
productB.operation(); // Output: Operación de Producto B
````