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
      const articles = data.items.map((i) => {
        return `        
        <article>
            <a href="${i.url}" class="thumbnail" style="background-image: url(${i.image});"></a>
            <div class="content">
                <h2><a href="${i.url}">${i.name}</a></h2>
                <p>${i.date}</p>
            </div>
        </article>
      `}).join('');
      shadow.innerHTML = `<div class="articles">${articles}</div>`
  }

  async fetch() {
    return await (await fetch(`./${this.getAttribute('data')}`)).json();
  }
}

customElements.define('card-list', CardList);
```

# Goods

<card-list data="index.json"></card-list>