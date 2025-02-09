# The basic stuff

### Simplified version
```js
const pipe = (...fns) => handler => fns.reduce((effects, fn) => fn(effects), handler);
```

Sample of _from_, _map_, _filter_ implementation [Link](https://www.codemotion.com/magazine/frontend/javascript/the-magic-behind-rxjs/)
```js
function createObservable(operator) {
    return {
        subscribe(next) {
            operator(next);
        }
    }
}

function from(initData) {
    return {
        pipe: (...pipeFns) => {
            return {
                subscribe: (onNext, onError, onComplete) => {
                    const dataObs = createObservable(handler => initData.forEach(handler));

                    let curObs = dataObs;
                    pipeFns.forEach(pipeFn => {
                        curObs = pipeFn(curObs);
                    });

                    curObs.subscribe(onNext);

                    onComplete();
                }
            }
        }
    }
}

function map(mapFn) {
    return sourceObs => {
        const curObs = createObservable(destinationNext => {
            sourceObs.subscribe(value => {
                const newValue = mapFn(value);
                destinationNext(newValue);
            })
        });

        return curObs;
    }
}

function filter(filterFunction) {
    return sourceObs => {
        const curObs = createObservable(destinationNext => {
            sourceObs.subscribe(value => {
                if (filterFunction(value)) {
                    destinationNext(value);
                }
            })
        })
        return curObs;
    }
}
```
