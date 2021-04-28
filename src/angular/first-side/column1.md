# Bootstrapping

Bootstraps the app, using the root component from the specified __NgModule__.

```js
import { platformBrowserDynamic }
    from '@angular/platform-browser-dynamic';

platformBrowserDynamic()
    .bootstrapModule(AppModule);
```

# NgModule

**Defines a module** that contains components, directives, pipes, and providers.

```js
import { NgModule } from '@angular/core';

@NgModule({
    declarations: [
        MyRootComponent,
        MyComponent,
        MyDirective,
        MyPipe],
    imports: [MyModule, NpmModule],
    exports: [MyComponent],
    providers: [MyService],
    bootstrap: [MyRootComponent] // Only root module
})
class MyModule {}
```








The **pipes** and **directive** is declared as **components**
