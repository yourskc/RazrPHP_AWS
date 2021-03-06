# RazrPHP

Program in PHP with AWS? Razr PHP Framework cuts down on a lot of hastle and makes AWS even easier to use. Functionality with many systems including EC2, DynamoDB, S3, and more to come.

Have all the major functions ready, accessible, and easy to use at your finger tips.


<!---## Screenshots

![Screenshot](Assets/screenshota.png)
![Screenshot](Assets/screenshotb.png)--->

## Contributors

- [Nick Soggin](http://www.dreamthegame.com), iSkore Development Inc.
- [Clay O'Keefe](http://www.dreamthegame.com), iSkore Development Inc.

## Documentation

Simple to make AWS calls. Settup is easy too!

#### **AWS Setup**
###### - AWS doesn't lay out the Credentials setup for you set by step, so I will.
 * **1.** Go to AWS and get your **PUBLIC_KEY** and **PRIVATE_KEY**
    * AWS does have tutorials for this [HERE](http://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/ec2-key-pairs.html) and [HERE](http://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/ec2-key-pairs.html#having-ec2-create-your-key-pair)

 * **2.** Open Terminal
 * **3.** If you haven't created your credentials yet, in Terminal's fresh page, type in:</br>
        `
        nano ~/.aws/creds
        `</br>
    * The *nano* function page will open up. You will see `GNU nano 2.0.6...` at the top.
 * **4.** Inside the *nano* page, type in:</br>

```sh
[default]
aws_access_key_id = public_key_ABCDEFGHIJKLMNOPQRSTUVWXYZ
aws_secret_access_key = private_key_s0m3_CR42Y_l3tt3rS_i5y0ur53cr3tK3y
```
 * **5.** Once you've typed it out, hit **CONTROL + X** (Yes...Control, not Command).
 * **6.** Hit **Y** then **ENTER**
 * **7.** Get the [AWS_SDK_PHP](https://github.com/aws/aws-sdk-php/releases/tag/2.8.2)
 * **8.** Go to Your Elastic Beanstalk
 * **9.** When you are done creating your app and you see the *Overview* screen with the green check. Look to the side and hit *Configuration*.
 * **10.** Under **Software Configuration** -> **Document root:** type in: **/**
 * **11.** Under **Property Name** -> **AWS_ACCESS_KEY_ID** type in: **[your_access_key]**
 * **12.** Under **AWS_ACCESS_KEY_ID** is the **AWS_SECRET_KEY**, type in: **[your_secret_key]**
 * **13.** When your PHP Project is ready. Put all your files into one folder. Name the folder **[whatever]**, then compress the files inside **[whatever]**. Do not compress the whole folder. Only compress the files in the folder. If one of these files includes your **index.php** or **index.html**, your project will show up on EBS default URL.
 * **14.** Your project should be called *Archive.zip*. Go to EBS, upload the zip and there you go! All finished with AWS Setup!

#### **Razr Setup**
 * **1.**  Download **RazrPHP** and put it in your home folder *(~/)* (same folder as the aws_php_sdk)
 * **2.**  At the top of the file using **RAZR**, put in:
```php
    require ('razrAWS.php');
    use razrPHP as RAZR;
    $razr = new RAZR\rDynamo ();
```
 * **3.**  Thats it! You can now access RAZR Functions easily.

### **Razr Methods**
#### &nbsp;&nbsp;DynamoDB  
</br>
##### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - &nbsp;Create Table

```php
    $hK = array('hashKey', 'S', 'HASH');
    $rK = array('rangeKey', 'S', 'RANGE');
    $tput = array(1, 1);
    $t = $razr->razrTable('[table_name]', $hK, $rK, $tput);
    echo $t;
```
 * All of the above parameters are required except for 'hashKey' and 'rangeKey'. Those are editable to your choice.
 * You can add all other attributes in you first `Put Item` request
 * Recommendation - wait at least 5 seconds before making changes to the table. You can do this easily with `sleep(5);`

</br>
##### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - &nbsp;Describe Table
```php
    $t = $razr->describeTable('[table_name]');
```
</br>
##### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - &nbsp;Put Item

```php
    $r = array('hashKey' => array('S' => '[hash_key]'), 'rangeKey' => array('S' => '[range_key]'));
    $t = $razr->putItem('[table_name]', $r);
```
</br>
##### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - &nbsp;Get Item

```php
    $r = array('hashKey' => array('S' => '[hash_key]'), 'rangeKey' => array('S' => '[range_key]'));
    $t = $razr->getItem('[table_name]', $r);
    $t->getPath('Item/rangeKey/S');
    // - OR
    $t['Item']['rangeKey']['S'];
```

</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;All responses will be in JSON format. So you can access your response:
```php
/*Read the values accessable via*/ echo $razr; //for the JSON response
//Write the path of the value you would like:
$t->getPath('Table/ProvisionedThroughput/ReadCapacityUnits');
// - OR
$t['Table']['ProvisionedThroughput']['ReadCapacityUnits'];
```
</br>
##### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - &nbsp;Query Items

```php
$conditions = array();
$conditions['hash'] = 'hashKey';
$conditions['type'] = 'S';
$conditions['value']= '[hash_key]';
$conditions['oper'] = '[comparison_operator]';
$t = $razr->queryItems('[table_name]', $conditions);
```
</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Read your response query:
```php
foreach ($t as $item) {
    echo $item['rangeKey']['S']."\n";
}
```


## License

PHP Stack is released under the MIT License:

The MIT License (MIT)

Copyright (c) 2015 iSkore Development Inc.

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
