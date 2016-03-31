# msgapi-sdk-java
Version: 1.1.3

## Console client usage
###Local operations (no network communication)
####Encrypt
	java -jar threema-msgapi-tool.jar -e <privateKey> <publicKey>
Encrypt standard input using the given sender private key and recipient public key. Prints two lines to standard output: first the nonce (hex), and then the box (hex).

####Decrypt
	java -jar threema-msgapi-tool.jar -d <privateKey> <publicKey> <nonce>
Decrypt standard input using the given recipient private key and sender public key. The nonce must be given on the command line, and the box (hex) on standard input. Prints the decrypted message to standard output.

####Hash Email Address
	java -jar threema-msgapi-tool.jar -h -e <email>
Hash an email address for identity lookup. Prints the hash in hex.

####Hash Phone Number
	java -jar threema-msgapi-tool.jar -h -p <phoneNo>
Hash a phone number for identity lookup. Prints the hash in hex.

####Generate Key Pair
	java -jar threema-msgapi-tool.jar -g <privateKeyFile> <publicKeyPath>
Generate a new key pair and write the private and public keys to the respective files (in hex).

####Derive Public Key
	java -jar threema-msgapi-tool.jar -p <privateKey>
Derive the public key that corresponds with the given private key.

###Network operations
####Send Simple Message
	java -jar threema-msgapi-tool.jar -s <to> <from> <secret>
Send a message from standard input with server-side encryption to the given ID. 'from' is the API identity and 'secret' is the API secret. Returns the message ID on success.

####Send End-to-End Encrypted Text Message
	java -jar threema-msgapi-tool.jar -S <to> <from> <secret> <privateKey>
Encrypt standard input and send the message to the given ID. 'from' is the API identity and 'secret' is the API secret. Prints the message ID on success.

####Send End-to-End Encrypted Image Message
	java -jar threema-msgapi-tool.jar -S -i <to> <from> <secret> <privateKey> <imageFilePath>
Encrypt standard input and send the message to the given ID. 'from' is the API identity and 'secret' is the API secret. Prints the message ID on success.

####Send End-to-End Encrypted File Message
	java -jar threema-msgapi-tool.jar -S -f <to> <from> <secret> <privateKey> <file> [thumbnail]
Encrypt the file (and thumbnail) and send a file message to the given ID. 'from' is the API identity and 'secret' is the API secret. Prints the message ID on success.

####ID Lookup By Email Address
	java -jar threema-msgapi-tool.jar -l -e <email> <from> <secret>
Lookup the ID linked to the given email address (will be hashed locally).

####ID Lookup By Phone Number
	java -jar threema-msgapi-tool.jar -l -p <phoneNo> <from> <secret>
Lookup the ID linked to the given phone number (will be hashed locally).

####Fetch Public Key
	java -jar threema-msgapi-tool.jar -l -k <id> <from> <secret>
Lookup the public key for the given ID.

####Fetch Capability
	java -jar threema-msgapi-tool.jar -c <id> <from> <secret>
Fetch the capability of a Threema ID

####Decrypt and download
	java -jar threema-msgapi-tool.jar -D <id> <from> <secret> <privateKey> <messageId> <nonce> [outputFolder]
Decrypt a box (box from the stdin) message and download (if the message is a image or file message) the file(s) to the defined directory

## Feature Levels

| Level | Text | Capabilities | Image | File | Credits |
|-------|------|--------------|-------|------|---------|
| 1     | X    |              |       |      |         |
| 2     | X    | X            | X     | X    |         |
| 3     | X    | X            | X     | X    | X       |

You can see the implemented feature level by invoking the following command:

```
$ java -jar threema-msgapi-tool.jar -v
```
