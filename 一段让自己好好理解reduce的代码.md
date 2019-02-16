```
const pick = (obj, arr) =>
    arr.reduce((acc, curr) => (curr in obj && (acc[curr] = obj[curr]), acc), {});
const pick = (obj, arr) => arr.reduce((k, v) => {
    //第一个参数为迭代对象第二个为目标对象
    if ((v in obj) && (k[v] = obj[v])) {
        return v, k;
    }
}, {});
console.log(pick({'a': 1, 'b': '2', 'c': 3}, ['a', 'c']));
```

