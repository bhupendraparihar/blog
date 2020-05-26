---
title: "Patterns with Async call : Beautiful Javascript"
date: 2020-05-23 16:27:09
tags:
---
</title>

Asynchornous call is very famous for its callback hell

<pre>
getData(a => {
    getMoreData(a, b => {
        getMoreData(b, c => {
            getMoreData(c, d => {
                getMoreData(d, e => {
                    console.log(e);
                });
            });
        });
    });
});
</pre>

Promise Hell
<pre>
getData()
.then(a => getMoreData(a))
.then(b => getMoreData(b))
.then(c => getMoreData(c))
.then(d => getMoreData(d))
.then(e => console.log(e));
</pre>

Its' not over yet
<pre>
getData()
.then(getMoreData)
.then(getMoreData)
.then(getMoreData)
.then(getMoreData)
.then(console.log);
</pre>

Looks synchronous with async-await
<pre>
(async () => {
    const a = await getData();
    const b = await getMoreData(a);
    const c = await getMoreData(b);
    const d = await getMoreData(c);
    const e = await getMoreData(d);
    console.log(e);
})
</pre>