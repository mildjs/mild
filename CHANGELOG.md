
# Changelog

## Version 1.1.0

- Remove `typeorm` and `typeorm-di` dependencies
- `useExpressServer` require to pass `Container` from `typedi`  for injecting the service.

## Version 1.0.0

### Features
- `@Use` decorator (middleware) support class and method levels. using `@Use` in the class, it will be applied the all class's methods.
  - The order will apply on *the class* first, then *the method*

### Refactor

- Remove `Reflect-metadata` for collecting class or function metadata from the decorators, using the global variables instead (`getMetadataArgsStore()`)
- For Express middleware, rename the decorator from `@Middleware` to `@Use`
- Remove `addExpressServer`, please use `useExpressServer` instead.


## Version 0.1.4

### Express Extension

- Support dependency injection for the providers, using the module for controlling the controller and provider. [(commit link)](https://github.com/mildronize/route-controller/commit/f0d3af49c6e8385cb3224e6d11dc495ee8953b4e)

    Previously

    ```typescript
    const app = Express();
    addExpressController(app, [UserController, IndexController]);
    ```

    Added providers

    ```typescript
    const app = Express();
    useExpressServer(app, [UserModule, IndexModule]);
    ```

    ```typescript
    // UserModule.ts
    @Module({
        controllers: [UserController],
        providers: [UserService]
    })
    export class UserModule {}

    // IndexModule.ts
    @Module({
        controllers: [IndexController],
        providers: [IndexService]
    })
    export class IndexModule {}
    ```


### Decoratos

- Http Method & Middleware can swapable [(commit link)](https://github.com/mildronize/route-controller/commit/632fbddfc97dbf8f011f6f746a9183b7ff4efc74) 
    

    ```typescript
    @Get('/')
    @Middleware(validate) 
    ```

    or 

    ```typescript
    @Middleware(validate) 
    @Get('/')
    ```

    