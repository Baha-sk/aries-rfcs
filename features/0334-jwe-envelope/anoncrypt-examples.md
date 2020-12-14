## Anoncrypt Concrete examples

The following examples are for JWE **anoncrypt** packer for encrypting the payload `secret message`:

The packer generates the following protected headers for all these examples:
- Generated protected headers: `{"enc":"A256GCM","typ":"didcomm-envelope-enc"}`
    - raw (no padding) base64URL encoded: `eyJlbmMiOiJBMjU2R0NNIiwidHlwIjoiZGlkY29tbS1lbnZlbG9wZS1lbmMifQ`

Note: all `x` and `y` key coordinates values below are raw (no padding) base64URL encoded.

### 1 - JWE with 2 recipients having NIST P-256 keys:
- Recipient 1 public key JWK format:
```json
{
  "kty": "EC",
  "crv": "P-256",
  "x": "g8jkH7GqIx_qSJJC0gXu6Z6FcDgcxZZATuY2cnYVb5I",
  "y": "CxjNJPO4hyyKqeb0sGo-5mLCilBDf53G1iFXUh4oGOE"
}
```
- Recipient 1 kid (jwk thumbprint raw base64 URL encoded): `PYyLauhK6A3xNuxcsfZMzPnNE8SbUasaAAAoNegEL1o`
- Recipient 2 public key JWK format:
```json
{
  "kty": "EC",
  "crv": "P-256",
  "x": "T0RJ0teUslPPYhrgu4qFx62YmXKun1Ssd5TE5mkDtKE",
  "y": "SlZG9ztYbP6CzsWuyw6AWQKSYjfSDRn4yGY4eDqTGgA"
}
```
- Recipient 2 kid (jwk thumbprint raw base64 URL encoded): `N-KK-4KxJ6U0e6snfuMYI6KoWgc0wSPaEsyaMKnPSRQ`
- Finally, packing the payload outputs the following JWE (pretty printed for readability):
```json
{
  "protected": "eyJlbmMiOiJBMjU2R0NNIiwidHlwIjoiZGlkY29tbS1lbnZlbG9wZS1lbmMifQ",
  "recipients": [{
    "header": {
      "alg": "ECDH-ES+A256KW",
      "kid": "PYyLauhK6A3xNuxcsfZMzPnNE8SbUasaAAAoNegEL1o",
      "epk": {
        "use": "enc",
        "kty": "EC",
        "crv": "P-256",
        "x": "wc7bscjeSSyvu-xLN_eYSt6T1eWSV5scB_oUrpaexz0",
        "y": "Q9eJcEtbRv4o_mmlBbcqlJ_vS1HFNyyE0d20h_JB8vQ"
      }
    },
    "encrypted_key": "LlrTOfSf3dXeo7gmLLSbAFTJTzXzrcQwJuJE7q73spJdbC-rnHKlLg"
  }, {
    "header": {
      "alg": "ECDH-ES+A256KW",
      "kid": "N-KK-4KxJ6U0e6snfuMYI6KoWgc0wSPaEsyaMKnPSRQ",
      "epk": {
        "use": "enc",
        "kty": "EC",
        "crv": "P-256",
        "x": "ciiz13A7zt5Ncu7Ouyi1wV29jpU9gQ3UHj0oLGRt_4k",
        "y": "Ls7zcgkUajNnPp4blZL16OrboTntpHZp74NUScH_Ejw"
      }
    },
    "encrypted_key": "QQoN74Pi06nyX3FR8-raNyQXku0Qx0klg2qo4hzQtN7nY9hKjJxZbg"
  }],
  "iv": "vm8x5OwCAzERi_Kg",
  "ciphertext": "PsSGaLdwxTtGTxkIcy8",
  "tag": "ivMv5MTG58KOp83rWfpOlw"
}
```

### 2 - JWE with 1 recipient having a NIST P-256 key:
Packing a message with 1 recipient will use the JWE [compact format](https://tools.ietf.org/html/rfc7516#section-3.1).

Here is an example:
- Single Recipient public key JWK format:
```json
{
  "kty": "EC",
  "crv": "P-256",
  "x": "H00KC1dV9p5lQXeTMjCqbOnST8OQWh8hlUfMtURQMPw",
  "y": "BGlEXaa1IjrtDNOEPXb0GkCvUiWQ-RRIM0S2oHLXM0o"
}
```
- Single Recipient kid (jwk thumbprint raw base64 URL encoded): `w6zwG9Bgiyf6xJ02GUr2I3vFrPg_xYKgNxbZvC6-Zk8`
- Finally, packing the payload outputs the following compact serialized JWE:
`eyJhbGciOiJFQ0RILUVTK0EyNTZLVyIsImVuYyI6IkEyNTZHQ00iLCJlcGsiOnsidXNlIjoiZW5jIiwia3R5IjoiRUMiLCJraWQiOiJ3Nnp3RzlCZ2l5ZjZ4SjAyR1VyMkkzdkZyUGdfeFlLZ054Ylp2QzYtWms4IiwiY3J2IjoiUC0yNTYiLCJ4IjoiY1Y4WnFNc1NpT3UtSWFXSnh0V0xteHo4WU40dlBUbkdGQmZpSTNSbWxEVSIsInkiOiJTRzRMY0k2U1paNTVsdlBobTZBdUQ4cHFncDNDN1Y4Ti1WWGNsZ2pqd2hZIn0sImtpZCI6Inc2endHOUJnaXlmNnhKMDJHVXIySTN2RnJQZ194WUtnTnhiWnZDNi1aazgiLCJ0eXAiOiJkaWRjb21tLWVudmVsb3BlLWVuYyJ9.x-BaN8OiY6H8W2bMToQc8OUTH7qzdE84phYXN93bSbJHL5v3MBS0xQ.JjBHvW-9ul6u-uNr.ZMLkjGIOpDp_0JIbJ2Q.g7K6k-RhFE2yRlV6zyxxpA`

### 3 - JWE with 2 Recipients having NIST P-384 keys:
- Recipient 1 public key JWK format:
```json
{
  "kty":"EC",
  "crv":"P-384",
  "x":"qgYZf14NlTq92WAOH0eNoza1JFzQ9spm8T3uNl4y-mjDYdiA6vysbgpH9LGe6Sk9",
  "y":"Dg2ATTugFNusb6pohwQUSuZ1wXQRSbOiT_HQ2DU12ESwU3rkzQbeBfA_9MaxQRuo"
}
```
- Recipient 1 kid (jwk thumbprint raw base64 URL encoded): `WZLOVzULgXvVEReK9w9Y8Ss6yMauamPGi5HXsSniBow`
- Recipient 2 public key JWK format:
```json
{
  "kty":"EC",
  "crv":"P-384",
  "x":"W02dO1gtu9FVh2rJBmg3n_AWINtlNittgEm-_lfNejkeqgVpS-6GPcPiRkF1rFzv",
  "y":"84JN8jMbVcd66rhLSlvQgq_G7oqr1TgXRwPFZPxxk-tJ7FFHvLpklITLEuropX5n"
}
```
- Recipient 2 kid (jwk thumbprint raw base64 URL encoded): `SXnsEo6KQmCoQzlaa2qmv1tl0gSliUhto_EurlSkdAY`
- JWE:
```json
{
  "protected": "eyJlbmMiOiJBMjU2R0NNIiwidHlwIjoiZGlkY29tbS1lbnZlbG9wZS1lbmMifQ",
  "recipients": [{
    "header": {
      "alg": "ECDH-ES+A256KW",
      "kid": "WZLOVzULgXvVEReK9w9Y8Ss6yMauamPGi5HXsSniBow",
      "epk": {
        "use": "enc",
        "kty": "EC",
        "crv": "P-384",
        "x": "DfD-2u3DN6b-3M1mqPaNuDCknQWqSOCxnOT8wehEW0ZoDMpTbi7aYaQmDYNWBmqr",
        "y": "7eudwX9fY74d9e49YJFkFORRm8zylNHJ6lIFmP3Q__2zeBtKrPxXf26oTcOWRB0x"
      }
    },
    "encrypted_key": "P7yDEUXQ_MHTC0GqnZYyzgOHfyGJXXuT_GHgNxUFChfsa6Od6sRzFg"
  }, {
    "header": {
      "alg": "ECDH-ES+A256KW",
      "kid": "SXnsEo6KQmCoQzlaa2qmv1tl0gSliUhto_EurlSkdAY",
      "epk": {
        "use": "enc",
        "kty": "EC",
        "crv": "P-384",
        "x": "LE6hGwWAiBmToHr74NC8_LwsSUJRj1zWEemy3LicE6Lqu8dPMI35BPBAWnaNVnV_",
        "y": "HfWLkNQVWpztRjbq5pBLxYpAhKepeGjAd3B6qowrx8n_RH7_mihgcA_hTqw6TGW4"
      }
    },
    "encrypted_key": "pnXsXSYCsm7ColcG-FwTOIVxXQ3icCZmlE9KIw5u02OERTFMwzBKvg"
  }],
  "iv": "DSIAcIGo0z1ESGB3",
  "ciphertext": "KcNGfYK9bCqmg7uOeXw",
  "tag": "TdXwTz-FRxPhz7ZdVqoonQ"
}
```

### 4 - JWE with 1 recipient having a NIST P-384 key:

- Single Recipient public key JWK format:
```json
{
  "kty":"EC",
  "crv":"P-384",
  "x":"CQzaxoZT1Pka_DEJ-n1xOn7kbRjIWF1CaA4sTXJAXFoNstbPaxJyhZmjUlQHA32Q",
  "y":"MOEF5_yGK4rPRQ0QAIjAfIuLDx9oxexOIwGAEAO88LVJC5cjjzEdnD2zBBT-lQRJ"
}
```
- Single Recipient kid (jwk thumbprint raw base64 URL encoded): `bKGLDtcJDy9aqAYhvp1U3X4VP5rTopMwAcSn_4OyXNM`
- Finally, packing the payload outputs the following compact serialized JWE:
  `eyJhbGciOiJFQ0RILUVTK0EyNTZLVyIsImVuYyI6IkEyNTZHQ00iLCJlcGsiOnsidXNlIjoiZW5jIiwia3R5IjoiRUMiLCJraWQiOiJiS0dMRHRjSkR5OWFxQVlodnAxVTNYNFZQNXJUb3BNd0FjU25fNE95WE5NIiwiY3J2IjoiUC0zODQiLCJ4IjoibU1OWkVzRWtLT3ZZeGJnRmlKazA4OWM4NXNmT3l3aXQzd1BCRHc5SW0zTE9mcTEyckJvbDNKYnhWSmtYbVNlbyIsInkiOiJhLUZGUno0UzJ5MjhWcjBTS09CeHNWR3c0NTNkdlRtNkhVRTFMYzNwWnRrbWpRSVFiNUdWTzBfa3lETzRPSmtxIn0sImtpZCI6ImJLR0xEdGNKRHk5YXFBWWh2cDFVM1g0VlA1clRvcE13QWNTbl80T3lYTk0iLCJ0eXAiOiJkaWRjb21tLWVudmVsb3BlLWVuYyJ9.WuPDHfRUjY-CvFEHMaQucg7GmAoKYZsswlEjGTM-I7MkMowTXka-VQ.OwgKXwoYa0HCHT0O.VnTDEjX1lmjz_MCQdfg.K78jadld3xFMDTy3eF6Yng`
  
### 5 - JWE with 2 Recipients having NIST P-521 keys:
- Recipient 1 public key JWK format:
```json
{
  "kty":"EC",
  "crv":"P-521",
  "x":"AQxOg2fnpc78V86DegNqjRYy5_J7y78fjFLrR2ezct1xpCd51G_T5b3u_MB52PHOUlO0h-kQPW8OLa3Tj3l4Ewd4",
  "y":"AaEAnb7o-tEB-irYmo_v_tW3l6QNWaoMBQxewdJu-hcFrjc7TOH8hucroO7nMa4LNPVLAnvQQ1P4MjUuhuOpsFRy"
}
```
- Recipient 1 kid (jwk thumbprint raw base64 URL encoded): `011nfEQ1bPF1q2QJfC1u1c29tZqQNwpAdN8X9P9TQoQ`
- Recipient 2 public key JWK format:
```json
{
  "kty":"EC",
  "crv":"P-521",
  "x":"ANOlbmvmvhY8zCU7f3JhVg0EfHqeuPzAx2ckLa7v9IBghjUfY313FnIsNLhmtEuOGf7trp8A65yPZRa1Nr9OGUy6",
  "y":"AWnnWrZpGZNBf6CrXQRyWt1X2Eq4HTj2XYzPQvNXx0e7QPBmllqmek-14yX1rxX5IBBCgXA0KbCuWrpII2kRx36b"
}
```
- Recipient 2 kid (jwk thumbprint raw base64 URL encoded): `mpxcN_DhBddtizpYWtW5APpUVzTvwEd6Lq6jxb4wrIM`
- JWE:
```json
{
  "protected": "eyJlbmMiOiJBMjU2R0NNIiwidHlwIjoiZGlkY29tbS1lbnZlbG9wZS1lbmMifQ",
  "recipients": [{
    "header": {
      "alg": "ECDH-ES+A256KW",
      "kid": "011nfEQ1bPF1q2QJfC1u1c29tZqQNwpAdN8X9P9TQoQ",
      "epk": {
        "use": "enc",
        "kty": "EC",
        "crv": "P-521",
        "x": "AJqT5gRxlGMs0Cu7OfOz24JsxgR6lQF_3GrJlhS4o76C-FxQlRECXevcjEi0sjaZcfEWLFnmIACZcYTHuUs-ddaP",
        "y": "ADpMwsNamiy2kPVG4ZGth3Wl6B-FJa1Fks0XdHiUopCA9PMV1Ma1TTaC0ft8WVo7WQMhJzviLJYst9f5Es5DvWOL"
      }
    },
    "encrypted_key": "p09v35JcmMXFsD0kXNo25VbxqH8lyiThdYAnr2Z_LrSTcaz33FdUbw"
  }, {
    "header": {
      "alg": "ECDH-ES+A256KW",
      "kid": "mpxcN_DhBddtizpYWtW5APpUVzTvwEd6Lq6jxb4wrIM",
      "epk": {
        "use": "enc",
        "kty": "EC",
        "crv": "P-521",
        "x": "AZa1LgnVXAKa0lMEIHjixUVC6Eb4S8F8SpZPJix0E7a9hfxtRIRncEjUUNWc6VnIgN_IKZXIorlgJyiozV_lj9uD",
        "y": "ASRf3gBFOwmbidpCNrTRjH_qHuiXTBLIQcv7VliMgHBRFtvZcCrDl6BI-9vvGmMMnOpZvoWILtr8NT5W2rGUq4AO"
      }
    },
    "encrypted_key": "MzIg46-CSI9rAstRA9nG59sMgGASrtejaAtVCKP3bum8FVpz2xOMZw"
  }],
  "iv": "Buq-pFGe0weio2Xd",
  "ciphertext": "vJj3NfGAnQB6bkItJl8",
  "tag": "6RY7H5DOrv4_vLrNtwDfjg"
}
```

### 6 - JWE with 1 recipient having a NIST P-521 key:

- Single Recipient public key JWK format:
```json
{
  "kty": "EC",
  "crv": "P-521",
  "x": "ARZd4gbmXw7FKesn7a4o0uCgd1X8DgZ3WY_ODhnTnmVe5dKkQlJkC835KqK9piZMKr7Yu64mCWLhqAolThUX6wqi",
  "y": "AdxVzmYPdNQ9ZAEAEioj5SVsSYhhcTOP8tAqkhiQ1ggcXCgMhG3cHn_-_3p0QIY5MDQ-2PI2_0QTnPZ1ocVNJ9qv"
}
```
- Single Recipient kid (jwk thumbprint raw base64 URL encoded): `iq7Av7QtTRq3UQIFZ7xPrNbA20dPwIKcm6Tp_uaYi8A`
- Finally, packing the payload outputs the following compact serialized JWE:
  `eyJhbGciOiJFQ0RILUVTK0EyNTZLVyIsImVuYyI6IkEyNTZHQ00iLCJlcGsiOnsidXNlIjoiZW5jIiwia3R5IjoiRUMiLCJraWQiOiJpcTdBdjdRdFRScTNVUUlGWjd4UHJOYkEyMGRQd0lLY202VHBfdWFZaThBIiwiY3J2IjoiUC01MjEiLCJ4IjoiQWRJU2JjbTBLckZaeG1XUnhzR3U5NHF3eHVFV2pucTJiWDV6aEhESVFrM1IzcjZYMFJCNGxXdUVuQ054Vkc2YUVxVU1ZYmUwdU5xQVNsUEU4bE1HdFh1QyIsInkiOiJBSmJ0QzZScFhIeFVpLWxTcFR1TVBtUFpFTmoyQnVsYnJUOHhwRXJwMkV2Mkd4QXlBbW95RFV3OElMZmIydk8tQVVUXzZtZG9DTzVQZWotZFg5SVFPN0JuIn0sImtpZCI6ImlxN0F2N1F0VFJxM1VRSUZaN3hQck5iQTIwZFB3SUtjbTZUcF91YVlpOEEiLCJ0eXAiOiJkaWRjb21tLWVudmVsb3BlLWVuYyJ9.ZgXnvw46dMBUiWxZH3jQPANDegmF5BWFJl8cDPMJ7CHM9ADAC1hMEQ.zIe9L_VUh2EPX_Et.oKsbTQwaqpiSzgldLUw.r2LfmC7grOyDUmKIOY1dNA`
