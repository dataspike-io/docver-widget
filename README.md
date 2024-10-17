# DocVer-widget

### Live Demo

Please check <a href="https://dash.dataspike.io/widget/demo" target="_blank">live demo</a>

### Install

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
        <td>Check 
            <a target="_blank" 
            href="https://docs.dataspike.io/api#tag/Verifications/operation/create-verification">
                API documentation
            </a>
        </td>
    </tr>
    <tr>
        <td>apiUrl</td>
        <td>string</td>
        <td>
            <a target="_blank" href="https://docs.dataspike.io/api">
                https://api.dataspike.io
            </a>
        </td>
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
        <td>Check theme section</td>
        <td>Custom styles</td>
    </tr>
</table>

### Example:
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
### Html:
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

### Theme:
In comment described default value:
```typescript
export type Theme = {
    palette?: Partial<{
        textMain: string; // #000000
        textLight: string; // #737390
        primaryA1: string; // #6664E8
        primaryA2: string; // #5A58DF
        primaryA3: string; // #D0D0FC
        primaryA4: string; // #E8E8FC
        primaryA5: string; // #E0E0FA
        primaryA6: string; // #E6EDFB
        primaryA7: string; // #FFFFFF
        secondaryA1: string; // #F6CDD9
        secondaryA2: string; // #F6F0C0
        secondaryA3: string; // #52C27F
        secondaryA4: string; // #FF5050
        secondaryA5: string; // #FFFCFD
        secondaryA6: string; // #FABC46
        secondaryA7: string; // #B25DF5
        secondaryA8: string; // #EDECFC
        secondaryA9: string; // #DEE1F2
        secondaryA10: string; // #F6F8FE
        secondaryA11: string; // #EDECFC
        secondaryA12: string; // #FAFAFC
    }>;
    typography?: Partial<{
        fontFamily: string; // Mont, sans-serif
        body1: {
            fontFamily: string; // Mont, sans-serif
        };
        body2: {
            fontFamily: string; // Mont, sans-serif
        };
        caption: {
            fontFamily: string; // Mont, sans-serif
        };
        h1: Partial<{
            fontFamily: string; // Mont, sans-serif
            fontSize: string; // 50px
            fontWeight: string; // 500
            lineHeight: string; // 70px
            letterSpacing: string; // -0.01em
        }>;
        h2: Partial<{
            fontFamily: string; // Mont, sans-serif
            fontSize: string; // 28px
            fontWeight: string; // 500
            lineHeight: string; // 40px
            letterSpacing: string; // -0.01em
        }>;
        h3: Partial<{
            fontFamily: string; // Mont, sans-serif
            fontSize: string; // 20px
            fontWeight: string; // 500
            lineHeight: string; // 30px
            letterSpacing: string; // -0.01em
        }>;
        text: Partial<{
            fontSize: string; // 14px
            lineHeight: string; // 22px
            letterSpacing: string; // 0.002em
        }>;
        textBold: Partial<{
            fontSize: string; // 14px
            fontWeight: string; // 500
            lineHeight: string; // 22px
            letterSpacing: string; // 0.002em
        }>;
        smallText: Partial<{
            fontSize: string; // 12px
            lineHeight: string; // 18px
            letterSpacing: string; // 0.002em
        }>;
        smallTextBold: Partial<{
            fontSize: string; // 12px
            fontWeight: string; // 500
            lineHeight: string; // 18px
            letterSpacing: string; // 0.002em
        }>;
    }>;
};
```


If you have any question about integration, please [contact us](https://www.dataspike.io/contact-us).
