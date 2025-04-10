# Криптування даних

#### Запит криптування номеру картки

Приклад тіла запиту

```json
curl --location --request POST 'https://api-ecom-release.develop.bankalliance.ua/cipher/encrypt_by_jwk?message={{cardNumber}}' \
--header 'Content-Type: application/json' \
--header 'Cookie: visid_incap_2770403=fJEGXzciTnG2/y/pST3lzBM/JGMAAAAAQUIPAAAAAAAV+dwIpk/4YrgvV5ijeEu6' \
--data-raw '
{
    "kty": "EC",
    "use": "enc",
    "crv": "P-384",
    "x": "lxF9kVkpdTRqd256CO0Q3fOEgAPcek-U_Q72UoySdXXZWr9Tf8bSMhc8gwVbgtDC",
    "y": "3aQaGq0Va9OsGhPr63jZ2KEcfO1jqibz6bKFeJr6K6h4dHFGj298hv7sb6bYaUyD",
    "alg": "ECDH-ES+A256KW"
}'
```

Приклад відповіді

```
eyJhbGciOiJFQ0RILUVTK0EyNTZLVyIsImVuYyI6IkEyNTZHQ00iLCJlcGsiOnsia3R5IjoiRUMiLCJ4IjoiUTZpa29VREhpSEZBTXctRG1qUWdmLXVVS2ktWXpyc21qYXRPakI2a3RmZDJjbE1ndUk5TGRreHprMEtnNmNwaCIsInkiOiJNMjF6V1BEeVVOZDA2a216dU82WTNybXFMNUZXM0xyblNZOVBnTXVnRklrU1Q5ZGM3Qno1R0xscDN4U1lIdXlvIiwiY3J2IjoiUC0zODQifX0.Kgb_4R6L2SAL077b34Ulop5tU8ICVeRhQxTlpDosg-UbfsHWx1IIbA.gIkAptJJlhH6Gf-W.-A98wK-imBnwvdAmRpy2wgofZtZ6tRsp3W4Zna-Ye1kBcjFh-93iMz73LfRjvxsKQYzSEbcYXTbd.YHunREy1MjVTRpnTRSsnGw
```

#### Запит криптування cvv та expDate

Приклад тіла запиту

<pre class="language-json"><code class="lang-json">curl --location --request POST 'https://api-ecom-release.develop.bankalliance.ua/cipher/encrypt_by_jwk?message={{dateCvv}}' \
<strong>--header 'Content-Type: application/json' \
</strong>--header 'Cookie: visid_incap_2770403=fJEGXzciTnG2/y/pST3lzBM/JGMAAAAAQUIPAAAAAAAV+dwIpk/4YrgvV5ijeEu6' \
--data-raw '
{
    "kty": "EC",
    "use": "enc",
    "crv": "P-384",
    "x": "lxF9kVkpdTRqd256CO0Q3fOEgAPcek-U_Q72UoySdXXZWr9Tf8bSMhc8gwVbgtDC",
    "y": "3aQaGq0Va9OsGhPr63jZ2KEcfO1jqibz6bKFeJr6K6h4dHFGj298hv7sb6bYaUyD",
    "alg": "ECDH-ES+A256KW"
}'
</code></pre>

Приклад відповіді

```json
eyJhbGciOiJFQ0RILUVTK0EyNTZLVyIsImVuYyI6IkEyNTZHQ00iLCJlcGsiOnsia3R5IjoiRUMiLCJ4IjoiY3hEcmZmZjBuRWtVU0JyX0JUN2h3SWt5V1hOV3JjNnhtaVdLV3VHZ3hNaGJoR3kza21DQVRoRjRXb1FKTEstZiIsInkiOiI4dHlqUGJtc3lxdlhDZDJQMC1FZjdEcm8zRVhxczlIWXRieWQzQzFzZS00bDJ3YkJ1djZBT2dyZHhpaUNGS0pKIiwiY3J2IjoiUC0zODQifX0.qWawnXb-PgoDgG0hbeVt9bDs1pmg4isWPfjf_7wiUfXTKsPvVrLTaw.upp1rnEiiahsghoI.lQ1Kv2sYaQ.gxOr0AdNyOctlBqZqIuUQQ
```

#### Запит криптування тіла запиту Purchase

Приклад тіла запиту

```json
curl --location --request POST 'https://api-ecom-release.develop.bankalliance.ua/cipher/encrypt_by_jwk?message=%7B%0D%0A++++++++%22merchantId%22%3A+%22137d9304-0368-11ed-b939-0242ac120002%22%2C%0D%0A++++++++%22merchantRequestId%22%3A+%22{{requestUUIDT}}%22%2C%0D%0A++++++++%22encryptedCardNumber%22%3A+%22{{encryptedPanT}}%22%2C%0D%0A++++++++%22coinAmount%22%3A+%221000%22%2C%0D%0A++++++++%22comment%22%3A+%22comment%22%2C%0D%0A++++++++%22purpose%22%3A+%22purpose%22%2C%0D%0A++++++++%22desiredThreeDSMode%22%3A+%22MUST_NOT%22%2C%0D%0A++++++++%22date%22%3A+%22{{currentdateT}}.00%2B03%3A00%22%0D%0A++++++++%7D'
```

Приклад відповіді

```json
eyJhbGciOiJFQ0RILUVTK0EyNTZLVyIsImVuYyI6IkEyNTZHQ00iLCJlcGsiOnsia3R5IjoiRUMiLCJ4IjoiUTQ0TUJpOHJvQ2RyNjlHdm9DNUFoQkRaLXdrZGtiZ3hSSW44SlFjMlNwa3B6QmRaY0VJYklaM1dXNkstcDlsSCIsInkiOiJ6RXlwYWU0ZXVUSUlrQ0tkVC14ZTdUQ2haaGdLX2xLTmRqN29hUmdOd0J0bnMxUjVvU2ZiR2RPNktRdVpRYzgxIiwiY3J2IjoiUC0zODQifX0.GadCMT_Gc9K1cN-VMnV1HCddxmYS9Roj7gYIOdHkyCScryGOieZOZQ.VjJtho7IEYdFHLYm.FE-TwGErA2xQgoWUVDecvHAKVI2RbZ8glI_xRTe_RgjvLg4QT_4z7p-fMvSe3ERV6Hv2HHwew1uYCXPWa1vfsZLonxro9ccMZiXxHlDmhVQBojUJPGg5Sk6wYI4WIjgEvlgkQJ3JKnH2aNIqx-C-uDuKYmpF0oR1f8oxJiFlTBUZFxHsu00wlxtPNRFQWXgDFAZaMk0fTK2R_R8TpsKXBDT-ygrh8IrXkzdxMVRZFKnY24THnT9vrECdsd4XlMfazBwMaVRu8egEjU72-iYF5b8HN4TQdGZePWXolGpcYJ3pCmzW9BC5gD5wG3z2RYKBWiMlBjldJ5BT_ATjbkzrvMjslJxPJwTS8Z7dMPP_ibS055B-KL05kEIYIATbZBKITZGamzjoWOkfFLJsO2nsHxIggBOePNrJlhDt2rPUj4-wFCceCJhn65ZHDBhOhVQIoIAIpZzqAztYXBrfZRlcPbsDNX_sNQBUYeRHFRY9r77pSXnGnwkF0zxkD5-vSIKtDJAMCkFuu4DtXQIG-oW1ko6KolmAQm7HrlB_Hz_ysB54c59xT8zDCYeF11sc48erLHTKoKv315vjx4txf1JFjePSBmh624sDMZXg1wbiLHahSSl9igbP0_KGvtm5zA_B599_IsFHdjAgSZhUChsYFafEf9DewDo8zGEfPWtHZl76hMGbaFpZwXYeyC_vaqaCuSaBpzVVv8oYZqlK5BaZMRqrcvWaBTyHoSDcxzywjPE01aXrxzFn3WtauiILM76MREorUHrEmtGL6hW7ijmKn-MwxhmuVCvnC9p1nEq_4LQhNu3lGyLw3YGfl1ovfhOZOzNeclypKoJyfElbmuYSVrEpe1DV0JdejGiidTTvrolk9xp45kl4o-54BocPcqFiTsyDuGNZR1_RICfhoWEXyibiE6EHdJOFg2nAmj0zoa-FDA905hD-Cr1Vyn4c_YuqwgbRDILFMUng6sadmz_uJ2WNZyqhiPTxaHR7gT_DsRoOCL7FbaEbNexobnSQLRSPd3Ye0c3uzqxOOFTiG-pmFuZlzbOPP5N86RVIHwjN_8L1XczJfbHQAjd60InwP1EmY3FhVDTT8m3I1Pm8BZM7Qnn2nVA3eO1kuy2iVjqLDtEWQtvfUrlivx7-xtOUY3oGi0YvzgPuROSfwCf-znWtZpItkTDJYuq3_jQhxN4_ncGSNYjcP5Jn8kJEIIUhHXcJbpkgMaQkb4iVDN-evOWaek1Rs2cghLWGrfrxuHwsGsM4J7YN-oEye2dp4PfVwP72AsHmB0IVMmZYGg2BN3_CeIpMtGJax6CPUtfiFjOUpk1Wcksciiq7CQySJSlTLrbDOYzP3s-UeD9h7P_toPTpqnhQOdcRNqYwUnSixK7RblwDQU20qo_1EuvoO5W-nANvHuZOS9qDD6RuVbaV0F6GZGTAiwJfc9XWXP1bAv0KZUkM4Bt2RnKnfO4Bum-mVgUEO49z.iLpH0bfL0nGaiBCLUtNjvw
```

#### Запит криптування тіла запиту А2С

Приклад тіла запиту

```json
curl --location --request POST 'https://api-ecom-release.develop.bankalliance.ua/cipher/encrypt_by_jwk?message=%7B%0A%22encryptedCardNumber%22%3A%22{{encryptedPanT}}%22%2C%0A%22merchantId%22%3A%22137d9304-0368-11ed-b939-0242ac120002%22%2C%0A%22merchantRequestId%22%3A%22{{requestUUIDT}}%22%2C%0A%22purpose%22%3A%22%D0%B7%D0%B0%20%D1%82%D0%BE%D0%B2%D0%B0%D1%80%22%2C%0A%22coinAmount%22%3A%20120%2C%0A%22comment%22%3A%20%22test%22%2C%0A%22recipientCountry%22%3A%20%22840%22%2C%0A%22recipientCity%22%3A%20%22Kyiv%22%2C%0A%22recipientStreet%22%3A%20%22T.%20Shevchenka%2C%2011%22%2C%0A%22recipientFirstName%22%3A%20%22TestFirstname%22%2C%0A%22recipientLastName%22%3A%20%22TestLastName%22%2C%0A%22date%22%3A%20%22{{currentdateT}}.00%2B03%3A00%22%0A%7D' \
```

Приклад відповіді

```json
eyJhbGciOiJFQ0RILUVTK0EyNTZLVyIsImVuYyI6IkEyNTZHQ00iLCJlcGsiOnsia3R5IjoiRUMiLCJ4IjoiT3BPU3BzbmdhUFNZa3pyaFdOQ0hOdmVkcFpZa055aTFpV3FuODFJNnVtaWh3V3BRdWd3TExyNGNJbXdicm0zbiIsInkiOiJGQlJvVTNfOERsRmtCdEZuTzRwOEJFdFI3N3YxcWtIb3BNZmpTbjNxTmVvazVUSDN5RHN1V0dQTW9JR0JQOTZKIiwiY3J2IjoiUC0zODQifX0.cI9Lt-3nxTMgYYQzMRW3uTJ1ht2EKNNhWZQ0kL76Y8KGAs8YVnVJFw.V93PFOyteOScc-h9.Mf9xemx756NyTyTu9Qis9gNd7zshewoO2fBZDV9VWLYMhIR3VAQY1YaNAkR81XFcIV1dq4MGM61rQxdv9YvKz-RuwN0OsNfcUa8hYbtwwtmmLqg4gWVZFskF9jM1aQzhSFNsRM5eZgu3Qo7zk2mvWn5flX6BLKywQYstx-nYGi_9NRIwYVNKalAGUaOClneMxUepgJ_fYGmHfw2U4GDo09qWVsNfWLwRkT8jVXvKRfY755DQJgIDQm2HxhszdwG4YQjpA7SdYATNx1IFUwFQwIbeGntpZOPHRJCQ5zd2k_5bBGkEw1mvXBHtd8pEcbaPXxN4Bsx2vjSOBbItBmfbweLgtfcCwwZYxpi-dIMN-Yn1Gvh_ba7H0_WokObbo_MiwqJ-UBAYqPsJoH-7VetcqY9W-NGPYXIrHcVG5dEC7vx0_9HtVD1T8zZtCbA9MNMLQbzCa6YXqWFO5NzS8qTCCgV4KZ7NrQwfsStDpcXi3fsgGnV8EPRDyFg-KYed5pV8zL80Fsp4YDCo9FVFmm88mcGq1k1Dr6AKredjkSV0xutgrQdyELCWnjQ7hKlOu3RpTBtdBONnjhVWd8KtJo8AGQrZPBvLWJEcph5bJ7_bKJPJw8DIPoGbXWbb21Oo0iNwl1k1B2q3lvrdnJbi3PD1n09uii87oMetzJlwwOCNXb6xZdpSk0tNr_klcKrFuHvZPl9gMGEgodp1rYwt012ePNPEWM9YcavwsMxUxZL1m_y20fAjvYAVgBXeShT-kPLCvZhj75x4varjiEziQkuOv2MRmL1c4RRU9i3gX26ZrhSccxxJTgH0mUmdxN-sHLB1ee3smFQuCmF0hymPwlmG2EpmWDoIg8xMNQsmZ3ViTEBBA24CptVAudHN4P-RVoCkyOuRigamOuVYPMjR2Mm_E0RY7oDF-4815zd1AloieLMdpFSUNL-wRmxOWyozFeZcUsnP0oLlxanV8SrhZVGCjMVvQlhhxHrtB0vYQf00qQmCaQO7eE39dauutBvgZLj1BrwUfLAfRTHBBidDDPCmRUNO7tEk86rgkQ.v4DT6Pf_UrCIEql2MI0iPw
```

#### Запит криптування тіла запиту Refund

Приклад тіла запиту

```json
curl --location --request POST 'https://api-ecom-release.develop.bankalliance.ua/cipher/encrypt_by_jwk?message=%7B%0A%22merchantId%22%3A%22137d9304-0368-11ed-b939-0242ac120002%22%2C%0A%22merchantRequestId%22%3A%22{{requestUUIDT}}%22%2C%0A%22coinAmount%22%3A%20400%2C%0A%22operationId%22%3A%20%2216819994379960P3JOgL9oph%22%2C%0A%22date%22%3A%22{{currentdateT}}.00%2B03%3A00%22%0A%7D' 
```

Приклад відповіді

```json
eyJhbGciOiJFQ0RILUVTK0EyNTZLVyIsImVuYyI6IkEyNTZHQ00iLCJlcGsiOnsia3R5IjoiRUMiLCJ4IjoiTW5Edlg5WVBmdGg0OU9BRWlwWnQtZ1VPTkJ4ajNIM2NpQ3J3M0JVamFndXB4VUFZYmVnZll0SG9PVXNMWXVNbiIsInkiOiJOVnl0ZS1tUEZ1MXZSUnhiT2sxcWdLaHV4aThXdlZxYVo1c2JqeUc0VXN3S1EweGRfMXhRSmF0cmpfYWt2LVdyIiwiY3J2IjoiUC0zODQifX0.C6xXq_hTVMDJ6OBmLDJW0fytlv7DHLYhjmECFF8Ms22Lvo6Gmrhi9w.bHiTlA147DpUuMPT.AznDDpYaUKOQvPRT3UKYlcxByZtv1qm_TbK86Tn9pqlQz9rfucjDmBD31NuK4ZTyI_d9Vbv8vcK2JU96bg1_J5wbmgZqN_4hvyZvQ39QaL_xVUkt3EesYBH_0VyhWBm--ojnHxJgvWkF8X4xFAYp9sU7jVdsQUNRKZajLzgAR65uSTveEsZ69aifDze0C_GxDwNaRhuv6_twoQGoVLTf3IpVndAqFWhMoAqY-VNWuW9upqRWd5MVX0Lr7ngUKYWTMD0C4b2BJWsH8xoVZyuA_6ggRwqhhx5Jz0010pBMM29TNToCLA.n04GZIciLzo_BBnXKKO0Rg
```

#### Запит декриптування тіла відповіді

Приклад тіла запиту

```json
curl --location --request POST 'https://api-ecom-release.develop.bankalliance.ua/cipher/decrypt_by_jwk?message={{responseJwe}}' 
```

Приклад відповіді

```json
{
"operationId":"7efc160e-f9d9-49dd-bc1d-38c064193c5a",
"status":"SUCCESS",
"rrn":"1037470888"
}
```
