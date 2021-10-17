# Module

## Module?

의도하지 않은 변수의 오버라이딩을 막고, 모든 것이 전역변수가 되는 것을 막기 위해 존재합니다.

{% tabs %}
{% tab title="Import" %}
{% code title="Import.js" %}
```javascript
export default function add(a, b) {
  return a + b;
}
export function sup(a, b) {
  return a - b;
}
```
{% endcode %}
{% endtab %}

{% tab title="Export" %}
{% code title="Export.js" %}
```javascript
// Some cod
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% code title="Export.js" %}
```
// Some cod
```
{% endcode %}

import \* as calculator from './10-3-module1.js';

import add from './Import.js';

import 
