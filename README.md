<div align="center">

  # 🖼️ Media-Upload

  📷 **media-upload** is a vue package for multiple images upload with preview.

  🖼️ **media-upload** support **the create and the update form**, and it will handle the upload for you.

  ![media-upload - multiple image upload with preview ](/static/media-upload.gif)

</div>


# 👀 Demo

- [Fully featured demo](https://github.com/s1modev/media-upload-demo)
- [Full tutorial](https://dev.to/simodev/how-to-upload-multiple-images-with-preview-using-laravel-and-vue-282j)

![media-upload - multiple image upload with preview ](/static/media-upload.PNG)

# 💻 Install

via npm
```sh
npm install @s1modev/media-upload
```

or via yarn 
```sh
yarn add @s1modev/media-upload
```


# 🕹 Usage

```javascript
import { createApp } from 'vue';

import { UploadMedia, UpdateMedia } from '@s1modev/media-upload';

let app=createApp({})

app.component('upload-media' , UploadMedia);
app.component('update-media' , UpdateMedia);

app.mount("#app")
```

or

```javascript
import {UploadMedia, UpdateMedia} from "@s1modev/media-upload";
export default {
  components: {
    UploadMedia,
    UpdateMedia
  }
};
```


# 🔎 Example

This is an example in Laravel blade form.

## Create Form

```html
<div id="app">
  <upload-media 
    server="/api/upload"
    error="@error('media'){{$message}}@enderror">
  </upload-media>
</div>
```

## Update Form

```html
<div id="app">
  <update-media 
    server="/api/upload"
    media_file_path="/post_images"
    media_server="/api/media/{{$post->id}}" 
    error="@error('media'){{$message}}@enderror">
  </update-media>
</div>
```

# 📙 How does media-upload works?

**media-upload** contains two components `<upload-media />` for the create form and `<update-media />` for the update form!

## \<upload-media /> component

1. **media-upload** uploads the image `image.jpg` as multipart/form-data using a POST request.

2. **server** temporary saves the image with a unique name `123_image.jpg` in a `/tmp/uploads` file.

3. **server** returns the unique name `123_image.jpg` in a request response.

4. **media-upload** stores the unique name `123_image.jpg` in a hidden input field with `name="media[]"`.

5. **user** submits the media-upload parent form containing the hidden inputs fields the unique images names.

6. **server** uses the unique images names to move 123_image.jpg from the `/tmp/uploads` file to its final location.

## \<update-media /> component

- Almost the same concept as `<upload-media />` with some slight changes.


# 🔣 Inputs

## \<upload-media /> component:

Basically after the image get uploaded the server return the unique image name and **media-upload** stores it in a hidden input field `<input name="media[]">`

## \<update-media /> component:

- After the server returns the images names, **media-upload** lists them, and in case the user added an new image **media-upload** uploads the image `image.jpg` as multipart/form-data using a POST request and stores the added media unique name in an input `<input name="added_media[]">`

- In case the user deleted an image `123_image.jpg` **media-upload** stores it's name in an input field `<input name="deleted_media">`

- I case **media-upload** has at least one image or more listed you will notice that it has also an input field `<input name="media" value="1">`, this input is a way to validate the media as `required`, so if you want make media required in your form, you will only need to add on your backend validation `<input name="media" value="1">` as required `$request->media => 'required'`

# ⚙️ Props

## \<upload-media /> component

| Props | Type | Default | Description |
| --- | --- | --- | --- |
| **error** | String | - | If this prop is not null it will apply the error styling and show the error message. |
| **server** | String | /api/upload | The api that will temporary save the image. |

## \<update-media /> component

| Props | Type | Default | Description |
| --- | --- | --- | --- |
| **error** | String | - | If this prop is not null it will apply the error styling and show the error message. |
| **server** | String | /api/upload | The api that will temporary save the image. |
| **media_server** | String | - | The api that will return the saved images names. |
| **media_file_path** | String | /post_images | The file where the saved media are stored. |


# 💾 Emits

## \<upload-media /> component

| event | value | Description |
| --- | --- | --- |
| **@media** | array | Emit the added images. |

## \<update-media /> component

| event | value | Description |
| --- | --- | --- |
| **@saved_media** | array | Emit the saved images. |
| **@added_media** | array | Emit the added images. |
| **@deleted_media** | array | Emit the deleted images. |


# 🤝 Contributing

1. Fork this repository.
2. Create new branch with feature name.
3. Run `npm install` and `npm run dev`.
4. Create your feature.
5. Commit and set commit message with feature name.
6. Push your code to your fork repository.
7. Create pull request. 🙂


# ⭐️ Support

![media-upload - multiple image upload with preview ](/static/media-upload.PNG)

If you like this project, You can support me with starring ⭐ this repository.

# 📄 License

[MIT](LICENSE)

Developed with ❤️