## 工具类

```java
@Data
@AllArgsConstructor
@Slf4j
public class AliOssUtil {

    private String endpoint;
    private String accessKeyId;
    private String accessKeySecret;
    private String bucketName;

    /**
     * 文件上传
     *
     * @param bytes
     * @param objectName
     * @return
     */
    public String upload(byte[] bytes, String objectName) {

        // 创建OSSClient实例。
        OSS ossClient = new OSSClientBuilder().build(endpoint, accessKeyId, accessKeySecret);
        try {
            // 创建PutObject请求。
            ossClient.putObject(bucketName, objectName, new ByteArrayInputStream(bytes));
        } catch (OSSException oe) {
            System.out.println("Caught an OSSException, which means your request made it to OSS, "
                    + "but was rejected with an error response for some reason.");
            System.out.println("Error Message:" + oe.getErrorMessage());
            System.out.println("Error Code:" + oe.getErrorCode());
            System.out.println("Request ID:" + oe.getRequestId());
            System.out.println("Host ID:" + oe.getHostId());
        } catch (ClientException ce) {
            System.out.println("Caught an ClientException, which means the client encountered "
                    + "a serious internal problem while trying to communicate with OSS, "
                    + "such as not being able to access the network.");
            System.out.println("Error Message:" + ce.getMessage());
        } finally {
            if (ossClient != null) {
                ossClient.shutdown();
            }
        }

        //文件访问路径规则 https://BucketName.Endpoint/ObjectName
        StringBuilder stringBuilder = new StringBuilder("https://");
        stringBuilder
                .append(bucketName)
                .append(".")
                .append(endpoint)
                .append("/")
                .append(objectName);

        log.info("文件上传到:{}", stringBuilder.toString());

        return stringBuilder.toString();
    }
}
```

## 配置类

```java
@Configuration
@Slf4j
public class OssConfig {

    @Bean
    @ConditionalOnMissingBean // 在没有这个都对象的时候才会创建
    public AliOssUtil aliOssUtil(AliOssProperties aliOssProperties){
        log.info("项目启动");
        return new AliOssUtil(aliOssProperties.getEndpoint(),aliOssProperties.getAccessKeyId(),aliOssProperties.getAccessKeySecret(),aliOssProperties.getBucketName());
    }
}
```

## 读取配置文件

```java
@Component
@ConfigurationProperties(prefix = "sky.alioss")
@Data
public class AliOssProperties {

    private String endpoint;
    private String accessKeyId;
    private String accessKeySecret;
    private String bucketName;

}
```

## yaml配置

```yml
sky:
  alioss:
    endpoint: oss-cn-beijing.aliyuncs.com
    access-key-id: xxx
    access-key-secret: xxxx
    bucket-name: xxx
```

## 使用

```java
@RestController
@RequestMapping("/admin/common")
public class CommonCpntroller {
    @Autowired
    private AliOssUtil aliOssUtil;
    @PostMapping("/upload")
    public Result Upload(MultipartFile file){
        try {
            // 获取原始文件名
            String filename = file.getOriginalFilename();
            // 获取文件后缀
            String endname = filename.substring(filename.lastIndexOf("."));
            String newfilename = UUID.randomUUID().toString() + endname;
            // 调取上传方法
            String upload = aliOssUtil.upload(file.getBytes(), newfilename);
            return Result.success(upload);
        } catch (IOException e) {
            return Result.error(MessageConstant.UPLOAD_FAILED);
        }
    }
}
```