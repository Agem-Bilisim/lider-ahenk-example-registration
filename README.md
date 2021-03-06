# lider-ahenk-example-registration

Lider Ahenk example registration bundle

## How to Build

Just run `mvn clean install -DskipTests`

## How to Run

> Make sure you have Lider running. See these documentation:  [\[1\]](https://github.com/Pardus-Kurumsal/lider/wiki/02.-Building-&-Running)

1. Type `bundle:install mvn:tr.org.liderahenk/example-registration/1.0.0-SNAPSHOT` on Karaf shell. This will add bundle to the Karaf instance.
2. Again on Karaf shell, run `bundle:start <BUNDLE_ID>` to run plugin bundle.
3. Finally, restart XMPP Client bundle via `bundle:restart <BUNDLE_ID>`.

## How to Use
Example Registration bundle implemented for Ahenk registration according to mac address with specific ou values. Thus entries of registered Ahenk are more meaningful listed in ldap tree.

1- Be sure about there is a configuration file, which name is tr.org.liderahenk.example.registration.cfg, under Lider etc file.</br></br>
2- tr.org.liderahenk.example.registration.cfg has two attributes; 
**file.protocol**: Possible values are http(read remote csv file via http), local(read csv file which is on Lider machine), inner(read csv file which is embedded in bundle)
**file.path** : If protocol was defined as http, path value must be valid url. If protocol is local, path value must be folder path whic contains csv files. ( This folder can be host inner folders. Bundle looks folders recursively)</br></br>
3-Example csv file:</br>
`
<mac_address>,<cn>,<ou>,<ou>,<ou>,<ou>,...
08:00:27:f0:13:13,Ahenk_1,Ankara,Cankaya,Bilkent,Cyberpark,Floor_4
08:00:27:f0:15:15,Ahenk_2,Ankara,Cankaya,Bilkent,Cyberpark,Floor_5
08:00:27:f0:15:15,Ahenk_3,Ankara,Cankaya,Bilkent,Tepe,Level_2
08:00:27:f0:14:14,Ahenk_4,Ankara,Cankaya,Hacettepe,CS,Floor_1
`
</br></br>
Be careful about cn values must be uniqe and ou values are ordered 
You don't have to create file with csv extension but file must has this format
</br></br>
There will be ldap tree after registration according to example csv file:</br>
|_Ankara</br>
-----|__Cankaya</br>
-----------|___Bilkent</br>
--------------------|___Cyberpark</br>
-----------------------------|____Floor_4</br>
--------------------------------------|*Ahenk_1*</br>
-----------------------------|____Floor_5</br>
--------------------------------------|*Ahenk_2*</br>
--------------------|___Tepe</br>
-----------------------------|____Level_2</br>
--------------------------------------|*Ahenk_3*</br>
------------|___Hacettepe</br>
--------------------|___CS</br>
-----------------------------|____Floor_1</br>
--------------------------------------|*Ahenk_4*</br>

For local protocol you can use multiple folder which contains csv files
records</br>
------|__Department1</br>
--------------|__Level1.csv</br>
--------------|__Level2.csv</br>
------|__Department2</br>
--------------|__Level1.csv</br></br>
tr.org.liderahenk.example.registration.cfg:</br></br>
**file.protocol**:local</br>
**file.path**:/home/lider/records</br>

