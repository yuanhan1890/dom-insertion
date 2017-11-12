This demo compares dom insertion count when vue and inferno patches vnode's children.

## Libraries

Vue2.5.3, Inferno3.0, G2.3.13

## Modification

**Vue**:

```javascript
// Line 5189 in Vue.js
function insertBefore (parentNode, newNode, referenceNode) {
  if (Vue.inCounting && parentNode.childNodes[0] && !Number.isNaN(parseInt(parentNode.childNodes[0].innerHTML))) {
    // Array.prototype.map.call(parentDom.childNodes, child => child.innerHTML).join(',')
    Vue.count ++
    if(Vue.logInsert) {
      console.log(`vue:[${Array.prototype.map.call(parentNode.childNodes, child => parseInt(child.innerHTML)).join(',')}]`)
    }
  }
  parentNode.insertBefore(newNode, referenceNode);
}
```

**Inferno**:

```javascript
// Line 2291 in Inferno.js
if (Inferno.inCounting && parentDom.childNodes[0] && !Number.isNaN(parseInt(parentDom.childNodes[0].innerHTML))) {
    if (Inferno.logInsert) {
        console.log(`infero:[${Array.prototype.map.call(parentDom.childNodes, child => child.innerHTML).join(',')}]`)
    }
    Inferno.count ++
}
```

## screenshot

![result result](https://github.com/yuanhan1890/dom-insertion/blob/master/screenshot.png)