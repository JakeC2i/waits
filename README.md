# BRIT - the dependency injector

BRIT is **B**arebone **R**eflective Dependency **I**njector for **T**ypeScript.

### What it is

It's a simple, Angular-like, reflection-based dependency injector for NodeJS and Browser.

### What it can do

Its stand-out feature is the ability to "asynchronously wait" for the synchronously constructed class
to be marked as ready, before proceeding with its injection / instantiation job with other classes.

### Prerequisites

Your `tsconfig.json` must include:

```json
{
  "compilerOptions": {
    "experimentalDecorators": true,
    "emitDecoratorMetadata": true  
  }
}
```

### Installation

```
$ npm install brit
```

### Basic usage

Decorate all class declarations (including root class) with `@Injectable`.

```typescript
// This is some dependency class
@Injectable()
export class Walls {
  constructor() {
    console.log('Walls constructed synchronously and ready');
  }
}

// This is the root class
@Injectable()
export class House {
  constructor(
    private _walls: Walls
  ) {
    console.log('House constructed and ready');
  }
}

// Get injector and begin the injection!
const injector = getInjectorManager().getInjector();
injector.injectFor<House>(House)
  .then((house) => {
    console.log(house);
  })
  .catch(error => {
    console.error(error);
  });
```

### Advanced usage

All other features are shown in the `/example` directory.
Inspect the `/example/_classes.ts` and learn!

* Asynchronous (regular) usage - run `npm run async-example`;
* Synchronous usage - run `npm run sync-example`

### TODO

* Tests
* Multiple injectors, remove singleton requirement
* Constructor arguments for the injectable provider
* Cyclic dependency detection

### License

This project is licensed under the MIT License.
