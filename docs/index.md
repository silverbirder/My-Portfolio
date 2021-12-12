# Blog
## This is my-el

<custom-square l="100" c="red" j="index.json"></custom-square>

```js script
// import emojiPickerElement from 'https://cdn.skypack.dev/emoji-picker-element';

class Square extends HTMLElement {
  static get observedAttributes() {
    return ['c', 'l', 'j'];
  }
  constructor() {
    super();
    const shadow = this.attachShadow({mode: 'open'});
    const div = document.createElement('div');
    const style = document.createElement('style');
    shadow.appendChild(style);
    shadow.appendChild(div);
  }

  connectedCallback() {
    updateStyle(this);
  }
  attributeChangedCallback(name, oldValue, newValue) {
    updateStyle(this);
    if (name != "j") return;
    if (oldValue == newValue) return;
    fetch(`./${this.getAttribute('j')}`).then((r) => { r.json().then((j) => { console.log(j);})})
  }
}

customElements.define('custom-square', Square);

function updateStyle(elem) {
  const shadow = elem.shadowRoot;
  shadow.querySelector('style').textContent = `
    div {
      width: ${elem.getAttribute('l')}px;
      height: ${elem.getAttribute('l')}px;
      background-color: ${elem.getAttribute('c')};
    }
  `;
}
```
