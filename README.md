# [Threema Gateway](http://gateway.threema.ch/) PHP Java

Version: [1.1.3](https://github.com/simmac/threema-msgapi-sdk-java/releases/tag/v1.1.3)

An automatically created documentation of this SDK can be found [here](http://simmac.github.io/threema-msgapi-sdk-java/).

## Notes about this version
This is a fork of the [original repo](https://github.com/threema-ch/threema-msgapi-sdk-java) after it was announced that it is no longer maintained by Threema.
As this is the community version of the Threema Gateway Java SDK it may contain additional changes compared to the official one downloadable from the Threema website. If you are looking for an exact mirror of the downloadable Threema version you can switch to the branch [`official`](https://github.com/simmac/threema-msgapi-sdk-java/tree/official).  

The contributors of this repositoriy are not affiliated with Threema or the Threema GmbH.

## Installation
NOTE: This instructions are copied from [https://gateway.threema.ch/en/developer/howto/create-keys/java](https://gateway.threema.ch/en/developer/howto/create-keys/java).

### Install Java:
If you don't have a Java runtime installed yet, go to [java.com](https://java.com) to download one for your platform.

### Download and unzip the Java API tool:
You can either download the [precompiled .jar file](https://github.com/simmac/threema-msgapi-sdk-java/releases/download/v1.1.3/threema-msgapi-tool.jar) or clone the repository and build the tool on your own

### Generate a keypair by running the tool
Open a shell (on Windows open the command line) and go to the directory where you have extracted the ZIP.
Create a new private and public key by typing the following command:
`java -jar threema-msgapi-tool.jar -g privateKey.txt  publicKey.txt`
A new key pair will be generated. The private key will be saved in privateKey.txt and the public key in publicKey.txt. Both keys are formatted in hexadecimal with a prefix that indicates the key type.
**IMPORTANT: Create a backup (or preferrably multiple backups) of your private key! If you lose it, your custom Threema ID will be unusable. We have no way to recover lost private keys for you, and it is also not possible to assign a new key to an existing ID.**

### Request custom Threema ID and submit key
Log in to your profile on the Threema Gateway website, click on "ID" in the navigation bar and then "Request Threema ID".
Choose End-to-End mode, enter the desired ID, and copy & paste the **public key** from the publicKey.txt file.

### Wait for review 
Wait until your custom Threema ID has been reviewed and accepted. As this is a manual process, it may take several days.

When your ID has been accepted, you will receive an API secret for authentication with the service.

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

## Contributing
Nice to see you want to contribute. We may periodically send patches to Threema to make it possible for them to implement them in the official SDK version.  

## Other platforms (PHP and Python):
All repositories are no longer maintained by the Threema GmbH. However, the community has forked the repositories for every platform where they are maintained unofficially.

You can find the PHP repository [here](https://github.com/rugk/threema-msgapi-sdk-php)

and the Python repository [here](https://github.com/lgrahl/threema-msgapi-sdk-python)
