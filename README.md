# [InstaZoom](https://instazoom.org) - Instagram photo and Video Downloader

I wrote this class mainly for my [online Instagram photo, video and IGTV downloader] [1], but I thought share this piece for your own extensions.

  - Validates Instagram URL (domain validation, URL path validation).
  - Uses OG properties to detect the image and video URL.
  - Supports Instagram photos, videos, and Instagram TV videos
  - Verbose error reporting with proper exceptions.
  - Full unit tests
  - No dependencies other than PHP curl extension (which is most likely enabled by already)
  

### Requirements
* PHP 7.2
* Curl


### Thanks to:
* [MetaData][2] - Meta data parsing regex and curl class.

### Installation

**With composer**
Install the library by running the following in your project. 
```bash
composer require jessiebecker9/InstaZoom
```
**Without composer**
Download the zip file from Github, and configure your autoload handler to autoload PSR-4 `jessiebecker9/InstaZoom` namespace from the downloaded contents `src` directory. 

You could also manually require the file. Requires a certain amount of guilty feeling because it's 2017 and you are not using a decent autoload mechanism. 

```php 
require_once 'src/InstaZoom.php'
```

### Usage
```php
<?php
use jessiebecker9\InstaZoom\InstagramDownload;
$url = 'http://instagram.com/p/tmwAlCGygb/';

try {
  $client = new InstagramDownload($url);
  $url = $client->getDownloadUrl(); // Returns the download URL.
  $type = $client->getType(); // Returns "image" or "video" depending on the media type.
}
catch (\InvalidArgumentException $exception) {
  /*
   * \InvalidArgumentException exceptions will be thrown if there is a validation 
   * error in the URL. You might want to break the code flow and report the error 
   * to your form handler at this point.
   */
  $error = $exception->getMessage();
}
catch (\RuntimeException $exception) {
  /*
   * \RuntimeException exceptions will be thrown if the URL could not be 
   * fetched, parsed, or a media could not be extracted from the URL. 
   */
  $error = $exception->getMessage();
}
```


[1]:https://instazoom.org
[2]:https://github.com/baj84/MetaData
