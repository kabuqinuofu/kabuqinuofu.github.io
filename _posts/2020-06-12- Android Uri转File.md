---
layout: post
title: "Android Uri转File"
date: 2020-06-12 
description: "Uri转File"
tag: Android 
---   

```
    private File uri2File(Uri uri) {
        String imgPath;
        String[] arr = {MediaStore.Images.Media.DATA};
        Cursor cursor = getContentResolver().query(uri, arr, null, null, null);
        if (cursor == null) {
            imgPath = uri.getPath();
        } else {
            int img_index = cursor.getColumnIndexOrThrow(MediaStore.Images.Media.DATA);
            cursor.moveToFirst();
            imgPath = cursor.getString(img_index);
            cursor.close();
        }
        return new File(imgPath);
    }
```

