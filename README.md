# react-outside-click-handler

> A React component for handling outside clicks

## Usage

```
import OutsideClickHandler from 'react-outside-click-handler';

function MyComponent() {
  return (
    <OutsideClickHandler
      onOutsideClick={() => {
        alert('You clicked outside of this component!!!');
      }}
    >
      Hello World
    </OutsideClickHandler>
  );
}
```

For full browser support, `react-outside-click-handler` expects its consumer to include [airbnb-browser-shims](https://github.com/airbnb/browser-shims) or another similar shim. This is specifically due to the use of the [`node.contains`](https://developer.mozilla.org/en-US/docs/Web/API/Node/contains) method.

## Props

### children: `PropTypes.node.isRequired`

Since the `OutsideClickHandler` specifically handles clicks outside a specific subtree, `children` is expected to be defined. A consumer should also not render the `OutsideClickHandler` in the case that `children` are not defined.

_Note that if you use a `Portal` (native or `react-portal`) of any sort in the `children`, the `OutsideClickHandler` will not behave as expected._

### onOutsideClick: `PropTypes.func.isRequired`

The `onOutsideClick` prop is also required as without it, the `OutsideClickHandler` is basically a heavy-weight `<div />`. It takes the relevant clickevent as an arg and gets triggered when the user clicks anywhere outside of the subtree generated by the DOM node.

### disabled: `PropTypes.bool`

If the `disabled` prop is true, outside clicks will not be registered. This can be utilized to temporarily disable interaction without unmounting/remounting the entire tree.

### useCapture: `PropTypes.bool`

See https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events#Event_bubbling_and_capture for more information on event bubbling vs. capture.

If `useCapture` is true, the event will be registered in the capturing phase and thus, propagated top-down instead of bottom-up as is the default.

### display: `PropTypes.oneOf(['block', 'flex, 'inline-block'])`

By default, the `OutsideClickHandler` renders a `display: block` `<div />` to wrap the subtree defined by `children`. If desired, the `display` can be set to `inline-block` or `flex` instead. There is no way not to render a wrapping `<div />`.
