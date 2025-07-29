# cloudfront-webapp

1. Bucket name:  `my-webapp-bucket`

2. Uncheck  “Block all public access”

3. Upload your index.html

```
<html>
<head>
  <title>Simple Demo WebApp</title>
</head>
<body>
  <h1>Welcome to My Demo WebApp</h1>
</body>
</html>
```


4. Bucket Policy

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::my-webapp-bucket/*"
    }
  ]
}
```


5. Enable Static Website Hosting on S3 , Index document: index.html

6. Test this in a browser. 


7. Create Distribution

  - Origin domain: Select your S3 bucket

  - Default root object: index.html

  - Choose: "Origin access control (OAC)"

  - Click Create control setting

  - Policy: "Public" or "Read-only"

  - Viewer protocol policy: Redirect HTTP to HTTPS



8. use policy

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowCloudFrontServicePrincipalRead",
      "Effect": "Allow",
      "Principal": {
        "Service": "cloudfront.amazonaws.com"
      },
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::my-webapp-bucket/*",
      "Condition": {
        "StringEquals": {
          "AWS:SourceArn": "arn:aws:cloudfront::YOUR_ACCOUNT_ID:distribution/YOUR_DISTRIBUTION_ID"
        }
      }
    }
  ]
}
```

9. Access


