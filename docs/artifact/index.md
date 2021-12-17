# Artifact

```js script
class CardList extends HTMLElement {
  static get observedAttributes() {
    return ['data'];
  }
  constructor() {
    super();
    const shadowRoot = this.attachShadow({ mode: 'open' });
  }

  connectedCallback() {
      this.render();
  }

  attributeChangedCallback(name, oldValue, newValue) {
      // nothing
  }

  async render() {
      const shadow = this.shadowRoot;
      const data = await this.fetch();
      shadow.innerHTML = data.items.map((i) => {
        return `<div>${i.name}</div>`
      }).join('');
  }

  async fetch() {
    return await (await fetch(`./${this.getAttribute('data')}`)).json();
  }
}

customElements.define('card-list', CardList);
```

<card-list data="index.json"></card-list>