# momo-wallet-php-client

This is PHP client library for Momo Wallet

## Requirements

- PHP gnupg extension: http://php.net/manual/en/gnupg.installation.php

## Usage

1. Add `composer.json` config

```
{
    "require": {
      "viecco/momo-wallet-php-client": "master@dev",
    },
    "repositories": [{
      "type": "vcs",
      "url": "https://github.com/viecco/momo-wallet-php-client"
    }]
}
```

2. Run `composer update`

3. Test code

```
use Momo\Client as MomoClient;
use Momo\Crypto\CryptGPG as Crypto;

$config = [
  'partner_code' => 'xxx',
  'wallet_id' => 'xxx',
  'wallet_password' => 'xxx',
];

$partnerPrivateKey = file_get_contents("./keys/partner-sec.asc");
$partnerPublicKey  = file_get_contents("./keys/partner-pub.asc");
$partnerPassphrase = '';
$momoPublicKey  = file_get_contents("./keys/momo-pub.asc");

$clientCrypto = new Crypto($momoPublicKey, $partnerPrivateKey, $partnerPassphrase);
$momo = new MomoClient($config, $clientCrypto);
$data = $momo->getPaymentStatus('xxx');

print_r($data);

```
