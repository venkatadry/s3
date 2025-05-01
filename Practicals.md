I have a user test-user .no polices are attached to the user.

I have the following bucket policy applied to the bucket. My expectation is test-user should be able to see the cucket and see the objects.but user says access is denied and not able to see the bucket too
```
    {
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
            "Action": [
                "s3:GetObject",
                "s3:PutObject",
                "s3:DeleteObject",
                "s3:GetObjectAcl",
                "s3:PutObjectAcl"
            ],
            "Resource": "arn:aws:s3:::xyzkvp/*"
        }
    ]
}```


The test-user  was now added s3-readonly- access
 It worked now. SO, Bucket policy cannot give anything beyond its bucket scope.
For the bucket policy to work IAM user should have policy attached to list the buckets so once the user able to list the buckets then the bucket policy is applied on the specific bucket or objects.
