# DocVer Widget Documentation
### Introduction
DocVer Widget is a tool that allows users to easily verify documents through an interactive interface. This widget helps ensure document verification and provides feedback on the verification status.

### Live Demo
You can see the widget in action by visiting the <a href="https://dash.dataspike.io/widget/demo" target="_blank">live demo</a>.

### Installation
You can install the DocVer widget in several ways:

### Option 1: Using Yarn

If you have Yarn installed, run the following command in your terminal:

```bash
yarn install @dataspike/docver-widget
```

### Option 2: Using NPM
If you prefer NPM, use this command:

```bash
npm install @dataspike/docver-widget
```

### Option 3: Linking a Static JS File
You can also link the widget directly in your HTML by adding the following `<script>` tag. Replace `{version}` with the current version number found on [npm](https://www.npmjs.com/package/@dataspike/docver-widget):

```html
<script src="https://static.dataspike.io/scripts/dataspike-{version}.js"></script>
```

## How to Use the Widget
### Step 1: Import the Widget
If you are using a JavaScript framework (like React), start by importing the widget:

```javascript
import { DocsVerificationWidget } from '@dataspike/docver-widget';
```

### Step 2:  Render the Widget
Before rendering the widget, you need to create a verification for the applicant using the API. This should be done on the backend, and you will only pass the verificationUrlId to the frontend.

The code looks like this:

```javascript
const renderWidget = async () => {
   const verificationUrlId = await getVerificationId(); // using your backend API
   const container = document.getElementById('root');
   if (container) {
      DocsVerificationWidget({
         id: verificationUrlId, // Use the obtained verification URL ID
         elementId: 'root',
         apiUrl: 'https://api.dataspike.io',
      });
   }
};
```
### Implementation Details for `getVerificationId`

The `getVerificationId` API should be implemented by your development team. This API is responsible for creating a verification process on the **backend** and should only return the `verificationUrlId` to the frontend.

- **Parameters**: The API will internally use `applicantId` and `profileId` to create the verification. These parameters must be kept confidential and should not be exposed to the frontend or any external parties.

- **Verification Creation**: Upon receiving a request to `getVerificationId`, the API will handle the creation of the verification with the specified `applicantId` and `profileId`.

- **Response**: Once the verification is successfully created, the API should respond with only the `verificationUrlId`, which is the identifier required for rendering the widget. This ensures that sensitive information remains secure and is not accessible outside of the **backend**.

By following this approach, you maintain the integrity and confidentiality of the verification process while ensuring a smooth integration wit

### Alternative Method: Using HTML `<script>` Tags
If you prefer using plain HTML and JavaScript, do it like this:

```html
<!DOCTYPE html>
<html lang="en">
<head>
   <meta charset="utf-8" />
   <script type="module" defer src="https://static.dataspike.io/scripts/dataspike-{version}.js"></script>
</head>
<body>
<noscript>You need to enable JavaScript to run this app.</noscript>
<div id="root"></div>
<script>
   document.addEventListener('DOMContentLoaded', () => {
      const renderWidget = async () => {
         const verificationUrlId = await getVerificationId(); // using your backend API
         const container = document.querySelector('#root');
         if (container) {
            window.DocsVerificationWidget({
               id: verificationUrlId, // Use the obtained verification URL ID
               elementId: 'root',
               apiUrl: 'https://api.dataspike.io',
            });
         }
      };
      renderWidget();
   });
</script>
</body>
</html>
```

#### Widget Properties
The widget can be customized using several properties. Here’s a description of each property you can use:

| Property Name         | Type   | Description                                                                                                                                                                                                                                                                                                         |
|-----------------------|--------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `applicantId`        | `string` | A unique identifier assigned to each applicant in the system. This ID is used to track and manage data for a specific user applying for document verification. For more details, visit the [Applicants API](https://docs.dataspike.io/api/#tag/Applicants).                                                         |
| `profileId`          | `string` | A unique identifier for a verification profile that contains parameters and settings for the verification process. This ID specifies the checks that should be performed for each applicant. For more information, check the [Verification Profiles API](https://docs.dataspike.io/api/#tag/Verification-profiles). |
| `id`                  | `string` | Unique identifier for the document to be verified. This is the same as `verification_url_id`. This is the Verification Short ID, used to verify and reference a specific verification process or entity. For further information, see the [Verifications API](https://docs.dataspike.io/api/#tag/Verifications).    |
| `apiUrl`              | `string` | API URL for interaction. Defaults to `https://api.dataspike.io`.                                                                           |
| `elementId`           | `string` | ID of the HTML element where the widget will be rendered.                                                                                  |
| `onFinish`            | `() => Promise<void>` | Callback invoked when the user finishes the verification process.                                                                          |
| `onInit`              | `(verificationStatus: 'completed' &#124; 'expired' &#124; 'active' &#124; 'error', error?: unknown) => Promise<void>` | Callback triggered before the verification starts. Provides status and any errors, which can be useful for debugging or informing the user. |
| `theme`               | `object` | Custom styles for the widget. See the "Theme" section below for details.                                                                   |



### Usage Examples
Here’s an example of using the widget with event handling:

```javascript
DocsVerificationWidget({
    id: 'VF57124F182867E0',
    elementId: 'root',
    apiUrl: 'https://api.dataspike.io',
    onFinish: async () => {
        alert('Verification completed!');
    },
    onInit: async (status) => {
        console.log('Verification status:', status);
    },
});
```

### Customizing the Theme
You can customize the appearance of the widget by providing a theme object. Below are the parameters you can change:

```javascript
const customTheme = {
    palette: {
        textMain: '#000000',
        primaryA1: '#6664E8',
        // Add other colors as needed
    },
    typography: {
        fontFamily: 'Mont, sans-serif',
        h1: {
            fontSize: '50px',
            fontWeight: '500',
        },
        // Customize other text styles
    },
};

// Include the theme in your widget call
DocsVerificationWidget({
    id: 'VF57124F182867E0',
    elementId: 'root',
    theme: customTheme,
});
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
## Errors and Debugging

If you encounter issues with the widget, check the following common errors:

1. **Invalid Document ID**: Ensure that the `id` is correct and corresponds to the document in the system.
2. **Connection Issues**: Verify that the `apiUrl` is correct and the API is accessible.
3. **JavaScript Errors**: Open the browser console (F12 or Cmd + Option + I) and check for any error messages.

## Frequently Asked Questions (FAQ)

1. **How do I change the appearance of the widget?**
   You can change the appearance by providing a `theme` object with custom styles.

2. **What should I do if the widget does not display?**
   Check that the `elementId` is correct and that there is an element with this ID in your HTML.

3. **How do I handle verification results?**
   Use the `onFinish` callback to perform actions after verification is completed, such as showing a notification to the user.fication is completed, such as showing a notification to the user.

## Additional Documentation
For comprehensive details about the API, including endpoints, request/response formats, and more, please refer to the <a href="https://docs.dataspike.io/api/#section/Introduction" target="_blank">Dataspike API Documentation</a> Dataspike API Documentation. This resource provides in-depth information essential for integrating and utilizing the API effectively.

If you have any question about integration, please [contact us](https://www.dataspike.io/contact-us).
