# Lab Activity: Bundling and Pushing a Theme

**Prerequisites**

* Completed a customized theme, tested and are ready to deploy live

## Bundling

### Bundling a Customized Theme

You have verified all requirements have been met. Stencil CLI provides two options for creating a .zip file that contains all your theme's essentials while excluding redundant components.

**Note:**

**Writable Permissions Are Required**

Without these permissions, bundling your theme will fail, blocking its upload to BigCommerce.

**No Automatic Check for Dependencies**

The _stencil bundle_ and _stencil push_ commands do not check for the dependencies that these build systems install. So if those dependencies are missing, these commands will not immediately report errors. However, your resulting .zip file will not properly upload to BigCommerce, and will not run properly on a storefront.

**Verify Directory and File Permissions**

If you have added any new subdirectories or files to your base theme, verify that you have:

Set newly added directories to permission 755 (drwxr-xr-x). Set newly added files to permission 644 (rw-r--r--).

[Troubleshooting](https://docs.bigcommerce.com/developer/docs/storefront/stencil/deployment/upload-errors) theme uploads.
* [Shrink Your Theme by Excluding Static Asses (WebDAV)](https://support.bigcommerce.com/s/article/File-Access-WebDAV#manual)
* [Staging a Theme for CDN Delivery](https://support.bigcommerce.com/s/article/Optimizing-Your-Images?language=en_US#imageop-cdn)

### Bundling a Theme

**Bundle Only**

1. Enter the following command in CLI:


```bash showLineNumbers={false}
stencil bundle
```

2. The _bundle_ command will notify you of its progress and completion
3. A _.zip_ file is generated

Check the resulting .zip file's size. (It cannot exceed 50 MB). If your .zip file meets this requirement you are now ready to [upload your theme](https://docs.bigcommerce.com/developer/docs/storefront/stencil/deployment/upload).

If your .zip file exceeds 50 MB, you will need to use one of the following procedures to restructure your theme to a size that is manageable for upload to BigCommerce:

1. Shrink your theme with the help of WebDAV
2. Stage your Theme for CDN Delivery to restructure your theme to a size that's manageable to upload to BigCommerce. See [Checking a Theme's Size](https://docs.bigcommerce.com/developer/docs/storefront/stencil/deployment/performance-optimization) for more information

### Successful Bundling

![Successful Bundling](../images/bundle.png)

Stencil CLI will display:
* "ok" confirmations
* "not ok" errors
* warnings for individual substeps in bundling and uploading your theme
If bundling is successful, you will next see a "Processing" progress bar to track the upload.

**Note**

If bundling your theme triggers multiple lint errors related to the bundle.js file, then your theme is missing the .eslintignore file. Please retrieve this file from the Stencil Cornerstone repo, then re-run stencil bundle or stencil push.

## Pushing

### Upload a Theme

BigCommerce provides two alternatives for uploading a theme to your BigCommerce store.

1. Control Panel Upload
2. Command Line Upload

The Control Panel upload process was covered in the _Stencil Essentials_ course. This course will teach you how to upload a theme with the _stencil push_ command.

### Bundle and Push

1. Enter the following command in CLI:

```bash showLineNumbers={false}
stencil push
```

2. Enter **y** to apply the theme to your store
3. Select the theme variation you would like to apply
4. Navigate to the URL of the store to view the applied theme

**Command Line Upload (OAuth Required)** This stencil push command allows you to both bundle and upload your theme to the store with a single terminal command, and in one continuous process. The _stencil push_ command is available only for themes that you have successfully initialized using an **OAuth Token** (with _Themes: modify scope)._

Stencil CLI is designed to display the same notifications, prompts, and selection options that you would receive when using the control panel's GUI.

![Successful Upload](../images/Successful-Upload.jpg)

**Successful Upload**

Upon a successful upload, you will be prompted: _Would you like to apply your theme to your store at &lt;storehash&gt;? (y/n)_ Any response except _y_ or _Y_ will be processed as "No." You can always apply the theme later through the control panel.

**Apply Which Variation?**

If you chose to apply the newly uploaded theme, you will be prompted with: &quot;Which variation would you like to apply?&quot;

Use your arrow keys to move the selection caret/highlight to the variation you want, and then press _Enter_.

Stencil CLI will then confirm which variation is active on the storefront.

![Upload Successful](../images/upload_validated.jpg)

Note: [stencil pull](https://docs.bigcommerce.com/developer/docs/storefront/stencil/cli/options-and-commands)

Pulls the configuration from the active theme on your live store and updates your local configuration.

This is useful if any theme settings have been changed within the Theme Styles interface in the control panel, as it will prevent you from overwriting them with your next theme upload by first syncing them.
