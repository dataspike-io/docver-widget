# DocVer-widget

Install:

``` 
yarn install @dataspike/docver-widget
 ```
or
 ``` 
npm i @dataspike/docver-widget
 ```
or add static js file

 ``` 
https://static.dataspike.io/scripts/dataspike-{version}.js
 ```
Actual version you can find in https://www.npmjs.com/package/@dataspike/docver-widget

How to use:

``` 
import { DocsVerificationWidget } from @dataspike/docver-widget;
....
DocsVerificationWidgetProps(props);
 ```

Available props:

<table>
    <tr>
        <th>Prop name</th>
        <th>Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>id</td>
        <td>string</td>
        <td>Verification Id</td>
    </tr>
    <tr>
        <td>apiUrl</td>
        <td>string</td>
        <td>API base URL</td>
    </tr>
    <tr>
        <td>elementId</td>
        <td>string</td>
        <td>Id of element when widget will be rendered</td>
    </tr>
    <tr>
        <td>onFinish</td>
        <td>() => Promise&lt;void&gt;</td>
        <td>Callback raised when user finish verification</td>
    </tr>
    <tr>
        <td>onInit</td>
        <td>(verificationStatus: 'completed' | 'expired' | 'active' | 'error', error?: unknown) => Promise&lt;void&gt;</td>
        <td>Callback raised before verification started</td>
    </tr>
    <tr>
        <td>theme</td>
        <td>Check index.d.ts inside package</td>
        <td>Custom styles</td>
    </tr>
</table>

Example:
 ```
import { DocsVerificationWidget } from '@dataspike/docver-widget';

export const renderWidget = async () => {
    if (container) {
        DocsVerificationWidget({
            id: 'VF57124F182867E0'
            elementId: 'root',
            apiUrl: 'https://api.dataspike.io',
        });
    }
};

renderWidget()
 ```

Or 

```
<script type="module" defer src="https://static.dataspike.io/scripts/dataspike-{version}.js"></script>
<script>
    document.addEventListener('DOMContentLoaded', () => {
        const renderWidget = async () => {
            const container = window.document.querySelector('#root');
            if (container) {
                window.DocsVerificationWidget({
                    id: 'VF57124F182867E0',
                    elementId: 'root',
                    apiUrl: 'https://api.dataspike.io',
                });
            }
        };

        renderWidget()
    });
</script>
```
Html:
```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="utf-8" />
    </head>
    <body>
        <noscript>You need to enable JavaScript to run this app.</noscript>
        <div id="root"></div>
    </body>
</html>
```

If you have any question about integration, please [contact us](https://www.dataspike.io/contact-us).
