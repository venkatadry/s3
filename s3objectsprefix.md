S3 lifecycle rules only support prefixes, not suffixes like .txt. So you cannot directly target .txt files using lifecycle rules unless those files share a common prefix in their names or folder paths.
S3 prefix only matches the beginning of object keys, not the end (like .txt). So you can't use .txt as a prefix to target all text files
S3 doesn't support wildcards like * in prefixes
Then setting the prefix as "dependency" in your lifecycle rule is absolutely correct. It will match:
dependency_links.txt
dependencyXYZ.csv
dependency/anything.txt



1.user test-user with policy
```{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:ListBucket",
                "s3:ListAllMyBuckets"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
```

I have bucket s3://xyzkvp
with .txt and .html files

Bucket Policy
```{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "ListObjectsInBucket",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::920373005946:user/test-user"
            },
            "Action": "s3:ListBucket",
            "Resource": "arn:aws:s3:::xyzkvp"
        },
        {
            "Sid": "AllObjectActions",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::920373005946:user/test-user"
            },
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::xyzkvp/*.html"
        }
    ]
}
```

Now the test-user with attached Policy can only list the buckets
with the bucket policy test-user was able to access only .html files and the .txt files is throwing error "Access Denied"
Happy i acheived what i want
