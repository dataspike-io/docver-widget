# DocVer-widget

Install:

``` 
yarn @dataspike/docver-widget
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

| Prop   name |         type          |                                Description |
|-------------|:---------------------:|-------------------------------------------:|
| id          |        string         |                            Verification Id |
| apiUrl      |        string         |                               API base URL |
| elementId   |        string         | Id of element when widget will be rendered |
| onFinish    | `() => Promise<void>` | Callback raised when user finish verification |

Example:
 ```
import { DocsVerificationWidget } from '@dataspike/docver-widget';

export const renderWidget = async () => {
    if (container) {
        DocsVerificationWidget({
            id: 'VC0CE6CB061884763'
            elementId: 'root',
            apiUrl: 'https://api.dataspike.io',
        });
    }
};

renderWidget()
 ```

If you have any question about integration, please [contact us](https://www.dataspike.io/contact-us).
