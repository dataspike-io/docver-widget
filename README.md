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

How to use:

``` 
import { DocsVerificationWidget } from @dataspike/docver-widget;
....
DocsVerificationWidgetProps(props);
 ```

Available props:

| Prop   name    |                                                           type                                                           |                                  Description |
|----------------|:------------------------------------------------------------------------------------------------------------------------:|---------------------------------------------:|
| id             |                                                          string                                                          |   id of element when widget will be rendered |
| apiUrl         |                                                          string                                                          |                                 API base URL |
| token          |                                                          string                                                          |                                   Auth token |
| checks         |                                               VerificationPhotosKeysEnum[]                                               |                              Required checks |
| verificationId |                                                          string                                                          |                   Id of current verification |
| onStartNewVerification |    () => Promise<{ <br/>token: string; <br/>verificationId: string; <br/>checks: VerificationPhotosKeysEnum[]  }>        | Callback rasied on start of new verification |

Where:
``` 
export enum VerificationPhotosKeysEnum {
    SELFIE = 'selfie',
    PASSPORT = 'passport',
    ID_CARD_FRONT = 'id_card_front',
    ID_CARD_BACK = 'id_card_back',
    RESIDENCE_PERMIT_FRONT = 'residence_permit_front',
    RESIDENCE_PERMIT_BACK = 'residence_permit_back',
    VISA = 'visa',
    POA = 'poa', // (Proof Of Address)
    LIVENESS_PHOTO = 'liveness_photo',
    DRIVER_LICENSE_FRONT = 'driver_license_front',
    DRIVER_LICENSE_BACK = 'driver_license_back',
}
 ```

Example:
 ```
import axios from 'axios';
import Cookies from 'universal-cookie';

import { VerificationPhotosKeysEnum, DocsVerificationWidget } from '@dataspike/docver-widget';

export const renderWidget = async () => {
    const authorize = await axios.get('https://demo-sdk.dataspike.dev/api/authorize');
    const cookies = new Cookies();
    cookies.set('ds-demo-sdk-session-id', authorize.data.session_id, { path: '/' });

    const verification = await axios.post(
        'https://demo-sdk.dataspike.dev/api/start_full_verification',
        {
            checks: [
                VerificationPhotosKeysEnum.PASSPORT,
                VerificationPhotosKeysEnum.LIVENESS_PHOTO,
                VerificationPhotosKeysEnum.POA,
            ],
        },
        {
            withCredentials: true,
        },
    );

    const container = document.getElementById('root');

    if (container) {
        DocsVerificationWidget({
            id: 'root',
            apiUrl: 'https://api.dataspike.dev',
            token: verification.data.token,
            checks: verification.data.checks,
            verificationId: verification.data.verification_id,
            onStartNewVerification: async () => {
                const newVerification = await axios.post(
                    'https://demo-sdk.dataspike.dev/api/start_full_verification',
                    {
                        checks: [
                            VerificationPhotosKeysEnum.PASSPORT,
                            VerificationPhotosKeysEnum.LIVENESS_PHOTO,
                            VerificationPhotosKeysEnum.POA,
                        ],
                    },
                    {
                        withCredentials: true,
                    },
                );

                return {
                    token: newVerification.data.token,
                    checks: newVerification.data.checks,
                    verificationId: newVerification.data.verification_id,
                };
            },
        });
    }
};

renderWidget()
 ```

**Note:** https://demo-sdk.dataspike.dev is for test purpose only.
You have to implement your own API to control authentication and verificationId.

If you have any question about integration, please [contact us](https://www.dataspike.io/contact-us).
