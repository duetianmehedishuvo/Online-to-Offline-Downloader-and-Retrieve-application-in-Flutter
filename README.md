
# Online to Offline Downloader and Retrieve application in Flutter

Download any file from url, save to phones local storage in android in flutter

## Getting Started

Added This Libary :

             path_provider: ^1.6.11
			 
			 
And added this Permission:

In Android:

	Android>App>src>main>AndroidManifest.xml

	<uses-permission android:name="android.permission.INTERNET"/>
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
    
And Method Here:
	
	Future<File> createFile() async {
    try {
      /// setting filename
      final filename = 'shuvo.png';

      /// getting application doc directory's path in dir variable
      String dir = (await getApplicationDocumentsDirectory()).path;

      /// if `filename` File exists in local system then return that file.
      /// This is the fastest among all.
      if (await File('$dir/$filename').exists()) return File('$dir/$filename');

      ///if file not present in local system then fetch it from server
      String url = 'https://pbs.twimg.com/profile_images/973421479508328449/sEeIJkXq.jpg';

      /// requesting http to get url
      var request = await HttpClient().getUrl(Uri.parse(url));

      /// closing request and getting response
      var response = await request.close();

      /// getting response data in bytes
      var bytes = await consolidateHttpClientResponseBytes(response);

      /// generating a local system file with name as 'filename' and path as '$dir/$filename'
      File file = new File('$dir/$filename');

      /// writing bytes data of response in the file.
      await file.writeAsBytes(bytes);

      /// returning file.
      return file;
    }

    /// on catching Exception return null
    catch (err) {
      print(err);
      return null;
    }
  }
  
This Methos Initialize in intstate ..Example is given  main.dart file   
