# Reverse Engineering

By analyzing the dm_decryptFile function in libcmm.so, it can be observed that an 8-byte static value (DAT_000ca1f0)
is copied into a local buffer and passed directly to the cen_desMinDo function,
which performs DES decryption

<img width="1616" height="604" alt="image" src="https://github.com/user-attachments/assets/aff2ae4a-39bf-422e-88f1-9e7b6f3366d3" />

later can key can be used to decode files for example like that:

```
openssl enc -d -des-ecb -K key_here -nopad -in file.xml
```
