# **Registrasi Klaim Asuransi Umum**

### **Description**
Method to register a new claim for General Insurance

### **HTTP Request**
> POST https://apidev.askrindo.co.id/api/polis/create

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
| trxId | string | Yes | Unique ID, 9 digit padded with leading zero(s)  i.e: 000000123 |
| trxDateRequest | string | Yes | UNIX Timestamp |
| nomorPolis | string | Yes | 1= Realtime, 2= Pending |
| namaPelapor | string | Yes | Nama Pelapor |
| noRekening | string | Yes | Account Number |
| emailPelapor | string | Yes | Email Pelapor |
| telpPelapor | string | Yes | No kontak pelapor |
| dateOfLoss | string | Yes | UNIX Timestamp |
| lokasiKejadian | string | Yes | Lokasi tempat kejadian klaim terjadi|
| lossCause | string | Yes | Sebab kejadian |
| Files | string | Yes | URL File sharing(Google Drive,e-filling,dll) |
| Files[] | JSON Array | Yes | File List(Jenis File,Nama File,File yang di Encode dalam Base64) |

```json
{ 
    "trxId" : "000000123", 
    "trxDateRequest" : "1597288286", 
    "nomorPolis" : "1101.20.011.7.00016-6/00", 
    "namaPelapor" : "Yolanda", 
    "emailPelapor" : "putuyolanda2@gmail.com", 
    "telpPelapor" : "123450191", 
    "dateOfLoss" : "1597288286", 
    "lokasiKejadian" : "Kaliasem", 
    "lossCause" : "Sengaja", 
    "additionalFiles1" : "-", 
    "additionalFiles2" : ["-"] 
}
```

### **Response**
| Field | Data Type | Description |
|:---------|:-----|:------------|
| trxDateResponse | string | UNIX Timestamp |
| data | JSON Object | |
| vaNumber | JSON Array | |
| vaNumber | string | Virtual Account Number |
| bankCode | string | Bank Code |
| currency | string | Currency |
| amountPremi | JSON Object | Policy Period |
| IDR | string | Premium Currency |
| policyNo | string | Insurance Policy Number |
| message | string | |
| transactionId | string | Transaction ID |
| errorNumber | string ||
| status | string | Response Code |

```json
{
	"trxDateResponse":"1594368719",
	"data":{
		vaNumber":[
		{
			"vaNumber":"8817220000006392",
			"bankCode":"BMRI",
			"currency":"IDR"
		}],
		"amountPremi":{
			"IDR":"80000.00"
		},
		"policyNo":"1101.20.004.7.00053-8/00"
	},
	"message":"Sukses",
	"transactionId":"0000111",
	"errorNumber":"",
	"status":"01"
}
```
