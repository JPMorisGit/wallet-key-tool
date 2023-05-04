# wallet-key-tool

![image](https://user-images.githubusercontent.com/82718999/236110434-1aa38980-245e-45a0-8ae4-31c3f4e6d77a.png)

![image](https://user-images.githubusercontent.com/82718999/236110447-f62cd45c-b804-4be0-aaa2-70c85e0bb178.png)

Comfortable GUI application to edit the contents of various
Bitcoin wallet files, add or remove keys, read one format and
export to another, move keys between different wallets, etc.

## how to build from source

* have JDK 7 installed (6 will not work)
* clone this repository
* in the root directory execute: <pre>./gradlew assemble</pre>

you will find the runnable .jar file in build/libs/

## I'm too lazy to build it myself, where is the jar?

See the [releases](https://github.com/prof7bit/wallet-key-tool/releases)
section and look for the "wallet-key-tool.jar" file, download and
run it as described below.

This release version might be a bit behind the latest
master branch, so I recommend you get the source and
build it yourself, its really not that complicated, the
gradle build system does a wonderful job of automating
it all, you don't even need gradle to be installed, it
will download it for you.


## how to run

On Windows you probably just need to double-click the jar file
and it will start (If you have Java installed).

On systems where there is a command line interface (this also
works on Windows, its just a bit harder to find there, they
really seem to hate their own users) you can also run it by
executing the following command:

    java -jar wallet-key-tool.jar

This will open a GUI window with which you can interact, info
and error messages will be printed to stderr. If you want to
increase the log level then run it like this:

    java -Dorg.slf4j.simpleLogger.defaultLogLevel=TRACE -jar wallet-key-tool.jar

Note: the -D option must come before the -jar option, it is
passed directly to java. Allowable log levels are:
ERROR, WARN, INFO, DEBUG, TRACE, the default is INFO,
if you want to see stack traces then use TRACE.

If you just want to dump the contents of a wallet to the
console with no GUI interaction then you can pass it a file
name, if you do this then it will not attempt to open any
graphical user interface, it will just dump the wallet contents
to stdout and exit. Note that the format of the dump is still
subject to change, keep this in mind when writing a parser
for it.

    java -jar wallet-key-tool.jar <filename>

This will prompt for a password on stdin if the file is
encrypted. If you want to avoid the password prompt you can
supply a password with the --password="my pass phrase" switch
(you need the quotes if it contains spaces). Beware that this
is dangerous since it might leave the password in your shell
history or make it visible in the process list, use it only
if you know what you are doing.

Example session in the console (I did not enter a passphrase,
I just pressed enter, so no private keys were decrypted):

    java -jar build/libs/wallet-key-tool.jar /home/bernd/Schotter/Schotter.wallet
    [main] INFO org.multibit.store.MultiBitWalletProtobufSerializer - Loading wallet extension org.multibit.walletProtect.2
    Wallet is encrypted. Enter passphrase:
    no passphrase entered, will skip decryption
    1QKm5sWXuFJ6Zrvqw7NR7gYXyipPSqfv4n KEY DECRYPTION SKIPPED
    1DrL3o6ZMAGttc96SPxqTo2yooq52P62kf KEY DECRYPTION SKIPPED
    1E79vvzr1KkHXVXNUBwqoW7XDsMYULVqrq KEY DECRYPTION SKIPPED
    [...]


## How to import project in Eclipse

* have the gradle plugin installed in Eclipse
* have the Xtend plugin installed in Eclipse
* import -> gradle -> gradle project
* [browse] select the root folder of this project
* [build model] and wait a few seconds
* [select all] the project should be in the list, make sure its selected
* [finish] and wait another few seconds until import is complete

## How to buy me a beer

If you are feeling generous you could send some change to 13MAejQp1193VPdUFexTh6vxD7DuzBVRJW

## Changes

- v1.4.2 
bugfix: parsing of blockchain.info version 2 format

- v1.4.1
Bug fix:

fix missing context menu on Windows
Enhancement:

file dialog with option to show hidden files
quick buttons for important folders like %APPDATA% on Windows or ~/Library/Application Support/ on Mac.
For the convenience of Windows user from now on there will also be an .exe version in case your Java installation is not configured to run .jar files on double-click. They are optional, you can either use the .jar version if it works or the .exe version if .jar does not work, you don't need both. They are absolutely identical in functionality, the only difference is they have an .exe starter (built with launch4j).

sha256sum wallet-key-tool.jar
2b5dbda86b8ea5ae05010ad598767fe1e0753b08efd3fa3c6629f49b053c350a wallet-key-tool.jar

sha256sum wallet-key-tool.exe
63753320482ad15927ef13ba66b37d72c0adf2658fb1a8f2317d6394afaf7382 wallet-key-tool.exe

Assets 4

- v1.4.0

adds the ability to import wallet.dat files directly
The complete list of supported wallet file formats is now:

import
Multibit *.wallet
Multibit *.key
Blockchain.info *.aes.json
Bitcoin-core "dumpwallet" file
Bitcoin-core wallet.dat
(untested: Schildbach backup)
export
Multibit *.wallet
Multibit *.key
Bitcoin-core "dumpwallet" file
(untested: Schildbach backup)
