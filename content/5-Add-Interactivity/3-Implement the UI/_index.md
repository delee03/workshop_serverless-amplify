+++
title = "Implement the UI"
date = 2024
weight = 3
chapter = false
pre = "<b>6.3. </b>"
+++

1. Navigate to the profilesapp/src/main.jsx file and update it with the following code. Then, save the file.

![Update App.JSX](/images/workshop-setup/5_Root.png?width=full)

```typescript
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App.jsx";
import "./index.css";
import { Authenticator } from "@aws-amplify/ui-react";

ReactDOM.createRoot(document.getElementById("root")).render(
    <React.StrictMode>
        <Authenticator>
            <App />
        </Authenticator>
    </React.StrictMode>
);
```

You have updated the main.jsx file to include the Authenticator component from the Amplify UI library. The Authenticator component provides a set of pre-built authentication UI components that you can use to create a sign-up and sign-in flow for your application.

2. Open the profilesapp/src/App.jsx file, and update it with the following code. Then, save the file.

The code starts by configuring the Amplify library with the client configuration file (amplify_outputs.json). It then generates a data client using the generateClient() function. The app will use the data client to get the user’s profile data.

```typescript
import { useState, useEffect } from "react";
import {
    Button,
    Heading,
    Flex,
    View,
    Grid,
    Divider,
} from "@aws-amplify/ui-react";
import { useAuthenticator } from "@aws-amplify/ui-react";
import { Amplify } from "aws-amplify";
import "@aws-amplify/ui-react/styles.css";
import { generateClient } from "aws-amplify/data";
import outputs from "../amplify_outputs.json";
/**
 * @type {import('aws-amplify/data').Client<import('../amplify/data/resource').Schema>}
 */

Amplify.configure(outputs);
const client = generateClient({
    authMode: "userPool",
});

export default function App() {
    const [userprofiles, setUserProfiles] = useState([]);
    const { signOut } = useAuthenticator((context) => [context.user]);

    useEffect(() => {
        fetchUserProfile();
    }, []);

    async function fetchUserProfile() {
        const { data: profiles } = await client.models.UserProfile.list();
        setUserProfiles(profiles);
    }

    return (
        <Flex
            className="App"
            justifyContent="center"
            alignItems="center"
            direction="column"
            width="70%"
            margin="0 auto"
        >
            <Heading level={1}>My Profile</Heading>

            <Divider />

            <Grid
                margin="3rem 0"
                autoFlow="column"
                justifyContent="center"
                gap="2rem"
                alignContent="center"
            >
                {userprofiles.map((userprofile) => (
                    <Flex
                        key={userprofile.id || userprofile.email}
                        direction="column"
                        justifyContent="center"
                        alignItems="center"
                        gap="2rem"
                        border="1px solid #ccc"
                        padding="2rem"
                        borderRadius="5%"
                        className="box"
                    >
                        <View>
                            <Heading level="3">{userprofile.email}</Heading>
                        </View>
                    </Flex>
                ))}
            </Grid>
            <Button onClick={signOut}>Sign Out</Button>
        </Flex>
    );
}
```

3. Open a new terminal window, navigate to your projects root directory (profilesapp), and run the following command to launch the app:

```bash
npm run dev
```

4. Select the Local host link to open the Vite + React application.

![Local Host](/images/workshop-setup/RunLocalhost.png?width=full)

5. Choose the **Create Account tab**, and use the authentication flow to create a new user by entering **your email address and a password**. Then, **choose Create Account**.

![Local Host Website](/images/workshop-setup/5_Localhost1.png?width=full)

6. You will get a verification code sent to your email. Enter the verification code to log in to the app.

![Local Host Website](/images/workshop-setup/5_3_DienCodeOTP.png?width=full)

![Local Host Website](/images/workshop-setup/5_3_CodeEmail.png?width=full)

7. When signed in, the app will display your email address and a Sign Out button.

![Local Host Website](/images/workshop-setup/5_3_LoginSuccessful.png?width=full)

As you can see, you can login to the app and view your profile information at your localhost.

8. Now, you can push the changes to your GitHub repository by running the following commands in your terminal:

```bash

git add -A
git commit -m "Add interactivity to the web app displaying user profile information"
git push

```

9. AWS Amplify automatically builds your source code and deployed your app at _https://...amplifyapp.com_, and on every git push your deployment instance will update. Select the Visit deployed URL button to see your web app up and running live, you can use the **Host** tab to deploy your app to the AWS global content delivery network (CDN) and view it online
   in Amplify Console.

![Automatically](/images/workshop-setup/5_End_AutoDeploy.png?width=full)

You can login to the app and view your profile information at your deployed URL.

![ Host Website](/images/workshop-setup/DangNhapThanhCong1.png?width=full)

You have successfully implemented the UI for your web application. You can now view your profile information and sign out of the app.

10. You can now proceed to your DynamoDB table to view the data that was saved when you signed up.

Step 1: Open the AWS Management Console, and then navigate to the DynamoDB console.
you can see two table created by Amplify CLI.

![ DynamoDB](/images/workshop-setup/5_KiemTraDynamoDB.png?width=full)

Step 2: Choose the **Expolore items** tab, and then choose the **UserProfile** table to view the data that was saved when you signed up.

![Record User Info](/images/workshop-setup/EndXemRecordAccount1.png?width=full)
