**SMS Text Only Contains GSM-7 Encoded Characters**

> 160 characters per message, supports long messages. Character count includes the signature. If the message exceeds 160 characters, it will be billed as 154 characters per message.

> For GSM-7 basic characters, each character counts as 1 character. For GSM-7 extended characters, each character counts as 2 characters. (Refer to the standards and screenshot below for basic and extended characters)

**SMS Text Contains Characters Other Than GSM-7 Encoding (e.g., Chinese, Japanese, Korean)**

> For non-GSM-7 languages, the limit is 70 characters per message (regardless of Chinese or English). Supports long messages. Character count includes the signature.

**Terminology Explanation**

> **GSM-7** is a character encoding standard that packs the most commonly used letters and symbols from many languages into 7 bits for use in GSM networks. Since an SMS message is transmitted in 140 8-bit bytes, a GSM-7 encoded SMS message can carry up to 160 characters.

> [GSM 03.38 Standard Document](http://www.etsi.org/deliver/etsi_gts/03/0338/05.00.00_60/gsmts_0338v050000p.pdf)

> [GSM Supported Characters](https://en.wikipedia.org/wiki/GSM_03.38#GSM_7-bit_default_alphabet_and_extension_table_of_3GPP_TS_23.038_.2F_GSM_03.38) Text as follows: ![GSM-7 Characters](https://github.com/nxtele/http-api-document/blob/main/1.png?raw=true)

**Special Country**
> For Malaysia (Country Code 60), an additional 7 characters will be automatically added to the original character count.