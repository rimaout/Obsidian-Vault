
## Downloading All Files From Google Photos

1.  Navigate to [Google Takeout](https://takeout.google.com/settings/takeout)
2.  Deselect all, and select the Photos archive
3.  Download and unzip your archive.

Each picture and video from Takeout will be accompanied by a metadata.json file containing all the EXIF data. Some pictures will even be stripped of their own EXIF data, usually Location and Date values, making the import process to another platform messy. We will need to merge the JSON and image file back together if we want to correctly import those images elsewhere.



## Fixing Image EXIF Data

1.  Install [https://exiftool.org/](https://exiftool.org/). This will allow us to read and write EXIF data, specifically from the JSON to the image/video.
2.  Open Terminal and use the below line in the codeblock. Replace "<DirToProcess\>" with your unzipped folder of images (in Mac OS, you can drag the folder in terminal and it will populate the path). The ExifTool will go through all subdirectories so **use the root folder’s path**

``` Terminal
exiftool -r -d %s -tagsfromfile "%d/%F.json" "-GPSAltitude<GeoDataAltitude" "-GPSLatitude<GeoDataLatitude" "-GPSLatitudeRef<GeoDataLatitude" "-GPSLongitude<GeoDataLongitude" "-GPSLongitudeRef<GeoDataLongitude" "-Keywords<Tags" "-Subject<Tags" "-Caption-Abstract<Description" "-ImageDescription<Description" "-DateTimeOriginal<PhotoTakenTimeTimestamp" -ext "\*" -overwrite\_original -progress --ext json _<DirToProcess>
```

This will copy all GPS location data, tags, captions, descriptions, dates and time taken information to ALL files (-ext "\*") within the specified directory, excluding JSON (--ext json). See notes below to limit the file types. **If you have pictures older than 1970, refer to** [**this comment**](https://legault.me/post/correctly-migrate-away-from-google-photos-to-icloud#comment-5150115544) **for a fix.**

### Notes

-   See all Google Takeout’s JSON file data and names [here](https://github.com/StarGeekSpaceNerd/Metadata_Reference/blob/master/Photos.google.com.md#user-content-google-takeout).
-   See all Exiftool options [here](https://exiftool.org/exiftool_pod.html).
-   You can change _\-ext "\*"_ to specific files types like _\-ext jpg_, or _\-ext mp4._
-   Note that this will overwrite all files in that directory so keep the original archive zip as a backup.

## Moving Library to iCloud

1.  Use Photos.app on Mac to upload your pictures. Make sure to use the **File > Import** instead of dragging everything in the app, it works much better for large libraries.
2.  Everything should import well. If there are some pictures that show up at the wrong date, manually correct them with **Image > Adjust Date and Time**.

## Taking Care of Your Existing Google Photos Library

1.  If you are keeping Google Photos as a secondary backup, there’s a couple of things to do. The Google Photos phone app will recognize all newly added pictures in your iCloud as new pictures and will start uploading them again as duplicates. I couldn’t find a way to prevent that so I let the Google Photos app upload the whole library again.
2.  Once all pictures are uploaded to Google Photos, navigate to [https://photos.google.com/search/\_tra\_](https://photos.google.com/search/_tra_) where pictures will be sorted by Upload Time. Select all newly added pictures and delete them. Google Photos will not reupload the deleted duplicates. It will continue uploading new pictures you take on your phone in the future as usual.