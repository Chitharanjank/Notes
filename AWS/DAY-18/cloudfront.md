### Amazon CloudFront 
Amazon CloudFront is a Content Delivery Network (CDN) service that speeds up the delivery of your website content by caching it at multiple edge locations worldwide. It reduces latency and improves the performance of serving static and dynamic content.

When hosting a static website in an Amazon S3 bucket, the simplest approach is to make the bucket public. However, this poses security risks. A better approach is to keep the S3 bucket private and use CloudFront with an Origin Access Control (OAC) or Origin Access Identity (OAI) to securely serve the content.

### Hosting a Private Static Website using S3 and CloudFront (OAI)

#### Step 1: Create an S3 Bucket & Upload Website Files
1. Go to **AWS S3 Console** → Create a new **S3 bucket**.
2. **Disable public access** to the bucket.
3. Upload your **static website files** (HTML, CSS, JavaScript, images, etc.).

#### Step 2: Configure Bucket Policy for CloudFront (Using OAI)
1. **Go to CloudFront**, create a new **distribution**.
2. Set **S3 bucket** as the origin.
3. Create a new **Origin Access Identity (OAI)** in CloudFront.
4. Attach the following **S3 bucket policy** to grant CloudFront access:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::cloudfront:user/CloudFront Origin Access Identity your-OAI-ID"
      },
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::your-bucket-name/*"
    }
  ]
}
```

#### Step 3: Configure CloudFront Distribution
1. In CloudFront, set **Default Root Object** to `index.html`.
2. Enable **HTTPS** (recommended).
3. Set up a **custom domain (optional)** and add an **SSL certificate** from AWS Certificate Manager.
4. **Deploy the distribution**.

#### Step 4: Access Your Website
- The website will now be accessible through the **CloudFront URL** (e.g., `https://dxxxxx.cloudfront.net`).
- You can also **map a custom domain** (e.g., `www.example.com`) using **Route 53**.
