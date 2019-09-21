[![Build Status](https://travis-ci.org/midoks/php-eureka-client.svg?branch=master)](https://travis-ci.org/midoks/php-eureka-client)

# PHP Eureka Client

PHP client for the [Netflix Eureka server](https://github.com/Netflix/eureka). Supports all [Eureka REST operations](https://github.com/Netflix/eureka/wiki/Eureka-REST-operations).

## Installation
Run
```
composer require midoks/php-eureka-client
```
or add dependency to your composer.json file
```
"require": {
    ...
    "midoks/php-eureka-client": "^1.0"
}

```
## Usage example
### 1. Use needed packages
```php
use Eureka\Client;
```
### 2. Create Eureka app instance
```php
// We will use app name and instance id for making requests below.
$client = new \Euraka\Client($this->host, $this->port, $this->context);

```
### 3. Create Eureka client
```php
// Eureka client usage example.
// Create guzzle client.
$guzzle = new Client();

// Create eureka v2 client.
$eurekaClient = new EurekaClient('localhost', 8080);

// Create eureka v1 client.
$eurekaClient = new EurekaClient('localhost', 8080, 'eureka');
```
### 4. Make requests
```php
try {
  // Register new application instance.
  $response = $eurekaClient->register($appName, $instance);

  // Query for all instances.
  $allApps = $eurekaClient->getAllApps();

  // Query for all application instances.
  $app = $eurekaClient->getApp($appName);

  // Query for a specific application instance.
  $appInstance = $eurekaClient->getAppInstance($appName, $instanceId);

  // Query for a specific instance.
  $instance = $eurekaClient->getInstance($instanceId);

  // Send application instance heartbeat.
  $response = $eurekaClient->heartBeat($appName, $instanceId);

  // Take instance out of service.
  $response = $eurekaClient->takeInstanceOut($appName, $instanceId);

  // Put instance back into service.
  $response = $eurekaClient->putInstanceBack($appName, $instanceId);

  // Update metadata.
  $response = $eurekaClient->updateAppInstanceMetadata($appName, $instanceId, [
    'new_key' => 'new_value',
  ]);

  // Query for all instances under a particular vip address/
  $instances = $eurekaClient->getInstancesByVipAddress('test_vip_address');

  // Query for all instances under a particular secure vip address.
  $instances = $eurekaClient->getInstancesBySecureVipAddress('test_secure_vip_address');

  // De-register application instance.
  $response = $eurekaClient->deRegister($appName, $instanceId);
}
catch (Exception $e) {
  echo $e->getMessage() . PHP_EOL;
}
```