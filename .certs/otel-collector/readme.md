# Regenerate ssl
```bash
# 1. Generate the certificate with Subject Alternative Names (SANs):
openssl req -x509 -nodes -days 9999 -newkey rsa:2048 -keyout otel-collector.key -out otel-collector.crt -config otel-collector.conf -extensions v3_req

# 2. Install to system trust store (Linux):
sudo cp ./otel-collector.crt /usr/local/share/ca-certificates/otel-collector.crt
sudo update-ca-certificates

# 3. Install to Chrome's certificate database (NSS):
sudo apt update && sudo apt install -y libnss3-tools
certutil -d sql:$HOME/.pki/nssdb -A -t "CP,CP," -n "otel-collector" -i ./otel-collector.crt

# 4. Verify it was added:
certutil -d sql:$HOME/.pki/nssdb -L | grep otel-collector

# 5. Optionally convert to a pfx
openssl pkcs12 -export -out otel-collector.pfx -inkey otel-collector.key -in otel-collector.crt -passout pass:password

# 6. Make sure everythings readable by all users
chmod 644 ./otel-collector.crt
chmod 644 ./otel-collector.key
chmod 644 ./otel-collector.pfx
```