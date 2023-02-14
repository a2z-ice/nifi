# nifi
1. Create a new keystore using the Java keytool command:

```bash
keytool -genkey -alias mykey -keyalg RSA -keystore keystore.jks -storepass mypassword -keypass mypassword

```
2. This command creates a new JKS file named keystore.jks and generates a new RSA key pair with the alias mykey. You will be prompted to enter additional information, such as your name and organization.

Export the JKS file to a PKCS12 file:

```bash
keytool -importkeystore -srckeystore keystore.jks -destkeystore keystore.p12 -deststoretype PKCS12 -srcstorepass mypassword -deststorepass mypassword

```

3. This command exports the keystore.jks file to a PKCS12 file named keystore.p12. You will be prompted to enter the JKS password again.

Convert the PKCS12 file to a PEM file:
```bash
openssl pkcs12 -in keystore.p12 -out keystore.pem -nodes -password pass:mypassword

```

4. This command converts the keystore.p12 file to a PEM file named keystore.pem that contains the private key and certificate chain.

Encode the PEM file as base64:
```bash
base64 keystore.pem > keystore.b64

```

5. This command encodes the keystore.pem file as a base64-encoded string and saves it to a file named keystore.b64.

You can now use the contents of keystore.b64 as a secret in Kubernetes to provide SSL/TLS for NiFi. Note that you should also create a separate key file for the SSL/TLS key password and include it as a separate secret in Kubernetes.

---

# Duplicate

1. Create a new keystore using the Java keytool command and export it as a PKCS12 file:
```bash
keytool -genkey -alias mykey -keyalg RSA -keystore keystore.jks -storepass mypassword -keypass mypassword
keytool -importkeystore -srckeystore keystore.jks -destkeystore keystore.p12 -deststoretype PKCS12 -srcstorepass mypassword -deststorepass mypassword

```
2. Convert the PKCS12 file to a PEM file and encode it as base64:
```bash
openssl pkcs12 -in keystore.p12 -out keystore.pem -nodes -password pass:mypassword
base64 keystore.pem > keystore.b64

```
