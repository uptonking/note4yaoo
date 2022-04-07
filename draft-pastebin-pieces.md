---
title: draft-pastebin-pieces
tags: [draft, todo]
pinned: true
created: '2019-11-11T06:57:46.101Z'
modified: '2021-03-22T18:24:50.639Z'
---

# draft-pastebin-pieces

 

------  

- debt
  - 金敏小姐(2017) - 30000
  - 大丫(2016) - 17000 + 2000
  - 小姨(2016) - 20000 + 1500
  - mom 
    - 6212 2518 0900 0758 487
    - 6212251809000758487

- 拼多多 链接分析

```

- 小虎宝儿 买一送一

https://mobile.yangkeduo.com/promotion_op.html?id=181215&subject_id=&type=5&refer_share_id=de9501e0a57f42b7a702565df1d963b4&refer_share_uid=9312667688517&refer_share_uin=TDBQE7Z3O5XOS4XUPTVYWPPN4E_GEXDA&refer_share_channel=copy_link&refer_share_form=text

- 拓路者 买一送一

https://mobile.yangkeduo.com/promotion_op.html?id=181999&subject_id=&type=5&refer_share_id=6b73d175a0c644e1ac09971b272f40f1&refer_share_uid=9312667688517&refer_share_uin=TDBQE7Z3O5XOS4XUPTVYWPPN4E_GEXDA&refer_share_channel=copy_link&refer_share_form=text

```

- js产生定长字符串

```JS
Math.random()
  .toString(36)
  .replace(/[^a-z]+/g, '')
  .substring(0, 5);
```

- authing返回值

```JS
{
  "thirdPartyIdentity": {
    "provider": null,
    "refreshToken": null,
    "accessToken": null,
    "scope": null,
    "expiresIn": null,
    "updatedAt": null
  },
  "id": "619cb7c0032ec5e844cb3afe",
  "createdAt": "2021-11-23T09:43:28.608Z",
  "updatedAt": "2021-11-24T06:30:23.372Z",
  "userPoolId": "60c8119da4f0d6f59c0b9560",
  "isRoot": false,
  "status": "Activated",
  "oauth": null,
  "email": "jinyaoo@qq.com",
  "phone": null,
  "username": null,
  "unionid": null,
  "openid": null,
  "nickname": null,
  "company": null,
  "photo": "https://files.authing.co/authing-console/default-user-avatar.png",
  "browser": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.45 Safari/537.36 Edg/96.0.1054.29",
  "device": "Windows",
  "password": "aebb787f0bd5f0f99a252af7015881dd",
  "salt": "ief7ddcppmn",
  "loginsCount": 13,
  "lastIp": "183.128.81.208",
  "name": null,
  "givenName": null,
  "familyName": null,
  "middleName": null,
  "profile": null,
  "preferredUsername": null,
  "website": null,
  "gender": "U",
  "birthdate": null,
  "zoneinfo": null,
  "locale": null,
  "address": null,
  "formatted": null,
  "streetAddress": null,
  "locality": null,
  "region": null,
  "postalCode": null,
  "city": null,
  "province": null,
  "country": null,
  "registerSource": [
    "basic:email"
  ],
  "secretInfo": null,
  "emailVerified": true,
  "phoneVerified": false,
  "lastLogin": "2021-11-24T06:30:23.363Z",
  "blocked": false,
  "isDeleted": false,
  "sendSmsCount": 0,
  "sendSmsLimitCount": 1000,
  "encryptedPassword": "rNCATAAD4zq4N1faSBGrBWC0CsA0spYZHrzA1OoqGDlOC+u4UGk6rT13Iystmbgo7c7aQiM2uHRMHBVFLFD0TyWJ4J9sA1uqYrr/wk7w/vmk+jw6YNWJrVnPUAzdaOiY2jovycjoIAg29d6ZKIusP70Kte4WMmT8LsBVONP/JaM=",
  "signedUp": "2021-11-23T09:43:28.608Z",
  "externalId": null,
  "mainDepartmentId": null,
  "mainDepartmentCode": null,
  "lastMfaTime": null,
  "passwordSecurityLevel": 1,
  "resetPasswordOnFirstLogin": false,
  "syncExtInfo": null,
  "phoneCountryCode": null,
  "lastIP": "183.128.81.208",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1cGRhdGVkX2F0IjoiMjAyMS0xMS0yM1QxMzozMToxOS4yMDdaIiwiYWRkcmVzcyI6eyJjb3VudHJ5IjpudWxsLCJwb3N0YWxfY29kZSI6bnVsbCwicmVnaW9uIjpudWxsLCJmb3JtYXR0ZWQiOm51bGx9LCJwaG9uZV9udW1iZXJfdmVyaWZpZWQiOmZhbHNlLCJwaG9uZV9udW1iZXIiOm51bGwsImxvY2FsZSI6bnVsbCwiem9uZWluZm8iOm51bGwsImJpcnRoZGF0ZSI6bnVsbCwiZ2VuZGVyIjoiVSIsImVtYWlsX3ZlcmlmaWVkIjp0cnVlLCJlbWFpbCI6Imppbnlhb29AcXEuY29tIiwid2Vic2l0ZSI6bnVsbCwicGljdHVyZSI6Imh0dHBzOi8vZmlsZXMuYXV0aGluZy5jby9hdXRoaW5nLWNvbnNvbGUvZGVmYXVsdC11c2VyLWF2YXRhci5wbmciLCJwcm9maWxlIjpudWxsLCJwcmVmZXJyZWRfdXNlcm5hbWUiOm51bGwsIm5pY2tuYW1lIjpudWxsLCJtaWRkbGVfbmFtZSI6bnVsbCwiZmFtaWx5X25hbWUiOm51bGwsImdpdmVuX25hbWUiOm51bGwsIm5hbWUiOm51bGwsInN1YiI6IjYxOWNiN2MwMDMyZWM1ZTg0NGNiM2FmZSIsImV4dGVybmFsX2lkIjpudWxsLCJ1bmlvbmlkIjpudWxsLCJ1c2VybmFtZSI6bnVsbCwiZGF0YSI6eyJ0eXBlIjoidXNlciIsInVzZXJQb29sSWQiOiI2MGM4MTE5ZGE0ZjBkNmY1OWMwYjk1NjAiLCJhcHBJZCI6IjYxOTYxYTdiOGI5MGFmMzdlN2M0MjJlMCIsImlkIjoiNjE5Y2I3YzAwMzJlYzVlODQ0Y2IzYWZlIiwidXNlcklkIjoiNjE5Y2I3YzAwMzJlYzVlODQ0Y2IzYWZlIiwiX2lkIjoiNjE5Y2I3YzAwMzJlYzVlODQ0Y2IzYWZlIiwicGhvbmUiOm51bGwsImVtYWlsIjoiamlueWFvb0BxcS5jb20iLCJ1c2VybmFtZSI6bnVsbCwidW5pb25pZCI6bnVsbCwib3BlbmlkIjpudWxsLCJjbGllbnRJZCI6IjYwYzgxMTlkYTRmMGQ2ZjU5YzBiOTU2MCJ9LCJ1c2VycG9vbF9pZCI6IjYwYzgxMTlkYTRmMGQ2ZjU5YzBiOTU2MCIsImF1ZCI6IjYxOTYxYTdiOGI5MGFmMzdlN2M0MjJlMCIsImV4cCI6MTYzODk0NTAyMywiaWF0IjoxNjM3NzM1NDIzLCJpc3MiOiJodHRwczovL2FmZmluZS5hdXRoaW5nLmNuL29pZGMifQ.wfYszdakFTr4ag39xgEnbYzV2OnrkEymHBErxcMGtpg",
  "tokenExpiredAt": "2021-12-08T06:30:23.357Z",
  "_id": "619cb7c0032ec5e844cb3afe",
  "registerMethod": "basic:email",
  "registerInClient": "60c8119da4f0d6f59c0b9560",
  "decryptedToken": {
    "type": "user",
    "userPoolId": "60c8119da4f0d6f59c0b9560",
    "appId": "61961a7b8b90af37e7c422e0",
    "id": "619cb7c0032ec5e844cb3afe",
    "userId": "619cb7c0032ec5e844cb3afe",
    "_id": "619cb7c0032ec5e844cb3afe",
    "phone": null,
    "email": "jinyaoo@qq.com",
    "username": null,
    "unionid": null,
    "openid": null,
    "clientId": "60c8119da4f0d6f59c0b9560"
  }
}
```

- 图片base64编码示例

```
data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAOEAAADhCAMAAAAJbSJIAAAAhFBMVEX///+EMTGAJyeDLi6sfn5/JCR8GBiYV1fk1dW8l5d+ICDKsLB5DQ2CKyv9+vqcYGB6ExPYxMTw5+e3j4+OQ0N6EBB9HR2hamq/nZ3Su7umc3Pq39/cysp4BAS5kpJ7FxeIOTmRS0v38/PFpaWyiIjt5OSod3eINzeeZmaaXFyUUlKPSEjcOe1gAAAE6klEQVR4nO3dbVfaShSG4ZnEIAJRUAmgUKxw7LH9///v9GW51tHkCZM9k72Jfe7PBXIZCiHsIc6hbjfru146PMLH1Gz8Oq+KrJcm8/utNc+59a70/ZXv1ubAZY++X82NidtZz8CfxCtT4Y8+n6JvxC+GwHHfz9E/xDs74WGiIfT7o5nwIlMR+pEZUUvoRxefXegrI6Ke0FcPn11oRNQU2hBVhX6y+uxCC2JdmEfXSvzXXJjfR/fURiy0iTXhKP5T+bpoJb4m2OwO1YXj6Pu8ahVqEw2EvvieYMODsxDqEk2EPvt6nWDbw7IRahKNhD77oUW0Evrs/jnB5gdkJlQj2gl96VWIhkJfPmkQdYTgYLzMFYgqwvwVnLPUeKKqCCebKfjuoMxvEyBa0xFOHSSWfRO1hHZENaHbAGJe/BPPaElPiIlZr0RFISYmOK+A0xS6BfgqLy96JKoKMbHHvagrdNt58+FNXsU/LEhZiIn7vojaQrddAuK8J6K6UH0v6gvdGO3FWS/jUwZCN0Z7cd4H0ULoHkfgA+OuB6KJ0I0RcbmIfvSP2QjdY4X2YnKikRATl5vox3+fldA9ZoA4S0w0E7oNmjdLTLTbh/iU47LpDyLOSojeE//sxZREI+F43zrPkHIv2gi3s1bgzzeNQ/RWvGUi3J4e250nI1oI0Sf9dy1Tzb8bCBdhs/Op5t/1hZvQyfJERHUhOvfdREwy4q8t7AD0fp9ixF9ZeOi2+CEFUVeIgOUIDIEmGPFXFaIlVsXl9Qoch8cTNYUQ+GsIDBJjR/wVhV/mAHj5+1YPVT9EPSEEvg1jImLkQg014XF/AujcCyK+DEF4HDVv/eTmfzeExJhVDEqzGBcAWNy8uyX6Z1XEiL/OxNA38HZXm9xHxIhVDJZTX01LEyDxpuGBgrIUNu4Y9B+2kBINhWBxyd3pF91O2QnhC+SJI4OumQlb3gHSEq2Ere/iV4goWcVgJDxxmLIGxOx79/l3G+HJ47ADOBUgWMVgIgw4lj6gvdh5FYOFMOjz0HQHiPcdiQbCKuxj+xS89XddxVATVovb2I6tK2/L1XPQvTxfgbvpSKyvkq3msZ1YWlzG3k23VQzKK53TVH7rQByksNMqhmEKfRn+ijpQoZ8Ef6cxVKHfhT5PByusQr/qH6ywCH2aDlaYhZ5hHKywDD1vQ+HZRiGF5x+FLcL4H56tT+WVRWy1zZQLs5foHw9+/UgsH9ax1bZTLkxwnqb2K0qNU9Dd2n788tRUGDbn3a0FhTAKJVEoiUIchZIolEQhjkJJFEqiEEehJAolUYijUBKFkijEUSiJQkkU4iiURKEkCnEUSqJQEoU4CiVRKIlCHIWSKJREIY5CSRRKohBHoSQKJVGIo1AShZIoxFEoiUJJFOIolEShJApxFEqiUBKFOAolUSiJQhyFkiiURCGOQkkUSqIQR6EkCiVRiKNQEoWSKMRRKIlCSRTiKJREoSQKcRRKolAShTgKJVEoiUIchZLOXFiN3XVcjcLY+0wo9NUstvql8ybR91m7njWvjUDh+UchhecfhX+R8DhYYfO15+vVrgkzlLKwqwo7t91bb6qwahModL5+daZBVAVfanUKLvF95o0OoUDnHibWWytoEvpK+rvVfmhP1HzUCejcoaiyMh9KZVYV625A564Xx9XlUFodF/BF5j+Mt9zZWpXGVgAAAABJRU5ErkJggg==

```

- install app-ubuntu-calibre
 - sudo mkdir -p /opt/calibre && sudo rm -rf /opt/calibre/* && sudo tar xvf calibre-5.13.0-x86_64.txz -C /opt/calibre && sudo /opt/calibre/calibre_postinstall

- TO-DO: components、datable、chart

- 知乎禁止转载的回答测试
  - https://www.zhihu.com/question/25950466/answer/31731502
  - 只有复制内容较长时才会提示申请转载，比如复制超过150字

- webpack react fast refresh

```

"@pmmmwh/react-refresh-webpack-plugin": "^0.4.0-beta.7", 
"react-refresh": "^0.8.3", 

const ReactRefreshWebpackPlugin = require('@pmmmwh/react-refresh-webpack-plugin'); 

new ReactRefreshWebpackPlugin(), 

'react-refresh/babel', 
```

- webpack 5移除了node模块兼容

```

"crypto-browserify": "^3.12.0", 
"stream-browserify": "^3.0.0", 
"vm-browserify": "^1.1.2", 
```

- class extends

```js
class B {
  print = () => {
    console.log('print b');
  }
}

class D extends B {
  print() {
    console.log('before-super-print');
    super.print();
    console.log('after-super-print');
    console.log('print d');
  }
}

const d = new D();
d.print();
d.__proto__.print()
// print b
// before-super-print
```

- musicbrainz-rename

```

$if2(%albumartist%,%artist%)/
$if(%albumartist%,%album%/,)
$if($gt(%totaldiscs%,1),%discnumber%-,)$if($and(%albumartist%,%tracknumber%),$num(%tracknumber%,2) ,)$if(%_multiartist%,%artist% - ,)%title%
```

- maven-aliyun: https://maven.aliyun.com/repository/central 
- emotion的button

```

 const renderButton = (Root: React.ElementType<any> = 'button') => (
    <Root
      ref={forwardRef}
      type={Root === 'button' ? 'button' : undefined}
      {...(rest as HTMLElementProps<any>)}
      {...commonProps}
    >
      <span
        className={css`
          // Usually for this to take effect, you would need the element to be
          // "positioned". Due to an obscure part of CSS spec, flex children
          // respect z-index without the position property being set.
          //
          // https://www.w3.org/TR/css-flexbox-1/#painting
          z-index: 1;
        `}
      >
        {children}
      </span>
    </Root>
  );

  if (usesCustomElement(props)) {
    return renderButton(props.as);
  }

  if (usesLinkElement(props)) {
    return renderButton('a');
  }

  return renderButton();
```
