# ps-visitor

node.js visit command `ps aux` and `kill`.

## Install

```bash
$ npm install ps-visitor
```

## API

### ps (condition, extra, keywords, filterWaste = true)

- `condition:Object`(optional): result query condition.
- `extra:string`(optional): `ps aux | ...` cmd extra, example: `grep node`.
- `keywords:string|string[]`(optional): result easy filter.
- `filterWaste:boolean`(optional): filter includes `grep` and `ps aux` process status.
- `return:Promise.<Object[]>`: return result.

### kill (pid, signal)

- `pid:number|string`: process id.
- `signal:number|string`(optional): kill signal id or name.
- `return:Promise`

### result

```javascript
resutl: [{
    user: '',
    pid: '',
    cpu: '',
    mem: '',
    vsz: '',
    rss: '',
    tt: '',
    stat: '',
    started: '',
    time: '',
    command: ''
}, ......]
```

### condition

```javascript
condition: {
    user: '~username',
    pid: '123456',
    cpu: '>1 <3',
    mem: '>2 <4',
    vsz: '>100 <200',
    rss: '>200 <300',
    tt: '',
    stat: '',
    started: '',
    time: '',
    command: '~node ~-h'
}
```

- `~`: contains
- `>`: greater then
- `<`: lower than

    ......

## Usage

```javascript
const ps_visitor = require('ps-visitor');

ps_visitor.ps({
  command: '~SourceTree'
}, 'grep SourceTree').then((result) => {
  console.log(result);
});

// console.log information:
// [ { user: 'username',
//     pid: '81756',
//     cpu: '0.0',
//     mem: '1.3',
//     vsz: '4382936',
//     rss: '159904',
//     tt: '??',
//     stat: 'S',
//     started: '9Sep17',
//     time: '1:59.54',
//     command: '/Applications/SourceTree.app/Contents/MacOS/SourceTree' } ]

```


