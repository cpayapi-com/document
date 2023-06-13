# Signature

[Home](https://github.com/cpayapi-com/document/blob/main/README.md) /
[API Overview](https://github.com/cpayapi-com/document/blob/main/api-reference/overview.md) /
_Signature_

## Table of Contents

- [Introduction](#introduction)
- [Code Examples](#code-examples)
   - [PHP](#php)
   - [Golang](#golang)
   - [Java](#java)


## Introduction
The signature is hashed with `SecurityKey` using `SHA256` algorithm.

Examples:
```shell
curl https://domain/path/getSth?xx=1001&yy=&aa=hello&sign=signstring -H "Content-Type:application/x-www-form-urlencoded"

curl -X POST 'https://domain/path/updateSth' -d '{"xx":1001,"yy":"","aa":"hello","sign":"signstring"}' -H "Content-Type:application/json"
```

1. All parameters will be sorted by parameter name and stitched into a string, e.g. `aa=hello&xx=1001`.
   > Parameter `yy` is ignored here due to its empty value.

2. Append `SecurityKey` to the end of string `aa=hello&xx=1001`, and you will get a new string, e.g. `aa=hello&xx=1001&key=abc123`

3. Encrypt the string generated in previous step by `SHA256` algorithm.

4. Convert the ciphertext into lower case.

## Code Examples

### PHP
> Note: Please don't use function `http_build_query` to build the parameters.  

```php

function genSignature($params, $securityKey) {
  if (!is_array($params) || count($params) == 0) {
    return '';
  }

  ksort($params);
  $qs = '';
  foreach ($params as $k => $v) {
    if (!empty($v)) {
      $qs = $qs . "{$k}={$v}&";
    }
  }
  // e.g. $qs='aa=hello&xx=1001&key=abc123'
  $qs = $qs.'key='.$securityKey;
  return strtolower(hash_hmac("sha256", $qs, $securityKey));
}

// using
$params = [
  'aa' => 'hello',
  'xx' => 1001,
  'yy' => ""
];
$sign = genSignature($params, 'abc123');

// 1c4492e23f7812c5781a30046c5d760ba3ae344de99a5700542715866f448825
echo $sign;

```

### Golang
```go

package main

import (
	"crypto/hmac"
	"crypto/sha256"
	"encoding/hex"
	"fmt"
	"sort"
	"strings"

	"github.com/shopspring/decimal"
)

func GenSignature(p map[string]interface{}, securityKey string) string {
	delete(p, "sign")

	counter := len(p)
	ks := make([]string, 0, counter)
	for k := range p {
		ks = append(ks, k)
	}
	sort.Strings(ks)

	var val interface{}
	qs, tmp := "", ""
	for i := 0; i < counter; i++ {
        val = p[ks[i]]
        tmp = fmt.Sprintf("%v", val)

		switch val.(type) {
		case int64, int, float64:
			ss, _ := decimal.NewFromString(tmp)
			tmp = ss.String()
		}
		if len(tmp) > 0 {
			qs += ks[i] + "=" + tmp + "&"
		}
	}

    // e.g. $qs='aa=hello&xx=1001&key=abc123'
	qs = qs + fmt.Sprintf("key=%s", securityKey)
	h := hmac.New(sha256.New, []byte(securityKey))
	h.Write([]byte(qs))
	return strings.ToLower(hex.EncodeToString(h.Sum(nil)))
}

// using
params := make(map[string]interface{})
params["aa"] = "hello"
params["xx"] = 1001
params["yy"] = ""

// 1c4492e23f7812c5781a30046c5d760ba3ae344de99a5700542715866f448825
sign := GenSignature(params, "abc123")
fmt.Println(sign)

```

### Java
```java
package com.xxx.demo;

import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;
import java.util.*;

public class Demo {
    public static void main(String[] args) {
        Map<String, Object> params = new HashMap<>();
        params.put("aa", "hello");
        params.put("xx", 1001);
        params.put("yy", "");
        try {
            String sign = genSignature(params, "abc123");

            // 1c4492e23f7812c5781a30046c5d760ba3ae344de99a5700542715866f448825
            System.out.println(sign);
        } catch (Exception e) {
            throw new RuntimeException(e);
        }
    }

    public static String genSignature(Map<String, Object> params, String securityKey) throws Exception {
        if (params.isEmpty()) {
            throw new Exception("invalid params");
        }
        Collection<String> keySet = params.keySet();
        List<String> list = Lists.newArrayList(keySet);
        Collections.sort(list);
        StringBuilder sb = new StringBuilder();
        for (String s : list) {
            sb.append(s).append("=").append(params.get(s)).append("&");
        }
        sb.append("key=").append(securityKey);
        // sb.toString() = $qs='aa=hello&xx=1001&key=abc123'

        Mac sha256HMAC = Mac.getInstance("HmacSHA256");
        SecretKeySpec secretKey = new SecretKeySpec(securityKey.getBytes("UTF-8"), "HmacSHA256");
        sha256HMAC.init(secretKey);
        byte[] array = sha256HMAC.doFinal(sb.toString().getBytes("UTF-8"));

        StringBuilder res = new StringBuilder();
        for (byte item : array) {
            res.append(Integer.toHexString((item & 0xFF) | 0x100).substring(1, 3));
        }
        return res.toString().toLowerCase();
    }
}
```