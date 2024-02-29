#!/bin/bash
# Encryption and Decryption Script

# Step 1: Generate data (you can replace this with your actual data)
echo "This is sensitive data." > data.txt

# Step 2: Generate a symmetric key (you can use AES, for example)
symmetric_key="mysecretkey"

# Step 3: Encrypt the data using the symmetric key
openssl enc -aes-256-cbc -salt -in data.txt -out data.txt.enc -k "$symmetric_key"

# Step 4: Generate a digital signature for the encrypted data
openssl dgst -sha256 -sign private_a.pem -out data.txt.sig data.txt.enc

# Step 5: Verify the digital signature (optional, for demonstration)
openssl dgst -sha256 -verify public_a.pem -signature data.txt.sig data.txt.enc

# Step 6: Decrypt the data using the symmetric key
openssl enc -d -aes-256-cbc -in data.txt.enc -out decrypted_data.txt -k "$symmetric_key"

# Display the decrypted data
cat decrypted_data.txt
