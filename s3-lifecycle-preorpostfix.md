
https://stackoverflow.com/questions/28437887/s3-lifecycle-rule-with-suffix
https://docs.aws.amazon.com/AmazonS3/latest/userguide/lifecycle-configuration-examples.html
https://docs.aws.amazon.com/AmazonS3/latest/userguide/how-to-set-lifecycle-configuration-intro.html
https://docs.aws.amazon.com/AmazonS3/latest/userguide/troubleshoot-lifecycle.html


I have a bunch of files in an S3 bucket. I'd like to create a rule to delete all of the files that end in .pdf after 1 day.

Can I do this with S3 lifecycle rules?

Because I tried *.pdf delete after 1 day, and that didn't work.

I also tried something like copy_* delete after 1 day and that didn't work either.


This isn't a direct answer to the question. As you noticed, suffix-based rules aren't supported. However, you can use tags.
You do need to tag your objects as you upload them, and you can do that regardless of your upload method (CLI or console). You can enable tagging for existing objects, as well. Again, either through console or CLI (http://docs.aws.amazon.com/cli/latest/reference/s3api/put-object-tagging.html).

Once tagging is done, make a lifecycle rule that's only applicable to objects associated with that tag.

Tags are replicated (http://docs.aws.amazon.com/AmazonS3/latest/dev/crr-what-is-isnot-replicated.html). So if you have replication enabled, this setup works in destination, as well.
