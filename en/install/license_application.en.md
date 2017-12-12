## License Application

License is the precondition to use KAP. After installing and deploying KAP, you need apply for license to use KAP. There are KAP license, KAP Plus license and KyBot license in KAP products. Both KAP license and KAP Plus license include Evaluation License (Evaluation Period for each: Two months) and Official License. KyBot online service includes Basic, Standard and Professional Versions. The Professional Version provides more services and SLA support. The license of KAP and KAP Plus is different, so their application process varies a little. This article will introduce how to apply for KAP license and KAP Plus license.

### Application Process

To apply for KAP license and KAP Plus license, do the following: 

- Use your account to login to [Kyligence Account Center](http://account.kyligence.io/). If you do not have an account, please sign up first. If you already have an account, use you account to login.

![Kyligence Account Center](images/license_1.en.png)

- After login, select the license of **KAP Plus** or **KAP** based on your requirement. If you apply for KAP Evaluation License, just click the corresponding **Download Evaluation License** link. If you apply for KAP Plus Evaluation License, fill in an application form first. When you are approved to use KAP Plus, you will received a notification email sent by the system. Then login  [Kyligence Account Center](http://account.kyligence.io/) again and click the corresponding  **Download Evaluation License** link.

![Evaluation License Application](images/license_2.en.png)

- If you want to purchase **Official License** of KAP Plus or KAP, you need to provide **License Request File**. Click **Help -> About KAP** in KAP Plus or KAP.   


![Official License Application](images/license_3.en.png)

   And then click **Generate License Request File**. You will get the request file.

![Request License File](images/license_4.en.png)

### Load License File

After receiving the LICENSE file (Evaluation License or Official License) and installing KAP or KAP Plus, you need to load the LICENSE file to make KAP or KAP Plus effective. To load the file, do the following:

In KAP login page, click **Help -> Upload License**, you will see **Upload License** Window. Click **Browse** and locate the place which you save the LICENSE file. And then click **Open -> Submit** to upload it to KAP. 

![Upload License File](images/license_5.en.png)

In addition, you may also copy it to KAP's install directory to make KAP effective. We assume you downloaded the LICENSE file to Downloads folder and installed KAP under the directory of ${KYLIN_HOME}:

```
scp Downloads/LICENSE root@sandbox:/${KYLIN_HOME}
```

