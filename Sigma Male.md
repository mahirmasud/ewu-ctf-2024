
# Sigma Male 

Run the code then you will get a checker flag...put it in flag checker to get the flag

```python
import re

# Given encrypted message and parameters
encrypted_message = [1112, 666, 667, 1222, 554, 446, 106, 1222, 1110, 446, 106, 1112, 1333, 1222, 555, 780, 1222, 1113, 446, 447, 447, 1222, 1112, 446, 1220, 1222, 777, 887, 0, 999, 334, 334]
b = 557
possible_c_values = range(3, 1338)  # c is between 3 and 1337

# Common English words to check for in decrypted text
common_words = ["to", "and", "that", "you", "with", "for", "this", "NRF", "be", "to"]

# Function to decrypt using a specific value of c
def decrypt_message(encrypted_message, b, c):
    decrypted_message = ""
    for value in encrypted_message:
        try:
            # Reverse the encryption formula and obtain the ASCII code
            char_code = ((value + c) * pow(b, -1, 1337)) % 1337
            if 32 <= char_code <= 126:  # Printable ASCII range
                decrypted_message += chr(char_code)
            else:
                return None  # Skip non-printable results
        except ValueError:
            return None  # If modular inverse fails, skip this c
    return decrypted_message

# Brute-force over possible values of c, searching for common words
for c in possible_c_values:
    result = decrypt_message(encrypted_message, b, c)
    if result:
        # Check for the presence of common English words in the decrypted result
        if any(word in result for word in common_words):
            print(f"Decrypted message with c={c}: {result}")
            break
else:
    print("No valid decryption found.")
```


