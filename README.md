# Top Down Operator Precedence JavaScript Parser


In Douglas Crockford's article [Top Down Operator Precedence](http://javascript.crockford.com/tdop/tdop.html) 
he implements a parser first presented by Vaughan Pratt. I'll be building the same Parser myself, with the hopes of extending it for fun.  
<br>
<br>
# Background






# Use

As this project is in a very early stage, it has limited useability. 
It currently runs on NodeJS, but I hope to extend it for the browser too. 
The `printTree` module will take a JS file as an argument, and output the tree 
generated by `parser.js` to the command-line. 
<br>
<br>
A little test file is included, `test01.js`, which looks like:

##test01.js
```javascript

var fun = function (x, y, z) {
  return ((x * y) / z);
};

var wow = fun(2, 3, 4);

```
<br>
<br>
You can see how the parser works by using `printTree` on the `test01.js` file (or any [Simplified JavaScript](http://stackoverflow.com/a/4577277)) via

```
$ node printTree test01.js
```
<br>
<br>
The output should look like so:
```
Scanning..
Parsing..
Printing Tree for test01.js:

[ { value: '=',
    arity: 'binary',
    first: 
     { value: 'fun',
       arity: 'name',
       reserved: false,
       nud: [Function: itself],
       led: null,
       std: null,
       lbp: 0,
       scope: 
        { def: 
           { var: { value: 'var', arity: 'name', reserved: true },
             fun: [Circular],
             wow: 
              { value: 'wow',
                arity: 'name',
                reserved: false,
                nud: [Function: itself],
                led: null,
                std: null,
                lbp: 0,
                scope: [Circular] } },
          parent: undefined } },
    second: 
     { value: 'function',
       arity: 'function',
       first: 
        [ { value: 'x',
            arity: 'name',
            reserved: false,
            nud: [Function: itself],
            led: null,
            std: null,
            lbp: 0,
            scope: 
             { def: 
                { x: [Circular],
                  y: 
                   { value: 'y',
                     arity: 'name',
                     reserved: false,
                     nud: [Function: itself],
                     led: null,
                     std: null,
                     lbp: 0,
                     scope: [Circular] },
                  z: 
                   { value: 'z',
                     arity: 'name',
                     reserved: false,
                     nud: [Function: itself],
                     led: null,
                     std: null,
                     lbp: 0,
                     scope: [Circular] },
                  return: 
                   { value: 'return',
                     arity: 'statement',
                     reserved: true,
                     first: 
                      { value: '/',
                        arity: 'binary',
                        first: 
                         { value: '*',
                           arity: 'binary',
                           first: { value: 'x', arity: 'name' },
                           second: { value: 'y', arity: 'name' } },
                        second: { value: 'z', arity: 'name' } } } },
               parent: 
                { def: 
                   { var: { value: 'var', arity: 'name', reserved: true },
                     fun: 
                      { value: 'fun',
                        arity: 'name',
                        reserved: false,
                        nud: [Function: itself],
                        led: null,
                        std: null,
                        lbp: 0,
                        scope: [Circular] },
                     wow: 
                      { value: 'wow',
                        arity: 'name',
                        reserved: false,
                        nud: [Function: itself],
                        led: null,
                        std: null,
                        lbp: 0,
                        scope: [Circular] } },
                  parent: undefined } } },
          { value: 'y',
            arity: 'name',
            reserved: false,
            nud: [Function: itself],
            led: null,
            std: null,
            lbp: 0,
            scope: 
             { def: 
                { x: 
                   { value: 'x',
                     arity: 'name',
                     reserved: false,
                     nud: [Function: itself],
                     led: null,
                     std: null,
                     lbp: 0,
                     scope: [Circular] },
                  y: [Circular],
                  z: 
                   { value: 'z',
                     arity: 'name',
                     reserved: false,
                     nud: [Function: itself],
                     led: null,
                     std: null,
                     lbp: 0,
                     scope: [Circular] },
                  return: 
                   { value: 'return',
                     arity: 'statement',
                     reserved: true,
                     first: 
                      { value: '/',
                        arity: 'binary',
                        first: 
                         { value: '*',
                           arity: 'binary',
                           first: { value: 'x', arity: 'name' },
                           second: { value: 'y', arity: 'name' } },
                        second: { value: 'z', arity: 'name' } } } },
               parent: 
                { def: 
                   { var: { value: 'var', arity: 'name', reserved: true },
                     fun: 
                      { value: 'fun',
                        arity: 'name',
                        reserved: false,
                        nud: [Function: itself],
                        led: null,
                        std: null,
                        lbp: 0,
                        scope: [Circular] },
                     wow: 
                      { value: 'wow',
                        arity: 'name',
                        reserved: false,
                        nud: [Function: itself],
                        led: null,
                        std: null,
                        lbp: 0,
                        scope: [Circular] } },
                  parent: undefined } } },
          { value: 'z',
            arity: 'name',
            reserved: false,
            nud: [Function: itself],
            led: null,
            std: null,
            lbp: 0,
            scope: 
             { def: 
                { x: 
                   { value: 'x',
                     arity: 'name',
                     reserved: false,
                     nud: [Function: itself],
                     led: null,
                     std: null,
                     lbp: 0,
                     scope: [Circular] },
                  y: 
                   { value: 'y',
                     arity: 'name',
                     reserved: false,
                     nud: [Function: itself],
                     led: null,
                     std: null,
                     lbp: 0,
                     scope: [Circular] },
                  z: [Circular],
                  return: 
                   { value: 'return',
                     arity: 'statement',
                     reserved: true,
                     first: 
                      { value: '/',
                        arity: 'binary',
                        first: 
                         { value: '*',
                           arity: 'binary',
                           first: { value: 'x', arity: 'name' },
                           second: { value: 'y', arity: 'name' } },
                        second: { value: 'z', arity: 'name' } } } },
               parent: 
                { def: 
                   { var: { value: 'var', arity: 'name', reserved: true },
                     fun: 
                      { value: 'fun',
                        arity: 'name',
                        reserved: false,
                        nud: [Function: itself],
                        led: null,
                        std: null,
                        lbp: 0,
                        scope: [Circular] },
                     wow: 
                      { value: 'wow',
                        arity: 'name',
                        reserved: false,
                        nud: [Function: itself],
                        led: null,
                        std: null,
                        lbp: 0,
                        scope: [Circular] } },
                  parent: undefined } } } ],
       second: 
        { value: 'return',
          arity: 'statement',
          reserved: true,
          first: 
           { value: '/',
             arity: 'binary',
             first: 
              { value: '*',
                arity: 'binary',
                first: { value: 'x', arity: 'name' },
                second: { value: 'y', arity: 'name' } },
             second: { value: 'z', arity: 'name' } } } } },
  { value: '=',
    arity: 'binary',
    first: 
     { value: 'wow',
       arity: 'name',
       reserved: false,
       nud: [Function: itself],
       led: null,
       std: null,
       lbp: 0,
       scope: 
        { def: 
           { var: { value: 'var', arity: 'name', reserved: true },
             fun: 
              { value: 'fun',
                arity: 'name',
                reserved: false,
                nud: [Function: itself],
                led: null,
                std: null,
                lbp: 0,
                scope: [Circular] },
             wow: [Circular] },
          parent: undefined } },
    second: 
     { value: '(',
       arity: 'binary',
       first: { value: 'fun', arity: 'name' },
       second: 
        [ { value: 2, arity: 'literal' },
          { value: 3, arity: 'literal' },
          { value: 4, arity: 'literal' } ] } } ]


```



## References

[Eli Bendersky](http://eli.thegreenplace.net/2010/01/02/top-down-operator-precedence-parsing/) has a nice blog-post
 about how TDOP works. I plan on adding documentation to the parser and
 it will be in part based on his work. 

