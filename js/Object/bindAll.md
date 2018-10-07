# bindAll

## EXPLAIN 
当外部调用方法时候this的指向会指向其他作用域,这个方法是把this指向当前对象
```javascript
const bindAll = (obj, ...fns) =>
  fns.forEach(
    fn => (
      (f = obj[fn]),
      (obj[fn] = function() {
        return f.apply(obj);
      })
    )
  );
```
## REVISE

## USE

## EXAMPLES 
```javascript
var view = {
  label: 'docs',
  click: function() {
      // 当外部使用这个方法的时候,可以调用这个this 
    console.log('clicked ' + this.label);
  }
};
bindAll(view, 'click');
jQuery(element).on('click', view.click); // Logs 'clicked docs' when clicked.

```