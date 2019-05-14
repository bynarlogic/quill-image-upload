# Quill ImageUpload Module

A module for Quill rich text editor to upload images to be selected from toolbar editor. This is a fork of [https://github.com/fxmontigny/quill-image-upload] and supports AWS S3 integration. Image files are saved to <your-s3-bucket>/quill-images. 

## Usage

### Webpack/ES6

```javascript
import Quill from 'quill';
import { ImageUpload } from 'quill-image-upload';

Quill.register('modules/imageUpload', ImageUpload);

const quill = new Quill(editor, {
	// ...
	modules: {
		// ...
		imageUpload: {
			url: '', // server url. If the url is empty then the base64 returns
			method: 'POST', // change query method, default 'POST'
			name: 'file', // custom form name
			withCredentials: false, // withCredentials
			headers: {}, // add custom headers, example { token: 'your-token'}
			csrf: { token: 'token', hash: '' }, // add custom CSRF
			customUploader: () => {}, // add custom uploader
			// personalize successful callback and call next function to insert new url to the editor
			callbackOK: (serverResponse, next) => {
				next(serverResponse);
			},
			// personalize failed callback
			callbackKO: serverError => {
				alert(serverError);
			},
			// optional
			// add callback when a image have been chosen
			checkBeforeSend: (file, next) => {
				console.log(file);
				next(file); // go back to component and send to the server
			}
		}
	}
});
```

### Script Tag

Copy image-upload.min.js into your web root or include from node_modules

```html
<script src="/node_modules/quill-image-upload/image-upload.min.js"></script>
```

```javascript
var quill = new Quill(editor, {
	// ...
	modules: {
		// ...
		imageUpload: {
			url: '', // server url. If the url is empty then the base64 returns
			method: 'POST', // change query method, default 'POST'
			name: 'image', // custom form name
			withCredentials: false, // withCredentials
			headers: {}, // add custom headers, example { token: 'your-token'}
			// personalize successful callback and call next function to insert new url to the editor
			callbackOK: (serverResponse, next) => {
				next(serverResponse);
			},
			// personalize failed callback
			callbackKO: serverError => {
				alert(serverError);
			}
		}
	}
});
```
