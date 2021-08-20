# base64

## Deprecated method

base64 인코딩, 디코딩을 검색해 보면 atob 메소드들이 나옵니다. 정말 간단하지만, 에디터에서 해당 메소드는 legacy 코드라고 하네요! ㅠ

```javascript
test = 'webisfree';
test2 = btoa(test);

"d2ViaXNmcmVl"  //  base64로 변환되어 출력되었음

atob("d2ViaXNmcmVl");

"webisfree"  //  base64에서 디코딩하여 원래값을 반환

btoa(unescape(encodeURIComponent(str))) // encoding이 안될 때(한글이거나 8비트로 문자열이 표현되지 않을 때 변환이 안될 수 있습니다. 그럴 땐 아래처럼 진행)
```



