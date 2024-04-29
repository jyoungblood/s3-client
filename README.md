# Amazon S3 PHP Class

(new version forked from [amazon-s3-php-class](https://github.com/tpyo/amazon-s3-php-class))

Updates and improvements planned, but it's pretty much the same as the original for now.

## Installation

```
composer require jyoungblood/s3-client
```


## Usage

```php
S3::setAuth($awsAccessKey, $awsSecretKey);
```


### Object Operations

#### Uploading objects

Put an object from a file:

```php
S3::putObject(S3::inputFile($file, false), $bucketName, $uploadName, S3::ACL_PUBLIC_READ)
```

Put an object from a string and set its Content-Type:

```php
S3::putObject($string, $bucketName, $uploadName, S3::ACL_PUBLIC_READ, array(), array('Content-Type' => 'text/plain'))
```

Put an object from a resource (buffer/file size is required - note: the resource will be fclose()'d automatically):

```php
S3::putObject(S3::inputResource(fopen($file, 'rb'), filesize($file)), $bucketName, $uploadName, S3::ACL_PUBLIC_READ)
```

#### Retrieving objects

Get an object:

```php
S3::getObject($bucketName, $uploadName)
```

Save an object to file:

```php
S3::getObject($bucketName, $uploadName, $saveName)
```

Save an object to a resource of any type:

```php
S3::getObject($bucketName, $uploadName, fopen('savefile.txt', 'wb'))
```

#### Copying and deleting objects

Copy an object:

```php
S3::copyObject($srcBucket, $srcName, $bucketName, $saveName, $metaHeaders = array(), $requestHeaders = array())
```

Delete an object:

```php
S3::deleteObject($bucketName, $uploadName)
```

### Bucket Operations

Get a list of buckets:

```php
S3::listBuckets()  // Simple bucket list
S3::listBuckets(true)  // Detailed bucket list
```

Create a bucket:

```php
S3::putBucket($bucketName)
```

Get the contents of a bucket:

```php
S3::getBucket($bucketName)
```

Delete an empty bucket:

```php
S3::deleteBucket($bucketName)
```

