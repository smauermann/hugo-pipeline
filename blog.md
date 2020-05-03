- we use cloudformation
  - why? reproducible and easy cleanup
- start with s3 bucket containing website files:

```yaml
Resources:
  WebsiteBucket:
    Type: AWS::S3::Bucket
    Properties:
      AccessControl: PublicRead
      BucketName: hugo-website-bucket
      WebsiteConfiguration:
        IndexDocument: index.html
        ErrorDocument: error.html
    DeletionPolicy: Retain
Outputs:
  WebsiteURL:
    Value: !GetAtt [WebsiteBucket, WebsiteURL]
    Description: URL for website hosted on S3
  S3BucketSecureURL:
    Value: !Join ["", ["https://", !GetAtt [WebsiteBucket, DomainName]]]
    Description: Name of S3 bucket to hold website conten
```
