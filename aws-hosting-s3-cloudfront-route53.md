1. get domain
2. create hosted zone in route53
3. point domain nameservers at route53
4. verify that it worked (dig)
```
dig NS my.domain
```

5. create s3 bucket
6. create ACM certificate
7. create CloudFront Distribution pointing at S3 bucket
8. [point route53 at CloudFront](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-to-cloudfront-distribution.html) (e.g. with A and AAAA records for CloudFront)
9. upload index.html to S3 bucket
10. try in web browser, debug as needed
