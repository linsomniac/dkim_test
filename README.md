# dkim_test - Display diagnostic information about a DKIM message

This is a python program that can take a DKIM message and verify it.  While
verifying, it will display diagnostic information.  In particular, if the
DKIM signature includes the "z" information, it will display any headers
that do not match the signature.

## Using

You will need the "[dkimpy](https://pypi.org/project/dkimpy/)" library: `pip install dkimpy`
(NOTE: This is different from the similarly named "pydkim")

Then just run `python3 dkim_test <EMAIL_FILE>`

You can optionally include a DKIM DNS record, otherwise it will be looked up in DNS:
`python3 dkim_test --dns-record 'v=DKIM1; <REST OF RECORD>' <EMAIL_FILE>`

The DNS record can be looked up using: `host -t txt <SELECTOR>._domainkey.<DOMAIN>` but you must remove any
double-quote/space/double-quote separators within it.

## Example

```shell
[N] sean@seans-laptop ~/p/dkim_test (master)> ./dkim_test --dns-record 'v=DKIM1; k=rsa; p=MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA359FxfMhz6Sw0vszgKMFfk+b6xQ7Z60QRCJRLKGNvok49okHeneQUep30RhcKhBrdo5ICzBIQP3Q7a+FKDPuWQ/erCMCqTSLD/pF/eZVTFqSoF46+IXC4k55POeZlC0PwWbJfjeDrZobuqNBTsUlfk0+hJ8GIkAg0MRbVmwequgrWAFoSlDLtV2WP4vzu+V0ZnV8e4ohZGiYv9kHfWeH7KBKp9U2NLckb6iJzvz4v7D/NjcHUJrPNt8WvlUm41lEi9Y92m52kFkuTlWOySvbL/tQHD+e1YusjkcYL9TqzGZjaioPf6bqyfbP0UFOycdoiRvJBikhAR8m8PWOpmhhmwIDAQAB' test
msg
2024-01-18 02:46:15,234 - debug - DEBUG - sig: {b'v': b'1', b'a': b'rsa-sha256', b'c': b'relaxed/simple', b'd': b'stg.example.com', b's': b'2018', b't': b'1705514370', b'bh': b'IV1s4b3EH75xXFDsvkD/BI5CVv9r6J01axQeUQQBjOw=', b'h': b'From:List-Unsubscribe:List-Unsubscribe-Post:Feedback-ID:From', b'z': b'From:=20"user@example.com=20via=20SMTP=20PRO"=20<rootatweb1.stg.ex\r\n\t ample.com=3Dexample.com=3Dxt2v8k@stg.example.com>|List-Unsubscribe:=2\r\n\t 0Test=201|List-Unsubscribe-Post:=20Test=202|Feedback-ID:=20Test=20\r\n\t 3', b'b': b'uauvSkatJmthXvzQCF1pA3D66+X+A5ydRxgGqlclvbOMM0CUFBBFcOOq2EywNx4iP\r\n\t iG77b+F3RYVHMGMnBIE7CRRJvEpinxbqkP+KSL8LY7FGi9xyudVjMq2oBTcJFMI/lo\r\n\t VNlXLcRyi6ryCCSLcwky2UyJMNfOomOe8RcyBZaeX8ZLkRkjCco+evAmMzug7SAVnd\r\n\t iwMSgsKGkY97m5Q1cmmDiJWrU7vrTnkGy09FG6k9k/9nWpRcBFIGjJxDGIPfHFgASa\r\n\t kb05HVIdY0rK36cLMEtQ1H2GIxG7fU6Xa/uCCwRZWnaEKGSShxPos82L/Tia8JZ8gw\r\n\t LhX2eD8bnJgtg=='}
2024-01-18 02:46:15,235 - debug - DEBUG - bh: b'IV1s4b3EH75xXFDsvkD/BI5CVv9r6J01axQeUQQBjOw='
2024-01-18 02:46:15,235 - debug - DEBUG - b'DKIM-Signature' valid: False

Verification results: False
DKIM signature header mismatch: From
  Message: "user@example.com via SMTP PRO" <rootatweb1.stg.example.com=example.com=xt2v8kATstg.example.com@example.com>
     DKIM: "user@example.com via SMTP PRO" <rootatweb1.stg.example.com=example.com=xt2v8k@stg.example.com>
```
