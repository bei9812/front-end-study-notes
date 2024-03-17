# Rxjs

1. 学习网站
`https://rxmarbles.com/`   **用原子图显示operators**
`https://reactive.how/rxjs`     **用对比图显示不同的用原子图显示operators**
`https://rxjs.dev/operator-decision-tree`   **官网能够提根据不同的条件给出使用哪个operator的建议**
`https://stackblitz.com/edit`   **在线编辑rxjs**
<br>
2. 引入
```
import { Subject, fromEvent, interval } from 'rxjs';
import { filter,take } from 'rxjs/operators';
```
3. 观察者概念
```
var click$ = fromEvent(document, 'click'); //建立可观察的Observable物件
var observer = { next: (x) => console.log(x) }; //建立观察者物件Observer
var subs$ = click$.subscribe(observer); //建立订阅物件 （订阅Observable物件，并传入Observer观察者物件）
```

4. 取消订阅
```
var a = interval(500).pipe(take(4)).subscribe(console.log);
a.unsubscribe();
```

5. 多个操作符
```
var subs =  click$.pipe(
    filter(d as => d.clientX < 100),
    take(4)).subscribe(console.log)
```

6. Subject广播
```
var subject = new Subject(); //建立主题物件Subject 之后靠这个主题物件进行广播
var clicks$ = fromEvent(document, 'click'); //建立可观察的Observable物件
clicks$ = clicks$.pipe(take(2)); //设定取得两个事件资料就将Observable物件设为完成
clicks$.subscribe(subject);//设定将clicks$全部交友subject主题物件进行广播
var subs1$ = subject.subscribe((x)=> console.log(x.clientX))
```