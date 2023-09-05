Number encoding process. Contact our NOC to provide a salt value as the encoding salt. Use the following code to encode the number and send it to the client, or use the encoded number on the client side to make calls. The real number will be encoded into another number to initiate the call, preventing the leakage of the actual number.

# Encoding Code Reference
## Java
```
public static String aaas(Long phone, Long salt) {
    String phoneStr = phone + "";
    int len = phoneStr.length();
    String prefix = "";
    int suffix = 0;
    if (len > 8) {
        prefix = phoneStr.substring(0, len - 8);
        phoneStr = phoneStr.substring(len - 8);
        phone = Long.valueOf(phoneStr);
        suffix = 8 - phone.toString().length();
    } else {
        phone = Long.valueOf(phoneStr);
        suffix = len - phone.toString().length();
    }
    Long newphone = (phone & 0xff000000);
    newphone = (phone & 0xff000000);
    newphone += (phone & 0x0000ff00) << 8;
    newphone += (phone & 0x00ff0000) >> 8;
    newphone += (phone & 0x0000000f) << 4;
    newphone += (phone & 0x000000f0) >> 4;
    newphone ^= salt;
    return prefix + "" + newphone + "" + suffix + "" + newphone.toString().length();
}
```
## JS
```
function encode_phone(phone, salt) {
    len = phone.toString().length;
    prefix = "";
    suffix = 0;
    if (len > 8) {
        prefix = phone.toString().substr(0, len - 8);
        phone = phone.toString().substr(len - 8);
        suffix = 8 - parseInt(phone).toString().length;
        phone = parseInt(phone);
    } else {
        phone = parseInt(phone);
        suffix = len - phone.toString().length;
    }
    newphone = (phone & 0xff000000);
    newphone += (phone & 0x0000ff00) << 8;
    newphone += (phone & 0x00ff0000) >> 8;
    newphone += (phone & 0x0000000f) << 4;
    newphone += (phone & 0x000000f0) >> 4;
    newphone ^= salt;
    return prefix + "" + newphone + "" + suffix + "" + newphone.toString().length;
}
```
## PHP
```
function encode_phone($phone, $salt)
{
    $len = strlen($phone);
    $prefix = "";
    $suffix = 0;
    if ($len > 8) {
        $prefix = substr($phone, 0, $len - 8);
        $phone = substr($phone, $len - 8);
        $phone = (int)$phone;
        $suffix = 8 - strlen($phone);
    } else {
        $phone = (int)$phone;
        $suffix = $len - strlen($phone);
    }
    $newphone = ($phone & 0xff000000);
    $newphone += ($phone & 0x0000ff00) << 8;
    $newphone += ($phone & 0x00ff0000) >> 8;
    $newphone += ($phone & 0x0000000f) << 4;
    $newphone += ($phone & 0x000000f0) >> 4;
    $newphone ^= $salt;
    return $prefix . $newphone . $suffix . strlen($newphone);
}
```