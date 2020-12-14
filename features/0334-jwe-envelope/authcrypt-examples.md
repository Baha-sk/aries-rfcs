## Authcrypt Concrete examples

The following examples are for JWE **authcrypt** packer for encrypting the payload `secret message`:

Since **autchrypt** requires the sender public key, it must be previously sent, out of band, to the recipient(s). For security reasons, the JWE envelope only includes the sender kid as `skid` in the protected headers. The recipient must be able to load the corresponding sender public key during unpack(JWE).

Note: all `x` and `y` key coordinates values below are raw (no padding) base64URL encoded.

### 1 - JWE with 2 recipients having NIST P-256 keys:
The packer generates the following protected headers that includes the skid:
- Generated protected headers: `{"enc":"A256GCM","skid":"BPBJOhGBKJejqJWfCVt2fRJzbyZZN5DZ8BhhJSIpPbo","typ":"didcomm-envelope-enc"}`
  - raw (no padding) base64URL encoded: `eyJlbmMiOiJBMjU2R0NNIiwic2tpZCI6IkJQQkpPaEdCS0planFKV2ZDVnQyZlJKemJ5WlpONURaOEJoaEpTSXBQYm8iLCJ0eXAiOiJkaWRjb21tLWVudmVsb3BlLWVuYyJ9`
- Sender key JWK format:
```json
{
  "kty":"EC",
  "crv":"P-256",
  "x":"fhInN8Dbze6qmXBhmbz2dXkUU4t2fHAyjBmnUf_YF_I",
  "y":"xP6rcPkZ6AfvcTlAw8_JbYWGJjh-l8BzpgOnY7NcBF0"
}
```
- Sender kid (jwk thumbprint raw base64 URL encoded): `BPBJOhGBKJejqJWfCVt2fRJzbyZZN5DZ8BhhJSIpPbo`
- Recipient 1 public key JWK format:
```json
{
  "kty":"EC",
  "crv":"P-256",
  "x":"8R4aDNKMsPMBYr2_2e71HWKhJIye9FwmzWNuoom3yZs",
  "y":"USILgZ8ACxqRy4FJR7CuyC6XojMuCFwcDaRVDJ2SfWY"
}
```
- Recipient 1 kid (jwk thumbprint raw base64 URL encoded): `MuPvLd3rbmiDH0e-RWS5D4s-VwvUkL6WeylDyGdJK6M`
- Recipient 2 public key JWK format:
```json
{
  "kty":"EC",
  "crv":"P-256",
  "x":"AMAO-xi5NgYsQlYMoNEUqPqlV6ITAMuST0fMm_PkBlQ",
  "y":"lS5-EhMkewOYQGc2kJ3G-E8SMAu1grGF12Ei0gRyljs"
}
```
- Recipient 2 kid (jwk thumbprint raw base64 URL encoded): `9sFzSdDl6pBJxsS7TmaxA1jW7TRj6I7T6gtNrGc4-bI`
- Finally, packing the payload outputs the following JWE (pretty printed for readability):
```json
{
  "protected": "eyJlbmMiOiJBMjU2R0NNIiwic2tpZCI6IkJQQkpPaEdCS0planFKV2ZDVnQyZlJKemJ5WlpONURaOEJoaEpTSXBQYm8iLCJ0eXAiOiJkaWRjb21tLWVudmVsb3BlLWVuYyJ9",
  "recipients": [{
    "header": {
      "alg": "ECDH-1PU+A256KW",
      "kid": "MuPvLd3rbmiDH0e-RWS5D4s-VwvUkL6WeylDyGdJK6M",
      "epk": {
        "use": "enc",
        "kty": "EC",
        "kid": "MuPvLd3rbmiDH0e-RWS5D4s-VwvUkL6WeylDyGdJK6M",
        "crv": "P-256",
        "x": "kdGS4kkDF2JBwDTKTaWlAnwYVnCAV2CJkFXX1IL6uIU",
        "y": "z3FzLFImNMDrbYWMLd1D0FQHgtsGUT7d9yVvS3OPY18"
      }
    },
    "encrypted_key": "L0FMaFCuvN3T0olU8CZR3Xm7li-8CxZnv3mAnBHwgdKgmyANLprOag"
  }, {
    "header": {
      "alg": "ECDH-1PU+A256KW",
      "kid": "9sFzSdDl6pBJxsS7TmaxA1jW7TRj6I7T6gtNrGc4-bI",
      "epk": {
        "use": "enc",
        "kty": "EC",
        "kid": "9sFzSdDl6pBJxsS7TmaxA1jW7TRj6I7T6gtNrGc4-bI",
        "crv": "P-256",
        "x": "BOZ9PKEoV0dPzJobJzZCo7vZP7oc_-uSe2U8Dcgv4QQ",
        "y": "0eaBpift45lpXTQEA30ZaeiJ9rhEJB11S1ombfVxDDM"
      }
    },
    "encrypted_key": "Wsa-6pn14zEdvnCXFsq3YzHgG-EU2LcYLa3R3Q4MRywv9RD19bhEdg"
  }],
  "iv": "t-f4d_4WyaciaPc4",
  "ciphertext": "D9QpEOoE1HkaN4CewGo",
  "tag": "008ZEqBNsiXWMPDMpDAqIg"
}
```

### 2 - JWE with 1 recipient having a NIST P-256 key:

Packing a message with 1 recipient will use the JWE [compact format](https://tools.ietf.org/html/rfc7516#section-3.1).

Here is an example:
- Generated protected headers: `{"enc":"A256GCM","skid":"nN9Qx8hu_chs5Jd7xl5SOS0-ZWWyPUq1L3RbJoiVsFk","typ":"didcomm-envelope-enc"}`
  - raw (no padding) base64URL encoded: `eyJlbmMiOiJBMjU2R0NNIiwic2tpZCI6Im5OOVF4OGh1X2NoczVKZDd4bDVTT1MwLVpXV3lQVXExTDNSYkpvaVZzRmsiLCJ0eXAiOiJkaWRjb21tLWVudmVsb3BlLWVuYyJ9`
- Sender key JWK format:
```json
{
  "kty":"EC",
  "crv":"P-256",
  "x":"qlkcsI6kS1UUU1Q7LG00oYBteAqZ2y2TDT44q6_m3NA",
  "y":"Zwj18tE-L5RWSuHSHXjU-jSfs6pA6ElfW0KJFBKfK5E"
}
```
- Sender kid (jwk thumbprint raw base64 URL encoded): `nN9Qx8hu_chs5Jd7xl5SOS0-ZWWyPUq1L3RbJoiVsFk`
- Single Recipient public key JWK format:
```json
{
  "kty":"EC",
  "crv":"P-256",
  "x":"ucAQeBL0aHCvxLl9KBsOfrCbINidvruL_qNBzi_4zWc",
  "y":"-NJXxjuoZTfht2MzvG1F0cA0s1bqq2LdtHN2jQwZmdI"
}
```
- Single Recipient kid (jwk thumbprint raw base64 URL encoded): `Vjum_rhFNTYEG3CobfvdFPiqz-GJQKvmWLl32P_LO9w`
- Finally, packing the payload outputs the following compact serialized JWE:
`eyJhbGciOiJFQ0RILTFQVStBMjU2S1ciLCJlbmMiOiJBMjU2R0NNIiwiZXBrIjp7InVzZSI6ImVuYyIsImt0eSI6IkVDIiwia2lkIjoiVmp1bV9yaEZOVFlFRzNDb2JmdmRGUGlxei1HSlFLdm1XTGwzMlBfTE85dyIsImNydiI6IlAtMjU2IiwieCI6ImRZSTFQcndpWFc1Tm53eTFQOXpWaG9XVEI4WW1WTUNVbHZFMkRJNWNKSjAiLCJ5IjoiZ0lPWWtwUUhoN0d4VGUtNTNFNkZDUmNod3NlcVdZSmJEdnBWNmZWYWdyTSJ9LCJraWQiOiJWanVtX3JoRk5UWUVHM0NvYmZ2ZEZQaXF6LUdKUUt2bVdMbDMyUF9MTzl3Iiwic2tpZCI6Im5OOVF4OGh1X2NoczVKZDd4bDVTT1MwLVpXV3lQVXExTDNSYkpvaVZzRmsiLCJ0eXAiOiJkaWRjb21tLWVudmVsb3BlLWVuYyJ9.3Xh8uGMOfk5kDBGpiwerMoqw6NYrSkBiVsLIOl6xgvLMidQBDvkv0A.CQTM_AJ01TvrN1g-.UEd0MxyWAV9TSK2gPg0.PDpA4EVlE_ywGGRl4kjjGQ`

### 3 - JWE with 2 Recipients having NIST P-384 keys:
- Generated protected headers: `{"enc":"A256GCM","skid":"2prcNxBFfPg6c9Q2qNlO7EtLkY4bY5TZw5OGH7SE9nQ","typ":"didcomm-envelope-enc"}`
  - raw (no padding) base64URL encoded: `eyJlbmMiOiJBMjU2R0NNIiwic2tpZCI6IjJwcmNOeEJGZlBnNmM5UTJxTmxPN0V0TGtZNGJZNVRadzVPR0g3U0U5blEiLCJ0eXAiOiJkaWRjb21tLWVudmVsb3BlLWVuYyJ9`
- Sender key JWK format:
```json
{
  "kty":"EC",
  "crv":"P-384",
  "x":"cFS2uXIRTb8Dwntgsic7WNmKtI2AiUm4HAU3L5YZ7VnC-tgZ2pt7e_Rc1-_o6aNh",
  "y":"_U3rJXixkbnu5-JDT9svpU8lvl87g5njcilCiDS0smGIAVDRN2720Rat_o_VQRVk"
}
```
- Sender kid (jwk thumbprint raw base64 URL encoded): `2prcNxBFfPg6c9Q2qNlO7EtLkY4bY5TZw5OGH7SE9nQ`
- Recipient 1 public key JWK format:
```json
{
  "kty":"EC",
  "crv":"P-384",
  "x":"VR8xBHX_is9fgnBOiSSv3Fi9BDaioAuTFJzJpuDeGE7trbWedJbaP8dcfweJuEXA",
  "y":"pXr7UvATJ-J4tWCPspselqlzTIADWNpaMNAprXfzsTVzEb51SKsw2OyqaHW5otMm"
}
```
- Recipient 1 kid (jwk thumbprint raw base64 URL encoded): `l43L62a4OFJ8M2rlbufPpkhxeaeUl4KobCLp-Ydh4Iw`
- Recipient 2 public key JWK format:
```json
{
  "kty":"EC",
  "crv":"P-384",
  "x":"rHipfs0JOQGVSy_3RmKB9WwkTOGsmTaPw7VK-bIRGXSasom0wCLdb19NvT2MaNiw",
  "y":"W2GSX8zc06uSh8JRlIIQcl5igCA0CWHoLmE4lNCqpcTiesgas4fbiQY4tMEbtDAO"
}
```
- Recipient 2 kid (jwk thumbprint raw base64 URL encoded): `fzddOmU0rn6u_hOfw3mPiPbJTrr7dOy1DmmRpD3nuJs`
- JWE:
```json
{
  "protected": "eyJlbmMiOiJBMjU2R0NNIiwic2tpZCI6IjJwcmNOeEJGZlBnNmM5UTJxTmxPN0V0TGtZNGJZNVRadzVPR0g3U0U5blEiLCJ0eXAiOiJkaWRjb21tLWVudmVsb3BlLWVuYyJ9",
  "recipients": [{
    "header": {
      "alg": "ECDH-1PU+A256KW",
      "kid": "l43L62a4OFJ8M2rlbufPpkhxeaeUl4KobCLp-Ydh4Iw",
      "epk": {
        "use": "enc",
        "kty": "EC",
        "crv": "P-384",
        "x": "i18pUcAAJEvUz05Z50Eq6BFUjHCyZ6CpqaAod6fv4G849h_LzxeDcXJTleffpl8M",
        "y": "xGv29j3QOmWOrf3mLKPiTcc9ozju_5k-bwQLEqSnrzzCldB8FUpuSzTG5B_-4bv7"
      }
    },
    "encrypted_key": "BhcNeL62JoH3JSoFDGsaDrSGhRf5WYtDrJmOfjjkojzSUXxUGSX2Hw"
  }, {
    "header": {
      "alg": "ECDH-1PU+A256KW",
      "kid": "fzddOmU0rn6u_hOfw3mPiPbJTrr7dOy1DmmRpD3nuJs",
      "epk": {
        "use": "enc",
        "kty": "EC",
        "crv": "P-384",
        "x": "UmOsah42wB5yIFUW03DwNXYkZXneqPWeF_RnnHj6FpjZnpINw-4OYHCipAs9OeqH",
        "y": "BZIZY3oF9wnUPzPCE3W11j_udUyulx_jq7j35xvRpKN3f3YEhXP34LO9WN3BMDGc"
      }
    },
    "encrypted_key": "1LajR2QSjf9a8rARVLh3ACBDnONjXJLBA9az51VQBJAFwsqVaKl5sA"
  }],
  "iv": "E4ZwtG7DAKorlVNK",
  "ciphertext": "cKoEM9LBkrslLbdham0",
  "tag": "0q1ER9Kl-mDQiba2Hg3Yfg"
}
```

### 4 - JWE with 1 recipient having a NIST P-384 key:
- Generated protected headers: `{"enc":"A256GCM","skid":"IG_x2SxR_KyQeR3t6rsFgJ_n8D0J8xgXiLoJzJa93LU","typ":"didcomm-envelope-enc"}`
  - raw (no padding) base64URL encoded: `eyJlbmMiOiJBMjU2R0NNIiwic2tpZCI6IklHX3gyU3hSX0t5UWVSM3Q2cnNGZ0pfbjhEMEo4eGdYaUxvSnpKYTkzTFUiLCJ0eXAiOiJkaWRjb21tLWVudmVsb3BlLWVuYyJ9`
- Sender key JWK format:
```json
{
  "kty":"EC",
  "crv":"P-384",
  "x":"i8EMT7H8GvOHBxIpnK4KRtY-JFpGbrv9jZCL9vCPdJlTNuSRCUTN-Qg_X7198IJs",
  "y":"atlgVxKn7s7EFPjOUkkd9n93sQGk25prOaD92AhdQwoMmKXHkvryUetxI7M8DH6J"
}
```
- Sender kid (jwk thumbprint raw base64 URL encoded): `IG_x2SxR_KyQeR3t6rsFgJ_n8D0J8xgXiLoJzJa93LU`
- Single Recipient public key JWK format:
```json
{
  "kty":"EC",
  "crv":"P-384",
  "x":"eifGKTEyqQEc80MWWVUIG5UPtYZHrkXnLRoE4drk81v9395uAhqpoHap1WfrgxWm",
  "y":"nL2EOW-gl78CXB6iPzljtXp6gNdaVDWkGkrDdb-ial7-ODQzCuTYSWIisdWCbSgP"
}
```
- Single Recipient kid (jwk thumbprint raw base64 URL encoded): `PF0zWzsSVianFLt9w8vSCSbL2N47FKLY2o7EqXP0nvo`
- Finally, packing the payload outputs the following compact serialized JWE:
  `eyJhbGciOiJFQ0RILTFQVStBMjU2S1ciLCJlbmMiOiJBMjU2R0NNIiwiZXBrIjp7InVzZSI6ImVuYyIsImt0eSI6IkVDIiwia2lkIjoiUEYweld6c1NWaWFuRkx0OXc4dlNDU2JMMk40N0ZLTFkybzdFcVhQMG52byIsImNydiI6IlAtMzg0IiwieCI6Ik5RRlY4eld5WkNPYkRqb2kyVVd2WUdWSFZwaGVzYUNCaGxOWTllaXBiZEdyR2ZIdlN3VFpOV0NOUzlNOWxlQWsiLCJ5IjoibUsyY0pJblc2ZkcwbWFvSng1ZTJKT2Q4c2ZIZXdVZ1M3MGVfSmkwNnlWYVltMjdkcGVyeENMWDRFcDZLYllJcyJ9LCJraWQiOiJQRjB6V3pzU1ZpYW5GTHQ5dzh2U0NTYkwyTjQ3RktMWTJvN0VxWFAwbnZvIiwic2tpZCI6IklHX3gyU3hSX0t5UWVSM3Q2cnNGZ0pfbjhEMEo4eGdYaUxvSnpKYTkzTFUiLCJ0eXAiOiJkaWRjb21tLWVudmVsb3BlLWVuYyJ9.o6ZQl59iNS4YoRdwIxG17HGD_Yl77TT_lEwyRCsZvKLf6dltjGSG0A.fsiWAPS_KMrRCaDE.cx5LHW_9rucJ3DuGRXY.x-LezO4vj8kyhRe3IWtChw`
  
### 5 - JWE with 2 Recipients having NIST P-521 keys:
- Generated protected headers: `{"enc":"A256GCM","skid":"1zmWk0tE-IEIJD1JcRvv3WGe1uKiZx7xfmpuFGgF0lk","typ":"didcomm-envelope-enc"}`
  - raw (no padding) base64URL encoded: `eyJlbmMiOiJBMjU2R0NNIiwic2tpZCI6IjF6bVdrMHRFLUlFSUpEMUpjUnZ2M1dHZTF1S2laeDd4Zm1wdUZHZ0YwbGsiLCJ0eXAiOiJkaWRjb21tLWVudmVsb3BlLWVuYyJ9`
- Sender key JWK format:
```json
{
  "kty": "EC",
  "crv": "P-521",
  "x": "AdhVfT3Ki3JplMa0VyKcSQpoQkWxN8YRrh5jljDFHV5lC29EjGhSq95fLA9cb4fP5NY3e7l8j52Xr8XmLO5n1zVR",
  "y": "Ado2VVuYgUV15bHsuqXx_YTb5w3_kWNOuzwJKKwqh5D-RfAInh5p0EiSwOZKYhVN0OT8fcd_Me_3fOqNxRORdl30"
}
```
- Sender kid (jwk thumbprint raw base64 URL encoded): `1zmWk0tE-IEIJD1JcRvv3WGe1uKiZx7xfmpuFGgF0lk`
- Recipient 1 public key JWK format:
```json
{
  "kty": "EC",
  "crv": "P-521",
  "x": "AAOnYv8AM5_dzN9Agw1tGlimUBlHagRiH9BL86UvEObd_66ZUFgSL6MnZ-Ir2IQurHJpqE1f6KDu2iR9at2S6QzT",
  "y": "AVqOpK0LgLULOW9jYK856ANmia6D4SutpSkIwQ36UGuQeBFEKjPhMPdM-g1Gy_ZUOf4C5fEjHtb94pGWnDExHcgW"
}
```
- Recipient 1 kid (jwk thumbprint raw base64 URL encoded): `BxdEEMqIDdSXbhOEMsn8nzUv8iVs4WI84pXBRQJSSGI`
- Recipient 2 public key JWK format:
```json
{
  "kty": "EC",
  "crv": "P-521",
  "x": "AAs-4SCtBFWWVCbUBblFCgPlxsCNOrTtUAwoP-FB4GMj14vPTaBvnjn8kTV3dR7InUtN2rzOiB8AInidcxzR0ssP",
  "y": "AKV7Z9qbhdvrOis865SMO_BovWPAdzYhb8ov7KhGcfVtcW_jGLzb71dpvaH6dzmoqMPxpU2peb5r3bfg9m7Sck6c"
}
```
- Recipient 2 kid (jwk thumbprint raw base64 URL encoded): `UK7qxJGKz6mxS5Kf1iRSS903GBxNZ6NnpW6T-9nRql0`
- JWE:
```json
{
  "protected": "eyJlbmMiOiJBMjU2R0NNIiwic2tpZCI6IjF6bVdrMHRFLUlFSUpEMUpjUnZ2M1dHZTF1S2laeDd4Zm1wdUZHZ0YwbGsiLCJ0eXAiOiJkaWRjb21tLWVudmVsb3BlLWVuYyJ9",
  "recipients": [{
    "header": {
      "alg": "ECDH-1PU+A256KW",
      "kid": "BxdEEMqIDdSXbhOEMsn8nzUv8iVs4WI84pXBRQJSSGI",
      "epk": {
        "use": "enc",
        "kty": "EC",
        "crv": "P-521",
        "x": "AFu68XGeBZ-PPtFK2MGuuRHGaVMu1RMNtlzKd0tV7bI6LzLcsJn_9OkLsmk99ooBmIKUh1F8IyYVEgkmbjFOGEUt",
        "y": "AIbbKGljHSkq-x4KQJUx-I8um0o0MEcuOqWH_6gFKm_B1R5rxRUQ57LPDpGVHFFHfZs897mEMQo9AMbKpeWYIwFY"
      }
    },
    "encrypted_key": "r8qtJxcjieEWndVZdOSsoAgspaSguOZ-xLe-ZyFeUuJqd1H_AaNLYQ"
  }, {
    "header": {
      "alg": "ECDH-1PU+A256KW",
      "kid": "UK7qxJGKz6mxS5Kf1iRSS903GBxNZ6NnpW6T-9nRql0",
      "epk": {
        "use": "enc",
        "kty": "EC",
        "crv": "P-521",
        "x": "AGmx6tTwLxpXG7bzJBz3GhFXpvhvl_ArT8ocJMlr4POxIhqzfTumGdTUtf70W9zYpZQP1vxfSdtpdD4cRxInWVKM",
        "y": "ABk--snk1KMxD2HOCZ2BtIdQeoF7My4FknN-j0-7wFEOMjWZFzWuFlXy70KtFhwKY1fjxk_59fOoWtsvNM_Bypjj"
      }
    },
    "encrypted_key": "VejyY73O8ZqlqyczQ-MvaFy3H68q9XhjXXH3cWomzQG6Ulyw5khGcw"
  }],
  "iv": "W9bIY0gf0cZW4yGA",
  "ciphertext": "m4gZiDXloGQ9VeyZfdg",
  "tag": "QjZV7fNUUxG10wQH7PlBnQ"
}
```

### 6 - JWE with 1 recipient having a NIST P-521 key:
- Generated protected headers: `{"enc":"A256GCM","skid":"3Gk9f97TO5-u33a3X3_Yy7Dwpi2zeKcFAe4NHCrSiWA","typ":"didcomm-envelope-enc"}`
  - raw (no padding) base64URL encoded: `eyJlbmMiOiJBMjU2R0NNIiwic2tpZCI6IjNHazlmOTdUTzUtdTMzYTNYM19ZeTdEd3BpMnplS2NGQWU0TkhDclNpV0EiLCJ0eXAiOiJkaWRjb21tLWVudmVsb3BlLWVuYyJ9`
- Sender key JWK format:
```json
{
  "kty": "EC",
  "crv": "P-521",
  "x": "AGPH4atXUzB82uXeZCZ6du7zHzDrgDMNUSR6CYCwqYDw6gzxlFoxjv59izugEdl7k_dmdMqHAHogKer3zxcvcd98",
  "y": "AfI2wUdaitifNuPKc2HDI4aQzKFIhVh1cR7KbLYpztWU6nV1XV-1R0uvDzxo63rj8Cr7mtnbwgKiI6uIpTCSJiiE"
}
```
- Sender kid (jwk thumbprint raw base64 URL encoded): `3Gk9f97TO5-u33a3X3_Yy7Dwpi2zeKcFAe4NHCrSiWA`
- Single Recipient public key JWK format:
```json
{
  "kty": "EC",
  "crv": "P-521",
  "x": "AZe6m9X8Xv7LXluoGwx3a9LTTk_Z6rXTaRJBz-qr3Dz7nRv28ETHR4-XlyW777ychj2W9Ym39jZhpS8wyKKigcbc",
  "y": "AOOCeR9yA7UXN7U3_2thb_97V4OXckmSKrN-rBMAx86BQmUwKcQWT9FeuWWazsNf3tswPDWAitr3zeIqzCR8zOQL"
}
```
- Single Recipient kid (jwk thumbprint raw base64 URL encoded): `3h8b5WM3yj5MgPb1iTnSp0rfyFS8NGMPCxzgD7Y7CU4`
- Finally, packing the payload outputs the following compact serialized JWE:
  `eyJhbGciOiJFQ0RILTFQVStBMjU2S1ciLCJlbmMiOiJBMjU2R0NNIiwiZXBrIjp7InVzZSI6ImVuYyIsImt0eSI6IkVDIiwia2lkIjoiM2g4YjVXTTN5ajVNZ1BiMWlUblNwMHJmeUZTOE5HTVBDeHpnRDdZN0NVNCIsImNydiI6IlAtNTIxIiwieCI6IkFDRnJueXZUT0lfV0w0aG9Lamg2NnFfUzJHMFRLdkNOOFZsLTQ5NXhjVnlWNGdPQzRTWWRabXhacnJrc2VyWGM3cDlYUUk2WExQQU5VVUg1c1NqNEhEMkUiLCJ5IjoiQVIwVzBWbHg5a1lJYjNaeDJmcWlhb0Z1SEh1N0lUTnFERXpSWnhJZUdEUk8wREdpbk8zeWlrUDZnLWI2VFVmUFdrVmhjZEpEM2hOaUhDZFZCOVllRlBUdSJ9LCJraWQiOiIzaDhiNVdNM3lqNU1nUGIxaVRuU3AwcmZ5RlM4TkdNUEN4emdEN1k3Q1U0Iiwic2tpZCI6IjNHazlmOTdUTzUtdTMzYTNYM19ZeTdEd3BpMnplS2NGQWU0TkhDclNpV0EiLCJ0eXAiOiJkaWRjb21tLWVudmVsb3BlLWVuYyJ9.-A7BetvOiGxV56SgxVxk7zI8s7HMylw9c8KhfNJXvEIZ-QpHAkAoog.vYmMxQ7S-FhEt7eE.SduRuwcfp31g2fykGEs.dDIDlOROeTdgxP5QFJvsDw`
