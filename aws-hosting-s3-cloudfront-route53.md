1. get domain
2. create hosted zone in route53
3. point domain nameservers at route53
4. create s3 bucket
5. create ACM certificate (e.g. verify domain ownership via CNAME records)
6. create CloudFront Distribution pointing at S3 bucket
7. [point route53 at CloudFront](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-to-cloudfront-distribution.html) (e.g. with A and AAAA records for CloudFront)
8. upload index.html to S3 bucket
9. try in web browser, debug as needed
