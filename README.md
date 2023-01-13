# Web-Components-Example

```ts
const RubyElement = class MyElement extends HTMLElement {
  /**
   * 监控属性
   */
  static observedAttributes = ['data-ruby'] as const

  /**
   * 组件初始化函数
   */
  constructor() {
    super();
    const shadowRoot = this.attachShadow({ mode: 'open' });
    shadowRoot.innerHTML = `<ruby><slot></slot><rp>(</rp><rt></rt><rp>)</rp></ruby>`;
    // shadowRoot.adoptedStyleSheets = [sheet];
  }

  // 生命周期函数
  connectedCallback() {
    console.log('Custom square element added to page.');
  }
  disconnectedCallback() {
    console.log('Custom square element removed from page.');
  }
  adoptedCallback() {
    console.log('Custom square element moved to new page.');
  }

  /**
   * 监控属性变更
   */
  attributeChangedCallback(
    name: typeof MyElement['observedAttributes'][number],
    oldValue: string,
    newValue: string
  ) {
    console.log('Custom square element attributes changed.', { name, oldValue, newValue });
    if (name === "data-ruby") {
      this.shadowRoot!.querySelector('rt')!.innerHTML = newValue;
    }
  }

  // 注册元素
  static {
    customElements.define('ru-by', this);
  }
}
```
