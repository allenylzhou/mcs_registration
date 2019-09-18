# Mission City Swing Registration App

Primary Owner: [Maggie Moreno](https://github.com/missmaggiemo)

- See the live production app here https://registration.missioncityswing.com/

- See the test/development app https://mcs-reg-test.firebaseapp.com/

## Developer's Guide

You'll need yarn and node v8.11.3. I recommend using nvm to manage your node and npm version.

Install NVM-- see more detailed directions here https://github.com/nvm-sh/nvm/blob/master/README.md
```
$ curl https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh > ~/Desktop/install-nvm.sh

# read the file

$ bash ~/Desktop/install-nvm.sh
```

Install Yarn
```
$ brew install yarn
```

Install JS dependencies of this repo
```
$ nvm use
$ yarn install
$ yarn start
```

This is a [ReactJS](https://reactjs.org/) app bootstrapped with [Create React App](https://github.com/facebookincubator/create-react-app) and built on top of [Firebase](https://firebase.google.com/). That means that all of the middleware/backend is taken care of by Firebase, and when you clone this repo, all you will see is the ReactJS codebase. Don't be alarmed.

Second, the codebase as-is has the backend-for-frontend API calls but doesn't have the database(s) set up. So if you want to contribute more than just a typo fix, you'll have to reach out to me, [Maggie Moreno](https://github.com/missmaggiemo), and I'll help you get set up.

And lastly, if you are taking the time to read this, I already adore you and am so looking forward to your help.

Thank you!

<3 Maggie Moreno

### Developing Payments locally

1. Follow Steps 1 and 2 of this guide: https://square.github.io/react-square-payment-form/docs/paymentform to create a Square developer account and get your Sandbox credentials
2. In src/lib/payment.js, replace your sandbox credentials
```
// Square Application ID
export const APPLICATION_ID: string = process.env.NODE_ENV === 'production' ? 'sq0idp-v7U5CDrd7BsGSyBaJ5ubow' : '<YOUR_SANDBOX_APPLICATION_ID>';
// Square Location ID
export const LOCATION_ID: string = process.env.NODE_ENV === 'production' ? '04Z8B2G52FQXP' : '<YOUR_SANDBOX_LOCATION_ID>';
export const USE_SANDBOX: boolean = process.env.NODE_ENV === 'production' ? false : true;
```
3. Create an untracked file called functions/.runtimeconfig.json and replace your sandbox credentials
```
{
  "paymentservice": {
    "hostname": "connect.squareupsandbox.com",
    "accesstoken": "<YOUR_SANDBOX_ACCESS_TOKEN>",
    "locationid": "<YOUR_SANDBOX_LOCATION_ID>"
  }
}
```
4. In a separate tab, run your functions emulator locally
`cd functions`
`npm run build`
`firebase emulators:start --only functions`
5. In a separate tab, run the react app
`npm start` or `yarn start` from the root directory
6. You're now set up to take payments with your sandbox account when you develop locally. Use the test credit card from this guide: https://square.github.io/react-square-payment-form/docs/paymentform#7-generate-a-nonce
