### 基础数据类型

```
let flag: boolean = true;
let num: number = 123;
let arr: number[] = [1, 3, 4];
let arr2: any[] = ['s', '3', 'v'];
let arr1: Array<number> = [1, 2, 3, 4];
//元组 tuple
let arr3: [number, string] = [123, 'this is'];

//enum  枚举
enum Color {blue, red, 'orange'}

let c: Color = Color.blue;
console.log(c);// 如果标识符没有赋值,它的值就是下标
enum Err {'undefined' = 1, 'null' = 2, 'success' = -1}

//任意类型any
let num2: any = 123;
let num3: any = 'str';
//任意类型的类型
//null  undefined
let num4:number|undefined;

let num5:null;
//一个元素可能是
let num6:number|null|undefined;
//void 没有任意类型  没有返回值
function run():void {

}
//never  类型  代表从来都不会出现的值
let a:never;
```