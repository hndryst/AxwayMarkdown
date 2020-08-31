# **Inquiry Status Klaim Asuransi Umum**

### **Description**
Method to retrieve the status of General Insurance Claim

### **HTTP Request**
> POST https://apidev.askrindo.co.id/api/claim/inquiry

### **Request Header**
| Name | Format | Mandatory | Description
|:---------|:-----|:------------|:--------------|
| Authentication | Bearer token | Yes | Refer to Authentication API for requesting your token |
| askSignature | Hash Value | Yes | See below for more details |
| Content-Type | application/json | Yes | |
  

**Hash Value**
To successfully authorize the API call,the **askSignature** header must contain a hash value with the following requirement:
- Type: HMAC SHA-256  
- String: clientId:secret  
- Secret Key: secret  
- Encoding: Lowercase Hex  

**Example**  
	**clientId:** "12345678-abcd-ef12-3456-12ab34cd56ef"  
	**secret:** "abcd1234-1234-56ab-cdef-123456abcdef"  
	**String:** "12345678-abcd-ef12-3456-12ab34cd56ef:abcd1234-1234-56ab-cdef-123456abcdef"  
	**Hash Value:** "d4d71c6d4bef2503dc28bf2932701b83dc571d11a34d0bbee2141e15f25f98cd"  

### **Request Payload**
| Field | Data Type | Mandatory | Description
|:---------|:-----|:------------|:--------------|
| trxId | string | Yes | Unique ID, 9 digit padded with leading zero(s) i.e: 000000123 |
| trxDateRequest | string | Yes | UNIX Timestamp |
| docNoType | string | Yes | 1= No Polis,2= No Registrasi Klaim |
| documentNo | string | Yes | No Polis or No Registrasi Klaim |

```json
{
    "trxId" : "CLM0016",
    "trxDateRequest" : "1583712000",
    "docNoType" : "1",
    "documentNo" : "1101.20.011.7.00016-6/00"
}
```

### **Response**
| Field | Data Type | Description |
|:---------|:-----|:------------|
| trxDateResponse | string | UNIX Timestamp |
| data | JSON Object | |
| premiums | JSON Array | |
| currency | string | Currency |
| amountPremium | string | Premium Amount |
| nomorPolis | string | Policy Number |
| jangkaWaktu | string | Policy Period |
| nama | string | Policy Holder |
| produk | string | Product |
| status | string | Policy Status |
| message | string | |
| transactionId | string | Transaction ID |
| errorNumber | string ||
| status | string | Response Code |

```json
{
    "trxDateResponse": "1594299134",
    "data": {
        "premiums": [
            {
                "currency": "IDR",
                "amountPremium": 1500000.0
            }
        ],
        "nomorPolis": "1101.20.004.7.00007-5/00",
        "jangkaWaktu": "30062020 - 30072020",
        "nama": "Afrian",
        "produk": "PA / Personnal Accident",
        "status": "Active"
    },
    "message": "Sukses",
    "transactionId": null,
    "errorNumber": "200",
    "status": "00"
}
```
