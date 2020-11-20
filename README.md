# amazon-SDK
亚马逊api java sdk
由杨超辉制作。本人只是上传。
  /**
     * 构建授权参数
     */
    public ApiClient buildApiClient(String clientId, String clientSecret, String refreshToken, String region, String endpoint){
        String authEndpoint = "https://api.amazon.com/auth/o2/token";
        AWSAuthenticationCredentials awsAuthenticationCredentials = AWSAuthenticationCredentials.builder()
                .accessKeyId(accessKey)
                .secretKey(secretKey)
                .region(region)
                .build();
        AWSAuthenticationCredentialsProvider awsAuthenticationCredentialsProvider = AWSAuthenticationCredentialsProvider.builder()
                .roleArn(roleArn)
                .roleSessionName(roleSessionName)
                .build();
        //需要授权的操作
        LWAAuthorizationCredentials lwaAuthorizationCredentials =
                LWAAuthorizationCredentials.builder()
                        .clientId(clientId)
                        .clientSecret(clientSecret)
                        .refreshToken(refreshToken)
                        .endpoint(authEndpoint)
                        .build();
        LWAAuthorizationSigner lwaAuthorizationSigner = new LWAAuthorizationSigner(lwaAuthorizationCredentials);
        AWSSigV4Signer awsSigV4Signer;
        if ( awsAuthenticationCredentialsProvider == null) {
            awsSigV4Signer = new AWSSigV4Signer(awsAuthenticationCredentials);
        }
        else {
            awsSigV4Signer = new AWSSigV4Signer(awsAuthenticationCredentials,awsAuthenticationCredentialsProvider);
        }
        ApiClient apiClient = new ApiClient();
        apiClient.setAWSSigV4Signer(awsSigV4Signer)
                .setLWAAuthorizationSigner(lwaAuthorizationSigner)
                .setBasePath(endpoint);
        return apiClient;
    }
