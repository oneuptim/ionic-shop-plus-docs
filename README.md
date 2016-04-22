
# [Ionic Shop (Advanced Edition)](https://www.noodl.io/market/product/P201602271203444/ionic-shop-advanced-edition-full-ecommerce-app-w-stripe-payments-and-admin) | Documentation

The **Ionic Shop - Advanced Edition** is the complete solution to start your own eCommerce app or webshop today. It contains everything you need to sell your
products immediately and receive payments on your account. It also comes with a complete Admin Management part that can be used by non-developers to manage the content of the app.

View a demo, preview it on your phone, read more about all the functionalities and download the template on the [product page](https://www.noodl.io/market/product/P201602271203444/ionic-shop-advanced-edition-full-ecommerce-app-w-stripe-payments-and-admin).

[<img src="http://www.seipel-ibisevic.com/assets-external/ionic-shop-plus/v3/banner_envato_web.png">](https://www.noodl.io/market/product/P201602271203444/ionic-shop-advanced-edition-full-ecommerce-app-w-stripe-payments-and-admin)

# External Dependencies
The following external accounts are needed to work with this package as it is:

- An account for the database (firebase.com)
- An account to receive payments (stripe.com)
- An account on Mashape to consume the Stripe Payments API (mashape.com)

# Getting started

Unzip the package in your workspace. You will find two folders:

- ionic-app
- admin

# Setup 1: Payment setup

We first need to define a couple of constants in our app. If you are working with Angular/Ionic `v1.x`, head over to `app.js` and you'll see the following:

```
// Stripe Payments API
// Obtain from:
// - https://market.mashape.com/noodlio/noodlio-pay-smooth-payments-with-stripe
var NOODLIO_PAY_API_URL         = "https://noodlio-pay.p.mashape.com";
var NOODLIO_PAY_API_KEY         = "<YOUR-MASHAPE-API-KEY>";

// Stripe Account
// Connect on both:
// - https://www.noodl.io/pay/connect and
// - https://www.noodl.io/pay/connect/test
var STRIPE_ACCOUNT_ID           = "<YOUR-STRIPE-ACCOUNT-ID>"

// Define whether you are in development mode (TEST_MODE: true) or production mode (TEST_MODE: false)
var TEST_MODE = false;
```

The `NOODLIO_PAY_API_URL` is basically the location of the server and is fixed. The variable `TEST_MODE` simply takes the values `true` or `false` and defines whether we are in test mode (development) or production (actually charging the user). Now let's define two constants:

**Mashape**

To consume the Stripe Payments API, we'll need to obtain our unique `NOODLIO_PAY_API_KEY`. To do so, head over to [Mashape](https://market.mashape.com/noodlio/noodlio-pay-smooth-payments-with-stripe) and click on the right "Get your API Keys and Start Hacking" or press on "Sign up free".

[<img src="http://noodlio-templates.firebaseapp.com/noodlio-pay/img/mashape-api-keys.png">](https://market.mashape.com/noodlio/noodlio-pay-smooth-payments-with-stripe)

After you are signed in, you'll find your unique API Key in the request example on the [Stripe Payments API page](https://market.mashape.com/noodlio/noodlio-pay-smooth-payments-with-stripe):

```
curl -X POST --include 'https://noodlio-pay.p.mashape.com/charge/token' \
  -H 'X-Mashape-Key: <YOUR-MASHAPE-API-KEY>' \
  -H 'Content-Type: application/x-www-form-urlencoded' \
  -H 'Accept: application/json' \
  ... other values
```

Replace the `NOODLIO_PAY_API_KEY` with this unique identifier.

**Stripe Account**

If you haven't already [sign up for a Stripe Account](https://www.stripe.com). After that, you'll need to retrieve your unique Stripe Account ID (field: `stripe_account`), which you can obtain on the following pages (Note: you'll need to visit both links once):

- For the production mode:
[https://www.noodl.io/pay/connect](https://www.noodl.io/pay/connect)
- For the development mode:
[https://www.noodl.io/pay/connect/test](https://www.noodl.io/pay/connect/test)

The Stripe Account ID looks something like `acct_12abcDEF34GhIJ5K`. Replace the constant `STRIPE_ACCOUNT_ID` wherever you have defined it.

That's it. Our server is configured and ready to receive payments.

# Setup 2: Firebase Admin Rights, Security Rules and Firebase Constants
We use Firebase as a database to host your shopping items, i.e. the products that you are selling. These items are managed through an admin panel that is provided with this package in the folder `admin`.

## Creating a Firebase Account

1. If you already have a Firebase account, login, go to your Dashboard and create a new app.
2. Open this workspace by pressing **Manage this app**.
   In your browser, remember the url (i.e. something like: `[your-app-name].firebaseio.com`. We define this as the `FBURL` (needed in steps below)

## Firebase Admin Rights
The instructions for this part are visually explained in the folder `admin/img/examples`.

## Security Rules
To secure your app we will need to add Firebase security rules:

1. open the file `firebase_rules.txt` and copy the content
2. go to your Firebase and open your app `[your-app-name]`.
3. On the right, press **Security & Rules**
4. Paste (overwrite) all content with the content of `firebase_rules.txt`

### Firebase Constants

We need to replace the FBURL at two locations:

1. Open `ionic-app/www/js/app.js` and replace `FBURL` with the appropriate value (i.e. `[your-app-name].firebaseio.com)`
2. Open `admin/js/app.js` and replace `FBURL` with the appropriate value (i.e. `[your-app-name].firebaseio.com)`

# Setup 3: Admin panel
The last step is to setup your Admin panel. You can unzip the files on your computer and then simply open `index.html` with Chrome to work with it.

Alternatively, host it in the cloud with for instance Cloud9:

1. go to `www.c9.io`
2. create an account or login
3. in your dashboard, create a new workspace (select nodejs)
4. open this workspace
5. delete all files in there
6. upload (drag and drop) all the files from this package to the workspace
7. open index.html and then press Run (green button in top)

After step 7, you will see something like the following in the terminal:
```
Your code is running at https://[admin-workspace-name]-[your-username].c9users.io.
```
Note: if you are not active for two days, you will need to login to your workspace and press again the green button Run to activate the admin. This can be overcome by uploading all your files to a custom server. Feel free to email me if you wish to do this.

## Extending the Authorized Domains for oAuth redirect
If you are hosting the Admin panel on a foreign location (in the cloud), you will need to extend the authorized domains for oAuth redirects in Firebase. To do so:

1. Go to Firebase and open your app `[your-app-name]`
2. On the right press **Login & Auth**
3. In the first top field add the location of your admin panel. If you are hosting it on cloud9 then you would typically add: `https://[admin-workspace-name]-[your-username].c9users.io`

# Setup 4: Ionic App Setup
Now that we have prepared the back-end, it's time to setup and run the front-end. If you are familiar with Ionic Framework, then you know the structure of such apps. If you are new to Ionic, then you probably need to setup the dependencies. Here is [how to get started with Ionic](http://ionicframework.com/getting-started/):

```
$ npm install -g cordova ionic
```

Usually you would follow up by typing something like `ionic start myApp tabs`. This is not needed anymore since all the files are in the folder `ionic-app`. To run the application, the only thing you need to do is:

```
$ cd ionic-app
$ ionic-serve
```

If you are working locally, you can then visit `http://localhost:8100/` in your browser to
preview your application.

You can also unpack all the files in a cloud environment such as Cloud9 (see instructions above, they are similar).

# Wrapping up
So far you have setup all the constants and variables. If everything went well, all should be working fine now. To proceed, you can now login to your admin panel and add items. These items will be immediately (after refreshing) shown in your Ionic App. You can try to make a test purchase in the Ionic App. You will see the payment immediately reflected on your Stripe Account. The orders will be also visible in both the admin management as the orders section of the app. Have fun earning money!

# Questions?

If you have questions or remarks, please let me know by either typing a comment on this site, or by e-mailing me to: `noodlio@seipel-ibisevic.com`

Have fun!

# Changelog

[View it on the product page](https://www.noodl.io/market/product/P201602271203444/ionic-shop-advanced-edition-full-ecommerce-app-w-stripe-payments-and-admin)
