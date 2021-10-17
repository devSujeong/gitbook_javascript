# Module

## Module?

의도하지 않은 변수의 오버라이딩을 막고, 모든 것이 전역변수가 되는 것을 막기 위해 존재합니다.

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

{% code title="Export.js" %}
```javascript
import * as calculator from './Import.js';
import add from './Import.js';
import add, {sup as minus} from './Import.js';
```
{% endcode %}

