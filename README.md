# minio-multiuser

A bash script that creates and drops users and policies.

# Why?

A default installation of MinIO gives you one root user and password to manage all buckets. Creating users manually is a tiring process, so I built this script that will create and remove users and policies at once.

# Usage

```
liam@server ~ # mcm.sh -r liam -a create -b test-bucket
Bucket created successfully `liam/test-bucket`.
Added user `DFZCO26PV1ECQBD2` successfully.
Added policy `DFZCO26PV1ECQBD2-test-bucket-rw-20210408053955` successfully.
Policy `DFZCO26PV1ECQBD2-test-bucket-rw-20210408053955` is set on user `DFZCO26PV1ECQBD2`
Bucket test-bucket assigned to DFZCO26PV1ECQBD2 with password WCKLXXMW7YA7PE6DB56BZHCIMFYKR0E9.

liam@server ~ # mcm.sh -r liam -a drop -u DFZCO26PV1ECQBD2
Removed policy `DFZCO26PV1ECQBD2-test-bucket-rw-20210408053955` successfully.
Removed user `DFZCO26PV1ECQBD2` successfully.
User and policy deleted. Bucket retained. To remove, run /usr/bin/mc rb <remote>/<bucket-name>.
```

Edit the script to reflect your actual `mc` command (the value of the `MINIO` variable). This could be a path to the `mc` binary (by default) or a Docker command. Then, give it execute permissions: `chmod +x mcm.sh`

To create a user, bucket and policy all in one go, run `mcm.sh -r <remote> -a create -b <bucket name>`. If a bucket already exists, it'll silently fail to create the bucket but will still assign access to the user that will be created.

To specify your own username and password, simply append `-u <username>` and `-p <password>` to the command. Usernames and passwords are randomly generated if ommitted from the command.

To drop a user and policy all in one go, run `mcm.sh -r <remote> -a drop -u <username>`. This does **NOT** drop a bucket by default.

# License

This script is licensed under the MIT Open Source License.
