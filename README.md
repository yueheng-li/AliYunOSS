# AliYunOSS 对Aliyun 的OSS上传文件
## Ali云账号做成，申请OSS服务
## 创建Bucket
## 创建AccessKey
* Access Key ID
* Access Key Secret
## maven依赖的添加
``` java
		<dependency>
			<groupId>com.aliyun.oss</groupId>
			<artifactId>aliyun-sdk-oss</artifactId>
			<version>2.7.0</version>
		</dependency>
```

## 添加上传代码
``` java
		public class SimpleGetObjectSample {
    
    private static String endpoint = "OSS的公网域名";
    private static String accessKeyId = "申请的Access Key ID";
    private static String accessKeySecret = "申请的Access Key Secret";
    
    private static String bucketName = "创建的bucket的名称";
    private static String key = "上传之后的名称";
    
    public static void main(String[] args) throws IOException {
        /*
         * Constructs a client instance with your account for accessing OSS
         */
        OSSClient client = new OSSClient(endpoint, accessKeyId, accessKeySecret);
        
        try {
            
            /**
             * Note that there are two ways of uploading an object to your bucket, the one 
             * by specifying an input stream as content source, the other by specifying a file.
             */
            
            /*
             * Upload an object to your bucket from an input stream
             */
            InputStream inputStream = new FileInputStream(new File("C:\\Users\\xxxx\\Pictures\\1-3.PNG"));
            client.putObject(bucketName, key, inputStream);
           
            
        } catch (OSSException oe) {
            System.out.println("Caught an OSSException, which means your request made it to OSS, "
                    + "but was rejected with an error response for some reason.");
            System.out.println("Error Message: " + oe.getErrorCode());
            System.out.println("Error Code:       " + oe.getErrorCode());
            System.out.println("Request ID:      " + oe.getRequestId());
            System.out.println("Host ID:           " + oe.getHostId());
        } catch (ClientException ce) {
            System.out.println("Caught an ClientException, which means the client encountered "
                    + "a serious internal problem while trying to communicate with OSS, "
                    + "such as not being able to access the network.");
            System.out.println("Error Message: " + ce.getMessage());
        } finally {
            /*
             * Do not forget to shut down the client finally to release all allocated resources.
             */
            client.shutdown();
        }
    }
```
