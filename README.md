# Amazon Pay Checkout v2

This module will enable "Amazon Pay Checkout v2" on your Magento 2 installation. Amazon Pay Checkout v2 is the next generation web checkout technology of Amazon Pay that provides several advantages over the previous Amazon Pay Checkout solution.

## What's new in Amazon Pay Checkout v2?

* Hosted checkout experience (replacing widgets solution of the previous module)
* Fewer checkout steps (merging consent and address/payment selection screen)
* Avoids problems on browsers that have active cookie blocking or tracking protection mechanisms
* Supports virtual goods
* Automatic, graceful handling of declined authorization, increasing checkout conversion rate
* Integrated support for PSD2/SCA (Strong Customer Authentication)

## About Amazon Pay

Amazon Pay offers a familiar and convenient buying experience that can help your customers spend more time shopping and less time checking out. Amazon Pay is used by large and small companies. From years of shopping safely with Amazon, customers trust their personal information will remain secure and know many transactions are covered by the Amazon A-to-z Guarantee. Businesses have the reassurance of our advanced fraud protection and payment protection policy.

## Dependencies

You can find a list of modules in the require section of the `composer.json` file located in the
same directory as this `README.md` file.

## Installation Steps

**Important:** Before proceeding, please make a backup of your current Magento 2 installation.

### 1. Install module

The module can be either installed via composer (recommend), or manually. The steps for each option are described below. 

#### Composer installation
```
$ composer require amzn/amazon-payments-magento-2-plugin:dev-V2checkout
$ bin/magento module:enable Amazon_PayV2
```
If composer installation didn't work, use the manual procedure below. If any of these were successful, please proceed with **2. Post-installation procedure**, otherwise reach out to Amazon Pay merchant support for additional assistance.

#### Manual installation
* Download the [Amazon Pay V2 checkout plugin](https://github.com/amzn/amazon-payments-magento-2-plugin/tree/V2checkout) via `git clone` or 'Download ZIP'
* Copy src/PayV2 to app/code/Amazon/PayV2  
(If `magento-root/app/code/Amazon/PayV2` path is not present, please create the folders Amazon and PayV2)  

In Magento root, execute:
```
$ composer require amzn/amazon-pay-sdk-v2-php
$ composer require aws/aws-php-sns-message-validator
$ bin/magento module:enable Amazon_PayV2
```

### 2. Post-installation procedure

Execute the following steps to perform the module upgrade, compile dependency injection, deploy static content and clean caches.

```
$ bin/magento setup:upgrade
$ bin/magento setup:di:compile
$ bin/magento setup:static-content:deploy
$ bin/magento cache:clean
```

## PWA Support

1. The module exposes the REST endpoints that needs to set up. You can find them at [src/PayV2/etc/webapi.xml](https://github.com/amzn/amazon-payments-magento-2-plugin/blob/V2checkout/src/PayV2/etc/webapi.xml)
1. The front end needs to be setup by the merchant/developer.

## Extension Points

Amazon Pay does not provide any specific extension points.

## Configuration

### Amazon Pay V2 configuration ###

After successfully installting the module, please follow the steps below for configuring it.

1. Go to Stores -> Configuration -> Sales -> Payment Methods -> Amazon Pay -> Configure
1. Switch to 'V2' under the Amazon Pay Product Version
1. Under 'Private Key' field, click on the 'Generate a new public/private key pair for Amazon Pay'. This saves the Private Key in the settings and displays the text [encrypted]
1. Click 'Download Public Key' to save the Public Key locally
1. To obtain the Public Key ID, please email your Amazon Pay POC with your Seller Central Merchant ID and Public key that you just downloaded (attached in the email)
1. Amazon Pay will respond with the Public Key ID, which then you add in the Public Key ID field
1. Merchant Id will be the same as you V1 credentails, please copy and paste it here
1. Store Id refers to the Client Id in V1 settings, please copy and paste it here
1. Rest of the settings are all similar to the V1 settings. We recommend to use the same settings as used in V1. [View V1 Confirgurations documentation](https://amzn.github.io/amazon-payments-magento-2-plugin/configuration.html)
