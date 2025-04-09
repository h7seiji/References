# Cloudfront

## How Caching Works

The caching process follows these steps:

1. A user makes the first request for content
2. CloudFront retrieves the content from your origin server
3. The content is cached at the nearest edge location
4. Subsequent requests from nearby users are served directly from the cache

## Origin

An Origin in AWS is the source server or storage location that contains the original files you want to distribute through Amazon CloudFront CDN.
Think of it as the primary location where your content lives before being cached across different geographical locations.

- Origins store your original content (images, videos, files, etc.)
- CloudFront CDN retrieves content from these origins
- Content is then cached at edge locations closer to users aws.amazon.com

### Types of Origins

- Amazon S3 buckets
- MediaStore containers
- Application Load Balancers
- Lambda function URLs
- EC2 instances
- Custom origins
