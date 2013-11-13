---
layout: modern
title: 如何“重新发明”闭包
---

我最初是在<a href="http://paulgraham.com/hackpaint.html">《黑客与画家》</a>看到“闭包”这个术语，虽然我那时候还没有明白这个词语的意思，但那时我查阅了它在维基百科上的定义，却依然没有明白。直到现在，因为我在捣鼓 <a href="http://en.wikipedia.org/wiki/Lambda_calculus">Lambda Calculus</a> ，才慢慢懂得“闭包”的含义。

为了防止以后的自己忘记，于是我写这篇 Blog 来帮助别人理解或者未来的自己。P.S. 本文使用 Scheme 语言进行解释，并且以实现一个“累加器”函数为目的。

怎么在 Scheme 中写一个匿名函数返回输入的值呢？显然很简单...

    ((lambda (x) x) 7)
    ;; => 7
    
那如果要在匿名函数中实现返回一个数的平方呢？

    ((lambda (x) (* x x)) 5)
    ;; => 25
    
既然可以使用乘法，那我们或许可以使用其它函数，如 set!

    (set! x 0)                         ;先将x设置为0
    ((lambda (i) (set! x (+ x i))) 2)  ;将2累加到x上
    ;; => x: 2
    ((lambda (i) (set! x (+ x i))) 3)
    ;; => x: 5                         ;因为x已经等于2，所以累加3到x得到5
    
这样使用“累加器”不方便，如果把它做成一个函数会呢？

    (define acc
      (lambda (x)
        (lambda (i)
          (set! x (+ x i))             ;累加i到x上
          x)))                         ;返回x的值
          
    (set! foo (acc 5))
    (foo 2) ;is equivalent to ((acc 5) 2)
    ;; => 7
    (foo 3) ;is equivalent to ((acc ((acc 5) 2)) 3)
    ;; => 10
    
这样我们就实现了一个“累加器”。它的作用就是把计算产生的值储存在一个结果中（函数中结果即x，之后累加的数字都储存在x中）。此处就用到了闭包，因为函数中的 i 并不是直接使用的。

如果还有心情的话看下一个例子...无解释。

    > (set! lst '())
    > lst
    ()
    > ((lambda (x) (set! lst (cons x lst))) 1)
    > lst
    (1)
    > ((lambda (x) (set! lst (cons x lst))) 3)
    > lst
    (3 1)
    > ((lambda (x) (set! lst (cons x lst))) 7)
    > lst
    (7 3 1)