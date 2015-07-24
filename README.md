
### Install and Configure

#### Prerequisites 

- Sign up for Amazon's programmatic billing access [here](http://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/detailed-billing-reports.html) to receive detailed billing(hourly) reports. Verify you receive monthly billing file in the following format: <accountid>-aws-billing-detailed-line-items-<year>-<month>.csv.zip.
- [Docker](https://docs.docker.com/installation/) and [Docker Compose](https://docs.docker.com/compose/install/) installed.

##### 1. ELB Setup

- Create an Amazon ELB with the following listeners for HTTPS authentication
      ```
      LB Protocol   LB Port   Instance Protocol   Instance Port   Cipher   SSL Certificate
      HTTP          80        HTTP                80              N/A        N/A
      HTTPS         443       HTTP                80              N/A        your-ssl-cert
      ```

##### 2. Docker Setup

- Open docker-compose.yml add the AWS Access Key ID and Secret Key 
- `vi docker-compose.yml`
      ```
      ice:
        build: ice
        command: |
          -Djava.net.preferIPv4Stack=true
          -Djava.net.preferIPv4Addresses
          -Dice.s3AccessKeyId=<s3AccessKeyId>
          -Dice.s3SecretKey=<s3SecretKeyId>
      ```

- Open ice.properties and configure a basic setup by updating the following 
- `vi ice/assets/ice.properties` 
      ```
      # s3 bucket name that detailed billing uses
      ice.billing_s3bucketname=
      
      # Your company name
      ice.companyName=
      
      # s3 bucket name for Ice output files (same s3 bucket is fine)
      ice.work_s3bucketname=
      
      # Your AWS account number. You can also replace "production" with your own identifier 
      ice.account.production=
      ```

