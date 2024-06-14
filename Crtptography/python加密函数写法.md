使用常见的加密算法，比如AES、DES、RSA等。可以使用Python中的第三方库，比如cryptography和pycryptodome来实现。示例代码如下：

```
# 使用AES加密解密字符串
from cryptography.fernet import Fernet
 
def encrypt_string(message, key):
    cipher_suite = Fernet(key)
    encrypted_message = cipher_suite.encrypt(message.encode())
    return encrypted_message.decode()
 
def decrypt_string(encrypted_message, key):
    cipher_suite = Fernet(key)
    decrypted_message = cipher_suite.decrypt(encrypted_message.encode())
    return decrypted_message.decode()
 
key = Fernet.generate_key()
message = "Hello, world!"
 
encrypted_message = encrypt_string(message, key)
decrypted_message = decrypt_string(encrypted_message, key)
 
print("Encrypted message:", encrypted_message)
print("Decrypted message:", decrypted_message)
```

```
# 使用RSA加密解密字符串
from cryptography.hazmat.primitives import serialization, hashes
from cryptography.hazmat.primitives.asymmetric import rsa
from cryptography.hazmat.primitives.asymmetric import padding
 
def generate_rsa_key_pair():
    private_key = rsa.generate_private_key(
        public_exponent=65537,
        key_size=2048
    )
    public_key = private_key.public_key()
    
    return private_key, public_key
 
def encrypt_string_rsa(message, public_key):
    encrypted_message = public_key.encrypt(
        message.encode(),
        padding.OAEP(
            mgf=padding.MGF1(algorithm=hashes.SHA256()),
            algorithm=hashes.SHA256(),
            label=None
        )
    )
    return encrypted_message
 
def decrypt_string_rsa(encrypted_message, private_key):
    decrypted_message = private_key.decrypt(
        encrypted_message,
        padding.OAEP(
            mgf=padding.MGF1(algorithm=hashes.SHA256()),
            algorithm=hashes.SHA256(),
            label=None
        )
    )
    return decrypted_message.decode()
 
private_key, public_key = generate_rsa_key_pair()
message = "Hello, world!"
 
encrypted_message = encrypt_string_rsa(message, public_key)
decrypted_message = decrypt_string_rsa(encrypted_message, private_key)
 
print("Encrypted message:", encrypted_message)
print("Decrypted message:", decrypted_message)
```

使用自定义的加密算法。比如通过位移、异或、替换等操作来加密解密字符串。示例代码如下：
# 使用位移操作加密解密字符串
```
def encrypt_string_shift(message, shift):
    encrypted_message = ""
    for char in message:
        encrypted_char = chr((ord(char) + shift) % 256)
        encrypted_message += encrypted_char
    return encrypted_message
 
def decrypt_string_shift(encrypted_message, shift):
    decrypted_message = ""
    for char in encrypted_message:
        decrypted_char = chr((ord(char) - shift) % 256)
        decrypted_message += decrypted_char
    return decrypted_message
 
message = "Hello, world!"
shift = 3
 
encrypted_message = encrypt_string_shift(message, shift)
decrypted_message = decrypt_string_shift(encrypted_message, shift)
 
print("Encrypted message:", encrypted_message)
print("Decrypted message:", decrypted_message)
```

```
# 使用异或操作加密解密字符串
def encrypt_string_xor(message, key):
    encrypted_message = ""
    for i, char in enumerate(message):
        encrypted_char = chr(ord(char) ^ ord(key[i % len(key)]))
        encrypted_message += encrypted_char
    return encrypted_message
 
def decrypt_string_xor(encrypted_message, key):
    decrypted_message = ""
    for i, char in enumerate(encrypted_message):
        decrypted_char = chr(ord(char) ^ ord(key[i % len(key)]))
        decrypted_message += decrypted_char
    return decrypted_message
 
message = "Hello, world!"
key = "key"
 
encrypted_message = encrypt_string_xor(message, key)
decrypted_message = decrypt_string_xor(encrypted_message, key)
 
print("Encrypted message:", encrypted_message)
print("Decrypted message:", decrypted_message)
```

```
# 使用替换操作加密解密字符串
def generate_caesar_cipher_mapping(shift):
    mapping = {}
    for i in range(256):
        mapping[chr(i)] = chr((i + shift) % 256)
    return mapping
 
def encrypt_string_caesar(message, shift):
    mapping = generate_caesar_cipher_mapping(shift)
    encrypted_message = ""
    for char in message:
        encrypted_char = mapping[char]
        encrypted_message += encrypted_char
    return encrypted_message
 
def decrypt_string_caesar(encrypted_message, shift):
    mapping = generate_caesar_cipher_mapping(shift)
    decrypted_message = ""
    for char in encrypted_message:
        decrypted_char = mapping[char]
        decrypted_message += decrypted_char
    return decrypted_message
 
message = "Hello, world!"
shift = 3
 
encrypted_message = encrypt_string_caesar(message, shift)
decrypted_message = decrypt_string_caesar(encrypted_message, shift)
 
print("Encrypted message:", encrypted_message)
print("Decrypted message:", decrypted_message)
```
