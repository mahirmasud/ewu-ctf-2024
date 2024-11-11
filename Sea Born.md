
# SEA Born 

Run the code then you will get the flag...

```python
from Crypto.Util.Padding import unpad
from Crypto.Cipher import AES
from Crypto.Util import Counter

class SEADecryptor:
    def __init__(self, block_size, num_msgs):
        self.KEYS = [b'\x00' * 24 for _ in range(num_msgs)]
        self.CTRs = [Counter.new(block_size) for _ in range(num_msgs)]

    def decrypt(self, i, ciphertext):
        cipher = AES.new(self.KEYS[i], AES.MODE_CTR, counter=self.CTRs[i])
        plaintext = cipher.decrypt(bytes.fromhex(ciphertext))
        try:
            return unpad(plaintext, 24).decode()
        except:
            return plaintext.decode()  # return as-is if padding isn't correct


# Define the encrypted ciphertexts from the output
ciphertexts = [
    "995bd7aa8427b16bc361bc8377234d41f1884a0f279990615e471024e8d19265595cb3800d469a02acccac0f4d5059aa9cc463e2ae9b600d8c4584079f214825ab7abd4bdb1f9d6a6bf93e6e3c437f73417b0364cbb3adb49b57a429c3c4b47428fcc657610b6e1d6210c7d3500eebc648ad25c2b9033597",
    "995bd7f9a253923dc560a58032324945f790410e2789913472415e37e5dc936e5e47b3920d159d0fb19bae4e485c1bac95cf7eb0ed916901925a9244833d0134a632b747d71ec86c63ee2c2b7254213c5c66186fc9b1e0f28657bf33cfceb410",
    "8361f4b8f3539e388040be8432185450f6c7501327b1922d043e665b9ca8ee18322c8bfe7a2df67fc6f4d537232123c0",
    "8361f4b8f308b678f35189c360085260f4a97b4d69afc92979792a73f3fea9574207e1833d5bde5781dc834a64750ab398f543aafc915d259f03d43bdb001565e76fb54eda3b9505",
    "985fc6e3aa12832ecc77fdd351036215fb88490c6284973575491030a4de99740a5bfd8a1b158b09b68da34c5e194fbd9ec279abae836e489b4e910198274822b77abc51c252896871e26721735d796e45760279c0f4f9b0d54cbb2086c3bc6466fbdc4f3d7113695f0cdbcf4c12f7da54b139dea51f298b"
]

# Decrypt each message
decryptor = SEADecryptor(block_size=128, num_msgs=len(ciphertexts))

# Display decrypted messages
for i, ct in enumerate(ciphertexts):
    decrypted_text = decryptor.decrypt(i, ct)
    print(f"Decrypted msg{i + 1}: {decrypted_text}")
```


