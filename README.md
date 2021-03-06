# android-picture-form-example
This is example to build form with picture in Android app. This app was wrote in Kotlin. Follow these topic to build form using Kotlin.

## Introduce to App

![](https://lh4.googleusercontent.com/a-K0Dxl54Hjar0l3lXxBkSvKAqKvcUdAHChYWCYAOOGMnj9WD4_6CH1Hl87jeQfi-xe8QsjaGBy8IEo=w1440-h721-rw)

Pic.1 Before input

![](https://lh4.googleusercontent.com/RlXL1KQGNyDU7kftj9U42X0Nn8R4i2PasQ68zotAw5BPpGqT6nk52XDSdrNAMXlVh4iN6ALRbc2MwOs=w1440-h721-rw)

Pic.2 After input

The form app look like pictures as above. You can add picture and insert some information as you need to do.

## Knowledge of This App
1. Build UI with `xml` with these components: text field, radio buttons, button, and image.
1. Binding data in Kotlin way, without `findViewById`
1. Choose image from gallery and manage image data
1. Save data using `SharePreference`
1. Permission request on runtime (for Android March Mellow and upper version)

## Configure Kotlin
You have to follow the step as links below
* [Getting started with Android and Kotlin](https://kotlinlang.org/docs/tutorials/kotlin-android.html) - for config Kotlin at create project.
* [Kotlin Android Extensions](https://kotlinlang.org/docs/tutorials/android-plugin.html) - for avoid using `findViewById`
If you succeed to config Kotlin, let get start!

## Sanity Check
Make sure that you have `MainActivity.kt` and `activity_main.xml`. Your `MainActicity.kt` should have this:

```
class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
    }
}
```

".xml file is still the same, since Kotlin have no effect with them.

## Building UI
This app use few widget to build the form. You need to write the code in `activity_main.xml`. There are the component to build the app. All widgets have been styled for example: `textColor`, `textSize`, `textStyle` etc.

### Topic
The topic using `TextView`, the code shoud be like this.

```
<TextView
    android:id="@+id/topic" 
    android:layout_width="wrap_content" 
    android:layout_height="wrap_content" 
    android:text="Click the droid to add a picture" 
    android:textColor="@color/colorPrimary" 
    android:textSize="18sp" 
    android:textStyle="bold" />
```

### Image
Preview image in the form. This component using `ImageView`, this widget should be added the layout width and height. Here the code below

```
<ImageView
    android:id="@+id/image"
    android:layout_width="200dp"         
    android:layout_height="200dp"         
    android:src="@mipmap/ic_launcher" />
```
In this code, width and height were set to 200 dp. You can add any number as you need. The image that set in the code is image that already exist at project created time. This image has been set as default image. You can use any picture, but it must add to project if it doesn't exist in the project. follow [this](http://stackoverflow.com/questions/29047902/how-to-add-an-image-to-the-drawable-folder-in-android-studio) step

### Choice Option
The component allow user choose the genre of image content, which provide the choice to user. This component using `RadioGroup` and `RadioBotton` widget. Here the code below
```
<RadioGroup 
    android:layout_width="match_parent" 
    android:layout_height="wrap_content" 
    android:orientation="horizontal">  
    
    <RadioButton 
        android:id="@+id/people_check" 
        android:layout_width="wrap_content" 
        android:layout_height="wrap_content" 
        android:checked="true" 
        android:text="People" 
        android:textColor="@color/colorPrimary" />  
    
    <RadioButton 
        android:id="@+id/animal_check" 
        android:layout_width="wrap_content" 
        android:layout_height="wrap_content" 
        android:text="Animal" 
        android:textColor="@color/colorPrimary" />
        
    <RadioButton 
        android:id="@+id/object_check" 
        android:layout_width="wrap_content" 
        android:layout_height="wrap_content" 
        android:text="Object" 
        android:textColor="@color/colorPrimary" />  
        
    <RadioButton 
        android:id="@+id/place_check" 
        android:layout_width="wrap_content" 
        android:layout_height="wrap_content" 
        android:text="Place" 
        android:textColor="@color/colorPrimary" />  
    
    <RadioButton 
        android:id="@+id/other_check" 
        android:layout_width="wrap_content" 
        android:layout_height="wrap_content" 
        android:textColor="@color/colorPrimary" />  
        
 </RadioGroup>
```

what you need to do when build the radio button
1. Make sure that `RadioButton` is child of `RadioGroup` immediately.
2. All of `RadioButton` have been set the `id`. If id doesn't be assigned, radio buttons can be check at the same time (actually radio buttons used for option choice, there is only one option that can be check.
3. Assign `orientation` of `RadioGroup`. In this case, orientation has been set to "horizontal".

### Optional Text Edit Field
The `EditText` has been add as the child of `RadioGroup` to align it like to text of radio button. This widget allow user to choose other choice that not in the option. The code as below

```
<RadioGroup 
    android:layout_width="match_parent" 
    android:layout_height="wrap_content" 
    android:orientation="horizontal">  
    
    ...
    
    <EditText 
        android:id="@+id/other_text" 
        android:layout_width="match_parent" 
        android:layout_height="wrap_content" />  

</RadioGroup
```

### Caption
This field allow user add image caption to make more informative using `TextView` and `EditText` together. The code look like this

```
<LinearLayout 
    android:layout_width="match_parent" 
    android:layout_height="wrap_content">  
    
    <TextView 
        android:layout_width="wrap_content" 
        android:layout_height="wrap_content" 
        android:text="Caption: " 
        android:textColor="@color/colorPrimary" />  
        
    <EditText 
        android:id="@+id/caption" 
        android:layout_width="match_parent" 
        android:layout_height="wrap_content" />  
        
</LinearLayout>
```

As you can see, `TextView` and `EditText` are stay together as the child of `LinearLayout`. This layout has been align when ancestor that is `LinearLayout` of this `LinearLayout`'s orientation are different. In this case, the ancestor layout orientation has been set to "vertical". If no assgin orientation, it will be set to "horizontal" set a default. Moreover, width of `TextView` and `EditText` are different, because edit text field have to span to the right.

### Reset Button
To clear the data in this form, this button has been added using `Button` widget as code below
```
<Button 
    android:id="@+id/reset" 
    android:layout_width="wrap_content" 
    android:layout_height="wrap_content" 
    android:text="Reset" />
```

### Miscellaneous
Add some text to tell some information to user

```
<TextView 
    android:layout_width="wrap_content" 
    android:layout_height="wrap_content" 
    android:text="This form have auto-save when quit this application." 
    android:textColor="@color/colorPrimary" 
    android:textSize="12sp" />
```

## Input Image to Form
Other widget basically input using text, but the image need to build a stuff to control this process. This app allow user import picture when touch the image view.

### Make Image Clickable
- You need to add image view can be trigger via click. Therefore, add `android:clickable="true"` to `ImageView`.
- set when image view has been click using this code

```
image.setOnClickListener {}
```

which `image` is `id` of this `ImageView`. This code abandon `findViewById`, so you can use `ImageView` instance immediately. 

### Choose Image from Gallery
declair the function that open gallery
```
fun insertPictureFormGallery(view: View) {
    val galleryIntent = Intent(Intent.ACTION_PICK, MediaStore.Images.Media.EXTERNAL_CONTENT_URI)
    intent.putExtra("picture_id", view.id)
    startActivityForResult(galleryIntent, 1)
}
```
This function will be called when image view is clicked.
```
image.setOnClickListener {
    insertPictureFormGallery(image)
}
```
, which `image` is `ImageView`.

`putExtra` method use for passing any value to next step, in this case is `onActivityResult`. This code pass `id` of view to process in the next step.

### After Choose Image
```
override fun onActivityResult(requestCode: Int, resultCode: Int, data: Intent?) {
    if (requestCode == 1 && resultCode == Activity.RESULT_OK && data != null) {
        val selectedImageUri: Uri = data.data
        val view_id: Int = intent.getIntExtra("picture_id", 0)
        if (image.id == view_id) {
            image.setImageURI(selectedImageUri)
            topic.text = "Click the picture to change a picture"
        }
            
        imageUriString = selectedImageUri.toString()
    }
}
```
`getIntExtra` method is used for get value from previous step. In this code, the `if` statement to make sure that image view that pass from `onClick` is the same with image view that preview the chosen image. If you have only one image view, you can deprecate this statement. However, many image views should have this statement.In the statement, set image view as image chosen using Uri, like path to image, use `setImageaUri`method, and change the topic to explain user. Finally, collect `imageUriString`as string to class variable, which has been despair at the top of the activity class.

```
class MainActivity : AppCompatActivity() {
var imageUriString = ""

...

}
```
## Saving Data
This app using `SharePreference` to save the form data. `SharePreference`save data using key and value, which appropriate to save simple data. First, you need to declare class variable: `var :SharePreference? = null`. If you set value our variable as null, you need to declare a type of this value our variable followed by `?`. This class variable used for access from any where in this class.

### Assign Value
In `onCreate` method, assign `sharedPref` value like this

```
override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    setContentView(R.layout.activity_main)

    sharedPref = this.getPreferences(Context.MODE_PRIVATE)
}
```
then assign data into each fields using this method

```
private fun getData() {
    // for API 23 and upper: check permission at runtime
    checkPermission()

    val savedImage = sharedPref!!.getString("image", imageUriString)
    val savedGenre = sharedPref!!.getString("genre", getGenre())
    val savedCaption = sharedPref!!.getString("caption", caption.text.toString())

    image.setImageURI(Uri.parse(savedImage))
    imageUriString = savedImage
    topic.text = "Click the picture to change a picture"
    when (savedGenre) {
        people_check.text -> people_check.isChecked = true
        animal_check.text -> animal_check.isChecked = true
        object_check.text -> object_check.isChecked = true
        place_check.text -> place_check.isChecked = true
        else -> {
            other_check.isChecked = true
            other_text.setText(savedGenre)
        }
    }
    caption.setText(savedCaption)
}
```

At first, method `checkPermission` will be talk later, Let consider obtaining data part. call `sharedPref` with `!!` behind to let program throw `NullPointerExeption` when `sharePref` is null while compile. You can use `?`, [Elvis operator](https://kotlinlang.org/docs/reference/null-safety.html#elvis-operator), that equivalent to `if (sharePref != null) {...}`.

`Uri.parse(<String>)`, this statement convert string to uri then assign to image view

## Runtime Permission (for API v23 and upper)

To implement runtime permission, use this code.
```
private fun checkPermission() {
    // arbitrary integer value
    val REQUEST_CODE_ASK_PERMISSIONS = 1

    val permissionCheck = ContextCompat.checkSelfPermission(this,
            Manifest.permission.READ_EXTERNAL_STORAGE)

    if (permissionCheck != PackageManager.PERMISSION_GRANTED) {
        ActivityCompat.requestPermissions(this, arrayOf(Manifest.permission.READ_EXTERNAL_STORAGE), REQUEST_CODE_ASK_PERMISSIONS)
    }
}
```
, which `REQUEST_CODE_ASK_PERMISSIONS` can be any integer. At first, check the permission, if the app doesn't acquired the permission, which checked with `PackageManager.PERMISSION_GRANTED`, request permission using following code in if statement.

By the way, don't forget to add permission in "AndroidManifest.xml"

```
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
```

## ------------------
