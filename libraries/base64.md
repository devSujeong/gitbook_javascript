# base64

## Encoding

```javascript
test = 'webisfree';
test2 = btoa(test);

"d2ViaXNmcmVl"  //  base64로 변환되어 출력되었음
```

### Encoding이 안될 경우

한글이거나 8비트로 문자열이 표현되지 않을 때 변환이 안될 수 있습니다. 그럴 땐 아래처럼 진행

```javascript
btoa(unescape(encodeURIComponent(str)))
```

## Decoding

```javascript
atob("d2ViaXNmcmVl");

"webisfree"  //  base64에서 디코딩하여 원래값을 반환
```

## 

