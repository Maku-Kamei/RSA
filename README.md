from sympy import mod_inverse

def generate_keypair(p, q):
    n = p * q
    phi = (p - 1) * (q - 1)
    e = 65537  # Commonly used public exponent
    d = mod_inverse(e, phi)
    return ((e, n), (d, n))

def encrypt(public_key, plaintext):
    e, n = public_key
    cipher = [pow(ord(char), e, n) for char in plaintext]
    return cipher

def decrypt(private_key, ciphertext):
    d, n = private_key
    plain = [chr(pow(char, d, n)) for char in ciphertext]
    return ''.join(plain)

if __name__ == "__main__":
    p = int(input("Enter prime number p: "))
    q = int(input("Enter prime number q: "))
    
    public_key, private_key = generate_keypair(p, q)
    
    message = input("Enter message to encrypt: ")
    encrypted_message = encrypt(public_key, message)
    print("Encrypted message:", encrypted_message)
    
    decrypted_message = decrypt(private_key, encrypted_message)
    print("Decrypted message:", decrypted_message)
