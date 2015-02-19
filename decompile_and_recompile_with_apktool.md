## How to decompile and recompile a Protocoder app with Apktool

_Note: This is a work in progress and it's only for experimental purposes._

1. Install [Apktool][1] (a tool for reverse engineering Android apk files). 
   To perform this step successfully, please follow the [installation guide][2] 
   provided in the official website.

2. To decompile your **.apk** file run this command:
   ```
   apktool d name_of_apk.apk
   ```

3. The above step will create a folder with all the decompiled resources.
   In this step you have to add the new files to the assets folder.  
   
  For example:
  
   ```
   cp -R assets folder_of_decoded_apk
   ```

4. Optionally, you can rename the application package name. Making this 
   step you could have several Protocoder apps installed on your device.

   For this task you only have to edit the `AndroidManifest.xml` file and 
   rename the value for the **package** attribute.

   For example:

   We can rename `package="org.protocoder"`


   ```
   <manifest xmlns:android="http://schemas.android.com/apk/res/android" 
     package="org.protocoder" 
     platformBuildVersionCode="21" 
     platformBuildVersionName="5.0.1-1624448">
   ```
 
   for this new value:


   ```
   <manifest xmlns:android="http://schemas.android.com/apk/res/android" 
     package="org.protocoder.mycustomapp" 
     platformBuildVersionCode="21" 
     platformBuildVersionName="5.0.1-1624448">
   ```

5. To recompile your new **.apk** run this command:
   ```
	apktool b folder_of_decoded_apk
   ```

   Once you have run this command your **.apk** will be stored inside of the 
   `dist` folder.


6. Sign the **.apk** file using the [jarsigner][3] tool.

   For example:

   ```
	jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore ~/.android/debug.keystore -storepass android -keypass android name_of_apk.apk androiddebugkey
   ```

7. At this point you have an awesome protocoder app ready to be installed on 
   your device! :)

[1]: https://code.google.com/p/android-apktool/
[2]: https://code.google.com/p/android-apktool/wiki/Install
[3]: http://docs.oracle.com/javase/7/docs/technotes/tools/windows/jarsigner.html
