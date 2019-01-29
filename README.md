# BharatQR
BharatQR documentation for merchants 

## Test Environment url: https://testqr.wibmopay.com/qr/merchant

***

This is the documentation for integrating BharatQR. 

merchant_name and merchant_secret will be shared separately on email.

## Pseudocode For CheckSum Generation

You can find below the steps to be followed for generating the checksum when making the POST request. 
Also, pseudo code is written below to give you an idea. 

1. Initialize an array and put in elements as 
     arr = [merchant_display_name,merchant_mobile,merchant_email,merchant_name,merchant_secret]

2. Concatenate elements in array with pipe(|)  
     for (data in arr){  
     checksum_str  += str(data) + '|'  
     }
    
     checksum_str = checksum_str[:-1]  

3. Generate hash512  
     return hashlib.sha512(checksum_str).hexdigest().upper()

for further queries please reach out to the developers on backend@wibmopay.com

## Sample Code for checksum in Python  
```py
import hashlib  
arr = [merchant_display_name,merchant_mobile,merchant_email,merchant_name,merchant_secret] 
checksum_str = ''  
for data in arr:  
   checksum_str  += str(data) + '|'  

checksum_str = checksum_str[:-1]  
return hashlib.sha512(checksum_str).hexdigest().upper()  
```
## Sample Code for checksum in PHP  
```php
<?php  
$arr = array(merchant_display_name,merchant_mobile,merchant_email,merchant_name,merchant_secret);  
$checksum_str = '';  
foreach ($arr as $data){  
  $checksum_str  .= (string)$data . '|';  
}  

$checksum_str = substr($checksum_str, 0, -1);  
return strtoupper(hash("sha512", $checksum_str));  
?>  # Bharat QR 
```

## Sample Code for Checksum in Node JS  
```js
var crypto = require('crypto');  
var arr = [merchant_display_name,merchant_mobile,merchant_email,merchant_name,merchant_secret];  
var checksum_str = '';  
for(var i = 0;i<arr.length;i++){  
	checksum_str +=  arr[i] + '|';  
}  

checksum_str = checksum_str.substring(0, checksum_str.length - 1);  
return crypto.createHash('sha512').update(String(checksum_str)).digest('hex').toUpperCase();  
```

## Sample Code for Checksum in JAVA  
```Java
 static String sha1(String input) throws NoSuchAlgorithmException {
        MessageDigest mDigest = MessageDigest.getInstance("SHA-512");
        byte[] result = mDigest.digest(input.getBytes());
        StringBuffer sb = new StringBuffer();
        for (int i = 0; i < result.length; i++) {
            sb.append(Integer.toString((result[i] & 0xff) + 0x100, 16).substring(1));
        }
         
        return sb.toString();
    }
```
For testing of java checksum code please visti URL - http://tpcg.io/kc0v6z


**Documentation Last Updated - 29th january 2019**
