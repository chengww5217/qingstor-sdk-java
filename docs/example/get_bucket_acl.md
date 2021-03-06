## GET Bucket ACL

Initialize the Bucket service with accesskeyid and secretaccesskey

``` java
EnvContext env = new EnvContext("ACCESS_KEY_ID_EXAMPLE", "SECRET_ACCESS_KEY_EXAMPLE");
String zoneName = "pek3a";
String bucketName = "testBucketName";
Bucket bucket = new Bucket(env, zoneKey, bucketName);
```

Objects in above codes：
- bucket: An Object to operate Bucket. You can use all of the API with level Bucket and Object with the object.


After created the object, we need perform the action to get Bucket ACL：

```java
    private void getBucketACL(Bucket bucket) {
        try {
            Bucket.GetBucketACLOutput output = bucket.getACL();
            if (output.getStatueCode() == 200) {
                // Success
                Types.OwnerModel owner = output.getOwner();
                if (owner != null) {
                    System.out.println("owner = {'name': " + owner.getName() + ", 'ID': " + owner.getID() + "}");
                } else {
                    System.out.println("owner = null");
                }
                System.out.println("=======Get Bucket ACL======");
                List<Types.ACLModel> acls = output.getACL();
                if (acls != null && acls.size() > 0) {
                    System.out.println("ACLs = " + new Gson().toJson(acls));
                } else {
                    System.out.println("ACLs is empty.");
                }
                System.out.println("=============");
            } else {
                // Failed
                System.out.println("Failed to Get Bucket ACL.");
                System.out.println("StatueCode = " + output.getStatueCode());
                System.out.println("Message = " + output.getMessage());
                System.out.println("RequestId = " + output.getRequestId());
                System.out.println("Code = " + output.getCode());
                System.out.println("Url = " + output.getUrl());
            }
        } catch (QSException e) {
            e.printStackTrace();
        }
    }
```
