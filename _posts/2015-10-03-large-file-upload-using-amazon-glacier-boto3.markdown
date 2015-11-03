---
layout: post
title: "Backup large files to Amazon glacier using boto3"
date: 2015-10-03 07:00:00
tags: glacier boto3 python amazon multipart_upload
published: true
---

Amazon glacier gives us a cheap way to do backups. For each uploaded archive glacier gives us an archive id which we should save somewhere. This archive id is required to retrieve the file backup from glacier. Amazon docs recommends to keep track of these ids ourselves. I used python `shelve` to keep the list of archive ids returned by glacier and its file descriptions.

{% highlight python %}

# I am uploading as chunks of 32mb
CHUNK_SIZE = 1048576 * 32 
AWS_ACCESS_KEY_ID = "Your access key id"
AWS_SECRET_ACCESS_KEY = "Your secret access key"

def upload_large_file(vault_name, region_name, filepath, description):
    session = session(aws_access_key_id=AWS_ACCESS_KEY_ID, aws_secret_access_key=AWS_SECRET_ACCESS_KEY, region_name=region_name)
    glacier = session.resource("glacier")
    vault = glacier.Vault(account_id="-", name=vault_name)

    multipart_upload = self.vault.initiate_multipart_upload(accountId="-", archiveDescription=description, partSize=str(CHUNK_SIZE))
    upload_id = multipart_upload.id

    f = open(filepath)
    start_range = 0
    for chunk in read_in_chunks(f, CHUNK_SIZE):
        range_data = "bytes %s-%s/*" % (start_range, f.tell()-1)
        print("Uploading range %s" % range_data)
        multipart_upload.upload_part(range=range_data, body=chunk)
        start_range = f.tell()

    f.seek(0)
    response = multipart_upload.complete(archiveSize=str(start_range),
                                         checksum=calculate_tree_hash(f))
    f.close()
    archive_id = response.get('archiveId')
    return archive_id



def read_in_chunks(file_obj, chunk_size):
    """ Reads the given file as chunks, instead of loading everything into memory."""
    while True:
        data = file_obj.read(chunk_size)
        if not data:
            break
        yield data
{% endhighlight %}

Now you can upload a file into a vault named "BackupVault" in the region "us-west-2" like this.

{% highlight python %}
archive_id = upload_large_file("BackupVault, "us-west-2", "/home/ragsagar/largeFile.zip", "largeFile.zip")
{% endhighlight %}

This returned archive id can be saved in shelve.

{% highlight python %}
import shelve

description = "largeFile.zip"
archive_id = upload_large_file("BackupVault, "us-west-2", "/home/ragsagar/largeFile.zip", description)
db = shelve.open("/home/ragsagar/glacier.db")
db[description] = archive_id
db.close()
{% endhighlight %}

