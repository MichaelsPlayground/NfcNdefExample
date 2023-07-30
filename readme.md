# NFC NDEF example

This is a sample app that shows how to read from and write to a NDEF formatted NFC tag. I tested it 
NTAG216 tags and it works properly when using tags with factory settings.

A NDEF formatted tag ("NFC Data Exchange Format") does need two separate files:
1 a Container file (""CC") that is selected by a NFC reader that holds a link to the
2 data file where all data are stored.

## Why should I use NDEF ?

As NDEF is a standard you exchange data from the tag to an Android and iOS based smartphone. It sounds  
a little bit unusual but Apple decided that NDEF data transfer is the only allowed data exchange format 
available on their devices (except "Apple Pay" but this is a closed shop and available to Apple only).

## What kind of data can be exchanged using NDEF ?

A NDEF formatted tag (or better the file on it) should contain (ASCII-) text based data only as the typical reader
(Android/iOS smartphone) won't view data.

There are several "well known formatted" data and this sample is prepared to work with some of them (**writer side**):
- the easiest type is the **Text** NDEF message that is shown on reading (e.g. a simple adress)
- the most used type is the **URI (or URL)** type, meaning you can store a link to a website on it. When the 
tag is read by the NDF reader the smartphone usually opens a browser and displays the  website
- another popular type is the **Telefone number** type - here the smartphone will try to start a phone call
- nowadays another popular type are the  **Coordinates** encoded on the tag. This is very similiar to a link to the 
"Google Maps" website or similar but when using coordinates the smartphone tries to open an app that works with them like 
Goople Maps (if installed on the  smartphone)
- A special type is a **Streetview** coordinate - this will not show a map but a "street view image"
- Using an **Address** type will open the contact app and try to save the new entry
- Storing an **Email address** will force to open the standard email app on the smartphone and send an email 
to the stored address
- A rare used type is the **Application** type - this will force to open a specific app on the smartphone and - 
when the app is not installed on the device it opens the app store (e.g. "Google Playstore") and tries to download 
and install the app

All of these types are supported by the app and you test all of them. On some types you can add a timestamp string 
for easy testing.

On the **reader side** you tap the tag to the NFC reader and the message will pop up.

## Can I store more than one dataset on the NDEF tag ?

Let's analyze how the data is stored on the tag. All data is encapsulated in a **NDEF record** (think of a 
file in a directory). One or more of these records are stored in a **NDEF message** that is like a container. 
This makes it possible to store different data withing the same NDEF message (e.g. you can use a "Telephone 
number" record followed by an "address" record). The bad news are: only the first record will be shown when 
not using any specialised app but the regular phone. If you are using a dedicated app for a special purpose 
the user needs to install this app and opens it for reading.

My tip is: stay with one record only NDEF messages.

## What API is used for reading and writing ?

This app is using the **NFC Reader API** and not the intent based usage. This is because that kind of writing is 
more reliable and less faulty than all other connections. Just one restriction applies: the app needs to open and in 
the foreground to work (for reading and writing).

For that reason you need to very careful when the "write fragment" is active on the screen - data will be written 
before any further conformation.

A note on iOS compatibility: as I'm not owning an Apple phone I cannot test what will happen when a NDEF type is 
tapped to the phone, sorry.  

## Can I read and/or write protect my NDEF message ?

The answers are "no" and "yes", meaning: **you cannot (password) reading protect your NDEF message but you 
can protect the data against any altering (write protection).

Icons: https://www.freeiconspng.com/images/nfc-icon

Nfc Simple PNG Transparent Background: https://www.freeiconspng.com/img/20581

<a href="https://www.freeiconspng.com/img/20581">Nfc Png Simple</a>

Icon / Vector editor: https://editor.method.ac/

Minimum SDK is 21 (Android 5 / "Lollipop"), tested with SDK 33 (Android 13) on real devices.

