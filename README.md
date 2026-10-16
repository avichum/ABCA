# ABCA

A static "Hello, World!" page — no frameworks, no build step, no CDN dependencies.

To view it, open `index.html` in a browser (e.g. double-click the file, or run `open index.html` on macOS / `xdg-open index.html` on Linux).

## Deploy to AWS

`infra/cloudformation.yaml` provisions the hosting for this site: a private,
encrypted S3 bucket fronted by a CloudFront distribution that reads it through
an origin access control (so the bucket itself stays non-public and the site is
served over HTTPS).

Requires the [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
with credentials that can create S3 and CloudFront resources.

1. Create (or update) the stack:

   ```sh
   aws cloudformation deploy \
     --template-file infra/cloudformation.yaml \
     --stack-name abca-site \
     --parameter-overrides ProjectName=abca
   ```

   The first deploy takes a few minutes while the distribution rolls out.

2. Read the stack outputs:

   ```sh
   aws cloudformation describe-stacks \
     --stack-name abca-site \
     --query 'Stacks[0].Outputs' \
     --output table
   ```

3. Upload the site files to the bucket from the `SiteBucketName` output:

   ```sh
   aws s3 cp index.html "s3://<SiteBucketName>/index.html"
   aws s3 cp style.css "s3://<SiteBucketName>/style.css"
   ```

4. After re-uploading, invalidate the CloudFront cache using the
   `DistributionId` output:

   ```sh
   aws cloudfront create-invalidation --distribution-id <DistributionId> --paths '/*'
   ```

The site is then available at the `SiteUrl` output
(`https://<distribution>.cloudfront.net`). To use a custom domain instead, add
`Aliases` plus an ACM certificate (issued in `us-east-1`) to the distribution's
`ViewerCertificate`.

### Parameters

| Parameter | Default | Purpose |
| --- | --- | --- |
| `ProjectName` | `abca` | Prefix for the bucket name and CloudFront comment. |
| `IndexDocument` | `index.html` | Object served at the distribution root. |
| `PriceClass` | `PriceClass_100` | CloudFront edge locations (`PriceClass_100`, `PriceClass_200` or `PriceClass_All`). |

The bucket uses `DeletionPolicy: Retain`, so deleting the stack leaves the
uploaded files in place; remove the bucket manually if you no longer need it.

### Validating the template

```sh
aws cloudformation validate-template --template-body file://infra/cloudformation.yaml
# or, without AWS credentials:
pip install cfn-lint && cfn-lint infra/cloudformation.yaml
```
